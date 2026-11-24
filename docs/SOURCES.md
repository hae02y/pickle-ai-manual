# 공식 출처와 확인 범위

최초 확인일: 2026년 11월 2일. 기술 분석의 고정 소스 확인일: **2026년 11월 17일**. 제품 문구 재확인일: **2026년 11월 24일**. 아래는 Pickle.com 및 기반 기술의 공식 자료입니다. 제품 설명과 공개 소스에 대한 정적 분석이며, 독립적인 사용성·보안 감사 결과가 아닙니다.

## 기술 분석의 버전과 1차 자료

| 자료 | 이 책에서 확인한 범위 |
| --- | --- |
| [`pickle-com/credential-enclave` commit `cff16a3`](https://github.com/pickle-com/credential-enclave/tree/cff16a343bf5bb7953e5b65df6ab3600107e127d) | 2026-11-09 소스. 분석 당시 최신 태그 `v2.3.0`과 구분해 고정. README·protocol·egress policy·secure program 문서 중심 정적 분석. |
| [공개 README의 보장과 제한](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md) | 키 위임, attestation, 접근 로그, Vault `release`, PKCE 예외, operator·앱·AWS 신뢰 가정. |
| [프로토콜](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/protocol.md) | HKDF·Ed25519·HPKE·AEAD, 단계별 구현 범위, 로그 체인, release. |
| [Egress policy](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/egress-policy.md) | node 밖으로 나가는 값의 분류와 provider별 한계. |
| [Secure program 문서](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/secure-program/README.md) | 기기 측 프로그램의 범위와 검증 절차. |
| [AWS Nitro attestation](https://docs.aws.amazon.com/enclaves/latest/user/set-up-attestation.html) | 코드 측정값과 공개 키 attestation의 기반 기술. |
| [AWS S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html) | compliance mode의 보존·삭제 방지 성질. |
| [Sigstore Rekor](https://docs.sigstore.dev/logging/overview/) | 투명성 로그의 기본 보장과 포함성 증명의 의미. |

**분석 범위의 한계:** 실행 노드의 attestation과 실제 앱 바이너리를 독립 검증하지 않았습니다. 대화·음성·브라우저·기억 모델의 내부 소스도 공개되지 않았습니다. 11~16장의 모델 설명은 이 한계를 본문마다 표시합니다.

## 2026년 11월 24일 업데이트 노트 확인

| 공식 자료 | 확인한 문서 차이 |
| --- | --- |
| [한국어 약관](https://www.pickle.com/ko/terms-of-service) | 페이지의 시행일이 2026-12-08로 표시됨. 2026-11-24 현재 현행 약관으로 단정하지 않음 |
| [영어 소개](https://www.pickle.com/help/start/what-is-pickle) | 18세 이상, 기본 아침 브리핑 설명 |
| [영어 플랜](https://www.pickle.com/help/credits/plans) | 주간 사용량, 새 플랜 표와 Pickle Plus 판매 종료 설명 |
| [예약 작업](https://www.pickle.com/help/tasks/scheduled) | 아침 브리핑 기본 꺼짐 설명. 영어 소개와 문구가 다름 |

## 2026년 11월 19일 첫 작업 실습 장 확인

| 공식 자료 | 17장에서 사용한 내용 |
| --- | --- |
| [Give your Pickle a task](https://www.pickle.com/help/tasks/delegate) | Chat 요청, 조건 카드, 앱을 닫아도 계속되는 작업, 예약 확인 링크·화면, 실수 가능성 |
| [How does Pickle check before paying?](https://www.pickle.com/help/tasks/confirm-before-payment) | 사전 동의 범위, 금액·상품·시간 변경 시 확인, 결제 후 주문 내역 대조 |
| [Get to know the app layout](https://www.pickle.com/help/start/app-layout) | Chat·Explore 등 앱 진입 위치 |
| [View other chats](https://www.pickle.com/help/chat/other-chats) | 피클이 건 전화의 대화·연결 결과 확인 |
| [Save a site login](https://www.pickle.com/help/connect/save-login) | 로그인 값은 일반 채팅이 아닌 Vault 카드에 입력 |
| [View your access log](https://www.pickle.com/help/privacy/activity) | 자격 증명 사용 시도 기록과 외부 작업 성공의 차이 |
| [Terms of Service](https://www.pickle.com/terms-of-service) | 브라우저 인계와 이미 완료된 외부 단계의 중단 한계 |

17장의 식당 사례와 새 SVG는 저자 구성 예시입니다. 카카오톡 링크는 사용자가 독자 안내용으로 제공했으며 Pickle의 공식 제품 자료가 아닙니다.

## 19장 에이전트 앱 비교 (2026-11-24 확인)

| 제품 | 공식 기능·권한 문서 | 앱 아이콘 출처 |
| --- | --- | --- |
| Pickle | [작업 위임](https://www.pickle.com/help/tasks/delegate), [결제 확인](https://www.pickle.com/help/tasks/confirm-before-payment), [예약 작업](https://www.pickle.com/help/tasks/scheduled) | [공식 프레스킷](https://www.pickle.com/press-kit), 공식 사이트 앱 아이콘 |
| ChatGPT Work | [Work와 Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex), [클라우드 브라우저](https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt) | [ChatGPT 공식 사이트](https://chatgpt.com/) 앱 아이콘 |
| Claude Cowork | [시작 안내](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork), [컴퓨터 사용](https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork) | [Claude 공식 사이트](https://claude.ai/) 앱 아이콘 |
| Manus | [Browser Operator](https://manus.im/en/blog/manus-browser-operator), [자동화](https://www.manus.im/features/automations) | [Manus 공식 사이트](https://manus.im/) 앱 아이콘 |
| Gemini Apps | [Tasks](https://support.google.com/gemini/answer/17094507), [행동 권한](https://support.google.com/gemini/answer/18766567) | [Gemini 공식 사이트](https://gemini.google.com/app) 앱 아이콘 |

아이콘은 공식 사이트 제공 파일을 원본 비율대로 48픽셀로 표시합니다. 비교 장은 직접 성능 시험이 아니라 공식 문서의 기능 범위와 사용자의 검증 방법을 구분한 원고입니다. 인쇄·광고·판촉용 재사용 조건은 별도 확인 대상입니다.

| 자료 | 매뉴얼에서 확인한 내용 |
| --- | --- |
| [What is Pickle?](https://www.pickle.com/help/start/what-is-pickle) | 대화, 통화, 작업 위임, 연결 계정, 기억 |
| [Give your Pickle a task](https://www.pickle.com/help/tasks/delegate) | 작업 카드, 웹 작업과 전화, 완료 결과 |
| [Call your Pickle](https://www.pickle.com/help/chat/voice-call) | 음성 통화 진입·종료와 대화 연결 |
| [Manage scheduled tasks](https://www.pickle.com/help/tasks/scheduled) | 일회성·반복 작업, 일시중지·수정·삭제 |
| [Save a site login](https://www.pickle.com/help/connect/save-login) | 로그인 정보의 Vault 저장과 관리 |
| [Privacy](https://www.pickle.com/privacy) | 비밀정보 분리, 정보 이용과 접근 기록에 관한 회사 설명 |
| [한국어 서비스 약관](https://www.pickle.com/ko/terms-of-service) | 2026-11-02 당시 확인한 페이지는 2026-10-24 시행으로 표시되었음. 같은 URL은 2026-11-24에 2026-12-08 시행 예정 문서로 바뀌어 있으므로 과거 문구의 고정 링크로 취급하지 않음 |
| [요금제 확인하기](https://www.pickle.com/help/credits/plans) | 11월 2일 한국어 자료의 무료·일일 한도와 11월 17일 영어 자료의 유료·주간 크레딧이 다름 |
| [사용량 한도는 어떻게 되나요?](https://www.pickle.com/help/credits/usage-credits) | 한도 초기화·브리핑 소모 등 시점·언어별 차이 |
| [앱과 서비스 연결하기](https://www.pickle.com/help/connect/add-connection) | 연결 경로, 권한 요청, 연결 후 폭넓은 읽기 |
| [연결을 끊으면 어떻게 되나요?](https://www.pickle.com/help/connect/disconnect) | 연결 해제 후 지워지는 것과 남는 것 |
| [화면 구성 알아보기](https://www.pickle.com/help/start/app-layout) | 피클 프로필의 한 일·예약한 작업·함께한 추억 |
| [내 정보는 누가 볼 수 있나요?](https://www.pickle.com/help/privacy/who-can-see) | AI·제공사·운영 인력·다른 사람의 정보 범위 |
| [정보 공개 범위 설정하기](https://www.pickle.com/help/privacy/sharing-settings) | 친구·앱별·사람별 공개 설정과 제외 항목 |
| [진행 중인 일 확인하고 취소하기](https://www.pickle.com/help/tasks/check-and-cancel) | 작업 상태·조건 변경·취소 경로 |
| [피클 대신 화면을 직접 조작하기](https://www.pickle.com/help/tasks/take-over-browser) | 사용자에게 브라우저를 넘기는 경우와 복귀 절차 |
| [둘러보기의 제안 카드 쓰기](https://www.pickle.com/help/tasks/explore-suggestions) | 제안 카드를 기본 채팅으로 보내는 흐름 |

## 본문 이미지

아래 이미지는 Pickle 공식 도움말의 예시 화면을 **원본 URL로 표시**합니다. 이 저장소에 이미지 파일을 복제해 배포하지 않습니다. 실제 앱 화면은 바뀔 수 있습니다.

기술 심화 장의 시스템·Vault·로그 SVG 3개는 공개 자료를 바탕으로 이 저장소에서 직접 작성한 설명 도식입니다. 실제 Pickle 내부 설계도를 복제한 것이 아닙니다.

8장의 재시도 판단 SVG는 이 저장소에서 직접 작성했습니다. 공식 작업·결제 도움말을 바탕으로 한 독자용 판단 도식이며 앱 화면이 아닙니다.

17장의 첫 작업 단계 SVG도 이 저장소에서 작성한 설명 도식입니다. 해당 장의 작업 상태 화면은 Pickle 공식 도움말 URL로 표시하고 원문을 이미지 아래에 붙였습니다.

| 이미지 | 원문 출처 | 사용 장 |
| --- | --- | --- |
| [기본 채팅 화면](https://www.pickle.com/help-center/screens/chat-basic.webp) | [화면 구성 알아보기](https://www.pickle.com/help/start/app-layout) | 01 |
| [음성 통화 화면](https://www.pickle.com/help-center/screens/chat-voice-call.webp) | [피클과 통화하기](https://www.pickle.com/help/chat/voice-call) | 02 |
| [접근 기록 화면](https://www.pickle.com/help-center/screens/privacy-access-log.webp) | [접근 기록 보기](https://www.pickle.com/help/privacy/activity) | 05 |
| [앱 연결 목록](https://www.pickle.com/help-center/screens/connect-add-connection.webp) | [앱과 서비스 연결하기](https://www.pickle.com/help/connect/add-connection) | 05 |
| [피클 프로필의 한 일 화면](https://www.pickle.com/help-center/screens/tasks-check-and-cancel.webp) | [진행 중인 일 확인하고 취소하기](https://www.pickle.com/help/tasks/check-and-cancel) | 06, 08 |
| [정보 공개 범위 화면](https://www.pickle.com/help-center/screens/privacy-sharing-settings.webp) | [정보 공개 범위 설정하기](https://www.pickle.com/help/privacy/sharing-settings) | 07 |
| [브라우저 열기 카드](https://www.pickle.com/help-center/screens/tasks-take-over-browser.webp) | [피클 대신 화면을 직접 조작하기](https://www.pickle.com/help/tasks/take-over-browser) | 08 |
| [둘러보기 제안 카드](https://www.pickle.com/help-center/screens/tasks-explore-suggestions.webp) | [둘러보기의 제안 카드 쓰기](https://www.pickle.com/help/tasks/explore-suggestions) | 09 |
| [이전 사용량 화면](https://www.pickle.com/help-center/screens/credits-plans.webp) | [요금제 확인하기](https://www.pickle.com/help/credits/plans); 실제 플랜 화면은 바뀔 수 있음 | 10 |
| [작업 상태 화면](https://www.pickle.com/help-center/screens/tasks-check-and-cancel.webp) | [진행 중인 일 확인하고 취소하기](https://www.pickle.com/help/tasks/check-and-cancel) | 17 |

## 주의할 점

- 회사 문서 사이에도 시점에 따라 표현이 달라질 수 있습니다. 예를 들어 기능의 기본 켜짐 여부는 앱 화면을 우선합니다.
- 보안·개인정보 설명은 회사의 공개 주장입니다. 이 매뉴얼이 이를 독립 검증하지 않았습니다.
- 이용 조건과 사용량 한도는 변경될 수 있습니다. 앱 화면과 현재 적용되는 지역 약관을 확인하세요.
- 실제 예약·주문·통화의 결과는 외부 서비스 상태로 확인해야 합니다.
