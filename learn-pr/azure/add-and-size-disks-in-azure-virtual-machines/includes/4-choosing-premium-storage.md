일부 응용 프로그램은 다른 항목 보다 데이터 저장소 요구 사항이 보다를 배치합니다. 예를 들어 Microsoft Exchange server와 SharePoint 서버에는 가장 실행 고성능 디스크가 필요 합니다.

경우 기록 데이터베이스를 Azure로 법률 회사에 대 한 마이그레이션 시나리오에 다시 방문해 보겠습니다. 만들려는 프로그램 변호사와 다른 직원에 액세스할 수 있는지 사례 정보 최대한 빠른 속도로 합니다. 회사, 증가 하 고 늘어난된 수요를 처리 하 여 데이터베이스입니다.

한 가지 방법은 Azure에서 가상 머신 (Vm)의 성능을 최대화할 수 있습니다 (Vhd) 가상 하드 드라이브에 대 한 premium storage를 사용 하는 것입니다. Premium storage는 더 빠른 입력 및 출력 (IO) 표준 저장소 보다를 제공 합니다. 디스크 사용량이 많은 응용 프로그램에 대 한 더 나은 성능을 더 빠른 디스크 IO 발생합니다.

저장소 성능 계층을 비교 하 고 premium storage 계정에 자세히 알아보려면 보겠습니다.

## <a name="how-premium-storage-differs-from-standard-storage"></a>Standard storage에서 premium storage의 차이점

Azure premium storage는 Ssd (반도체 드라이브)에 구현 됩니다. Ssd 하드 디스크 드라이브 (Hdd) 보다 더 높은 IO 성능을 있고 없습니다 구동부 있기 때문에 신뢰할 수 있는 더 있을 수 있습니다. 읽기 또는 쓰기 헤드를 요청한 데이터를 검색할 디스크의 올바른 위치로 이동할 필요가 없습니다. 

표준 저장소는 Hdd에 구현 됩니다. 표준 저장소를 낮은 요금으로 청구 합니다. 비용을 제어 하는 데 표준 저장소를 선택 하 고 빠른 IO 성능이 필요한 경우 premium storage를 선택 합니다.

단일 VM에서 다양 한 표준 및 프리미엄 저장소 디스크를 사용할 수도 있습니다.

> [!NOTE]
> 관리 디스크를 사용 하는 경우 사용자가 세 번째 옵션: 표준 SSDs 합니다. 표준 Ssd 성능과 Hdd 및 Ssd premium 표준 간의 가격의 중간는 되지만 관리 되지 않는 디스크에 사용할 수 없습니다. 표준 SSDs 나중에이 모듈에에서 자세히 배웁니다.

## <a name="premium-storage-accounts"></a>프리미엄 저장소 계정

Vhd는 Azure 일반적인 용도의 storage 계정의 페이지 blob으로 저장 됩니다. Vhd에 대 한 premium storage를 사용 하려면 Vhd를 저장 해야 합니다는 **premium storage 계정**합니다. 나중에이 설정을 변경할 수 없습니다를 만들 때 저장소 계정의 성능 계층을 선택 합니다.

> [!IMPORTANT]
> 모든 Azure 지역에서 premium storage를 사용할 수 있습니다. 해당 지역의 가용성을 확인 하려면 참조 [지역별 사용 가능한 제품](https://azure.microsoft.com/en-us/global-infrastructure/services/)합니다.

### <a name="data-replication-and-premium-storage-accounts"></a>데이터 복제 및 프리미엄 저장소 계정

Microsoft Azure Storage 계정 데이터는 항상 내구성 및 고가용성을 위해 복제됩니다. Azure Storage 복제 복사본 데이터에서 보호 되는 계획 된 및 계획 되지 않은 이벤트 처럼 일시적인 하드웨어 장애, 네트워크, 정전, 대규모 자연 재해 및 등입니다. 동일한 데이터 센터, 동일한 지역 내의 영역 데이터 센터 또는 전체 지역에 데이터를 복제하도록 선택할 수 있습니다. 네 가지 유형의 복제에는

- **로컬 중복 저장소 (LRS)** -Azure는 동일한 Azure 데이터 센터 내에서 데이터를 복제 합니다. 데이터는 노드가 실패 하는 경우 사용 가능한 상태로 유지 됩니다. 그러나 전체 데이터 센터 오류가 발생 하면 데이터 불가능할 수도 있습니다.
- **지역 중복 저장소 (GRS)** -Azure는 주 지역에서 수백 마일 떨어진 보조 지역에 데이터를 복제 합니다. 저장소 계정이 GRS를 활성화 한 경우 다음 데이터는 지속 전체 지역 가동 중단 또는 주 지역을 복구할 수 없는 재해가 발생 하는 경우에.
- **읽기 액세스 지역 중복 저장소 (RA-GRS)** -Azure는 두 지역 간에 보조 위치 및 지역에서 복제 데이터에 대 한 읽기 전용 액세스를 제공 합니다. 데이터 센터 오류가 발생 하면 데이터는 읽을 수 있는 남아 있지만 수정할 수 없습니다.
- **영역 중복 저장소 (ZRS)** -Azure에 걸쳐 데이터를 복제 동기적으로 단일 지역에 3 개의 저장소 클러스터. 각 저장소 클러스터는 다른 저장소 클러스터와 물리적으로 분리되어 있으며 자체 AZ(가용성 영역)에 상주합니다. 이 유형의 복제를 사용 하 여 액세스를 계속 하 고 영역을 사용할 수 없게 되는 데이터를 관리할 수 있습니다.

표준 저장소 계정은 모든 복제 유형에 지원 하지만 premium storage 계정에 로컬 중복 저장소 (LRS)만 지원 합니다. 단일 지역에서 실행 하는 자체 Vm의 경우 이후이 제한은 일반적으로 VHD 저장소에 대 한 문제가 되지 합니다.

## <a name="migrating-from-standard-storage-to-premium-storage"></a>Standard storage에서 premium storage로 마이그레이션

처음에 올바른 유형의 저장소 계정에서 Vhd를 만드는 것이 좋습니다. 그러나 요구 사항이 변경 되는 경우에 따라, 요구가 증가할 또는 잘못 된 형식을 선택 하는 것을 알게 됩니다. 이러한 상황에서 premium storage로 이동을 고려 합니다.

마이그레이션을 시작 하기 전에 VM을 사용할 수 없게 됩니다 사용자에 게 가동 중지 시간이 관련 됩니다 하는 것이 좋습니다.

> [!NOTE]
> 표준에서 premium storage로 마이그레이션의 전체 세부 정보를 참조 하세요 [(관리 되지 않는 디스크) Azure Premium Storage로 마이그레이션](https://docs.microsoft.com/azure/storage/common/storage-migration-to-premium-storage)합니다.

Azure에서 VM을 만들면 비용과 성능 간에 적절 한 균형을 찾을 해야 합니다. Premium storage는 표준 저장소 보다 더 빠르게 IO를 지원 하기 때문에 데이터베이스와 같은 디스크 사용량이 많은 응용 프로그램에 대 한는 것이 적합 합니다.
