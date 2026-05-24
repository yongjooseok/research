# API 인증 및 키 관리 정책 추천안

## 요약 (한 줄씩)

| 정책 | 추천 |
|---|---|
| API 키 저장 | **OS Keychain 우선, .env fallback** |
| MCP 권한 분리 | **Tier별 화이트리스트** |
| API 등록 절차 | **CLI + 설정파일 + 대화형 혼합** |
| 키 회전 | **자동 알림만 (90일 기준)** |

---

## 1. API 키 저장 위치

### 옵션 비교

| 옵션 | 보안 | 사용성 | 크로스플랫폼 | 적합 사용자 |
|---|---|---|---|---|
| `.env` 파일만 | 낮음 | 높음 | 좋음 | 개발자 |
| OS Keychain만 | 높음 | 중간 | 한정 | macOS 위주 |
| 별도 vault (1Password 등) | 매우 높음 | 낮음 | 좋음 | 엔터프라이즈 |
| **OS Keychain + .env fallback** | **높음** | **높음** | **좋음** | **광범위** |

### 추천: OS Keychain 우선 + .env fallback

근거:
- 로그가 macOS 여러 대 사용 → Keychain 친숙
- 일반 사용자(변리사·의사 등 비개발자)도 안전
- Linux/Windows/CI 환경은 .env fallback으로 커버
- 구현: 키 접근 인터페이스 하나만 추상화하면 됨

코드 흐름:
```
1. OS Keychain 조회
2. 없으면 .env 조회
3. 둘 다 없으면 사용자에게 등록 안내
```

---

## 2. MCP 권한 분리

### 옵션 비교

| 옵션 | 명확성 | 안전성 | 구현 |
|---|---|---|---|
| 모든 Tier가 모든 MCP | 낮음 | 낮음 | 단순 |
| **Tier별 화이트리스트** | **높음** | **높음** | **중간** |
| Allow + Deny 혼합 | 매우 높음 | 매우 높음 | 복잡 |

### 추천: Tier별 화이트리스트

근거:
- 분리의 본래 목적이 책임 명확화
- 잘못된 도구 호출 차단 (Plan이 실수로 notebooklm_query 호출 등)
- 디버깅 용이

### Tier별 권한 매트릭스 (추정안)

| MCP / Tool | Router | Plan | Source | Extract |
|---|---|---|---|---|
| 분류/라우팅 | ✅ | ❌ | ❌ | ❌ |
| Notion (도메인 프로파일) | ❌ | ✅ | ❌ | ❌ |
| notebooklm: notebook_create | ❌ | ❌ | ✅ | ❌ |
| notebooklm: research_start | ❌ | ❌ | ✅ | ❌ |
| notebooklm: source_add | ❌ | ❌ | ✅ | ❌ |
| notebooklm: notebook_query | ❌ | ❌ | ❌ | ✅ |
| playwright | ❌ | ❌ | ✅ | ❌ |
| Core API (KOSIS/DART 등) | ❌ | ❌ | ✅ | ❌ |
| Domain API (특허청 등) | ❌ | ❌ | ✅ | ❌ |
| qa_*_verifier | ❌ | ❌ | ❌ | ✅ |
| 키 인증 관리 | ✅ | ✅ | ✅ | ✅ |

대부분의 도구가 Source 또는 Extract에 집중됨. Plan은 의외로 가벼움. Router는 거의 권한 없음 (의도된 설계).

---

## 3. 사용자 추가 API 등록 절차

### 옵션 비교

| 옵션 | 속도 | 진입장벽 | 일괄 관리 |
|---|---|---|---|
| CLI만 | 빠름 | 중간 | 어려움 |
| 설정 파일만 | 느림 | 높음 | 좋음 |
| 대화형만 | 친숙 | 낮음 | 어려움 |
| **3가지 혼합** | **상황별** | **낮음** | **좋음** |

### 추천: 혼합 (3가지 모두 지원)

근거:
- 사용자 유형이 다양함 (개발자·변리사·의사·1인 기업가)
- 시나리오별로 다른 방식이 적합

### 시나리오별 사용 방식

**시나리오 A — 빠른 등록 (개발자):**
```bash
nexus api add patent_kr --key=XXXX --provider="특허청" --domain="patent"
```

