<span data-ttu-id="a3508-101">HTTP 트래픽만 서버를 통과할 수 있도록 네트워크에 네트워크 보안 그룹을 적용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-101">Let's apply a Network Security Group to our network so that we only allow HTTP traffic through our server.</span></span>

## <a name="create-a-network-security-group"></a><span data-ttu-id="a3508-102">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a3508-102">Create a network security group</span></span>

<span data-ttu-id="a3508-103">SSH 액세스가 필요하다고 지정했으니, Azure에서 보안 그룹이 생성되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-103">Azure should have created a security group for us because we indicated we wanted SSH access.</span></span> <span data-ttu-id="a3508-104">하지만 전체 프로세스를 수행할 수 있도록 새 보안 그룹을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-104">But let's create a new security group so you can walk through the entire process.</span></span> <span data-ttu-id="a3508-105">이 작업은 VM에 _앞서_ 가상 네트워크를 만들려는 경우 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-105">This is particularly important if you decide to create your virtual network _before_ your VMs.</span></span> <span data-ttu-id="a3508-106">앞서 설명한 것처럼, 보안 그룹은 _선택 사항_이며 반드시 네트워크를 통해 만들어야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-106">As mentioned earlier, security groups are _optional_ and not necessarily created with the network.</span></span>

1. <span data-ttu-id="a3508-107">[Azure Portal](https://portal.azure.com?azure-portal=true)의 왼쪽 모서리 사이드바에서 **리소스 만들기** 단추를 클릭하여 새 리소스 생성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-107">In the [Azure portal](https://portal.azure.com?azure-portal=true), click the **Create a resource** button in the left corner sidebar to start a new resource creation.</span></span>

1. <span data-ttu-id="a3508-108">필터 상자에 "네트워크 보안 그룹"을 입력하고 목록에서 일치하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-108">Type "Network security group" into the filter box and select the matching item in the list.</span></span>

1. <span data-ttu-id="a3508-109">**Resource Manager** 배포 모델이 선택되었는지 확인하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-109">Make sure the **Resource Manager** deployment model is selected and click **Create**.</span></span>

1. <span data-ttu-id="a3508-110">보안 그룹에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-110">Provide a **Name** for your security group.</span></span> <span data-ttu-id="a3508-111">여기서도 명명 규칙을 적용하면 효율적이므로 "미국 동부의 웹 네트워크 보안 그룹 #1 테스트"에 "test-web-eus-nsg1"을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-111">Again, naming conventions are a good idea here, let's use "test-web-eus-nsg1" for "Test Web Network Security Group #1 in East US".</span></span> <span data-ttu-id="a3508-112">이름의 위치 부분은 보안 그룹을 배치할 위치를 반영하도록 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-112">You'll likely want to change the location portion of the to reflect where you put the security group.</span></span>

1. <span data-ttu-id="a3508-113">적절한 **구독**을 선택하고 기존 **리소스 그룹**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-113">Select the proper **Subscription** and use your existing **Resource group**.</span></span>

1. <span data-ttu-id="a3508-114">마지막으로 VM/Virtual Network와 동일한 **위치**에 리소스를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-114">Finally, put it into the same **Location** as the VM / Virtual Network.</span></span> <span data-ttu-id="a3508-115">이 작업이 중요한 것은 이 리소스가 다른 위치에 있는 경우 적용할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-115">This is important; you won't be able to apply this resource if it's in a different location.</span></span>

1. <span data-ttu-id="a3508-116">**만들기**를 클릭하여 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-116">Click **Create** to create the group.</span></span>

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a><span data-ttu-id="a3508-117">네트워크 보안 그룹에 새 인바운드 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="a3508-117">Add a new inbound rule to our Network Security Group</span></span>

<span data-ttu-id="a3508-118">배포는 빠르게 완료됩니다. 배포가 완료되면 보안 그룹에 새 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-118">Deployment should complete quickly, when it's finished we can add new rules to our security group.</span></span>

1. <span data-ttu-id="a3508-119">새 보안 그룹 리소스를 찾고 Azure Portal에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-119">Find the new security group resource and select it in the Azure portal.</span></span>

1. <span data-ttu-id="a3508-120">개요 페이지에서 네트워크를 잠글 수 있도록 만든 몇 가지 기본 규칙을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-120">On the overview page, you'll find that it has some default rules created to lock down the network.</span></span>

    <span data-ttu-id="a3508-121">인바운드 쪽:</span><span class="sxs-lookup"><span data-stu-id="a3508-121">On the inbound side:</span></span>

    - <span data-ttu-id="a3508-122">하나의 VNet에서 다른 VNet으로 들어오는 모든 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-122">All incoming traffic from one VNet to another is allowed.</span></span> <span data-ttu-id="a3508-123">따라서 VNet의 리소스 간에 서로 통신이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-123">This lets resources on the VNet talk to each other</span></span>
    - <span data-ttu-id="a3508-124">VM이 활성 상태인지 확인하기 위한 Azure Load Balancer "프로브" 요청</span><span class="sxs-lookup"><span data-stu-id="a3508-124">Azure Load balancer "probe" requests to ensure the VM is alive</span></span>
    - <span data-ttu-id="a3508-125">기타 모든 인바운드 트래픽은 아웃바운드 쪽에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-125">All other inbound traffic is denied On the outbound side:</span></span>
    - <span data-ttu-id="a3508-126">VNet에서 모든 네트워크 내 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-126">All in-network traffic on the VNet is allowed</span></span>
    - <span data-ttu-id="a3508-127">인터넷으로 나가는 모든 아웃바운드 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-127">All outbound traffic to the Internet is permitted</span></span>
    - <span data-ttu-id="a3508-128">기타 모든 아웃바운드 트래픽은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-128">All other outbound traffic is denied</span></span>

> [!NOTE]
> <span data-ttu-id="a3508-129">기본 규칙은 우선 순위 값이 높게 설정됩니다. 즉, 평가가 _마지막_으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-129">These default rules are set with high priority values, which means that they get evaluated _last_.</span></span> <span data-ttu-id="a3508-130">변경하거나 삭제할 수는 없지만 트래픽이 우선 순위가 낮은 값과 일치하도록 구체적인 규칙을 더 만들어서 _재정의_할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-130">They cannot be changed or deleted, but you can _override_ them by creating more specific rules to match your traffic with a lower priority value.</span></span>

1. <span data-ttu-id="a3508-131">보안 그룹에 대한 **설정** 패널에서 **인바운드 보안 규칙** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-131">Click the **Inbound security rules** section in the **Settings** panel for the security group.</span></span>

1. <span data-ttu-id="a3508-132">**+ 추가**를 클릭하여 새 보안 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-132">Click **+ Add** to add a new security rule.</span></span>

    ![보안 규칙 추가](../media-drafts/8-add-rule.png)

    <span data-ttu-id="a3508-134">보안 규칙에 필요한 정보를 입력하는 방법에는 기본 및 고급 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-134">There are two ways to enter the information necessary for a security rule: basic and advanced.</span></span> <span data-ttu-id="a3508-135">"추가" 패널의 맨 위에 있는 단추를 클릭하여 두 가지 방법을 서로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-135">You can switch between them by clicking the button at the top of the "add" panel.</span></span>

    ![기본 및 고급 규칙 입력](../media-drafts/8-advanced-create-rule.png)

    <span data-ttu-id="a3508-137">고급 모드는 규칙을 완전히 사용자 지정할 수 있는 기능을 제공하지만, 알려진 프로토콜을 구성해야 하는 경우 기본 모드가 사용하기에 조금 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-137">The advanced mode provides the ability to customize the rule completely, however, if you need to configure a known protocol, the basic mode is a bit easier to work with.</span></span>

1. <span data-ttu-id="a3508-138">기본 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-138">Switch to the Basic mode.</span></span>

1. <span data-ttu-id="a3508-139">HTTP 규칙에 대한 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-139">Add the information for our HTTP rule.</span></span>

    - <span data-ttu-id="a3508-140">**서비스**를 HTTP로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-140">Set the **Service** to be HTTP.</span></span> <span data-ttu-id="a3508-141">그러면 포트 범위가 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-141">This will set your port range up for you.</span></span>
    - <span data-ttu-id="a3508-142">**우선 순위**를 "1000"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-142">Set the **Priority** to "1000".</span></span> <span data-ttu-id="a3508-143">이 값은 기본 **거부** 규칙보다 작은 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-143">It has to be a lower number than the default **Deny** rule.</span></span> <span data-ttu-id="a3508-144">범위는 어떤 값으로든 시작할 수 있지만 나중에 예외를 만들어야 할 경우에 대비해 약간의 여유를 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-144">You can start the range at any value, but it's recommended you give yourself some space in case an exception needs to be created later.</span></span>
    - <span data-ttu-id="a3508-145">규칙에 이름을 지정합니다. 여기에서는 “allow-http-traffic”으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-145">Give the rule a name; we'll use "allow-http-traffic".</span></span>
    - <span data-ttu-id="a3508-146">규칙에 설명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-146">Give the rule a description.</span></span>

1. <span data-ttu-id="a3508-147">**고급** 모드로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-147">Switch back to the **Advanced** mode.</span></span> <span data-ttu-id="a3508-148">설정이 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-148">Notice that our settings are still present.</span></span> <span data-ttu-id="a3508-149">이 패널을 사용하여 보다 세분화된 설정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-149">We can use this panel to create more fine-grained settings.</span></span> <span data-ttu-id="a3508-150">특히 **원본**을 특정 IP 주소 또는 카메라 관련 IP 주소 범위로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-150">In particular, we would likely restrict the **Source** to be a specific IP address or range of IP addresses specific to the cameras.</span></span> <span data-ttu-id="a3508-151">로컬 컴퓨터의 현재 IP 주소를 아는 경우에는 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-151">If you know the current IP address of your local computer, you can try that.</span></span> <span data-ttu-id="a3508-152">그렇지 않으면 규칙을 테스트할 수 있도록 설정을 "임의"로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-152">Otherwise, leave the setting as "Any" so you can test the rule.</span></span>

1. <span data-ttu-id="a3508-153">**추가**를 클릭하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-153">Click **Add** to create the rule.</span></span> <span data-ttu-id="a3508-154">그러면 인바운드 규칙 목록이 업데이트되고 우선 순위가 결정됩니다. 이것은 규칙이 어떻게 검사될지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-154">This will update the list of inbound rules - notice they are in priority order, which is how they will be examined.</span></span>
    
## <a name="apply-the-security-group"></a><span data-ttu-id="a3508-155">보안 그룹 적용</span><span class="sxs-lookup"><span data-stu-id="a3508-155">Apply the security group</span></span>

<span data-ttu-id="a3508-156">네트워크 인터페이스에 보안 그룹을 적용하여 단일 VM이나 서브넷(서브넷의 모든 리소스에 적용됨)을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-156">Recall that we can apply the security group to a network interface to guard a single VM, or to a subnet where it would apply to any resources on that subnet.</span></span> <span data-ttu-id="a3508-157">후자의 접근 방식이 가장 일반적이므로 후자를 수행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-157">The latter approach tends to be the most common so let's do that.</span></span> <span data-ttu-id="a3508-158">Azure에서 가상 네트워크 리소스를 통해 또는 가상 네트워크를 사용하는 VM을 통해 간접적으로 이 리소스를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-158">We could get to this resource in Azure through either the virtual network resource or indirectly through the VM which is using the virtual network.</span></span>

1. <span data-ttu-id="a3508-159">가상 머신에 대한 **개요** 패널로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-159">Switch to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="a3508-160">VM은 **모든 리소스** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-160">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="a3508-161">**설정** 섹션에서 **네트워킹** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-161">Select the **Networking** item in the **Settings** section.</span></span>

    ![VM 설정의 네트워킹 항목](../media-drafts/8-network-settings.png)

1. <span data-ttu-id="a3508-163">네트워킹 속성에서는 **가상 네트워크/서브넷**를 포함하는 VM에 적용되는 네트워킹에 대한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-163">In the networking properties, you will find information about the networking applied to the VM including the **Virtual network/subnet**.</span></span> <span data-ttu-id="a3508-164">이것은 리소스로 이동되는 클릭 가능한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-164">This is a clickable link to get to the resource.</span></span> <span data-ttu-id="a3508-165">이 링크를 클릭하여 가상 네트워크를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-165">Click it to open the virtual network.</span></span> <span data-ttu-id="a3508-166">이 링크는 VM의 **개요** 패널_에서도_ 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-166">This link is _also_ available on the **Overview** panel of the VM.</span></span> <span data-ttu-id="a3508-167">두 가지 링크 중 하나를 클릭하면 가상 네트워크의 **개요**가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-167">Either of these will open the **Overview** of the virtual network.</span></span>

1. <span data-ttu-id="a3508-168">**설정** 섹션에서 **서브넷** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-168">In the **Settings** section, select the **Subnets** item.</span></span>

1. <span data-ttu-id="a3508-169">앞에서 VM + 네트워크를 만들었을 때 단일 서브넷(기본값)이 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-169">We should have a single subnet defined (default) from when we created the VM + network earlier.</span></span> <span data-ttu-id="a3508-170">목록에서 해당 항목을 클릭하여 세부 정보를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-170">Click the item in the list to open the details.</span></span>

1. <span data-ttu-id="a3508-171">**네트워크 보안 그룹** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-171">Click the **Network security group** entry.</span></span>

1. <span data-ttu-id="a3508-172">새 보안 그룹인 **test-web-eus-nsg1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-172">Select your new security group: **test-web-eus-nsg1**.</span></span> <span data-ttu-id="a3508-173">VM으로 만든 다른 그룹도 여기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-173">There should be another group here as well that was created with the VM.</span></span>

1. <span data-ttu-id="a3508-174">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-174">Click **Save** to save the change.</span></span> <span data-ttu-id="a3508-175">네트워크에 적용하는 데 1분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-175">It will take a minute to apply to the network.</span></span>

## <a name="verify-the-rules"></a><span data-ttu-id="a3508-176">규칙 확인</span><span class="sxs-lookup"><span data-stu-id="a3508-176">Verify the rules</span></span>

<span data-ttu-id="a3508-177">변경 내용의 유효성을 검사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-177">Let's validate the change.</span></span>

1. <span data-ttu-id="a3508-178">가상 머신의 **개요** 패널로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-178">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="a3508-179">VM은 **모든 리소스** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-179">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="a3508-180">**설정** 섹션에서 **네트워킹** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-180">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="a3508-181">네트워크의 **개요** 패널에는 규칙이 평가되는 방법이 간략하게 표시되는 **효과적인 보안 규칙** 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-181">In the **Overview** panel for the network, there is a link for **Effective security rules** that will quickly show you how rules are going to be evaluated.</span></span> <span data-ttu-id="a3508-182">링크를 클릭하여 분석을 열고 새 규칙이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-182">Click the link to open the analysis and make sure you see your new rule.</span></span>

    ![네트워크에 유효한 보안 규칙](../media-drafts/8-effective-rules.png)

1. <span data-ttu-id="a3508-184">물론, 규칙이 모두 작동하는지 검사하는 가장 좋은 방법은 서버에 HTTP 요청을 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-184">Of course, the best way to validate it's all working is to hit our server with an HTTP request.</span></span> <span data-ttu-id="a3508-185">계속 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-185">It should still work.</span></span> <span data-ttu-id="a3508-186">**HTTP** 규칙을 삭제하여 보안 그룹 규칙이 적용되고 있는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-186">You can even delete the **HTTP** rule to verify that the security group rules are now being applied.</span></span>

## <a name="one-more-thing"></a><span data-ttu-id="a3508-187">추가 사항</span><span class="sxs-lookup"><span data-stu-id="a3508-187">One more thing</span></span>

<span data-ttu-id="a3508-188">제대로 이해하기 까다로운 보안 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-188">Security rules are tricky to get right.</span></span> <span data-ttu-id="a3508-189">이 보안 그룹을 새로 적용하면서 실수가 있어서 SSH에 액세스할 수 없게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-189">We made a mistake when we applied this new security group - we lost our SSH access!</span></span> <span data-ttu-id="a3508-190">이 문제를 해결하려면 보안 그룹에 SSH 액세스를 지원하는 다른 규칙을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-190">To fix this, you can add another rule to the security group to support SSH access.</span></span> <span data-ttu-id="a3508-191">규칙에 대한 인바운드 TCP/IP 주소를 소유하는 주소로 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-191">Make sure to restrict the inbound TCP/IP addresses for the rule to be the ones you own.</span></span>

> [!WARNING]
> <span data-ttu-id="a3508-192">관리 액세스에 사용되는 포트는 항상 잠가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-192">Always make sure to lock down ports used for administrative access.</span></span> <span data-ttu-id="a3508-193">더 나은 방법은 개인 네트워크에 가상 네트워크를 연결하고 해당 주소 범위의 RDP 또는 SSH 요청만 허용하도록 VPN을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-193">An even better approach is to create a VPN to link the virtual network to your private network and only allow RDP or SSH requests from that address range.</span></span> <span data-ttu-id="a3508-194">SSH에 사용되는 포트를 기본값 이외의 포트로 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-194">You can also change the port used by SSH to be something other than the default.</span></span> <span data-ttu-id="a3508-195">포트 변경만으로는 공격을 막는 데 충분하지 않습니다. 포트를 변경하면 공격자자 발견하기 조금 더 어려워질 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a3508-195">Keep in mind that changing ports is not sufficient to stop attacks, it simply makes it a little harder to discover.</span></span>