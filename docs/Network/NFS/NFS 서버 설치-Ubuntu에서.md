# NFS 서버 설치 (Ubuntu에서)

sudo apt update
sudo apt install -y nfs-kernel-server

sudo mkdir -p /srv/nfs/otmm_disk1

sudo chown nobody:nogroup /srv/nfs/otmm_disk1
sudo chmod 777 /srv/nfs/otmm_disk1

echo "/srv/nfs/otmm_disk1 *(rw,sync,no_subtree_check,no_root_squash)" | sudo tee -a /etc/exports

sudo exportfs -ra

sudo systemctl restart nfs-kernel-server

# (선택) 전용 디스크를 /srv/nfs/otmm_disk1에 마운트

# 파티션 및 포맷

sudo parted /dev/sdb -- mklabel gpt
sudo parted /dev/sdb -- mkpart primary ext4 0% 100%
sudo mkfs.ext4 /dev/sdb1

# 마운트 위치 준비 및 마운트

sudo mount /dev/sdb1 /srv/nfs/otmm_disk1

# 재부팅 시 자동 마운트

echo "/dev/sdb1 /srv/nfs/otmm_disk1 ext4 defaults 0 2" | sudo tee -a /etc/fstab