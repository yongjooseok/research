# Source팀

리서치 4계층 아키텍처(Router → Plan → Source → Extract) 중 **Source tier**.

## 역할

Plan팀이 작성한 검색 계획서(`search_plan.md`)를 NotebookLM에서 정확히 실행하여, 수집 결과·갭 보고를 다음 단계(Extract 또는 의뢰인 직결)에 전달한다.

## 폴더 구조

- `input/` — Plan/output/에서 인계받은 검색 계획서 사본
- `output/` — 수집 보고서 및 Gap Report (§9-5)
- `personas/` — Source 페르소나 정의

## 페르소나

- `research-collector` v0.1 (`personas/research-collector.md`)
  - 검색 계획서 실행 전문가
  - NotebookLM MCP 직접 접근 권한 보유

## 인계 인터페이스

- **수신**: `Plan/output/[YYYY-MM-DD][도메인] 주제.md` → `Source/input/` (파일명 동일 복사)
- **환류**: §9-5 Gap Report → Plan팀 (회수 경로 미정, Source 가동 첫 결정 항목)
- 상세 규칙: `Plan/guides/handoff_interface.md`

## 미정 항목 (가동 전 결정 필요)

1. **회수 경로** [임시 결정 2026-05-24]
   - 채택: 옵션 ② `Source/output/[YYYY-MM-DD][도메인] 주제_gap.md` 누적
   - 영구성: 임시 (첫 실전 의뢰 1~2건 가동 후 재검토)
   - 근거: 모든 팀이 자기 폴더에만 쓰는 단순 권한 매트릭스 + D-G 정책 정합
   - 기각 옵션: `Plan/feedback/` 신설 (Plan tier D-G 하드 거절 정책과 충돌)
2. **Source/CLAUDE.md** — `/init`으로 별도 생성 예정
3. **수집 보고서 양식** — `output-standards/collection-report.md` (Extract팀 정의 시점에 설계)
4. **NotebookLM MCP 권한 매트릭스 enforce 룰** — 페르소나 v0.1 검증 후 설계

## 현재 상태

- 페르소나 v0.1 배치 완료
- CLAUDE.md 미작성 (수령 후 `/init`)
- 실전 의뢰 0건 — Plan/output/ 산출물 중 v0.1.2 패치 + D-C 재정비 완료분부터 인계 예정
