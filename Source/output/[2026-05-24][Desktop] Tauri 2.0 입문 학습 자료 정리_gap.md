# Gap Report — Tauri 2.0 입문 학습 자료 정리

> Source팀 첫 실전 의뢰. Plan §9 골격을 채워서 회수.

---

## 0. 메타

| 항목 | 내용 |
|---|---|
| 원본 Plan | `~/work/research/Plan/output/[2026-05-24][Desktop] Tauri 2.0 입문 학습 자료 정리.md` |
| Source 입력 사본 | (인계 안 받음 — Source/input/ 복사 단계 생략하고 Plan 원본 직접 참조) |
| 수집 실행일 | 2026-05-24 |
| 가동 페르소나 | `research-collector` v0.1 (Algorithm 5단계 전수) |
| NotebookLM 노트북 | [2026-05-24][Desktop] Tauri 2.0 입문 학습 자료 정리 |
| 노트북 ID | `0dd7048a-98f7-40b5-800c-07f79006abc6` |
| 노트북 URL | https://notebooklm.google.com/notebook/0dd7048a-98f7-40b5-800c-07f79006abc6 |
| 노트북 노트 | "소스 메타 라벨 (Plan §7-3)" (note_id: `92bfcd74-2756-4a52-aace-19e1f1d36315`) |
| 총 소스 적재 | 18건 시도 / 16건 NotebookLM 적재 / **실질 콘텐츠 가용 9건** |
| Tier 비율 (실질) | T1 44% (4/9) / T2 33% (3/9) / T3 22% (2/9) — Plan §6 목표 충족 |
| Q 답 가능성 | 8 중 6 완전 답 / 1 부분 답 / 1 갭 |

---

## 9-1. 부족했던 자료 영역

### 1) 공식 사이트 SPA 렌더링으로 인한 정적 fetch 한계

- `tauri.app` 메인 페이지·Guides·References는 NotebookLM이 정적 fetch만 수행 → 메뉴 구조·메인 카피만 인덱싱
- 결과: §2-2-4 (공식 권장 학습 경로 세부 순서), §2-2-8 (Rust 사전 지식 요구치) 두 항목 미확보
- 회피책: Plan에서 학습 경로 세부 페이지(예: `tauri.app/start/prerequisites`) URL을 직접 지정하면 적재 가능

### 2) 한국어 영상·강의 자료 부재

- Plan §5-3 한국어 YouTube 검색식 URL 적재 시 NotebookLM이 "Enable JavaScript" 빈 페이지로 인식
- 자막 추출 기능도 미가동 (Plan §5-3 row 3 `[? Source 팀 결정]` 마커였음)
- 결과: 한국어 영상·강의 0건 (Q5 답변에 명시)

### 3) 한국 기업 기술 블로그 Tauri 사용 사례 부재 + 검색 인프라 부재

- Plan §5-3 row 6: 카카오·우아한형제 등 기업 기술 블로그 `site:` Google 검색식 → 봇 차단으로 적재 자체 실패 (적재 실패 2건)
- 변형 보강: 각 블로그 자체 검색 URL (`?s=Tauri`) 4건 시도 → 모두 메인 페이지 fallback (SPA 검색 결과 렌더링)
- 결과: 한국 기업 블로그 Tauri 사용 사례 0건 (Q8 명시)
- 추정: Tauri 자체가 한국 대형 IT 기업 프로덕션 도입이 적은 분야라 글 자체가 부재할 가능성 (적재 갭이 아니라 콘텐츠 자체 갭일 수 있음)

### 4) 한국 GitHub repo (한국어 README) 검색 실패

- Plan §5-3 row 5: GitHub `language:ko Tauri` 검색식 URL 적재 → "Enable JavaScript" 빈 페이지
- 결과: 한국 한국어 README repo 0건 (Q8 명시)
- 회피책: GitHub Search API를 사용 시 JSON 응답 가능. NotebookLM MCP에 GitHub PAT 발급·연동 필요 (현재 미지원 또는 미설정)

### 5) Tistory Tauri 글 검색 실패

- Plan §5-3 row 2: Google `site:tistory.com Tauri` 검색식 → 봇 차단, 적재 실패
- Tistory 자체 통합 검색 URL 부재 (각 블로그별 검색만)
- 회피책: 개별 Tistory 블로그 URL을 사전 발굴해서 직접 적재

