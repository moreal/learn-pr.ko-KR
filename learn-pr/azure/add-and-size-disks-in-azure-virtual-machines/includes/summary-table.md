
다음 표에서 디스크 관리 및 비관리 디스크로 사용할 수 있습니다.

|디스크 유형  |관리 되지 않는  | 관리  | 저장소 계정에 대 한 관리 되지 않는|
|---------|---------|---------|---------|
|[Standard HDD](https://docs.microsoft.com/azure/virtual-machines/windows/standard-storage)      |   예      |  예       |  일반 저장소 계정       |
|[표준 SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-standard-ssd)    |   no      |   예      |  해당 없음       |
|[Premium SSD](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage)    |    예     |   예      |     Premium storage 계정    |

다음은 Vm의 디스크 유형을 선택할 때 수행한 절충 작업에 대 한 요약입니다.

|디스크 유형  |상대 IOPS *  | 상대 비용  | 시나리오|
|---------|---------|---------|---------|
|[Standard HDD](https://docs.microsoft.com/azure/virtual-machines/windows/standard-storage)      |   가장 낮은      |  가장 낮은       |  일관 된 성능 및 비용 효율적인 개발 및 테스트를 요구 하는 IOPs가 낮은 워크 로드에 대 한 사용       |
|[표준 SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-standard-ssd)    |   보통|   보통      |  일관 된 성능 및 비용 효율적인 개발 및 테스트를 요구 하는 IOPs가 낮은 워크 로드에 대 한 사용 |
|[Premium SSD](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage)    |    가장 높은     |   가장 높은      |     프로덕션 및 짧은 대기 시간과 높은 처리량은 중요 한 성능 위주의 워크 로드에 대 한 사용    |

* IOPS-초당 입/출력 작업입니다.