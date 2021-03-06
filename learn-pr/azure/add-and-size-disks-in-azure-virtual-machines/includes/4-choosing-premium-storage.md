일부 응용 프로그램은 다른 응용 프로그램보다 데이터 저장소 요구 사항이 많습니다. Dynamics CRM, Exchange Server, SAP Business Suite, SQL Server, Oracle, SharePoint 등의 앱이 최고 속도로 실행되려면 지속적인 고성능과 짧은 대기 시간이 필요합니다.

VM을 만들거나 새 디스크를 추가할 때 디스크 성능에 크게 영향을 주는 몇 가지 옵션이 있는데, 그 중에서 저장소 _형식_부터 살펴보겠습니다.

## <a name="types-of-disks"></a>디스크 유형 
Azure 디스크는 99.999% 가용성을 위해 설계되었습니다. 

디스크(프리미엄 SSD 디스크, 표준 HDD 저장소, 표준 SSD)를 만들 때 선택할 수 있는 저장소에는 세 가지 성능 계층이 있습니다. VM 크기에 따라 이러한 디스크 유형을 혼합하여 사용할 수 있습니다.

### <a name="premium-ssd-disks"></a>프리미엄 SSD 디스크 

프리미엄 SSD 디스크는 SSD(반도체 드라이브)에 의해 지원되며 I/O 사용량이 많은 작업을 실행하는 VM을 위해 성능이 우수하고 대기 시간이 짧은 디스크를 지원합니다. 이러한 드라이브는 구동부가 없기 때문에 대체적으로 신뢰성이 높습니다. 읽기 또는 쓰기 헤드는 요청된 데이터를 찾기 위해 디스크에서 올바른 위치로 이동할 필요가 없습니다. 

시리즈 이름에 "s"가 포함되는 VM 크기에 프리미엄 SSD 디스크를 사용할 수 있습니다. 예를 들어 **Dv3** 및 **Dsv3 시리즈**가 있다면 **Dsv3 시리즈**에서 프리미엄 SSD 디스크를 사용할 수 있습니다.

### <a name="standard-hdd-storage"></a>표준 HDD 저장소

표준 HDD 디스크는 기존 HDD(하드 디스크 드라이브)에 의해 지원됩니다. 표준 HDD 디스크는 프리미엄 디스크보다 저렴한 요율로 요금이 청구됩니다. 표준 HDD 디스크는 모든 VM 크기에 사용할 수 있습니다.

### <a name="standard-ssd"></a>표준 SSD

프리미엄 저장소는 특정 VM 크기로 제한됩니다. 따라서 만드는 VM 유형에 따라 저장소 기능(크기, 최대 용량, 저장소 유형)이 결정됩니다. 저가형 VM을 갖고 있는데 I/O 성능을 위한 SSD 저장소가 필요한 경우 어떻게 해야 할까요? 바로 이때 표준 SSD가 필요합니다. 표준 SSD는 성능과 비용의 측면에서 표준 HDD와 프리미엄 SSD의 중간에 해당합니다.

표준 SSD는 프리미엄 저장소를 지원하지 않는 VM 크기를 포함하여 모든 VM 크기에 사용할 수 있습니다. VM에 SSD를 사용하는 유일한 방법은 표준 SSD입니다. 이 디스크 유형은 특정 지역에만 제공되며 _관리 디스크_에만 사용할 수 있습니다.

### <a name="unmanaged-vs-managed-disks"></a>관리되지 않는 디스크 및 관리 디스크

VM 또는 VHD를 만들 때 **관리되지 않는** 디스크 또는 **관리** 디스크 중에 선택할 수 있습니다.