---

## 9-2. 추가로 발급/연동했어야 할 API

- **GitHub REST API + PAT**: Plan §5-1 row 2 (releases), row 4 (examples), §5-3 row 5 (한국어 repo 검색)에서 명시. 그러나 NotebookLM MCP는 URL 기반 fetch만 지원 → API 호출은 NotebookLM이 못 함. 우회: GitHub 웹 페이지 URL은 fetch 가능 (실제로 releases·examples는 웹 페이지 적재 성공)
- **YouTube Data API**: 자막 추출 등 영상 메타 수집. Plan §5-3 row 3에서 `[? Source 팀 결정]` 마커였으나 현재 환경에서 미가동
- **각 한국 기업 기술 블로그 API 또는 RSS**: 자체 검색 SPA 우회용. RSS는 카카오·우아한형제·토스 모두 제공 가능성 있음 (다음 Plan 패턴 개선 입력)

---

## 9-3. 다음 유사 주제에서 추가할 자료원

신규 OSS 데스크탑 프레임워크 입문 자료 정리 의뢰가 들어오면 다음을 §5-1~§5-3에 사전 등재 권장:

- **공식 사이트의 학습 경로 페이지를 깊이 1단계까지 명시** (예: `tauri.app/start/`가 아니라 `tauri.app/start/create-project/`, `tauri.app/start/prerequisites/` 등)
- **GitHub releases는 RSS URL로 등재** (`https://github.com/{org}/{repo}/releases.atom`) — NotebookLM이 RSS 안정적 fetch
- **한국어 Velog 태그 페이지** — 한국어 자료 핵심 (Tauri의 경우 13건 적재 성공한 유일한 한국어 풍부 소스)
- **dev.kr · GeekNews 한국어 카테고리** — 미검토. 다음 Plan 시도 권고
- **Awesome Korean Rust** 등 한국어 큐레이션 repo — Plan §5-3에 정식 등재 권고
- **YouTube 자체 검색 URL 대신 특정 채널 URL** (예: `youtube.com/@생활코딩`, `youtube.com/@DevwithDavid`) 직접 발굴

---

## 9-4. 도메인 프로파일 승격 후보

**도메인: Desktop Application Framework (Plan §9-4 정의 차용)**

다음 패턴이 재사용 가치 높음:

### T1 패턴 (4건 모두 검증 통과)
- 공식 사이트 메인 URL (`https://{프레임워크}.app/`) — 메인 카피·차별점 추출 가능
- GitHub releases URL (`https://github.com/{org}/{repo}/releases`) — 최신 안정 버전·날짜 추출 가능
- 공식 블로그 (`https://{프레임워크}.app/blog/`) — 메이저 릴리스 공지 일자 추출 가능
- 공식 examples 저장소 (`https://github.com/{org}/{repo}/tree/{branch}/examples`) — 입문 예제 디렉토리 목록 추출 가능

→ Wails, Slint, Neutralino, Sciter 등 다른 데스크탑 프레임워크 Plan에도 동일 구조 그대로 재사용 가능. **승격 권고**.

### T3 패턴 (한국어 자료 가용성 평가)
- Velog 태그 페이지: 성공 ✅ (NotebookLM이 동적 태그 페이지를 정상 fetch — 검증됨)
- Reddit 서브레딧: 성공 ✅
- Tistory `site:` 검색식: 실패 ❌ (Google 봇 차단)
- 한국 기업 기술 블로그 자체 검색: 실패 ❌ (SPA 렌더링)
- GitHub 검색 페이지: 실패 ❌ (JS 필요)

→ 한국어 자료 정리 Plan은 **Velog 태그 페이지를 핵심 자료원으로 박을 것**. Tistory·기업 블로그는 검색식이 아닌 개별 URL을 사전 발굴해야 함. **승격 권고: Velog 태그 페이지 패턴**.

---

## 9-5. Plan 사실관계 검증 결과

Plan 본문에 들어간 작성자 단정 (`[?]` 마커 부착 항목) ↔ NotebookLM 적재 자료 일치 여부 사후 점검.

