<span data-ttu-id="1d348-101">귀사는 매우 중요한 데이터를 처리하고 많은 양의 정보를 Azure에 저장하기 때문에 공용 인터넷을 통한 연결의 보안과 안정성에 대한 우려가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-101">As your company deals with highly sensitive data and has large amounts of information it will store in Azure, there are some concerns about the security and reliability of connections over the public internet.</span></span> <span data-ttu-id="1d348-102">Azure가 높은 수준의 연결, 보안 및 안정성을 입증할 수 없다면 귀사는 도매를 Azure로 마이그레이션할 의사가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-102">The company is not willing to migrate wholesale to Azure unless it can demonstrate higher levels of connectivity, security, and reliability.</span></span>

<span data-ttu-id="1d348-103">여기에는 공용 인터넷을 통한 연결뿐만 아니라 Azure 데이터 센터에 직접 연결된 전용 회선이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-103">Here, we will go beyond connections that run over the public internet to dedicated lines direct into the Azure datacenters.</span></span>

## <a name="azure-expressroute"></a><span data-ttu-id="1d348-104">Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1d348-104">Azure ExpressRoute</span></span>

<span data-ttu-id="1d348-105">Microsoft Azure ExpressRoute를 사용하면 조직은 공급자가 구현한 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-105">Microsoft Azure ExpressRoute enables organizations to extend their on-premises networks into the Microsoft Cloud over a private connection implemented by a connectivity provider.</span></span> <span data-ttu-id="1d348-106">이 정렬은 Azure 데이터 센터에 대한 연결이 인터넷을 통하지 않고 전용 연결을 통해 수행되는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-106">This arrangement means that the connectivity to the Azure datacenters does not go over the internet but across a dedicated link.</span></span> <span data-ttu-id="1d348-107">또한 ExpressRoute는 Office 365 및 Dynamics 365와 같은 다른 Microsoft 클라우드 기반 서비스와 효율적인 연결을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-107">ExpressRoute also facilitates efficient connections with other Microsoft cloud-based services, such as Office 365 and Dynamics 365.</span></span>

<span data-ttu-id="1d348-108">ExpressRoute에서 제공하는 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-108">Advantages that ExpressRoute provides include:</span></span>

- <span data-ttu-id="1d348-109">50Mbps~10Gbps의 빠른 속도와 동적 대역폭 확장</span><span class="sxs-lookup"><span data-stu-id="1d348-109">Faster speeds, from 50 Mbps to 10 Gbps, with dynamic bandwidth scaling</span></span>

- <span data-ttu-id="1d348-110">짧아진 대기 시간</span><span class="sxs-lookup"><span data-stu-id="1d348-110">Lower latency</span></span>

- <span data-ttu-id="1d348-111">기본 제공 피어링을 통해 향상된 안정성</span><span class="sxs-lookup"><span data-stu-id="1d348-111">Greater reliability though built-in peering</span></span>

- <span data-ttu-id="1d348-112">강력한 보안</span><span class="sxs-lookup"><span data-stu-id="1d348-112">Highly secure</span></span>

<span data-ttu-id="1d348-113">ExpressRoute는 다음과 같이 다양한 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-113">ExpressRoute brings a number of further benefits, such as:</span></span>

- <span data-ttu-id="1d348-114">지원되는 모든 Azure 서비스에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="1d348-114">Connectivity to all supported Azure services</span></span>

- <span data-ttu-id="1d348-115">모든 지역에 대한 글로벌 연결(프리미엄 추가 항목 필요)</span><span class="sxs-lookup"><span data-stu-id="1d348-115">Global connectivity to all regions (requires premium add-on)</span></span>

- <span data-ttu-id="1d348-116">Border Gateway Protocol을 통한 동적 라우팅</span><span class="sxs-lookup"><span data-stu-id="1d348-116">Dynamic routing over Border Gateway Protocol</span></span>

