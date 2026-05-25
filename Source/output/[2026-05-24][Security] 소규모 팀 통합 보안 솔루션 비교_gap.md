# Gap Report — 소규모 팀(5~20명) 통합 보안 솔루션 비교

> Source팀 두 번째 실전 의뢰. Plan §9 골격을 채워서 회수.

---

## 0. 메타

| 항목 | 내용 |
|---|---|
| 원본 Plan | `~/work/research/Plan/output/[2026-05-24][Security] 소규모 팀 통합 보안 솔루션 비교.md` |
| 수집 실행일 | 2026-05-24 |
| 가동 페르소나 | `research-collector` v0.1 (Algorithm 5단계 전수) |
| 자율 권한 수준 | Plan 잤그대로 유지 (Joo 결정, 2026-05-24) — 자율 소스 보강 금지, 검색어 변형만 허용 |
| NotebookLM 노트북 | [2026-05-24][Security] 소규모 팀 통합 보안 솔루션 비교 |
| 노트북 ID | `1d1623b3-cf23-40d5-936d-2c6d734fc784` |
| 노트북 URL | https://notebooklm.google.com/notebook/1d1623b3-cf23-40d5-936d-2c6d734fc784 |
| 노트북 노트 | "소스 메타 라벨 (Plan §7-3)" (note_id: `08a3db50-93a9-467e-aa94-bc4c80b51ee4`) |
| 총 소스 적재 | 39건 시도 / 36건 NotebookLM 적재 / **실질 콘텐츠 가용 29건** |
| Tier 비율 (실질) | T1 62% (18/29) / T2 14% (4/29) / T3 31% (9/29) |
| Q 답 가능성 | 8 중 7 완전 답 / 1 갭 (Q6 한국어 도입 사례) |

---

## 9-1. 부족했던 자료 영역

### 1) 한국어 도입 사례 0건 — 의뢰의 핵심 결정 3에 직접 타격

Plan §2-1 핵심 결정 3 (글로벌 vs 한국 가용성 우선 도구 선택)에 직결되는 한국어 도입 사례·후기·비교 자료가 **전체 0건**.

- OKKY·Disquiet 메인 페이지만 적재 (각 사이트 자체 검색 SPA로 실패)
- 카카오테크·토스테크·LINE Engineering 자체 검색 SPA로 메인 fallback
- 우아한형제 자체 검색 보안 차단
- 베스핀글로벌·메가존클라우드·NHN Cloud 메인 페이지만 적재 (Tauri 의뢰 동일 한계)
- Medium @daangn 적재 실패

**근본 원인**: Plan §5-3에 한국어 자료 풍부 소스(Velog `보안` 태그 페이지 등)가 미등재. Tauri 의뢰에서 Velog 태그가 한국어 자료 13건의 핵심이었던 패턴이 Security에 반영 안 됨.

### 2) T2 한국 매체 자료 적재 실패

- KISA: 자체 검색 URL이 메인 fallback
- IT World Korea: 자체 검색 URL이 404 ("페이지를 찾을 수 없습니다")
- 결과: T2 실질 가용 4/7 (Plan §6 T2 ≥ 25% 목표에 14%로 미달)

### 3) Capterra 적재 실패

- T1 슬롯 4 G2/Capterra/Gartner 중 Capterra가 Cloudflare 봇 차단으로 적재 실패
- G2 1건만 가용 (다행히 "Best Password Managers for Small Business 2026" 페이지로 Q1-Q2 응답 핵심 역할)

### 4) Plan §2-2-1 단정 5종 중 2종이 G2 password manager 카테고리 미포함

- Bitwarden·1Password·NordLayer는 G2 카테고리에 표시되어 검증 통과
- **Tailscale·JumpCloud는 G2 password manager 카테고리에 미표시** (Tailscale은 Business VPN/ZTNA, JumpCloud는 IAM/Directory 카테고리에 주로 분류)
- Q1에서 G2 결과는 Dashlane·Keeper·Rippling 3종을 새로 발견 — 페르소나가 단정한 "통합 보안" 범주가 좁음