관리되지 않는 디스크의 경우 VM 디스크에 해당하는 VHD를 유지하는 데 사용되는 저장소 계정을 사용자가 관리해야 합니다. 사용하는 공간에 대한 저장소 계정 요금을 사용자가 지불해야 합니다. 단일 저장소 계정의 고정 속도 제한은 20,000 I/O 작업 수/초입니다. 즉 하나의 저장소 계정이 전체 제한에서 40개의 표준 가상 하드 디스크를 지원할 수 있습니다. 확장해야 하는 경우 둘 이상의 저장소 계정이 필요하며, 이에 따라 복잡해질 수 있습니다.

관리 디스크가 보다 최신형이며 **권장되는 디스크 저장소 모델**입니다. 저장소 계정을 관리하는 부담이 Azure에서 해결되기 때문에 복잡한 업무가 원활하게 해결됩니다. 디스크 유형과 디스크 크기를 지정하면 Azure가 사용할 디스크와 저장소를 _모두_ 알아서 만들고 관리합니다. 저장소 계정 제한에 대해 걱정할 필요가 없으므로 규모 확장이 쉬워집니다. 기존의 관리되지 않는 디스크에 비해 다음과 같은 이점이 있습니다.

- **안정성 향상**: Azure는 비슷한 수준의 탄력성을 제공하기 위해 높은 안정성과 관련된 VHD가 Azure 스토리지의 다른 부분에 배치되도록 합니다.
- **보안 강화**: 관리 디스크는 리소스 그룹에서 관리되는 리소스입니다. 즉, 역할 기반 액세스 제어를 사용하여 VHD 데이터로 작업할 수 있는 사용자를 제한할 수 있습니다.
- **스냅숏 지원**: 스냅숏을 사용하여 VHD의 읽기 전용 복사본을 만들 수 있습니다. 소유하는 VM을 종료해야 하지만 스냅숏을 만드는 데는 몇 초 밖에 걸리지 않습니다. 작업이 완료되면 VM의 전원을 켜고 스냅숏을 사용하여 복제된 VM을 만들어서 프로덕션 문제를 해결하거나 스냅숏을 만든 시점으로 VM을 롤백할 수 있습니다.
- **백업 지원**: 관리 디스크는 VM의 서비스에 영향을 주지 않으면서 Azure Backup을 사용하여 재해 복구를 위해 다른 지역에 자동으로 백업할 수 있습니다.

보장되는 성능 특성 외에도 여러 추가 혜택이 있으므로 항상 새 VM에는 관리 디스크를 선택해야 합니다.

### <a name="disk-comparison"></a>디스크 비교
다음은 용도에 맞는 제품을 선택할 수 있도록 표준 HDD, 표준 SSD, 프리미엄 SSD를 비교한 표입니다.

|    | Azure 프리미엄 디스크 |Azure 표준 SSD 디스크(미리 보기)| Azure 표준 HDD 디스크 
|--- | ------------------ | ------------------------------- | ----------------------- 
| **디스크 유형** | 반도체 드라이브(SSD) | 반도체 드라이브(SSD) | 하드 디스크 드라이브 (HDD)  
| **개요**  | IO 사용량이 많은 작업을 실행하거나 중요 업무용 프로덕션 환경을 호스팅하는 VM을 위해 SSD 기반의 고성능, 낮은 대기 시간 디스크 지원 |HDD보다 더욱 일관된 성능 및 안정성 낮은 IOPS 작업용으로 최적화됨| 저빈도 액세스를 위한 HDD 기반의 비용 효율적인 디스크
| **시나리오**  | 프로덕션 및 성능이 중요한 워크로드 |웹 서버, 조금 사용되는 엔터프라이즈 응용 프로그램 및 개발/테스트| 백업, 중요하지 않음, 저빈도 액세스 
| **디스크 크기** | 32-4095GiB | 128-4095GiB | 32-4095GiB 
| **디스크당 최대 처리량** | 250MiB/초 | 최대 60MiB/초 | 최대 60MiB/초 
| **디스크당 최대 IOPS** | 7500IOPS | 최대 500IOPS | 최대 500IOPS 

아래는 디스크 성능에 대한 자세한 내용입니다.

