<span data-ttu-id="131f3-101">Woodgrove Bank에서 근무하면서 온라인 뱅킹 서비스를 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-101">Recall that you work for Woodgrove Bank, and that you are about to launch online banking services.</span></span> <span data-ttu-id="131f3-102">이 부문은 경쟁이 치열하므로 99.99% 이상의 서비스 가용성을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-102">This sector is highly competitive, so you need to guarantee of a minimum of 99.99% service availability.</span></span> <span data-ttu-id="131f3-103">세 개의 가상 머신으로 구성된 풀이 포함된 Azure Load Balancer를 통해 이 목표를 달성할 수 있다고 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-103">You have determined that Azure Load Balancer with a pool of three virtual machines will meet this goal.</span></span>

<span data-ttu-id="131f3-104">이 연습에서는 Azure Portal을 사용하여 부하 분산 장치 및 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-104">In this exercise, you will create a load balancer and a virtual network using the Azure portal.</span></span> <span data-ttu-id="131f3-105">이들 중 하나만 필요하므로 포털을 통해 이를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-105">Since we only need one of these, the portal is an easy way to create it.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-public-load-balancer"></a><span data-ttu-id="131f3-106">공용 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="131f3-106">Create a public load balancer</span></span>

1. <span data-ttu-id="131f3-107">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-107">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="131f3-108">사이드바에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-108">In the sidebar, click **Create a resource**.</span></span>

1. <span data-ttu-id="131f3-109">**네트워킹** 섹션을 클릭한 다음, **Load Balancer**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-109">Select the **Networking** section, and then click **Load Balancer**.</span></span> <span data-ttu-id="131f3-110">해당 선택이 항목에 표시되지 않으면 검색 상자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-110">If you don't see that choice, you can use the search box.</span></span>

    ![선택된 네트워킹 섹션 및 강조 표시된 부하 분산 장치를 사용하여 Azure Marketplace를 보여 주는 스크린샷](../media/3-azure-marketplace.png)

1. <span data-ttu-id="131f3-112">**부하 분산 장치 만들기** 블레이드에서 다음 정보를 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-112">In the **Create load balancer** blade, enter or select the following information:</span></span>
    - <span data-ttu-id="131f3-113">**이름:** _woodgrove-LB_</span><span class="sxs-lookup"><span data-stu-id="131f3-113">**Name:** _woodgrove-LB_</span></span>
    - <span data-ttu-id="131f3-114">**유형:** _공용_</span><span class="sxs-lookup"><span data-stu-id="131f3-114">**Type:** _Public_</span></span>
    - <span data-ttu-id="131f3-115">**SKU:** _기본_</span><span class="sxs-lookup"><span data-stu-id="131f3-115">**SKU:** _Basic_</span></span>
    - <span data-ttu-id="131f3-116">**공용 IP 주소:** **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-116">**Public IP address:** Select **Create new**.</span></span> <span data-ttu-id="131f3-117">텍스트 상자에 _woodgrove-LB-ip_를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-117">In the text box, type _woodgrove-LB-ip_.</span></span> <span data-ttu-id="131f3-118">할당을 _동적_으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-118">Leave the Assignment as _Dynamic_.</span></span>
    - <span data-ttu-id="131f3-119">**구독:** 선택된 _컨시어지 구독_이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-119">**Subscription:** It should already have _Concierge Subscription_ selected.</span></span>
    - <span data-ttu-id="131f3-120">**리소스 그룹:** **기존 리소스 그룹 사용**을 선택하고 _<rgn>[샌드박스 리소스 그룹 이름]</rgn>_ 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-120">**Resource group:** Select **Use existing** and choose _<rgn>[sandbox resource group name]</rgn>_.</span></span>
    - <span data-ttu-id="131f3-121">**위치:** 다음 목록에서 사용자에게 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-121">**Location:** Select a region near you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    ![새 Load Balancer 만들기 화면을 보여 주는 스크린샷](../media/3-create-load-balancer.png)

1. <span data-ttu-id="131f3-123">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-123">Click **Create**.</span></span>