| Plan 위치 | 단정 내용 | 마커 | NotebookLM 확인 결과 |
|---|---|---|---|
| §2-2-1 | Tauri 2.0 정식 출시 여부·안정 버전 | `[? LLM 추정]` | ✅ **검증**. 출시일 2024-10-02 (공식 블로그), 최신 v2.11.2 (GitHub releases 2026-05-16). 마커 제거 가능. |
| §2-2-2 | 2.0의 1.x 대비 변경점 (모바일 지원) | `[? LLM 추정]` | ✅ **검증**. 공식 메인 페이지에 "Linux, macOS, Windows, Android and iOS - all from a single codebase" 명시. Swift/Kotlin 네이티브 통합. 단, 구체 breaking changes 항목은 미확보. 마커 부분 제거 가능. |
| §2-2-3 | Electron 대비 차별점 수치 | `[? LLM 추정]` | ✅ **검증 (정성)**. Minimal Size 600KB, Cross Platform, Frontend Independent 3가지 공식 표방 확인. **단, 메모리·성능 수치는 공식 미포함 (커뮤니티 사례 6MB만 확인)**. 마커는 "수치는 미확보" 형태로 변형 권고. |
| §2-2-4 | 공식 권장 학습 경로 URL | `[? 30초 룰 위반]` | 🟡 **부분 검증**. tauri.app은 살아있고 Get started·Guides·References 메뉴 존재 확인. 단 세부 학습 경로 순서는 SPA 렌더링으로 정적 fetch 미포함. 마커는 `[? Source 30초 룰 부분 통과]`로 변형 권고. |
| §2-2-5 | 한국어 자료 가용성 | `[? LLM 추정]` | ✅ **검증**. Velog에 13건 한국어 글 확인 (작성자 8명, 2022-01 ~ 2026-04). 입문 시리즈 작성자 1명(@zigizibangsi) 존재. YouTube·강의는 미적재 (검색 실패). 마커는 "Velog 풍부, 영상은 부재"로 변형 권고. |
| §2-2-8 | Rust 사전 지식 요구치 | `[? LLM 추정]` | ❌ **갭**. 공식 출처에 "Rust 기초/중급" 등 표현 미포함. 일반 언급("application logic in Rust")만. 마커 유지 + Plan에서 `tauri.app/start/prerequisites/` 같은 깊은 URL 사전 등재 권고. |
| §5-1 row 1 | `tauri.app` 가용성 | `[? 30초 룰 위반]` | ✅ **검증**. URL 유효, NotebookLM 정상 적재 (title: "Tauri 2.0 | Tauri"). 마커 제거 가능. |
| §5-1 row 3 | `tauri.app/blog` 존재 | `[? LLM 추정]` | ✅ **검증**. URL 유효, 정상 적재 (title: "Blog | Tauri"). 마커 제거 가능. |
| §5-1 row 4 | 공식 examples 저장소 경로 | `[? LLM 추정]` | ✅ **검증**. `dev/examples` 경로 유효, 14개 디렉토리 확인 (`api, commands, drag, file-associations, helloworld, icons, isolation, multiwebview, multiwindow, resources, run-return, splashscreen, state, streaming`). 마커 제거 가능. |
| §5-2 전 행 | T2 매체 Tauri 기사 존재 | `[? LLM 추정]` | 🟡 **부분 검증**. HackerNews Algolia 검색에서 Tauri 2.0 관련 21건 thread 확인. Dev.to·The New Stack 인덱스 페이지 적재 성공. **InfoQ는 검색 결과 페이지 인덱싱 실패, 메인 fallback**. 마커는 "InfoQ 갭"으로 변형 권고. |
| §5-3 전 행 | T3 한국어 자료 가용성 | `[? LLM 추정]` / `[? 검증 안 함: 일반적 인상]` | 🟡 **부분 검증**. Velog ✅ (13건), Reddit ✅. **Tistory·한국 기업 블로그·YouTube·GitHub 한국어 검색 모두 적재 실패**. 마커는 "Velog 외 한국어 자료 적재 인프라 보강 필요"로 변형 권고. |

### 집계

