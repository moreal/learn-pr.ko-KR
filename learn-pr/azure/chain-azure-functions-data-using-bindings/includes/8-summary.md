이 모듈은 모두 데이터와 서비스를 함수에 통합하는 것에 관한 것이었습니다. 함수에 추가할 때 표시되는 바인딩 형식에 대해 빠르게 둘러보았습니다. 그런 다음, 입력 바인딩을 사용하여 Azure Cosmos DB에서 데이터를 읽는 방법을 살펴보았습니다. 플랫폼은 연결 문자열 관리를 담당하며, 여기서는 바인딩을 사용하여 코드에서 데이터를 읽는 것이 얼마나 쉬운지를 확인했습니다. 마지막으로, 출력 바인딩을 사용하여 다른 원본을 작성하는 데 집중했습니다. 이 과정은 다음 표에 요약되어 있습니다.

[!INCLUDE [summary table](./summary-table.md)]

여기서 습득한 방법을 적용하여 함수에서 바인딩을 추가하고 테스트할 수 있습니다. 바인딩을 사용하여 더 많이 연습하고 여기서 습득한 내용을 토대로 하는 몇 가지 흥미로운 아이디어는 다음과 같습니다.

* Blob Storage 및 이 모듈에서 사용하지 않은 다른 입력 바인딩에서 읽는 다른 함수를 만듭니다.

* 지원되는 다른 출력 바인딩 형식을 사용하여 더 많은 대상에 쓰는 다른 함수를 만듭니다.

* 마지막 단원에서 큐를 도입하고, 출력 바인딩을 사용하여 메시지를 큐에 게시했습니다. 다음 단계로, 큐에 있는 메시지를 읽고 `Console.Log()`를 사용하여 **메시지 텍스트**를 콘솔에 출력하는 다른 함수를 추가하는 것을 고려합니다.

이 모듈에서 보았듯이, Azure Portal에서는 함수를 작성하고 데이터와 다른 서비스에 연결하는 데 사용하기 쉬운 기능을 제공합니다.

## <a name="clean-up-resources"></a>리소스 정리

Azure에서 *리소스*는 함수 앱, 함수, 저장소 계정 등을 의미합니다. 리소스는 *리소스 그룹*으로 그룹화되며, 그룹을 삭제하여 그룹의 모든 항목을 삭제할 수 있습니다.

이 모듈을 완료하는 리소스를 만들었습니다. [계정 상태](https://azure.microsoft.com/account/) 및 [서비스 가격 책정](https://azure.microsoft.com/pricing/)에 따라 이러한 리소스에 대한 요금이 청구될 수 있습니다. 리소스가 더 이상 필요하지 않게 되면 다음과 같이 삭제합니다.

1. Azure Portal에서 **리소스 그룹** 페이지로 이동합니다.

   함수 앱 페이지에서 해당 페이지로 이동하려면 **개요** 탭을 선택한 다음, **리소스 그룹** 아래의 링크를 선택합니다.

   대시보드에서 해당 페이지로 이동하려면 **리소스 그룹**을 선택한 다음, 이 모듈에 사용한 리소스 그룹을 선택합니다. 

> [!NOTE]
> 이 모듈에 대해 제안한 리소스 그룹의 기본 이름은 [!INCLUDE [resource-group-name](./rg-name.md)]이지만, 다른 이름을 사용할 수도 있습니다.

2. **리소스 그룹** 페이지에서 포함된 리소스 목록을 검토하고 삭제하려는 리소스인지 확인합니다.

3. **리소스 그룹 삭제**를 선택하고 지시를 따릅니다.

   삭제는 몇 분 정도 소요됩니다. 완료되면 알림이 잠시 표시됩니다. 또한 페이지 위쪽의 종 모양 아이콘을 선택하여 알림을 확인할 수도 있습니다.

## <a name="further-reading"></a>추가 참고 자료

이 목록은 완전한 목록이 아니지만, 이 모듈에서 다루는 흥미로운 주제와 관련된 몇 가지 리소스는 다음과 같습니다.

 * [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions/)

* [Azure Functions 과제](https://aka.ms/afc)

* [Azure 서버리스 컴퓨팅 쿡북](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [Node.js에서 큐 저장소를 사용하는 방법](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [Azure Cosmos DB 소개: SQL API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [Azure Cosmos DB의 기술적 개요](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [Azure Cosmos DB 설명서](https://docs.microsoft.com/azure/cosmos-db/)
