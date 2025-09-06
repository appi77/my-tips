# 동적 NFS 프로비저너 설치

### ✅ 1단계: Helm 리포 추가 및 업데이트

```bash

helm repo add nfs-subdir-external-provisioner [https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/](https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/)
helm repo update
```

✅ 2단계: 동적 NFS 프로비저너 설치

```bash
kubectl delete storageclass otmm-nfs
helm uninstall nfs-provisioner -n kube-system

showmount -e 192.168.137.2
Export list for 192.168.137.2:
/esxi_disk1 (everyone)
/otmm_disk1 (everyone)
/dm_storage (everyone)

helm install nfs-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--set nfs.server=192.168.137.2 \
--set nfs.path=/otmm_disk1 \
--set storageClass.name=otmm-nfs \
--set storageClass.defaultClass=false \
--namespace kube-system

showmount -e 192.168.137.131
Export list for 192.168.137.131:
/srv/nfs/otmm_disk1 *

helm install nfs-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--set nfs.server=192.168.137.131 \
--set nfs.path=/srv/nfs/otmm_disk1 \
--set storageClass.name=otmm-nfs \
--set storageClass.defaultClass=false \
--namespace kube-system

```

참고:

nfs.server: NFS 서버의 IP (여기서는 192.168.137.131)

nfs.path: 전체 PV가 서브디렉터리로 생성될 NFS 상의 루트 경로

✅ 3단계: 정상 설치 확인

```bash

kubectl get pods -n kube-system -l app=nfs-subdir-external-provisioner
kubectl get pods -n kube-system -l release=nfs-provisioner
kubectl get sc
```

otmm-nfs 라는 StorageClass가 생겼는지

PROVISIONER는 cluster.local/...nfs-subdir-external-provisioner 형식

PVC는 이 StorageClass를 쓰면 자동으로 Bound 됨