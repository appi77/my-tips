---
title: PostgreSQL 설치 또는 연결 with Docker
---
# PostgreSQL 설치 (또는 외부 DB 연결)

Ubuntu 22.04 LTS에서 PostgreSQL 14 설치 및 기본 설정 절차

---

### ✅ 1단계: PostgreSQL 공식 패키지 저장소 등록

```bash
sudo apt update
sudo apt install -y wget ca-certificates
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
echo "deb http://apt.postgresql.org/pub/repos/apt jammy-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list

```

---

### ✅ 2단계: PostgreSQL 14 설치

```bash
sudo apt update
sudo apt install -y postgresql-14

```

설치 후 PostgreSQL 서비스는 자동으로 시작됩니다.

---

### ✅ 3단계: 서비스 상태 확인 및 자동 실행 설정

```bash
sudo systemctl status postgresql
sudo systemctl enable postgresql

```

`active (running)` 상태인지 확인하세요.

---

### ✅ 4단계: postgres 사용자 비밀번호 설정

```bash
sudo -u postgres psql

```

PostgreSQL 셸에 진입한 후 다음 명령 실행:

```sql
\password postgres

```

비밀번호 입력 후:

```sql
\q

```

으로 종료합니다.

---

### ✅ 5단계: 외부 접속 허용 (선택)

### 1) PostgreSQL 설정 파일 수정

```bash
sudo nano /etc/postgresql/14/main/postgresql.conf

```

다음 항목을 찾아 수정:

```
listen_addresses = '*'

```

### 2) `pg_hba.conf` 수정

```bash
sudo nano /etc/postgresql/14/main/pg_hba.conf

```

외부 IP 허용을 위해 아래와 같이 추가:

```
host    all             all             0.0.0.0/0               md5

```

> 보안을 위해 실제 운영 환경에서는 IP 범위를 제한하세요.
> 

---

### ✅ 6단계: 방화벽 설정 (선택)

```bash
sudo ufw allow 5432/tcp
sudo ufw reload

```

---

### ✅ PostgreSQL 재시작

```bash
sudo systemctl restart postgresql

```

---

**DB 생성, 사용자 추가, DB 접속 방법**