<span data-ttu-id="131f3-124">부하 분산 장치 리소스를 만들고 배포하는 동안 백 엔드 서브넷에 사용할 Azure Virtual Network를 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-124">While the load balancer resource is being created and deployed, let's create the Azure Virtual Network we'll use for the backend subnet.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="131f3-125">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="131f3-125">Create a virtual network</span></span>

1. <span data-ttu-id="131f3-126">왼쪽 메뉴에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-126">In the left menu, click **Create a resource**.</span></span> <span data-ttu-id="131f3-127">**새로 만들기** 블레이드에서 **네트워킹** 및 **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-127">In the **New** blade, click **Networking**, and then click **Virtual network**.</span></span>

    ![선택된 네트워킹 섹션 및 강조 표시된 부하 분산 장치를 사용하여 Azure Marketplace를 보여 주는 스크린샷](../media/3-azure-marketplace-2.png)

1. <span data-ttu-id="131f3-129">**가상 네트워크 만들기** 블레이드에서 다음 정보를 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-129">In the **Create virtual network** blade, enter or select the following information:</span></span>
    - <span data-ttu-id="131f3-130">**이름:** _woodgrove-VNET_</span><span class="sxs-lookup"><span data-stu-id="131f3-130">**Name:** _woodgrove-VNET_</span></span>
    - <span data-ttu-id="131f3-131">**주소 공간:** _172.20.0.0/16_</span><span class="sxs-lookup"><span data-stu-id="131f3-131">**Address space:** _172.20.0.0/16_</span></span>
    - <span data-ttu-id="131f3-132">**구독:** 선택된 _컨시어지 구독_이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-132">**Subscription:** It should already have _Concierge Subscription_ selected.</span></span>
    - <span data-ttu-id="131f3-133">**리소스 그룹:** 목록에서 기존 _<rgn>[리소스 그룹 이름]</rgn>_ 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-133">**Resource group:** Select the existing _<rgn>[Resource Group Name]</rgn>_ resource group from the list.</span></span>
    - <span data-ttu-id="131f3-134">**서브넷 이름:** _backendSubnet_</span><span class="sxs-lookup"><span data-stu-id="131f3-134">**Subnet name:** _backendSubnet_</span></span>
    - <span data-ttu-id="131f3-135">**서브넷 주소 범위:** _172.20.0.0/24_</span><span class="sxs-lookup"><span data-stu-id="131f3-135">**Subnet address range:** _172.20.0.0/24_</span></span>
    - <span data-ttu-id="131f3-136">**DDoS 보호:** _기본_</span><span class="sxs-lookup"><span data-stu-id="131f3-136">**DDoS protection:** _Basic_</span></span>
    - <span data-ttu-id="131f3-137">**서비스 엔드포인트:** _사용 안 함_</span><span class="sxs-lookup"><span data-stu-id="131f3-137">**Service endpoints:** _Disabled_</span></span>

    ![새 Load Balancer 만들기 화면을 보여 주는 스크린샷](../media/3-create-vnet.png)

1. <span data-ttu-id="131f3-139">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-139">Click **Create**.</span></span>

<span data-ttu-id="131f3-140">가상 네트워크를 배포하는 동안 네트워크 보안 그룹을 하나 더 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-140">While the virtual network is being deployed, let's create one more thing: a network security group.</span></span>

## <a name="create-and-configure-a-network-security-group"></a><span data-ttu-id="131f3-141">네트워크 보안 그룹 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="131f3-141">Create and configure a network security group</span></span>

1. <span data-ttu-id="131f3-142">**리소스 만들기** 클릭</span><span class="sxs-lookup"><span data-stu-id="131f3-142">Click **Create a resource**</span></span>

1. <span data-ttu-id="131f3-143">**네트워킹** 그룹을 선택하고 **네트워크 보안 그룹** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-143">Select the **Networking** group, and Click on the **Network security group** item.</span></span>

    ![선택된 네트워킹 섹션 및 강조 표시된 네트워크 보안 그룹을 사용하여 Azure Marketplace를 보여 주는 스크린샷](../media/3-azure-marketplace-3.png)


