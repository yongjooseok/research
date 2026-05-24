# 검색 요청서 평가: React Native와 Expo 입문 학습 정리

> 평가 대상: `[2026-05-23][Mobile] React Native와 Expo 입문 학습 정리.md`
> 평가자: 클로드 (로그 위임)
> 평가일: 2026-05-23
> 워크플로우: Plan → Source → Extract (NEXUS와 별개)

---

## 종합 결론

**구조와 사고 체계는 매우 우수**하지만, **2026년 5월 시점의 사실관계가 일부 outdated**되어 있고 **NotebookLM이라는 도구의 특성과 어긋나는 부분**이 있다. 우선순위 A 항목 3가지를 수정한 뒤 Source 팀에 넘기는 것을 권장한다.

---

## [정확성] 사실관계 검증

문서가 가정한 버전·분류 정보가 1년 가까이 outdated.

| 항목 | 문서 가정 | 2026-05-23 실제 |
|---|---|---|
| React Native stable | 0.77 (예시) | **0.85.1** (2026-04-13 릴리스) |
| Expo SDK stable | SDK 53 (예시) | **SDK 56.0.3** (5월 20일 stable), 일반 권장은 SDK 55 |
| React 버전 | 미명시 | React 19.2.3 |
| New Architecture | "활성화 여부 확인 대상" | 0.76+ 기본 활성화, **0.82+ 의무화** |
| Workflow 분류 | Expo Go / Dev Build / **Bare workflow** | **CNG가 기본**, Bare는 legacy 표현으로 후퇴 |
| RN vs Expo 위상 | "공식 권장 시작 경로 확인 필요" | "Expo가 이겼다" — 공식 RN docs도 Expo 권장, `npx create-expo-app`이 표준 |

**영향**:
- 메타 라벨링 예시가 outdated → Source 팀이 예시 기준으로 자료를 모으면 1년 전 자료가 섞일 위험
- 핵심 질문 4번의 분류(Bare workflow)는 2026년 현 시점 Expo 공식 문서 분류와 불일치 → 검색해도 깔끔한 답을 못 얻을 가능성 높음

---

## [강점]

### 1. 구조의 완성도
- Plan → Source → Extract 역할 분리 명확
- Tier 분류 체계적 (1차 공식 / 2차 분석 / 3차 현장)
- 메타 라벨링 형식 명시 (`[Tier|Lang|Date]`)
- 품질 검증 체크리스트 + Gap Report → PDCA 사이클 내장

### 2. 키워드 체계
- 한/영 분리, Primary / Secondary / Long-tail 3단계
- 제외 키워드로 노이즈 차단 (React 웹, Flutter, 채용 등)
- 원어 그대로 유지 (`bare workflow`, `엑스포 SDK`)

### 3. 자료 다양성
- T1 6 / T2 5 / T3 5 균형
- 영어 70% / 한국어 30% 가중치 (이 주제에 적절)
- 최신성 1년 (RN/Expo 반기 단위 변화 반영)

### 4. 실행 가능성
- NotebookLM 분석 질의문 8개가 핵심 질문 8개와 1:1 매칭
- Notebook 이름·소스 순서까지 명시되어 Source 팀이 추가 질문 없이 따라할 수 있음

---

## [약점]

### 1. 버전·분류 정보 outdated
위 [정확성] 섹션 참조. 가장 시급한 수정 대상.

### 2. NotebookLM의 도구 특성과 일부 어긋남
NotebookLM은 **자료 분석** 도구이지 **자료 발견·검색** 도구가 아니다. URL을 직접 add할 수는 있지만 "어떤 URL을 가져올지"는 사람이 정해야 한다.

- "RN docs 핵심 5-7 페이지" → 어떤 페이지가 핵심인지 기준 부재
- "최근 6개월 릴리스" → 몇 개의 릴리스를 받을지 미명시
- "Reddit 상위 5 스레드" → 어떤 키워드로 어떻게 상위를 정의할지 모호

### 3. 일부 자료원의 적합성 의문

> **Retrospective `[?]` 마킹 (2026-05-23 추가)**: 아래 표의 "문제" 컬럼 단정 중 평가자(Claude)가 1차 출처를 직접 확인하지 않은 항목에 `[?]` 부착. 제1원칙(`guides/authoring_guide.md`)은 평가 단계에도 동일 적용 — LLM 평가자도 training data 회상으로 자료원 성격을 단정할 자격 없음. Source 단계에서 NotebookLM 적재 후 실제 확인 필요.

