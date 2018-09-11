<span data-ttu-id="23afa-101">회사가 매우 중요한 데이터를 처리하고 많은 양의 정보를 Azure에 저장하므로 공용 인터넷을 통한 연결의 보안과 안정성에 대해 우려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-101">As your company deals with highly-sensitive data and has large amounts of information it will store in Azure, there are some concerns about the security and reliability of connections over the public internet.</span></span> <span data-ttu-id="23afa-102">Azure가 더 높은 수준의 연결, 보안 및 안정성을 시연할 수 없다면 회사에서는 도매를 Azure로 마이그레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-102">The company is not willing to migrate wholesale to Azure unless it can demonstrate higher levels of connectivity, security, and reliability.</span></span>

<span data-ttu-id="23afa-103">여기에서는 공용 인터넷을 통해 실행되는 연결부터 Azure 데이터 센터에 직접 연결된 전용 회선을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-103">Here, we will go beyond connections that run over the public internet to dedicated lines direct into the Azure data centers.</span></span>

## <a name="azure-expressroute"></a><span data-ttu-id="23afa-104">Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23afa-104">Azure ExpressRoute</span></span>

<span data-ttu-id="23afa-105">Microsoft Azure ExpressRoute를 사용하면 조직이 연결 공급자에 의해 구현된 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-105">Microsoft Azure ExpressRoute enables organizations to extend their on-premises networks into the Microsoft cloud over a private connection implemented by a connectivity provider.</span></span> <span data-ttu-id="23afa-106">이 정렬은 Azure 데이터 센터에 대한 연결이 인터넷이 아닌 전용 연결을 통해 수행되는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-106">This arrangement means that the connectivity to the Azure data centers does not go over the internet but across a dedicated link.</span></span> <span data-ttu-id="23afa-107">또한 ExpressRoute는 Office 365 및 Dynamics 365와 같은 다른 Microsoft 클라우드 기반 서비스와 효율적인 연결을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-107">ExpressRoute also facilitates efficient connections with other Microsoft cloud-based services, such as Office 365 and Dynamics 365.</span></span>

<span data-ttu-id="23afa-108">ExpressRoute에서 제공하는 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-108">Advantages that ExpressRoute provides include:</span></span>

- <span data-ttu-id="23afa-109">동적 대역폭 크기 조정을 포함한 50Mbps에서 10Gbps 사이의 빠른 속도</span><span class="sxs-lookup"><span data-stu-id="23afa-109">Faster speeds, from 50 Mbps to 10 Gbps, with dynamic bandwidth scaling</span></span>

- <span data-ttu-id="23afa-110">낮은 대기 시간</span><span class="sxs-lookup"><span data-stu-id="23afa-110">Lower latency</span></span>

- <span data-ttu-id="23afa-111">기본 제공 피어링을 통한 안정성</span><span class="sxs-lookup"><span data-stu-id="23afa-111">Greater reliability though built-in peering</span></span>

- <span data-ttu-id="23afa-112">뛰어난 보안</span><span class="sxs-lookup"><span data-stu-id="23afa-112">Highly secure</span></span>

<span data-ttu-id="23afa-113">ExpressRoute는 다음과 같은 다양한 추가 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-113">ExpressRoute brings a number of further benefits, such as:</span></span>

- <span data-ttu-id="23afa-114">지원되는 모든 Azure 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="23afa-114">Connectivity to all supported Azure services</span></span>

- <span data-ttu-id="23afa-115">모든 지역에 대한 글로벌 연결(프리미엄 추가 항목 필요)</span><span class="sxs-lookup"><span data-stu-id="23afa-115">Global connectivity to all regions (requires premium add-on)</span></span>

- <span data-ttu-id="23afa-116">Border Gateway Protocol을 통한 동적 라우팅</span><span class="sxs-lookup"><span data-stu-id="23afa-116">Dynamic routing over Border Gateway Protocol</span></span>

