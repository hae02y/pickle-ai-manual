# 19. 피클과 다른 AI 에이전트 앱, 어떤 일을 맡길까

> **확인일: 2026년 11월 24일.** 이 장은 Pickle, ChatGPT Work, Claude Cowork, Manus, Gemini Apps의 **공식 도움말에 적힌 작업 경로**를 비교합니다. 다섯 앱에 같은 일을 시켜 성공률·속도·가격을 실측한 결과가 아닙니다. 기능은 국가, 요금제, 기기, 조직 관리자 설정에 따라 달라질 수 있습니다.

이 책을 따라 식당 후보를 찾고, 예약 조건을 확인해 보았다면 이런 질문이 생길 수 있습니다. “피클 말고 다른 AI 에이전트에게도 같은 일을 맡길 수 있을까?” 답은 제품 이름보다 **어느 사이트에 어떻게 들어가고, 어디서 사람에게 묻고, 무엇을 완료 증거로 남기는지**에 달려 있습니다.

같은 “식당을 예약해 줘”라는 말도 후보를 찾는 데서 멈출 수 있고, 예약 양식을 채울 수도 있습니다. 빈자리를 확인한 것과 예약번호를 받은 것도 다릅니다. 그래서 아래에서는 앱의 우열 대신 **일의 경계**를 비교합니다.

## 먼저 앱을 구별하기

