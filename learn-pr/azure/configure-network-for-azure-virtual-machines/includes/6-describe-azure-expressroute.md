회사는 매우 중요 한 데이터를 처리 하 고에 많은 양의 정보를 Azure에 저장 됩니다, 몇 가지 문제가 있는 보안과 안정성을 연결 하는 방법에 대 한 공용 인터넷을 통해. 회사 더 높은 수준의 연결, 보안 및 안정성을 시연할 수 있습니다 하지 않는 한 Azure로 도매 마이그레이션할 의향이 있습니다.

여기에서 Azure 데이터 센터에 인터넷을 통해 직접 전용된 회선을 실행 하는 연결 이외의 살펴보겠습니다.

## <a name="azure-expressroute"></a>Azure ExpressRoute

Microsoft Azure ExpressRoute를 사용 하면 연결 공급자를 구현한 개인 연결을 통해 Microsoft 클라우드로 온-프레미스 네트워크를 확장할 수 있도록 합니다. 이 정렬 Azure 데이터 센터에 대 한 연결이 인터넷을 통해 하지만 전용된 링크를 통해 이동 하지는 것을 의미 합니다. 또한 ExpressRoute는 Office 365 및 Dynamics 365와 같은 다른 Microsoft 클라우드 기반 서비스와 효율적인 연결을 용이하게 합니다.

ExpressRoute에서 제공하는 장점은 다음과 같습니다.

- 동적 대역폭 크기 조정을 포함한 50Mbps에서 10Gbps 사이의 빠른 속도

- 낮은 대기 시간

- 기본 제공 피어 링을 통해 안정성

- 뛰어난 보안

ExpressRoute는 다음과 같은 다양한 추가 혜택을 제공합니다.

- 지원되는 모든 Azure 서비스에 연결

- 모든 지역에 대한 글로벌 연결(프리미엄 추가 항목 필요)

- Border Gateway Protocol을 통한 동적 라우팅

- 연결 가동 시간에 대 한 서비스 수준 계약 (Sla)

- 비즈니스용 Skype에 대한 QoS(서비스 품질)

또한 경로 제한 증가, 글로벌 서비스 연결, 회선 당 가상 네트워크 연결 등의 혜택을 제공 하는 ExpressRoute premium 추가 기능에 있습니다.

## <a name="expressroute-connectivity-models"></a>ExpressRoute 연결 모델

다음 메커니즘을 통해 ExpressRoute에 연결될 수 있습니다.

- 임의(IP VPN)의 네트워크

- 이더넷 교환을 통한 가상 교차 연결

- 지점 간 이더넷 연결

 ExpressRoute 기능 및 특징은 위의 모든 연결 모델에 걸쳐 동일합니다.

### <a name="what-is-layer-3-connectivity"></a>3계층 연결이란?

Microsoft에서는 업계 표준 동적 라우팅 프로토콜 (BGP) 교환에 공용 주소 인스턴스 Azure에서 온-프레미스 네트워크와 Microsoft 간에 라우팅합니다. 다른 트래픽 프로필의 네트워크를 사용하여 여러 BGP 세션을 설정합니다.

### <a name="any-to-any-ipvpn-networks"></a>임의(IPVPN)의 네트워크

IPVPN 공급자는 일반적으로 관리 되는 레이어 3 연결을 통해 지사와 회사 데이터 센터 간의 연결을 제공합니다. ExpressRoute를 사용 하 여 Azure 데이터 센터는 다른 지사 것 처럼 나타납니다.

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a>이더넷 Exchange를 통해 가상 간 연결

조직의 클라우드 exchange 기능을 함께 배치 되며, 요청을 Microsoft 클라우드 간 연결 하지만 공급자의 이더넷 교환 합니다. Microsoft 클라우드로 이러한 간 연결은 레이어 2 또는 3 계층으로 작업할 수는 네트워킹 OSI 모델와 같이 연결을 관리 합니다.

### <a name="point-to-point-ethernet-connection"></a>지점 간 이더넷 연결

지점 간 이더넷 연결 Microsoft 클라우드로 온-프레미스 데이터 센터 또는 사무실에 간에 레이어 2 또는 관리 되는 레이어 3 연결을 제공할 수 있습니다.

## <a name="how-expressroute-works"></a>ExpressRoute의 작동 원리

Azure ExpressRoute Microsoft 클라우드로 높은 대역폭 연결을 위해 ExpressRoute 회로 및 라우팅 도메인의 조합을 사용 합니다.

### <a name="what-are-expressroute-circuits"></a>ExpressRoute 회로 무엇입니까