| 자료원 | 문제 | 권장 |
|---|---|---|
| Smashing Magazine Mobile | RN/Expo 글 거의 없음, 일반 모바일 디자인 위주 `[?] 검증 안 함: 일반적 인상` | 제외 또는 교체 |
| InfoQ Mobile | RN 전문 아님, 기업 IT 관점 위주 `[?] 검증 안 함: 일반적 인상` | 우선순위 하향 |
| 토스(toss.tech) | 자체 네이티브/KMM 중심, RN 글 매우 적음 `[?] 검증 안 함: 일반적 인상` | 제외 |
| 카카오·우아한형제들 | RN 글 있긴 하지만 1년 이내 신규는 드묾 `[?] 검증 안 함: 일반적 인상` | "있는 경우만"으로 retreat한 것은 OK |

### 4. 자료 수집 후 변환 단계 부재
NotebookLM은 URL 직접 추가가 가능하지만, 일부 형식은 별도 변환이 필요하다.

- HTML 페이지 → URL 직접 add OK
- YouTube → URL 직접 add OK (자막 자동 처리)
- **Reddit 스레드** → URL add 가능하나 댓글 트리 포함 안정성 낮음 → 핵심 텍스트만 추출 후 .md로 변환 권장
- **Stack Overflow Q&A** → 마찬가지로 텍스트 추출 권장
- 변환 기준이 문서에 명시 안 됨

### 5. 핵심 질문 4번의 분류 오류
"Bare workflow"는 2026년 시점에서 legacy 표현. 현재 Expo의 표준 분류는:
- **Expo Go** (학습용 빠른 프로토타입)
- **Development Build + CNG** (실제 앱 개발 표준)
- **Existing native projects with Expo modules** (기존 RN 프로젝트에 Expo 점진 도입)

이 3분류로 질문을 재구성해야 검색 결과가 깔끔하게 나옴.

---

## [누락]

### 1. NotebookLM 한계 인지
- 소스 수 제한 (Free 50, Plus는 더 많음 — 현 시점 정책 재확인 필요)
- 한국어 답변 품질 영어 대비 떨어질 수 있음
- 인용 출처 표기는 자동이지만, 어떤 소스가 답변의 어느 부분을 뒷받침했는지 추적이 항상 정확하진 않음

### 2. 답변 신뢰성 검증 단계
- NotebookLM 답변 자체의 환각 검증 절차 없음
- 자료원 간 충돌이 있을 경우 처리 방법 없음 (예: 공식 docs vs 블로그 의견)

### 3. Plan → Source → Extract 폴더 간 인터페이스
- Source가 Extract로 넘기는 산출물 형식 명시 없음
- 7-5에 "최종 통합본 `output/...md`" 라고만 함 → 그 .md의 구조(목차·인용 형식·다음 단계)는 미정의

### 4. 시간 추정
- Source 팀이 자료 수집 + 업로드 + 8개 질의응답까지 걸리는 예상 시간 없음
- 향후 유사 작업 견적에 활용할 데이터 부재

### 5. 한국어 자료 보완 출처
- 카카오/우아한/토스에서 자료가 부족할 경우 대안 명시 없음
- 권장 보완: 인프런·패스트캠퍼스 강의 시놉시스, 한국어 YouTube (코딩애플·노마드코더), Velog/Tistory site 검색은 이미 포함되어 있음

---

## [개선] 우선순위별 보완 항목

### 우선순위 A — 지금 수정 후 Source 팀에 전달

**A-1. 버전 정보 업데이트**
- 7-3 메타 라벨링 예시:
  - `React Native 0.77` → `React Native 0.85`
  - `Expo SDK 53 changelog` → `Expo SDK 55 / 56 changelog`
- 핵심 질문 7번: "RN 0.85+ / Expo SDK 55-56 / React 19.2 / Node 20.19.4+" 명시
- 키워드에 추가: `Continuous Native Generation`, `CNG`, `expo prebuild`, `Expo Skills`

**A-2. 핵심 질문 4번 재설계**
- 현재: "Expo Go / Development Build / Bare workflow 차이"
- 변경: "Expo Go / Development Build + CNG / 기존 네이티브 프로젝트에 Expo 점진 도입의 세 가지 경로 차이와 입문자 선택 가이드"

