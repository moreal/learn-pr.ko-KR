<span data-ttu-id="06ab5-101">온-프레미스 환경과 Azure를 통합하려면 암호화된 연결을 만드는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-101">To integrate your on-premises environment with Azure, you need the ability to create an encrypted connection.</span></span> <span data-ttu-id="06ab5-102">공용 인터넷 또는 전용 링크를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-102">You can connect over the public internet or over a dedicated link.</span></span> <span data-ttu-id="06ab5-103">여기에서는 온-프레미스 환경에서 들어오는 연결에 대한 엔드포인트를 제공하는 Azure VPN Gateway를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-103">Here, we'll look at Azure VPN Gateway, which provides an endpoint for incoming connections from on-premises environments.</span></span>

<span data-ttu-id="06ab5-104">Azure 가상 네트워크를 설정하고 Azure에서 사이트 및 Azure 가상 네트워크 간에 모든 데이터 전송이 암호화되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-104">You have set up an Azure virtual network and need to ensure that any data transfers from Azure to your site and between Azure virtual networks are encrypted.</span></span> <span data-ttu-id="06ab5-105">지역과 구독 간에 가상 네트워크를 연결하는 방법도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-105">You also need to know how to connect virtual networks between regions and subscriptions.</span></span>

## <a name="describe-a-vpn-gateway"></a><span data-ttu-id="06ab5-106">VPN 게이트웨이 설명</span><span class="sxs-lookup"><span data-stu-id="06ab5-106">Describe a VPN gateway</span></span>

<span data-ttu-id="06ab5-107">Azure VPN 게이트웨이는 인터넷을 통해 온-프레미스 위치에서 Azure로 들어오는 암호화된 연결에 대한 엔드포인트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-107">An Azure VPN gateway provides an endpoint for incoming encrypted connections from on-premises locations to Azure over the internet.</span></span> <span data-ttu-id="06ab5-108">다른 지역의 Azure 데이터 센터를 연결하는 Microsoft의 전용 네트워크를 통해 Azure 가상 네트워크 간에 암호화된 트래픽을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-108">It can also send encrypted traffic between Azure virtual networks over Microsoft's dedicated network that links Azure datacenters in different regions.</span></span> <span data-ttu-id="06ab5-109">이 구성을 사용하면 다른 지역의 가상 머신 및 서비스를 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-109">This configuration allows you to link virtual machines and services in different regions securely.</span></span>

<span data-ttu-id="06ab5-110">각 가상 네트워크에는 하나의 VPN Gateway만이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-110">Each virtual network can have only one VPN gateway.</span></span> <span data-ttu-id="06ab5-111">해당 VPN Gateway에 대한 모든 연결은 사용 가능한 네트워크 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-111">All connections to that VPN gateway share the available network bandwidth.</span></span>

<span data-ttu-id="06ab5-112">각 가상 네트워크 게이트웨이 내에는 두 개 이상의 VM(가상 머신)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-112">Within each virtual network gateway are two or more virtual machines (VMs).</span></span> <span data-ttu-id="06ab5-113">이러한 VM은 _게이트웨이 서브넷_이라는 지정된 특별한 서브넷에 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-113">These VMs have been deployed to a special subnet that you specify, called the _gateway subnet_.</span></span> <span data-ttu-id="06ab5-114">이러한 VM에는 특정 게이트웨이 서비스와 함께 다른 네트워크 연결에 대한 라우팅 테이블이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-114">They contain routing tables for connections to other networks, along with specific gateway services.</span></span> <span data-ttu-id="06ab5-115">이러한 VM 및 게이트웨이 서브넷은 강화된 네트워크 장치와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-115">These VMs and the gateway subnet are similar to a hardened network device.</span></span> <span data-ttu-id="06ab5-116">이러한 VM을 직접 구성할 필요가 없으며 게이트웨이 서브넷에 추가 리소스를 배포하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-116">You don't need to configure these VMs directly and should not deploy any additional resources into the gateway subnet.</span></span>

