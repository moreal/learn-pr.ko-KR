<span data-ttu-id="f015d-101">Azure를 사용하여 온-프레미스 환경에 통합하려면 암호화된 연결을 만드는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-101">To integrate your on-premises environment with Azure, you need the ability to create an encrypted connection.</span></span> <span data-ttu-id="f015d-102">공용 인터넷 또는 전용 연결을 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-102">You can connect over the public Internet or over a dedicated link.</span></span> <span data-ttu-id="f015d-103">여기에서는 온-프레미스 환경에서 들어오는 연결에 대한 엔드포인트를 제공하는 Azure VPN Gateway를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-103">Here, we'll look at the Azure VPN Gateway, which provides an endpoint for incoming connections from on-premises environments.</span></span>

<span data-ttu-id="f015d-104">Azure Virtual Network를 설정하고 Azure에서 사이트로 및 Azure Virtual Network 간에 데이터 전송이 모두 암호화되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-104">You have set up an Azure Virtual Network and need to ensure that any data transfers from Azure to your site and between Azure Virtual Networks are encrypted.</span></span> <span data-ttu-id="f015d-105">지역과 구독 간에 가상 네트워크를 연결하는 방법도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-105">You also need to know how to connect virtual networks between regions and subscriptions.</span></span>

## <a name="describe-a-vpn-gateway"></a><span data-ttu-id="f015d-106">VPN Gateway 설명</span><span class="sxs-lookup"><span data-stu-id="f015d-106">Describe a VPN Gateway</span></span>

<span data-ttu-id="f015d-107">Azure VPN Gateway는 인터넷을 통해 온-프레미스 위치에서 Azure로 들어오는 암호화된 연결에 대해 엔드포인트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-107">The Azure VPN Gateway provides an endpoint for incoming encrypted connections from on-premises locations to Azure over the Internet.</span></span> <span data-ttu-id="f015d-108">다른 지역의 Azure 데이터 센터를 연결하는 Microsoft의 전용 네트워크를 통해 Azure Virtual Networks 간에 암호화된 트래픽을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-108">It can also send encrypted traffic between Azure virtual networks over Microsoft's dedicated network that links Azure data centers in different regions.</span></span> <span data-ttu-id="f015d-109">이 구성을 사용하면 다른 지역에 있는 가상 머신 및 서비스를 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-109">This configuration allows you to link virtual machines and services in different regions securely.</span></span>

<span data-ttu-id="f015d-110">각 가상 네트워크에는 하나의 VPN Gateway만이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-110">Each virtual network can have only one VPN gateway.</span></span> <span data-ttu-id="f015d-111">해당 VPN Gateway에 대한 모든 연결은 사용 가능한 네트워크 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-111">All connections to that VPN gateway share the available network bandwidth.</span></span>

<span data-ttu-id="f015d-112">각 가상 네트워크 게이트웨이 내에는 두 개 이상의 VM(가상 머신)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-112">Within each virtual network gateway are two or more virtual machines (VMs).</span></span> <span data-ttu-id="f015d-113">이러한 VM은 _게이트웨이 서브넷_이라는 지정된 특별한 서브넷에 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-113">These VMs have been deployed to a special subnet that you specify, called the _gateway subnet_.</span></span> <span data-ttu-id="f015d-114">특정 게이트웨이 서비스와 함께 다른 네트워크에 대한 연결의 라우팅 테이블이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-114">They contain routing tables for connections to other networks, along with specific gateway services.</span></span> <span data-ttu-id="f015d-115">이러한 VM 및 게이트웨이 서브넷은 강화된 네트워크 장치와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-115">These VMs and the gateway subnet are similar to a hardened network device.</span></span> <span data-ttu-id="f015d-116">이러한 VM을 직접 구성할 필요가 없으며 게이트웨이 서브넷에 추가 리소스를 배포하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-116">You don't need to configure these VMs directly and should not deploy any additional resources into the gateway subnet.</span></span>