**A-3. 자료원 교체·보완**

| 제거 후보 | 대체 후보 |
|---|---|
| Smashing Magazine Mobile | Software Mansion blog, Wix Mobile Engineering |
| InfoQ Mobile (우선순위 하향만) | Gitnation (App.js Conf 공식 토크 페이지) |
| 토스 tech blog | 한국어 YouTube (코딩애플 RN 시리즈) |

### 우선순위 B — 다음 사이클에 반영

**B-1. NotebookLM 자료 변환 기준 추가** (5번 섹션 끝에)
```
자료 형식별 NotebookLM import 방식
- HTML 페이지: URL 직접 추가
- YouTube 영상: URL 직접 추가
- Reddit/Stack Overflow: 핵심 텍스트 추출 후 .md 업로드
- PDF: 그대로 업로드
- 컨퍼런스 슬라이드: PDF로 변환 후 업로드
```

**B-2. 답변 검증 단계 추가** (8번 체크리스트 다음)
```
## 9. 답변 신뢰성 검증
- T1 자료 인용 비율 ≥ 50% (공식 docs 우선)
- 자료원 간 충돌 시 T1 우선, 차이는 별도 메모
- 버전·날짜 명시 답변만 신뢰 (모호한 "최근에는…" 답변은 추가 검증)
```

**B-3. Plan → Source → Extract 인터페이스 표준화** (7-5 확장)
```
산출물 .md 표준 구조:
1. 메타 (질의 일자, 자료원 수, 자료 신뢰도 분포)
2. 핵심 질문별 답변 (T1 인용 우선)
3. 자료 간 충돌·미해결 영역
4. Extract 팀 인계 메모 (어떤 부분을 정리·요약할지)
```

**B-4. 시간 추정 추가**
```
Source 팀 작업 시간 (1차 추정):
- 자료 수집·정리: 2-3시간
- NotebookLM 업로드: 30분
- 질의응답 + 답변 정리: 1-2시간
- 합계: 4-6시간
```

---

## 즉시 적용 가능한 패치 (복붙용)

### 패치 1: 7-3 메타 라벨링 예시 교체
```
[T1|EN|2026-04-13] React Native 0.85.1 Releases — Stable
[T1|EN|2026-05-20] Expo SDK 56 changelog — Hermes V1 default
[T1|EN|2026-02-25] Expo SDK 55 changelog — RN 0.83 기반
[T2|EN|2026-03-17] Medium "React Native in 2026: What Changed"
[T3|EN|2026-01-12] App.js Conf 2025 keynote 자막
[T3|KO|2025-11-05] Velog "엑스포로 첫 앱 만들기"
```

### 패치 2: 핵심 질문 4번
```
4. Expo Go / Development Build + CNG / 기존 네이티브 프로젝트에 Expo 모듈
   점진 도입 — 세 경로의 차이는 무엇이며, 입문자는 언제 무엇을 선택?
   (참고: 2026년 시점 "bare workflow"는 legacy 표현으로 후퇴, CNG가 표준)
```

### 패치 3: 키워드 추가 (4-2 영어 Secondary)
```
기존: Expo SDK, Expo Router, EAS Build, Development Build, New Architecture, ...
추가: Continuous Native Generation, CNG, expo prebuild, Expo Skills, Hermes V1
```

---

## 평가의 불확실한 부분 (명시)

- NotebookLM의 정확한 소스 수 제한, 한국어 처리 품질은 1년 가까이 변화가 있을 수 있어 현 시점 최신 정책 직접 확인 권장
- Expo SDK 56이 5월 20일 stable이라 입문자에게 SDK 55를 권할지 56을 권할지는 5월 23일 시점에서 미묘함 (보수적으로는 SDK 55)
- "Bare workflow" 용어가 완전 deprecated되진 않았으나, 공식 docs 분류상 비중이 크게 줄었다는 의미. 검색 시 여전히 다수 결과가 나오긴 함

---

## 결론 한 줄

**구조는 그대로 두고, 우선순위 A 3건만 패치한 뒤 Source 팀에 넘기면 작업 가능**. B 항목은 첫 번째 사이클 끝난 뒤 Gap Report 반영해서 정리하면 충분하다.