- <span data-ttu-id="23afa-117">연결 가동 시간 동안 SLA(서비스 수준 약정)</span><span class="sxs-lookup"><span data-stu-id="23afa-117">Service Level Agreements (SLA) for connection uptime</span></span>

- <span data-ttu-id="23afa-118">비즈니스용 Skype에 대한 QoS(서비스 품질)</span><span class="sxs-lookup"><span data-stu-id="23afa-118">Quality of Service (QoS) for Skype for Business</span></span>

<span data-ttu-id="23afa-119">또한 ExpressRoute 프리미엄 추가 항목에서는 경로 제한 증가, 글로벌 서비스 연결, 회선당 vNet 연결 증가 등의 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-119">Additionally, there is the ExpressRoute premium add-on, which offers benefits such as increased route limits, global service connectivity, and increased vNet links per circuit.</span></span>

## <a name="expressroute-connectivity-models"></a><span data-ttu-id="23afa-120">ExpressRoute 연결 모델</span><span class="sxs-lookup"><span data-stu-id="23afa-120">ExpressRoute Connectivity Models</span></span>

<span data-ttu-id="23afa-121">다음 메커니즘을 통해 ExpressRoute에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-121">Connections into ExpressRoute can be through the following mechanisms:</span></span>

- <span data-ttu-id="23afa-122">임의(IP VPN)의 네트워크</span><span class="sxs-lookup"><span data-stu-id="23afa-122">IP VPN network (any-to-any)</span></span>

- <span data-ttu-id="23afa-123">이더넷 교환을 통한 가상 교차 연결</span><span class="sxs-lookup"><span data-stu-id="23afa-123">Virtual cross-connection through an Ethernet exchange</span></span>

- <span data-ttu-id="23afa-124">지점 간 이더넷 연결</span><span class="sxs-lookup"><span data-stu-id="23afa-124">Point-to-point Ethernet connection</span></span>

 <span data-ttu-id="23afa-125">ExpressRoute 기능 및 특징은 위의 모든 연결 모델에 걸쳐 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-125">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span></span>

### <a name="what-is-layer-3-connectivity"></a><span data-ttu-id="23afa-126">3계층 연결이란?</span><span class="sxs-lookup"><span data-stu-id="23afa-126">What is layer 3 connectivity?</span></span>

<span data-ttu-id="23afa-127">Microsoft에서는 업계 표준 동적 라우팅 프로토콜(BGP)을 사용하여 온-프레미스 네트워크, Azure의 인스턴스 및 Microsoft 공용 주소 간에 경로를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-127">Microsoft uses industry standard dynamic routing protocol (BGP) to exchange routes between your on-premises network, your instances in Azure, and Microsoft public addresses.</span></span> <span data-ttu-id="23afa-128">다른 트래픽 프로필의 네트워크를 사용하여 여러 BGP 세션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-128">We establish multiple BGP sessions with your network for different traffic profiles.</span></span>
### <a name="any-to-any-ipvpn-networks"></a><span data-ttu-id="23afa-129">임의(IPVPN)의 네트워크</span><span class="sxs-lookup"><span data-stu-id="23afa-129">Any-to-any (IPVPN) networks</span></span>

<span data-ttu-id="23afa-130">IPVPN 공급자는 일반적으로 관리 계층 3 연결을 통해 지사와 회사 데이터 센터 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-130">IPVPN providers typically provide connectivity between branch offices and your corporate data center over managed layer 3 connections.</span></span> <span data-ttu-id="23afa-131">ExpressRoute를 사용하면 Azure 데이터 센터는 다른 지사인 것처럼 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-131">With ExpressRoute, the Azure data centers appear as if they were another branch office.</span></span>

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a><span data-ttu-id="23afa-132">이더넷 교환을 통한 가상 교차 연결</span><span class="sxs-lookup"><span data-stu-id="23afa-132">Virtual Cross-connection through an Ethernet Exchange</span></span>