### 5) Bitwarden 공식 `/security/` 페이지 부재

- `https://bitwarden.com/security/`는 404
- Bitwarden 보안 정보는 `/pricing/` 페이지 하단 FAQ·메인 페이지에 분산 (적재 후 검증)
- 변형 보강 시도 `/help/article/bitwarden-security-faqs/`도 404 (URL 패턴 오래됨)

### 6) NordLayer `/security/` 페이지 제목 추출 미흡

- 적재 시 title이 URL 자체로 표시됨 (`https://nordlayer.com/security/`)
- 단, 본문 fetch는 정상 (Q5 컴플라이언스 응답에서 ISO 27001·SOC 2 Type I·HIPAA·PCI-DSS 정보 추출됨)

### 7) ISMS-P (한국 정보보호 인증) 미확인

- Plan §2-2-7에서 "ISMS·SOC 2·ISO 27001·GDPR" 명시했으나 5개 제품 어디에도 ISMS 보유 명시 없음
- 한국 진출 글로벌 SaaS 중 ISMS-P 보유 사례 별도 검색 권고 (한국 정부·공공·금융 도입 결정에 필수)

---

## 9-2. 추가로 발급/연동했어야 할 API

- **G2 API**: Plan §5-1 row 4 "G2/Capterra/Gartner" 중 G2 웹 페이지만 fetch 성공. Capterra·Gartner는 API 또는 RSS 필요
- **Reddit API**: r/sysadmin·r/cybersecurity 서브레딧 메인 fetch는 정상이나, 특정 thread 검색 결과는 적재 안 됨. Reddit API로 thread 검색 + JSON 응답 사용 권고
- **YouTube Data API**: 한국어 검색 결과 페이지가 JS 의존이라 적재 실패. API로 메타·자막 수집 권고
- **한국 매체 RSS**: KISA·IT World Korea·Datanet·Bloter 모두 RSS 제공 가능성 (검색 URL 대신 RSS 등재 권고)

---

## 9-3. 다음 유사 주제에서 추가할 자료원

SaaS 비교 의뢰 (Security·DevOps·Data 도구 등) 시 다음을 §5-1~§5-3에 사전 등재 권장:

### T1 보강
- **G2 카테고리 페이지를 도구 영역별로 명시** (예: "Password Manager Small Business" + "Business VPN" + "Endpoint Management" 각각). Tauri+Security 두 의뢰 모두 G2 페이지가 핵심 정보원이었음 (도메인 프로파일 ★★★★★)
- **각 제품 G2 리뷰 페이지 직접 URL** (예: `g2.com/products/{slug}/reviews`) — 도입 후기 정량 데이터
- **Trustpilot·SoftwareReviews** — Gartner 대체 가능 (로그인 불필요)

### T2 보강
- **각 매체 RSS feed** — site:Google 검색식 대신
- **The Verge·TechCrunch 자체 검색 결과 페이지** (Tauri+Security 둘 다 정상 fetch 확인됨)

### T3 보강 (한국어)
- **Velog 태그 페이지** (예: `velog.io/tags/비밀번호관리`, `velog.io/tags/bitwarden`) — Tauri 의뢰에서 한국어 자료 13건의 핵심이었음. **Security 의뢰에는 미등재된 것이 결정적 갭 원인**
- **Awesome Korean Security** 등 한국어 큐레이션 repo
- **dev.kr·GeekNews 한국어 카테고리**
- **한국 기업 RSS feed** (카카오테크·토스테크·우아한형제는 모두 RSS 제공) — site:Google 검색식 폐기

---

## 9-4. 도메인 프로파일 승격 후보

**도메인: SaaS 비교 (Security·DevOps·Data 등 통합)**

Tauri 의뢰는 "Desktop Application Framework", 본 의뢰는 "Security SaaS 비교" — 두 도메인은 다르나 다음 패턴은 도메인 무관 재사용 가치 ★★★★★

### T1 패턴 (공통 — 두 의뢰 모두 검증 통과)
- 각 제품 메인 + `/pricing` + `/security` 또는 `/compliance` 3페이지 묶음 — Q3·Q4·Q5·Q7·Q8 답변 핵심
- G2 카테고리 페이지 — Q1 (제품 식별) + Q2 (커버 영역) 답변 핵심

### T3 패턴 (Tauri 의뢰에서 검증된 한국어 자료 인프라)
- **Velog 태그 페이지**: 한국어 도입 사례·후기 1순위 (Tauri 13건 적재 성공)
- Reddit 서브레딧 메인: 영어 사용자 후기 1순위
- HackerNews Algolia 검색: 영어 thread 토픽 1순위

→ **"SaaS 비교 도메인 프로파일" 본 의뢰로 v0.1 형성. Tauri 의뢰로 검증된 한국어 인프라를 SaaS 비교에도 적용 권고.**

### T1 패턴 (보안 도메인 특화)
- 각 제품 Trust Center 페이지 (예: `bitwarden.com/trust/`, `tailscale.com/security/`) — 컴플라이언스 인증 1차 자료
- 각 제품 SOC 2 Report (NDA 필요) — 깊은 분석 필요시
- ISMS-P 보유 글로벌 SaaS 목록 (한국 KISA 인증 페이지) — 한국 공공·금융 도입 시 필수

---

## 9-5. Plan 사실관계 검증 결과

Plan 본문에 들어간 작성자 단정 (`[?]` 마커 부착 항목) ↔ NotebookLM 적재 자료 일치 여부 사후 점검.

| Plan 위치 | 단정 내용 | 마커 | NotebookLM 확인 결과 |
|---|---|---|---|
| §1 Meta | 도메인 "Security" | `[? 분류 체계 전제 미확인]` | ✅ **검증**. Plan팀 표준 §2에 `[Security]` 존재 (도메인 라벨 표준 §2 10종 중 1건). 마커 제거 가능. **Plan 측 일관성 이슈**: 표준 라벨인데 마커가 부착됨. |
| §2-2-1 | 통합 보안 SaaS 5종 (Bitwarden·1Password·NordLayer·Tailscale·JumpCloud) | `[? LLM 추정]` | 🟡 **부분 검증**. Bitwarden·1Password·NordLayer는 G2 password manager SMB 카테고리에 표시 ✅. **Tailscale·JumpCloud는 G2 password manager 미포함** (각각 VPN·IAM 카테고리). 새 발견 3종 (Dashlane·Keeper·Rippling IT). 마커는 "범주 광의 필요"로 변형 권고. |
| §2-2-2 | 각 제품 커버 영역 | `[? LLM 추정]` | ✅ **검증**. 8제품×4영역 매트릭스 완성 (비밀번호·VPN·디바이스·SSO+IAM). 1Password·NordLayer·Keeper·JumpCloud가 통합 영역 가장 넓음. 마커 제거 가능. |
| §2-2-3 | 5~20명 가격 모델 | `[? LLM 추정]` | ✅ **검증**. 5제품 가격·할인·최소 사용자 수 완전 정리 (Bitwarden $4/Teams, 1Password $19.95/Starter, NordLayer $8 5명 최소, Tailscale $8/$0 6명, JumpCloud $9~$13). 마커 제거 가능. |
| §2-2-4 | 한국 결제·UI·고객지원 | `[? LLM 추정]` | ✅ **검증**. **1Password만 한국어 UI 공식 명시**. 나머지 4종은 한국 결제·한국어 UI·한국 고객지원 모두 "공식 명시 없음". 마커 제거 가능. |
| §2-2-7 | 컴플라이언스 인증 | `[? LLM 추정]` | ✅ **검증**. Bitwarden 가장 광범위 (ISO 27001·SOC 2 Type II·SOC 3·GDPR·CCPA·HIPAA·DPF). Tailscale은 데이터 비저장으로 HIPAA out-of-scope. **ISMS-P 한국 인증은 5개 제품 어디에도 명시 없음 (Plan 단정 안 했으나 한국 도입 시 핵심)**. 마커 제거 가능. |
| §5-1 row 1~4 | 공식 사이트 URL | `[? LLM 추정]` / `[? 30초 룰 위반]` | 🟡 **부분 검증**. 18/22 URL 정상 적재. **실패 4건**: Bitwarden `/security/` (404), Bitwarden security FAQs 변형 (404), Capterra (Cloudflare 차단), NordLayer `/security/` 제목 추출 미흡. 마커 대부분 제거 가능. |
| §5-2 전 행 | T2 매체 보안 도구 기사 | `[? LLM 추정]` | 🟡 **부분 검증**. EN 4종 (The Verge·TechCrunch·Ars·Krebs) 자체 검색 페이지 ✅. KO 2종 (KISA·IT World Korea) 적재 실패. T2 실질 14%로 Plan §6 목표 ≥25% 미달. |
| §5-3 row 1·2·4·5·6 | T3 한국·영문 자료 | `[? LLM 추정]` | 🟡 **부분 검증**. Reddit r/sysadmin·r/cybersecurity ✅, HackerNews Algolia ✅, OKKY·Disquiet 메인 ✅, 한국 SI/MSP 3사 메인 ✅. **단 자체 검색 결과·구체 thread는 미적재** (메인 페이지만). Q6 한국어 사례 응답에 활용 못 함. |
| §5-3 row 3 | 한국 스타트업 블로그 보안 도구 후기 | `[? 검증 안 함: 일반적 인상]` | ❌ **검증 실패 (갭)**. 카카오테크·토스테크·LINE Engineering 모두 메인 fallback (SPA 검색 결과 미렌더). 우아한형제 자체 검색 보안 차단. **한국 스타트업 블로그에 Bitwarden·1Password 등 도입 후기 자체가 부재할 가능성 (콘텐츠 갭)**. |

### 집계

- **검증 통과**: **6건** (§1 도메인, §2-2-2 커버 영역, §2-2-3 가격, §2-2-4 한국 지원, §2-2-7 컴플라이언스, §5-1 부분 검증 포함 시 7건)
- **부분 검증**: **3~4건** (§2-2-1 제품 5종, §5-1 URL, §5-2 T2, §5-3 T3 일부)
- **검증 실패 (갭)**: **1건** (§5-3 row 3 한국 스타트업 블로그 보안 도구 후기)
- **Q6 한국어 도입 사례 응답**: **갭 0건** (적재 인프라 부재가 직접 원인)
- **마커 `[?]`로 표시되어 Source가 확인한 항목**: **10건 전수**

### 다음 Plan 작성 시 참고할 패턴

1. **SaaS 비교 의뢰 패턴 v0.1**: G2 카테고리 페이지가 제품 식별·커버 영역의 1차 자료. Plan 단계에서 **정확한 G2 카테고리 슬러그를 사전 확인** 권고 (예: `password-manager?segment=small-business`, `business-vpn`, `endpoint-management`).
2. **"통합 보안 SaaS"는 광의 정의 필요**: 비밀번호 관리·VPN·디바이스 보안이 한 카테고리에 묶이지 않음. Plan 단계에서 카테고리 매핑 사전 작업 권고.
3. **한국어 자료 정리는 Velog 태그 페이지를 1순위**: Tauri 의뢰에서 검증된 패턴. 본 Security 의뢰에 미등재된 것이 한국어 사례 0건의 직접 원인.
4. **공식 `/security/` 페이지 URL은 제품마다 다름**: Bitwarden은 `/trust/` 또는 `/help/`에 분산. Plan 단계에서 30초 룰로 각 제품별 정확한 URL 확인 권고.
5. **G2 외 Capterra·Gartner는 봇 차단**: Cloudflare WAF로 NotebookLM fetch 실패. 대안 출처(Trustpilot·SoftwareReviews) 권고.
6. **ISMS-P 한국 인증 자료**: 한국 공공·금융·대기업 도입 결정 시 필수. Plan §2-2-7 또는 §5-1에 한국 KISA 인증 페이지 사전 등재 권고.