1. <span data-ttu-id="131f3-145">보안 그룹의 이름을 **woodgrove-NSG**로 지정하고 Azure 샌드박스 리소스 그룹에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-145">Give it the name **woodgrove-NSG** and put it into the Azure sandbox resource group.</span></span>

1. <span data-ttu-id="131f3-146">보안 그룹이 Azure Load Balancer와 같은 위치에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-146">Make sure it's in the same location as the Azure Load Balancer.</span></span>

    ![네트워크 보안 그룹 만들기 화면을 보여 주는 스크린샷](../media/3-create-nsg.png)

1. <span data-ttu-id="131f3-148">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-148">Click **Create**.</span></span>

<span data-ttu-id="131f3-149">부하 분산 장치, 가상 네트워크 및 NSG이 배포될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-149">Wait until the load balancer, virtual network, and NSG are deployed.</span></span> <span data-ttu-id="131f3-150">그러면 네트워크 보안을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-150">Then we can configure the network security.</span></span>

## <a name="configure-the-network-security-group"></a><span data-ttu-id="131f3-151">NSG(네트워크 보안 그룹) 구성</span><span class="sxs-lookup"><span data-stu-id="131f3-151">Configure the network security group</span></span>

1. <span data-ttu-id="131f3-152">Azure Portal의 맨 위에 있는 검색 표시줄을 통해 또는 배포 알림에서 새 네트워크 보안 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-152">Select your new network security group - either from the deployment notification, or through the search bar at the top of the Azure portal.</span></span>

    ![알림 패널에서 배포 성공을 보여 주는 스크린샷](../media/3-deployment-success.png)

1. <span data-ttu-id="131f3-154">**설정** > **인바운드 보안 규칙** 섹션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-154">Select the **Settings** > **Inbound security rules** section.</span></span> <span data-ttu-id="131f3-155">항상 적용되는 세 개의 미리 정의된 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-155">Notice that we have three pre-defined rules that are always applied.</span></span> <span data-ttu-id="131f3-156">이러한 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-156">These rules are:</span></span>
    - <span data-ttu-id="131f3-157">**AllowVnetInbound** - 가상 네트워크에서 모든 내부 트래픽 흐름을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-157">**AllowVnetInbound** - Allow all internal traffic flowing on the virtual network.</span></span> <span data-ttu-id="131f3-158">이 규칙은 상호 통신을 위해 네트워크를 공유하는 VM을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-158">This rule allows VMs that share the network to talk to each other.</span></span>
    - <span data-ttu-id="131f3-159">**AllowAzureLoadBalancerInBound** - 서비스가 활성화돼 있는지 여부를 확인하려면 부하 분산 장치가 네트워크에서 서비스를 "ping"하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-159">**AllowAzureLoadBalancerInBound** - Allow the load balancer to "ping" services on the network to see whether they are alive.</span></span>
    - <span data-ttu-id="131f3-160">**DenyAllInbound** - 다른 모든 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-160">**DenyAllInbound** - Deny all other traffic.</span></span>

    <span data-ttu-id="131f3-161">**DenyAllInbound** 규칙은 높은 우선 순위 규칙이 없는 모든 인바운드 트래픽이 차단되는지 확인하므로 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-161">The **DenyAllInbound** rule is particularly important - it ensures that all inbound traffic that doesn't have a higher priority rule is blocked.</span></span> <span data-ttu-id="131f3-162">그래서 웹 서버에 대한 HTTP(80) 트래픽을 허용하는 새 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-162">That's why we will need to add a new rule to allow HTTP (80) traffic for our web servers.</span></span>

    > [!NOTE]
    > <span data-ttu-id="131f3-163">NSG 규칙에서 우선 순위는 0 - 65500까지 이동하며 규칙은 순서대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-163">Priority in NSG rules goes from 0 - 65500 and rules are evaluated in order.</span></span> <span data-ttu-id="131f3-164">처음으로 일치하는 규칙이 의사 결정권자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-164">The first matching rule becomes the decision maker.</span></span> <span data-ttu-id="131f3-165">항상 규칙을 약 1000부터 시작하여 상당히 낮게 배치하려 하므로 해당 규칙은 미리 정의된 규칙에 대해 우선권이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-165">You will always want to place your rules fairly low - starting around 1000 so they take precedence over the pre-defined ones.</span></span>