<span data-ttu-id="23afa-133">조직이 클라우드 교환 기능을 사용하여 함께 배치되는 경우 공급자의 이더넷 교환을 통해 Microsoft 클라우드에 교차 연결을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-133">If your organization is co-located with a cloud exchange facility, you request cross-connections to the Microsoft cloud though your provider's Ethernet exchange.</span></span> <span data-ttu-id="23afa-134">Microsoft 클라우드에 대한 이러한 교차 연결은 네트워킹 OSI 모델에서와 같이 계층 2 또는 계층 3 관리 연결에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-134">These cross-connections to the Microsoft cloud can operate either at Layer 2 or Layer 3 managed connections, as in the networking OSI model.</span></span>

### <a name="point-to-point-ethernet-connection"></a><span data-ttu-id="23afa-135">지점 간 이더넷 연결</span><span class="sxs-lookup"><span data-stu-id="23afa-135">Point-to-point Ethernet Connection</span></span>

<span data-ttu-id="23afa-136">지점 간 이더넷 연결은 온-프레미스 데이터 센터 또는 지점 간에 Microsoft 클라우드에 대한 계층 2 또는 관리 계층 3 연결을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-136">Point-to-point Ethernet links can provide Layer 2 or managed Layer 3 connections between your on-premises data centers or offices to the Microsoft Cloud.</span></span>

## <a name="how-expressroute-works"></a><span data-ttu-id="23afa-137">ExpressRoute의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="23afa-137">How ExpressRoute Works</span></span>

<span data-ttu-id="23afa-138">Azure ExpressRoute는 ExpressRoute 회로 및 라우팅 도메인의 조합을 사용하여 Microsoft 클라우드에 대한 높은 대역폭 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-138">Azure ExpressRoute uses a combination of ExpressRoute circuits and routing domains to provide high-bandwidth connectivity to the Microsoft cloud.</span></span>

### <a name="what-are-expressroute-circuits"></a><span data-ttu-id="23afa-139">ExpressRoute 회로란?</span><span class="sxs-lookup"><span data-stu-id="23afa-139">What are ExpressRoute Circuits</span></span>

<span data-ttu-id="23afa-140">ExpressRoute 회로는 온-프레미스 인프라와 Microsoft 클라우드 간의 논리적 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-140">An ExpressRoute circuit is the logical connection between your on-premises infrastructure and the Microsoft cloud.</span></span> <span data-ttu-id="23afa-141">일부 조직에서는 중복상의 이유로 여러 연결 공급자를 사용하지만 연결 공급자는 해당 연결을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-141">A connectivity provider implements that connection, although some organizations use multiple connectivity providers for redundancy reasons.</span></span> <span data-ttu-id="23afa-142">각 회로에는 50, 100, 200, 500Mbps 또는 1, 10Gbps 중 하나의 고정된 대역폭이 포함되고 해당 회로는 각각 연결 공급자 및 피어링 위치에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-142">Each circuit has a fixed bandwidth of either 50, 100, 200 or 500 Mbps, or 1 or 10 Gbps, and each of those circuits map to a connectivity provider and a peering location.</span></span> <span data-ttu-id="23afa-143">또한 각 ExpressRoute 회로에는 기본 할당량 및 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-143">In addition, each ExpressRoute circuit has default quotas and limits.</span></span>

<span data-ttu-id="23afa-144">ExpressRoute 회로는 네트워크 연결 또는 네트워크 장치에 해당하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-144">An ExpressRoute circuit is not equivalent to a network connection or a network device.</span></span> <span data-ttu-id="23afa-145">각 회로는 _service_ 또는 _s- key_라는 GUID에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-145">Each circuit is defined by a GUID, called a _service_ or _s- key_.</span></span> <span data-ttu-id="23afa-146">이 S 키는 Microsoft, 연결 공급자와 조직 간의 연결 링크를 제공하며 암호화 비밀이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-146">This s-key provides the connectivity link between Microsoft, your connectivity provider, and your organization - it is not a cryptographic secret.</span></span> <span data-ttu-id="23afa-147">각 S 키에는 Azure ExpressRoute 회로에 대한 일대일 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-147">Each s-key has a one-to-one mapping to an Azure ExpressRoute circuit.</span></span>