<span data-ttu-id="06ab5-117">가상 네트워크 게이트웨이 생성을 완료하는 데 시간이 걸릴 수 있으므로 적절하게 계획해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-117">Creating a virtual network gateway can take some time to complete, so it's vital that you plan appropriately.</span></span> <span data-ttu-id="06ab5-118">가상 네트워크 게이트웨이를 만들 때 프로비전 프로세스는 게이트웨이 VM을 생성하고 게이트웨이 서브넷에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-118">When you create a virtual network gateway, the provisioning process generates the gateway VMs and deploys them to the gateway subnet.</span></span> <span data-ttu-id="06ab5-119">이러한 VM에는 게이트웨이를 구성하는 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-119">These VMs will have the settings that you configure on the gateway.</span></span>

<span data-ttu-id="06ab5-120">키 설정은 **_게이트웨이 형식_** 이며 VPN Gateway의 경우 "vpn" 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-120">A key setting is the **_gateway type_**, which for a VPN gateway will be of type "vpn".</span></span> <span data-ttu-id="06ab5-121">VPN 게이트웨이에 대한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-121">Options for VPN gateways include:</span></span>

- <span data-ttu-id="06ab5-122">IPsec/IKE VPN 터널링을 통해 VPN 게이트웨이를 다른 VPN 게이트웨이에 연결하는 네트워크 간 연결.</span><span class="sxs-lookup"><span data-stu-id="06ab5-122">Network-to-network connections over IPsec/IKE VPN tunneling, linking VPN gateways to other VPN gateways.</span></span>

- <span data-ttu-id="06ab5-123">사이트 간 연결을 만드는 전용 VPN 장치를 통해 온-프레미스 네트워크를 Azure에 연결하기 위한 교차 프레미스 IPsec/IKE VPN 터널링.</span><span class="sxs-lookup"><span data-stu-id="06ab5-123">Cross-premises IPsec/IKE VPN tunneling, for connecting on-premises networks to Azure through dedicated VPN devices to create site-to-site connections.</span></span>

- <span data-ttu-id="06ab5-124">Azure의 리소스에 클라이언트 컴퓨터를 연결하기 위한 IKEv2 또는 SSTP를 통한 지점 및 사이트 간 연결.</span><span class="sxs-lookup"><span data-stu-id="06ab5-124">Point-to-site connections over IKEv2 or SSTP, to link client computers to resources in Azure.</span></span>

<span data-ttu-id="06ab5-125">이제 VPN 게이트웨이를 계획하기 위해 고려해야 할 요인을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-125">Now, let's look at the factors you need to consider for planning your VPN gateway.</span></span>

## <a name="plan-a-vpn-gateway"></a><span data-ttu-id="06ab5-126">VPN 게이트웨이 계획</span><span class="sxs-lookup"><span data-stu-id="06ab5-126">Plan a VPN gateway</span></span>

<span data-ttu-id="06ab5-127">VPN 게이트웨이를 계획할 때 고려해야 할 세 가지 아키텍처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-127">When you're planning a VPN gateway, there are three architectures to consider:</span></span>

- <span data-ttu-id="06ab5-128">인터넷을 통한 지점 및 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-128">Point to site over the internet</span></span>
- <span data-ttu-id="06ab5-129">인터넷을 통한 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-129">Site to site over the internet</span></span>
- <span data-ttu-id="06ab5-130">Azure ExpressRoute와 같은 전용 네트워크를 통한 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-130">Site to site over a dedicated network, such as Azure ExpressRoute</span></span>

### <a name="planning-factors"></a><span data-ttu-id="06ab5-131">계획 요소</span><span class="sxs-lookup"><span data-stu-id="06ab5-131">Planning factors</span></span>

<span data-ttu-id="06ab5-132">계획 프로세스 동안 처리해야 하는 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-132">Factors that you need to cover during your planning process include:</span></span>

