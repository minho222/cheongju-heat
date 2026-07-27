# 청주 폭염·온열질환 모니터

충청북도 청주시 기준 실시간 체감온도(기온+습도)를 계산해 산업안전보건법상 **폭염작업 단계·필요 조치**를 보여주고, **근무시간(08:30~19:00) 매시간 자동 기록**하는 웹페이지.

- `index.html` — 사이트 본체 (GitHub Pages로 공개)
- `data/log.json` — 자동 측정 기록 저장소 (GitHub Actions가 갱신)
- `.github/workflows/collect.yml` — 매시간 자동 수집 (근무시간만 기록)

데이터 출처: [Open-Meteo](https://open-meteo.com) · 체감온도 공식: 기상청 여름철 산출식

---

## 웹 업로드로 배포하는 법 (인증 이슈 우회)

### 1. 새 저장소 만들기
- github.com → 우측 상단 **+** → **New repository**
- 이름: 예) `cheongju-heat` · **Public** 선택 · **Create repository**

### 2. 파일 올리기
- 새 repo 화면 → **uploading an existing file** 클릭
- 이 폴더의 **`index.html`** 과 **`README.md`** 를 드래그해서 업로드 → **Commit changes**

### 3. 하위 폴더 파일 만들기 (드래그가 어려우면 직접 생성)
- **Add file → Create new file**
  - 파일명에 `data/log.json` 입력 → 내용 `[]` → Commit
  - 파일명에 `.github/workflows/collect.yml` 입력 → 이 폴더의 collect.yml 내용 붙여넣기 → Commit
  - (파일명에 `/` 를 치면 자동으로 폴더가 만들어집니다)

### 4. 자동기록 권한 켜기
- repo **Settings → Actions → General → Workflow permissions**
- **Read and write permissions** 선택 → Save
  (Actions가 data/log.json 을 커밋할 수 있어야 함)

### 5. Actions 활성화 & 첫 실행
- 상단 **Actions** 탭 → 워크플로우 활성화(Enable) 안내가 나오면 승인
- **Collect Cheongju heat log** → **Run workflow** 로 한 번 수동 실행(테스트)

### 6. 웹페이지 공개 (GitHub Pages)
- **Settings → Pages**
- Source: **Deploy from a branch** · Branch: **main** / **/(root)** → Save
- 잠시 후 `https://<아이디>.github.io/cheongju-heat/` 로 접속

---

## 참고
- 기록은 컴퓨터가 꺼져 있어도 GitHub 서버에서 매시간 자동 저장됩니다.
- 법령은 개정될 수 있으니 실제 적용 전 국가법령정보센터 원문 확인 권장.
- 옥외작업은 "측정 곤란 시 기상청 발표 체감온도 사용" 근거에 해당. 실내·열원 작업장은 현장 실측 필요.
