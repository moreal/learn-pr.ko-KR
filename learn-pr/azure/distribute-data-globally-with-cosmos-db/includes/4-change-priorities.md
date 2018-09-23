여러 지역에서 데이터를 복제하면 Azure Cosmos DB에서 제공하는 자동화된 장애 조치 솔루션을 활용할 수 있습니다. 자동화된 장애 조치는 재해 또는 읽기 또는 쓰기 지역 중 하나를 오프라인 상태로 전환하는 다른 이벤트가 발생한 경우 작동하는 기능입니다. 이 기능은 오프라인 상태인 지역에서 다음 우선 순위가 지정된 지역으로 요청을 리디렉션합니다. 

미국 동부, 미국 서부, 영국 서부에 복제한 온라인 의류 사이트의 경우 미국 동부가 오프라인 상태로 전환되면 우선 순위를 지정하고, 영국 서부 대신 미국 서부로 읽기를 리디렉션하여 대기 시간을 제한할 수 있습니다. 

이 단원에서는 회사의 데이터가 복제된 지역에서 장애 조치가 작동하고 우선 순위를 설정하는 방법을 알아보세요.

## <a name="failover-basics"></a>장애 조치 기본 사항

드물게 발생하는 Azure 지역 가동 중단 또는 데이터 센터 가동 중단의 경우 Azure Cosmos DB는 영향을 받은 지역에 있는 모든 Azure Cosmos DB 계정의 장애 조치를 자동으로 트리거합니다.

**읽기 지역에 가동 중단이 발생하면 어떻게 되나요?**

영향을 받은 지역 중 하나에 읽기 지역이 있는 Azure Cosmos DB 계정은 자동으로 쓰기 지역과의 연결이 끊어지고 오프라인으로 표시됩니다. Cosmos DB SDK에서는 지역 검색 프로토콜을 구현하여 지역을 사용할 수 있는 시기를 자동으로 감지하고 기본 설정 지역 목록에서 사용 가능한 다음 지역으로 읽기 호출을 리디렉션합니다. 기본 설정 지역 목록의 어느 지역도 사용할 수 없는 경우 호출은 현재 쓰기 지역으로 자동으로 대체됩니다. 지역 장애 조치를 처리하기 위해 응용 프로그램 코드를 변경할 필요가 없습니다. 이 프로세스 전체에서 Azure Cosmos DB를 통해 일관성이 계속 보장됩니다.

영향을 받은 지역이 가동 중단에서 복구되면 해당 지역에서 영향을 받은 모든 Azure Cosmos DB 계정이 서비스를 통해 자동으로 복구됩니다. 영향을 받은 지역에 읽기 지역이 있는 Azure Cosmos DB 계정은 자동으로 현재 쓰기 지역과 동기화되고 온라인 상태가 됩니다. Azure Cosmos DB SDK에서는 새로운 지역의 가용성을 검색하고 응용 프로그램에서 구성한 기본 설정 지역 목록을 기반으로 하여 해당 지역을 현재 읽기 지역으로 선택해야 하는지 평가합니다. 후속 읽기는 응용 프로그램 코드를 변경하지 않고도 복구된 지역으로 리디렉션됩니다.

**쓰기 지역에 가동 중단이 발생하면 어떻게 되나요?**

영향을 받은 지역이 현재 쓰기 지역이고 Azure Cosmos DB 계정에 대해 자동 장애 조치(Failover)가 사용되도록 설정되면 해당 지역은 자동으로 오프라인으로 표시됩니다. 그런 다음, 대체 지역이 영향을 받은 Azure Cosmos DB 계정의 쓰기 지역으로 승격됩니다.

자동 장애 조치(Failover) 중에 Azure Cosmos DB는 지정된 우선 순위에 따라 지정된 Azure Cosmos DB 계정의 다음 쓰기 지역을 자동으로 선택합니다. 응용 프로그램은 DocumentClient 클래스의 WriteEndpoint 속성을 사용하여 쓰기 지역의 변경 내용을 검색할 수 있습니다.

영향을 받은 지역이 가동 중단에서 복구되면 해당 지역에서 영향을 받은 모든 Cosmos DB 계정이 서비스에서 자동으로 복구됩니다.

이제 데이터베이스에 대한 읽기 지역을 수정하겠습니다.

## <a name="set-read-region-priorities"></a>읽기 지역 우선 순위 설정

1. Azure Portal의 **글로벌 데이터 복제** 화면에서 **자동 장애 조치(failover)** 를 클릭합니다. 데이터베이스가 이미 둘 이상의 지역에 복제된 경우에만 자동 장애 조치(failover)가 활성화됩니다.
2. **자동 장애 조치(failover)** 화면에서 **자동 장애 조치(failover) 사용**을 **켜기**로 변경합니다.
3. **읽기 지역** 섹션에서 **미국 동부** 행의 왼쪽 부분을 클릭한 다음, 최상위 위치에 끌어다 놓습니다.
4. **일본 동부** 행의 왼쪽 부분을 클릭한 다음, 두 번째 위치에 끌어다 놓습니다.
5. **확인**을 클릭합니다.

    ![포털에서 읽기 지역 변경](../media/4-change-priorities/change-read-priorities.gif)

## <a name="summary"></a>요약

이 단원에서는 자동 장애 조치(failover)에서 제공하는 기능, 예기치 않은 가동 중단으로부터 보호하는 방법 및 읽기 지역 우선 순위를 수정하는 방법을 알아보았습니다.