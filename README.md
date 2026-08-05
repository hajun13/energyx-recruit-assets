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
| `qatar-safety.jpg` | 카타르 장점 · 체감되는 높은 안전 수준 | `_originals/2.png` | 도하 West Bay 보행로 |
| `qatar-stress.jpg` | 카타르 장점 · 낮은 일상 스트레스 | jobhtml/qatar1.png | ⚠ 구버전 대체본 |
| `qatar-biz.jpg` | 글로벌 비즈니스 허브 (큰 카드) | jobhtml/qatar-biz.png | |
| `qatar-family.jpg` | 가족 동반·장기 체류 환경 (큰 카드) | `_originals/1.png` | 도하 West Bay 해안 산책로 |
| `income-1.jpg` | 세계 최상위권 소득 · 사진 1 | `_originals/image4.png` | 도하 코르니쉬 (카타르) · 739x415 저해상도 |
| `income-2.jpg` | 세계 최상위권 소득 · 사진 2 | `_originals/image2.jpeg` | ⚠ **아부다비 (UAE)** — 카타르 아님 |
| `intl-1.jpg` | 외국인 중심의 국제도시 · 사진 1 | `_originals/image3.png` | The Pearl, 도하 (카타르) |
| `intl-2.jpg` | 외국인 중심의 국제도시 · 사진 2 | `_originals/image1.jpeg` | ⚠ **상하이 푸둥 (중국)** — 카타르 아님 |
| `benefit-massage.png` | 베네핏 아이콘 · 웰니스/스파/마사지 | jobhtml/benefit-massage.png | |
| `benefit-clean.png` | 베네핏 아이콘 · 집안일/청소 도우미 | jobhtml/benefit-clean.png | |
| `benefit-food.png` | 베네핏 아이콘 · 사내 식당 | jobhtml/benefit-food.png | |
| `benefit-health.png` | 베네핏 아이콘 · 건강보험 | jobhtml/benefit-health.png | |
| `benefit-family.png` | 베네핏 아이콘 · 동반 가족 생활 지원 | Pictures/Screenshots/스크린샷 2026-07-07 163438.png | |
| `banner.gif` | `recu.html` 상단 GIF 배너 | jobhtml/energyx-hq.gif | recu.html 전용 |

### ⚠ 확인이 필요한 항목

**촬영지가 카타르가 아닌 사진 2장** — 채용 공고 맥락상 도하로 오해될 수 있습니다.

- `income-2.jpg` — 아부다비(UAE) 코르니쉬 야경
- `intl-2.jpg` — 상하이 푸둥 야경

**구버전 대체본 1장** — `qatar-stress`는 Cloudinary에서 `ig_...prcabz.png`로 교체됐으나
그 원본이 로컬에 없어 교체 이전 버전(jobhtml/qatar1.png)을 넣었습니다.
문구("낮은 일상 스트레스")와 내용이 맞아 그대로 써도 무방합니다.

**저해상도 1장** — `income-1.jpg`는 원본이 739x415로, 카드 표시 크기(2x 기준 약 820x500)에
약간 못 미칩니다. 화면에서는 크게 티나지 않지만 더 큰 원본이 있으면 교체를 권합니다.

`_originals/`에는 리사이즈 전 원본이 보관돼 있습니다 (저장소에는 올라가지 않음).

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
