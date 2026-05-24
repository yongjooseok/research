# 검색 플랜: React Native와 Expo 입문 학습 정리 (2026년 5월 기준, 글로벌)

> Source 팀이 NotebookLM에서 그대로 실행해 자료를 확보하기 위한 지시서.

---

## 1. 메타

| 항목 | 내용 |
|---|---|
| 주제 | React Native와 Expo 입문 학습 정리 (2026년 5월 기준, 글로벌 생태계) |
| 목적 | 입문자가 RN과 Expo의 관계·역할·기본 워크플로우를 정리해, 다음에 깊이 팔 토픽을 결정 |
| 작성자 | 로그 (Plan 보조: Claude) |
| 작성일 | 2026-05-23 |
| 산출물 활용처 | 내부 지식 베이스 (학습 정리 노트) |
| 마감 (선택) | — |
| 긴급도 (선택) | 하 |

---

## 2. 목적 분해

### 2-1. 핵심 결정/판단
- 입문 단계에서 선택할 워크플로우 결정 (Expo 권장 / Bare RN)
- 학습 로드맵의 다음 토픽 결정 (예: Expo Router 심화 vs New Architecture 이해 vs EAS Build)

### 2-2. 알아야 할 사실
- React Native와 Expo의 정의·역사·관계
- 2026년 5월 시점 최신 안정 버전 (RN, Expo SDK) 및 권장 Node·Xcode·JDK
- New Architecture (Fabric / TurboModules / JSI / Hermes) 기본 활성화 여부
- Expo Router의 위상 (파일 기반 라우팅 채택 정도)
- EAS (Build·Submit·Update) 역할과 무료/유료 구간
- 현 시점 Expo 공식 docs의 표준 워크플로우 분류 체계 [?] 분류 체계 전제 미확인 (Expo Go / Development Build / Bare workflow / CNG 등 용어가 현행 분류 어디에 매핑되는지 포함)
- 각 워크플로우의 권장 시나리오와 입문자 선택 기준
- 입문자가 자주 막히는 지점 (설정·디버깅·네이티브 모듈)
- 공식 권장 입문 경로 (RN docs vs Expo docs의 통합 상태)

### 2-3. 알 필요 없는 것 (의도적 제외)
- 5년 이상 된 historical 변화 (Expo SDK 30대 이하)
- 네이티브 iOS / Android 단독 개발
- Flutter / Ionic / Cordova 등 경쟁 프레임워크 상세 비교
- 엔터프라이즈급 CI/CD 파이프라인 심화
- 한국 시장 특수성 (글로벌 기준 학습이 목적)

---

## 3. 핵심 질문 (Analysis Questions)

1. 2026년 5월 현재, React Native와 Expo의 관계는 무엇이며 입문자에게 공식적으로 권장되는 시작 경로는?
2. New Architecture (Fabric / TurboModules / JSI)는 안정화되어 기본값으로 활성화되어 있는가?
3. Expo Router는 입문 단계에서 React Navigation 대비 얼마나 보편적으로 채택되었는가?
4. 2026년 5월 현 시점 Expo 공식 docs가 입문자에게 제시하는 **표준 워크플로우 분류 체계**는 무엇이며 [?] 분류 체계 전제 미확인, 각 분류 간 차이와 입문자 선택 가이드는?
   (※ "Expo Go", "Development Build", "Bare workflow", "CNG(Continuous Native Generation)" 등 자주 언급되는 용어가 현 시점 공식 분류와 어떻게 대응되는지 포함해서 정리)
5. EAS Build / Submit / Update의 무료 구간으로 입문자가 어디까지 할 수 있는가?
6. 입문자가 자주 겪는 막힘 5가지 (환경 설정 · 의존성 · 네이티브 모듈 · 디버깅 · 배포)와 통상 해결책은?
7. 2026년 5월 기준 안정 버전 (RN · Expo SDK)과 권장 Node · Xcode · JDK 환경은?
8. 한국어 자료 중 입문자가 신뢰하고 따라갈 만한 가이드는 어떤 출처에 있는가?

---

## 4. 키워드 체계

### 4-1. 한국어 (KO) — 필수

| 구분 | 키워드 |
|---|---|
| Primary | `React Native 입문`, `Expo 입문`, `React Native와 Expo 차이` |
| Secondary | `리액트 네이티브 시작하기`, `엑스포 SDK`, `Expo Go`, `Expo Router`, `EAS 빌드`, `리액트 네이티브 새 아키텍처`, `Development Build` |
| Long-tail | `2026 리액트 네이티브 시작 가이드`, `Expo로 앱 개발 처음`, `리액트 네이티브 vs Expo 어떤 걸 써야`, `엑스포 로컬 빌드 방법`, `리액트 네이티브 New Architecture 활성화` |
| 제외 | `React (웹)`, `리액트 라우터`, `Next.js`, `채용`, `구인` |

