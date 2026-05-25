# Claude Code 작업 의뢰서 — Plan/guides/handoff_interface.md 정합 패치

> 작성: Source팀 (Claude Code 보조)
> 작성일: 2026-05-24
> 작업 위치: `~/work/research/Plan/guides/handoff_interface.md`
> 범위: 회수 경로 표기 1회 패치 (§2 표·§4-1 본문·§5 상태표·§6 변경 이력)
> 작업 주체: **Plan팀 (별도 세션)** — Source는 Plan/ 변경 권한 없음

---

## 0. 한 줄 요약

Source팀이 2026-05-24 임시 결정한 회수 경로(`Source/output/[YYYY-MM-DD][도메인] 주제_gap.md` 누적)를 Plan/guides/handoff_interface.md에 동기화. 기존 `Plan/feedback/` 신설 가정 3곳 수정 + 변경 이력 1행 추가.

---

## 1. 사전 컨텍스트

### 1-1. 결정 이력

- **2026-05-24 Source 측 결정** (의뢰서: `~/work/research/Source/claude-code-handoff-interface-sync-request.md` 작성과 동일 세션):
  - 채택: 옵션 ② `Source/output/[YYYY-MM-DD][도메인] 주제_gap.md` 누적
  - 영구성: **임시** (첫 실전 의뢰 1~2건 가동 후 재검토)
  - 근거: 모든 팀이 자기 폴더에만 쓰는 단순 권한 매트릭스 + Plan D-G 하드 거절 정책 정합
  - 기각 옵션: `Plan/feedback/` 신설 (Plan tier D-G 하드 거절 정책과 충돌)
- **반영 완료 자산**:
  - `Source/CLAUDE.md` §3-2·§6-4·§7-1·§9 (4곳)
  - `Source/README.md` 미정 항목 §1
- **미반영 자산** (본 의뢰서 대상):
  - `Plan/guides/handoff_interface.md` §2 표 L40 / §4-1 본문 L103~106 / §5 상태표 L122 / §6 변경 이력
  - `Plan/CLAUDE.md` §5 (`Plan/feedback/[YYYY-MM-DD][도메인] 주제_gap.md` 가정) — 본 의뢰서 §3-2 작업 5에서 함께 처리할지 결정 필요

### 1-2. 참조 문서

- `~/work/research/Source/CLAUDE.md` §3-2 (회수 경로 임시 결정 본문)
- `~/work/research/Source/README.md` "미정 항목" §1 (채택·근거·기각 옵션)
- `~/work/research/Plan/guides/handoff_interface.md` (수정 대상 본문)
- `~/work/research/Plan/CLAUDE.md` §5 (대칭 갱신 대상 후보)

---

## 2. 작업 1 — §2 핸드오프 경로 표 수정

### 2-1. 위치

`Plan/guides/handoff_interface.md` L37~40 표 마지막 행

### 2-2. 현재 본문

```markdown
| 항목 | 규약 |
|---|---|
| Plan 출력 경로 | `~/work/research/Plan/output/[YYYY-MM-DD][도메인] 주제.md` |
| Source 입력 경로 | `~/work/research/Source/input/[YYYY-MM-DD][도메인] 주제.md` |
| 인계 방식 | 파일명 그대로 복사 (Plan output 원본 보존) |
| Source → Plan 회수 경로 | `~/work/research/Plan/feedback/[YYYY-MM-DD][도메인] 주제_gap.md` (신설 예정) |
```

### 2-3. 변경 본문

```markdown
| 항목 | 규약 |
|---|---|
| Plan 출력 경로 | `~/work/research/Plan/output/[YYYY-MM-DD][도메인] 주제.md` |
| Source 입력 경로 | `~/work/research/Source/input/[YYYY-MM-DD][도메인] 주제.md` |
| 인계 방식 | 파일명 그대로 복사 (Plan output 원본 보존) |
| Source → Plan 회수 경로 | `~/work/research/Source/output/[YYYY-MM-DD][도메인] 주제_gap.md` **[임시 결정 2026-05-24]** |
```

**수정 요점**: 경로 `Plan/feedback/` → `Source/output/`, "(신설 예정)" → "**[임시 결정 2026-05-24]**"

---

## 3. 작업 2 — §4-1 회수 경로 본문 수정

### 3-1. 위치

`Plan/guides/handoff_interface.md` L103~106 (§4-1 회수 경로)