- <span data-ttu-id="06ab5-133">처리량 - Mbps 또는 Gbps</span><span class="sxs-lookup"><span data-stu-id="06ab5-133">Throughput - Mbps or Gbps</span></span>
- <span data-ttu-id="06ab5-134">백본 - 인터넷 또는 개인?</span><span class="sxs-lookup"><span data-stu-id="06ab5-134">Backbone - internet or private?</span></span>
- <span data-ttu-id="06ab5-135">공용(정적) IP 주소의 가용성</span><span class="sxs-lookup"><span data-stu-id="06ab5-135">Availability of a public (static) IP address</span></span>
- <span data-ttu-id="06ab5-136">VPN 장치 호환성</span><span class="sxs-lookup"><span data-stu-id="06ab5-136">VPN device compatibility</span></span>
- <span data-ttu-id="06ab5-137">여러 클라이언트 연결 또는 사이트 간 연결?</span><span class="sxs-lookup"><span data-stu-id="06ab5-137">Multiple client connections or a site-to-site link?</span></span>
- <span data-ttu-id="06ab5-138">VPN Gateway 형식</span><span class="sxs-lookup"><span data-stu-id="06ab5-138">VPN gateway type</span></span>
- <span data-ttu-id="06ab5-139">Azure VPN Gateway SKU</span><span class="sxs-lookup"><span data-stu-id="06ab5-139">Azure VPN Gateway SKU</span></span>

<span data-ttu-id="06ab5-140">다음 표에서는 이러한 계획 문제 중 일부를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-140">The following table summarizes some of these planning issues.</span></span> <span data-ttu-id="06ab5-141">나머지는 나중에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-141">The remainder are discussed later.</span></span>

|                           |  <span data-ttu-id="06ab5-142">지점 및 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-142">Point to site</span></span>            | <span data-ttu-id="06ab5-143">사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-143">Site to site</span></span>                          |  <span data-ttu-id="06ab5-144">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06ab5-144">ExpressRoute</span></span>                 |
| -------------             | -------------             | -------------                         | ---------                     |
| <span data-ttu-id="06ab5-145">Azure 지원 서비스</span><span class="sxs-lookup"><span data-stu-id="06ab5-145">Azure supported services</span></span>  | <span data-ttu-id="06ab5-146">Cloud 서비스 및 VM</span><span class="sxs-lookup"><span data-stu-id="06ab5-146">Cloud services and VMs</span></span>    | <span data-ttu-id="06ab5-147">Cloud 서비스 및 VM</span><span class="sxs-lookup"><span data-stu-id="06ab5-147">Cloud services and VMs</span></span>                | <span data-ttu-id="06ab5-148">지원되는 모든 서비스</span><span class="sxs-lookup"><span data-stu-id="06ab5-148">All supported services</span></span>        |
| <span data-ttu-id="06ab5-149">일반적인 대역폭</span><span class="sxs-lookup"><span data-stu-id="06ab5-149">Typical bandwidth</span></span>         | <span data-ttu-id="06ab5-150">VPN Gateway SKU에 따름</span><span class="sxs-lookup"><span data-stu-id="06ab5-150">Depends on VPN Gateway SKU</span></span>    | <span data-ttu-id="06ab5-151">집계를 사용하여 최대 1Gbps</span><span class="sxs-lookup"><span data-stu-id="06ab5-151">Up to 1 Gbps with aggregation</span></span>         | <span data-ttu-id="06ab5-152">50Mbps에서 10Gbps 사이</span><span class="sxs-lookup"><span data-stu-id="06ab5-152">From 50 Mbps to 10 Gbps</span></span>       |
| <span data-ttu-id="06ab5-153">지원되는 프로토콜</span><span class="sxs-lookup"><span data-stu-id="06ab5-153">Protocols supported</span></span>       | <span data-ttu-id="06ab5-154">SSTP 및 IPsec</span><span class="sxs-lookup"><span data-stu-id="06ab5-154">SSTP and IPsec</span></span>            | <span data-ttu-id="06ab5-155">IPsec</span><span class="sxs-lookup"><span data-stu-id="06ab5-155">IPsec</span></span>                                 | <span data-ttu-id="06ab5-156">직접 연결, VLAN</span><span class="sxs-lookup"><span data-stu-id="06ab5-156">Direct connection, VLANs</span></span>      |
| <span data-ttu-id="06ab5-157">라우팅</span><span class="sxs-lookup"><span data-stu-id="06ab5-157">Routing</span></span>                   | <span data-ttu-id="06ab5-158">RouteBased(동적)</span><span class="sxs-lookup"><span data-stu-id="06ab5-158">RouteBased (dynamic)</span></span>      | <span data-ttu-id="06ab5-159">PolicyBased(정적) 및 RouteBased</span><span class="sxs-lookup"><span data-stu-id="06ab5-159">PolicyBased (static) and RouteBased</span></span>   | <span data-ttu-id="06ab5-160">BGP</span><span class="sxs-lookup"><span data-stu-id="06ab5-160">BGP</span></span>                           |
| <span data-ttu-id="06ab5-161">연결 복원력</span><span class="sxs-lookup"><span data-stu-id="06ab5-161">Connection resiliency</span></span>     | <span data-ttu-id="06ab5-162">활성-수동</span><span class="sxs-lookup"><span data-stu-id="06ab5-162">Active-passive</span></span>            | <span data-ttu-id="06ab5-163">활성-수동 또는 활성-활성</span><span class="sxs-lookup"><span data-stu-id="06ab5-163">Active-passive or active-active</span></span>       | <span data-ttu-id="06ab5-164">활성-활성</span><span class="sxs-lookup"><span data-stu-id="06ab5-164">Active-active</span></span>                 |
| <span data-ttu-id="06ab5-165">사용 사례</span><span class="sxs-lookup"><span data-stu-id="06ab5-165">Use case</span></span>                  | <span data-ttu-id="06ab5-166">테스트 및 프로토타입</span><span class="sxs-lookup"><span data-stu-id="06ab5-166">Testing and prototyping</span></span>   | <span data-ttu-id="06ab5-167">개발, 테스트 및 소규모 프로덕션</span><span class="sxs-lookup"><span data-stu-id="06ab5-167">Dev, test and small-scale production</span></span>  | <span data-ttu-id="06ab5-168">엔터프라이즈/중요 업무용</span><span class="sxs-lookup"><span data-stu-id="06ab5-168">Enterprise/mission critical</span></span>   |