<span data-ttu-id="f015d-117">가상 네트워크 게이트웨이 생성을 완료하는 데 시간이 걸릴 수 있으므로 적절하게 계획해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-117">Creating a virtual network gateway can take some time to complete, so it's vital that you plan appropriately.</span></span> <span data-ttu-id="f015d-118">가상 네트워크 게이트웨이를 만들 때 프로비전 프로세스는 게이트웨이 VM을 생성하고 게이트웨이 서브넷에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-118">When you create a virtual network gateway, the provisioning process generates the gateway VMs and deploys them to the gateway subnet.</span></span> <span data-ttu-id="f015d-119">이러한 VM에는 게이트웨이를 구성하는 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-119">These VMs will have the settings that you configure on the gateway.</span></span>

<span data-ttu-id="f015d-120">키 설정은 **_게이트웨이 형식_** 이며 VPN Gateway의 경우 "vpn" 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-120">A key setting is the **_gateway type_**, which for a VPN gateway will be of type "vpn".</span></span> <span data-ttu-id="f015d-121">VPN Gateway에 대한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-121">Options for VPN gateways include:</span></span>

- <span data-ttu-id="f015d-122">IPsec/IKE VPN 터널링을 통한 VNET 간 연결은 VPN Gateway를 다른 VPN Gateway에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-122">VNET to VNET connections over IPsec/IKE VPN tunneling, linking VPN gateways to other VPN gateways.</span></span>

- <span data-ttu-id="f015d-123">교차 프레미스 IPsec/IKE VPN 터널링은 사이트 간 연결을 만드는 전용 VPN 장치를 통해 온-프레미스 네트워크를 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-123">Cross-premises IPsec/IKE VPN tunneling, for connecting on-premises networks to Azure through dedicated VPN devices to create site-to-site connections.</span></span>

- <span data-ttu-id="f015d-124">IKEv2 또는 SSTP를 통한 지점 및 사이트 간 연결은 Azure의 리소스에 클라이언트 컴퓨터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-124">Point to Site connections over IKEv2 or SSTP, to link client computers to resources in Azure.</span></span>

<span data-ttu-id="f015d-125">이제 VPN Gateway를 계획하는 데 고려해야 할 요인을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-125">Now, let's look at the factors you need to consider for planning your VPN gateway.</span></span>

## <a name="plan-a-vpn-gateway"></a><span data-ttu-id="f015d-126">VPN Gateway 계획</span><span class="sxs-lookup"><span data-stu-id="f015d-126">Plan a VPN Gateway</span></span>

<span data-ttu-id="f015d-127">VPN Gateway를 계획할 때 고려해야 하는 세 가지 아키텍처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-127">When planning a VPN gateway, there are three architectures that we need to consider:</span></span>

- <span data-ttu-id="f015d-128">인터넷을 통한 지점 및 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-128">Point to site over the Internet</span></span>
- <span data-ttu-id="f015d-129">인터넷을 통한 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-129">Site to site over the Internet</span></span>
- <span data-ttu-id="f015d-130">Azure ExpressRoute와 같은 전용 네트워크를 통한 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-130">Site to site over a dedicated network, such as Azure ExpressRoute</span></span>

### <a name="planning-factors"></a><span data-ttu-id="f015d-131">계획 요소</span><span class="sxs-lookup"><span data-stu-id="f015d-131">Planning Factors</span></span>

<span data-ttu-id="f015d-132">계획 프로세스 중에 처리해야 하는 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-132">Factors that you need to cover during your planning process include:</span></span>