ExpressRoute 회로 Microsoft 클라우드 및 온-프레미스 인프라 간의 논리적 연결입니다. 일부 조직에서는 중복상의 이유로 여러 연결 공급자를 사용하지만 연결 공급자는 해당 연결을 구현합니다. 각 회로 50, 100, 200 고정된 대역폭 Mbps 또는, 500mbps, 1gbps 또는 10gbps를 있고 각 해당 회로 연결 공급자 및 피어 링 위치에 매핑합니다. 또한 각 ExpressRoute 회로에는 기본 할당량 및 제한이 있습니다.

ExpressRoute 회로 네트워크 연결 또는 네트워크 장치에 해당 하는 것은 아닙니다. 각 회로 라는 GUID에 의해 정의 되는 _서비스_ 하거나 _s 키_합니다. 암호화 암호 없는-이 s 키 조직, Microsoft 및 연결 공급자, 사이의 연결 링크를 제공 합니다. 각 S 키에는 Azure ExpressRoute 회로에 대한 일대일 매핑이 있습니다.

각 회로 중복성을 위해 구성 된 BGP 세션 쌍은 최대 3 개의 피어 링을 가질 수 있습니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

- Azure 개인
- 공용 azure
- Microsoft

### <a name="routing-domains"></a>라우팅 도메인

ExpressRoute 회로 다음 여러 라우팅 도메인이 있는 각 ExpressRoute 회로 사용 하 여 라우팅 도메인에 매핑합니다. 이러한 도메인 위에 나열 된 세 가지 피어 링와 동일 합니다. 활성-활성 구성에서 각 라우터 쌍은 각 라우팅 도메인을 동일하게 구성해야 합니다. 그러면 높은 가용성을 제공합니다. Azure 공용 및 Azure 개인 피어 링 이름을 IP을 주소 지정 스키마를 나타냅니다.

#### <a name="azure-private-peering"></a>Azure 개인 피어링

Azure 개인 피어 링 가상 머신과 같은 Azure 계산 서비스 및 가상 네트워크를 사용 하 여 배포 된 클라우드 서비스에 연결 합니다. 보안과 관련해서 개인 피어링 도메인은 온-프레미스 네트워크를 Azure로 확장한 것입니다. 해당 네트워크와 Azure Virtual Network 간의 양방향 연결을 사용하도록 설정하여 내부 네트워크 내에서 Azure VM IP 주소를 표시합니다.

> [!NOTE]
> 하나의 가상 네트워크를 개인 피어 링 도메인에 연결할 수 있습니다.

#### <a name="azure-public-peering"></a>Azure 공용 피어링

Azure 공용 피어 링에서 Azure Storage, Azure SQL database 및 Azure 웹 서비스 등 공용 IP 주소를 사용할 수 있는 서비스에 개인 연결을 사용 하도록 설정 합니다. 공용 피어 링을 사용 하 여 트래픽이 인터넷을 통해 라우팅되지 않고 해당 서비스 공용 IP 주소에 연결할 수 있습니다. 연결은 항상 WAN에서 Azure로 이루어지며 다른 방법은 없습니다. 이 역시 이것 아니면 저것 인 접근 방식을 공용 피어 링을 사용 하도록 설정 하려는 서비스를 선택할 수 없습니다.

> [!NOTE]
> Azure PaaS 서비스는 것이 좋습니다 Microsoft 공용 피어 링 하는 대신 피어 링을 사용 하도록 합니다.

#### <a name="microsoft-peering"></a>Microsoft 피어링

Microsoft 피어 링 연결을 클라우드 기반 SaaS 서비스, Office 365, Dynamics 365 등을 지원합니다. 피어링 옵션은 회사의 WAN과 Microsoft 클라우드 서비스 간의 양방향 연결을 제공합니다.

### <a name="expressroute-health"></a>ExpressRoute 상태

Microsoft Azure에서 대부분의 기능과 마찬가지로 ExpressRoute 연결을 모니터링하여 만족스럽게 수행되도록 할 수 있습니다. 모니터링에는 다음과 같은 내용이 포함됩니다.

- 가용성
- 가상 네트워크에 연결
- 대역폭 사용률

이 모니터링 작업의 핵심 도구는 네트워크 성능 모니터, 특히 ExpressRoute에 대한 NPM입니다.

## <a name="summary"></a>요약

Azure ExpressRoute를 사용하여 온-프레미스 또는 공동 배치 환경의 인프라와 Azure 데이터 센터 간에 개인 연결을 만듭니다. ExpressRoute 연결은 공용 인터넷을 통해 이동 하지 않습니다 하 고 안정성, 빠른 속도 및 일반적인 인터넷 연결 보다 더 낮은 대기 시간을 제공 합니다.