### <a name="gateway-skus"></a><span data-ttu-id="06ab5-169">게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="06ab5-169">Gateway SKUs</span></span>

<span data-ttu-id="06ab5-170">Azure는 게이트웨이 서비스에 대해 다음과 같은 SKU를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-170">Azure offers the following SKUs for gateway services:</span></span>

| <span data-ttu-id="06ab5-171">SKU</span><span class="sxs-lookup"><span data-stu-id="06ab5-171">SKU</span></span>              |  <span data-ttu-id="06ab5-172">S2S/-네트워크 간 터널</span><span class="sxs-lookup"><span data-stu-id="06ab5-172">S2S/network-to-network tunnels</span></span> | <span data-ttu-id="06ab5-173">P2S 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-173">P2S connections</span></span>  |  <span data-ttu-id="06ab5-174">집계 처리량 벤치마크</span><span class="sxs-lookup"><span data-stu-id="06ab5-174">Aggregate throughput benchmark</span></span>   | <span data-ttu-id="06ab5-175">용도</span><span class="sxs-lookup"><span data-stu-id="06ab5-175">Use for</span></span>                         |
| -------------    | -------------             | -------------    | ---------                         | ---------                       |
| <span data-ttu-id="06ab5-176">기본</span><span class="sxs-lookup"><span data-stu-id="06ab5-176">Basic</span></span>            | <span data-ttu-id="06ab5-177">최댓값 10</span><span class="sxs-lookup"><span data-stu-id="06ab5-177">Max 10</span></span>                    | <span data-ttu-id="06ab5-178">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="06ab5-178">Max 128</span></span>          | <span data-ttu-id="06ab5-179">100Mbps</span><span class="sxs-lookup"><span data-stu-id="06ab5-179">100 Mbps</span></span>                          | <span data-ttu-id="06ab5-180">개발/테스트/POC</span><span class="sxs-lookup"><span data-stu-id="06ab5-180">Dev/test/POC</span></span>                    |
| <span data-ttu-id="06ab5-181">VpnGw1</span><span class="sxs-lookup"><span data-stu-id="06ab5-181">VpnGw1</span></span>           | <span data-ttu-id="06ab5-182">최댓값 30</span><span class="sxs-lookup"><span data-stu-id="06ab5-182">Max 30</span></span>                    | <span data-ttu-id="06ab5-183">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="06ab5-183">Max 128</span></span>          | <span data-ttu-id="06ab5-184">650Mbps</span><span class="sxs-lookup"><span data-stu-id="06ab5-184">650 Mbps</span></span>                          | <span data-ttu-id="06ab5-185">프로덕션/중요 워크로드</span><span class="sxs-lookup"><span data-stu-id="06ab5-185">Production/critical workloads</span></span>   |
| <span data-ttu-id="06ab5-186">VpnGw2</span><span class="sxs-lookup"><span data-stu-id="06ab5-186">VpnGw2</span></span>           | <span data-ttu-id="06ab5-187">최댓값 30</span><span class="sxs-lookup"><span data-stu-id="06ab5-187">Max 30</span></span>                    | <span data-ttu-id="06ab5-188">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="06ab5-188">Max 128</span></span>          | <span data-ttu-id="06ab5-189">1Gbps</span><span class="sxs-lookup"><span data-stu-id="06ab5-189">1 Gbps</span></span>                            | <span data-ttu-id="06ab5-190">프로덕션/중요 워크로드</span><span class="sxs-lookup"><span data-stu-id="06ab5-190">Production/critical workloads</span></span>   |
| <span data-ttu-id="06ab5-191">VpnGw3</span><span class="sxs-lookup"><span data-stu-id="06ab5-191">VpnGw3</span></span>           | <span data-ttu-id="06ab5-192">최댓값 30</span><span class="sxs-lookup"><span data-stu-id="06ab5-192">Max 30</span></span>                    | <span data-ttu-id="06ab5-193">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="06ab5-193">Max 128</span></span>          | <span data-ttu-id="06ab5-194">1.25Gbps</span><span class="sxs-lookup"><span data-stu-id="06ab5-194">1.25 Gbps</span></span>                          | <span data-ttu-id="06ab5-195">프로덕션/중요 워크로드</span><span class="sxs-lookup"><span data-stu-id="06ab5-195">Production/critical workloads</span></span>   |