- <span data-ttu-id="f015d-133">처리량 - Mbps 또는 Gbps</span><span class="sxs-lookup"><span data-stu-id="f015d-133">Throughput - Mbps or Gbps</span></span>
- <span data-ttu-id="f015d-134">백본 - 인터넷 또는 개인?</span><span class="sxs-lookup"><span data-stu-id="f015d-134">Backbone - Internet or private?</span></span>
- <span data-ttu-id="f015d-135">공용(정적) IP 주소의 가용성</span><span class="sxs-lookup"><span data-stu-id="f015d-135">Availability of a public (static) IP address</span></span>
- <span data-ttu-id="f015d-136">VPN 장치 호환성</span><span class="sxs-lookup"><span data-stu-id="f015d-136">VPN device compatibility</span></span>
- <span data-ttu-id="f015d-137">여러 클라이언트 연결 또는 사이트 간 연결?</span><span class="sxs-lookup"><span data-stu-id="f015d-137">Multiple client connections or a site-to-site link?</span></span>
- <span data-ttu-id="f015d-138">VPN Gateway 형식</span><span class="sxs-lookup"><span data-stu-id="f015d-138">VPN gateway type</span></span>
- <span data-ttu-id="f015d-139">Azure VPN Gateway SKU</span><span class="sxs-lookup"><span data-stu-id="f015d-139">Azure VPN Gateway SKU</span></span>

<span data-ttu-id="f015d-140">다음 표에서는 이러한 계획 문제 중 일부를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-140">The following table summarizes some of these planning issues.</span></span> <span data-ttu-id="f015d-141">나머지는 나중에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-141">The remainder are discussed later.</span></span>

|                           |  <span data-ttu-id="f015d-142">지점 및 사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-142">Point-to-Site</span></span>            | <span data-ttu-id="f015d-143">사이트 간 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-143">Site-to-site</span></span>                          |  <span data-ttu-id="f015d-144">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f015d-144">ExpressRoute</span></span>                 |
| -------------             | -------------             | -------------                         | ---------                     |
| <span data-ttu-id="f015d-145">Azure 지원 서비스</span><span class="sxs-lookup"><span data-stu-id="f015d-145">Azure supported services</span></span>  | <span data-ttu-id="f015d-146">Cloud Services 및 VM</span><span class="sxs-lookup"><span data-stu-id="f015d-146">Cloud services and VMs</span></span>    | <span data-ttu-id="f015d-147">Cloud Services 및 VM</span><span class="sxs-lookup"><span data-stu-id="f015d-147">Cloud services and VMs</span></span>                | <span data-ttu-id="f015d-148">지원되는 모든 서비스</span><span class="sxs-lookup"><span data-stu-id="f015d-148">All supported services</span></span>        |
| <span data-ttu-id="f015d-149">일반적인 대역폭</span><span class="sxs-lookup"><span data-stu-id="f015d-149">Typical Bandwidth</span></span>         | <span data-ttu-id="f015d-150">게이트웨이 SKU에 따름</span><span class="sxs-lookup"><span data-stu-id="f015d-150">Depends on Gateway SKU</span></span>    | <span data-ttu-id="f015d-151">집계를 사용하여 최대 1Gbps</span><span class="sxs-lookup"><span data-stu-id="f015d-151">Up to 1 Gbps with aggregation</span></span>         | <span data-ttu-id="f015d-152">50Mbps에서 10Gbps 사이</span><span class="sxs-lookup"><span data-stu-id="f015d-152">From 50 Mbps to 10 Gbps</span></span>       |
| <span data-ttu-id="f015d-153">지원되는 프로토콜</span><span class="sxs-lookup"><span data-stu-id="f015d-153">Protocols supported</span></span>       | <span data-ttu-id="f015d-154">SSTP 및 IPSec</span><span class="sxs-lookup"><span data-stu-id="f015d-154">SSTP and IPSec</span></span>            | <span data-ttu-id="f015d-155">IPSec</span><span class="sxs-lookup"><span data-stu-id="f015d-155">IPSec</span></span>                                 | <span data-ttu-id="f015d-156">직접 연결, VLAN</span><span class="sxs-lookup"><span data-stu-id="f015d-156">Direct connection, VLANs</span></span>      |
| <span data-ttu-id="f015d-157">라우팅</span><span class="sxs-lookup"><span data-stu-id="f015d-157">Routing</span></span>                   | <span data-ttu-id="f015d-158">RouteBased(동적)</span><span class="sxs-lookup"><span data-stu-id="f015d-158">RouteBased (dynamic)</span></span>      | <span data-ttu-id="f015d-159">PolicyBased (정적) 및 RouteBased</span><span class="sxs-lookup"><span data-stu-id="f015d-159">PolicyBased (static) and RouteBased</span></span>   | <span data-ttu-id="f015d-160">BGP</span><span class="sxs-lookup"><span data-stu-id="f015d-160">BGP</span></span>                           |
| <span data-ttu-id="f015d-161">연결 복원력</span><span class="sxs-lookup"><span data-stu-id="f015d-161">Connection resiliency</span></span>     | <span data-ttu-id="f015d-162">활성-수동</span><span class="sxs-lookup"><span data-stu-id="f015d-162">active-passive</span></span>            | <span data-ttu-id="f015d-163">활성-수동 또는 활성-활성</span><span class="sxs-lookup"><span data-stu-id="f015d-163">active-passive or active-active</span></span>       | <span data-ttu-id="f015d-164">활성-활성</span><span class="sxs-lookup"><span data-stu-id="f015d-164">active-active</span></span>                 |
| <span data-ttu-id="f015d-165">사용 사례</span><span class="sxs-lookup"><span data-stu-id="f015d-165">Use case</span></span>                  | <span data-ttu-id="f015d-166">테스트 및 프로토타입</span><span class="sxs-lookup"><span data-stu-id="f015d-166">Testing and prototyping</span></span>   | <span data-ttu-id="f015d-167">개발, 테스트 및 소규모 프로덕션</span><span class="sxs-lookup"><span data-stu-id="f015d-167">Dev, test and small-scale production</span></span>  | <span data-ttu-id="f015d-168">엔터프라이즈/중요 업무용</span><span class="sxs-lookup"><span data-stu-id="f015d-168">Enterprise/Mission Critical</span></span>   |

