# 검색 플랜 시스템 변경 로그

`research/Plan/` 시스템(템플릿·가이드·체크리스트·메모리·평가 보고서)의 의도된 변경을 시간순으로 기록.
사실값(버전·통계)이 아닌 **시스템 양식/규칙 변경**만 기록 — Plan 본체 산출물 변경은 각 파일 자체에 인라인으로 남김.

기록 단위: 작업 세션. 한 세션이 여러 파일을 손대도 한 엔트리로 묶음.

---

## 2026-05-23 (세션 3) — 신규 Plan: Expo CLI 설치 전 준비물

### 배경
사용자 요청으로 새 주제 Plan 작성. 시스템 워크플로우상 "검색 보고서"는 Source 단계의 NotebookLM 산출물이므로, 본 작업은 그 전 단계인 Plan 작성으로 진행 (사용자 확인 완료).

### 변경 내역
- 신규 파일: `output/[2026-05-23][Mobile] Expo CLI 설치 전 준비물.md`
- 5종 사유 카테고리 적용 분포 (작성자 자체 집계, 9-5 사후 검증 전 추정):
  - `[?] LLM 추정`: 다수 (Node 버전·watchman·JDK·Xcode 요구치, 자료원 적합성 등)
  - `[?] 분류 체계 전제 미확인`: 4건 (CLI 설치 방식, OS 분류, Expo Go 범위, 옛/현 expo-cli 구분)
  - `[?] 30초 룰 위반`: 2건 (공식 docs 페이지 경로·Reddit 상위 정의 기준)
  - `[?] 검증 안 함: 일반적 인상`: 1건 (입문자 흔한 막힘 항목)
- 7-3 메타 라벨링 예시에 버전·날짜 사실값 미기재 (형식만 노출)
- 자료원 적합성 단정 모두 `[?] LLM 추정`으로 처리 (Software Mansion·코딩애플·LogRocket Expo 빈도 등)

### 시스템 양식 변경 없음
본 세션은 양식·규칙 변경 없이 양식을 적용한 신규 산출물 생성만 포함. 시스템 변경은 세션 1·2 참조.

---

## 2026-05-23 (세션 2) — 평가 반영 후속 보강

### 배경

세션 1 이후 사용자(로그)가 4개 점검 항목 제기:
1. 변경 로그 누락
2. RN/Expo 플랜 본체에 평가 보고서 우선순위 A 3건 미반영
3. 평가 보고서 파일 위치 (`blog/`) 의문 → `research/Plan/evaluations/` 채택
4. `[?] <사유>` 5종 카테고리 정식 등재 누락

### 변경 내역

#### A. 평가 보고서 이동 및 명명 규칙 확립
- `~/Library/Mobile Documents/com~apple~CloudDocs/blog/plan-evaluation-rn-expo.md`
  → `research/Plan/evaluations/[2026-05-23][Mobile] React Native와 Expo 입문 학습 정리_평가.md`
- 이동 사유: 평가는 본체와 생성·소비 주체가 다른 메타 자산. 누적 위치 필요.
- 명명 규칙 신설: `[YYYY-MM-DD][도메인] 주제_평가.md` (본체 명명과 1:1 대응)
- 원본은 `/mnt/user-data/outputs/`에서 Claude(chat)가 만든 것을 사용자가 다운로드해 `blog/`에 임시 보관한 것. Claude Code 이번 작업과 무관.

#### B. 5종 사유 카테고리 정식 등재
- `guides/authoring_guide.md` 제1원칙 섹션에 표로 등재
- 5종: `[?]` (사유 생략) / `[?] LLM 추정` / `[?] 30초 룰 위반` / `[?] 검증 안 함: 일반적 인상` / `[?] 분류 체계 전제 미확인`
- 카테고리 사용 규칙 4개 명시 (1개만 부착, 우선순위, 인간/LLM 차이, 자유 서술 금지)
- 메모리(`feedback_plan_no_guessing.md`) 동기화
- 9-5 골격에 사유 코드별 분포 집계 항목 추가 (본체·템플릿)
- 기존 retrospective 마커 문구(`[?] 평가 당시 직접 확인 안 함: 일반적 인상`) → 5종 표준(`[?] 검증 안 함: 일반적 인상`)으로 통일