> [!Note]
> <span data-ttu-id="06ab5-196">올바른 SKU를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-196">It's important that you choose the right SKU.</span></span> <span data-ttu-id="06ab5-197">잘못된 SKU를 사용하여 VPN 게이트웨이를 설정한 경우 중지하고 게이트웨이를 다시 빌드해야 합니다. 그러려면 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-197">If you have set up your VPN gateway with the wrong one, you'll have to take it down and rebuild the gateway, which can be time consuming.</span></span>

## <a name="workflow"></a><span data-ttu-id="06ab5-198">워크플로</span><span class="sxs-lookup"><span data-stu-id="06ab5-198">Workflow</span></span>

<span data-ttu-id="06ab5-199">Azure에서 가상 사설 네트워킹을 사용하여 클라우드 연결 전략을 설계할 때 다음과 같은 워크플로를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-199">When designing a cloud connectivity strategy using virtual private networking on Azure, you should apply the following workflow:</span></span>

1. <span data-ttu-id="06ab5-200">연결 토폴로지를 설계하면서 연결된 모든 네트워크의 주소 공간을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-200">Design your connectivity topology, listing the address spaces for all connecting networks.</span></span>

1. <span data-ttu-id="06ab5-201">Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-201">Create an Azure virtual network.</span></span>

1. <span data-ttu-id="06ab5-202">가상 네트워크의 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-202">Create a VPN gateway for the virtual network.</span></span>

1. <span data-ttu-id="06ab5-203">필요에 따라 온-프레미스 네트워크 또는 기타 가상 네트워크에 대한 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-203">Create and configure connections to on-premises networks or other virtual networks, as required.</span></span>

1. <span data-ttu-id="06ab5-204">필요한 경우 Azure VPN 게이트웨이에 대한 지점 및 사이트 간 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-204">If required, create and configure a point-to-site connection for your Azure VPN gateway.</span></span>

### <a name="design-considerations"></a><span data-ttu-id="06ab5-205">설계 고려 사항</span><span class="sxs-lookup"><span data-stu-id="06ab5-205">Design considerations</span></span>

<span data-ttu-id="06ab5-206">가상 네트워크를 연결하기 위해 VPN 게이트웨이를 설계할 때 다음과 같은 요인을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-206">When you design your VPN gateways to connect virtual networks, you must consider the following factors:</span></span>

