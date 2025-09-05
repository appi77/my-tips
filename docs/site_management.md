---
title: VS Code + MkDocs + GitHub Pages 생성
---

# 🚀 VS Code + MkDocs + GitHub Pages 생성

## 1. 준비

#### 필수 설치:
    - Python (3.8 이상)
    - Git
    - VS Code

## 2. 로컬 MkDocs 프로젝트 생성

터미널(VS Code 내 터미널)에서:

```bash
# MkDocs 설치 (Material 테마 포함)
pip install mkdocs-material

# 프로젝트 생성
mkdocs new my-tips

cd my-tips
```

**생성된 구조:**

```text
my-tips/
  ├─ docs/
  │    └─ index.md     ← 홈페이지
  └─ mkdocs.yml        ← 설정 파일
```

## 3. VS Code에서 작성

`docs/` 폴더 안에 원하는 만큼 `.md` 파일 생성

예:

```text
docs/
  index.md
  linux.md
  networking.md
  windows.md
```

`mkdocs.yml` 안에 네비게이션 구성 (사이드바 역할):

```yaml
site_name: My Tips
theme:
  name: material

nav:
  - 홈: index.md
  - 리눅스: linux.md
  - 네트워크: networking.md
  - 윈도우: windows.md
```

`.gitignore` 안에 `site/` 폴더 제외 추가

## 4. 로컬 미리보기

```bash
mkdocs serve
```

→ 브라우저에서 [http://127.0.0.1:8000](http://127.0.0.1:8000) 접속<br>
👉 UI 확인 가능

## 5. GitHub에 올리기(TERMINAL)

```bash
git init
git add .
git commit -m "첫 MkDocs 사이트"
git branch -M main
git remote add origin https://github.com/username/my-tips.git
git push -u origin main
```
## 5. GitHub에 올리기(GUI)
```bash
Soure Control(Ctrl+Shift+G) 에서
init
Message 작성(필수-버그인듯) 하고 Commit

```

## 6. GitHub Pages 자동 배포

- GitHub 저장소 → Settings → Pages → Source:
  - Deploy from a branch 선택
  - Branch = `gh-pages` 지정
- 로컬에서 배포 실행:

```bash
mkdocs gh-deploy
```

→ 자동으로 `gh-pages` 브랜치에 사이트 파일 업로드
→ [https://username.github.io/it-tips](https://username.github.io/it-tips) 에서 사이트 확인

---

## 🎯 정리

- VS Code에서 Markdown 작성
- `mkdocs serve`로 로컬 미리보기
- `git push` + `mkdocs gh-deploy` → GitHub Pages 자동 배포

👉 이 흐름으로 쓰면, 진짜 Notion 스타일 개인 지식창고가 GitHub에 생깁니다.
