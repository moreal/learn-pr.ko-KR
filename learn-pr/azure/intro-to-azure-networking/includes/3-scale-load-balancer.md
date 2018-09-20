<span data-ttu-id="05704-101">이제 Azure에서 가동되고 실행되는 사이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-101">You now have your site up and running on Azure.</span></span> <span data-ttu-id="05704-102">그러나 사이트가 연중 무휴로 실행되는지 확인하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="05704-102">But how can you help ensure your site is running 24/7?</span></span>

<span data-ttu-id="05704-103">예를 들어 매주 유지 관리를 수행해야 하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="05704-103">For instance, what happens when you need to do weekly maintenance?</span></span> <span data-ttu-id="05704-104">유지 관리 기간 동안에는 서비스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-104">Your service will still be unavailable during your maintenance window.</span></span> <span data-ttu-id="05704-105">그리고 사이트는 전 세계 사용자에게 연결되므로 유지 관리를 위해 시스템을 가동 중지할 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-105">And because your site reaches users all over the world, there's no good time to take down your systems for maintenance.</span></span> <span data-ttu-id="05704-106">또한 너무 많은 사용자가 동시에 연결하면 성능 문제가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-106">You may also run into performance issues if too many users connect at the same time.</span></span>

## <a name="what-are-availability-and-high-availability"></a><span data-ttu-id="05704-107">가용성 및 고가용성이란?</span><span class="sxs-lookup"><span data-stu-id="05704-107">What are availability and high availability?</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="05704-108">![고가용성을 나타내는 속도 학습](../media/3-availability.png)</span><span class="sxs-lookup"><span data-stu-id="05704-108">![A speed train representing high availability](../media/3-availability.png)</span></span>
  :::column-end:::
    <span data-ttu-id="05704-109">:::column span="3"::: _가용성_은 서비스가 중단 없이 가동되어 실행되는 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-109">:::column span="3"::: _Availability_ refers to how long your service is up and running without interruption.</span></span> <span data-ttu-id="05704-110">_고가용성_ 또는 _가용성이 높음_은 오랜 기간 동안 가동되어 실행되는 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-110">_High availability_, or _highly available_, refers to a service that's up and running for a long period of time.</span></span>

<span data-ttu-id="05704-111">필요한 정보에 액세스할 수 없을 때 얼마나 실망하는지 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-111">You know how frustrating it is when you can't access the information you need.</span></span> <span data-ttu-id="05704-112">매일 방문하는 소셜 미디어 또는 뉴스 사이트를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="05704-112">Think of a social media or news site that you visit daily.</span></span> <span data-ttu-id="05704-113">언제든 사이트에 액세스할 수 있거나, "503 서비스를 사용할 수 없음"과 같은 오류 메시지가 자주 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="05704-113">Can you always access the site, or do you often see error messages like "503 Service Unavailable"?</span></span>
  :::column-end:::
 :::row-end:::

<span data-ttu-id="05704-114">“99.999 가용성(five nines availability)”과 같은 용어를 들어본 적이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05704-114">You may have heard terms like "five nines availability."</span></span> <span data-ttu-id="05704-115">99.999 가용성은 전체 시간의 99.999% 동안 서비스가 실행되도록 보장한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="05704-115">Five nines availability means that the service is guaranteed to be running 99.999 percent of the time.</span></span> <span data-ttu-id="05704-116">100% 가용성을 달성하기는 어렵지만, 많은 팀에서 99.999 이상의 가용성을 위해 노력합니다.</span><span class="sxs-lookup"><span data-stu-id="05704-116">Although it's difficult to achieve 100 percent availability, many teams strive for at least five nines.</span></span>

## <a name="what-is-resiliency"></a><span data-ttu-id="05704-117">복원력이란?</span><span class="sxs-lookup"><span data-stu-id="05704-117">What is resiliency?</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="05704-118">![복원력을 나타내는 상태 차트](../media/3-resiliency.png)</span><span class="sxs-lookup"><span data-stu-id="05704-118">![A health chart representing resiliency](../media/3-resiliency.png)</span></span>
  :::column-end:::
    <span data-ttu-id="05704-119">:::column span="3"::: _복원력_은 비정상적인 상태에서도 작동을 유지하는 시스템의 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-119">:::column span="3"::: _Resiliency_ refers to a system's ability to stay operational during abnormal conditions.</span></span>