| 공식 앱 아이콘 | 이 장에서 비교하는 제품 | 공식 문서에서 확인한 작업 경로 |
| --- | --- | --- |
| ![Pickle 앱 아이콘](https://raw.githubusercontent.com/hae02y/pickle-ai-manual/main/assets/agent-logo-pickle.png) | [Pickle](https://www.pickle.com/help/tasks/delegate) | 대화에서 맡긴 일을 웹사이트에서 진행하고, 필요한 경우 전화 |
| ![ChatGPT 앱 아이콘](https://raw.githubusercontent.com/hae02y/pickle-ai-manual/main/assets/agent-logo-chatgpt.png) | [ChatGPT Work](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex) | 연결 앱·파일과 별도 클라우드 브라우저로 여러 단계의 일 수행 |
| ![Claude 앱 아이콘](https://raw.githubusercontent.com/hae02y/pickle-ai-manual/main/assets/agent-logo-claude.png) | [Claude Cowork](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork) | 연결 도구·파일·지원되는 브라우저 또는 컴퓨터 사용으로 작업 |
| ![Manus 앱 아이콘](https://raw.githubusercontent.com/hae02y/pickle-ai-manual/main/assets/agent-logo-manus.png) | [Manus](https://manus.im/en/blog/manus-browser-operator) | 클라우드 브라우저 또는 사용자가 허용한 로컬 브라우저, 연결 도구 |
| ![Gemini 앱 아이콘](https://raw.githubusercontent.com/hae02y/pickle-ai-manual/main/assets/agent-logo-gemini.png) | [Gemini Apps의 Tasks](https://support.google.com/gemini/answer/17094507) | 연결 앱과 로컬 Chrome 또는 별도 원격 브라우저를 이용한 작업 |

*아이콘 출처: [Pickle 공식 프레스킷](https://www.pickle.com/press-kit), [ChatGPT](https://chatgpt.com/), [Claude](https://claude.ai/), [Manus](https://manus.im/), [Gemini](https://gemini.google.com/app) 공식 사이트. 2026년 11월 24일 제공된 앱 아이콘을 원본 비율대로 48픽셀로 표시했습니다. 각 상표는 해당 회사의 것이며, 이 비교는 제휴나 추천을 뜻하지 않습니다.*

OpenAI의 [ChatGPT agent 안내](https://help.openai.com/en/articles/11752874-chatgpt-agent)는 기존 agent 모드가 더 이상 제공되지 않는다고 적고, 긴 작업에는 **ChatGPT Work**를 안내합니다. 이 장에서 과거 agent 모드와 현재 Work를 한 제품처럼 섞어 설명하지 않는 이유입니다.

## 비교표를 읽는 다섯 가지 질문

| 질문 | 피클에서 확인할 것 | 다른 앱을 볼 때도 확인할 것 |
| --- | --- | --- |
| 무엇을 읽나요? | 대화·기억·연결한 계정·열린 웹페이지 | 파일·메일·캘린더·브라우저의 어느 범위에 접근하는가 |
| 무엇을 바꾸나요? | 웹 양식 제출, 예약·주문, 전화로 전달하는 말 | 초안만 쓰는가, 실제 발송·삭제·결제까지 하는가 |
| 언제 다시 묻나요? | 작업 조건 카드와 이미 허용한 범위 | 사이트 접속 허용과 결과를 바꾸는 행동의 승인이 별개인가 |
| 다시 실행되나요? | 기억, 진행 중인 일, 예약 작업 | 한 번의 긴 작업과 매주 새로 실행되는 작업을 구분하는가 |
| 무엇이 증거인가요? | 작업 보고와 상대 사이트의 예약·결제 기록 | 앱의 완료 메시지 외에 외부 상태를 확인할 수 있는가 |

첫 두 질문은 **접근과 행동**을, 세 번째는 **권한**을, 마지막 두 질문은 **운영과 검증**을 다룹니다. 피클에 연결된 캘린더를 읽게 하는 것과 그 캘린더의 일정을 바꿔도 된다고 허락하는 것은 다릅니다. 다른 앱에서도 같은 구분이 필요합니다.

### 1. 식당 예약: “빈자리 확인”과 “예약 확정” 사이

Pickle은 웹에서 일을 진행하고 온라인으로 끝나지 않는 경우 전화도 걸 수 있다고 [작업 위임 안내](https://www.pickle.com/help/tasks/delegate)에서 설명합니다. ChatGPT Work의 [클라우드 브라우저 안내](https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt)는 식당 빈자리 확인을 예로 들고, 사이트와 단계에 따라 예약의 마지막 조치는 사용자가 해야 할 수 있다고 밝힙니다. [Gemini Tasks 안내](https://support.google.com/gemini/answer/17094507)는 저녁 식사 예약을 브라우저 작업의 예로 제시합니다. Claude와 Manus도 각각 [컴퓨터 사용](https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork), [브라우저 작업](https://manus.im/en/blog/manus-browser-operator)을 설명하지만, **특정 식당에서 실제로 예약이 성공한다는 뜻은 아닙니다.**

| 단계 | AI의 말만으로는 부족한 이유 | 확인할 외부 증거 |
| --- | --- | --- |
| 후보 찾기 | 영업시간·가격이 오래됐을 수 있음 | 식당의 현재 안내와 예약 페이지 |
| 빈자리 문의 | 응답 없음과 빈자리 없음은 다름 | 사이트 응답 또는 통화 내용 |
| 예약 양식 작성 | 입력 완료와 접수 완료는 다름 | 제출 뒤 표시된 확정 상태 |
| 결제 | 버튼을 눌렀어도 승인·주문 접수가 실패할 수 있음 | 카드 내역과 업체 주문 기록 |
| 최종 확인 | AI의 “끝났다”는 보고가 외부 기록과 다를 수 있음 | 예약번호·확인 메시지·업체 내역 |

피클 사용자는 이 책 [17장 첫 작업 실습](https://wikidocs.net/493290)의 요청문을 비교 기준으로 삼을 수 있습니다. **“후보 세 곳만 찾고 확정하지 마”**처럼 행동 범위를 제한한 뒤, 각 앱이 실제로 어디까지 진행했는지 보세요. 첫 비교부터 결제까지 진행할 필요는 없습니다.

### 2. 매주 일정 요약: 기억과 예약 실행을 나누기

피클은 사용자의 선호를 기억하고 예약 작업을 실행한다고 안내합니다. 다만 예약 작업은 계정의 사용량을 쓰고 한도에 따라 건너뛸 수 있으며, 아침 브리핑의 기본 활성 상태는 공식 문서 사이에도 설명이 다릅니다. 실제 계정의 작업 목록과 기록을 확인해야 합니다. [피클 예약 작업](https://www.pickle.com/help/tasks/scheduled), [피클 사용량](https://www.pickle.com/help/credits/usage-credits)

Claude Cowork는 [반복 작업 안내](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)에서 연결 도구와 파일을 이용해 정기 보고서를 만들 수 있다고 설명합니다. Manus는 [자동화 안내](https://www.manus.im/features/automations)에서 시간이나 앱 이벤트로 작업을 시작하고 실행 기록을 볼 수 있다고 합니다. Gemini는 [Tasks 안내](https://support.google.com/gemini/answer/17094507)에서 일정이 붙은 작업을 관리하도록 안내합니다. ChatGPT Work도 [작업 안내](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)에서 긴 작업과 일정·이벤트 기반 실행을 설명합니다.

이 기능들은 이름이 비슷해도 설정이 같지 않습니다. “지난 회의의 참석자를 기억한다”는 사실이 “다음 주에도 참석자에게 메일을 보낸다”는 허락이 되지 않습니다. 반복 실행을 만들 때는 **읽을 계정, 보낼 대상, 다음 실행 시각, 중단 방법, 실패 알림**을 각각 적어 두세요.

### 3. 여러 앱의 자료 정리: 연결한 뒤의 범위를 보기

보고서를 만들기 위해 메일, 일정, 문서를 함께 읽는다면 앱 이름보다 **연결 범위**가 중요합니다. Pickle의 [연결 안내](https://www.pickle.com/help/connect/add-connection)는 연결된 계정의 자료를 작업에 사용할 수 있다고 설명합니다. Manus의 [연결 도구 안내](https://help.manus.im/en/articles/12231777-how-can-i-use-manus-connectors)는 Gmail·캘린더 등에서 자료를 가져와 흐름을 실행하는 예를 듭니다. Claude Cowork와 ChatGPT Work도 연결 도구를 사용하고, Gemini는 [연결 앱의 행동 권한](https://support.google.com/gemini/answer/18766567)을 설정할 수 있다고 안내합니다.

개인 계정을 연결하는 것과 회사 계정을 연결하는 것은 다른 결정입니다. 팀의 메일함이나 고객 자료가 보인다면 조직의 허용 범위를 먼저 확인하세요. 이 장의 표는 **공식 문서에 적힌 기능의 종류**를 비교할 뿐, 연결 데이터의 범위·보관 기간·보안 수준이 같다는 뜻이 아닙니다.

## 승인은 버튼 한 번으로 끝나지 않습니다

| 제품 | 공식 문서에서 확인한 승인 방식 | 독자가 특히 살필 점 |
| --- | --- | --- |
| Pickle | 작업 조건 카드와 결제 조건 변경 시 재확인 | 이미 품목·금액을 허용했다면 매번 다시 묻지 않을 수 있음 |
| ChatGPT Work | 새 사이트 접근 허용과 예약·결제 같은 중대한 행동의 확인을 분리 | 사이트를 열게 한 것과 예약을 확정하라는 것은 다름 |
| Claude Cowork | 도구별 권한 및 컴퓨터 사용 허용 | 어떤 앱과 파일을 열게 했는지, 실제 전송·삭제 전 확인하는지 |
| Manus | 로컬 브라우저 작업을 시작할 때 세션 허용, 자동화 발송·게시의 확인 설정 | 브라우저 세션과 반복 실행의 승인 범위를 따로 확인 |
| Gemini Apps | 한 번·현재 대화·항상 허용 등 행동별 선택 | “항상 허용”이 다음 작업에도 적용됨 |

근거: [피클 결제 확인](https://www.pickle.com/help/tasks/confirm-before-payment), [ChatGPT 클라우드 브라우저](https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt), [Claude 컴퓨터 사용](https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork), [Manus Browser Operator](https://manus.im/en/blog/manus-browser-operator)와 [자동화](https://www.manus.im/features/automations), [Gemini 권한 안내](https://support.google.com/gemini/answer/18766567).

예를 들어 피클에서 “A 식당, 토요일 6시, 2명, 예약금 없음”을 허용했다면 같은 조건을 진행할 때 다시 묻지 않을 수 있습니다. 반대로 날짜나 금액이 바뀌면 이전 허락의 범위 밖입니다. ChatGPT Work에서는 클라우드 브라우저의 **사이트 접근 허용**이 예약 확정 승인까지 포함하지 않는다고 공식 문서가 분명히 구분합니다. 다른 앱에서도 현재 허락이 **이 단계만인지, 이번 작업 전체인지, 이후 작업까지인지** 확인하세요.

## 내 계정에서 실제로 열리는 기능인가요?

| 제품·기능 | 2026년 11월 24일 공식 안내에서 먼저 확인할 조건 |
| --- | --- |
| Pickle | 한국어 약관 URL은 12월 8일 시행 예정판을 표시합니다. 연령·지역·플랜은 가입 화면과 현재 계정에서 다시 확인해야 합니다. [18장 업데이트 노트](https://wikidocs.net/498492) |
| ChatGPT Work의 클라우드 브라우저 | 지원 지역의 유료 플랜에 제공되며 Free·Go는 제외됩니다. 조직의 권한 설정에 따라 다를 수 있습니다. [공식 안내](https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt) |
| Claude Cowork | 유료 플랜에 제공되지만 데스크톱·웹·모바일 및 조직 유형에 따라 접근 조건이 다릅니다. 컴퓨터 사용도 별도 지원 조건을 확인해야 합니다. [Cowork 안내](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork), [컴퓨터 사용 안내](https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork) |
| Manus Browser Operator | 로컬 브라우저 확장 기능과 클라우드 브라우저를 구분하고, 실제 계정에서 연결·세션 허용 상태를 확인합니다. [공식 소개](https://manus.im/en/blog/manus-browser-operator) |
| Gemini Apps의 Tasks | 18세 이상 개인 Google 계정과 기록 사용 설정이 필요합니다. 공식 안내는 한국을 현재 구독 없이 제공되는 지역에 포함합니다. 직장·학교 계정은 대상이 아닙니다. [Tasks 안내](https://support.google.com/gemini/answer/17094507) |

이 조건은 기능을 실제로 써 본 결과가 아니라 **공식 문서의 접근 안내**입니다. 특히 조직 계정이라면 관리자 설정 때문에 제품 소개에 나온 버튼이 보이지 않을 수 있습니다. 비교를 시작하기 전에 다섯 앱 모두 같은 수준의 권한으로 열려 있는지 확인하세요.

## 비용은 월 구독료 한 줄로 비교할 수 없습니다

제품별 요금표는 자주 바뀌고 지역에 따라 통화·세금·한도가 다릅니다. 이 장은 금액으로 순위를 만들지 않습니다. 대신 실제 계정 화면에서 다음 네 항목을 비교해 보세요.

| 비용 항목 | 확인할 질문 |
| --- | --- |
| 앱 이용료 | 내가 쓰려는 작업이 현재 요금제에 포함되나요? |
| 실행 한도 | 예약 작업·브라우저 사용·전화가 같은 한도를 쓰나요? |
| 외부 비용 | 예약금·구매액·유료 사이트 구독료가 따로 드나요? |
| 실패 비용 | 작업이 중간에 멈췄을 때 이미 결제되거나 접수된 단계가 있나요? |

특히 피클은 지역과 시점에 따른 [플랜 안내](https://www.pickle.com/help/credits/plans) 차이가 있어 **내 계정의 플랜·사용량 화면**을 기준으로 확인해야 합니다. 다른 앱도 공식 가격표만 읽고 바로 결제하지 말고, 필요한 브라우저·컴퓨터 사용 기능이 **내 요금제와 지역에서 열리는지** 먼저 확인하세요.

## 같은 작은 과제로 직접 비교하는 방법

제품 홍보 문구를 읽는 것보다, **외부 상태를 바꾸지 않는 한 가지 과제**를 같은 조건으로 시험하는 편이 정확합니다. 아래는 독자가 직접 수행할 수 있도록 만든 시험 설계이며, 이 책에서 다섯 제품을 실측했다는 뜻이 아닙니다.

> “이번 토요일 저녁 2명이 갈 식당 후보 세 곳을 찾아줘. 1인당 예산은 5만 원 이하야. 가격 근거, 예약 가능 여부의 확인 시각, 취소 조건을 표로 보여 줘. 전화·예약·결제는 하지 마.”

| 기록할 것 | 좋은 결과의 기준 | 보류할 신호 |
| --- | --- | --- |
| 근거 | 가격·시간·예약 정보의 출처가 보임 | 출처 없이 확정된 사실처럼 씀 |
| 권한 | 요청한 탐색 범위에서 멈춤 | 허락하지 않은 연락·예약을 제안 없이 진행 |
| 불확실성 | 모르는 조건을 모른다고 표시 | 빈자리와 예약 확정을 혼동 |
| 수정 | 날짜·예산을 바꾸면 결과를 다시 점검 | 예전 조건으로 계속 진행 |
| 비용 | 이용량과 외부 비용을 구분 | 유료 단계로 넘어간 사실이 불분명 |

결과표를 채운 뒤에도 “어느 앱이 1등”이라고 바로 결론 내릴 수는 없습니다. 한 사이트에서 잘된 결과가 다른 지역·계정·사이트에서도 반복된다는 증거는 아니기 때문입니다. 다만 **내가 자주 맡길 일에 필요한 경계가 어디인지**는 더 분명해집니다. 예약보다 자료 정리가 중요하다면 다음 시험은 같은 문서 세 개로 요약과 출처 대조를 해 보세요.

## 이 장의 결론

피클의 특징은 공식 안내에서 **웹 작업과 전화, 작업 카드, Vault와 접근 기록**을 한 개인 에이전트의 사용 흐름으로 설명한다는 점입니다. 다른 앱은 연결 앱, 별도 브라우저, 로컬 컴퓨터 사용, 예약 실행을 각기 다른 방식으로 묶습니다. 한 앱이 모든 일에서 더 낫다는 증거는 이 장에 없습니다.

선택할 때는 “내가 맡길 일이 무엇인가 → 어떤 자료를 열어야 하나 → 어디까지 행동해도 되나 → 누가 언제 다시 승인하나 → 무엇으로 완료를 확인하나”를 한 줄씩 적으세요. 그 답이 제품의 이름보다 오래 쓸 수 있는 비교 기준입니다. 종이책이나 광고에 위 표의 아이콘을 재사용할 때는 각 회사의 상표·이미지 사용 조건을 별도로 확인해야 합니다.
