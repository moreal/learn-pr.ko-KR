귀사는 매우 중요한 데이터를 처리하고 많은 양의 정보를 Azure에 저장하기 때문에 공용 인터넷을 통한 연결의 보안과 안정성에 대한 우려가 있습니다. Azure가 높은 수준의 연결, 보안 및 안정성을 입증할 수 없다면 귀사는 도매를 Azure로 마이그레이션할 의사가 없습니다.

여기에는 공용 인터넷을 통한 연결뿐만 아니라 Azure 데이터 센터에 직접 연결된 전용 회선이 포함됩니다.

## <a name="azure-expressroute"></a>Azure ExpressRoute

Microsoft Azure ExpressRoute를 사용하면 조직은 공급자가 구현한 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장할 수 있습니다. 이 정렬은 Azure 데이터 센터에 대한 연결이 인터넷을 통하지 않고 전용 연결을 통해 수행되는 것을 의미합니다. 또한 ExpressRoute는 Office 365 및 Dynamics 365와 같은 다른 Microsoft 클라우드 기반 서비스와 효율적인 연결을 용이하게 합니다.

ExpressRoute에서 제공하는 장점은 다음과 같습니다.

- 50Mbps~10Gbps의 빠른 속도와 동적 대역폭 확장

- 짧아진 대기 시간

- 기본 제공 피어링을 통해 향상된 안정성

- 강력한 보안

ExpressRoute는 다음과 같이 다양한 이점을 제공합니다.

- 지원되는 모든 Azure 서비스에 대한 연결

- 모든 지역에 대한 글로벌 연결(프리미엄 추가 항목 필요)

- Border Gateway Protocol을 통한 동적 라우팅

- 연결 작동 시간에 대한 SLA(서비스 수준 계약)

- 비즈니스용 Skype에 대한 QoS(서비스 품질)

또한 ExpressRoute 프리미엄 추가 기능에서는 경로 제한 증가, 글로벌 서비스 연결 및 회선당 가상 네트워크 연결 증가 등의 혜택을 제공합니다.

## <a name="expressroute-connectivity-models"></a>ExpressRoute 연결 모델

다음 메커니즘을 통해 ExpressRoute에 연결할 수 있습니다.

- 임의(IPVPN)의 네트워크

- 이더넷 교환을 통한 가상 교차 연결

- 지점 간 이더넷 연결

 ExpressRoute 기능 및 특징은 위의 모든 연결 모델에서 모두 동일합니다.

### <a name="what-is-layer-3-connectivity"></a>계층 3 연결이란?

Microsoft에서는 업계 표준 동적 라우팅 프로토콜(BGP)을 사용하여 온-프레미스 네트워크, Azure의 인스턴스 및 Microsoft 공용 주소 간에 경로를 교환합니다. 다른 트래픽 프로필에 네트워크를 사용하여 여러 BGP 세션을 설정합니다.

### <a name="any-to-any-ipvpn-networks"></a>임의(IPVPN)의 네트워크

IPVPN 공급자는 일반적으로 관리 계층 3 연결을 통해 지사와 회사 데이터 센터 간의 연결을 제공합니다. ExpressRoute를 사용하면 Azure 데이터 센터가 다른 지사인 것처럼 나타납니다.

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a>이더넷 교환을 통한 가상 교차 연결

조직이 클라우드 교환 시설과 함께 배치되는 경우 공급자의 이더넷 교환을 통해 Microsoft 클라우드에 교차 연결을 요청합니다. Microsoft 클라우드에 대한 이러한 교차 연결은 네트워킹 OSI 모델에서와 같이 계층 2 또는 계층 3 관리 연결에서 작동할 수 있습니다.

### <a name="point-to-point-ethernet-connection"></a>지점 간 이더넷 연결

지점 간 이더넷 연결은 온-프레미스 데이터 센터 또는 지점 간의 계층 2 또는 관리되는 계층 3 연결을 Microsoft 클라우드에 제공할 수 있습니다.

## <a name="how-expressroute-works"></a>ExpressRoute의 작동 원리

Azure ExpressRoute는 ExpressRoute 회로 및 라우팅 도메인의 조합을 사용하여 Microsoft 클라우드에 고대역폭 연결을 제공합니다.

### <a name="what-are-expressroute-circuits"></a>ExpressRoute 회로란?