- <span data-ttu-id="1d348-117">연결 작동 시간에 대한 SLA(서비스 수준 계약)</span><span class="sxs-lookup"><span data-stu-id="1d348-117">Service-level agreements (SLAs) for connection uptime</span></span>

- <span data-ttu-id="1d348-118">비즈니스용 Skype에 대한 QoS(서비스 품질)</span><span class="sxs-lookup"><span data-stu-id="1d348-118">Quality of Service (QoS) for Skype for Business</span></span>

<span data-ttu-id="1d348-119">또한 ExpressRoute 프리미엄 추가 기능에서는 경로 제한 증가, 글로벌 서비스 연결 및 회선당 가상 네트워크 연결 증가 등의 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-119">Additionally, there is the ExpressRoute premium add-on, which offers benefits such as increased route limits, global service connectivity, and increased virtual network links per circuit.</span></span>

## <a name="expressroute-connectivity-models"></a><span data-ttu-id="1d348-120">ExpressRoute 연결 모델</span><span class="sxs-lookup"><span data-stu-id="1d348-120">ExpressRoute connectivity models</span></span>

<span data-ttu-id="1d348-121">다음 메커니즘을 통해 ExpressRoute에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-121">Connections into ExpressRoute can be through the following mechanisms:</span></span>

- <span data-ttu-id="1d348-122">임의(IPVPN)의 네트워크</span><span class="sxs-lookup"><span data-stu-id="1d348-122">IP VPN network (any-to-any)</span></span>

- <span data-ttu-id="1d348-123">이더넷 교환을 통한 가상 교차 연결</span><span class="sxs-lookup"><span data-stu-id="1d348-123">Virtual cross-connection through an Ethernet exchange</span></span>

- <span data-ttu-id="1d348-124">지점 간 이더넷 연결</span><span class="sxs-lookup"><span data-stu-id="1d348-124">Point-to-point Ethernet connection</span></span>

 <span data-ttu-id="1d348-125">ExpressRoute 기능 및 특징은 위의 모든 연결 모델에서 모두 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-125">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span></span>

### <a name="what-is-layer-3-connectivity"></a><span data-ttu-id="1d348-126">계층 3 연결이란?</span><span class="sxs-lookup"><span data-stu-id="1d348-126">What is layer 3 connectivity?</span></span>

<span data-ttu-id="1d348-127">Microsoft에서는 업계 표준 동적 라우팅 프로토콜(BGP)을 사용하여 온-프레미스 네트워크, Azure의 인스턴스 및 Microsoft 공용 주소 간에 경로를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-127">Microsoft uses an industry-standard dynamic routing protocol (BGP) to exchange routes between your on-premises network, your instances in Azure, and Microsoft public addresses.</span></span> <span data-ttu-id="1d348-128">다른 트래픽 프로필에 네트워크를 사용하여 여러 BGP 세션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-128">We establish multiple BGP sessions with your network for different traffic profiles.</span></span>

### <a name="any-to-any-ipvpn-networks"></a><span data-ttu-id="1d348-129">임의(IPVPN)의 네트워크</span><span class="sxs-lookup"><span data-stu-id="1d348-129">Any-to-any (IPVPN) networks</span></span>

<span data-ttu-id="1d348-130">IPVPN 공급자는 일반적으로 관리 계층 3 연결을 통해 지사와 회사 데이터 센터 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-130">IPVPN providers typically provide connectivity between branch offices and your corporate datacenter over managed layer 3 connections.</span></span> <span data-ttu-id="1d348-131">ExpressRoute를 사용하면 Azure 데이터 센터가 다른 지사인 것처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-131">With ExpressRoute, the Azure datacenters appear as if they were another branch office.</span></span>

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a><span data-ttu-id="1d348-132">이더넷 교환을 통한 가상 교차 연결</span><span class="sxs-lookup"><span data-stu-id="1d348-132">Virtual cross-connection through an Ethernet Exchange</span></span>

