# 14. 계정 연결: OAuth, 토큰, 외부 데이터의 경계

> 이 장은 [공개 소스의 연결 흐름](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md)과 [egress policy](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/egress-policy.md)를 분석한다. 실제 연결 가능한 앱과 권한 목록은 계정·시점별로 바뀔 수 있다.

## OAuth가 해결하는 문제와 남기는 문제

OAuth 연결에서는 사용자가 서비스 제공자에게 피클의 접근 범위를 승인하고, 피클 쪽은 발급된 토큰으로 API를 호출한다. 이는 서비스 비밀번호를 매번 넘기는 방식과 다르다. 공개 소스의 node는 지원되는 연결에서 토큰을 enclave 안에서 받아 사용하고, `forward` 요청을 미리 정의된 provider 주소로 보낸다고 설명한다. 하지만 **토큰을 숨기는 것과 API 응답 데이터까지 숨기는 것은 별개**다. 이메일 본문, 문서 내용, 계정 정보 같은 응답은 작업을 수행하기 위해 운영자 쪽 AI 시스템으로 넘어갈 수 있다.

| 데이터 | 공개 소스가 말하는 경계 | 독자의 판단 |
| --- | --- | --- |
| OAuth access/refresh token | 지원 경로에서 node 안에서 발급·사용; `release`로 반환하지 않음 | 토큰 보호와 서비스 데이터 처리 범위를 구분 |
| API 응답 내용 | 피클의 작업 처리 영역으로 전달될 수 있음 | 읽기 권한 자체를 최소화 |
| Vault 비밀번호 | `release` 이후 worker/브라우저 쪽에 평문 전달 가능 | 사이트별 로그인 저장 필요성 판단 |
| 카드 번호·CVC | 사용 시 한 필드씩 `release` 가능 | 금액·상점·한도·승인 확인 |
| TOTP seed/코드 | seed는 node 안, 생성된 코드는 밖으로 나갈 수 있음 | 코드 사용 작업을 접근 로그에서 확인 |

## PKCE가 있는 연결과 없는 연결

**PKCE**는 OAuth 승인 코드만 가로채도 토큰으로 교환하기 어렵게 하는 추가 검증자다. 공개 node는 PKCE verifier를 enclave 안에서 만든다고 설명한다. 그러나 [`egress-policy.md`의 한계 표](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/egress-policy.md)에 따르면 **Slack과 Notion처럼 이 구현에서 PKCE를 쓰지 않는 provider**는 승인 코드가 operator callback을 지나가며, operator가 client secret을 보유한다. 따라서 operator가 그 코드를 직접 교환할 수 있다. 이는 “모든 연결의 토큰이 처음부터 operator에게 절대 노출될 수 없다”는 포괄적 주장을 제한한다.

PKCE 적용 여부는 **이 소스 버전의 provider별 구현**에 대한 설명이다. 서비스 제공자의 일반 지원 여부와 혼동하면 안 된다. 연결 목록과 구현은 업데이트될 수 있으므로 최신 release를 재확인한다.

## 허용 주소와 권한 범위

node가 연결 API를 호출할 때 목적지를 제한해도, provider의 API 권한이 넓으면 많은 데이터를 읽을 수 있다. 또한 공개 소스는 일부 주소 허용 규칙이 **접두사 기반이라 넓을 수 있음**을 한계로 적는다. 기술적 통제를 평가할 때는 `토큰 비공개 → 네트워크 목적지 제한 → API 권한 → 응답 데이터 처리`를 **서로 다른 네 가지 질문**으로 봐야 한다.

| 연결 전 질문 | 왜 필요한가 |
| --- | --- |
| 어떤 권한 범위를 승인하나? | 필요한 작업보다 넓은 읽기·쓰기 권한을 피하기 위해 |
| 어떤 데이터가 작업 요청에 실제로 쓰이나? | 토큰이 보호되어도 응답 내용은 AI 작업에 들어갈 수 있어서 |
| 연결을 끊으면 provider 쪽 토큰도 철회되나? | 앱의 목록 삭제와 provider의 권한 철회가 다를 수 있어서 |
| 작업 기록에서 어떤 사용을 확인할 수 있나? | 의도하지 않은 호출을 탐지하기 위해 |

실무적으로는 [05장](https://wikidocs.net/471757)의 최소 권한 원칙에 따라 **작업을 시작하기 직전에 연결하고, 끝난 뒤 provider의 권한 관리 화면까지 확인**하는 것이 좋다. 이는 보안에 대한 제품 약속이 아니라 독자에게 권하는 운영 절차다.

