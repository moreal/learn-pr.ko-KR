디스크 성능을 예측하기 위해 선택할 수 있는 설정과 속성을 확인했습니다. 이제 _캐싱_을 통해 개선하는 방법을 살펴보겠습니다.

## <a name="disk-caching"></a>디스크 캐싱

캐시는 일반적으로 메모리에 더 빠르게 액세스할 수 있도록 데이터를 저장하는 특화된 구성 요소입니다. 캐시의 데이터는 이전에 읽은 데이터이거나 이전 계산에서 생성된 결과 데이터인 경우가 많습니다. 목표는 디스크에서 데이터를 가져오는 것보다 더 빠르게 데이터에 액세스하는 것입니다.

캐싱은 영구 저장소보다 더 빠른 읽기 및 쓰기 성능을 갖춘 전문적이고 때로는 비용이 많이 드는 임시 저장소를 사용합니다. 이 캐시 저장소는 종종 제한적이므로 캐싱을 통해 가장 큰 이점을 얻을 수 있는 데이터 작업을 결정해야 합니다. 그러나 Azure와 같이 캐시를 광범위하게 사용할 수 있는 경우에도 사용할 캐시 유형을 결정하기 전에 각 디스크의 워크로드 패턴을 파악하는 것이 여전히 중요합니다.

**읽기 캐싱**은 데이터 _검색_ 속도를 높입니다. 데이터를 영구 저장소에서 읽는 대신 더 빠른 캐시에서 읽습니다. 데이터 읽기는 다음 조건에서 캐시에 도달합니다.

- 데이터는 이미 읽었으며 캐시에 있습니다.
- 그리고 캐시는 이 모든 데이터를 보유할 만큼 충분히 큽니다.

읽기 캐싱은 순차 읽기 집합과 같이 읽기 큐에 대한 일부 _예측 가능성_이 있을 때 유용합니다. 액세스하는 데이터가 저장소 전반에 분산된 임의 I/O의 경우 캐싱은 거의 또는 전혀 유용하지 않으며 디스크 성능을 저하할 수도 있습니다.

**쓰기 캐싱**은 영구 저장소에 _데이터를 쓰는_ 속도를 높입니다. 쓰기 캐시를 사용하면 앱에서 저장할 데이터를 고려할 수 있습니다. 실제로 데이터는 디스크에 쓰기 위해 대기하는 캐시의 큐에 있습니다. 상상할 수 있듯이 캐시된 데이터가 작성되기 전에 시스템이 종료되는 경우 이 메커니즘은 잠재적인 실패 지점이 될 수 있습니다. SQL Server와 같은 일부 시스템은 쓰기 캐시된 데이터를 영구 디스크 저장소 자체로 처리합니다.

### <a name="azure-disk-caching"></a>Azure 디스크 캐싱

디스크 저장소와 관련된 두 가지 유형의 디스크 캐싱이 있습니다.

- Azure Storage 캐싱
- Azure VM(가상 머신) 디스크 캐싱

Azure Storage 캐싱은 Azure Blob Storage, Azure Files 및 Azure의 다른 콘텐츠에 대한 캐시 서비스를 제공합니다. 이러한 유형의 캐시 구성은 이 모듈의 범위를 벗어납니다.

Azure 가상 머신 디스크 캐싱은 Azure VM에 연결된 VHD(가상 하드 디스크) 파일에 대한 읽기 및 쓰기 액세스를 최적화합니다. 이 모듈에서는 디스크 캐싱을 집중적으로 다루겠습니다.

### <a name="azure-virtual-machine-disk-types"></a>Azure 가상 머신 디스크 유형

Azure VM에 사용되는 세 가지 유형의 디스크가 있습니다.

- **OS 디스크**: Azure VM이 만들어지면 Azure에서 OS(운영 체제)용 VHD를 자동으로 연결합니다.

- **임시 디스크**: Azure VM이 만들어지면 Azure에서 임시 디스크를 자동으로 추가합니다. 이 디스크는 페이지 및 스왑 파일과 같은 데이터에 사용됩니다. 이 디스크의 데이터는 유지 관리하거나 VM을 다시 배포하는 중에 손실될 수 있습니다. 따라서 데이터베이스 파일이나 트랜잭션 로그와 같은 영구 데이터를 저장하는 데는 사용하지 마세요.

- **데이터 디스크**: 응용 프로그램 데이터 또는 유지해야 하는 다른 데이터를 저장하기 위해 가상 머신에 연결된 VHD입니다.

OS 디스크 및 데이터 디스크는 Azure VM 디스크 캐싱을 활용합니다. VM 디스크의 캐시 크기는 VM 인스턴스 크기 및 VM에 탑재된 디스크의 수에 따라 다릅니다. 캐싱은 최대 4개의 데이터 디스크에 대해서만 사용하도록 설정할 수 있습니다.

