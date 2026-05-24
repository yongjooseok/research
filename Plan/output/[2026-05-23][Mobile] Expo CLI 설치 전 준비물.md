# 검색 플랜: Expo CLI 설치 전 반드시 확인해야 할 준비물 (2026년 5월 기준, 글로벌)

> Source 팀이 NotebookLM에서 이 문서를 그대로 실행해 자료를 확보하기 위한 지시서.
> 본 Plan은 `guides/authoring_guide.md` 제1원칙(사실관계 추정 금지·단일 마커 `[?]`·5종 사유 카테고리)을 따른다. 작성자(Claude)가 training data 회상으로 단정한 사실값은 모두 `[?] LLM 추정` 또는 해당 사유 코드 부착.

---

## 1. 메타

| 항목 | 내용 |
|---|---|
| 주제 | Expo CLI 설치 전 반드시 확인해야 할 준비물 (2026년 5월 기준, 글로벌, 입문자 개인 환경 한정) |
| 목적 | 입문자가 Expo CLI를 처음 설치하기 전 자기 환경(OS·Node·시뮬레이터·필수 도구)을 점검·준비하는 체크리스트 결정 |
| 작성자 | 로그 (Plan 보조: Claude) |
| 작성일 | 2026-05-23 |
| 산출물 활용처 | 내부 지식 베이스 (학습 정리 노트) → 후속 입문 가이드 글의 사전 준비 섹션 근거 |
| 마감 (선택) | — |
| 긴급도 (선택) | 하 |

---

## 2. 목적 분해

### 2-1. 핵심 결정/판단

- 입문자가 Expo CLI 설치 직전 거쳐야 할 **사전 점검 체크리스트**(OS·Node·기타 도구) 항목 결정
- iOS 시뮬레이터/Android 에뮬레이터 중 입문 단계에서 어느 것을 먼저 준비할지(또는 Expo Go만으로 시작 가능한지) 결정 `[?] 분류 체계 전제 미확인` (현 시점 Expo가 권장하는 입문 경로 분류 자체 확인 필요)

### 2-2. 알아야 할 사실

- 2026-05-23 시점 Expo가 권장하는 **CLI 설치 방식** `[?] 분류 체계 전제 미확인` (글로벌 npm 설치 / `npx create-expo-app` / `npx expo` on-demand 호출 중 어느 게 표준인지)
- 요구·권장 Node.js 버전 `[?] LLM 추정` (LTS 정책과 어느 메이저까지 호환되는지)
- 요구·권장 패키지 매니저 `[?] LLM 추정` (npm / yarn / pnpm / bun 지원 여부)
- watchman 필요 여부 및 어느 OS에서 권장되는지 `[?] LLM 추정`
- Git 설치 필요 여부 `[?] LLM 추정`
- iOS 시뮬레이터 사용 시 요구되는 Xcode 버전·CommandLineTools 요구 `[?] LLM 추정`
- Android 에뮬레이터 사용 시 요구되는 JDK 버전·Android Studio·SDK·platform-tools `[?] LLM 추정`
- **Expo Go** 앱(개인 디바이스 시뮬)만으로 입문이 가능한 범위 `[?] 분류 체계 전제 미확인`
- 지원 호스트 OS 분류 `[?] 분류 체계 전제 미확인` (macOS / Windows / WSL / Linux 각각의 제약)
- 설치 전 흔히 누락되는 사전 준비 항목 (네이티브 모듈 빌드용 컴파일러, Rosetta on Apple Silicon, 환경변수 등) `[?] 검증 안 함: 일반적 인상`

### 2-3. 알 필요 없는 것 (의도적 제외)

- Expo CLI 설치 이후의 프로젝트 구조·라우팅·배포 워크플로우 (본 Plan 범위 밖, 별도 주제)
- iOS/Android 네이티브 단독 개발 환경(Swift/Kotlin) 준비물
- Flutter·Ionic·Cordova 등 다른 모바일 프레임워크 준비물
- 엔터프라이즈/CI 환경 (개인 입문자 한정)
- 한국 시장 특수성 (글로벌 docs 기준)
- 과거 deprecated된 `expo-cli` 글로벌 패키지의 이력 (현행 표준만 다룸 — 단, 옛 글로벌 설치를 가진 사용자의 마이그레이션은 "흔한 막힘"의 한 항목으로 포함)

