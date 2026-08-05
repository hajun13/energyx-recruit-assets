# 채용 페이지 이미지 자산

`recu*.html` 6개 파일이 공유하는 이미지 세트입니다.
기존 Cloudinary(`res.cloudinary.com/jophxzt6`) 계정이 한도 초과로 **HTTP 401** 상태가 되어
모든 이미지가 깨졌기 때문에, GitHub + jsDelivr CDN으로 옮깁니다.

## 배포 URL 형식

```
https://cdn.jsdelivr.net/gh/<계정>/<저장소>@<태그>/assets/<파일명>
```

브랜치(`@main`)가 아니라 **태그(`@v1`, `@v2` …)** 를 쓰세요.
jsDelivr는 브랜치 URL을 최대 7일 캐시해서, 같은 파일명으로 이미지를 교체해도
한동안 옛 이미지가 그대로 나옵니다. 태그를 쓰면 새 태그를 달아 URL만 올리면 즉시 반영됩니다.

## 파일 목록

| 파일 | 페이지 내 위치 | 원본 | 비고 |
|---|---|---|---|
| `card1.jpg` | 상단 하이라이트 01 · 글로벌 성장의 중심 | jobhtml/card1.png | |
| `card2.jpg` | 상단 하이라이트 02 · 초기 핵심 멤버 | jobhtml/card2.png | |
| `card3.jpg` | 상단 하이라이트 03 · 글로벌 프로젝트 | jobhtml/card3.png | |
| `card4.jpg` | 상단 하이라이트 04 · 커리어 도약 | jobhtml/card4.png | |
| `qatar-clean.jpg` | 카타르 장점 · 깨끗하고 정돈된 도시환경 | jobhtml/qatar4.png | |
| `qatar-infra.jpg` | 카타르 장점 · 우수한 생활 인프라 | jobhtml/qatar2.png | |
| `qatar-safety.jpg` | 카타르 장점 · 체감되는 높은 안전 수준 | jobhtml/qatar3.png | ⚠ 구버전 대체본 |
| `qatar-stress.jpg` | 카타르 장점 · 낮은 일상 스트레스 | jobhtml/qatar1.png | ⚠ 구버전 대체본 |
| `qatar-biz.jpg` | 글로벌 비즈니스 허브 (큰 카드) | jobhtml/qatar-biz.png | |
| `qatar-family.jpg` | 가족 동반·장기 체류 환경 (큰 카드) | jobhtml/qatar-family.png | ⚠ 구버전 대체본 |
| `income-1.jpg` | 세계 최상위권 소득 · 사진 1 | — | ❌ **원본 필요** |
| `income-2.jpg` | 세계 최상위권 소득 · 사진 2 | — | ❌ **원본 필요** |
| `intl-1.jpg` | 외국인 중심의 국제도시 · 사진 1 | — | ❌ **원본 필요** |
| `intl-2.jpg` | 외국인 중심의 국제도시 · 사진 2 | — | ❌ **원본 필요** |
| `benefit-massage.png` | 베네핏 아이콘 · 웰니스/스파/마사지 | jobhtml/benefit-massage.png | |
| `benefit-clean.png` | 베네핏 아이콘 · 집안일/청소 도우미 | jobhtml/benefit-clean.png | |
| `benefit-food.png` | 베네핏 아이콘 · 사내 식당 | jobhtml/benefit-food.png | |
| `benefit-health.png` | 베네핏 아이콘 · 건강보험 | jobhtml/benefit-health.png | |
| `benefit-family.png` | 베네핏 아이콘 · 동반 가족 생활 지원 | Pictures/Screenshots/스크린샷 2026-07-07 163438.png | |
| `banner.gif` | `recu.html` 상단 GIF 배너 | jobhtml/energyx-hq.gif | recu.html 전용 |

### ⚠ 구버전 대체본 3장

`qatar-safety` / `qatar-stress` / `qatar-family`는 나중에 Cloudinary에서
`ig_...` 파일로 교체됐는데 그 원본이 로컬에 없습니다. 그래서 교체 이전 버전을 넣었습니다.
셋 다 해당 문구와 내용이 맞아 그대로 써도 무방하며, 최신본을 쓰려면
Cloudinary 콘솔에서 아래 파일을 받아 덮어쓰면 됩니다.

- `ig_08bf95e005b853a5016a45e5c01e308191817875edd23653ab_kz0gdx.png` → `qatar-safety.jpg`
- `ig_08bf95e005b853a5016a45e6183344819193b8188608f7ad22_prcabz.png` → `qatar-stress.jpg`
- `ig_0b52bcef9f84b79e016a45e6a36d848191999027ea5130ebfa_wlqdlq.png` → `qatar-family.jpg`

### ❌ 원본이 필요한 4장

로컬에 사본이 전혀 없습니다. Cloudinary 콘솔에서 받아 `assets/`에 아래 이름으로 넣어주세요.

- `image1_jwc22x.jpg` → `income-1.jpg`
- `image2_yk169d.jpg` → `income-2.jpg`
- `image3_prhwq5.png` → `intl-1.jpg` (확장자 jpg로 저장)
- `image4_pulf8l.png` → `intl-2.jpg` (확장자 jpg로 저장)

## 도구

| 스크립트 | 용도 |
|---|---|
| `tools/build_assets.py` | 원본을 `assets/`로 모으고 웹용으로 리사이즈·압축 (26.5MB → 3.7MB) |
| `tools/rehost_urls.py` | 6개 HTML의 Cloudinary/imgbb URL을 jsDelivr URL로 일괄 치환 (115곳) |

```bash
# 먼저 확인만
python tools/rehost_urls.py --owner <계정> --repo <저장소> --ref v1 --dry-run
# 실제 치환 (.bak 백업 생성)
python tools/rehost_urls.py --owner <계정> --repo <저장소> --ref v1
# 배포 후 URL 응답 확인
python tools/rehost_urls.py --owner <계정> --repo <저장소> --ref v1 --verify
```