<span data-ttu-id="23afa-148">각 회로에는 중복성을 위해 구성된 BGP 세션 쌍인 최대 3개의 피어링이 있을 수 있습니다. 여기에는 다음 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-148">Each circuit can have up to three peerings, which are a pair of BGP sessions that are configured for redundancy, they are:</span></span>

- <span data-ttu-id="23afa-149">Azure 개인</span><span class="sxs-lookup"><span data-stu-id="23afa-149">Azure Private</span></span>
- <span data-ttu-id="23afa-150">Azure 공용</span><span class="sxs-lookup"><span data-stu-id="23afa-150">Azure Public</span></span>
- <span data-ttu-id="23afa-151">Microsoft</span><span class="sxs-lookup"><span data-stu-id="23afa-151">Microsoft</span></span>

### <a name="routing-domains"></a><span data-ttu-id="23afa-152">라우팅 도메인</span><span class="sxs-lookup"><span data-stu-id="23afa-152">Routing Domains</span></span>

<span data-ttu-id="23afa-153">ExpressRoute 회로는 여러 라우팅 도메인이 포함된 각 ExpressRoute 회로를 사용하여 라우팅 도메인에 매핑됩니다. 이 도메인은 위에 나열된 세 개의 피어링과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-153">ExpressRoute circuits then map to routing domains, with each ExpressRoute circuit having multiple routing domains, these domains being the same as the three peerings listed above.</span></span> <span data-ttu-id="23afa-154">활성-활성 구성에서 각 라우터 쌍은 각 라우팅 도메인을 동일하게 구성해야 합니다. 그러면 높은 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-154">In an active-active configuration, each pair of routers would have each routing domain configured identically, thus providing high availability.</span></span> <span data-ttu-id="23afa-155">Azure 공용 및 Azure 개인 피어링 이름은 IP 주소 지정 스키마를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-155">The Azure Public and Azure Private peering names represent the IP addressing schemes.</span></span>

#### <a name="azure-private-peering"></a><span data-ttu-id="23afa-156">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="23afa-156">Azure Private Peering</span></span>

<span data-ttu-id="23afa-157">Azure 개인 피어링은 가상 머신과 같은 Azure 계산 서비스 및 가상 네트워크를 사용하여 배포된 클라우드 서비스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-157">Azure Private Peering connects to Azure compute services such as virtual machines and cloud services that are deployed with a virtual network.</span></span> <span data-ttu-id="23afa-158">보안과 관련해서 개인 피어링 도메인은 온-프레미스 네트워크를 Azure로 확장한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-158">As far as security goes, the private peering domain is simply an extension of your on-premises network into Azure.</span></span> <span data-ttu-id="23afa-159">해당 네트워크와 Azure Virtual Network 간의 양방향 연결을 사용하도록 설정하여 내부 네트워크 내에서 Azure VM IP 주소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-159">You then enable bidirectional connectivity between that network and any Azure virtual networks, making the Azure VM IP addresses visible within your internal network.</span></span>

> [!NOTE]
> <span data-ttu-id="23afa-160">하나의 가상 네트워크만 개인 피어링 도메인에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-160">You can only connect ONE virtual network to the private peering domain</span></span>

#### <a name="azure-public-peering"></a><span data-ttu-id="23afa-161">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="23afa-161">Azure Public Peering</span></span>

