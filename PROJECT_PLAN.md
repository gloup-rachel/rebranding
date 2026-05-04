# FRISAT MVP 세일즈 페이지 구축 계획 (옵션 E - HTML + Vercel)

## Context

**FRISAT (사용자 자사)**: 인하우스 마케팅 AI 시스템 구축 서비스. 3인 팀, 디자이너·개발자 없음. 기존 자사 사이트 없음.

**리스페이스(Respace)는 FRISAT의 고객사**이며 작업 디렉토리의 `apps_script_respace.js` 등은 고객사 자산 — FRISAT 자사 사이트와 분리.

### 신규 서비스 본질
- **VP**: "8주 안에, 확실한 마케팅 전문가가 당신 팀의 AI 프리셋을 완성해드립니다."
- **퍼널**: 무료 진단 미팅 → AX워크샵(200만) 또는 8주 패키지(1,000만) → 유지보수(월 150-250만) → 자문(월 150만)
- **연 LTV**: 2,500만~3,200만/계약
- **가격 정책**: **미노출** (사이트엔 비공개, 진단 미팅에서 제시)

### ICP 페인포인트
1. 마케팅 실질 인원 1-3인 (회사 5-50인 규모)
2. AI 도입 의지 있지만 "어떻게"가 없음
3. 전문가 채용 사실상 불가능

### 의도하는 결과
**MVP 세일즈 페이지 1개**를 1-2일 내 frisat.ai에 배포 → 광고 송출로 메세지·오퍼·채널 검증 → 데이터 기반으로 정식 홈페이지 디벨롭.

### 솔루션 결정사항 (2026-05-04 확정)
**옵션 E: HTML + Tailwind + GitHub + Vercel + 외부 임베드**
- Claude가 코드 100% 작성 → 사용자는 GitHub commit + Vercel 배포만
- 기각된 옵션: 옵션 A/B/C(슬래시·아임웹), 옵션 D(Framer 템플릿). MVP 단계에선 모두 과투자
- 정식 홈페이지 디벨롭 시점에 Framer/Webflow/Next.js 등 재선택

---

## 도구 스택 (확정안)

| 영역 | 도구 | 비용 | 역할 |
|---|---|---|---|
| 코드 | `index.html` (Tailwind CSS via CDN) | 무료 | 단일 파일 1페이지 |
| 저장소 | GitHub Private Repo | 무료 | 버전 관리 |
| 호스팅 | Vercel Hobby | 무료 | 자동 SSL·CDN·GitHub 연동 자동 배포 |
| 도메인 | frisat.ai 또는 .io/.now (내부 투표 중) | 연 $60-90 | Vercel DNS 연결 |
| 폼 | Tally Free | 무료 | 진단 5문항, Webhook |
| 미팅 예약 | Cal.com Free | 무료 | iframe 임베드 |
| CRM | HubSpot Free | 무료 | 리드 관리·시퀀스·미팅 추적 |
| Webhook 중개 | Make.com Free | 무료 (100건/월) | Tally → HubSpot |
| 트래킹 | GTM + GA4 | 무료 | 다중 채널 픽셀 일괄 |
| 광고 픽셀 | Meta + Google + 네이버 | 무료 | GTM 통해 |
| 챗봇 | 채널톡 Free (선택) | 무료 | 인바운드 + 자사 시연 |

**총 비용**: 첫 달 약 9만원 (도메인만), **이후 월 0원** (도메인 외)

---

## MVP 사이트 IA (7섹션 단일 페이지)

| # | 섹션 | 핵심 카피 | 임베드/링크 |
|---|---|---|---|
| 1 | Hero | **"AI로 스스로 돌아가는 마케팅 조직, 8주 만에."** + 작은 deco bar + CTA 2개 ("도입 상담 신청" Primary / "프로세스 보기" Secondary) + 하단 통계 바 (8주·100%·AI 기반) | 목업 Purple B 톤 정확히 적용 |
| 2 | Problem | 3개 카드 (VOC 원문) | - |
| 3 | Solution | Cat A·B·C 3개 카테고리 | - |
| 4 | Process | 8주 타임라인 (1주/2주/3-5주/6-8주) | - |
| 5 | **Live Demo** | 실제 운영 중 시스템 데모 카드 2개 (Cat A 대시보드 / Cat A+B 월간 리포트) | 데모 URL 임베드 또는 새 탭 열기 — Reference 섹션 대체 (2026-05-04 결정) |
| 6 | "진단 후 맞춤 제안" | 가격 미노출 정책 — 신뢰 메세지 + CTA | (Pricing 섹션 대체) |
| 7 | Final CTA | "지금 무료 진단 신청하기" | Tally 폼 + Cal.com 임베드 |