## <a name="cache-options-for-azure-vms"></a>Azure VM에 대한 캐시 옵션

VM 디스크 캐싱에는 일반적으로 세 가지 옵션이 있습니다.

- **읽기/쓰기**: 캐시를 쓰기 저장합니다. 필요할 때 응용 프로그램에서 쓰기 캐시된 데이터를 영구 디스크로 올바르게 처리하는 경우에만 이 옵션을 사용합니다.
- **읽기 전용**: 캐시에서 읽기를 수행합니다.
- **없음**: 캐시가 없습니다. 이 옵션은 쓰기 전용 및 쓰기 집약적 디스크에 대해 선택합니다. 로그 파일은 쓰기 집약적 작업이므로 적합한 후보가 됩니다.

각 디스크 유형에 대해 모든 캐싱 옵션을 사용할 수 있는 것은 아닙니다. 다음 표에는 각 디스크 유형에 대한 캐싱 옵션이 나와 있습니다.

|               | **읽기 전용**  | **읽기/쓰기** | **없음** |
|---------------|----------------|----------------|----------|
| OS 디스크       | 예            | 예(기본값)  | 예      |
| 데이터 디스크     | 예(기본값)  | 예            | 예      |
| 임시 디스크     | 아니요             | 아니요             | 아니요       |

> [!NOTE]
> **L 시리즈** 및 **B-시리즈** 가상 머신에 대한 디스크 캐싱 옵션은 변경할 수 없습니다.

## <a name="performance-considerations-for-azure-vm-disk-caching"></a>Azure VM 디스크 캐싱 성능에 대한 고려 사항

그렇다면 캐시 설정이 Azure VM에서 실행되는 워크로드의 성능에 미치는 영향은 어떨까요?

### <a name="os-disk"></a>OS 디스크

VM OS 디스크의 경우 기본 동작은 캐시를 읽기/쓰기 모드에서 사용하는 것입니다. OS 디스크에 데이터 파일을 저장하는 응용 프로그램이 있고 앱에서 데이터 파일에 대해 임의의 읽기/쓰기 작업을 빈번하게 수행하는 경우 해당 파일을 캐싱이 해제된 데이터 디스크로 이동하는 것이 좋습니다. 그 이유는 무엇인가요? 읽기 큐에 순차적 읽기가 포함되지 않으면 캐싱에 거의 또는 전혀 도움이 되지 않기 때문입니다. 데이터를 순차적으로 유지하는 것처럼 캐시를 유지 관리하는 오버헤드는 디스크 성능을 떨어뜨릴 수 있습니다.

### <a name="data-disks"></a>데이터 디스크

성능에 민감한 응용 프로그램의 경우 OS 디스크 대신 데이터 디스크를 사용해야 합니다. 별도의 디스크를 사용하면 각 디스크에 적절한 캐시 설정을 구성할 수 있습니다.

예를 들어 SQL Server를 실행하는 Azure VM에서 데이터 디스크(일반 및 TempDB 데이터용)에 대해 **읽기 전용** 캐싱을 사용하도록 설정하면 성능이 크게 향상될 수 있습니다. 반면에, 로그 파일은 캐싱이 없는 데이터 디스크에 적합한 후보입니다.

> [!WARNING]
> Azure 디스크의 캐시 설정이 변경되면 대상 디스크를 분리한 이후 다시 연결합니다. 운영 체제 디스크인 경우 VM이 다시 시작됩니다. 디스크 캐시 설정을 변경하기 전에 이 중단의 영향을 받을 수 있는 모든 응용 프로그램/서비스를 중지합니다.

다음 도구 중 하나를 사용하여 가상 머신 디스크 캐시 설정을 구성할 수 있습니다.

- Azure Portal
- Azure CLI
- Azure PowerShell
- Resource Manager 템플릿

## <a name="using-the-azure-portal-to-configure-caching"></a>Azure Portal을 사용하여 캐싱을 구성

Azure Portal을 사용하여 새 VM을 프로비전하는 경우 먼저 VM을 배포한 후에 OS 디스크에 대한 기본 캐싱 구성을 읽기/쓰기에서 변경할 수 있습니다.

기존 VM에 데이터 디스크를 추가하는 경우에는 캐시 옵션을 구성한 후에 디스크를 VM에 배포할 수 있습니다.

Azure 디스크의 캐시 설정이 변경되면 대상 디스크를 분리하고 다시 연결합니다. 운영 체제 디스크인 경우 VM이 다시 시작됩니다. 디스크 캐시 설정을 변경하기 전에 이 중단의 영향을 받을 수 있는 모든 응용 프로그램/서비스를 중지합니다.

Azure Portal을 사용하여 VM을 만들고 캐시 설정을 변경해 보겠습니다.
