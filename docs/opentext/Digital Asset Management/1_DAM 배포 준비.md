---
title: INFRA 작업
---

# DAM 배포 준비

🧱 전체 구성 개요

---

> 최소 2대로 구성하지만, 리소스에 따라 더 많은 노드를 구성할 수 있습니다.
> 

---

## 🧾 1단계: VM 생성 (ESXi)

### 🔧 사양 권장

- CPU: 최소 4 vCPU
- RAM: 8GB 이상 (Master), 16GB 이상 (Worker)
- Disk: 100GB 이상
- NIC: 브리지 네트워크 또는 내부 NAT 가능

### 📌 설치할 OS

- **Ubuntu Serve r 22.04 LTS** (설치 ISO 필요)

---

## 🧾 2단계: OS 설치 및 초기 설정

각 VM에 다음과 같이 설정합니다.
[https://velog.io/@pennori/Ubuntu-22.04-쿠버네티스-1.29-설치](https://velog.io/@pennori/Ubuntu-22.04-%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-1.29-%EC%84%A4%EC%B9%98) 와 비교

```bash
# 방화벽 해제
sudo ufw disable
#sudo로 로그인
sudo apt update && sudo apt upgrade -y

# 호스트명 설정 (각 노드에 다르게)
sudo hostnamectl set-hostname k8s-master   # 또는 k8s-worker
```

---

## 🧾 3단계: Docker 설치

```bash
sudo -i
# docker 패키지 설치
apt install -y docker.io
docker ps # docker 상태 확인
docker version # docker 버전 확인
# docker 서비스 등록 및 실행
sudo systemctl enable docker
sudo systemctl start docker

```

## 🧾 4단계: **쿠버네티스 클러스 구성**

```bash
sudo -i
# Swap 비활성화 (모든 노드)
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab
# IP Forwarding 기능 활성화 (트래픽 관리 효율 제고 목적)
echo '1' > /proc/sys/net/ipv4/ip_forward    # 실행시 1 반환 확인
cat /proc/sys/net/ipv4/ip_forward 
# 컨테이너 런타임 환경 구성 - containerd 활용
cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
# 커널에 생성한 모듈을 등록하여 사용가능하도록 설정
modprobe overlay
modprobe br_netfilter
#노드간 통신을 위한 iptables bridge 설정 추가
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

# 재부팅 후에도 값이 유지
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

# 재부팅하지 않고 sysctl 파라미터 적용
sudo sysctl --system
# 컨테이너 런타임 환경 구성 - containerd 환경 설정
mkdir /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
# 컨테이너 런타임 환경 구성 - cgroup 설정
vi /etc/containerd/config.toml   # line 1에 있는 disabled_plugins = [] 확인, 값이 없어야 함
<<내용 수정 시작>>
          [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
            BinaryName = ""
            CriuImagePath = ""
            CriuPath = ""
            CriuWorkPath = ""
            IoGid = 0
            IoUid = 0
            NoNewKeyring = false
            NoPivotRoot = false
            Root = ""
            ShimCgroup = ""
            SystemdCgroup = true
..
<<내용 수정 끝>>
sudo service containerd restart
systemctl status containerd
# 컨테이너 런타임 환경 구성 - docker daemon 설정
vi /etc/docker/daemon.json # 새 파일 생성
# 아래 내용 붙여넣기
...
{
"exec-opts": ["native.cgroupdriver=systemd"],
"log-driver": "json-file",
"log-opts": {
"max-size": "100m"
},
"storage-driver": "overlay2"
}
...

mkdir -p /etc/systemd/system/docker.service.d
usermod -aG docker ecmadmin #sudo 없이 사용
systemctl daemon-reload
systemctl restart kubelet
systemctl enable docker
systemctl restart docker
systemctl status docker  # Active 상태 확인 
systemctl restart containerd.service
systemctl status containerd.service

#도커 버전 확인
docker version

#도커의 cgroup 드라이버가 systemd 변경 확인
docker info

```

## 🧾 5단계: Kubernetes 설치 (`kubeadm`, `kubelet`, `kubectl`)

```bash
# 패키지 업데이트
apt-get update

apt-get install -y apt-transport-https ca-certificates curl gpg

# 패키지 레파지토리에 대한 공개키 다운로드
# `/etc/apt/keyrings` 해당 디렉토리가 없을 경우 먼저 생성 해야 함.
mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# 키 정보와 레파지토리 URL 지정
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

# 패키지 업데이트 후 다운로드 
apt-get update
apt-get install -y kubelet kubeadm kubectl

# 자동 업데이트 방지
sudo apt-mark hold kubelet kubeadm kubectl

# 버전 확인
kubeadm version
kubectl version
kubelet --version

# 자동 시작 등록
systemctl daemon-reload
systemctl restart kubelet.service
systemctl enable --now kubelet.service
```

---

## 🧾 5단계: Kubernetes 클러스터 복사 (**worker** 노드)

```bash
vm 복사
sudo hostnamectl set-hostname k8s-worker

```

## 🧾 6단계: Kubernetes 클러스터 초기화 (Master 노드)

### 🔸 컨테이너 런타임: `containerd` 설정

Ubuntu 22.04부터는 containerd가 기본입니다. `kubeadm`은 containerd와 호환됩니다.

### 🔸 클러스터 초기화

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
kubeadm join 192.168.137.131:6443 --token 8g60x8.dx9t64rlmvyun1ww \
        --discovery-token-ca-cert-hash sha256:732cfacddea0e6b32213295cc36677a7fd3ea84a0ab266bdb6fc8f245fa20cae

 
실패시        
sudo kubeadm reset -f
sudo systemctl stop kubelet
sudo docker system prune -a --volumes -f  # 또는 containerd 사용 시 컨테이너 삭제

sudo rm -rf /etc/kubernetes
sudo rm -rf /var/lib/etcd
sudo rm -rf ~/.kube

다시시도
sudo systemctl daemon-reexec
sudo systemctl restart kubelet
sudo kubeadm reset -f
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

> CIDR은 Flannel 네트워크 플러그인 기준입니다.
> 

### 🔸 일반 사용자에게 `kubectl` 권한 부여

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

export KUBECONFIG=$HOME/.kube/config

```

### 🔸 클러스터 상태 확인 (잠시 기다린 후)

```bash
kubectl get nodes
kubectl get pods -n kube-system

```

---

## 🧾 7단계: 네트워크 플러그인 설치 (예: Flannel)

```bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
확인
kubectl get pods -n kube-system
kubectl get nodes

```

---

## 🧾 8단계: Worker 노드 조인

Master 노드 초기화 결과로 나온 **join 명령어**를 복사하여 Worker 노드에서 실행:

```bash
sudo kubeadm join <MASTER_IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>

sudo kubeadm join 192.168.137.131:6443 --token 8g60x8.dx9t64rlmvyun1ww \
        --discovery-token-ca-cert-hash sha256:732cfacddea0e6b32213295cc36677a7fd3ea84a0ab266bdb6fc8f245fa20cae

```

---

## 🧾 9단계: 클러스터 확인 (Master 노드에서)

```bash
kubectl get nodes

```

> 두 노드가 Ready 상태여야 합니다.
> 

---

## 🧾 10단계: Helm 설치 (모든 노드)

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

```

---

## ✅ 이후 단계: OpenText DAM 배포 준비

이제 클러스터가 구성되었으므로 다음을 수행해야 합니다:

- Ingress Controller (NGINX 등) 설치
- StorageClass 설정 (RWX 필요)
- OpenText Container Registry 로그인 및 Docker 이미지 pull
- PostgreSQL 설치 (또는 외부 DB 연결)
- DAM용 Helm Chart 및 values.yaml 구성

---

---

[Ingress Controller (NGINX 등) 설치](Ingress%20Controller%20(NGINX%20%EB%93%B1)%20%EC%84%A4%EC%B9%98%201f37aa6ede2380fb8539c110bfe4a03e.md)

[StorageClass 설정 (RWX 필요)](../../Database/PostgreSQL/PostgreSQL 설치 또는 외부 DB 연결.md)

[OpenText Container Registry 로그인 및 Docker 이미지 pull](OpenText%20Container%20Registry%20%EB%A1%9C%EA%B7%B8%EC%9D%B8%20%EB%B0%8F%20Docker%20%EC%9D%B4%EB%AF%B8%EC%A7%80%20pull%201f37aa6ede238079b1dbfb0408bdc72c.md)

[PostgreSQL 설치 (또는 외부 DB 연결)](PostgreSQL%20%EC%84%A4%EC%B9%98%20(%EB%98%90%EB%8A%94%20%EC%99%B8%EB%B6%80%20DB%20%EC%97%B0%EA%B2%B0)%201f37aa6ede2380608c2ee436b6d504cf.md)

[DAM용 Helm Chart 및 values.yaml 구성- -](DAM%EC%9A%A9%20Helm%20Chart%20%EB%B0%8F%20values%20yaml%20%EA%B5%AC%EC%84%B1-%20-%201f37aa6ede238069bf34f37117309d65.md)