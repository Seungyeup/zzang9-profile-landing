# 구윤진 강사 투표 랜딩페이지

2026 엠베스트 0타 강사 선발대회용 모바일 우선(mobile-first) 정적 랜딩페이지입니다.
빌드 과정 없이 `index.html` 한 파일로 동작합니다.

## 로컬 미리보기

브라우저로 `index.html` 을 바로 열거나, 간단한 정적 서버를 사용하세요.

```bash
python3 -m http.server 8000
# http://localhost:8000 접속
```

## 배포 전에 채워야 할 항목

| 위치 | 내용 |
|------|------|
| `index.html` 내 `VOTE_URL` | 실제 투표 페이지 URL (현재 `https://example.com/vote`) |
| `.hero__photo` 의 `background-image` | 프로필 사진 (`background-image:url('profile.jpg')`) |
| 경력 & 성과 3개 행 | 실제 경력/수상/커리큘럼 내용 |
| SNS 링크 3개 `href` | Instagram · YouTube · 엠베스트 강의실 실제 주소 |
| `<head>` 의 `og:url` / `og:image` | 배포 도메인 확정 후 (카카오톡/링크 공유 미리보기용, 권장 1200×630) |

강의 영상 2개는 시안의 YouTube 영상 ID(`RFSKrmF9FbY`, `vNDMPPEaBzU`)가 그대로 들어가 있습니다.
교체하려면 해당 `.video-frame` 의 `data-yt` / `data-start` / 썸네일 `src` 를 수정하세요.

## Cloudflare Pages 배포

### 방법 A — GitHub 연동 (권장)

1. 이 저장소를 GitHub 에 푸시합니다.
2. Cloudflare 대시보드 → **Workers & Pages → Create → Pages → Connect to Git**
3. 저장소 선택 후 빌드 설정:
   - **Framework preset:** None
   - **Build command:** (비워둠)
   - **Build output directory:** `/` (저장소 루트)
4. Save and Deploy. 이후 `main` 브랜치에 푸시할 때마다 자동 배포됩니다.

### 방법 B — Wrangler 직접 업로드

```bash
npm i -g wrangler
wrangler pages deploy . --project-name=zzang9-vote
```

`_headers` 파일이 함께 배포되어 HTML 은 항상 최신, 기본 보안 헤더가 적용됩니다.