<span data-ttu-id="1d348-133">조직이 클라우드 교환 시설과 함께 배치되는 경우 공급자의 이더넷 교환을 통해 Microsoft 클라우드에 교차 연결을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-133">If your organization is co-located with a cloud exchange facility, you request cross-connections to the Microsoft Cloud though your provider's Ethernet exchange.</span></span> <span data-ttu-id="1d348-134">Microsoft 클라우드에 대한 이러한 교차 연결은 네트워킹 OSI 모델에서와 같이 계층 2 또는 계층 3 관리 연결에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-134">These cross-connections to the Microsoft Cloud can operate at either layer 2 or layer 3 managed connections, as in the networking OSI model.</span></span>

### <a name="point-to-point-ethernet-connection"></a><span data-ttu-id="1d348-135">지점 간 이더넷 연결</span><span class="sxs-lookup"><span data-stu-id="1d348-135">Point-to-point Ethernet connection</span></span>

<span data-ttu-id="1d348-136">지점 간 이더넷 연결은 온-프레미스 데이터 센터 또는 지점 간의 계층 2 또는 관리되는 계층 3 연결을 Microsoft 클라우드에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-136">Point-to-point Ethernet links can provide layer 2 or managed layer 3 connections between your on-premises datacenters or offices to the Microsoft Cloud.</span></span>

## <a name="how-expressroute-works"></a><span data-ttu-id="1d348-137">ExpressRoute의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="1d348-137">How ExpressRoute works</span></span>

<span data-ttu-id="1d348-138">Azure ExpressRoute는 ExpressRoute 회로 및 라우팅 도메인의 조합을 사용하여 Microsoft 클라우드에 고대역폭 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-138">Azure ExpressRoute uses a combination of ExpressRoute circuits and routing domains to provide high-bandwidth connectivity to the Microsoft Cloud.</span></span>

### <a name="what-are-expressroute-circuits"></a><span data-ttu-id="1d348-139">ExpressRoute 회로란?</span><span class="sxs-lookup"><span data-stu-id="1d348-139">What are ExpressRoute circuits</span></span>

<span data-ttu-id="1d348-140">ExpressRoute 회로는 온-프레미스 인프라와 Microsoft 클라우드 간의 논리적 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-140">An ExpressRoute circuit is the logical connection between your on-premises infrastructure and the Microsoft Cloud.</span></span> <span data-ttu-id="1d348-141">일부 조직에서는 중복성을 이유로 여러 연결 공급자를 사용하지만 연결 공급자는 해당 연결을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-141">A connectivity provider implements that connection, although some organizations use multiple connectivity providers for redundancy reasons.</span></span> <span data-ttu-id="1d348-142">각 회로의 고정 대역폭은 50, 100, 200 또는 500Mbps이거나 1 또는 10Gbps이며 이들 회로 각각은 연결 공급자 및 피어링 위치에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-142">Each circuit has a fixed bandwidth of either 50, 100, 200 or 500 Mbps, or 1 or 10 Gbps, and each of those circuits map to a connectivity provider and a peering location.</span></span> <span data-ttu-id="1d348-143">또한 각 ExpressRoute 회로에는 기본 할당량 및 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-143">In addition, each ExpressRoute circuit has default quotas and limits.</span></span>

<span data-ttu-id="1d348-144">ExpressRoute 회로는 네트워크 연결 또는 네트워크 장치와 동일하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-144">An ExpressRoute circuit is not equivalent to a network connection or a network device.</span></span> <span data-ttu-id="1d348-145">각 회로는 _service_ 또는 _s- key_라는 GUID로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-145">Each circuit is defined by a GUID, called a _service_ or _s-key_.</span></span> <span data-ttu-id="1d348-146">이 S 키는 Microsoft, 연결 공급자 및 조직 간의 연결 링크를 제공하며, 암호화 비밀이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-146">This s-key provides the connectivity link between Microsoft, your connectivity provider, and your organization - it is not a cryptographic secret.</span></span> <span data-ttu-id="1d348-147">각 S 키에는 Azure ExpressRoute 회로에 대한 일대일 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-147">Each s-key has a one-to-one mapping to an Azure ExpressRoute circuit.</span></span>

