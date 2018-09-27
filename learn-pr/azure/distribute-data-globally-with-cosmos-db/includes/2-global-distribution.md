고객에게 온라인 의류 사이트의 제품에 가장 빠르게 액세스할 수 있는 방법을 제공하는 것은 고객에게는 물론 비즈니스 성공에도 매우 중요합니다. 데이터가 사용자에게 도달하기 위해 이동해야 하는 거리를 좁히면 더 많은 콘텐츠를 더 빠르게 제공할 수 있습니다. 데이터가 Azure Cosmos DB에 저장된 경우 마우스로 한 번 가리키고 클릭하기만 하면 사이트의 데이터가 전 세계 여러 지역으로 복제됩니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

이 단원에서는 글로벌 배포와 기본 다중 마스터 데이터베이스 서비스의 이점을 살펴본 후 계정을 3개의 추가 지역으로 복제합니다.

## <a name="global-distribution-basics"></a>글로벌 배포 기본 사항

글로벌 배포를 사용하면 한 지역의 데이터를 여러 Azure 지역에 복제할 수 있습니다. 데이터베이스를 복제할 지역을 언제든지 추가하거나 제거할 수 있으며, Azure Cosmos DB는 사용자가 지역을 추가한 후 데이터가 30분 이내에 작동하도록 보장합니다(데이터가 100TB 미만인 경우).

둘 이상의 지역에 데이터를 복제하기 위한 두 가지 일반적인 시나리오는 다음과 같습니다.

1. 전세계 어느 위치에 있든 관계 없이 최종 사용자에게 대기 시간이 짧은 데이터 액세스 제공
2. BCDR(무중단 업무 방식 및 재해 복구)를 위한 지역 복원 기능 추가

