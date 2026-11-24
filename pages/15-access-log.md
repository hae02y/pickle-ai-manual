# 15. 접근 로그: 사용 전 기록, 검증, 사각지대

> 분석 자료: [공식 접근 로그 안내](https://pickle.com/help/privacy/activity), [`credential-enclave` README](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md), [`protocol.md` 7장](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/protocol.md). **로그가 있다는 사실과 개별 작업의 성공은 동일하지 않다.**

## 기록의 인과 순서

[고정 커밋 README](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md)의 핵심 설계는 자격 증명을 사용하기 **전에** 로그 항목을 S3 Object Lock 저장소에 쓰는 것이다. 저장소가 성공 응답을 준 뒤에야 node가 해당 행위를 진행한다. node는 항목에 서명하고 이전 항목과 해시로 연결한다. 기기 앱은 계정의 로그 복호화 키로 내용을 읽고 체인을 검증한다.

[AWS S3 Object Lock의 compliance mode](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html)는 지정된 보존 기간 동안 객체 버전을 덮어쓰거나 삭제하지 못하게 한다. 이 공개 소스가 각 항목에 설정하는 기간은 **365일**이다. 이는 회사가 모든 계정의 로그를 영구 보관한다는 뜻이 아니다.

![자격 증명 사용 전 로그 기록과 기기 검증 흐름](https://raw.githubusercontent.com/hae02y/pickle-ai-manual/main/assets/pickle-log-sequence.svg)

*그림: 공개 [`README`](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md)와 [접근 로그 안내](https://pickle.com/help/privacy/activity)를 바탕으로 이 책에서 작성.*

이를 간단히 쓰면 다음과 같다.

`비밀 사용의 선행 조건 = 유효한 위임 ∧ 해당 호출의 조건 충족 ∧ 로그 저장 성공`

이 식은 공개 소스의 호출·기록 순서를 설명하기 위한 축약이다. 식의 “조건”에는 해당 API가 검사하는 범위만 들어간다. [`protocol.md`의 `policy` 필드](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/protocol.md)는 현재 단계에서 빈 객체로 취급된다. 따라서 **앱의 결제 승인 UI가 금액·상점 조건까지 enclave 안에서 강제한다고 읽으면 안 된다.**

## 로그에서 증명할 수 있는 것

| 관찰 | 가능한 결론 | 불가능한 결론 |
| --- | --- | --- |
| 서명·체인이 유효한 `release` 기록 | 해당 node가 비밀 값을 내보내려는 행위를 기록했다 | 사이트 로그인이나 결제가 성공했다 |
| `forward` 기록 | 특정 provider 요청을 시작하려 했다 | provider가 요청을 받아 처리했다 |
| 기록이 보이지 않음 | 현재 앱 조회 범위에 해당 항목이 없다 | 모든 node에서 절대 사용이 없었다 |
| S3 저장 실패 | 소스 설계상 해당 node가 비밀 사용을 중단해야 한다 | 서비스 전체가 정상 동작했다 |

로그는 **행동의 의도와 시도**에 대한 증거다. 예약 확정번호, 카드 승인 내역, provider의 감사 로그 같은 외부 증거와 결합해야 실제 결과를 알 수 있다. 또한 작업이 실패하거나 시작되지 않아도 선행 기록은 남을 수 있다.

예를 들어 오후 7시에 카드 사용 기록이 보이고 피클이 주문을 완료했다고 보고했더라도, 카드사가 승인했는지와 업체가 주문을 접수했는지는 아직 별개다. 반대로 주문 내역이 있는데 접근 로그가 보이지 않는다면 로그의 조회 범위와 동기화 상태를 먼저 살펴야 한다. 한 자료의 빈칸을 근거로 다른 자료의 사건을 지우지 않는다.

## 검증의 한계

[공개 README의 제한 설명](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/README.md)은 로그의 경계를 밝힌다. node가 정상 종료하지 못해 최종 `head`를 남기지 않으면 **마지막으로 확인된 지점 이후 항목을 최종 서명 지점과 대조하지 못할 수 있다.** 기록 자체가 없어진다는 뜻과는 다르다. 철회 요청에서 운영자가 살아 있는 node를 누락하면 그 node의 위임도 만료 전까지 남을 수 있다.

저장소 보존과 가용성은 AWS 및 운영자 계정의 지속성에 의존한다. [고정 프로토콜](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/protocol.md)은 각 항목을 Object Lock으로 365일간 삭제하지 못하게 하고, 이후 삭제가 가능하며, 버킷 수명 규칙은 약 400일로 설명한다. 이 수치는 **400일간 앱 열람을 보장한다는 뜻이 아니다.**

새 release로 위임을 옮길 때 사용하는 Sigstore Rekor 검증도 범위를 나눠 읽어야 한다. [프로토콜](https://github.com/pickle-com/credential-enclave/blob/cff16a343bf5bb7953e5b65df6ab3600107e127d/docs/protocol.md)은 node가 signed entry timestamp를 확인하지만 inclusion proof와 checkpoint까지 확인하지 않는다고 밝힌다. 이는 로그에 항목이 있다는 주장에 대해 확인한 증거의 종류가 다르다는 뜻이다.

## 독자가 실제로 점검할 순서

1. 피클 앱의 [접근 로그](https://pickle.com/help/privacy/activity)에서 **어느 연결·어느 시각·어떤 행위**였는지 본다.
2. 승인 카드, 작업 요청, 접근 로그의 시각과 대상을 맞춰 본다.
3. 결제·예약·메일 전송은 해당 사이트의 내역으로 **결과를 별도 확인**한다.
4. 이상하면 피클 연결을 해제하고, provider 계정의 연결 앱 권한과 카드·비밀번호 상태를 직접 점검한다.
5. 접근 로그가 비어 있어도 앱 오류·동기화 지연·검증 불완전 표시를 확인한다.

이 순서는 포렌식 완결 절차가 아니라 일반 사용자의 검토 절차다. 전문 감사를 한다면 release 측정값, attestation, S3 객체, 앱의 검증 결과, 외부 provider 기록을 함께 확보해야 한다.

독자에게 필요한 결론은 단순하다. **접근 로그는 “무슨 비밀을 쓰려고 했는가”를 묻는 데 강하고, 외부 서비스 내역은 “무슨 일이 실제로 일어났는가”를 묻는 데 강하다.** 두 자료를 함께 봐야 작업을 설명할 수 있다.