1. <span data-ttu-id="131f3-166">**추가**를 클릭하여 새 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-166">Click **Add** to add a new rule.</span></span>

    ![추가 단추가 강조 표시된 인바운드 네트워크 보안 규칙을 보여주는 스크린샷](../media/3-inbound-security-rules.png)

1. <span data-ttu-id="131f3-168">"기본" 보기로 전환하려면 맨 위의 **기본** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-168">Click the **Basic** button at the top to switch the the "basic" view.</span></span>

1. <span data-ttu-id="131f3-169">새 규칙에 대한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-169">Fill in the details for the new rule.</span></span>
    - <span data-ttu-id="131f3-170">**서비스**에 대한 _HTTP_를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-170">Select _HTTP_ for the **Service**.</span></span>
    - <span data-ttu-id="131f3-171">**우선 순위**를 _1000_으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-171">Set the **Priority** to _1000_.</span></span>
    - <span data-ttu-id="131f3-172">규칙의 이름을 지정합니다(또는 기본값을 그대로 둡니다).</span><span class="sxs-lookup"><span data-stu-id="131f3-172">Give the rule a name (or leave the default).</span></span>

    ![HTTP 세부 정보를 사용하여 입력된 인바운드 보안 규칙 추가 대화 상자를 보여 주는 스크린샷](../media/3-add-inbound-rule.png)

1. <span data-ttu-id="131f3-174">**추가**를 클릭하여 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-174">Click **Add** to add the rule.</span></span>

    ![NSG 규칙 목록에서 새로 추가된 HTTP 규칙을 보여 주는 스크린샷](../media/3-new-added-rule.png)

## <a name="apply-the-network-security-group-to-the-vnet"></a><span data-ttu-id="131f3-176">네트워크 보안 그룹을 VNet에 적용</span><span class="sxs-lookup"><span data-stu-id="131f3-176">Apply the network security group to the VNet</span></span>

<span data-ttu-id="131f3-177">다음으로, 가상 네트워크에 이 NSG를 적용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-177">Next, let's apply this NSG to the virtual network.</span></span>

1. <span data-ttu-id="131f3-178">가상 네트워크를 발견하면 맨 위의 검색 상자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-178">Find your virtual network - you can use the search box at the top.</span></span> <span data-ttu-id="131f3-179">이 가상 네트워크는 **woodgrove-VNET**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-179">It's named **woodgrove-VNET**.</span></span>

1. <span data-ttu-id="131f3-180">**설정** > **서브넷**을 선택하여 정의된 서브넷으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-180">Select **Settings** > **Subnets** to get to your defined subnets.</span></span>

1. <span data-ttu-id="131f3-181">**backendSubnet** 항목을 클릭하여 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-181">Click the **backendSubnet** entry to open the properties.</span></span>

    ![서브넷의 서브넷 영역에서 backendSubnet 항목을 보여 주는 스크린샷](../media/3-subnets.png)

1. <span data-ttu-id="131f3-183">**네트워크 보안 그룹**에서 “없음” 항목을 클릭</span><span class="sxs-lookup"><span data-stu-id="131f3-183">Click the "None" entry on the **Network security group**</span></span>

    ![backendSubnet의 빈 네트워크 보안을 보여 주는 스크린샷](../media/3-add-network-security-group.png)

1. <span data-ttu-id="131f3-185">**woodgrove-NSG**를 선택하여 이 VNET에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-185">Select the **woodgrove-NSG** to add it to this VNET.</span></span>

1. <span data-ttu-id="131f3-186">**저장** 을 클릭하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-186">Click **Save** to apply the change.</span></span>

<span data-ttu-id="131f3-187">이제 네트워크 준비됐으므로 이 네트워크에 위치할 일부 가상 머신을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="131f3-187">Now that our network is ready, let's create some virtual machines to sit on this network!</span></span>