### <a name="gateway-skus"></a><span data-ttu-id="f015d-169">게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="f015d-169">Gateway SKUs</span></span>

<span data-ttu-id="f015d-170">Azure는 게이트웨이 서비스에 대해 다음과 같은 SKU를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-170">Azure offers the following SKUs for gateway services:</span></span>

| <span data-ttu-id="f015d-171">SKU</span><span class="sxs-lookup"><span data-stu-id="f015d-171">SKU</span></span>              |  <span data-ttu-id="f015d-172">S2S/VNet 간 터널</span><span class="sxs-lookup"><span data-stu-id="f015d-172">S2S/VNet-to-VNet Tunnels</span></span> | <span data-ttu-id="f015d-173">P2S 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-173">P2S Connections</span></span>  |  <span data-ttu-id="f015d-174">집계 처리량 벤치마크</span><span class="sxs-lookup"><span data-stu-id="f015d-174">Aggregate Throughput Benchmark</span></span>   | <span data-ttu-id="f015d-175">용도</span><span class="sxs-lookup"><span data-stu-id="f015d-175">Use for</span></span>                         |
| -------------    | -------------             | -------------    | ---------                         | ---------                       |
| <span data-ttu-id="f015d-176">기본</span><span class="sxs-lookup"><span data-stu-id="f015d-176">Basic</span></span>            | <span data-ttu-id="f015d-177">최댓값 10</span><span class="sxs-lookup"><span data-stu-id="f015d-177">Max 10</span></span>                    | <span data-ttu-id="f015d-178">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="f015d-178">Max 128</span></span>          | <span data-ttu-id="f015d-179">100Mbps</span><span class="sxs-lookup"><span data-stu-id="f015d-179">100 Mbps</span></span>                          | <span data-ttu-id="f015d-180">개발/테스트/POC</span><span class="sxs-lookup"><span data-stu-id="f015d-180">Dev/test/POC</span></span>                    |
| <span data-ttu-id="f015d-181">VpnGw1</span><span class="sxs-lookup"><span data-stu-id="f015d-181">VpnGw1</span></span>           | <span data-ttu-id="f015d-182">최댓값 30</span><span class="sxs-lookup"><span data-stu-id="f015d-182">Max 30</span></span>                    | <span data-ttu-id="f015d-183">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="f015d-183">Max 128</span></span>          | <span data-ttu-id="f015d-184">650Mbps</span><span class="sxs-lookup"><span data-stu-id="f015d-184">650 Mbps</span></span>                          | <span data-ttu-id="f015d-185">프로덕션/중요 워크로드</span><span class="sxs-lookup"><span data-stu-id="f015d-185">Production/Critical workloads</span></span>   |
| <span data-ttu-id="f015d-186">VpnGw2</span><span class="sxs-lookup"><span data-stu-id="f015d-186">VpnGw2</span></span>           | <span data-ttu-id="f015d-187">최댓값 30</span><span class="sxs-lookup"><span data-stu-id="f015d-187">Max 30</span></span>                    | <span data-ttu-id="f015d-188">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="f015d-188">Max 128</span></span>          | <span data-ttu-id="f015d-189">1Gbps</span><span class="sxs-lookup"><span data-stu-id="f015d-189">1 Gbps</span></span>                            | <span data-ttu-id="f015d-190">프로덕션/중요 워크로드</span><span class="sxs-lookup"><span data-stu-id="f015d-190">Production/Critical workloads</span></span>   |
| <span data-ttu-id="f015d-191">VpnGw3</span><span class="sxs-lookup"><span data-stu-id="f015d-191">VpnGw3</span></span>           | <span data-ttu-id="f015d-192">최댓값 30</span><span class="sxs-lookup"><span data-stu-id="f015d-192">Max 30</span></span>                    | <span data-ttu-id="f015d-193">최댓값 128</span><span class="sxs-lookup"><span data-stu-id="f015d-193">Max 128</span></span>          | <span data-ttu-id="f015d-194">1.25Gbps</span><span class="sxs-lookup"><span data-stu-id="f015d-194">1.25Gbps</span></span>                          | <span data-ttu-id="f015d-195">프로덕션/중요 워크로드</span><span class="sxs-lookup"><span data-stu-id="f015d-195">Production/Critical workloads</span></span>   |