<span data-ttu-id="1d348-148">각 회로에는 중복성을 위해 구성된 BGP 세션 쌍인 피어링을 최대 3개까지 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-148">Each circuit can have up to three peerings, which are a pair of BGP sessions that are configured for redundancy.</span></span> <span data-ttu-id="1d348-149">해당 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-149">They are:</span></span>

- <span data-ttu-id="1d348-150">Azure 개인</span><span class="sxs-lookup"><span data-stu-id="1d348-150">Azure private</span></span>
- <span data-ttu-id="1d348-151">Azure 공용</span><span class="sxs-lookup"><span data-stu-id="1d348-151">Azure public</span></span>
- <span data-ttu-id="1d348-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d348-152">Microsoft</span></span>

### <a name="routing-domains"></a><span data-ttu-id="1d348-153">라우팅 도메인</span><span class="sxs-lookup"><span data-stu-id="1d348-153">Routing domains</span></span>

<span data-ttu-id="1d348-154">그런 다음, ExpressRoute 회로는 라우팅 도메인에 매핑되며 각 ExpressRoute 회로에는 여러 라우팅 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-154">ExpressRoute circuits then map to routing domains, with each ExpressRoute circuit having multiple routing domains.</span></span> <span data-ttu-id="1d348-155">이러한 도메인은 위에 나열된 세 개의 피어링과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-155">These domains are the same as the three peerings listed above.</span></span> <span data-ttu-id="1d348-156">활성-활성 구성에서 라우터 쌍마다 각 라우팅 도메인이 동일하게 구성되므로 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-156">In an active-active configuration, each pair of routers would have each routing domain configured identically, thus providing high availability.</span></span> <span data-ttu-id="1d348-157">Azure 공용 및 Azure 개인 피어링 이름은 IP 주소 지정 스키마를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-157">The Azure public and Azure private peering names represent the IP addressing schemes.</span></span>

#### <a name="azure-private-peering"></a><span data-ttu-id="1d348-158">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="1d348-158">Azure private peering</span></span>

<span data-ttu-id="1d348-159">Azure 개인 피어링은 가상 머신과 같은 Azure 계산 서비스 및 가상 네트워크를 사용하여 배포된 클라우드 서비스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-159">Azure private peering connects to Azure compute services such as virtual machines and cloud services that are deployed with a virtual network.</span></span> <span data-ttu-id="1d348-160">보안과 관련해서 개인 피어링 도메인은 단순히 온-프레미스 네트워크를 Azure로 확장한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-160">As far as security goes, the private peering domain is simply an extension of your on-premises network into Azure.</span></span> <span data-ttu-id="1d348-161">그런 다음, 해당 네트워크와 Azure 가상 네트워크 간의 양방향 연결을 사용하도록 설정하여 내부 네트워크 내에서 Azure VM IP 주소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-161">You then enable bidirectional connectivity between that network and any Azure virtual networks, making the Azure VM IP addresses visible within your internal network.</span></span>

> [!NOTE]
> <span data-ttu-id="1d348-162">하나의 가상 네트워크만 개인 피어링 도메인에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-162">You can connect only one virtual network to the private peering domain.</span></span>

#### <a name="azure-public-peering"></a><span data-ttu-id="1d348-163">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="1d348-163">Azure public peering</span></span>