<span data-ttu-id="05704-120">이러한 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-120">These conditions include:</span></span>

- <span data-ttu-id="05704-121">자연재해</span><span class="sxs-lookup"><span data-stu-id="05704-121">Natural disasters.</span></span>
- <span data-ttu-id="05704-122">계획된 업데이트와 계획되지 않은 시스템 유지 관리(소프트웨어 업데이트 및 보안 패치 포함)</span><span class="sxs-lookup"><span data-stu-id="05704-122">System maintenance, both planned and unplanned, including software updates and security patches.</span></span>
- <span data-ttu-id="05704-123">사이트로의 트래픽 급증</span><span class="sxs-lookup"><span data-stu-id="05704-123">Spikes in traffic to your site.</span></span>
- <span data-ttu-id="05704-124">악의적인 당사자의 위협(예: DDoS(분산 서비스 거부) 공격)</span><span class="sxs-lookup"><span data-stu-id="05704-124">Threats made by malicious parties, such as distributed denial of service, or DDoS, attacks.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="05704-125">마케팅 팀에서 새 비타민 보조 식품을 홍보하기 위해 반짝 할인 행사를 하려 한다고 상상해 보세요.</span><span class="sxs-lookup"><span data-stu-id="05704-125">Imagine your marketing team wants to have a flash sale to promote a new line of vitamin supplements.</span></span> <span data-ttu-id="05704-126">이 기간에 트래픽이 엄청나게 급증할 것으로 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-126">You might expect a huge spike in traffic during this time.</span></span> <span data-ttu-id="05704-127">이 급증은 처리 시스템을 압도함으로써 시스템이 느려지거나 중지되어 사용자를 실망시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-127">This spike could overwhelm your processing system, causing it to slow down or halt, disappointing your users.</span></span> <span data-ttu-id="05704-128">직접 이러한 실망을 경험했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-128">You may have experienced this disappointment for yourself.</span></span> <span data-ttu-id="05704-129">온라인 판매 사이트에 액세스하여 웹 사이트가 응답하지 않은 경우를 발견한 적이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="05704-129">Have you ever tried to access an online sale only to find the website wasn't responding?</span></span>

## <a name="what-is-a-load-balancer"></a><span data-ttu-id="05704-130">부하 분산 장치란?</span><span class="sxs-lookup"><span data-stu-id="05704-130">What is a load balancer?</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="05704-131">![부하 분산을 나타내는 크기 조정](../media/3-lb.png)</span><span class="sxs-lookup"><span data-stu-id="05704-131">![A scale representing load balancing](../media/3-lb.png)</span></span>
  :::column-end:::
    <span data-ttu-id="05704-132">:::column span="3"::: A _부하 분산 장치_는 트래픽을 풀의 각 시스템 간에 균등하게 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="05704-132">:::column span="3"::: A _load balancer_ distributes traffic evenly among each system in a pool.</span></span> <span data-ttu-id="05704-133">부하 분산 장치는 고가용성 및 복원력 모두를 달성하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-133">A load balancer can help you achieve both high availability and resiliency.</span></span>

<span data-ttu-id="05704-134">각 계층에 동일하게 구성된 추가 VM을 추가하여 시작한다고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="05704-134">Say you start by adding additional VMs, each configured identically, to each tier.</span></span> <span data-ttu-id="05704-135">한 시스템이 가동 중지되거나 너무 많은 사용자에게 서비스를 동시에 제공하는 경우에 대비하여 추가 시스템을 준비하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-135">The idea is to have additional systems ready, in case one goes down or is serving too many users at the same time.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="05704-136">여기서 문제는 각 VM에 자체의 IP 주소가 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05704-136">The problem here is that each VM would have its own IP address.</span></span> <span data-ttu-id="05704-137">또한 한 시스템이 가동 중지되거나 사용량이 많은 경우에는 트래픽을 분산시킬 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-137">Plus, you don't have a way to distribute traffic in case one system goes down or is busy.</span></span> <span data-ttu-id="05704-138">사용자에게 하나의 시스템으로 표시되도록 VM을 연결하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="05704-138">How do you connect your VMs so that they appear to the user as one system?</span></span>

