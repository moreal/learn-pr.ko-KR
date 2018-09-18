Microsoft Cognitive Services는 앱을 보강하는 데 사용할 수 있는 지능형 서비스 제품군입니다. 앞에서 텍스트 분석 API 서비스의 일부분을 살펴보면서 텍스트에 대한 대략적인 정보를 찾아보았습니다. 서비스를 사용하여 고객의 텍스트 피드백에서 감정을 분석했습니다. Azure Functions에 호스트되고 이러한 텍스트 메시지를 여러 버킷 또는 큐로 분류하여 추가 처리하는 솔루션을 만들었습니다.

REST API 호출 방법을 알면 이러한 지능형 서비스를 솔루션에 쉽게 통합할 수 있습니다. 모든 솔루션은 다음과 같은 비슷한 패턴을 따릅니다.

- 액세스 키를 등록합니다.
- API 테스트 콘솔에서 탐색합니다.
- 액세스 키 및 올바른 지역을 사용하여 요청을 작성합니다.
- 솔루션의 요청을 게시하고 응답을 구문 분석하여 인사이트를 얻습니다.

Azure Functions에서 만든 서버리스 논리에 이 인텔리전스를 추가했습니다. 다른 유형의 앱에서 이러한 서비스를 간편하게 호출할 수 있습니다. 시작을 도와주는 여러 클라이언트 라이브러리, 자습서 및 빠른 시작이 제공됩니다.

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>솔루션의 추가 향상을 위한 제안

솔루션을 더욱 개선하기 위해 고려해 볼 수 있는 몇 가지 아이디어가 있습니다. 

- 더 많은 텍스트 예제를 사용하여 솔루션을 테스트하고 감정 점수를 긍정적, 중립, 부정적으로 분류하도록 설정한 임계값이 적절한지 확인합니다. 
- [!INCLUDE [negative-q](./q-name-negative.md)] 큐의 메시지를 읽고 텍스트 분석 API를 호출하여 텍스트의 핵심 문구를 찾는 또 다른 함수를 함수 앱에 추가하는 방안을 생각해 봅니다.
- 입력 큐에는 원시 텍스트 피드백이 포함되어 있습니다. 실제 세계에서는 피드백을 이메일 주소, 거래처 번호 같은 형태의 사용자 ID와 연결하게 됩니다. 따라서 ID 필드 및 텍스트를 포함하는 JSON 문서가 되도록 입력 큐 항목을 개선해야 합니다. 그 후 텍스트 메시지를 작업할 때 해당 ID를 사용합니다.
 - 현재 우리 솔루션은 영어로 "하드 코딩"됩니다. 텍스트 분석 API에서 지원되는 모든 언어로 텍스트를 처리할 수 있게 하려면 어떻게 변경해야 하는지 고민해 보세요.  

Cognitive Services API 중 하나를 호출하는 방법을 배웠으니, 몇 가지 다른 서비스를 살펴보고 솔루션에 사용하는 방법을 생각해 봅시다. 

## <a name="further-reading"></a>추가 참고 자료

- [Text Analytics 개요](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [Text Analytics에서 감정을 감지하는 방법](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [Cognitive Services 설명서](https://docs.microsoft.com/azure/cognitive-services/)

## <a name="clean-up-resources"></a>리소스 정리

Azure에서 *리소스*란 앱, 함수, 저장소 계정 등을 의미합니다. 리소스는 *리소스 그룹*으로 그룹화되며 그룹을 삭제하면 그룹의 모든 항목을 삭제할 수 있습니다.

이 모듈을 완료하기 위해 리소스를 만들었습니다. [계정 상태](https://azure.microsoft.com/account/) 및 [서비스 가격 책정](https://azure.microsoft.com/pricing/)에 따라 리소스에 대해 요금이 청구될 수 있습니다. 리소스가 더 이상 필요하지 않게 되면 다음과 같이 삭제합니다.

1. Azure Portal에서 **리소스 그룹** 페이지로 이동합니다.

   함수 앱 페이지에서 해당 페이지로 이동하려면 **개요** 탭을 선택한 후 **리소스 그룹** 아래의 링크를 선택합니다.

   대시보드에서 해당 페이지로 이동하려면 **리소스 그룹**을 선택한 다음, 이 모듈에 사용한 리소스 그룹을 선택합니다. 

> [!NOTE]
> 이 모듈에서 제안한 리소스 그룹의 기본 이름은 [!INCLUDE [resource-group-name](./rg-name.md)]이지만, 다른 이름을 사용할 수도 있습니다.

2. **리소스 그룹** 페이지에서 포함된 리소스 목록을 검토하고 삭제하려는 항목인지 확인합니다.

3. **리소스 그룹 삭제**를 선택하고 지시를 따릅니다.

   삭제는 몇 분 정도 소요됩니다. 완료되면 알림이 잠시 표시됩니다. 페이지 위쪽의 종 모양 아이콘을 선택해도 알림을 확인할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

이 목록은 전체 목록이 아니며, 다음은 이 모듈에서 다루는 흥미로운 토픽과 관련된 리소스입니다.

 * [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions/)

* [Azure Functions 과제](https://aka.ms/afc)

* [Azure 서버리스 컴퓨팅 쿡북](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [Node.js에서 큐 저장소를 사용하는 방법](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [Azure Cosmos DB: SQL API 소개](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [Azure Cosmos DB의 기술 개요](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [Azure Cosmos DB 설명서](https://docs.microsoft.com/azure/cosmos-db/)