> [!Note] 
> <span data-ttu-id="f015d-196">올바른 SKU를 선택해야 합니다. 잘못된 SKU를 사용하여 VPN Gateway를 설정한 경우 중지하고 게이트웨이를 다시 빌드해야 합니다. 그러려면 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-196">It's important that you choose the right SKU, if you have set up your VPN gateway with the wrong one, you'll have to take it down and rebuild the gateway, which can be time consuming</span></span>

## <a name="workflow"></a><span data-ttu-id="f015d-197">워크플로</span><span class="sxs-lookup"><span data-stu-id="f015d-197">Workflow</span></span>

<span data-ttu-id="f015d-198">Azure에서 가상 사설망을 사용하여 클라우드 연결 전략을 설계할 때 다음과 같은 워크플로를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-198">When designing a cloud connectivity strategy using virtual private networking on Azure, you should apply the following workflow:</span></span>

1. <span data-ttu-id="f015d-199">연결 토폴로지를 디자인하면서 연결된 모든 네트워크의 주소 공간을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-199">Design your connectivity topology, listing the address spaces for all connecting networks.</span></span>

1. <span data-ttu-id="f015d-200">Azure Virtual Network를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-200">Create an Azure virtual network.</span></span>

1. <span data-ttu-id="f015d-201">가상 네트워크의 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-201">Create a VPN gateway for the virtual network.</span></span>

1. <span data-ttu-id="f015d-202">필요에 따라 온-프레미스 네트워크 또는 기타 가상 네트워크에 대한 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-202">Create and configure connections to on-premises networks or other virtual networks, as required.</span></span>

1. <span data-ttu-id="f015d-203">필요에 따라 Azure VPN Gateway에 대한 지점 및 사이트 간 연결을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-203">If required, create and configure a Point-to-Site connection for your Azure VPN gateway.</span></span>

