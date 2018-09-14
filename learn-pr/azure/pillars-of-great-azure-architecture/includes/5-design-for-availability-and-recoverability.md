조직의 임상 전문가는 가동 중지 시간을 허용하지 않습니다. 응용 프로그램은 사용자에게 영향을 최소화하면서 오류를 처리할 수 있어야 합니다. 해당 응용 프로그램이 지역화된 인시던트 및 대규모 재해 모두에 대해 작동을 유지하도록 어떻게 보장하나요? 

여기에서 아키텍처 설계에 가용성 및 복구 기능을 포함시키는 방법을 설명하겠습니다.

## <a name="availability-and-recoverability"></a>가용성 및 복구 기능

복잡한 응용 프로그램의 많은 작업은 규모에 관계 없이 잘못될 수 있습니다. 개별 서버 및 하드 드라이브가 실패할 수 있습니다. 배포 문제로 인해 데이터베이스의 모든 테이블이 의도치 않게 삭제될 수 있습니다. 전체 데이터 센터에 연결할 수 없습니다. 랜섬웨어 인시던트는 모든 데이터를 악의적으로 암호화할 수 있습니다.

*가용성*을 위한 설계는 부분 네트워크 중단 같은 소규모 인시던트 및 임시 조건을 통해 작동 시간을 유지하는 데 중점을 둡니다. 고가용성을 응용 프로그램의 각 구성 요소에 통합하고 단일 실패 지점을 제거하여 응용 프로그램이 지역화된 오류를 처리할 수 있도록 보장합니다. 또한 이러한 설계는 인프라 유지 관리의 영향을 최소화합니다. 고가용성 설계는 일반적으로 신속하고 자동으로 문제를 해결하는 것을 목적으로 합니다.

*복구 기능*을 위한 설계는 데이터 손실 및 더 큰 규모의 재해에서의 복구에 중점을 둡니다. 이러한 유형의 인시던트에서의 복구는 자동이 아니며, 어느 정도의 가동 중지 시간 또는 영구적인 데이터 손실로 이어질 수 있습니다. 재해 복구는 실행 못지않게 신중한 계획이 중요합니다.

아키텍처 설계에 고가용성 및 복구 기능을 포함시키면 사업을 가동 중지 시간 및 손실된 데이터로 인한 재정적 손실에서 보호해줍니다. 사용자의 명성이 고객의 신뢰 상실로 부정적 영향을 받지 않도록 보장해줍니다.

## <a name="architecting-for-availability-and-recoverability"></a>가용성 및 복구 기능을 위한 아키텍처

가용성 및 복구 기능을 위한 아키텍처는 응용 프로그램이 고객에게 한 약속을 충족할 수 있도록 보장해줍니다.

가용성의 경우에는 커밋하고 있는 SLA(서비스 수준 약정)를 식별합니다. SLA 관련 응용 프로그램의 잠재적인 고가용성 기능을 검사하고 적절한 검사가 있는지 및 개선해야 하는지 여부를 식별합니다. 아키텍처의 구성 요소에 중복성을 추가하는 것이 목표이므로 중단이 발생할 가능성이 별로 없습니다. 고가용성 설계 구성 요소의 예제로는 클러스터링 및 부하 분산이 있습니다. 클러스터링은 단일 VM을 조정된 VM 집합으로 바꿉니다. 하나의 VM이 실패하거나 연결될 수 없는 경우 서비스는 요청을 처리할 수 있는 다른 VM을 장애 조치(failover)할 수 있습니다. 부하 분산은 서비스의 많은 인스턴스에 요청을 분산하면서 실패한 인스턴스를 검색하고 해당 인스턴스로 요청이 라우팅되지 않도록 방지합니다.

복구 기능의 경우에는 가능한 데이터 손실 및 주요 가동 중지 시간 시나리오를 검사하는 분석을 수행합니다. 분석에는 복구 전략에 대한 탐색 및 각 전략에 대한 비용과 편익 간 균형 유지가 포함되어야 합니다. 이 연습에서는 조직의 우선 순위에 대한 중요한 인사이트를 제공하며 응용 프로그램의 역할을 명확하게 합니다. 결과에는 응용 프로그램의 복구 지점 목표(RPO) 및 복구 시간 목표(RTO) 또는 재해 복구에 대한 투자를 고려해 볼 때 허용될 수 있는 최고 수준의 데이터 손실 및 가동 중지 시간이 포함되어야 합니다. RPO 및 RTO를 정의했으면 백업을 설계하고, 기능을 데이터 손실을 보호하는 아키텍처 및 가동 중지 시간을 완화하는 복제로 복구할 수 있습니다.

모든 클라우드 공급자는 응용 프로그램의 가용성 및 복구 기능을 개선하는 데 사용할 수 있는 서비스 및 기능 모음을 제공합니다. 가능하면 기존 서비스 및 모범 사례를 사용하고 직접 만들어 사용하지 마십시오.

하드 드라이브에 장애가 발생할 수 있고, 데이터 센터에 연결할 수 없고, 해커의 공격이 있을 수 있습니다. 가용성 및 복구 기능을 사용하여 고객과 좋은 평판을 유지 관리하는 것이 좋습니다. 가용성은 네트워크 중단 등의 조건을 통한 가동 시간의 유지 관리에 중점을 두며, 복구 기능은 재해 발생 후 데이터 검색에 중점을 둡니다.