### 4-2. 영어 (EN) — 필수

| 구분 | 키워드 |
|---|---|
| Primary | `React Native getting started`, `Expo getting started`, `React Native vs Expo 2026` |
| Secondary | `Expo SDK`, `Expo Router`, `EAS Build`, `Development Build`, `New Architecture`, `Fabric TurboModules`, `Hermes`, `Metro bundler`, `bare workflow` |
| Long-tail | `should I use Expo or bare React Native 2026`, `migrating from React Navigation to Expo Router`, `React Native New Architecture default enabled`, `EAS Build free tier limits`, `Expo Go vs Development Build for beginners` |
| 제외 | `React.js` (웹), `Next.js`, `Ionic`, `Flutter`, `Cordova`, `hiring`, `jobs` |

### 4-3. 추가 언어 (해당 시)
해당 없음 (영어 생태계 중심 주제)

---

## 5. 소스 매트릭스

### 5-1. Tier 1: 1차 자료 (공식·원전)

| 자료원명 | URL / 검색식 | 검색 방식 | 인증 | 파일 형식 | 목표 건수 | 언어 | API 필요 여부 |
|---|---|---|---|---|---|---|---|
| React Native 공식 docs | https://reactnative.dev/docs/getting-started | 웹 UI | 없음 | HTML | 핵심 5~7 페이지 `[?] 30초 룰 위반` (구체 페이지 미확정) | EN | 불필요 |
| Expo 공식 docs | https://docs.expo.dev | 웹 UI | 없음 | HTML | 핵심 7~10 페이지 `[?] 30초 룰 위반` (구체 페이지 미확정) | EN | 불필요 |
| React Native Releases | https://github.com/facebook/react-native/releases | 웹 UI / RSS | 없음 | HTML | 최근 6개월 | EN | [API 필요: GitHub Releases API/RSS — 토큰 미사용 가능하나 rate limit 시 토큰 권장] |
| Expo SDK Changelogs | https://expo.dev/changelog | 웹 UI | 없음 | HTML | 최근 6개월 | EN | 불필요 |
| React Native Blog | https://reactnative.dev/blog | 웹 UI / RSS | 없음 | HTML | 최근 1년 | EN | 불필요 |
| Expo Blog | https://expo.dev/blog | 웹 UI / RSS | 없음 | HTML | 최근 1년 | EN | 불필요 |

### 5-2. Tier 2: 2차 자료 (분석·종합)

> 변경 이력 (2026-05-23): 평가 보고서 권고에 따라 `InfoQ Mobile`·`Smashing Magazine Mobile`·`토스(toss.tech)` 후보를 표에서 제거. 평가자 단정("RN 글 거의 없음" 등)이 1차 확인 없는 LLM 추정이므로 본체에는 박지 않고, 권고된 대체 자료원도 동일 이유로 `[?] LLM 추정`으로 표시. Source 단계에서 실제 RN/Expo 글 빈도 확인 후 채택·기각.

| 자료원명 | URL / 검색식 | 검색 방식 | 인증 | 파일 형식 | 목표 건수 | 언어 | API 필요 여부 |
|---|---|---|---|---|---|---|---|
| LogRocket Blog (react-native 태그) | https://blog.logrocket.com/tag/react-native/ | 웹 UI | 없음 | HTML | 5 | EN | 불필요 |
| Callstack Blog | https://www.callstack.com/blog | 웹 UI | 없음 | HTML | 3 | EN | 불필요 |
| Software Mansion Blog `[?] LLM 추정` | URL Source 팀 확인 필요 `[?] LLM 추정` | 웹 UI | 없음 | HTML | 3 | EN | 불필요 |
| Wix Mobile Engineering `[?] LLM 추정` | URL Source 팀 확인 필요 `[?] LLM 추정` | 웹 UI | 없음 | HTML | 2 | EN | 불필요 |
| 한국 테크 블로그 (카카오·우아한형제들) | tech.kakao.com / techblog.woowahan.com (각 사이트 검색 "React Native") | 웹 UI 검색 | 없음 | HTML | 2~3 (있는 경우) | KO | 불필요 |

### 5-3. Tier 3: 3차 자료 (현장·여론)

> 변경 이력 (2026-05-23): 한국어 보완 자료원으로 **코딩애플 YouTube RN 시리즈** 후보가 평가 보고서에서 권고됨 `[?] LLM 추정` (실제 시리즈 존재·품질 1차 확인 안 됨). Source 단계에서 채널 확인 후 채택.

