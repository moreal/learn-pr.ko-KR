Azure SQL 데이터베이스가 작동 중이니 원하는 SQL Server 관리 도구에 연결하여 실제 데이터로 채울 수 있습니다.

처음에는 데이터베이스를 온-프레미스에서 실행할지 아니면 클라우드에서 실행할지 고려합니다. Azure SQL Database를 사용하면 몇 가지 기본적인 옵션을 구성할 수 있고 앱에 연결할 수 있는 완전한 기능의 SQL 데이터베이스를 사용할 수 있습니다.

유지 관리할 인프라 또는 소프트웨어 패치는 없습니다. 이제 자유롭게 운송 물류 앱 프로토타입의 작동 및 실행에 좀 더 집중하고 데이터베이스 관리 부하를 줄일 수 있습니다. 프로토타입은 한 번 쓰고 마는 데모가 아닙니다. Azure SQL Database는 프로덕션 수준의 보안 및 성능 기능을 제공합니다.

각 Azure SQL 논리 서버에는 하나 이상의 데이터베이스가 포함되어 있습니다. Azure SQL Database에는 DTU와 vCore라는 두 가지 가격 책정 모델이 제공되며, 이를 통해 모든 데이터베이스에서 비용 대비 성능의 균형을 맞출 수 있습니다.

이제 막 사용하기 시작했거나, 미리 구성된 간단한 구매 옵션을 원하는 경우 DTU를 선택합니다. 만들고 비용을 지불하는 계산 및 저장소 리소스를 보다 효과적으로 제어하려는 경우 vCore를 선택합니다.

Azure Cloud Shell을 사용하면 데이터베이스 작업을 쉽게 시작할 수 있습니다. Cloud Shell에서 Azure CLI에 액세스할 수 있고, 여기에서 Azure 리소스에 대한 정보를 얻을 수 있습니다. 또한 Cloud Shell은 새 데이터베이스로 즉시 작업하는 데 도움이 되는 `sqlcmd`와 같은 여러 다양한 공통 유틸리티도 제공합니다.

## <a name="cleanup"></a>정리

Azure SQL Database 설치로 자유롭게 실험해보세요. 완료되면 데이터베이스를 삭제하는 가장 쉬운 방법은 부모 리소스 그룹을 삭제하는 것입니다.

1. 포털에서 **리소스 그룹**을 클릭합니다.

1. **logistics-db-rg**를 선택합니다.

1. **리소스 그룹 삭제**를 클릭합니다.

    ![리소스 그룹 삭제](../media-draft/delete-rg.png)

1. 프롬프트에서 “logistics-db-rg”를 입력하고 **삭제**를 클릭합니다.

## <a name="additional-resources"></a>추가 리소스

이 문서에서는 자습서 및 샘플을 포함하는 많은 정보를 제공합니다. 다음은 여기에서 설명한 내용에 대한 몇 가지 링크입니다.

- [Azure SQL Database 설명서](https://docs.microsoft.com/azure/sql-database/)
- [Azure SQL Database 구매 모델 및 리소스](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)
- [Azure SQL Database 논리 서버 및 그에 대한 관리](https://docs.microsoft.com/azure/sql-database/sql-database-logical-servers)
- [Azure SQL Database 및 SQL Data Warehouse 방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)

Cloud Shell에 대해 자세히 알아보려면 [Azure Cloud Shell 개요](https://docs.microsoft.com/azure/cloud-shell/overview)를 참조하세요.

`sqlcmd` 유틸리티에 대한 자세한 내용은 [sqlcmd 유틸리티](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-2017)를 참조하세요.