고객에게 대기 시간이 짧은 액세스를 제공하려면 사용자의 위치와 가장 가까운 지역에 데이터를 복제하는 것이 좋습니다. 온라인 의류 회사의 경우에는 로스앤젤레스, 뉴욕, 도쿄에 고객을 보유하고 있습니다. [Azure 지역](https://azure.microsoft.com/global-infrastructure/regions/) 페이지를 살펴보고 이러한 고객 집합과 가장 가까운 지역을 확인하세요. 이러한 위치에 사용자를 복제할 것입니다.

BCDR 솔루션을 제공하려면 [비즈니스 연속성 및 재해 복구(BCDR): Azure 쌍을 이루는 지역](https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/) 문서에서 설명된 하위 지역 쌍에 기초하여 지역을 추가하는 것이 좋습니다.

데이터베이스가 복제되면 처리량 및 저장소도 동일하게 복제됩니다. 따라서 원본 데이터베이스의 저장소가 10GB이고 처리량이 1,000RU/s이며, 이를 3개 지역에 추가로 복제했다면 각 지역의 데이터는 10GB이고, 처리량은 1,000RU/s가 됩니다. 저장소와 처리량이 각 지역에 복제되기 때문에 지역에 복제하는 비용이 원래 지역과 동일하므로 3개 지역에 추가로 복제할 경우 복제되지 않은 원래 데이터베이스보다 약 4배의 비용이 듭니다.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>포털에서 Azure Cosmos DB 계정 만들기

1. 샌드박스를 활성화하는 데 사용한 것과 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

    > [!IMPORTANT]
    > Azure Portal과 샌드박스에 동일한 계정으로 로그인합니다.
    >
    > 위의 링크로 Azure Portal에 로그인하여 컨시어지 구독에 액세스를 제공하는 샌드박스에 연결되었는지 확인합니다.

1. **리소스 만들기** > **데이터베이스** > **Azure Cosmos DB**를 클릭합니다.

   ![Azure Portal 데이터베이스 창](../media/2-global-distribution/2-create-nosql-db-databases-json-tutorial.png)

1. **Azure Cosmos DB 계정 만들기** 페이지에서 위치를 포함한 새 Azure Cosmos DB 계정에 대한 설정을 입력합니다.

    <!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    설정|값|설명
    ---|---|---
    ID|*고유한 이름 입력*|이 Azure Cosmos DB 계정을 식별하는 고유한 이름을 입력합니다. URI를 만들기 위해 제공하는 ID에 *documents.azure.com*이 추가되므로 식별할 수 있는 고유한 ID를 사용합니다.<br><br>ID는 소문자, 숫자 및 하이픈(-) 문자만 포함할 수 있으며, 3-50자를 포함해야 합니다.
    API|SQL|API는 만들 계정의 형식을 결정합니다. Azure Cosmos DB는 응용 프로그램의 요구 사항을 충족하기 위해 SQL(문서 데이터베이스), Gremlin(그래프 데이터베이스), MongoDB(문서 데이터베이스), Azure Table 및 Cassandra라는 다섯 가지 API를 제공합니다. 현재 각 API에는 별도의 계정이 필요합니다. <br><br>이 모듈에서는 SQL 구문을 사용하여 쿼리할 수 있고 SQL API를 통해 액세스할 수 있는 문서 데이터베이스를 만들므로 **SQL**을 선택합니다.|
    구독|*컨시어지 구독*|컨시어지 구독을 선택합니다. 컨시어지 구독이 나열되어 표시되지 않으면 여러 테넌트를 구독에서 사용하도록 설정하고 테넌트를 변경해야 합니다. 이렇게 하려면 [샌드박스용 Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)과 같은 다음 포털 링크를 사용하여 다시 로그인합니다.
    리소스 그룹|기존 항목 사용<br><br><rgn>[샌드박스 리소스 그룹 이름]</rgn>|**기존 항목 사용**을 선택한 다음, <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 입력합니다.
    위치|*가장 가까운 지역 선택*|위의 지역 목록에서 가장 가까운 지역을 선택합니다.
    지역 중복| 사용 안 함 | 이 설정은 두 번째(쌍을 이루는) 지역에서 복제된 버전의 데이터베이스를 만듭니다. 나중에 데이터베이스를 복제할 것이므로 지금은 사용하지 않도록 설정해 둡니다.
    다중 마스터 | 사용 | 이 설정을 사용하면 동시에 여러 지역에 작성할 수 있습니다. 이 설정은 계정 만드는 동안에만 구성될 수 있습니다.
    Virtual Network|비워 둠|지금은 가상 네트워크를 비워 둡니다. 나중에 구성할 수 있습니다.

1. **검토 + 만들기**를 클릭합니다.

    ![Azure Cosmos DB에 대한 새 계정 페이지](../media/2-global-distribution/2-azure-cosmos-db-create-new-account.png)

1. 설정의 유효성을 검사한 후에 **만들기**를 클릭하여 계정을 만듭니다.

1. 계정 생성에는 몇 분 정도가 소요됩니다. 포털이 배포에 성공했다는 알림을 표시할 때까지 기다린 후 알림을 클릭합니다.

    ![알림 경고](../media/2-global-distribution/2-azure-cosmos-db-notification.png)

1. [알림] 창에서 **리소스로 이동**을 클릭합니다.

    ![리소스로 이동](../media/2-global-distribution/2-azure-cosmos-db-go-to-resource.png)

    포털에서 **축하합니다! Azure Cosmos DB 계정이 만들어졌습니다.** 페이지가 표시됩니다.

    ![Azure Portal 알림 창](../media/2-global-distribution/2-azure-cosmos-db-account-created.png)

## <a name="replicate-data-in-multiple-regions"></a>여러 지역에 데이터 복제

로스앤젤레스, 뉴욕, 도쿄에 있는 글로벌 사용자에게 가장 가까운 데이터베이스를 지금 복제해 보겠습니다.

1. 계정 페이지의 메뉴에서 **전역적으로 데이터 복제**를 클릭합니다.
1. **전역적으로 데이터 복제** 페이지에서 미국 서부 2, 미국 동부 및 일본 동부 지역을 선택한 다음, **저장**을 클릭합니다.

    Azure Portal에서 지도가 보이지 않으면 화면 왼쪽의 메뉴를 최소화하여 표시합니다.

    새 지역에 데이터가 기록되는 동안 이 페이지에 **업데이트 중** 메시지가 표시됩니다. 새로운 지역의 데이터는 30분 이내에 볼 수 있습니다.

    ![지도에서 지역을 클릭하여 추가](../media/2-global-distribution/2-global-replication.gif)

## <a name="summary"></a>요약

이 단원에서는 전 세계에서 사용자가 가장 집중되어 있는 지역에 데이터를 복제하여 해당 사용자가 사이트의 데이터에 액세스할 때 발생하는 대기 시간을 축소했습니다.
