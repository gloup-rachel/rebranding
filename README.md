# FRISAT 프리셋 리브랜딩 — MVP 사이트 작업 폴더

> 인하우스 마케팅 AI 시스템 구축 서비스 "FRISAT"의 신규 서비스 론칭 + MVP 세일즈 페이지 구축 작업물 모음
> 최종 업데이트: 2026-05-04

---

## 폴더 구성

| 파일 | 역할 | 다음 액션 |
|---|---|---|
| **`index.html`** | MVP 세일즈 페이지 본체. 7섹션 단일 페이지 (Hero / Problem / Solution / Process / Live Demo / 맞춤 제안 / Final CTA). Tailwind CDN + Pretendard. | GitHub repo로 push → Vercel 자동 배포 |
| **`demos/` 폴더** | 5개 라이브 데모 HTML (B2C 뷰티 브랜드 케이스). Cat A 2개·Cat B 2개·Cat C 1개. `index.html`에서 상대경로(`./demos/...`)로 연결 | 같은 GitHub repo 배포 시 frisat.ai/demos/A1_dashboard.html 등으로 자동 접근 |
| **`SETUP_GUIDE.md`** | Day 1-2 셋업 가이드. GitHub·Vercel·Tally·Cal.com·HubSpot·GTM·광고 픽셀까지 단계별 절차 | Day 1 도메인 등록부터 시작 |
| **`PROJECT_PLAN.md`** | 전체 프로젝트 계획서. 솔루션 옵션 비교(A/B/C/D/E)·도구 스택·의사결정 가이드·디자인 가이드 v1.0 적용 내역 | 새로운 의사결정 발생 시 업데이트 |
| **`DESIGN_MOCKUP_PURPLE.html`** | 컬러 팔레트 후보 비교 목업 (Purple A/B/C 3안). **Purple B `#6C31D4` 최종 확정** | `index.html` 톤이 이 목업과 어긋나면 비교 참조 |

### `demos/` 폴더 상세

| 파일 | 카테고리 | 데모 내용 | index.html 연결 |
|---|---|---|---|
| `A1_dashboard.html` | Cat A | 통합 매출/재고 현황 대시보드 | Cat A 카드 1번 |
| `A2_roi_sim.html` | Cat A | 월 마감 ROI 시뮬레이션 | Cat A 카드 2번 |
| `B1_monitor_bot.html` | Cat B | 채널별 모니터링 봇 (Schedule) | Cat B 카드 1번 |
| `B2_strategy_bot.html` | Cat B | AI 마케팅 전략 봇 (SKILL 가이드) | Cat B 카드 2번 |
| `C_global.html` | Cat C | 글로벌 확장 대시보드 | Cat C 단독 풀너비 카드 |

**⚠️ 오키뷰티 표기 주의**: 데모 파일 내부엔 "오키뷰티(OKEE BEAUTY)" 명시되어 있음. 노션 가이드엔 "오키뷰티 동의 획득 후 추가"로 보류 상태였음. 현재 사이트 카드 라벨에선 "B2C 뷰티 브랜드 케이스"로 익명화. 동의 획득 완료 시 카드 라벨에 "오키뷰티" 명시 변경 가능.

---

## 서비스 개요

- **VP**: "AI로 스스로 돌아가는 마케팅 조직, 8주 만에."
- **타겟(ICP)**: 마케팅 1~3인 팀 (회사 규모 5~50인)
- **퍼널**: 무료 진단 미팅 → AX워크샵(200만) 또는 8주 패키지(1,000만) → 유지보수(월 150-250만) → 자문(월 150만)
- **연 LTV 기준**: 2,500만 ~ 3,200만/계약
- **가격 정책**: **미노출** (사이트엔 비공개, 진단 미팅에서 맞춤 제안)

---

## 솔루션 스택 확정 (옵션 E)

| 영역 | 도구 | 비용 |
|---|---|---|
| 코드 | `index.html` (Tailwind CDN, 빌드 없음) | 무료 |
| 저장소 | GitHub Private Repo | 무료 |
| 호스팅 | Vercel Hobby | 무료 (자동 SSL·CDN) |
| 도메인 | frisat.ai / .io / .now (내부 투표 중) | 연 $60-90 |
| 폼 | Tally Free | 무료 |
| 미팅 예약 | Cal.com Free | 무료 |
| CRM | HubSpot Free | 무료 |
| Webhook 중개 | Make.com Free | 무료 (월 1,000건) |
| 트래킹 | GTM + GA4 | 무료 |
| 광고 픽셀 | Meta + Google + 네이버 (모두 GTM 일괄) | 무료 |