### 3-2. 현재 본문

```markdown
### 4-1. 회수 경로
- 파일: `Plan/feedback/[YYYY-MM-DD][도메인] 주제_gap.md`
- 원본 Plan output은 불변 (히스토리 보존)
- gap 파일은 §9만 분리해서 회수 (전체 복사 X)
```

### 3-3. 변경 본문

```markdown
### 4-1. 회수 경로 [임시 결정 2026-05-24]
- 파일: `~/work/research/Source/output/[YYYY-MM-DD][도메인] 주제_gap.md`
- 원본 Plan output은 불변 (히스토리 보존)
- gap 파일은 §9만 분리해서 회수 (전체 복사 X)
- **영구성**: 임시 (첫 실전 의뢰 1~2건 가동 후 재검토)
- **근거**: 모든 팀이 자기 폴더에만 쓰는 단순 권한 매트릭스 + D-G 하드 거절 정책 정합
- **기각 옵션**: `Plan/feedback/` 신설 (D-G 정책 충돌)
- Plan 측 후처리: §4-2 절차로 `Source/output/*_gap.md` 풀(pull)
```

**수정 요점**:
- 헤더에 "[임시 결정 2026-05-24]" 추가
- 파일 경로 `Plan/feedback/` → `~/work/research/Source/output/`
- 영구성·근거·기각 옵션 3행 신설 (Source/README §1 미정 항목과 동기화)
- 마지막 행에 Plan 측 후처리 방식 명시 (풀 모델)

---

## 4. 작업 3 — §5 현재 상태 표 갱신

### 4-1. 위치

`Plan/guides/handoff_interface.md` L118~123 (§5 현재 상태 표)

### 4-2. 현재 본문

```markdown
| 구성요소 | 상태 |
|---|---|
| Plan 측 인터페이스 명문화 | ✅ 본 문서 |
| Source 폴더 존재 | ❌ 미정의 |
| 회수 경로 `Plan/feedback/` 신설 | ⏸ Source 가동 시 |
| §9-5 실회수 | ⏸ Source 가동 시 |
```

### 4-3. 변경 본문

```markdown
| 구성요소 | 상태 |
|---|---|
| Plan 측 인터페이스 명문화 | ✅ 본 문서 |
| Source 폴더 존재 | ✅ 2026-05-24 셋업 완료 |
| 회수 경로 결정 | 🟡 임시 결정 (Source/output/ 누적, 2026-05-24) |
| §9-5 실회수 | ⏸ 첫 실전 의뢰 가동 시 |
```

**수정 요점**:
- Source 폴더 존재: ❌ → ✅ (2026-05-24 셋업 완료)
- 회수 경로 행 텍스트 변경 + 상태 ⏸ → 🟡 (임시 결정 표시)
- §9-5 실회수: "Source 가동 시" → "첫 실전 의뢰 가동 시" (Source 페르소나 v0.1 배치는 이미 완료, 정확한 트리거는 의뢰 가동)

---

## 5. 작업 4 — §6 변경 이력 1행 추가

### 5-1. 위치

`Plan/guides/handoff_interface.md` L129~130 (§6 변경 이력 마지막)

### 5-2. 추가할 행

기존 행 다음에 1행 추가:

```markdown
- 2026-05-24: 회수 경로 임시 결정 반영 (Source/output/ 누적). §2 표·§4-1 본문·§5 상태표 동기화. 영구 결정은 첫 실전 의뢰 1~2건 가동 후 재검토.
```

### 5-3. changelog 기록 의무 (Plan/CLAUDE.md §6 의무)

`Plan/guides/changelog.md`에도 세션 단위 엔트리 추가:
- 의뢰 출처: 본 의뢰서 (Source/claude-code-handoff-interface-sync-request.md)
- 변경 자산: handoff_interface.md (§2·§4-1·§5·§6)
- 변경 사유: Source 측 회수 경로 임시 결정 동기화

---

## 6. 작업 5 (조건부) — Plan/CLAUDE.md §5 갱신

### 6-1. 의사결정 필요

`Plan/CLAUDE.md` §5 본문에 다음 행이 있음:

```markdown
- 회수: `Plan/feedback/[YYYY-MM-DD][도메인] 주제_gap.md` (가동 후 신설)
```

이 행도 본 의뢰서로 함께 갱신할지 분리할지 Plan팀 결정.

### 6-2. 갱신 시 변경안

```markdown
- 회수: `~/work/research/Source/output/[YYYY-MM-DD][도메인] 주제_gap.md` [임시 결정 2026-05-24]
```

### 6-3. 분리 권고 시점

Plan/CLAUDE.md는 자동 참조 규칙이므로 변경 시 영향 범위가 더 큼. handoff_interface.md 갱신 검증 완료 후 별도 의뢰서로 처리하는 것도 가능.

---

## 7. 금지 사항 (Hard Constraints)

다음은 **어떤 경우에도 수행 금지**. 시도 시 작업 중단 + 보고:

1. **`~/work/research/Source/` 폴더의 어떤 파일도 변경 금지** (Source 측 결정값은 이미 반영 완료. 본 의뢰는 Plan 측 동기화)
2. **"임시" 표기 누락 금지** — §2·§4-1·§5·§6 모두 "임시 결정 2026-05-24" 또는 "임시" 단어 포함
3. **영구 결정으로 격상 금지** — Source 측 결정은 임시. Plan 측에서 임의로 영구 결정으로 승격하지 말 것
4. **재검토 트리거 명시 유지** — "첫 실전 의뢰 1~2건 가동 후 재검토" 문구 §4-1·§6에 보존
5. **`Plan/feedback/` 폴더 신설 금지** — 임시 결정에서 기각된 옵션. 신설 시도 시 작업 중단

---

## 8. 검증 체크리스트

작업 완료 후 다음 모두 확인하고 보고:

- [ ] §2 표 마지막 행: `Source/output/...주제_gap.md` + `[임시 결정 2026-05-24]` 포함
- [ ] §4-1 헤더에 "[임시 결정 2026-05-24]"
- [ ] §4-1 파일 경로 `~/work/research/Source/output/`
- [ ] §4-1 본문에 영구성·근거·기각 옵션 3행 추가
- [ ] §5 상태표: Source 폴더 존재 ✅, 회수 경로 🟡 임시 결정
- [ ] §6 변경 이력 2026-05-24 행 추가
- [ ] `guides/changelog.md` 세션 엔트리 추가 (Plan/CLAUDE.md §6 의무)
- [ ] `~/work/research/Source/` 폴더 내 파일 mtime 변경 없음
- [ ] `Plan/feedback/` 폴더 신설되지 않음
- [ ] 작업 5 (Plan/CLAUDE.md §5) 처리 방침 보고 — 함께 갱신 / 별도 의뢰 분리 중 선택

---

## 9. 보고 형식

작업 종료 시 다음 5가지 보고:

1. 변경된 파일 목록 (`git status -s ~/work/research/Plan/` 결과)
2. §8 체크리스트 통과/실패 항목
3. 작업 5 처리 방침 (함께 갱신 했는지 / 별도 의뢰 분리 권고인지)
4. 발견된 이슈·결정 필요 항목
5. Source 측 후속 작업 권고 (있을 경우)

---

## 10. 결정 필요 마커 (의뢰서 자체)

본 의뢰서가 의도적으로 결정을 보류한 항목 2건:

1. **작업 5 (Plan/CLAUDE.md §5) 통합 여부** — 본 의뢰서로 함께 처리 vs 별도 의뢰. Plan팀 판단 위임 (§6 참조)
2. **영구 결정 시점** — 현재는 "첫 실전 의뢰 1~2건 가동 후". 정확한 회수(回收) 시점은 첫 실전 의뢰 완료 후 별도 의뢰서로 처리

---

## 11. 부록 — 임시 결정 표기 일관성 참조

다음 4자산이 "임시 결정 2026-05-24" 위상으로 동기화됨을 확인:

| 자산 | 위치 | 표기 |
|---|---|---|
| Source/CLAUDE.md §3-2 | L66 | `**회수 경로 [임시 결정 2026-05-24]**` |
| Source/CLAUDE.md §7-1 | L123 | `**회수 경로** [임시 결정 2026-05-24]` |
| Source/README.md 미정 항목 §1 | L29 | `**회수 경로** [임시 결정 2026-05-24]` |
| Plan/guides/handoff_interface.md | (본 의뢰 후) | §2·§4-1·§5·§6 동기화 |

Plan/CLAUDE.md §5는 작업 5 결정에 따라 5번째 자산으로 합류 가능.

---

**의뢰서 종료. Plan팀 작업 착수 가능.**
