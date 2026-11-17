# 16. 위협 모델과 재현 가능한 검증 절차

> 이 장은 **공개 자료에 근거한 보안·시스템 분석**이다. 서비스 침투 시험, 실제 계정 실험, 코드 전체의 형식 검증, 제3자 보안 감사가 아니다. 출처의 정확한 버전은 [`credential-enclave` commit `cff16a3`](https://github.com/pickle-com/credential-enclave/tree/cff16a343bf5bb7953e5b65df6ab3600107e127d)이며, 최신 release 태그는 분석 당시 `v2.3.0`이었다.

## 위협 모델: 자산, 상대, 신뢰 가정

| 자산 | 가능한 위협 | 공개 설계의 대응 | 남는 가정·위험 |
| --- | --- | --- | --- |
| 기기 마스터 키 | 유출·변조 앱 | Keychain 및 기기 측 secure program | 앱 바이너리 자체는 아직 공개되지 않아 정직성을 가정 |
| OAuth 토큰 | operator의 토큰 탈취 | enclave 내부 교환·사용, 외부 반환 제한 | PKCE가 없는 연결과 과거 import 경로의 예외 |
| Vault 값 | 브라우저·worker에 노출 | 저장·사용 전까지 enclave 보호, 필드별 `release` | 반환 후 평문을 받는 실행 환경을 신뢰해야 함 |
| 계정 데이터 | 과도한 API 읽기·AI 처리 | provider 목적지 및 권한 경계 | 응답 내용은 작업 처리를 위해 operator 영역으로 이동 가능 |
| 사용 기록 | 삭제·변조·은폐 | 선행 S3 Object Lock 기록, 서명·해시 체인 | AWS·operator 계정, 불완전 head, node 누락 |
| 위임 키 | 오래된 노드의 지속 접근 | 최대 30일 위임, 철회 처리 | 누락된 살아 있는 node에 잔여 위임 가능 |

## 반례로 보는 보장 범위

보안 주장은 반례를 만들어 보면 더 정확해진다. 다음 사례는 공개 소스가 **스스로 제한으로 적은 상황**을 일상 작업으로 바꾼 것이다.

| 겉으로 보이는 주장 | 반례·조건 | 근거 |
| --- | --- | --- |
| “토큰이 enclave에 있으니 연결 서비스의 모든 정보가 비공개다” | 메일 본문 같은 API 응답은 작업 처리를 위해 operator 쪽으로 나간다 | [`README`의 What a credential fetches](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md#what-it-does-not-guarantee) |
| “연결 해제하면 즉시 모든 접근이 끝난다” | operator가 살아 있는 node를 철회 목록에서 누락하면 해당 위임은 만료 전까지 남을 수 있다 | 같은 README의 Withdrawing a delegation |
| “허용된 API 목적지는 오직 한 요청이다” | provider API 허용 목록이 경로 접두사이면 그 아래 여러 주소에 토큰이 도달할 수 있다 | 같은 README의 Width of the address lists |
| “암호문은 항상 가장 최신 상태다” | operator가 예전 암호화 레코드를 node에 다시 제시할 수 있다 | 같은 README의 Freshness of a record |
| “API 호출 로그가 있으면 후속 접근도 통제된다” | API 호출이 provider 쪽의 지속 감시·공유 링크·서명 URL을 만들 수 있다 | 같은 README의 APIs that open a lasting access |
| “암호화는 메타데이터까지 숨긴다” | 응답 크기와 시간은 관찰될 수 있다 | 같은 README의 Side channels |

이 반례는 실제 사고 발생을 주장하지 않는다. **설계의 보장 범위를 지나치게 넓게 해석하지 않기 위한 시험 사례**다. 예를 들어 예전 레코드 재제시는 비밀을 읽게 하는 취약점이라기보다 **무결성·최신성**의 제한이다. 위험의 종류까지 구분해야 후속 대응도 정확해진다.

위협 모델은 “안전/불안전”이라는 단답을 피한다. 보호 수준은 **어떤 자산이 어느 경계 안에 있을 때**에 따라 달라진다. 예를 들어 토큰 비공개와 이메일 내용 비공개는 다른 성질이다. 전자는 공개 enclave 소스가 비교적 강하게 다루지만, 후자는 작업 목적상 성립하지 않을 수 있다.

## 공개 소스에서 확인한 강점과 제한

| 주장 | 근거 | 판단 |
| --- | --- | --- |
| node의 실행 이미지 측정값을 attestation으로 확인할 수 있다 | [`README` 검증 절차](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md) | **소스상 확인**. 실제 서비스 노드 검증은 미수행. |
| 자격 증명 사용 기록을 선행 저장한다 | [`README` 보장 표](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md), [프로토콜](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/protocol.md) | **소스상 확인**. 시도와 성공을 구분해야 함. |
| Vault가 모든 순간의 비밀을 operator에게 숨긴다 | [`egress policy`의 `release` 한계](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/egress-policy.md) | **성립하지 않음**. 반환 후 평문 경계가 바뀜. |
| 모든 AI 모델과 안전 정책이 공개되었다 | 공개 저장소의 범위 | **근거 없음**. 모델·플래너·음성·브라우저 실행 코드는 미공개. |
| 현재 서비스가 공개 코드와 동일한 노드를 실행한다 | attestation과 빌드 측정값 실측 필요 | **미검증**. 정적 소스 리뷰만으로는 결론 불가. |

## 재현 절차

기술 독자는 다음 순서로 이 분석을 다시 확인할 수 있다. **실서비스 검증에는 해당 계정의 접근 가능 노드와 release 파일이 필요**하다.

1. [`pickle-com/credential-enclave`](https://github.com/pickle-com/credential-enclave)를 받으면서 commit `cff16a343bf5bb7953e5b65df6ab3600107e127d`를 고정한다. `README.md`, `docs/protocol.md`, `docs/egress-policy.md`, `secure-program/README.md`를 읽는다.
2. `README`의 “What the source guarantees”와 “What it does not guarantee”를 나란히 대조한다. 특히 `release`, PKCE 예외, 기록의 최종 head, 위임 이전을 확인한다.
3. release 태그의 `measurements.json`과 공식 검증 도구를 사용한다. 가능하면 독립 환경에서 enclave 이미지를 재현 빌드하고 PCR0·PCR1·PCR2를 비교한다. [공식 검증 명령](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md#how-to-verify)을 따른다.
4. 실행 node의 attestation을 nonce와 함께 받아 AWS 인증서 체인, 측정값, 공개 키 바인딩을 검증한다. nonce 없이 저장된 문서만 보는 것은 현재 실행 상태의 증명이 아니다.
5. 앱 접근 로그, 외부 provider의 사용 내역, 예약·결제 결과를 대조한다. 로그 항목의 존재를 작업 성공으로 세지 않는다.

이 책은 1–2단계의 **문서와 소스 구조 검토**를 수행했다. 3–5단계는 실제 서비스 환경·계정에 대한 독립 실측이 필요하므로 수행했다고 주장하지 않는다.

## 남아 있는 연구 질문

1. 어떤 입력 표현(스크린샷, DOM, 접근성 트리)을 브라우저 에이전트가 사용하며, 실패 후 어떻게 상태를 복구하는가?
2. 음성 통화의 ASR·TTS·대화 제어는 어떤 지연과 오류율을 갖는가?
3. 기억의 저장·수정·검색은 어떤 구조이며, 잘못된 기억이 반복 실행에 어떻게 전파되는가?
4. 앱의 승인 UI에서 정한 금액·상점·수신자 경계가 어느 서버 구성 요소에서 강제되는가?
5. 공개 소스의 현재 release와 실제 사용자의 지역·플랜·앱 바이너리 사이에 어떤 차이가 있는가?

이 질문들은 추측으로 메우지 않는다. 회사의 추가 공개 자료나 재현 가능한 실측이 나오면 [출처 목록](../docs/SOURCES.md)에 버전과 날짜를 남기고 개정한다.