<span data-ttu-id="1d348-164">Azure 공용 피어링을 사용하면 Azure Storage, Azure SQL 데이터베이스 및 Azure 웹 서비스와 같은 공용 IP 주소에서 사용할 수 있는 서비스에 대한 개인 연결이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-164">Azure public peering enables private connections to services that are available on public IP addresses, such as Azure Storage, Azure SQL databases, and Azure web services.</span></span> <span data-ttu-id="1d348-165">공용 피어링을 사용하면 트래픽을 인터넷으로 라우팅하지 않고도 해당 서비스 공용 IP 주소에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-165">With public peering, you can connect to those service public IP addresses without your traffic being routed over the internet.</span></span> <span data-ttu-id="1d348-166">연결은 항상 WAN에서 Azure로 이루어지며 역순으로는 이루어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-166">Connectivity is always from your WAN to Azure, not the other way around.</span></span> <span data-ttu-id="1d348-167">또한 공용 피어링을 사용하려는 서비스는 선택할 수 없기 때문에 양자택일 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-167">This is also an all-or-nothing approach, as you cannot select the services for which you want public peering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1d348-168">Azure PaaS 서비스의 경우 공개 피어링보다는 Microsoft 피어링을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-168">For Azure PaaS services, it's recommended to use Microsoft peering rather than public peering.</span></span>

#### <a name="microsoft-peering"></a><span data-ttu-id="1d348-169">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="1d348-169">Microsoft peering</span></span>

<span data-ttu-id="1d348-170">Microsoft 피어링은 Office 365 및 Dynamics 365와 같은 클라우드 기반 SaaS 제품에 대한 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-170">Microsoft peering supports connections to cloud-based SaaS offerings, such as Office 365 and Dynamics 365.</span></span> <span data-ttu-id="1d348-171">이 피어링 옵션은 회사의 WAN과 Microsoft 클라우드 서비스 간의 양방향 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-171">This peering option provides bi-directional connectivity between your company's WAN and Microsoft cloud services.</span></span>

### <a name="expressroute-health"></a><span data-ttu-id="1d348-172">ExpressRoute 상태</span><span class="sxs-lookup"><span data-stu-id="1d348-172">ExpressRoute health</span></span>

<span data-ttu-id="1d348-173">Microsoft Azure에서 대부분의 기능과 마찬가지로 ExpressRoute 연결을 모니터링하여 만족스럽게 수행되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-173">As with most features in Microsoft Azure, you can monitor ExpressRoute connections to ensure that they are performing satisfactorily.</span></span> <span data-ttu-id="1d348-174">모니터링에는 다음 영역에 대한 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-174">Monitoring includes coverage of the following areas:</span></span>

- <span data-ttu-id="1d348-175">가용성</span><span class="sxs-lookup"><span data-stu-id="1d348-175">Availability</span></span>
- <span data-ttu-id="1d348-176">가상 네트워크에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="1d348-176">Connectivity to virtual networks</span></span>
- <span data-ttu-id="1d348-177">대역폭 사용률</span><span class="sxs-lookup"><span data-stu-id="1d348-177">Bandwidth utilization</span></span>

<span data-ttu-id="1d348-178">이 모니터링 작업의 핵심 도구는 네트워크 성능 모니터, 특히 ExpressRoute에 대한 NPM입니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-178">The key tool for this monitoring activity is Network Performance Monitor, particularly NPM for ExpressRoute.</span></span>

## <a name="summary"></a><span data-ttu-id="1d348-179">요약</span><span class="sxs-lookup"><span data-stu-id="1d348-179">Summary</span></span>

<span data-ttu-id="1d348-180">Azure ExpressRoute는 Azure 데이터 센터와 온-프레미스 또는 공동 배치 환경의 인프라 사이에 개인 연결을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-180">Azure ExpressRoute is used to create private connections between Azure datacenters and infrastructure on your premises or in a colocation environment.</span></span> <span data-ttu-id="1d348-181">ExpressRoute 연결은 공용 인터넷을 통해 연결되지 않으며 일반적인 인터넷 연결보다 안정적이고 속도가 빠르며 대기 시간이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="1d348-181">ExpressRoute connections don't go over the public internet, and they offer more reliability, faster speeds, and lower latencies than typical internet connections.</span></span>
