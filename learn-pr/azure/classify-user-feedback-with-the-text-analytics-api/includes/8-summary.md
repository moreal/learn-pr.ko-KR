Azure Cognitive Services는 앱을 보강하는 데 사용할 수 있는 지능형 서비스 제품군입니다. 텍스트 분석 API에는 텍스트를 의미 있는 인사이트로 전환하는 몇 가지 작업이 있습니다. 서비스를 사용하여 고객의 텍스트 피드백에서 감정을 발견했습니다. Azure Functions에 호스트되고 이러한 텍스트 메시지를 여러 버킷 또는 큐로 분류하여 추가 처리하는 솔루션을 만들었습니다.

REST API 호출 방법을 알면 이러한 지능형 서비스를 솔루션에 쉽게 통합할 수 있습니다. 모든 솔루션은 다음과 같은 비슷한 패턴을 따릅니다.

- 액세스 키를 등록합니다.
- API 테스트 콘솔에서 탐색합니다.
- 액세스 키 및 올바른 지역을 사용하여 요청을 작성합니다.
- 솔루션의 요청을 게시하고 응답을 구문 분석하여 인사이트를 얻습니다.

Azure Functions에서 만든 서버리스 논리에 이 인텔리전스를 추가했습니다. 다른 유형의 앱에서 이러한 서비스를 간편하게 호출할 수 있습니다. 시작을 도와주는 여러 클라이언트 라이브러리, 자습서 및 빠른 시작이 제공됩니다.

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>솔루션의 추가 향상을 위한 제안

솔루션을 더욱 개선하기 위해 고려해 볼 수 있는 몇 가지 아이디어가 있습니다.

- 추가 텍스트 샘플로 솔루션을 테스트합니다. 감정 점수를 긍정적, 중립, 부정적으로 분류하도록 설정한 임계값이 적절한지 확인합니다.
- [!INCLUDE [negative-q](./q-name-negative.md)] 큐의 메시지를 읽고 텍스트 분석 API를 호출하여 텍스트의 핵심 문구를 찾는 또 다른 함수를 함수 앱에 추가하는 방안을 생각해 봅니다.
- 입력 큐에는 원시 텍스트 피드백이 포함되어 있습니다. 실제로는 피드백을 메일 주소, 거래처 번호 같은 형태의 사용자 ID와 연결하게 됩니다. ID 필드 및 텍스트를 포함하는 JSON 문서가 되도록 입력 큐 항목을 개선해야 합니다. 그 후 텍스트 메시지를 작업할 때 해당 ID를 사용합니다.
- 현재 우리 솔루션은 영어로 “하드 코드”됩니다. 텍스트 분석 API에서 지원되는 모든 언어로 텍스트를 처리할 수 있게 하려면 어떻게 변경해야 하는지 고민해 보세요.
- Logic Apps에 익숙한 경우 추가 참고 자료 섹션에서 텍스트 분석을 위한 기본 제공 커넥터의 링크를 참조하세요.

Cognitive Services API 중 하나를 호출하는 방법을 배웠으니, 몇 가지 다른 서비스를 살펴보고 솔루션에 사용하는 방법을 생각해 봅시다.

## <a name="further-reading"></a>추가 참고 자료

- [텍스트 분석 개요](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [텍스트 분석 데모](https://azure.microsoft.com/services/cognitive-services/text-analytics/)
- [텍스트 분석에서 감정을 감지하는 방법](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [Cognitive Services 설명서](https://docs.microsoft.com/azure/cognitive-services/)

- [Text Analytics Logic Apps 커넥터](https://docs.microsoft.com/connectors/cognitiveservicestextanalytics/)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