---

## 3. 핵심 질문 (Analysis Questions)

1. 2026년 5월 현재 Expo 공식 docs가 권장하는 **CLI 설치/호출 방식**은 무엇이며 `[?] 분류 체계 전제 미확인`, 글로벌 설치는 권장/비권장 중 어디인가?
2. Expo CLI를 쓰려면 요구·권장되는 **Node.js 버전 범위**는? (LTS 정책 포함)
3. macOS / Windows / WSL / Linux 각각에서 **추가로 필요한 사전 도구**는 무엇인가? `[?] 분류 체계 전제 미확인` (현 시점 공식이 분류로 안내하는 OS 목록 확인 후 그에 맞춰 비교)
4. **Expo Go** 앱만으로 입문자가 어디까지 진행 가능하며, 그 한계는 무엇인가?
5. iOS 시뮬레이터·Android 에뮬레이터를 입문 단계에서 준비하지 않고도 학습이 가능한가? 가능하다면 어떤 단계까지인가?
6. 입문자가 설치 단계에서 자주 막히는 5가지 (Node 버전 불일치·watchman 부재·JDK 미설치·Xcode CommandLineTools 누락·환경변수 등 `[?] 검증 안 함: 일반적 인상`)와 통상 해결책은?
7. 옛 `expo-cli`(글로벌 패키지) 사용자가 현행 방식으로 옮겨갈 때 무엇을 제거·재설치해야 하는가? `[?] LLM 추정` (옛/현 구분 자체 확인 필요)

---

## 4. 키워드 체계

### 4-1. 한국어 (KO) — 필수

| 구분 | 키워드 |
|---|---|
| Primary | `Expo CLI 설치 준비`, `Expo 시작 환경 설정`, `Expo 입문 사전 준비` |
| Secondary | `npx create-expo-app`, `엑스포 노드 버전`, `엑스포 watchman`, `엑스포 윈도우 설치`, `엑스포 맥 설치`, `Expo Go 앱` |
| Long-tail | `Expo CLI 처음 설치하는데 뭐 필요`, `엑스포 시작 전 체크리스트`, `엑스포 윈도우에서 막힘`, `expo-cli deprecated 어떻게 옮겨` |
| 제외 | `Expo SDK 업그레이드`, `EAS Build 설정`, `React Native 단독`, `Flutter`, `채용`, `구인` |

### 4-2. 영어 (EN) — 필수

| 구분 | 키워드 |
|---|---|
| Primary | `Expo CLI prerequisites`, `Expo install requirements`, `Expo system requirements`, `Expo getting started prerequisites` |
| Secondary | `npx create-expo-app`, `Node version Expo`, `watchman macOS Expo`, `Expo Windows setup`, `Expo Go app`, `Expo local development environment` |
| Long-tail | `what do I need before installing Expo CLI`, `Expo CLI minimum Node version 2026`, `migrating from expo-cli global to npx expo`, `Expo Android emulator JDK version` |
| 제외 | `EAS Build`, `Expo Router migration`, `React Native bare`, `Flutter`, `Ionic`, `hiring`, `jobs` |

### 4-3. 추가 언어 (해당 시)

해당 없음 (영어 docs 중심 주제, 한국어는 보조).

---

## 5. 소스 매트릭스

> 변경 이력 (2026-05-23 초안): 자료원 후보는 모두 작성자(Claude) 추정 기반이라 자료원 자체 적합성(특정 블로그에 Expo 입문 글이 충분한지 등)에 `[?]` 부착. Source 단계에서 NotebookLM 적재 전 1차 확인 후 채택·기각.

### 5-1. Tier 1: 1차 자료 (공식·원전)

