# 인증서 (self-signed) 적용

```jsx
1단계: 루트 CA 키 및 인증서 생성
# 1. 루트 CA 개인 키 생성
openssl genrsa -out rootCA.key 4096
# 2. 루트 CA 인증서 생성 (유효기간 10년, 자체 서명)
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 3650 -out rootCA.crt \
-subj "/C=KR/ST=Seoul/L=Seoul/O=Penta System/OU=IT/CN=MyRootCA"
```

📜 1단계: OpenSSL 설정 파일(optional)

```jsx
#openssl.cnf
[ req ]
default_bits       = 2048
distinguished_name = req_distinguished_name
req_extensions     = req_ext
#x509_extensions    = v3_ca
prompt             = no

[ req_distinguished_name ]
C = KR
ST = Seoul
L = Seoul
O = Penta System
OU = IT
CN = dam-a.penta.co.kr

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = dam-a.penta.co.kr

```

🛠️ 2단계: 서버 인증서용 키 및 CSR 생성

```jsx
# 서버 키 생성
openssl genrsa -out tls.key 2048

# CSR 생성 (SAN을 포함하는 설정 파일 사용)
openssl req -new -key tls.key -out tls.csr -config openssl.cnf
```

🔏 3단계: 루트 CA로 서명 (인증서 발급)

```jsx
openssl x509 -req -in tls.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial \
-out tls.crt -days 365 -sha256 -extensions req_ext -extfile openssl.cnf

```

Secret tls 명 tls-secret 를 values.custom.yaml에 적용한다 

```bash
# Ingress Controller 설치 > TLS 인증서 생성 및 Secret 등록
kubectl create secret tls tls-secret \
  --cert=tls.crt --key=tls.key \
  -n otxf
  kubectl create secret tls tls-secret \
  --cert=tls.crt --key=tls.key \
  -n dam
  
  
  kubectl delete secret tls-secret -n otxf
  kubectl delete secret tls-secret -n dam
```

vi values.custom.yaml

```yaml
ingressSecret: &ingress_secret tls-secret
```

# 인증서 재 적용

Wildcard 인증서로 변경되었을때

### ✅ 1. secret 삭

---

```bash
kubectl delete secret tls-secret -n otxf
kubectl delete secret tls-secret -n dam
```

✅ 2 `tls.crt`와 `tls.key`로 만들기

```bash

cat STAR.penta.co.kr.crt chainca.crt > tls.crt

cp STAR.penta.co.kr.key tls.key

```

---

### ✅ 3. 기존 Secret 삭제 후 재생성

```bash
# 새 Secret 생성
kubectl create secret tls tls-secret --cert=tls.crt --key=tls.key -n otxf
kubectl create secret tls tls-secret --cert=tls.crt --key=tls.key -n dam
```

```bash
🧪 검증 팁
원하시면 다음 명령으로 추출한 파일이 정상인지 확인해볼 수 있습니다.

인증서 확인:
openssl x509 -in tls.crt -text -noout
개인 키 확인:
openssl rsa -in tls.key -check

```

---

### ✅ 4. Secret을 사용하는 Deployment/Ingress 재시작 (필요 시)

일부 Ingress Controller나 Deployment는 Secret 변경만으로 자동 반영되지 않으므로, 다음 중 하나를 하세요:

- Ingress Controller 재시작 (예: `nginx-ingress`, `traefik` 등)
- 관련 파드 수동 재시작:
    
    ```bash
    
    kubectl rollout restart deployment ingress-nginx-controller -n ingress-nginx
    
    ```
    

---

### ✅ 요약

1. `esxi_frontend.pem` 내용을 확인하고 `tls.crt`, `tls.key`로 분리
2. 기존 Secret 삭제
3. 새 Secret 생성
4. 반영을 위해 Ingress 또는 파드 재시작

필요하다면 `esxi_frontend.pem` 파일 내용을 분석해서 분리해드릴 수 있으니, 내용 일부를 (민감 정보 제외하고) 공유해주세요.

Wildcard 인증서로 변경되었고, 기존에 `tls.crt`, `tls.key`로 사용되던 파일 대신 `esxi_frontend.pem` 파일이 생겼다면, 이 PEM 파일의 구조에 따라 작업 방식이 달라집니다. 보통 wildcard 인증서는 다음과 같이 구성됩니다: