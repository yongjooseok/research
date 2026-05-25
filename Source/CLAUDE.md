# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## 0. 이 저장소의 성격

코드 저장소가 아니라 **리서치 워크플로우 저장소**다. 빌드·테스트·린트 명령이 없다. 모든 작업은 마크다운 파일 생성·수정·이동으로 이루어진다.

`~/work/research/Source/`는 리서치 4계층 아키텍처(Router → Plan → Source → Extract) 중 **Source tier** 폴더다. 책임 범위:

- Plan팀이 작성한 검색 계획서(`search_plan.md`)를 NotebookLM에서 실행
- 수집 결과·Gap Report를 다음 단계(Extract 또는 의뢰인 직결)에 인계

상위 README는 `README.md`, 페르소나는 `personas/research-collector.md` v0.1.

---

## 1. 폴더 경계 (하드 거절)

**다음 경로 변경 시도 시 즉시 거절 + 의뢰인 확인:**
- `~/work/research/Plan/` (모든 하위, 읽기만 허용)
- `~/work/research/Extract/` (모든 하위, 현재 미정의)

거절 메시지 형식:
> "Plan/Extract 폴더는 Source tier 권한 밖. Source 폴더 내 동등 작업이 있다면: [대체 경로 제안]. 그래도 진행하려면 명시 확인 필요."

**예외**: `~/work/research/README.md`, `~/work/research/Plan/CLAUDE.md`, `~/work/research/Plan/guides/*`는 읽기 허용 (참조용). Plan의 어떤 파일도 mtime 변경 금지.

---

## 2. 페르소나 자동 호출

### 2-1. 수집 페르소나
의뢰가 "수집 실행" / "search_plan 인계" / "NotebookLM 가동" / Plan output 인계 키워드 포함 시:
- 자동 호출: `personas/research-collector.md` v0.1
- Algorithm 5단계 순차 가동 (계획서 수신·검증 → 노트북 생성 → 수집 실행 → 품질 점검 → 보고서+환류)
- 산출물: `output/[YYYY-MM-DD][도메인] 주제_수집보고서.md` (잠정 양식 — Output Standards 미설계)

### 2-2. 페르소나 본분 (위반 시 작업 멈춤)
- **계획 변형 금지** — search_plan.md §1~§9 임의 해석·수정 X. 불명확 시 Plan팀 환류
- **결론 도출 금지** — Source는 수집 정직성만 책임 (Extract 영역·의뢰인 권한 침투 X)
- **갭 정직 보고** — 못 찾은 것·실패한 것 숨기지 않음 (§9-5 Gap Report 입력)

### 2-3. 페르소나 파일 직접 수정 금지
`personas/research-collector.md` 수정은 별도 의뢰 영역 (v0.1.x 패치 등). 자동 호출 작업은 페르소나 호출만 수행하고 파일 수정 시도 시 의뢰인 확인.

---

## 3. 핸드오프 인터페이스

### 3-1. Plan → Source 수신
- Plan 출력: `~/work/research/Plan/output/[YYYY-MM-DD][도메인] 주제.md`
- Source 입력: `~/work/research/Source/input/[YYYY-MM-DD][도메인] 주제.md` (파일명 동일 복사, Plan output 원본 불변)
- 인계 거부 조건 (`Plan/guides/handoff_interface.md` §2-2):
  - §1 메타 미완비
  - §3 핵심 질문 5개 미만
  - §5-1/5-2/5-3 확정 자료원 부재 또는 T1 < 2
  - §7 NotebookLM 실행 지시 누락
  - §9 Gap Report 골격 부재
- 거부 시 사유 명시 회신, Plan팀 보완 후 재인계.

### 3-2. Source → Plan 환류
- §9 전체 채워서 회수 (§9-5 Gap Report 포함)
- **회수 경로 [임시 결정 2026-05-24]**:
  - 경로: `~/work/research/Source/output/[YYYY-MM-DD][도메인] 주제_gap.md`
  - 영구성: 임시 (첫 실전 의뢰 1~2건 가동 후 재검토)
  - 근거: 모든 팀이 자기 폴더에만 쓰는 단순 권한 매트릭스 + D-G 정책 정합
  - 기각 옵션: `Plan/feedback/` 신설 (Plan tier D-G 하드 거절 정책과 충돌)

### 3-3. §5-4 후보 자료원 후처리
Plan이 §5-4에 분리해놓은 후보 자료원 각각에 대해:
1. 1차 확인 후 §5-1/5-2/5-3 본 표로 **승격** (확정 자료원으로)
2. 또는 **기각** (접근 불가·중복·부적합)
3. 결과를 §9-1 부족 자료 영역에 누적 기록

---

## 4. NotebookLM MCP 사용

Source tier의 본질적 권한이자 핵심 도구. Plan tier는 §7 지시서로 간접 위임만 했으나, Source는 직접 호출한다.

- 노트북 생성·소스 추가·메타 라벨 부착·분석 질의 실행 모두 MCP 도구 사용
- 소스 추가 순서: T1 → T2 → T3 (권위 등급 순)
- 메타 라벨 양식: `[T#|LANG|YYYY-MM-DD]`
- 인증 오류 시 사용자에게 `! nlm login` 안내 (Claude가 직접 실행 X)
- 노트북 URL·ID는 수집 보고서에 기록

검색 결과 빈약 시 검색어 변형은 자율 판단 영역. 변형 사유·시도 횟수 기록 의무.

---

## 5. 파일명 규약

도메인 라벨은 Plan팀 표준(`Plan/guides/domain_label_standard.md` §2 10종) 차용:
`[Mobile]` `[Desktop]` `[Web]` `[AI]` `[Security]` `[DevOps]` `[Data]` `[Tools]` `[Business]` `[Meta]`

- input/ 파일: Plan output 파일명을 **그대로 복사** (변경 금지)
- output/ 파일: `[YYYY-MM-DD][도메인] 주제_수집보고서.md` (잠정)
- 새 도메인 등장 시 Source가 임의 등재 금지 → Plan팀 §4 확장 절차 의뢰

---

## 6. 점검 의무 (즉시 작업 멈추고 보고)

다음 발견 시 즉시 멈춤 + 의뢰인 보고:

1. Plan/Extract 폴더 변경 시도 (§1 하드 거절 발동)
2. 페르소나 본분 위반 (§2-2 3건 중 1건 이상)
3. 페르소나 파일 직접 수정 필요 발견 (별도 의뢰 영역)
4. 회수 경로 임시 결정(§3-2) 외 경로로 §9-5 환류 시도 (예: `Plan/feedback/` 신설)
5. NotebookLM MCP 인증 만료 (사용자에게 `nlm login` 안내 후 대기)
6. 인계 파일이 §2-2 인계 거부 조건 1건 이상 해당 (재인계 요청)
7. 도메인 라벨 표준 외 라벨 발견 (Plan팀 확장 절차 의뢰)

---

## 7. 미정 항목 (가동 전 결정 필요)

`README.md` "미정 항목" 동기화:

1. **회수 경로** [임시 결정 2026-05-24] — 채택: `Source/output/[YYYY-MM-DD][도메인] 주제_gap.md` 누적 (§3-2 참조). 영구성: 임시 (첫 실전 의뢰 1~2건 가동 후 재검토)
2. **수집 보고서 양식** — `output-standards/collection-report.md` (Extract팀 정의 시점에 설계)
3. **NotebookLM MCP 권한 매트릭스 enforce 룰** — 페르소나 v0.1 검증 후 설계
4. **changelog 운영 여부** — Plan팀은 `guides/changelog.md` 운영. Source 누적량 발생 시 도입 검토.

---

## 8. 자산 인덱스 (참조 우선순위)

| 우선순위 | 자산 | 용도 |
|---|---|---|
| 1 | `personas/research-collector.md` | 수집 페르소나 (Algorithm 5단계) |
| 2 | `README.md` | 폴더 개요·미정 항목 |
| 3 | `Plan/guides/handoff_interface.md` (읽기) | Plan→Source 경계·인계 거부 조건 |
| 4 | `Plan/guides/domain_label_standard.md` (읽기) | 파일명 도메인 라벨 |
| 5 | `Plan/CLAUDE.md` (읽기) | Plan 측 규칙 (대칭 확인용) |
| 6 | `input/` | 인계받은 검색 계획서 |
| 7 | `output/` | 수집 보고서·Gap Report |

---

## 9. 등재 기록

- 등재일: 2026-05-24
- 등재 사유: Source 폴더 셋업 직후 `/init` (요청서 `claude-code-source-setup-request.md` 후속)
- 의존 결정값: Plan/CLAUDE.md §0·§5 (대칭), 페르소나 v0.1 본분 3건
- 다음 갱신 트리거: 회수 경로 재검토 (임시 결정 종료 시점, 첫 실전 의뢰 1~2건 가동 후) / 수집 보고서 양식 설계 / 페르소나 v0.1.x 패치