### <a name="design-considerations"></a><span data-ttu-id="f015d-204">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f015d-204">Design Considerations</span></span>

<span data-ttu-id="f015d-205">가상 네트워크를 연결하도록 VPN Gateway를 디자인할 때 다음과 같은 요인을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-205">When you design your VPN gateways to connect virtual networks, you must consider the following factors:</span></span>

- <span data-ttu-id="f015d-206">서브넷은 중복될 수 없습니다. 하나의 위치에 있는 서브넷에는 다른 위치와 동일한 주소 공간이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-206">Subnets cannot overlap   It is vital that a subnet in one location does not contain the same address space as in another location.</span></span>

- <span data-ttu-id="f015d-207">IP 주소는 고유해야 합니다. 다른 위치에서 동일한 IP 주소를 가진 두 호스트가 있을 수 없습니다. 해당하는 두 호스트 간에 트래픽을 라우팅할 수 없고 VNET 간 연결에 실패하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-207">IP addresses must be unique    You cannot have two hosts with the same IP address in different locations, as it will be impossible to route traffic between those two hosts and the VNET to VNET connection will fail.</span></span>

- <span data-ttu-id="f015d-208">VPN Gateway에는 **GatewaySubnet**라는 게이트웨이 서브넷이 필요합니다. 게이트웨이에서 이 이름이 작동해야 하고 다른 리소스를 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-208">VPN Gateways need a gateway subnet called **GatewaySubnet** It must have this name for the gateway to work and it should not contain any other resources.</span></span>

### <a name="create-an-azure-virtual-network"></a><span data-ttu-id="f015d-209">Azure Virtual Network 만들기</span><span class="sxs-lookup"><span data-stu-id="f015d-209">Create an Azure Virtual Network</span></span>

<span data-ttu-id="f015d-210">VPN Gateway를 만들기 전에 Azure vNet을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-210">Before you create a VPN gateway, you need to create the Azure vNet.</span></span>

### <a name="create-a-vpn-gateway"></a><span data-ttu-id="f015d-211">VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="f015d-211">Create a VPN Gateway</span></span>

<span data-ttu-id="f015d-212">만든 VPN Gateway 형식은 아키텍처에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-212">The type of VPN gateway you create will depend on your architecture.</span></span> <span data-ttu-id="f015d-213">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-213">Options are:</span></span>

- <span data-ttu-id="f015d-214">RouteBased 경로 기반 VPN 장치는 임의(와일드 카드) 트래픽 선택기를 사용하며, 라우팅/전달 테이블이 다른 IPsec 터널에 트래픽을 전달하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-214">RouteBased Route-based VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="f015d-215">경로 기반 연결은 일반적으로 각 IPsec 터널이 네트워크 인터페이스 또는 VTI(가상 터널 인터페이스)로 모델링되는 라우터 플랫폼에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-215">Route-based connections are typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

- <span data-ttu-id="f015d-216">PolicyBased 정책 기반 VPN 장치는 두 네트워크의 접두사 조합을 사용하여 트래픽이 IPsec 터널을 통해 암호화/암호 해독되는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-216">PolicyBased Policy-based VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="f015d-217">정책 기반 연결은 일반적으로 패킷 필터링을 수행하는 방화벽 장치에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-217">A policy-based connection is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="f015d-218">IPsec 터널 암호화 및 암호 해독이 패킷 필터링 및 처리 엔진에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-218">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>

## <a name="set-up-a-vpn-gateway"></a><span data-ttu-id="f015d-219">VPN Gateway 설정</span><span class="sxs-lookup"><span data-stu-id="f015d-219">Set up a VPN Gateway</span></span>

