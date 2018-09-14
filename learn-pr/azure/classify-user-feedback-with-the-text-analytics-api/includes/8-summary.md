Microsoft Cognitive Services는 응용 프로그램을 보강을 사용할 수 있는 지능형 서비스의 다양 한 제품군입니다. Text Analytics API에 텍스트를 의미 있는 정보로 변환 하는 몇 가지 작업이 있습니다. 고객의 피드백을 텍스트에서 감정 검색 서비스를 사용 했습니다. 이러한 텍스트 메시지를 여러 버킷으로 분류 또는 추가 처리를 위해 큐를 정렬 하기 위해 Azure Functions에서 호스팅되는 솔루션을 만들었습니다.

REST API를 호출 하는 방법을 알면 다음 쉽게 통합할 수 있습니다 이러한 지능형 서비스를 솔루션에. 모두 비슷한 패턴을 따릅니다.

- 액세스 키에 대 한 등록
- API 테스트 콘솔에서 탐색
- 액세스 키 및 올바른 지역을 사용 하 여 요청을 작성 합니다.
- 솔루션에서 요청을 게시 하 고 정보에 대 한 응답을 구문 분석 합니다.

Azure Functions에서 생성 하는 서버 리스 논리로 이러한 인텔리전스를 추가 했습니다. 다른 유형의 앱에서 이러한 서비스를 쉽게 호출할 수 있습니다. 여러 클라이언트 라이브러리가 자습서 및 빠른 시작을 시작 합니다.

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>솔루션의 추가 기능에 대 한 제안

일부의 좋은 방법이 더 않았습니다에서는 수행 하려는 경우 고려해 야 합니다.

- 자세한 텍스트 예제를 사용 하 여 솔루션을 테스트 합니다. 양수, 음수이 고 중립으로 감정 점수를 분류를 설정 하는 임계값을 적절 한 되는지 여부를 결정 합니다.
- 메시지를 읽는 함수 앱에 다른 함수를 추가 하는 것이 좋습니다는 [!INCLUDE [negative-q](./q-name-negative.md)] 큐 및 텍스트에서 키 구 찾기 텍스트 분석 API를 호출 합니다.
- 입력된 큐에는 원시 텍스트 피드백 포함 되어 있습니다. 실제 환경에는 일종의 전자 메일 주소, 계좌 번호와 같은 사용자 ID 사용 하 여 피드백을 연결 하 고 등. 포함 된 JSON 문서를 ID 필드 및 텍스트 입력된 큐 항목을 향상 시킵니다. 다음 텍스트 메시지와 함께 작업 하는 경우 해당 ID를 사용 합니다.
- 현재 솔루션은 "하드 코딩" 영어입니다. Text Analytics API에서 지 원하는 모든 언어에서 텍스트를 처리할 수 있도록 구현 하는 변경 내용에 대 한 생각 합니다.
- Logic Apps에 익숙한 경우 기본 제공 커넥터 추가 정보 섹션에서 텍스트 분석에 대 한 링크를 방문 합니다.

이제 이러한 Cognitive Services Api 중 하나를 호출 하는 방법을 알았으므로 몇 가지 다른 서비스를 탐색 하 고 솔루션에서 이러한를 사용 하는 방법을 고려해 야.

## <a name="further-reading"></a>추가 참고 자료

- [Text Analytics 개요](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [텍스트 분석 감정 감지 하는 방법](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [Cognitive Services 설명서](https://docs.microsoft.com/azure/cognitive-services/)

- [텍스트 분석 Logic Apps 커넥터](https://docs.microsoft.com/connectors/cognitiveservicestextanalytics/)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
