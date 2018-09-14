이 모듈을 함수에 데이터 및 서비스 통합이 전부 였습니다. 함수에 추가 하면 표시 되는 바인딩 형식 둘러보기로 시작 했습니다. 그런 다음 입력된 바인딩을 사용 하 여 Azure Cosmos DB에서 데이터를 읽는 살펴보았습니다. 연결 문자열을 관리 하는 플랫폼을 담당 하 고 바인딩을 사용 하 여 코드의 데이터를 읽을 얼마나 쉬운지 살펴보았습니다. 마지막 주의 데이터 출력 바인딩 사용 하 여 다양 한 원본 작성에 집중 했습니다. 이 과정은 다음 표에 요약 되어 있습니다.

[!INCLUDE [summary table](./summary-table.md)]

추가 및 함수에 바인딩을 테스트할 여기 배웠습니다 접근 방식을 적용할 수 있습니다. 다음은 몇 흥미로운 아이디어 바인딩을 사용 하 여 자세한 연습을 얻으려면 하 고 여기서 학습 한 내용에서 빌드할 수 있습니다.

* 이 모듈에서 사용 하지 않은 하는 다른 입력된 바인딩은 Blob Storage에서 읽기를 다른 함수를 만듭니다.

* 다른 지원 되는 출력 바인딩 유형을 사용 하 여 더 많은 대상에 쓸 다른 함수를 만듭니다.

* 마지막 단위에 있는 큐를 도입 하 고 출력 바인딩 사용 하 여 메시지를 게시 합니다. 다음 단계에서는 큐의 메시지를 읽고 인쇄 하는 다른 함수를 추가 고려 합니다 **메시지 텍스트** 콘솔에 `Console.Log()`입니다.

이 모듈에서 살펴본 것 처럼 Azure portal 함수를 작성 하 고 데이터 및 기타 서비스에 연결 하려면 사용 하기 쉬운 기능을 제공 합니다.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="further-reading"></a>추가 참고 자료

이 목록은 되도록 아니며 하는 동안 발생할 수 있는 흥미로운이 모듈에서 다루는 항목에 관련 된 일부 리소스는 다음과 같습니다.

 * [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions/)

* [Azure Functions 과제](https://aka.ms/afc)

* [Azure 서버 리스 컴퓨팅 쿡 북](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [Node.js에서 큐 저장소를 사용하는 방법](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [Azure Cosmos DB 소개: SQL API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [Azure Cosmos DB의 기술 개요](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [Azure Cosmos DB 설명서](https://docs.microsoft.com/azure/cosmos-db/)