- **검증 통과** (작성자 단정 ↔ NotebookLM 자료 일치): **7건** (§2-2-1, §2-2-2, §2-2-3, §2-2-5, §5-1 row 1, row 3, row 4)
- **부분 검증**: **3건** (§2-2-4, §5-2, §5-3)
- **검증 실패 (갭)**: **1건** (§2-2-8 Rust 사전 지식)
- **마커 `[?]`로 표시되어 Source가 확인한 항목**: **11건 전수**

### 다음 Plan 작성 시 참고할 패턴

1. **신규 OSS 입문 자료 정리 의뢰 패턴**: 공식 URL을 페르소나가 30초 룰로 확인하도록 강제 (§5-1은 4건 모두 통과). `[? 30초 룰 위반]` 마커가 본 표에 부착될 경우, **본 Plan처럼 §5-4 없이 본 표에 마커 부착 형태**는 D-C 정책(`handoff_interface.md` §3-2~§3-4)과 충돌. **§5-4 신설 + 마커 부착 자료원 이동 권고** (본 의뢰서로는 변형하지 않음, Plan팀 패치 영역).
2. **공식 사이트의 SPA 페이지는 메인 URL이 아니라 깊이 1~2단계 페이지 URL을 사전 등재**. 예: `tauri.app/start/prerequisites/`, `tauri.app/start/create-project/` 형태
3. **한국어 자료 정리는 Velog 태그 페이지를 1순위로 박기** (Tauri 사례에서 13건 적재 성공한 유일한 한국어 소스)
4. **Google `site:` 검색식은 NotebookLM 봇 차단으로 실패** — 대안: 사이트 자체 RSS, 자체 검색 결과 정적 페이지, 또는 개별 글 URL 사전 발굴
5. **GitHub 검색 페이지·YouTube 검색 페이지는 JS 필수로 빈 페이지** — 대안: GitHub API + JSON, YouTube API 또는 특정 채널 URL 직접 등재

---

## 추가: 변형 검색 사유·횟수 (Algorithm step 3 자율 판단 기록)

| 회차 | 자료원 | 변형 사유 | 시도 결과 |
|---|---|---|---|
| 1 | The New Stack `site:` (Plan §5-2) | Google 봇 차단 위험 | `thenewstack.io/?s=Tauri` 자체 검색 사용 → ✅ 적재 성공 |
| 1 | InfoQ `site:` (Plan §5-2) | 동상 | `infoq.com/search.action?queryString=Tauri` 사용 → ❌ 메인 fallback |
| 1 | Tistory `site:` (Plan §5-3) | 동상 | Google 검색 URL 사용 → ❌ 적재 실패 (봇 차단) |
| 1 | 한국 기업 `site:` (Plan §5-3) | 동상 | Google 검색 URL 사용 → ❌ 적재 실패 |
| 2 | 한국 기업 블로그 (1차 변형 실패 후) | SPA fallback 회피 | 4개 블로그 자체 검색 URL (`?s=Tauri`, `?q=Tauri`) 시도 → ❌ 모두 메인 fallback 또는 보안 차단 (우아한형제) |

**총 변형 시도 횟수: 6건. 성공 1건 (The New Stack), 실패 5건.** 페르소나 본분상 추가 변형 중단 + 갭 정직 기록 선택.

---

## 추가: D-C 정책 부재 환류 (Plan팀 별도 의뢰 권고)

본 Plan의 §5에는 **§5-4 후보 자료원 섹션이 부재**. `handoff_interface.md` §3-2~§3-4 D-C 정책은 30초 룰 미통과 자료원을 §5-4로 분리하도록 명시. 그러나 본 Plan은 `[? 30초 룰 위반]` (2건) / `[? LLM 추정]` (다수) 마커 자료원이 §5-1~§5-3 본 표에 산재.

본 Source 수집은 페르소나 본분("계획 변형 금지") 따라 §5-4 임의 신설 없이 진행. §9-5 검증 결과 표로 사후 처리.

**Plan팀 권고**:
1. `research-strategist-hypothesis` v0.1.x Algorithm에 §5-4 분리 의무 추가 (마커 부착 자료원 → §5-4 자동 이동)
2. 또는 `templates/search_plan_template.md` §5-4 섹션 의무 항목으로 격상
3. `quality_checklist.md`에 "§5-4 분리 점검" 체크박스 추가

별도 의뢰서 가능 영역. 본 의뢰서로 결정하지 않음 (Source 권한 밖).