---

## 추가: 변형 검색 사유·횟수 (Algorithm step 3 자율 판단 기록)

| 회차 | 자료원 | 변형 사유 | 결과 |
|---|---|---|---|
| 1 | Bitwarden `/security/` (T1) | 404 페이지 | `bitwarden.com/help/article/bitwarden-security-faqs/` 변형 → 404 |
| 1 | The Verge·TechCrunch·Wirecutter·Ars·Krebs (T2) | Google `site:` 봇 차단 | 각 매체 자체 검색 URL → 4/5 성공 (Wirecutter 적재 실패) |
| 1 | IT World Korea·KISA (T2) | 동상 | 자체 검색 URL → 0/2 (404 + 메인 fallback) |
| 1 | Reddit r/sysadmin·r/cybersecurity (T3) | 검색식 URL 부담 | 서브레딧 메인 + HackerNews Algolia → 3/3 성공 |
| 1 | OKKY·Disquiet (T3) | site:검색식 | 메인 페이지 → 2/2 (메인만, 검색 결과 없음) |
| 1 | 우아한형제·토스·카카오·라인 (T3) | site:검색식 | 각 자체 검색 URL → 1/4 (LINE 메인만, 나머지 SPA fallback) |
| 1 | YouTube 한국어 (T3) | 검색식 → JS 빈 페이지 | results URL → 적재 실패 |
| 1 | Medium @daangn (T3) | site:검색식 | medium.com/daangn URL → 적재 실패 |
| 1 | 베스핀글로벌·메가존·NHN Cloud (T3) | site:검색식 | 메인 페이지 → 3/3 (메인만) |

**총 변형 시도: 26건. 성공 17건, 실패 9건.** 페르소나 본분상 추가 변형 중단 + 갭 정직 기록.

---

## 추가: D-C 정책 부재 + 도메인 라벨 마커 환류 (Plan팀 별도 의뢰 권고)

본 Plan에서 두 가지 정합성 이슈 동시 발견:

### 1) §5-4 후보 자료원 섹션 부재 (Tauri 의뢰와 동일 패턴)

`handoff_interface.md` §3-2~§3-4 D-C 정책 미적용. `[? 30초 룰 위반]` 0건이라고 페르소나가 자체 명시했으나, 다수 `[? LLM 추정]` 자료원이 본 표(§5-1~§5-3)에 등재. Tauri Gap Report와 동일 환류.

### 2) 표준 도메인 라벨에 `[? 분류 체계 전제 미확인]` 마커 부착

- Plan §1 Meta: `[Security]` `[? 분류 체계 전제 미확인]`
- 그러나 `domain_label_standard.md` §2에 `[Security]`는 10종 표준 중 1건으로 명시
- 페르소나가 자체 결정한 라벨이 표준 안인데 마커가 부착됨
- **이는 `Plan/CLAUDE.md` §7-7 "의뢰서에 도메인 라벨 미명시 + 페르소나 자체 결정한 라벨에 마커 부착 시도" 케이스**. CLAUDE.md §7-7은 "표준 §2에서 적합 라벨 선택 또는 의뢰인 재확인"으로 처리하라고 명시했으나, 본 Plan은 마커를 부착한 채 산출.

**Plan팀 권고**:
1. `research-strategist-hypothesis` v0.1.x Algorithm step 1 (의뢰 분해)에 도메인 라벨 표준 체크 의무 추가
2. 도메인 라벨이 표준 §2에 있으면 마커 부착 금지 (Plan/CLAUDE.md §7-7 강제)
3. §5-4 분리 의무도 Tauri Gap Report 권고와 동일

별도 의뢰서 가능 영역. 본 의뢰서로 결정하지 않음 (Source 권한 밖).