**핵심 변경 (이전 plan 대비)**:
- Pricing 섹션은 가격 미노출 정책에 따라 "진단 후 맞춤 제안" 섹션으로 변형
- Reference 섹션(백년밥상·리스페이스 카드) → **Live Demo 섹션**으로 교체 (실제 작동하는 데모 임베드/링크)
- Demo URL 2개 결정 필요: ① Cat A 대시보드 데모, ② Cat A+B 월간 리포트 데모

---

## 자사 시연장 흐름 (Lead → Meeting Pipeline)

```
방문자 → frisat.ai 접속 → CTA 클릭
     ↓
[Tally 진단 폼 5문항 임베드]
     ↓
[Tally Webhook] → Make.com → HubSpot Free CRM Contact 자동 생성
     ↓
[자동 이메일 1] "진단 결과 정리해서 미팅 때 가져갑니다"
     ↓
[Cal.com 임베드] 30분 진단 미팅 자동 예약
     ↓
[24h 전 자동 리마인더]
     ↓
[미팅 후] HubSpot 시퀀스 follow-up 3통
```

이 흐름 자체가 "FRISAT이 만드는 시스템 데모".

---

## 2일 실행 계획 (Day 1-2)

### Day 1 — 사이트 배포 (4-5시간)
- [ ] **Day 1-AM**: 도메인 등록 (frisat.ai/io/now 중 투표 결과) — Porkbun 권장
- [ ] **Day 1-AM**: Claude가 `index.html` 초안 작성 (이미 진행)
- [ ] **Day 1-AM**: GitHub 저장소 생성 → `index.html` commit
- [ ] **Day 1-PM**: Vercel 가입 → GitHub 저장소 연결 → 자동 배포 → vercel.app 서브도메인 확인
- [ ] **Day 1-PM**: Vercel에 도메인 연결 → DNS 변경 (Porkbun) → SSL 자동 발급
- [ ] **Day 1-PM**: Tally·HubSpot·Cal.com 계정 가입 (옵션 E 가이드 참조)

### Day 2 — 인프라·임베드·트래킹 (4-5시간)
- [ ] **Day 2-AM**: Tally 진단 폼 5문항 작성 → Make.com → HubSpot Webhook 연결
- [ ] **Day 2-AM**: Cal.com 30분 미팅 이벤트 + Google Calendar 연동
- [ ] **Day 2-AM**: 사용자가 Tally·Cal.com URL을 Claude에 전달 → Claude가 `index.html`에 임베드 코드 추가 → commit → Vercel 자동 재배포
- [ ] **Day 2-PM**: GTM 컨테이너 + GA4 속성 → Claude가 head 코드 추가 → commit
- [ ] **Day 2-PM**: Meta Pixel + Google Ads + 네이버 전환 추적 → GTM에서 일괄 셋업
- [ ] **Day 2-PM**: E2E 테스트 (폼 제출 → HubSpot 도착 → Cal.com 예약 → 4개 픽셀 fire 확인)

### Day 3+ — 광고 송출 + 검증
- [ ] Meta·Google·네이버 광고 캠페인 셋업 (월 50-100만 소액 1차)
- [ ] HubSpot 이메일 시퀀스 3통 (Day 0/2/7)
- [ ] 1주 데이터 → 채널별 CPL 비교 → 카피·이미지 A/B 테스트 시작 (Claude 코드 수정 즉시 반영)

---

## 디자인 톤 (FRISAT 브랜드 가이드 v1.0 적용, 2026-05-04)

**콘셉트**: "따뜻한 전문가 (Warm Expert)" — A 구조(Problem-Solution-Process) + B 무드(공감형 비주얼)

**컬러 팔레트 (Periwinkle Pastel × Vivid Purple)**
| 역할 | 컬러명 | 헥스 | 사용처 |
|---|---|---|---|
| Primary 포인트 | Vivid Purple | `#6C31D4` | CTA·강조 수치·아이콘 (섹션당 1-2곳만) |
| Page BG | Purple Tint White | `#F9F8FF` | 모든 섹션 배경 (`#FFFFFF` 절대 금지) |
| Blob 1 | Periwinkle | `#8390CA` | Hero/CTA 배경 번짐, 투명도 ≤ 20% |
| Blob 2 | Soft Mint | `#C0E0DB` | 서브 섹션 배경 번짐 |
| Blob 3 | Blush Pink | `#F7A7A6` | 서브 섹션 배경 번짐 |
| Headline | Deep Purple Dark | `#1A1238` | 모든 헤드라인 (`#000000` 금지) |
| Body | Medium Purple Gray | `#8A87B8` | 본문·서브카피 |
| Badge BG | Light Purple Tint | `#E8DFFF` | 배지·칩·태그 |