## <a name="data-replication"></a>데이터 복제

Microsoft Azure Storage 계정 데이터는 내구성 및 고가용성을 위해 항상 복제됩니다. Azure Storage 복제는 계획된 이벤트 그리고 일시적 하드웨어 오류, 네트워크 또는 정전, 대규모 자연 재해 등의 계획되지 않은 이벤트로부터 데이터를 보호하기 위해 데이터를 복사합니다. 동일한 데이터 센터, 동일한 지역 내의 영역 데이터 센터 또는 전체 지역에 데이터를 복제하도록 선택할 수 있습니다. 복제에는 네 가지 유형이 있습니다.

- **LRS(로컬 중복 저장소)** - Azure는 동일한 Azure 데이터 센터 내에 데이터를 복제합니다. 노드 오류가 발생해도 데이터를 사용할 수 있습니다. 그러나 전체 데이터 센터에 오류가 발생하면 데이터를 사용할 수 없게 될 수도 있습니다.
- **GRS(지역 중복 저장소)** - Azure는 주 지역에서 수백 마일 떨어져 있는 보조 지역에 데이터를 복제합니다. 저장소 계정에서 GRS를 활성화하면 주 지역을 복구할 수 없는 전체 지역 정전 또는 재해가 발생하더라도 데이터는 지속됩니다.
- **RA-GRS(읽기 액세스 지역 중복 저장소)** - Azure는 두 번째 위치의 데이터에 대한 읽기 전용 액세스와 두 지역의 지리적 복제를 제공합니다. 데이터 센터에서 오류가 발생하면 데이터를 읽을 수 있지만 수정할 수는 없습니다.
- **ZRS(영역 중복 저장소)** - Azure는 단일 지역에 있는 3개의 저장소 클러스터에서 데이터를 동기적으로 복제합니다. 각 저장소 클러스터는 다른 저장소 클러스터와 물리적으로 분리되어 있으며 자체 AZ(가용성 영역)에 상주합니다. 이 유형의 복제를 사용하면 영역을 사용할 수 없게 되더라도 계속 데이터에 액세스하고 관리할 수 있습니다.

표준 저장소 계정은 모든 복제 유형을 지원하지만, 프리미엄 저장소 계정은 LRS(로컬 중복 저장소)만 지원합니다. VM 자체는 단일 지역에서 실행되므로 이 제한은 일반적으로 VHD 저장소에서 문제가 되지 않습니다.

## <a name="disk-performance"></a>디스크 성능

디스크 성능은 선택하는 디스크 유형에 따라 달라집니다. 각 디스크는 초당 I/O 작업 수 또는 IOPS("아이압스"로 발음)로 등급을 표시합니다. 또한 각 드라이브에는 초당 읽거나 쓸 수 있는 데이터 양을 결정하는 처리량 등급이 있습니다. 이 둘의 조합에 따라 디스크 속도가 결정됩니다.

표준 저장소를 사용할 경우 디스크당 최대 처리량은 **500IOPS 및 60MB/초**입니다(심지어 SSD에서도). 프리미엄 저장소를 사용할 경우 IOPS는 선택하는 디스크와 VM에 크기에 따라 달라집니다.

|  | P4 | P6 | P10 | P20 | P30 | P40 | P50 |
|--|----|----|-----|-----|-----|-----|-----|
| **디스크 크기** | 32GiB | 64GiB | 128GiB | 512GiB | 1TiB | 2TiB | 4TiB |
| **디스크당 최대 IOPS** | 120 | 240 | 500 | 2,300 | 5,000 | 7500 | 7500 |
| **디스크당 최대 처리량** | 25MB/초 | 50MB/초 | 100MB/초 | 200MB/초 | 250MB/초 | 250MB/초 |

보시다시피, **25MB/초** 및 **120IOPS**부터 **250MB/초** 및 **7500IOPS**까지 선택할 수 있습니다.