- <span data-ttu-id="06ab5-207">서브넷은 겹칠 수 없음</span><span class="sxs-lookup"><span data-stu-id="06ab5-207">Subnets cannot overlap</span></span>

    <span data-ttu-id="06ab5-208">하나의 위치의 서브넷은 다른 위치에 동일한 주소 공간을 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-208">It is vital that a subnet in one location does not contain the same address space as in another location.</span></span>

- <span data-ttu-id="06ab5-209">IP 주소는 고유해야 함</span><span class="sxs-lookup"><span data-stu-id="06ab5-209">IP addresses must be unique</span></span>

    <span data-ttu-id="06ab5-210">다른 위치에 동일한 IP 주소를 가진 두 호스트가 있을 수 없습니다. 해당하는 두 호스트 간에 트래픽을 라우팅할 수 없고 네트워크 간 연결에 실패하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-210">You cannot have two hosts with the same IP address in different locations, as it will be impossible to route traffic between those two hosts and the network-to-network connection will fail.</span></span>

- <span data-ttu-id="06ab5-211">VPN 게이트웨이에는 **GatewaySubnet**이라는 게이트 서브넷이 필요함</span><span class="sxs-lookup"><span data-stu-id="06ab5-211">VPN gateways need a gateway subnet called **GatewaySubnet**</span></span>

    <span data-ttu-id="06ab5-212">게이트웨이가 작동하려면 이 이름이 있어야 하며 다른 리소스를 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-212">It must have this name for the gateway to work, and it should not contain any other resources.</span></span>

### <a name="create-an-azure-virtual-network"></a><span data-ttu-id="06ab5-213">Azure 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="06ab5-213">Create an Azure virtual network</span></span>

<span data-ttu-id="06ab5-214">VPN 게이트웨이를 만들기 전에 Azure 가상 네트워크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-214">Before you create a VPN gateway, you need to create the Azure virtual network.</span></span>

### <a name="create-a-vpn-gateway"></a><span data-ttu-id="06ab5-215">VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="06ab5-215">Create a VPN gateway</span></span>

<span data-ttu-id="06ab5-216">생성하는 VPN 게이트웨이 형식은 아키텍처에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-216">The type of VPN gateway you create will depend on your architecture.</span></span> <span data-ttu-id="06ab5-217">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-217">Options are:</span></span>

- <span data-ttu-id="06ab5-218">경로 기반</span><span class="sxs-lookup"><span data-stu-id="06ab5-218">RouteBased</span></span>

    <span data-ttu-id="06ab5-219">경로 기반 VPN 장치는 임의(와일드 카드) 트래픽 선택기를 사용하며, 라우팅/전달 테이블이 서로 다른 IPsec 터널에 트래픽을 전달하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-219">Route-based VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="06ab5-220">경로 기반 연결은 일반적으로 각 IPsec 터널이 네트워크 인터페이스 또는 VTI(가상 터널 인터페이스)로 모델링되는 라우터 플랫폼에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-220">Route-based connections are typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

- <span data-ttu-id="06ab5-221">정책 기반</span><span class="sxs-lookup"><span data-stu-id="06ab5-221">PolicyBased</span></span>

    <span data-ttu-id="06ab5-222">정책 기반 VPN 장치는 두 네트워크의 접두사 조합을 사용하여 트래픽이 IPsec 터널을 통해 암호화/암호 해독되는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-222">Policy-based VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="06ab5-223">정책 기반 연결은 일반적으로 패킷 필터링을 수행하는 방화벽 장치에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-223">A policy-based connection is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="06ab5-224">IPsec 터널 암호화 및 암호 해독이 패킷 필터링 및 처리 엔진에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-224">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>

## <a name="set-up-a-vpn-gateway"></a><span data-ttu-id="06ab5-225">VPN 게이트웨이 설정</span><span class="sxs-lookup"><span data-stu-id="06ab5-225">Set up a VPN gateway</span></span>