<span data-ttu-id="05704-139">대답은 부하 분산 장치를 사용하여 트래픽을 분산시키는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05704-139">The answer is to use a load balancer to distribute traffic.</span></span> <span data-ttu-id="05704-140">부하 분산 장치는 사용자의 진입점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05704-140">The load balancer becomes the entry point to the user.</span></span> <span data-ttu-id="05704-141">사용자는 부하 분산 장치에서 요청을 받기 위해 선택한 시스템을 알지 못하거나 알고 있을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-141">The user doesn't know (or need to know) which system the load balancer chooses to receive the request.</span></span>

<span data-ttu-id="05704-142">다음 그림에서는 부하 분산 장치의 역할을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05704-142">The following illustration shows the role of a load balancer.</span></span>

![3계층 아키텍처의 웹 계층을 보여 주는 그림입니다.](../media/3-load-balancer.png)

<span data-ttu-id="05704-146">사용자의 요청을 받는 부하 분산 장치가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05704-146">You see that the load balancer receives the user's request.</span></span> <span data-ttu-id="05704-147">부하 분산 장치는 웹 계층의 VM 중 하나에 해당 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-147">The load balancer directs the request to one of the VMs in the web tier.</span></span> <span data-ttu-id="05704-148">VM을 사용할 수 없거나 응답을 중지하면 부하 분산 장치에서 트래픽을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-148">If a VM is unavailable or stops responding, the load balancer stops sending traffic to it.</span></span> <span data-ttu-id="05704-149">그런 다음, 부하 분산 장치는 트래픽을 응답성이 뛰어난 서버 중 하나로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-149">The load balancer then directs traffic to one of the responsive servers.</span></span>

<span data-ttu-id="05704-150">부하 분산을 통해 서비스를 중단하지 않고 유지 관리 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-150">Load balancing enables you to run maintenance tasks without interrupting service.</span></span> <span data-ttu-id="05704-151">예를 들어 각 VM에 대한 유지 관리 기간을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-151">For example, you can stagger the maintenance window for each VM.</span></span> <span data-ttu-id="05704-152">유지 관리 기간에 부하 분산 장치는 VM에서 응답하지 않음을 검색하고 풀의 다른 VM으로 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-152">During the maintenance window, the load balancer detects that the VM is unresponsive, and directs traffic to other VMs in the pool.</span></span>

<span data-ttu-id="05704-153">전자상거래 사이트의 경우 앱 및 데이터 계층에 부하 분산 장치가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-153">For your e-commerce site, the app and data tiers can also have a load balancer.</span></span> <span data-ttu-id="05704-154">이러한 구성은 모두 서비스의 요구 사항에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="05704-154">It all depends on what your service requires.</span></span>

## <a name="what-is-azure-load-balancer"></a><span data-ttu-id="05704-155">Azure Load Balancer란?</span><span class="sxs-lookup"><span data-stu-id="05704-155">What is Azure Load Balancer?</span></span>

<span data-ttu-id="05704-156">Azure Load Balancer는 사용자를 위해 유지 관리를 담당하기 위해 Microsoft에서 제공하는 부하 분산 장치 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="05704-156">Azure Load Balancer is a load balancer service that Microsoft provides that helps take care of the maintenance for you.</span></span>

<span data-ttu-id="05704-157">가상 머신에서 일반적인 부하 분산 장치 소프트웨어를 수동으로 구성하는 경우 추가로 시스템을 유지 관리해야 하는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-157">When you manually configure typical load balancer software on a virtual machine, there's a downside: you now have an additional system that you need to maintain.</span></span> <span data-ttu-id="05704-158">부하 분산 장치가 가동 중지되거나 일상적인 유지 관리가 필요한 경우 원래 문제로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="05704-158">If your load balancer goes down or needs routine maintenance, you're back to your original problem.</span></span>