#### C. 본체 RN/Expo 플랜 패치 (우선순위 A 반영)
- **A-1 (메타 라벨링)**: 7-3 예시에서 버전·날짜 사실값 제거. 형식만 노출. 버전 자리에 `[?] LLM 추정` 부착. 평가 보고서가 권고한 구체값(`0.85.1`, `SDK 56`)도 평가자의 LLM 추정이라 본체에 박지 않음.
- **A-2 (핵심 질문 4번)**: "Expo Go / Development Build / Bare workflow" 단정 분류 → "현 시점 Expo 공식 docs 표준 분류 체계 확인 후 그 분류에 따라 비교"하는 메타 질문으로 재구성. 분류명에 `[?] 분류 체계 전제 미확인` 부착. 섹션 2-2·7-4의 같은 표현도 동일 처리.
- **A-3 (자료원 교체)**: 5-2 표에서 `InfoQ Mobile`·`Smashing Magazine Mobile`·`토스 tech blog` 제거. 대체 후보 `Software Mansion Blog`·`Wix Mobile Engineering`·`코딩애플 YouTube` 추가하되 모두 `[?] LLM 추정` 부착. URL 미확정도 동일 마커. 변경 이력은 5-2/5-3 표 위에 인라인.
- 5-1/5-2/5-3 모든 표에 `API 필요 여부` 컬럼 채움 (세션 1에서 양식만 변경, 본체 데이터 미반영분 보강)
- 9-5 골격 추가
- 8번 체크리스트 카운트 갱신 (T3 5→6) 및 API 컬럼 체크 추가

#### D. 변경 로그 신설
- 이 파일(`guides/changelog.md`) 자체

---

## 2026-05-23 (세션 1) — 평가 1차 반영: 마커 1종 + 30초 룰 + LLM 특례 + Gap 9-5 + API 컬럼

### 배경

`evaluations/[2026-05-23][Mobile] React Native와 Expo 입문 학습 정리_평가.md`의 [개선] 섹션 A~E 5건 + 사용자 추가 1건(API 사전 명기) = 6개 항목 반영.

### 변경 내역

#### 1. 마커 1종 압축 (`[?]`)
- 기존 `[모름·NotebookLM 검증 필요]` + `[?]` 병기 → `[?]` 단일 표준
- 영향 파일: `guides/authoring_guide.md` 제1원칙 섹션 신설, `guides/quality_checklist.md` A 섹션 신설, 메모리 `feedback_plan_no_guessing.md`

#### 2. 30초 룰 명문화
- "1차 출처로 30초 안 확인 가능한가?" 기준
- 가능 → 확인 후 마커 없이 / 불가능 → `[?]`
- Plan 작성 30분 목표 보호 장치
- 영향: `guides/authoring_guide.md` 제1원칙 섹션

#### 3. LLM 작성자 특례
- LLM training data 회상은 "직접 확인" 아님
- 마커 없이 적으려면 WebSearch/WebFetch/Context7로 그 자리에서 호출 + 출처 URL 인라인
- 평가 단계에도 동일 적용
- 영향: `guides/authoring_guide.md`, 메모리

#### 4. Gap Report 9-5 신설
- `templates/search_plan_template.md`에 9-5 골격 추가
- `guides/authoring_guide.md`에 9-5 작성 가이드 추가
- 항목: 검증 통과 / 불일치 / `[?]` 마킹 / 다음 Plan 참고 패턴

#### 5. 평가 보고서 retrospective 마킹
- `evaluations/[2026-05-23][Mobile] ..._평가.md` [약점] 3번 자료원 표 4행에 `[?]` 부착
- 평가자(Claude)의 1차 확인 없는 단정에 사후 마커

#### 6. API 사전 명기
- `templates/search_plan_template.md` 5-1/5-2/5-3 표에 `API 필요 여부` 컬럼 신설
- `guides/authoring_guide.md` 섹션 5에 기록 규칙 4종 표 (`불필요` / `[API 필요: 도구·키]` / `[? Source 팀 결정]`)
- 9-2(사후 보고)를 사전 명시로 전환
- `guides/quality_checklist.md`에 API 컬럼 체크 추가

### 영향 파일 (세션 1)
- `templates/search_plan_template.md`
- `guides/authoring_guide.md`
- `guides/quality_checklist.md`
- 메모리: `feedback_plan_no_guessing.md`
- 평가 보고서 (당시 `blog/`에 위치, 세션 2에서 이동)