| 자료원명 | URL / 검색식 | 검색 방식 | 인증 | 파일 형식 | 목표 건수 | 언어 | API 필요 여부 |
|---|---|---|---|---|---|---|---|
| Expo 공식 docs (Get Started) | https://docs.expo.dev — `get-started` 섹션 `[?] LLM 추정` (정확 경로) | 웹 UI | 없음 | HTML | 핵심 4~6 페이지 `[?] 30초 룰 위반` (구체 페이지 미확정) | EN | 불필요 |
| React Native 공식 docs (Environment setup) | https://reactnative.dev/docs/environment-setup `[?] LLM 추정` (경로) | 웹 UI | 없음 | HTML | 1~2 페이지 (Expo 권장 분기 부분) | EN | 불필요 |
| Node.js 공식 (Releases·LTS 정책) | https://nodejs.org/en/about/previous-releases — LTS 정책 페이지 | 웹 UI | 없음 | HTML | 2 페이지 (현행 LTS 라인 + 정책) | EN | 불필요 |
| Expo SDK Changelog (최근) | https://expo.dev/changelog | 웹 UI / RSS | 없음 | HTML | 최근 6개월 중 CLI·요구사항 변경 언급분 | EN | 불필요 |
| Watchman 공식 docs (Facebook) | https://facebook.github.io/watchman/ `[?] LLM 추정` (URL) | 웹 UI | 없음 | HTML | 설치 페이지 1 | EN | 불필요 |
| Android Studio·SDK 공식 (developer.android.com) | https://developer.android.com/studio + `command-line tools` 페이지 | 웹 UI | 없음 | HTML | 1~2 페이지 | EN | 불필요 |

### 5-2. Tier 2: 2차 자료 (분석·종합)

| 자료원명 | URL / 검색식 | 검색 방식 | 인증 | 파일 형식 | 목표 건수 | 언어 | API 필요 여부 |
|---|---|---|---|---|---|---|---|
| LogRocket Blog (Expo 태그·검색) | https://blog.logrocket.com/?s=Expo+install | 웹 UI 검색 | 없음 | HTML | 2~3 `[?] LLM 추정` (해당 블로그 Expo 입문 글 빈도 미확인) | EN | 불필요 |
| Callstack Blog (Expo·setup 키워드) | https://www.callstack.com/blog?search=Expo | 웹 UI 검색 | 없음 | HTML | 1~2 `[?] LLM 추정` | EN | 불필요 |
| Software Mansion Blog | URL Source 팀 확인 필요 `[?] LLM 추정` | 웹 UI | 없음 | HTML | 1~2 `[?] LLM 추정` | EN | 불필요 |
| Dev.to (Expo·setup 태그 교집합) | https://dev.to/search?q=Expo%20install%20prerequisites | 웹 UI | 없음 | HTML | 3 | EN | 불필요 |
| 한국 테크 블로그 (카카오·우아한형제들) | tech.kakao.com / techblog.woowahan.com (각 사이트 검색 "Expo" 또는 "React Native 설치") | 웹 UI 검색 | 없음 | HTML | 1~2 (있는 경우) `[?] LLM 추정` (Expo 입문 글 존재 여부 미확인) | KO | 불필요 |

### 5-3. Tier 3: 3차 자료 (현장·여론)

| 자료원명 | URL / 검색식 | 검색 방식 | 인증 | 파일 형식 | 목표 건수 | 언어 | API 필요 여부 |
|---|---|---|---|---|---|---|---|
| Reddit r/expo | https://www.reddit.com/r/expo/top/?t=year | 웹 UI | 없음 | HTML 캡처 (핵심 텍스트만 .md 변환 권장) | 설치·환경 막힘 상위 5 스레드 `[?] 30초 룰 위반` (상위 정의 기준 미명시) | EN | 불필요 (웹 UI 권장) |
| Reddit r/reactnative (Expo·install 키워드) | r/reactnative 내부 검색: `Expo install` | 웹 UI | 없음 | HTML 캡처 | 3 | EN | 불필요 |
| Stack Overflow (expo·prerequisites·install 태그·키워드) | https://stackoverflow.com/questions/tagged/expo + 검색어 `prerequisites OR install OR setup` | 웹 UI | 없음 | HTML | 입문 빈도 Q 5 | EN | 불필요 |
| YouTube (Expo 입문 설치 영상) | youtube.com 검색: `Expo CLI install 2026`, `Expo setup tutorial` | 웹 UI / 자막 다운로드 | 없음 | 자막 텍스트 | 2~3 영상 (조회수 상위) | EN | [API 필요: youtube-transcript-api / yt-dlp 중 택일] |
| 한국 YouTube (코딩애플·노마드코더 등 입문 시리즈) `[?] LLM 추정` | youtube.com 검색: `코딩애플 Expo`, `노마드코더 React Native 설치` | 웹 UI / 자막 다운로드 | 없음 | 자막 텍스트 | 1~2 영상 | KO | [API 필요: youtube-transcript-api / yt-dlp] |
| 한국 개인 블로그 (Velog·Tistory) | Google 검색: `site:velog.io Expo 설치` / `site:tistory.com Expo 시작하기` | 웹 UI 검색 | 없음 | HTML | 2~3 | KO | 불필요 |