| 자료원명 | URL / 검색식 | 검색 방식 | 인증 | 파일 형식 | 목표 건수 | 언어 | API 필요 여부 |
|---|---|---|---|---|---|---|---|
| Reddit r/reactnative | https://www.reddit.com/r/reactnative/top/?t=year | 웹 UI / API | 없음 | HTML 캡처 (댓글 트리 포함 안정성 낮음 → 핵심 텍스트만 .md 변환 권장) | 상위 5 스레드 `[?] 30초 룰 위반` (상위 정의 기준 미명시) | EN | 불필요 (Reddit API는 인증 필요해 웹 UI 권장) |
| Stack Overflow (react-native 태그) | https://stackoverflow.com/questions/tagged/react-native?tab=Frequent | 웹 UI | 없음 | HTML (Q&A 텍스트 추출 후 .md 권장) | 입문 빈도 Q 3 | EN | 불필요 |
| YouTube (RN/Expo 컨퍼런스) | youtube.com 검색: `App.js Conf`, `React Native EU` (연도 Source 팀 확인) `[?] LLM 추정` | 웹 UI / 자막 다운로드 | 없음 | 자막 텍스트 | 3~5 토크 | EN | [API 필요: youtube-transcript-api / yt-dlp 중 택일] |
| Dev.to (reactnative 태그) | https://dev.to/t/reactnative/top/year | 웹 UI | 없음 | HTML | 3 | EN | 불필요 |
| 한국 YouTube (코딩애플 RN 시리즈) `[?] LLM 추정` | youtube.com 검색: `코딩애플 React Native` | 웹 UI / 자막 다운로드 | 없음 | 자막 텍스트 | 1~2 영상 | KO | [API 필요: youtube-transcript-api / yt-dlp] |
| 한국 개인 블로그 (Velog·Tistory) | Google 검색: `site:velog.io "React Native" 입문` / `site:tistory.com Expo 시작하기` | 웹 UI 검색 | 없음 | HTML | 2~3 | KO | 불필요 |

---

## 6. 검색 파라미터

| 파라미터 | 값 | 근거 |
|---|---|---|
| 언어 가중치 | EN 70% / KO 30% | 공식 docs · 컨퍼런스 모두 영어. 한국어는 보조 |
| 자료 최신성 | 1년 이내 (2025-05 이후) | RN · Expo 모두 반기 단위로 큰 변경 (New Architecture · Expo Router · EAS 변화 빠름) |
| 파일 타입 우선순위 | HTML > 영상 자막 > PDF | 공식 docs는 HTML 중심, PDF 거의 없음 |
| 자료 다양성 Tier 비율 | T1 ≥ 40% / T2 ≈ 30% / T3 ≤ 30% | 입문 학습이라 공식 자료 비중 상향 |
| 지역 필터 | 글로벌 (영어 생태계 중심) | 한국 시장 특수성 제외 |

---

## 7. NotebookLM 실행 지시

### 7-1. Notebook 생성
- Notebook 이름: `[2026-05-23][Mobile] React Native와 Expo 입문 학습 정리`

### 7-2. 소스 추가 순서
1. **T1**: RN docs 핵심 페이지 → Expo docs 핵심 페이지 → RN/Expo 릴리스·changelog → 공식 블로그
2. **T2**: LogRocket · Callstack · InfoQ → 한국 테크 블로그
3. **T3**: Reddit 상위 토론 → Stack Overflow 빈도 Q → YouTube 컨퍼런스 자막 → Dev.to → 한국 개인 블로그

### 7-3. 소스 메타 라벨링
형식: `[Tier|Lang|YYYY-MM-DD] 자료 제목`

예시 (형식만 표시 — 버전·날짜 사실값은 Source 단계에서 NotebookLM 적재 시 실측치로 채움):
```
[T1|EN|YYYY-MM-DD] React Native [버전 [?] LLM 추정] Releases — New Architecture 관련 노트
[T1|EN|YYYY-MM-DD] Expo SDK [버전 [?] LLM 추정] changelog
[T2|EN|YYYY-MM-DD] LogRocket "React Native vs Expo" 분석 글
[T3|EN|YYYY-MM-DD] App.js Conf 키노트 자막 [?] 검증 안 함: 일반적 인상 (해당 컨퍼런스 명·연도 미확정)
[T3|KO|YYYY-MM-DD] Velog "엑스포로 첫 앱 만들기" 류 입문 글
```

