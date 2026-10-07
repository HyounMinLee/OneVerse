# 오늘의 말씀

하루 한 구절씩 말씀을 기록하는 모바일 웹페이지입니다.
GitHub Pages로 호스팅하고, 등록한 구절은 이 저장소에 JSON 파일로 커밋됩니다.

## 구성

```
index.html      화면 전체 (HTML/CSS/JS 단일 파일)
.nojekyll       GitHub Pages의 Jekyll 처리 생략
data/           구절 데이터 (첫 저장 시 자동 생성)
  2026/
    2026-10.json
```

월 파일 예시:

```json
{
  "month": "2026-10",
  "entries": {
    "2026-10-07": {
      "date": "2026-10-07",
      "reference": "빌립보서 4:13",
      "text": "내게 능력 주시는 자 안에서 내가 모든 것을 할 수 있느니라",
      "note": "묵상 메모",
      "createdAt": "2026-10-07T00:00:00.000Z",
      "updatedAt": "2026-10-07T00:00:00.000Z"
    }
  }
}
```

구절 하나를 저장·수정·삭제할 때마다 커밋 1개가 생성됩니다.
커밋 메시지 예: `구절 등록: 2026-10-07 빌립보서 4:13`

## 설정 순서

### 1. 저장소 만들기

GitHub에서 새 저장소를 만들고 `index.html`, `.nojekyll`, `README.md`를 올립니다.

### 2. GitHub Pages 켜기

저장소 Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)` → Save

접속 주소: `https://<아이디>.github.io/<저장소이름>/`

무료 플랜은 공개 저장소에서만 Pages를 쓸 수 있습니다. 공개 저장소라면 묵상 메모를 포함한 `data/` 내용도 공개됩니다.

### 3. 토큰 발급 (Fine-grained personal access token)

GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token

- Repository access: Only select repositories → 이 저장소 하나만 선택
- Repository permissions → Contents: Read and write
- 만료일은 원하는 기간으로 설정 (만료되면 새로 발급해 다시 입력)

### 4. 앱에서 연결

폰에서 Pages 주소에 접속 → 오른쪽 위 연결 아이콘 → 토큰 입력 → 저장 및 확인

`github.io` 주소로 접속하면 소유자와 저장소 이름이 자동으로 채워집니다.
토큰은 그 기기의 브라우저에만 저장되고, 저장소에는 올라가지 않습니다.

## 동작 방식

- 토큰이 있는 기기: GitHub API로 읽고 쓰므로 저장 즉시 반영됩니다.
- 토큰이 없는 기기: Pages에 배포된 `data/` 파일을 읽어서 보여줍니다. 커밋 후 Pages 재배포가 끝나야 반영됩니다.
- 같은 월 파일을 동시에 수정해 충돌이 나면 최신 내용을 다시 읽어 한 번 재시도합니다.
- 최근에 본 데이터는 브라우저에 캐시되어 앱을 열면 바로 표시되고, 이어서 GitHub에서 최신 내용을 확인합니다.

## 주의

- 토큰을 저장한 폰을 다른 사람이 쓰면 이 저장소를 수정할 수 있습니다. 폰을 분실하면 GitHub에서 토큰을 바로 삭제하세요.
- 삭제한 구절도 Git 커밋 기록에는 남습니다.