<span data-ttu-id="f015d-220">수행해야 하는 단계는 설치하는 VPN Gateway의 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-220">The steps you need to take will depend on the type of VPN gateway that you are installing.</span></span> <span data-ttu-id="f015d-221">예를 들어, Azure Portal을 사용하여 지점 및 사이트 간 VPN Gateway를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-221">For example, to create a Point-to-Site VPN gateway by using the Azure portal, you would carry out the following steps:</span></span>

1. <span data-ttu-id="f015d-222">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f015d-222">Create a virtual network</span></span>

2. <span data-ttu-id="f015d-223">게이트웨이 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="f015d-223">Add a gateway subnet</span></span>

3. <span data-ttu-id="f015d-224">DNS 서버 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="f015d-224">Specify a DNS server (optional)</span></span>

4. <span data-ttu-id="f015d-225">가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="f015d-225">Create a virtual network gateway</span></span>

5. <span data-ttu-id="f015d-226">인증서 생성</span><span class="sxs-lookup"><span data-stu-id="f015d-226">Generate certificates</span></span>

6. <span data-ttu-id="f015d-227">클라이언트 주소 풀 추가</span><span class="sxs-lookup"><span data-stu-id="f015d-227">Add the client address pool</span></span>

7. <span data-ttu-id="f015d-228">터널 형식 구성</span><span class="sxs-lookup"><span data-stu-id="f015d-228">Configure tunnel type</span></span>

8. <span data-ttu-id="f015d-229">인증 형식 구성</span><span class="sxs-lookup"><span data-stu-id="f015d-229">Configure authentication type</span></span>

9. <span data-ttu-id="f015d-230">루트 인증서 공용 인증서 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="f015d-230">Upload the root certificate public certificate data</span></span>

10. <span data-ttu-id="f015d-231">내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="f015d-231">Install an exported client certificate</span></span>

11. <span data-ttu-id="f015d-232">VPN 클라이언트 구성 패키지 생성 및 설치</span><span class="sxs-lookup"><span data-stu-id="f015d-232">Generate and install the VPN client configuration package</span></span>

12. <span data-ttu-id="f015d-233">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="f015d-233">Connect to Azure</span></span>

<span data-ttu-id="f015d-234">각각 여러 옵션을 포함하여 Azure VPN Gateway를 사용하는 여러 구성 경로가 있으므로 이 과정에서 모든 설정을 다룰 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-234">As there are several configuration paths with Azure VPN Gateways, each with multiple options, it is not possible to cover every setup in this course.</span></span> <span data-ttu-id="f015d-235">자세한 내용은 추가 리소스 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f015d-235">For more information, see the Additional Resources section.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="f015d-236">게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="f015d-236">Configure the gateway</span></span>

<span data-ttu-id="f015d-237">게이트웨이가 만들어지면 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-237">Once your gateway is created, you'll need to configure it.</span></span>  <span data-ttu-id="f015d-238">이름, 위치, DNS 서버 등과 같은 것을 제공해야 하는 여러 구성 설정이 있습니다. 자세한 내용은 연습에서 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-238">There are several configuration settings you will need to provide such as the name, location, DNS server, etc. We will go into these in more detail in the exercise.</span></span>

## <a name="summary"></a><span data-ttu-id="f015d-239">요약</span><span class="sxs-lookup"><span data-stu-id="f015d-239">Summary</span></span>

<span data-ttu-id="f015d-240">Azure VPN Gateway는 지점 및 사이트 간, 사이트 간 또는 vnet 간 연결을 사용하도록 설정한 Azure vNet의 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-240">Azure VPN Gateways are a component in Azure vNets that enable point-to-site, site-to-site, or vnet-to-vnet connections.</span></span> <span data-ttu-id="f015d-241">Azure VPN Gateway를 사용하면 개별 클라이언트 컴퓨터가 Azure의 리소스에 연결하거나, Azure로 온-프레미스 네트워크를 확장하거나, 다른 지역 및 구독의 vNet 간에 연결을 용이하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015d-241">Azure VPN Gateways enable individual client computers to connect to resources in Azure, extend on-premises networks into Azure, or facilitate connections between vNets in different regions and subscriptions.</span></span>