ExpressRoute 회로는 온-프레미스 인프라와 Microsoft 클라우드 간의 논리적 연결입니다. 일부 조직에서는 중복성을 이유로 여러 연결 공급자를 사용하지만 연결 공급자는 해당 연결을 구현합니다. 각 회로의 고정 대역폭은 50, 100, 200 또는 500Mbps이거나 1 또는 10Gbps이며 이들 회로 각각은 연결 공급자 및 피어링 위치에 매핑됩니다. 또한 각 ExpressRoute 회로에는 기본 할당량 및 제한이 있습니다.

ExpressRoute 회로는 네트워크 연결 또는 네트워크 장치와 동일하지 않습니다. 각 회로는 _service_ 또는 _s- key_라는 GUID로 정의됩니다. 이 S 키는 Microsoft, 연결 공급자 및 조직 간의 연결 링크를 제공하며, 암호화 비밀이 아닙니다. 각 S 키에는 Azure ExpressRoute 회로에 대한 일대일 매핑이 있습니다.

각 회로에는 중복성을 위해 구성된 BGP 세션 쌍인 피어링을 최대 3개까지 사용할 수 있습니다. 해당 항목은 다음과 같습니다.

- Azure 개인
- Azure 공용
- Microsoft

### <a name="routing-domains"></a>라우팅 도메인

그런 다음, ExpressRoute 회로는 라우팅 도메인에 매핑되며 각 ExpressRoute 회로에는 여러 라우팅 도메인이 있습니다. 이러한 도메인은 위에 나열된 세 개의 피어링과 동일합니다. 활성-활성 구성에서 라우터 쌍마다 각 라우팅 도메인이 동일하게 구성되므로 고가용성을 제공합니다. Azure 공용 및 Azure 개인 피어링 이름은 IP 주소 지정 스키마를 나타냅니다.

#### <a name="azure-private-peering"></a>Azure 개인 피어링

Azure 개인 피어링은 가상 머신과 같은 Azure 계산 서비스 및 가상 네트워크를 사용하여 배포된 클라우드 서비스에 연결됩니다. 보안과 관련해서 개인 피어링 도메인은 단순히 온-프레미스 네트워크를 Azure로 확장한 것입니다. 그런 다음, 해당 네트워크와 Azure 가상 네트워크 간의 양방향 연결을 사용하도록 설정하여 내부 네트워크 내에서 Azure VM IP 주소를 표시합니다.

> [!NOTE]
> 하나의 가상 네트워크만 개인 피어링 도메인에 연결할 수 있습니다.

#### <a name="azure-public-peering"></a>Azure 공용 피어링

Azure 공용 피어링을 사용하면 Azure Storage, Azure SQL 데이터베이스 및 Azure 웹 서비스와 같은 공용 IP 주소에서 사용할 수 있는 서비스에 대한 개인 연결이 가능합니다. 공용 피어링을 사용하면 트래픽을 인터넷으로 라우팅하지 않고도 해당 서비스 공용 IP 주소에 연결할 수 있습니다. 연결은 항상 WAN에서 Azure로 이루어지며 역순으로는 이루어지지 않습니다. 또한 공용 피어링을 사용하려는 서비스는 선택할 수 없기 때문에 양자택일 접근 방식입니다.

> [!NOTE]
> Azure PaaS 서비스의 경우 공개 피어링보다는 Microsoft 피어링을 사용하는 것이 좋습니다.

#### <a name="microsoft-peering"></a>Microsoft 피어링

Microsoft 피어링은 Office 365 및 Dynamics 365와 같은 클라우드 기반 SaaS 제품에 대한 연결을 지원합니다. 이 피어링 옵션은 회사의 WAN과 Microsoft 클라우드 서비스 간의 양방향 연결을 제공합니다.

### <a name="expressroute-health"></a>ExpressRoute 상태

Microsoft Azure에서 대부분의 기능과 마찬가지로 ExpressRoute 연결을 모니터링하여 만족스럽게 수행되는지 확인할 수 있습니다. 모니터링에는 다음 영역에 대한 내용이 포함됩니다.

- 가용성
- 가상 네트워크에 대한 연결
- 대역폭 사용률

이 모니터링 작업의 핵심 도구는 네트워크 성능 모니터, 특히 ExpressRoute에 대한 NPM입니다.

## <a name="summary"></a>요약

Azure ExpressRoute는 Azure 데이터 센터와 온-프레미스 또는 공동 배치 환경의 인프라 사이에 개인 연결을 생성하는 데 사용됩니다. ExpressRoute 연결은 공용 인터넷을 통해 연결되지 않으며 일반적인 인터넷 연결보다 안정적이고 속도가 빠르며 대기 시간이 짧습니다.