**타이포그래피** (Pretendard Variable) — Purple B 목업 기준 절제 톤
- 메인 헤드라인: SemiBold(600) / 40-60px / letter-spacing -0.015em
- 카드 헤드라인·강조·CTA: SemiBold(600) / 16-20px
- 본문: Regular(400) / 14-18px / line-height 1.65-1.7
- **목업 톤 우선**: 가이드의 ExtraBold 800은 한국어 풀사이즈에선 과도하게 무거움. 목업의 우아한 SemiBold 600 채택. 강조는 색상(#6C31D4)으로

**컬러 사용 원칙 (중요)**
1. `#6C31D4`는 섹션당 1-2곳만 (강조·CTA·아이콘)
2. 번짐 블롭은 배경에서만, opacity 10-20%, blur 60px+
3. `#FFFFFF` 사용 금지 (배경은 `#F9F8FF` 고정)
4. 헤드라인 텍스트는 `#1A1238` 고정 (`#000000` 금지)
5. 다크 섹션(Final CTA) 배경은 `#1A1238`, 그 위 텍스트는 `#FFFFFF` 또는 `#E8DFFF`

**향후 톤 변경 시**: `tailwind.config.theme.extend.colors.brand` 한 곳만 수정 → 전체 일괄 반영

---

## 핵심 파일

### 신규 작업물
- `~/Documents/Claude/Projects/리스페이스 B2B 마케팅/실시간 대시보드/frisat_index.html` — MVP 사이트 코드
- `~/Documents/Claude/Projects/리스페이스 B2B 마케팅/실시간 대시보드/frisat_week1_setup_guide.md` — 옵션 E용 셋업 가이드 (재작성)

### 외부 자산 (사용자가 직접 운영)
- frisat.ai 도메인 (Porkbun)
- GitHub repo `frisat-mvp` (private)
- Vercel 프로젝트
- Tally 진단 폼
- HubSpot Free CRM
- Cal.com 미팅 페이지
- Make.com 시나리오 (Tally → HubSpot)
- GTM 컨테이너 + GA4
- Meta/Google/네이버 광고 계정

### 절대 손대지 않을 것 (고객사 자산)
- `apps_script_respace.js`, `respace_scoring_engine.py`, `respace_dashboard_v3.html` (리스페이스 운영)

---

## 검증 방법

### MVP 배포 완료 검증 (Day 2 끝)
1. frisat.ai 접속 → SSL 정상 → 7섹션 모두 보임
2. 모바일 반응형 정상 (Chrome DevTools 모바일 뷰)
3. Tally 폼 임베드 정상 → 테스트 제출 → HubSpot Contact 자동 생성
4. Cal.com 임베드 정상 → 테스트 예약 → Google Calendar 동기화 + 알림
5. GTM Preview 모드에서 GA4·Meta·Google·네이버 4개 픽셀 fire 확인
6. UTM 파라미터 (`?utm_source=test&utm_campaign=test`) → Tally hidden field에 자동 캡처

### MVP 검증 완료 기준 (Week 2-4)
1. 광고 4개 채널 모두에 "진단 신청" 전환 1건 이상 잡힘
2. 채널별 CPL 비교 가능
3. 진단 미팅 1건 이상 실제 진행
4. 사이트 카피·디자인 A/B 테스트 1회 이상 (Claude 코드 수정 즉시 반영)

---

## 정식 홈페이지 디벨롭 단계 (Future)

MVP 검증 완료 후:
- 메세지·오퍼·타겟·핵심 채널이 데이터로 검증된 상태
- 그때 Framer / Webflow / Next.js 중 선택 (당시 팀 규모·확장 요구에 따라)
- 1페이지 MVP의 카피·디자인은 검증된 자산이므로 신규 사이트로 그대로 이식
- 블로그·케이스 CMS·다국어·로그인 등 본격 기능은 이 시점에 도입

---

## 보류·확인 필요 사항

1. **도메인 확정**: 내부 투표 결과 (frisat.ai/io/now 중) → Day 1 시작 시점에 확정 필요
2. **노션 5개 문서 핵심 텍스트**: 브랜드 컬러·폰트 + ICP 디테일 + 서비스 구조 정밀 정보 → Day 2-3 시점에 사용자가 텍스트로 직접 제공 필요 (notion.site는 WebFetch 추출 불가)
3. **로고**: 별도 내부 진행 중. 완성 시 `/public/logo.png` 또는 SVG로 추가
4. **오키뷰티 레퍼런스 동의**: 획득 시 Reference 섹션 추가
5. **백년밥상·리스페이스 로고 사용 동의 확인**: Reference 섹션에 사용 예정
6. **챗봇 도입 시점**: 채널톡 vs 자사 데모 봇 — MVP에선 보류, Week 3-4 결정
