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

## 5. GitHub에 올리기
#### TERMINAL 에사:
```bash
git init
git add .
git commit -m "첫 MkDocs 사이트"
git branch -M main
git remote add origin https://github.com/appi77/my-tips.git
git push -u origin main
```
#### 또는 GUI에서:
- Source Control(Ctrl+Shift+G)에서
- Initialize Repository 클릭
- 커밋 메시지 입력 후 'Commit' 클릭
- 'Sync Changes' 클릭 후 원격 저장소(/appi77/my-tips.git) 선택 또는 지정


## 6. GitHub Pages 자동 배포
TERMINAL에서 배포 실행:
```bash
mkdocs gh-deploy
```
- 명령을 실행하면 사이트 파일이 자동으로 `gh-pages` 브랜치에 업로드됩니다.

업로드 후, GitHub 저장소에서 다음을 확인하세요:
- Settings → Pages → Source:
  - Deploy from a branch 선택
  - Branch가 `gh-pages`로 설정되어 있는지 확인

→ [https://username.github.io/it-tips](https://username.github.io/it-tips) 에서 사이트 확인

---

## 🎯 정리

- VS Code에서 Markdown 작성
- `mkdocs serve`로 로컬 미리보기
- `git push` + `mkdocs gh-deploy` → GitHub Pages 자동 배포

