# FRISAT MVP 셋업 가이드 (옵션 E - HTML + Vercel)

> **목표**: 2일 안에 frisat.ai에 MVP 세일즈 페이지 + 리드 파이프라인 + 광고 트래킹 셋업 완료
> **사용자 작업 시간**: 약 8-10시간 (Day 1: 4-5h, Day 2: 4-5h)
> **첫 달 비용**: 약 9만원 (도메인만), 이후 월 0원

---

## 작업 흐름 한눈에

```
[Day 1 오전]
도메인 등록 → GitHub 저장소 생성 → Claude 작성한 index.html commit
        ↓
[Day 1 오후]
Vercel 가입 → GitHub 연결 → 자동 배포 → 도메인 연결 → SSL 발급
Tally + HubSpot + Cal.com 계정 가입
        ↓
[Day 2 오전]
Tally 진단 폼 5문항 작성 → Make.com 시나리오 → HubSpot 연결
Cal.com 미팅 페이지 셋업
URL 두 개를 Claude에 전달 → Claude가 사이트에 임베드 추가
        ↓
[Day 2 오후]
GTM + GA4 셋업 → Claude가 head 코드 추가
Meta + Google Ads + 네이버 광고 계정 + 4개 픽셀 GTM 일괄
E2E 테스트 → 광고 송출 준비 완료
```

---

## Day 1: 사이트 배포

### 1.1 도메인 등록 (15분)

내부 투표 결과에 따라 1개 선택:

**가용성 즉시 확인** (병렬 검색):
- Porkbun: https://porkbun.com/checkout/search?q=frisat.ai
- Namecheap: https://www.namecheap.com/domains/registration/results/?domain=frisat.ai

**권장**: Porkbun ($60-75/년 .ai 기준, 무료 WHOIS·SSL)

**참고**:
- `.now` TLD는 Vercel(과거 ZEIT)이 회수해서 일반 등록 불가 가능성 — 결과 보고 결정
- `.io` 등록 가능, $35-45/년
- `.ai` 등록 가능, $60-90/년
- 한국 가비아는 `.ai`/`.io` 모두 미지원 — 해외 등록처 필수

**등록 후**: DNS 설정은 Day 1 PM에 Vercel 안내에 따라 변경 (지금은 그대로)

### 1.2 Claude가 `index.html` 작성 (이미 진행됨)

위치: `~/Documents/Claude/Projects/리스페이스 B2B 마케팅/실시간 대시보드/frisat_index.html`

이 파일을 GitHub 저장소에 올릴 때는 **파일명을 `index.html`로 변경** 필요 (Vercel 기본 진입 파일).

### 1.3 GitHub 저장소 생성 + 첫 commit (30분)

**GitHub 가입 (이미 있으면 skip)**:
1. https://github.com/signup
2. 사용자명·이메일·비밀번호 설정

**저장소 생성**:
1. https://github.com/new
2. Repository name: `frisat-mvp`
3. **Private** 선택 (소스 비공개)
4. "Add a README file" 체크 안 함 (충돌 방지)
5. "Create repository"

**`index.html` 업로드 (가장 쉬운 방법 — 웹 UI)**:
1. 저장소 페이지에서 "uploading an existing file" 링크 클릭
2. `frisat_index.html` 파일 선택 → 업로드 화면에서 파일명을 **`index.html`로 변경**
3. 페이지 하단 "Commit changes" 클릭
4. 완료 — 저장소 메인에 `index.html` 보임

**(선택) 로컬에서 git CLI 사용**:
```bash
mkdir frisat-mvp && cd frisat-mvp
cp "/Users/rachel/Documents/Claude/Projects/리스페이스 B2B 마케팅/실시간 대시보드/frisat_index.html" ./index.html
git init
git add index.html
git commit -m "Initial MVP page"
git branch -M main
git remote add origin https://github.com/[YOUR_USERNAME]/frisat-mvp.git
git push -u origin main
```

### 1.4 Vercel 가입 + 자동 배포 (15분)

1. https://vercel.com/signup → "Continue with GitHub" (GitHub 계정으로 가입)
2. Hobby 플랜 선택 (무료, 비상업적 명목이지만 1페이지 영업 사이트는 문제 없음 — 실제 트래픽 많아지면 Pro $20/월 검토)
3. Dashboard → "Add New..." → "Project"
4. GitHub 저장소 목록에서 `frisat-mvp` 선택 → "Import"
5. Framework Preset: **"Other"** 선택 (정적 HTML이라 빌드 불필요)
6. Build & Output Settings: 기본값 그대로
7. "Deploy" 클릭
8. 30초~1분 후 배포 완료 → `frisat-mvp.vercel.app` 또는 비슷한 URL 발급
9. URL 클릭 → 사이트 정상 보이면 성공