<span data-ttu-id="05704-159">대신 Azure Load Balancer를 사용하는 경우 유지 관리할 인프라 또는 소프트웨어가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-159">If instead, however, you use Azure Load Balancer, there's no infrastructure or software for you to maintain.</span></span>

<span data-ttu-id="05704-160">다음 그림은 다중 계층 아키텍처에서 Azure 부하 분산 장치의 역할을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05704-160">The following illustration shows  the role of Azure load balancers in a multi-tier architecture.</span></span>

![3계층 아키텍처의 웹 계층을 보여 주는 그림입니다.](../media/3-azure-load-balancer.png)

## <a name="what-about-dns"></a><span data-ttu-id="05704-164">DNS는 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="05704-164">What about DNS?</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="05704-165">![DNS를 나타내는 맵 상의 핀](../media/3-map-pin.png)</span><span class="sxs-lookup"><span data-stu-id="05704-165">![A pin on a map representing DNS](../media/3-map-pin.png)</span></span>
  :::column-end:::
    <span data-ttu-id="05704-166">:::column span="3"::: DNS(Domain Name System)는 사용자에게 친숙한 이름을 해당 IP 주소에 매핑하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="05704-166">:::column span="3"::: DNS, or Domain Name System, is a way to map user-friendly names to their IP addresses.</span></span> <span data-ttu-id="05704-167">DNS는 인터넷의 전화번호부라고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-167">You can think of DNS as the phonebook of the internet.</span></span>

<span data-ttu-id="05704-168">예를 들어 contoso.com 도메인 이름은 웹 계층의 부하 분산 장치 IP 주소인 40.65.106.192에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-168">For example, your domain name, contoso.com, might map to the IP address of the load balancer at the web tier, 40.65.106.192.</span></span>

<span data-ttu-id="05704-169">사용자 고유의 DNS 서버를 가져오거나 Azure 인프라에서 실행되는 DNS 도메인에 대한 호스팅 서비스인 Azure DNS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-169">You can bring your own DNS server or use Azure DNS, a hosting service for DNS domains that runs on Azure infrastructure.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="05704-170">다음 그림에서는 Azure DNS를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="05704-170">The following illustration shows Azure DNS.</span></span> <span data-ttu-id="05704-171">사용자가 contoso.com으로 이동하면 Azure DNS에서 트래픽을 부하 분산 장치로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="05704-171">When the user navigates to contoso.com, Azure DNS routes traffic to the load balancer.</span></span>

![부하 분산 장치 앞에 배치된 Azure 도메인 이름 시스템을 보여 주는 그림입니다.](../media/3-dns.png)

## <a name="summary"></a><span data-ttu-id="05704-173">요약</span><span class="sxs-lookup"><span data-stu-id="05704-173">Summary</span></span>

<span data-ttu-id="05704-174">이제 부하 분산을 통해 전자상거래 사이트의 가용성과 복원력이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-174">With load balancing in place, your e-commerce site is now more highly available and resilient.</span></span> <span data-ttu-id="05704-175">유지 관리를 수행하거나 트래픽이 약간 증가할 때 부하 분산 장치에서 트래픽을 사용 가능한 다른 시스템에 분산시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-175">When you perform maintenance or receive an uptick in traffic, your load balancer can distribute traffic to another available system.</span></span>

<span data-ttu-id="05704-176">VM에 사용자 고유의 부하 분산 장치를 구성할 수 있지만, 유지 관리할 인프라 또는 소프트웨어가 없으므로 Azure Load Balancer에서 유지 관리를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="05704-176">Although you can configure your own load balancer on a VM, Azure Load Balancer reduces upkeep because there's no infrastructure or software to maintain.</span></span>

<span data-ttu-id="05704-177">DNS는 사용자에게 친숙한 이름을 해당 IP 주소에 매핑합니다. 이는 전화번호부에서 사람이나 회사의 이름을 전화번호에 매핑하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-177">DNS maps user-friendly names to their IP addresses, much like how a phonebook maps names of people or businesses to phone numbers.</span></span> <span data-ttu-id="05704-178">사용자 고유의 DNS 서버를 가져오거나 Azure DNS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05704-178">You can bring your own DNS server, or use Azure DNS.</span></span>
