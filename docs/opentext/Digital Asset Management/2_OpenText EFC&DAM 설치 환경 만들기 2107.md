---
title: EFC & DAM 설치 환경 만들기
---
# OpenText EFC & DAM 설치 환경 만들기

## **1단계. 시스템 준비**

```bash
sudo ufw disable
sudo hostnamectl set-hostname dam-a
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget gnupg lsb-release git
#OpenText DAM을 Kubernetes 위에 설치하는 경우에도 스왑을 끄는 것이 권장됩니다.
swapon --show
sudo swapoff -a
sudo nano /etc/fstab     # swap 관련 주석처리
```

---

## **2단계. Docker 설치**

```bash
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker damadmin

```

로그아웃 후 다시 로그인 (docker 권한 적용)

---

## **3단계. Kind 기반 Kubernetes 클러스터 구성**

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

```

```bash
Ingress Controller 설치 
1. 클러스터 재생성 (NodePort → 443/80 직접 바인딩)
로 대체

kubectl cluster-info --context kind-dam-cluster
sudo snap install kubectl --classic

```

---

## **4단계. Helm 설치**

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

```

---

## **5단계. PostgreSQL 설치 및 구성**

```bash
sudo apt install -y postgresql
sudo systemctl enable --now postgresql

```

```bash
sudo -u postgres psql
```

**PostgreSQL 초기 설정**

```bash
sudo -u postgres psql
ALTER USER postgres WITH PASSWORD 'Admin@2024';
\q
### sudo find / -name postgresql.conf 2>/dev/null
sudo vi /etc/postgresql/12/main/postgresql.conf
listen_addresses = '*'
### sudo find / -name pg_hba.conf 2>/dev/null
sudo vi /etc/postgresql/12/main/pg_hba.conf
host    all             all             192.168.137.131/32         md5
host    otds     otdsuser    172.18.0.0/16     md5
host    rma     rmauser    172.18.0.0/16     md5
host    expcloud     expclouduser   172.18.0.0/16     md5

✅ PostgreSQL에 **SSL 비활성화 허용 설정** 필요
```

> PostgreSQL을 내부 네트워크에서만 사용하고 있다면 ssl = off가 보안상 문제가 되지 않습니다.
> 

## PostgreSQL 서버 재시작

---

```bash
sudo systemctl restart postgresql
# 또는 docker 컨테이너 기반이면
docker restart <postgres-container>
```

[인증서 (self-signed) 적용](../../보안/1_SSL/인증서-self-signed 적용.md)
[NFS 서버 설치 (Ubuntu에서)](../../Network/NFS/NFS 서버 설치-Ubuntu.md)
[Windows 2022 Core NFS 설치](../../Network/NFS/Windows 2022 Core NFS 설치.md)
[동적 NFS 프로비저너 설치](../../Network/NFS/동적 NFS 프로비저너 설치.md)