---

## 6. 검색 파라미터

| 파라미터 | 값 | 근거 |
|---|---|---|
| 언어 가중치 | EN 70% / KO 30% | 공식 docs는 영어. 한국어는 보조 자료. |
| 자료 최신성 | 6개월 이내 (2025-11 이후) | CLI 설치 방식·요구 Node 버전 등은 변화 빠름. 1년 잡으면 deprecated된 글로벌 `expo-cli` 시대 자료가 섞일 위험. |
| 파일 타입 우선순위 | HTML > 영상 자막 > PDF | 공식 docs는 HTML, PDF 거의 없음. |
| 자료 다양성 Tier 비율 | T1 ≥ 45% / T2 ≈ 25% / T3 ≤ 30% | 설치 요구사항은 공식 docs의 권위가 결정적이라 T1 가중 상향. |
| 지역 필터 | 글로벌 (영어 생태계 중심) | 한국 시장 특수성 제외. |

---

## 7. NotebookLM 실행 지시 (Source 팀)

### 7-1. Notebook 생성

- Notebook 이름: `[2026-05-23][Mobile] Expo CLI 설치 전 준비물`

### 7-2. 소스 추가 순서

1. **T1**: Expo Get Started → RN Environment setup → Node.js LTS 정책 → Expo Changelog → Watchman 공식 → Android Studio 공식
2. **T2**: LogRocket · Callstack · Software Mansion → Dev.to → 한국 테크 블로그
3. **T3**: Reddit r/expo · r/reactnative → Stack Overflow → YouTube (EN) → 한국 YouTube → Velog·Tistory

### 7-3. 소스 메타 라벨링

형식: `[Tier|Lang|YYYY-MM-DD] 자료 제목`

예시 (형식만 표시 — 실제 버전·날짜 사실값은 Source 단계에서 NotebookLM 적재 시 실측치로 채움):
```
[T1|EN|YYYY-MM-DD] Expo Get Started — Installation 페이지
[T1|EN|YYYY-MM-DD] React Native — Environment setup (Expo 분기)
[T1|EN|YYYY-MM-DD] Node.js LTS 정책 페이지
[T2|EN|YYYY-MM-DD] LogRocket "Setting up Expo in 202x"
[T3|EN|YYYY-MM-DD] r/expo 상위 설치 막힘 스레드
[T3|KO|YYYY-MM-DD] Velog "Expo 설치 처음 해봤다" 류 입문 글
```

> 본 예시에는 버전·날짜 사실값을 적지 않음. 작성자(Claude)가 1차 출처를 직접 확인하지 않은 상태에서 적으면 Source 팀이 그 값을 기준으로 검색할 위험. (제1원칙)

### 7-4. NotebookLM 분석 질의문