**총 비용**: 첫 달 약 9만원 (도메인만), 이후 월 0원

---

## 디자인 시스템 (Purple B 확정)

- **콘셉트**: 따뜻한 전문가 (Warm Expert)
- **컬러 팔레트**:
  - Primary: `#6C31D4` (Vivid Purple) — CTA·강조 (섹션당 1-2곳만)
  - Page BG: `#F9F8FF` (`#FFFFFF` 절대 금지)
  - Blob: Periwinkle `#8390CA` / Mint `#C0E0DB` / Blush `#F7A7A6` (opacity 10-20%)
  - Headline: `#1A1238` (`#000000` 금지)
  - Body: `#8A87B8` / Subtle: `#A89CC8` / Badge: `#E8DFFF`
- **폰트**: Pretendard Variable, SemiBold 600 헤드라인 (목업 톤)
- **블롭**: Organic 비대칭 형태 (`border-radius: 60% 40% 55% 45% / 45% 55% 40% 60%`)

---

## 진행 상태 (2026-05-04 기준)

### ✅ 완료
- [x] FRISAT 회사·서비스·ICP·퍼널 정의 (노션 문서 5종)
- [x] 솔루션 옵션 비교(A/B/C/D/E) → 옵션 E 확정
- [x] 디자인 가이드 v1.0 + Purple B `#6C31D4` 컬러 확정
- [x] `index.html` 7섹션 IA + 반응형 + 앵커 네비 + 통계 바 작성
- [x] Plan 파일 + Setup 가이드 작성
- [x] 작업물 한 폴더로 정리 (이 폴더)

### 🟡 진행 필요 (사용자 액션)
- [ ] **도메인 투표 결과 확정** (frisat.ai / .io / .now)
- [ ] **Day 1**: 도메인 등록 + GitHub repo `frisat-mvp` 생성 + `index.html` push + Vercel 연결
- [ ] **Day 1-PM**: Tally + HubSpot + Cal.com 계정 가입
- [ ] **Day 2**: Tally 진단 폼 5문항 작성 + Make.com Webhook + Cal.com 미팅 페이지 → URL 받으면 Claude에 전달
- [ ] **Day 2**: GTM ID + GA4 측정 ID 발급 → Claude에 전달 → `index.html`에 head 코드 추가
- [ ] **Day 3+**: 광고 4채널(Meta/Google/네이버) 캠페인 송출

### 🔵 결정 보류
- [ ] **Demo URL 2개**: 어디로 연결할지 (옵션 A: 같은 GitHub repo / 옵션 B: 별도 서브도메인)
- [ ] 데모 썸네일 실제 스크린샷 교체 시점
- [ ] 오키뷰티 레퍼런스 동의 획득 후 Demo 카드 추가 여부
- [ ] 노션 5개 문서 핵심 텍스트 → ICP 디테일·브랜드 디테일 보강

---

## 다음 작업 시 참조

- **Claude에게 사이트 수정 요청 시**: 자연어로 요청만 하면 됨 (예: "Hero 헤드라인을 X로 바꿔줘", "Solution 카드에 Y 추가") → Claude가 `index.html` Edit → 사용자가 GitHub commit → Vercel 자동 재배포
- **메모리 위치**: `~/.claude/projects/-Users-rachel-Documents-Claude-Projects-------B2B-------------/memory/` — FRISAT 컨텍스트는 자동 로드됨
- **Plan 원본 위치**: `~/.claude/plans/cryptic-foraging-zephyr.md` (이 폴더의 `PROJECT_PLAN.md`는 사본)

---

## 주의사항 (분리 원칙)

이 폴더는 **FRISAT 자사** 작업물 전용. 고객사인 **리스페이스** 자산(`apps_script_respace.js`, `respace_dashboard_v3.html` 등)은 `~/Documents/Claude/Projects/리스페이스 B2B 마케팅/`에 별도 보관. 두 프로젝트의 자산을 절대 혼용하지 않는다.
