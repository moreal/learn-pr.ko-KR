회사에서 성장하는 고객 및 제품 기반의 수요를 충족하기 위해 Azure Cosmos DB를 선택했습니다. 데이터베이스를 만드는 작업을 진행하고 있습니다.

첫 번째 단계는 Azure Cosmos DB 계정을 만드는 것입니다.

## <a name="what-is-an-azure-cosmos-db-account"></a>Azure Cosmos DB 계정이란?

Azure Cosmos DB 계정은 데이터베이스의 조직 엔터티 역할을 하는 Azure 리소스입니다. 청구를 위해 사용 현황을 Azure 구독에 연결합니다.

각 Azure Cosmos DB 계정은 Azure Cosmos DB가 지원하는 여러 데이터 모델 중 하나와 연결되며 필요한 만큼 많은 계정을 만들 수 있습니다. 

새 응용 프로그램을 만드는 경우 SQL API는 선호되는 데이터 모델입니다. 그래프나 표를 사용하거나 MongoDB 또는 Cassandra 데이터를 Azure로 마이그레이션하는 경우 추가 계정을 만들고 관련 데이터 모델을 선택합니다.

계정을 만들 때 의미 있는 ID를 선택합니다. 이 방법으로 계정을 식별합니다. 또한 데이터 센터와 사용자 간의 대기 시간을 최소화하기 위해 사용자와 가장 가까운 Azure 지역에서 계정을 만듭니다.

필요한 경우 계정을 만드는 동안 가상 네트워크 및 지리적 중복을 설정할 수 있지만, 나중에 설정할 수도 있습니다. 이 모듈에서는 이러한 설정을 사용하지 않습니다.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>포털에서 Azure Cosmos DB 계정 만들기

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

1. **리소스 만들기** > **데이터베이스** > **Azure Cosmos DB**를 클릭합니다.
   
   ![Azure Portal 데이터베이스 창](../media-draft/2-create-nosql-db-databases-json-tutorial.png)

1. **새 계정** 페이지에서 새 Azure Cosmos DB 계정에 대한 설정을 입력합니다.
 
    설정|값|설명
    ---|---|---
    ID|*고유한 이름 입력*|이 Azure Cosmos DB 계정을 식별하는 고유한 이름을 입력합니다. URI를 만들기 위해 제공하는 ID에 *documents.azure.com*이 추가되므로 식별할 수 있는 고유한 ID를 사용합니다.<br><br>ID는 소문자, 숫자 및 하이픈(-) 문자만 포함할 수 있으며, 3-50자를 포함해야 합니다.
    API|SQL|API는 만들 계정의 형식을 결정합니다. Azure Cosmos DB는 응용 프로그램의 요구 사항을 충족하기 위해 SQL(문서 데이터베이스), Gremlin(그래프 데이터베이스), MongoDB(문서 데이터베이스), Azure Table 및 Cassandra라는 다섯 가지 API를 제공합니다. 현재 각 API에는 별도의 계정이 필요합니다. <br><br>이 모듈에서는 SQL 구문을 사용하여 쿼리할 수 있고 SQL API를 통해 액세스할 수 있는 문서 데이터베이스를 만들므로 **SQL**을 선택합니다.|
    구독|*사용자의 구독*|이 Azure Cosmos DB 계정에 사용할 Azure 구독을 선택합니다.
    리소스 그룹|새로 만들기<br><br>*그런 후 ID에서 위에 제공된 동일한 고유한 이름을 입력합니다*.|**새로 만들기**를 선택하고 사용자 계정에 대한 새 리소스 그룹 이름을 입력합니다. 간단히 하기 위해 ID와 동일한 이름을 사용할 수 있습니다. 
    위치|*사용자와 가장 가까운 지역 선택*|Azure Cosmos DB 계정을 호스트할 지리적 위치를 선택합니다. 데이터에 가장 빨리 액세스할 수 있도록 사용자와 가장 가까운 위치를 사용합니다.
    지리적 중복 사용| 비워 둠 | 이 설정은 두 번째(쌍을 이루는) 지역에서 복제된 버전의 데이터베이스를 만듭니다. 나중에 데이터베이스를 복제할 수 있으므로 지금은 이 설정을 비워 둡니다.
    가상 네트워크|사용 안 함|지금은 가상 네트워크를 사용하지 않도록 설정해 둡니다. 나중에 사용하도록 설정할 수 있습니다.

1. **만들기**를 클릭합니다.

    ![Azure Cosmos DB에 대한 새 계정 페이지](../media-draft/2-azure-cosmos-db-create-new-account.png)

1. 계정 생성에는 몇 분 정도가 소요됩니다. 포털이 배포에 성공했다는 알림을 표시할 때까지 기다린 후 알림을 클릭합니다. 

    ![알림 경고](../media-draft/2-azure-cosmos-db-notification.png)

1. [알림] 창에서 **리소스로 이동**을 클릭합니다.

    ![리소스로 이동](../media-draft/2-azure-cosmos-db-go-to-resource.png)

    포털에서 **축하합니다! Azure Cosmos DB 계정이 만들어졌습니다.** 페이지가 표시됩니다.

    ![Azure Portal 알림 창](../media-draft/2-azure-cosmos-db-account-created.png)

## <a name="summary"></a>요약

Azure Cosmos DB 데이터베이스를 만드는 첫 번째 단계인 Azure Cosmos DB 계정을 만들었습니다. 데이터 형식에 적합한 설정을 선택하고 사용자의 대기 시간을 최소화하도록 계정 위치를 설정했습니다.
