이 모듈은 모두 데이터와 서비스를 함수에 통합하는 것에 관한 것이었습니다. 함수에 추가할 때 표시되는 바인딩 형식에 대해 빠르게 둘러보았습니다. 그런 다음, 입력 바인딩을 사용하여 Azure Cosmos DB에서 데이터를 읽는 방법을 살펴보았습니다. 플랫폼은 연결 문자열 관리를 담당하며, 여기서는 바인딩을 사용하여 코드에서 데이터를 읽는 것이 얼마나 쉬운지 확인했습니다. 마지막으로, 출력 바인딩을 사용하여 다른 원본을 작성하는 데 집중했습니다. 이 과정은 다음 표에 요약되어 있습니다.

[!INCLUDE [summary table](./summary-table.md)]

여기서 습득한 방법을 적용하여 함수에서 바인딩을 추가하고 테스트할 수 있습니다. 다음은 바인딩을 좀 더 연습하고 여기서 배운 내용을 더욱 발전시키는 몇 가지 흥미로운 아이디어입니다.

* Blob 저장소 및 이 모듈에서 사용하지 않은 다른 입력 바인딩에서 데이터를 읽는 다른 함수를 만듭니다.

* 지원되는 다른 출력 바인딩 형식을 사용하여 더 많은 대상에 쓰는 다른 함수를 만듭니다.

* 이전 섹션에서는 큐를 소개하고, 출력 바인딩을 사용하여 메시지를 큐에 게시했습니다. 다음 단계로, 큐에 있는 메시지를 읽고 `Console.Log()`를 사용하여 **메시지 텍스트**를 콘솔에 출력하는 다른 함수를 추가하는 것을 고려합니다.

이 모듈에서 보았듯이, Azure Portal에서는 함수를 작성하고 데이터와 다른 서비스에 연결하는 데 사용하기 쉬운 기능을 제공합니다.

이처럼 시각적 워크플로를 사용하고 사용자 지정 코드를 거의 또는 전혀 작성하지 않고 서버리스 통합을 수행하는 데 관심이 있는 분들은 Azure Logic Apps도 살펴보시기 바랍니다.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>추가 리소스

이 목록은 전체 목록은 아니지만, 이 모듈에서 다루는 흥미로운 주제와 관련된 몇 가지 리소스는 다음과 같습니다.

* [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions/)
* [Azure Functions 과제](https://aka.ms/afc)
* [Azure 서버리스 컴퓨팅 쿡북](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)
* [Node.js에서 큐 저장소를 사용하는 방법](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)
* [Azure Cosmos DB 소개: SQL API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)
* [Azure Cosmos DB의 기술적 개요](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)
* [Azure Cosmos DB 설명서](https://docs.microsoft.com/azure/cosmos-db/)