<span data-ttu-id="23afa-162">Azure 공용 피어링을 사용하면 Azure Storage, Azure SQL Database 및 Azure 웹 서비스 등 공용 IP 주소에서 사용할 수 있는 서비스에 개인 연결을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-162">Azure Public Peering enables private connections to services that are available on public IP addresses, such as Azure Storage, Azure SQL databases, and Azure Web services.</span></span> <span data-ttu-id="23afa-163">공용 피어링을 사용하면 트래픽을 인터넷으로 라우팅하지 않고 해당 서비스 공용 IP 주소에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-163">With public peering, you can connect to those service public IP addresses without your traffic being routed over the internet.</span></span> <span data-ttu-id="23afa-164">연결은 항상 WAN에서 Azure로 이루어지며 다른 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-164">Connectivity is always from your WAN to Azure, not the other way around.</span></span> <span data-ttu-id="23afa-165">공용 피어링을 사용하도록 설정하려는 서비스를 선택할 수 없으므로 양자택일 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-165">This is also an all-or-nothing approach, as you cannot select which services for which you want public peering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="23afa-166">Azure PaaS 서비스의 경우 공용 피어링 대신 Microsoft 피어링을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-166">For Azure PaaS services, it's recommended to use Microsoft peering rather than public peering</span></span>

#### <a name="microsoft-peering"></a><span data-ttu-id="23afa-167">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="23afa-167">Microsoft Peering</span></span>

<span data-ttu-id="23afa-168">Microsoft 피어링은 Office 365 및 Dynamics 365와 같은 클라우드 기반 SaaS 제품에 대한 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-168">Microsoft Peering supports connections to cloud-based SaaS offerings, such as Office 365 and Dynamics 365.</span></span> <span data-ttu-id="23afa-169">피어링 옵션은 회사의 WAN과 Microsoft 클라우드 서비스 간의 양방향 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-169">This peering option provides bi-directional connectivity between your company's WAN and Microsoft cloud services.</span></span>

### <a name="expressroute-health"></a><span data-ttu-id="23afa-170">ExpressRoute 상태</span><span class="sxs-lookup"><span data-stu-id="23afa-170">ExpressRoute Health</span></span>

<span data-ttu-id="23afa-171">Microsoft Azure에서 대부분의 기능과 마찬가지로 ExpressRoute 연결을 모니터링하여 만족스럽게 수행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-171">As with most features in Microsoft Azure, you can monitor ExpressRoute connections to ensure that they are performing satisfactorily.</span></span> <span data-ttu-id="23afa-172">모니터링에는 다음과 같은 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-172">Monitoring includes coverage of the following areas:</span></span>

- <span data-ttu-id="23afa-173">가용성</span><span class="sxs-lookup"><span data-stu-id="23afa-173">Availability</span></span>
- <span data-ttu-id="23afa-174">VNet에 대한 연결</span><span class="sxs-lookup"><span data-stu-id="23afa-174">Connectivity to VNets</span></span>
- <span data-ttu-id="23afa-175">대역폭 사용률</span><span class="sxs-lookup"><span data-stu-id="23afa-175">Bandwidth utilization</span></span>

<span data-ttu-id="23afa-176">이 모니터링 작업의 핵심 도구는 네트워크 성능 모니터, 특히 ExpressRoute에 대한 NPM입니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-176">The key tool for this monitoring activity is Network Performance Monitor, particularly NPM for ExpressRoute.</span></span>

## <a name="summary"></a><span data-ttu-id="23afa-177">요약</span><span class="sxs-lookup"><span data-stu-id="23afa-177">Summary</span></span>

<span data-ttu-id="23afa-178">Azure ExpressRoute를 사용하여 온-프레미스 또는 공동 배치 환경의 인프라와 Azure 데이터 센터 간에 개인 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-178">Azure ExpressRoute is used to create private connections between Azure datacenters and infrastructure on your premises or in a colocation environment.</span></span> <span data-ttu-id="23afa-179">ExpressRoute 연결은 공용 인터넷을 사용하지 않으며 일반적인 인터넷 연결보다 안정적이고 속도가 빠르며 대기 시간이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="23afa-179">ExpressRoute connections don't go over the public internet, and they offer more reliability, faster speeds, and lower latencies than typical internet connections.</span></span>