<span data-ttu-id="06ab5-226">수행해야 하는 단계는 설치하는 VPN 게이트웨이의 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-226">The steps you need to take will depend on the type of VPN gateway that you are installing.</span></span> <span data-ttu-id="06ab5-227">예를 들어 Azure Portal을 사용하여 지점 및 사이트 간 VPN 게이트웨이를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-227">For example, to create a point-to-site VPN gateway by using the Azure portal, you would carry out the following steps:</span></span>

1. <span data-ttu-id="06ab5-228">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="06ab5-228">Create a virtual network</span></span>

2. <span data-ttu-id="06ab5-229">게이트웨이 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="06ab5-229">Add a gateway subnet</span></span>

3. <span data-ttu-id="06ab5-230">DNS 서버 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="06ab5-230">Specify a DNS server (optional)</span></span>

4. <span data-ttu-id="06ab5-231">가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="06ab5-231">Create a virtual network gateway</span></span>

5. <span data-ttu-id="06ab5-232">인증서 생성</span><span class="sxs-lookup"><span data-stu-id="06ab5-232">Generate certificates</span></span>

6. <span data-ttu-id="06ab5-233">클라이언트 주소 풀 추가</span><span class="sxs-lookup"><span data-stu-id="06ab5-233">Add the client address pool</span></span>

7. <span data-ttu-id="06ab5-234">터널 형식 구성</span><span class="sxs-lookup"><span data-stu-id="06ab5-234">Configure the tunnel type</span></span>

8. <span data-ttu-id="06ab5-235">인증 유형 구성</span><span class="sxs-lookup"><span data-stu-id="06ab5-235">Configure the authentication type</span></span>

9. <span data-ttu-id="06ab5-236">루트 인증서 공용 인증서 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="06ab5-236">Upload the root certificate public certificate data</span></span>

10. <span data-ttu-id="06ab5-237">내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="06ab5-237">Install an exported client certificate</span></span>

11. <span data-ttu-id="06ab5-238">VPN 클라이언트 구성 패키지 생성 및 설치</span><span class="sxs-lookup"><span data-stu-id="06ab5-238">Generate and install the VPN client configuration package</span></span>

12. <span data-ttu-id="06ab5-239">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="06ab5-239">Connect to Azure</span></span>

<span data-ttu-id="06ab5-240">여러 옵션을 사용한 각 구성 경로 및 Azure VPN 게이트웨이를 통한 여러 구성 경로가 있으므로 이 과정에서 모든 설정을 다룰 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-240">As there are several configuration paths with Azure VPN gateways, each with multiple options, it is not possible to cover every setup in this course.</span></span> <span data-ttu-id="06ab5-241">자세한 내용은 추가 리소스 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06ab5-241">For more information, see the Additional Resources section.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="06ab5-242">게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="06ab5-242">Configure the gateway</span></span>

<span data-ttu-id="06ab5-243">게이트웨이를 만들면 이를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-243">Once your gateway is created, you'll need to configure it.</span></span>  <span data-ttu-id="06ab5-244">이름, 위치, DNS 서버 등과 같은 몇 가지 구성 설정을 제공해야 합니다. 자세한 내용은 연습에서 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-244">There are several configuration settings you will need to provide, such as the name, location, DNS server, etc. We will go into these in more detail in the exercise.</span></span>

## <a name="summary"></a><span data-ttu-id="06ab5-245">요약</span><span class="sxs-lookup"><span data-stu-id="06ab5-245">Summary</span></span>

<span data-ttu-id="06ab5-246">Azure VPN 게이트웨이는 지점 및 사이트 간, 사이트 간 또는 네트워크 간 연결을 가능하게 하는 Azure 가상 네트워크의 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-246">Azure VPN gateways are a component in Azure virtual networks that enable point-to-site, site-to-site, or network-to-network connections.</span></span> <span data-ttu-id="06ab5-247">Azure VPN 게이트웨이를 사용하면 개별 클라이언트 컴퓨터가 Azure의 리소스에 연결하거나, Azure로 온-프레미스 네트워크를 확장하거나, 다른 지역 및 구독의 가상 네트워크 간 연결을 용이하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ab5-247">Azure VPN gateways enable individual client computers to connect to resources in Azure, extend on-premises networks into Azure, or facilitate connections between virtual networks in different regions and subscriptions.</span></span>