1. 2026년 5월 기준 Expo 공식 docs가 권장하는 CLI 설치/호출 방식은? 글로벌 `expo-cli` 패키지가 deprecated 상태인지 명시적으로 확인.
2. Expo CLI를 쓰기 위한 Node.js 요구·권장 버전 범위와 LTS 정책상 어느 라인이 권장되는지를 정리.
3. 현 시점 Expo 공식이 분류로 안내하는 호스트 OS 목록(macOS / Windows / WSL / Linux 등 `[?] 분류 체계 전제 미확인`)을 확인한 뒤, 각 OS별 추가 사전 도구(watchman·CommandLineTools·JDK·Android Studio 등)를 표로 비교.
4. Expo Go 앱만으로 입문자가 도달 가능한 학습 단계와 한계는 무엇인가? Development Build로 전환이 필요한 시점은?
5. iOS 시뮬레이터·Android 에뮬레이터를 입문 단계에서 준비하지 않고 학습 가능한 경로가 있는가? 있다면 어디까지 가능한가?
6. 입문자가 설치 단계에서 자주 막히는 사례 5가지와 통상 해결책을 자료 근거로 정리.
7. 옛 `expo-cli` 글로벌 패키지를 가진 사용자가 현행 방식으로 옮길 때의 제거·재설치 절차는?
8. 한국어 자료 중 입문자가 신뢰하고 따라갈 만한 설치 가이드는 어떤 출처에 있는가?

### 7-5. 추출 후 산출물 위치

- NotebookLM Notes 내 정리 → 최종 통합본은 로컬:
  `output/[2026-05-23][Mobile] Expo CLI 설치 전 준비물_결과.md`

---

## 8. 품질 검증 체크리스트 (실행 전)

### 제1원칙: 사실관계 마커
- [x] 직접 1차 출처를 확인하지 못한 사실값(버전·요구사항·분류 체계·자료원 성격 등)에 모두 `[?]` 부착
- [x] 마커가 `[?]` **단일 형태**로 통일 (`[모름]`, `TBD` 혼용 없음)
- [x] 30초 룰 적용 — 본 Plan에서 작성자(Claude)는 사실값을 직접 확인하지 않고 모두 `[?]` 처리
- [x] LLM 작성자 특례 적용: training data 회상은 모두 `[?] LLM 추정`

### 내용 품질
- [x] 주제 한 줄 (시점·지역·대상 명시)
- [x] 목적이 결정/산출물 단위
- [x] "알 필요 없는 것" 6개 명시
- [x] 핵심 질문 7개 (5~10개 범위, 모두 자료로 답 가능)
- [x] 키워드 원어 그대로, 영어 ≥ 3개 충족
- [x] T1 6개·T2 5개·T3 6개로 한쪽 쏠림 없음
- [x] `API 필요 여부` 컬럼이 모든 자료원 행에 기록
- [x] 자료원 성격 단정 자리에 `[?] LLM 추정` 부착 (Software Mansion·코딩애플·LogRocket Expo 글 빈도 등)
- [x] 9-5 골격 포함

---

## 9. Gap Report (실행 후 — Source 팀 작성)

### 9-1. 부족했던 자료 영역
- 

### 9-2. 추가로 발급/연동했어야 할 API
- (예시 후보: youtube-transcript-api / yt-dlp — T3 YouTube 자막용으로 5-3에 사전 명기됨)

### 9-3. 다음 유사 주제에서 추가할 자료원
- 

### 9-4. 도메인 프로파일 승격 후보
> "모바일 프레임워크 입문 환경" 도메인 프로파일로 묶을 자료원 후보:
- (초안) Expo Get Started · RN Environment setup · Node.js LTS · Watchman 공식 · Android Studio 공식 · r/expo · Stack Overflow expo 태그

### 9-5. Plan 사실관계 검증 결과
> Plan 본문에 박힌 작성자 단정 vs NotebookLM 적재 자료의 일치 여부 사후 점검.

- 검증 통과 (작성자 단정 ↔ NotebookLM 자료 일치): [n건]
- 검증 실패 (작성자 단정 ↔ NotebookLM 자료 불일치, 어디?): [n건]
- 마커 `[?]`로 표시되어 Source가 확인한 항목: [n건]
  - 사유 코드별 분포 (LLM 추정 / 30초 룰 위반 / 검증 안 함: 일반적 인상 / 분류 체계 전제 미확인 / 사유 생략): [집계]
- 다음 Plan 작성 시 참고할 패턴: 