> 양식 변경 사유: Plan 작성자(Claude)가 RN/Expo stable 버전 사실값을 1차 출처에서 직접 확인하지 못함. 평가 보고서가 권고한 값(예: `RN 0.85.1`, `SDK 56`)도 평가자의 LLM 추정으로 동일 위험. 따라서 예시에서 사실값을 제거하고 형식만 노출. Source 팀이 NotebookLM 적재 시 실제 릴리스 페이지에서 본 값으로 라벨링.

### 7-4. NotebookLM 분석 질의문
1. 2026년 5월 기준 React Native와 Expo의 공식 권장 입문 경로를 단계별로 정리해줘. 공식 docs 우선 인용.
2. New Architecture (Fabric · TurboModules · JSI)가 기본값으로 활성화되어 있는지, 입문자에게 의미하는 바를 정리해줘.
3. 현 시점 Expo 공식 docs의 표준 워크플로우 분류 체계 [?] 분류 체계 전제 미확인를 확인한 뒤, 그 분류에 맞춰 각 워크플로우(Expo Go / Development Build / Bare workflow / CNG 등 용어가 매핑되는 항목 포함)를 비교 표로 만들고 입문자 선택 가이드를 제시해줘. (공식 분류와 다른 용어가 자주 쓰이면 그 차이도 표기)
4. Expo Router의 현재 위상과 React Navigation 대비 학습 우선순위는?
5. EAS Build · Submit · Update의 무료 구간 한계와 입문자가 사용할 시나리오는?
6. 입문자가 자주 겪는 막힘 5가지 (환경 설정 · 의존성 · 네이티브 모듈 · 디버깅 · 배포)와 통상 해결책을 자료 근거로 정리해줘.
7. 한국어 자료 중 신뢰할 만한 입문 가이드가 있다면 출처와 함께 제시해줘.
8. 2026년 5월 기준 안정 버전 (RN · Expo SDK)과 권장 Node · Xcode · JDK 환경을 표로 정리해줘.

### 7-5. 추출 후 산출물 위치
- NotebookLM Notes 내 정리 → 최종 통합본은 로컬:
  `output/[2026-05-23][Mobile] React Native와 Expo 입문 학습 정리_결과.md`

---

## 8. 품질 검증 체크리스트 (실행 전)

- [x] 키워드가 번역체가 아닌 **원어 그대로** (`bare workflow`, `엑스포 SDK` 등)
- [x] T1(1차) 자료원 6개가 **서로 보완적** (docs · 릴리스 · 블로그로 분산)
- [x] 모든 Tier가 채워져 있고 한쪽 Tier 쏠림 없음 (T1 6 / T2 5 / T3 6 — 2026-05-23 평가 반영으로 T2 일부 교체·T3 1개 추가)
- [x] `API 필요 여부` 컬럼이 모든 자료원 행에 기록됨
- [x] 자료원이 모두 구체적 (`Google` 같은 추상 자료원 없음. `site:` 검색식만 한국 블로그에 사용)
- [x] 최신성 1년이 RN·Expo 변화 속도(반기 단위)에 부합
- [x] 핵심 질문 모두 자료로 검증 가능 (미래 예측 X)
- [x] 제외 키워드가 노이즈 차단 (React 웹 / 경쟁 프레임워크 / 채용)
- [x] NotebookLM 실행 지시가 추가 질문 없이 따라할 수 있음 (Notebook 이름·소스 순서·질의문 명시)
- [x] "알 필요 없는 것" 5개 명시

---

## 9. Gap Report (실행 후 — Source 팀 작성)

### 9-1. 부족했던 자료 영역
- 

### 9-2. 추가로 발급/연동했어야 할 API
- (예: GitHub Releases RSS, YouTube transcript API)

### 9-3. 다음 유사 주제에서 추가할 자료원
- 

### 9-4. 도메인 프로파일 승격 후보
> "모바일 프레임워크 입문" 도메인 프로파일로 묶을 자료원 후보:
- (초안) RN docs · Expo docs · App.js Conf · React Native EU · Reddit r/reactnative · Stack Overflow react-native 태그

### 9-5. Plan 사실관계 검증 결과
> Plan 본문에 박힌 작성자 단정 vs NotebookLM 적재 자료의 일치 여부 사후 점검.

- 검증 통과 (작성자 단정 ↔ NotebookLM 자료 일치): [n건]
- 검증 실패 (작성자 단정 ↔ NotebookLM 자료 불일치, 어디?): [n건]
- 마커 `[?]`로 표시되어 Source가 확인한 항목: [n건]
  - 사유 코드별 분포 (LLM 추정 / 30초 룰 위반 / 검증 안 함: 일반적 인상 / 분류 체계 전제 미확인 / 사유 생략): [집계]
- 다음 Plan 작성 시 참고할 패턴: 