**시나리오 B — 일괄 관리 (여러 API 한 번에):**
```yaml
# ~/.nexus/apis.yaml
apis:
  - name: patent_kr
    provider: 특허청
    domain: patent
    key_ref: keychain://nexus/patent_kr
```

**시나리오 C — Gap Report 트리거 대화형 (비기술자):**
```
Gap Report:
  "특허 자료가 부족합니다. Google Patents API 추가하시겠어요?"

User: "응 추가할래"

NEXUS:
  1. 발급처 안내 (URL + 절차)
  2. 키 받으면 입력 요청
  3. 자동 검증 → keychain 저장
  4. 도메인 프로파일 자동 매핑
```

→ 이 시나리오 C가 **자가 진화 루프의 실체화**.

---

## 4. 키 회전 정책

### 옵션 비교

| 옵션 | 보안 | 사용성 | 1인 운영 적합성 |
|---|---|---|---|
| 회전 없음 | 약함 | 최상 | 무책임 |
| **자동 알림 (강제 X)** | **중간** | **상** | **적합** |
| 강제 회전 (만료 후 사용 불가) | 최상 | 하 | 과함 |

### 추천: 자동 알림 (90일 기본, 사용자 변경 가능)

근거:
- 플러그인 = 1인~소규모 사용자가 대부분
- 강제 회전은 엔터프라이즈급 정책. 과함.
- 알림으로 인식만 주면 사용자 자율 판단
- 단, 회전 없음은 무책임

### 알림 정책

| 시점 | 동작 |
|---|---|
| 키 등록 시 | `expires_at = now + 90일` 자동 기록 |
| 만료 30일 전 | Gap Report에 "갱신 권장" 표시 |
| 만료 7일 전 | Plan/Source 실행 시 경고 |
| 만료 후 | 사용은 계속 가능, "만료됨" 라벨 |
| 6개월 미사용 | "비활성" 표시 (자동 삭제 X) |

핵심 원칙:
- **자동 삭제 절대 금지** (사용자 데이터 보존)
- **사용 차단 절대 금지** (강제 회전 X)
- 알림과 라벨링만 (사용자 판단 존중)

---

## 통합 정책 (yaml로 정리)

```yaml
authentication_policy:
  
  storage:
    primary: os_keychain
    fallback: dotenv
    keychain_service: "nexus-research"
    reason: 보안과 사용성의 균형
  
  mcp_permissions:
    model: tier_whitelist
    enforce: strict  # 권한 외 호출 시 차단
    
    tiers:
      router: [routing_classifier]
      plan: [notion, domain_profile_reader]
      source: [notebooklm_write, playwright, core_apis, domain_apis]
      extract: [notebooklm_query, qa_verifiers]
      shared: [auth_manager]
  
  user_api_registration:
    methods:
      - cli_command           # 빠른 등록
      - config_yaml           # 일괄 관리
      - conversational_flow   # Gap Report 트리거 (비기술자 친화)
    
    auto_validation: true     # 등록 시 키 검증
    auto_map_to_domain: true  # 도메인 프로파일에 자동 매핑
  
  key_rotation:
    policy: notification_only
    default_expiry_days: 90
    user_configurable: true
    
    notifications:
      - days_before: 30
        location: gap_report
      - days_before: 7
        location: plan_source_runtime
      - on_expiry:
          action: label_only
          deny_usage: false
      - on_inactivity_6m:
          action: mark_inactive
          auto_delete: false  # 절대 자동 삭제 X
    
    principles:
      - 자동 삭제 금지
      - 사용 차단 금지
      - 사용자 자율 판단 우선
```

---

## 정책의 일관된 철학

4개 정책을 관통하는 원칙:

```
"보안은 자동, 통제는 사용자"

- 저장: OS가 알아서 안전하게 (자동)
- 권한: 시스템이 명확하게 분리 (자동)
- 등록: 사용자가 편한 방식 선택 (자율)
- 회전: 알림은 자동, 결정은 사용자 (자율)
```

자동화로 보안 부담을 줄이되,
사용자의 통제권은 절대 빼앗지 않는다.

이게 1인~소규모 사용자 도구의 적정 균형.

---

## 다음 단계

이 정책 확정 시 양식의 섹션 8 (`MCP, Tools & Authentication`)에 그대로 들어갑니다.

확정 여부 알려주시면 **Step 2: Plan 축 상세 계획서 작성**으로 진입.