### 1.5 도메인 연결 (15분)

**Vercel 측**:
1. 프로젝트 대시보드 → "Settings" → "Domains"
2. `frisat.ai` (또는 선택한 도메인) 입력 → "Add"
3. Vercel이 안내하는 DNS 레코드 복사:
   - A 레코드: `@` → `76.76.21.21`
   - 또는 CNAME: `www` → `cname.vercel-dns.com`

**Porkbun (등록처) 측**:
1. Porkbun → Domain Management → frisat.ai → "DNS Records"
2. Vercel이 안내한 A 레코드와 CNAME 추가
3. 5-30분 대기 → DNS 전파 완료
4. https://frisat.ai 접속 → 사이트 보이면 성공
5. SSL은 Vercel이 자동 발급 (Let's Encrypt)

### 1.6 Tally / HubSpot / Cal.com 계정 가입 (1시간)

Day 2에 본격 작업할 준비:
- Tally: https://tally.so 가입 (구글 로그인)
- HubSpot Free: https://www.hubspot.com/products/get-started-free 가입
- Cal.com: https://cal.com 가입 (구글 로그인)
- Make.com: https://www.make.com 가입 (Webhook 중개용)

Day 2에 본격 셋업.

---

## Day 2: 인프라 + 임베드 + 트래킹

### 2.1 Tally 진단 폼 5문항 (1시간)

**폼 제목**: "FRISAT 무료 AI 진단 신청"

**5문항** (모두 필수):

```
[Q1] 회사명 *
타입: Short answer
플레이스홀더: "예: 백년밥상"

[Q2] 담당자 직책 *
타입: Short answer
플레이스홀더: "예: 마케팅팀장 / 대표 / CMO"

[Q3] 회사 마케팅 전체 인원 (당신 포함) *
타입: Multiple choice
옵션:
  - 1명 (저 혼자)
  - 2-3명
  - 4-5명
  - 6명 이상

[Q4] 현재 가장 큰 마케팅 페인포인트는? *
타입: Multiple choice
옵션:
  - 매주 새로 시작하는 느낌, 반복 업무 구조가 없음
  - AI 도입하고 싶은데 어디서부터 해야 할지 모름
  - 우리 팀만의 시스템이 없어서 사람이 바뀌면 다 날아감
  - 데이터가 흩어져 있어서 의사결정이 늦음
  - 기타 (직접 입력)

[Q5] 연락 받을 이메일 *
타입: Email
플레이스홀더: "회사 도메인 이메일 권장"
```

**Hidden 필드 (UTM 자동 캡처)**:
- `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term` 5개를 Hidden field로 추가
- 광고 클릭 시 URL 파라미터가 자동으로 채워져 폼 데이터와 함께 전송됨

**Tally 폼 임베드 URL 복사**:
- 폼 작성 후 → "Share" → "Embed" → iframe URL 복사
- 형식: `https://tally.so/embed/[FORM_ID]?...`
- → **이 URL을 Claude에 전달하면 사이트에 임베드 추가**

### 2.2 HubSpot Free CRM 셋업 (1시간)

1. https://www.hubspot.com/products/get-started-free 가입
2. 회사 정보: FRISAT, 한국, 마케팅/컨설팅
3. 무료 플랜 그대로

**커스텀 속성 추가**:
- Settings → Properties → Contacts → "Create property"
  - `marketing_team_size` (Q3 매핑) - Single-line text
  - `pain_point` (Q4 매핑) - Single-line text
  - `utm_source`, `utm_medium`, `utm_campaign` - Single-line text 각각

### 2.3 Make.com 시나리오 (Tally → HubSpot) (45분)

**왜 Make.com**: Tally Webhook → HubSpot 직접 연결은 인증 복잡. Make.com 무료 플랜(월 1,000건)으로 중개하면 5분 셋업.

**시나리오 만들기**:
1. https://www.make.com → "Create a new scenario"
2. 첫 모듈 검색: "Tally" → "Watch Form Responses" → Tally 계정 연결 → 위 폼 선택
3. 두 번째 모듈 추가: "HubSpot CRM" → "Create or Update a Contact" → HubSpot 계정 연결
4. 필드 매핑:
   - email → Q5 응답
   - firstname → Q2 응답 (또는 별도 필드 추가)
   - company → Q1 응답
   - marketing_team_size → Q3 응답
   - pain_point → Q4 응답
   - utm_source/medium/campaign → 각 Hidden 필드
5. 시나리오 활성화 (오른쪽 토글 ON)

**테스트 제출**:
- Tally 폼 직접 접속 → 더미 데이터 제출
- 30초 내 HubSpot Contacts 탭에서 신규 Contact 확인
- Make.com 실행 이력에서 Success 확인

### 2.4 Cal.com 미팅 페이지 (1시간)

1. https://cal.com 가입 (구글 로그인)
2. URL 슬러그: `frisat` (즉 `cal.com/frisat`)
3. Event Type 생성: "FRISAT AI 진단 미팅"
   - Duration: 30분
   - Location: Google Meet (자동 링크 생성)
4. Availability: 평일 10-18시 (사용자 일정 맞춰 조정)
5. Google Calendar 연동 (Settings → Calendars → Connect Google) — 양방향 동기화
6. Workflows → "Add reminder": 미팅 24h 전, 1h 전 이메일 알림
7. Confirmation page: 진단 미팅 사전 안내 문구 추가

**Cal.com 임베드 코드 복사**:
- Event Type → "Embed" → "Inline Embed" → JavaScript snippet 복사
- → **이 코드를 Claude에 전달하면 사이트에 임베드 추가**

### 2.5 Tally + Cal.com 사이트에 임베드 (Claude 작업)

사용자가 Tally URL과 Cal.com 코드를 Claude에 전달:
- Claude가 `index.html` 수정 → GitHub commit → Vercel 자동 재배포
- 1-2분 후 frisat.ai에 폼·미팅 예약 임베드 정상 동작
- 사용자 직접 코드 수정 불필요

### 2.6 GTM + GA4 (1시간)

**GTM 컨테이너**:
1. https://tagmanager.google.com 가입 → 컨테이너 생성: "frisat.ai" (Web)
2. GTM ID (`GTM-XXXXXXX`) + 코드 스니펫 2개 복사
3. → **Claude에 전달**: Claude가 `index.html` head/body에 GTM 코드 삽입 → commit

**GA4 속성**:
1. https://analytics.google.com → 속성 생성: "frisat.ai"
2. 측정 ID (`G-XXXXXXX`) 복사
3. GTM → Tags → "New" → "Google Analytics: GA4 Configuration" → 측정 ID → 트리거 "All Pages"
4. Publish

**폼 제출 이벤트 트리거**:
1. GTM → Variables → Built-in → "Form ID", "Form Classes" 활성화
2. Triggers → "New" → "Form Submission" 또는 "Custom Event"
3. Tally는 iframe이라 직접 form submission 못 잡음 → Tally의 thank-you redirect URL을 활용:
   - Tally Settings → "After submission" → "Redirect to URL" → `https://frisat.ai/?thanks=1`
   - GTM Trigger: "Page View" + URL contains `thanks=1`
4. Tags → "GA4 Event" → 이벤트명 `lead_form_submit` → 위 트리거 연결
5. Preview → 테스트 폼 제출 → 이벤트 fire 확인

### 2.7 광고 채널 + 4개 픽셀 (2시간)

**광고 계정 가입**:
- Meta: https://business.facebook.com → 비즈니스 생성 → 광고 계정 + 페이지 + Pixel
- Google Ads: https://ads.google.com (전문가 모드)
- 네이버: https://searchad.naver.com → 가입 → 프리미엄 로그분석 신청

**GTM에 4개 픽셀 일괄**:
- Meta Pixel base code → GTM Custom HTML → 트리거 "All Pages"
- Meta "Lead" 이벤트 → 트리거 lead_form_submit
- Google Ads → Tools → Conversions → "Submit lead form" 전환 ID 발급 → GTM Google Ads Conversion 태그 → 트리거 lead_form_submit
- 네이버 프리미엄 로그분석 스크립트 → GTM Custom HTML → 트리거 "All Pages"
- 네이버 전환스크립트 → 트리거 lead_form_submit

**검증**:
- GTM Preview 모드 + Meta Pixel Helper + Google Tag Assistant
- 테스트 폼 제출 시 4개 채널 모두 fire 확인

---

## Day 2 완료 체크리스트 (E2E 검증)

- [ ] frisat.ai 접속 → SSL 정상 → 7섹션 모두 보임
- [ ] 모바일 뷰(Chrome DevTools) 정상
- [ ] Tally 폼 임베드 정상 작동
- [ ] 더미 폼 제출 → Make.com 실행 이력 Success → HubSpot Contact 자동 생성
- [ ] Cal.com 임베드 정상 → 더미 예약 → Google Calendar 동기화 + 알림 수신
- [ ] GA4 실시간 보고서에 본인 방문 잡힘
- [ ] GTM Preview에서 GA4·Meta·Google·네이버 4개 fire 확인
- [ ] UTM 파라미터 (`?utm_source=test&utm_campaign=test`) → Tally Hidden 필드 캡처 → HubSpot Contact 속성에 저장 확인
- [ ] 광고 4개 채널 계정 가입 완료

→ 8개 모두 ✅면 Day 3 광고 송출 진입 가능

---

## Day 3+ 광고 송출 + 검증

### Meta 광고 1차 (월 50만원)
- 캠페인 목표: Lead Generation
- 타겟: 한국, 25-45세, 관심사 "마케팅 자동화" / "B2B 마케팅" / "스타트업"
- 크리에이티브: Hero 헤드라인 그대로 + ICP 페인포인트 1개 강조 이미지 카피

### Google 검색광고 (월 30만원)
- 키워드: "AI 마케팅 자동화", "마케팅 시스템 구축", "인하우스 마케팅 AI", "마케팅 RPA", "AI 마케팅 컨설팅"
- 광고 카피: VP 한 줄 + CTA "무료 진단 신청"

### 네이버 검색광고 (월 30만원)
- 동일 키워드 + 한국어 자연 키워드 추가

### HubSpot 이메일 시퀀스 3통
- Day 0: 진단 신청 감사 + Cal.com 미팅 예약 안내
- Day 2: 진단 미팅 진행 사례 1건 공유 (사회적 증거)
- Day 7: Cat A/B/C 시스템 1개 디테일 (전문성 어필)

---

## 사이트 수정 요청 워크플로우

사용자/마케터가 사이트 변경 원할 때:

```
"Hero 헤드라인을 'AI 마케팅 전문가가 8주 안에 당신 팀에 이식됩니다'로 바꿔줘"
   ↓
Claude: index.html 해당 부분 Edit → git commit → push
   ↓
Vercel: 자동 감지 → 30초 내 재배포
   ↓
frisat.ai에 즉시 반영
```

**가능한 요청 예시**:
- "Problem 섹션 카드 순서 바꿔줘"
- "CTA 버튼 색을 더 진하게"
- "Reference에 '오키뷰티' 추가, 핵심 지표는 '신규 회원 380% 증가'로"
- "8주 타임라인의 5주차 산출물을 'Cat C 베타 운영' 으로 수정"
- "모바일에서 Hero 폰트 크기가 너무 큰 것 같아, 줄여줘"
- "전체 컬러를 노션 브랜드 가이드의 #1A2B4C(Primary)와 #FF6B35(Accent)로 교체"

→ **콘텐츠 마케터도 Claude에게 자연어로 요청만 하면 됨**. 코드 학습 불필요.

---

## 트러블슈팅

| 증상 | 해결 |
|---|---|
| frisat.ai 접속 안 됨 | DNS 전파 5-30분 대기. dnschecker.org에서 전파 상태 확인 |
| SSL 오류 | Vercel Settings → Domains → 도메인 옆 "Refresh" 클릭 |
| Tally 제출이 HubSpot에 안 옴 | Make.com 시나리오 실행 이력 확인. 활성화 토글 ON 확인 |
| Cal.com 임베드 안 보임 | iframe 차단 광고 차단기 끄고 재확인 |
| GA4 실시간에 본인 안 보임 | 광고 차단기·시크릿 모드 사용 |
| GTM 픽셀 fire 안 됨 | Preview 모드 활성화 + 트리거 조건 재확인 |
| Vercel 배포 실패 | GitHub Actions 로그 또는 Vercel 빌드 로그 확인 (정적 HTML이라 거의 실패 없음) |

---

## 정식 홈페이지 디벨롭 시점 (Future)

MVP 광고 검증 완료 후 (1-3개월 후 예상):
- 그때까지 메세지·오퍼·핵심 채널·CPL 수치가 데이터로 확정됨
- 정식 홈페이지: Framer / Webflow / Next.js 중 선택 (당시 팀·요구에 따라)
- MVP 카피·디자인은 검증된 자산이므로 신규 사이트로 이식
- 추가 기능: 블로그·케이스 CMS·다국어·로그인 등
