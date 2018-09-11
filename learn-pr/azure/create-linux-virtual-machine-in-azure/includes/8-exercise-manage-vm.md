<span data-ttu-id="addea-101">HTTP 트래픽만 서버를 통과할 수 있도록 네트워크에 네트워크 보안 그룹을 적용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-101">Let's apply a Network Security Group to our network so that we only allow HTTP traffic through our server.</span></span>

## <a name="create-a-network-security-group"></a><span data-ttu-id="addea-102">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="addea-102">Create a network security group</span></span>

<span data-ttu-id="addea-103">SSH 액세스를 원하는 것으로 지정했으므로 실제로는 Azure에서 보안 그룹이 자동으로 생성되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="addea-103">Azure should have created a security group for us because we indicated we wanted SSH access.</span></span> <span data-ttu-id="addea-104">하지만 전체 프로세스를 진행할 수 있도록 새 보안 그룹을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-104">But let's create a new security group so you can walk through the entire process.</span></span> <span data-ttu-id="addea-105">이 작업은 VM에 _앞서_ 가상 네트워크를 만들기로 결정한 경우 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-105">This is particularly important if you decide to create your virtual network _before_ your VMs.</span></span> <span data-ttu-id="addea-106">앞서 설명한 것처럼, 보안 그룹은 _선택 사항_이며 네트워크를 사용하여 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-106">As mentioned earlier, security groups are _optional_ and not necessarily created with the network.</span></span>

1. <span data-ttu-id="addea-107">[Azure Portal](https://portal.azure.com?azure-portal=true)의 왼쪽 모서리 세로 막대에서 **리소스 만들기** 단추를 클릭하여 새 리소스 생성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-107">In the [Azure portal](https://portal.azure.com?azure-portal=true), click the **Create a resource** button in the left corner sidebar to start a new resource creation.</span></span>

1. <span data-ttu-id="addea-108">필터 상자에 "네트워크 보안 그룹"을 입력하고 목록에서 일치하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-108">Type "Network security group" into the filter box and select the matching item in the list.</span></span>

1. <span data-ttu-id="addea-109">**Resource Manager** 배포 모델을 선택했는지 확인하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-109">Make sure the **Resource Manager** deployment model is selected and click **Create**.</span></span>

1. <span data-ttu-id="addea-110">보안 그룹의 **이름**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-110">Provide a **Name** for your security group.</span></span> <span data-ttu-id="addea-111">여기서도 명명 규칙을 적용하면 효율적이므로 "미국 동부의 웹 네트워크 보안 그룹 #1 테스트"에 "test-web-eus-nsg1"을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-111">Again, naming conventions are a good idea here, let's use "test-web-eus-nsg1" for "Test Web Network Security Group #1 in East US".</span></span> <span data-ttu-id="addea-112">이름의 위치 부분은 대개 보안 그룹을 배치할 위치를 반영하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-112">You'll likely want to change the location portion of the to reflect where you put the security group.</span></span>

1. <span data-ttu-id="addea-113">적절한 **구독**을 선택하고 기존 **리소스 그룹**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-113">Select the proper **Subscription** and use your existing **Resource group**.</span></span>

1. <span data-ttu-id="addea-114">마지막으로 VM/Virtual Network로 동일한 **위치**에 리소스를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-114">Finally, put it into the same **Location** as the VM / Virtual Network.</span></span> <span data-ttu-id="addea-115">이 작업이 중요한 것은 이 리소스가 다른 위치에 있는 경우 적용할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="addea-115">This is important; you won't be able to apply this resource if it's in a different location.</span></span>

1. <span data-ttu-id="addea-116">**만들기**를 클릭하여 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="addea-116">Click **Create** to create the group.</span></span>

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a><span data-ttu-id="addea-117">네트워크 보안 그룹에 새 인바운드 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="addea-117">Add a new inbound rule to our Network Security Group</span></span>

<span data-ttu-id="addea-118">배포는 빠르게 완료됩니다. 배포가 완료되면 보안 그룹에 새 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-118">Deployment should complete quickly, when it's finished we can add new rules to our security group.</span></span>

1. <span data-ttu-id="addea-119">새 보안 그룹 리소스를 찾아 Azure Portal에서 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-119">Find the new security group resource and select it in the Azure portal.</span></span>

1. <span data-ttu-id="addea-120">개요 페이지에서 네트워크를 잠그기 위해 만든 몇 가지 기본 규칙을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-120">On the overview page, you'll find that it has some default rules created to lock down the network.</span></span>

    <span data-ttu-id="addea-121">인바운드 쪽.</span><span class="sxs-lookup"><span data-stu-id="addea-121">On the inbound side:</span></span>

    - <span data-ttu-id="addea-122">서로 다른 VNet 간의 모든 들어오는 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-122">All incoming traffic from one VNet to another is allowed.</span></span> <span data-ttu-id="addea-123">이렇게 하면 VNet의 리소스 간에 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-123">This lets resources on the VNet talk to each other</span></span>
    - <span data-ttu-id="addea-124">Azure Load Balancer "프로브"가 VM이 활성화 상태인지 확인 요청</span><span class="sxs-lookup"><span data-stu-id="addea-124">Azure Load balancer "probe" requests to ensure the VM is alive</span></span>
    - <span data-ttu-id="addea-125">기타 모든 인바운드 트래픽은 아웃바운드 쪽에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-125">All other inbound traffic is denied On the outbound side:</span></span>
    - <span data-ttu-id="addea-126">VNet에서 모든 네트워크 내 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-126">All in-network traffic on the VNet is allowed</span></span>
    - <span data-ttu-id="addea-127">인터넷으로의 모든 아웃바운드 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-127">All outbound traffic to the Internet is permitted</span></span>
    - <span data-ttu-id="addea-128">기타 모든 아웃바운드 트래픽은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-128">All other outbound traffic is denied</span></span>

> [!NOTE]
> <span data-ttu-id="addea-129">이러한 기본 규칙은 우선 순위가 높은 값으로 설정됩니다. 즉, 해당 기본 규칙은 _마지막_으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-129">These default rules are set with high priority values, which means that they get evaluated _last_.</span></span> <span data-ttu-id="addea-130">기본 규칙을 변경하거나 삭제할 수 없지만 사용자 트래픽을 우선 순위가 낮은 값과 일치하도록 보다 구체적인 규칙을 만들어 기본 규칙을 _재정의_할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-130">They cannot be changed or deleted, but you can _override_ them by creating more specific rules to match your traffic with a lower priority value.</span></span>

1. <span data-ttu-id="addea-131">보안 그룹에 대한 **설정** 패널에서 **인바운드 보안 규칙** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-131">Click the **Inbound security rules** section in the **Settings** panel for the security group.</span></span>

1. <span data-ttu-id="addea-132">**+ 추가**를 클릭하여 새 보안 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-132">Click **+ Add** to add a new security rule.</span></span>

    ![보안 규칙 추가](../media-drafts/8-add-rule.png)

    <span data-ttu-id="addea-134">보안 규칙에 필요한 정보를 입력하는 방법은 기본 및 고급 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-134">There are two ways to enter the information necessary for a security rule: basic and advanced.</span></span> <span data-ttu-id="addea-135">"추가" 패널의 맨 위에 있는 단추를 클릭하여 두 가지 방법 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-135">You can switch between them by clicking the button at the top of the "add" panel.</span></span>

    ![기본 및 고급 규칙 입력](../media-drafts/8-advanced-create-rule.png)

    <span data-ttu-id="addea-137">고급 모드는 규칙을 완전히 사용자 지정할 수 있는 기능을 제공하지만, 알려진 프로토콜을 구성해야 하는 경우 기본 모드가 사용하기에 조금 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-137">The advanced mode provides the ability to customize the rule completely, however, if you need to configure a known protocol, the basic mode is a bit easier to work with.</span></span>

1. <span data-ttu-id="addea-138">기본 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-138">Switch to the Basic mode.</span></span>

1. <span data-ttu-id="addea-139">HTTP 규칙에 대한 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-139">Add the information for our HTTP rule.</span></span>

    - <span data-ttu-id="addea-140">**서비스**를 HTTP로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-140">Set the **Service** to be HTTP.</span></span> <span data-ttu-id="addea-141">그러면 포트 범위가 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-141">This will set your port range up for you.</span></span>
    - <span data-ttu-id="addea-142">**우선 순위**을 "1000"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-142">Set the **Priority** to "1000".</span></span> <span data-ttu-id="addea-143">우선 순위 값은 기본 **거부** 규칙보다 작은 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-143">It has to be a lower number than the default **Deny** rule.</span></span> <span data-ttu-id="addea-144">모든 값에서 범위를 시작할 수 있지만 나중에 예외를 만들어야 할 경우에 대비해 약간의 여유를 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-144">You can start the range at any value, but it's recommended you give yourself some space in case an exception needs to be created later.</span></span>
    - <span data-ttu-id="addea-145">규칙 이름을 “allow-http-traffic”으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-145">Give the rule a name; we'll use "allow-http-traffic".</span></span>
    - <span data-ttu-id="addea-146">규칙에 설명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-146">Give the rule a description.</span></span>

1. <span data-ttu-id="addea-147">**고급** 모드로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-147">Switch back to the **Advanced** mode.</span></span> <span data-ttu-id="addea-148">해당 설정이 아직 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-148">Notice that our settings are still present.</span></span> <span data-ttu-id="addea-149">이 패널을 사용하여 더 세분화된 설정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-149">We can use this panel to create more fine-grained settings.</span></span> <span data-ttu-id="addea-150">특히 **원본**을 특정 IP 주소 또는 카메라 관련 IP 주소 범위로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-150">In particular, we would likely restrict the **Source** to be a specific IP address or range of IP addresses specific to the cameras.</span></span> <span data-ttu-id="addea-151">로컬 컴퓨터의 현재 IP 주소를 알고 있는 경우 해당 제한을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-151">If you know the current IP address of your local computer, you can try that.</span></span> <span data-ttu-id="addea-152">그렇지 않은 경우 설정을 "모두"로 두고 규칙을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-152">Otherwise, leave the setting as "Any" so you can test the rule.</span></span>

1. <span data-ttu-id="addea-153">**추가**를 클릭하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="addea-153">Click **Add** to create the rule.</span></span> <span data-ttu-id="addea-154">이렇게 하면 우선 순위에 따라 인바운드 규칙 목록을 업데이트해서 해당 규칙을 검사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="addea-154">This will update the list of inbound rules - notice they are in priority order, which is how they will be examined.</span></span>
    
## <a name="apply-the-security-group"></a><span data-ttu-id="addea-155">보안 그룹 적용</span><span class="sxs-lookup"><span data-stu-id="addea-155">Apply the security group</span></span>

<span data-ttu-id="addea-156">단일 VM을 보호하기 위한 네트워크 인터페이스에 또는 서브넷의 모든 리소스에 적용되는 해당 서브넷에 보안 그룹을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-156">Recall that we can apply the security group to a network interface to guard a single VM, or to a subnet where it would apply to any resources on that subnet.</span></span> <span data-ttu-id="addea-157">후자 방법이 가장 일반적인 것 같아 해당 작업을 수행하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-157">The latter approach tends to be the most common so let's do that.</span></span> <span data-ttu-id="addea-158">가상 네트워크 리소스를 통하거나 간접적으로 가상 네트워크를 사용하는 VM을 통해 Azure에서 이 리소스를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-158">We could get to this resource in Azure through either the virtual network resource or indirectly through the VM which is using the virtual network.</span></span>

1. <span data-ttu-id="addea-159">가상 머신에 대한 **개요** 패널로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-159">Switch to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="addea-160">VM은 **모든 리소스** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-160">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="addea-161">**설정** 섹션에서 **네트워킹** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-161">Select the **Networking** item in the **Settings** section.</span></span>

    ![VM 설정의 네트워킹 항목](../media-drafts/8-network-settings.png)

1. <span data-ttu-id="addea-163">네트워킹 속성에서는 **가상 네트워크/서브넷**(리소스로 이동하는 클릭 가능한 링크)을 포함하여 VM에 적용된 네트워킹에 대한</span><span class="sxs-lookup"><span data-stu-id="addea-163">In the networking properties, you will find information about the networking applied to the VM including the **Virtual network/subnet**.</span></span> <span data-ttu-id="addea-164">정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-164">This is a clickable link to get to the resource.</span></span> <span data-ttu-id="addea-165">이 링크를 클릭하여 가상 네트워크를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="addea-165">Click it to open the virtual network.</span></span> <span data-ttu-id="addea-166">이 링크는 VM의 **개요** 패널에서 사용할 수_도_ 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-166">This link is _also_ available on the **Overview** panel of the VM.</span></span> <span data-ttu-id="addea-167">이러한 링크 중 하나를 클릭하면 가상 네트워크의 **개요**가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="addea-167">Either of these will open the **Overview** of the virtual network.</span></span>

1. <span data-ttu-id="addea-168">**설정** 섹션에서 **서브넷** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-168">In the **Settings** section, select the **Subnets** item.</span></span>

1. <span data-ttu-id="addea-169">앞서 VM + 네트워크를 만들었을 때부터 서브넷 하나(기본값)가 정의되어 있는 상태였어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-169">We should have a single subnet defined (default) from when we created the VM + network earlier.</span></span> <span data-ttu-id="addea-170">세부 정보를 열려면 목록에서 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-170">Click the item in the list to open the details.</span></span>

1. <span data-ttu-id="addea-171">**네트워크 보안 그룹** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-171">Click the **Network security group** entry.</span></span>

1. <span data-ttu-id="addea-172">새 보안 그룹 **test-web-eus-nsg1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-172">Select your new security group: **test-web-eus-nsg1**.</span></span> <span data-ttu-id="addea-173">VM과 함께 만든 다른 그룹도 여기에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-173">There should be another group here as well that was created with the VM.</span></span>

1. <span data-ttu-id="addea-174">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-174">Click **Save** to save the change.</span></span> <span data-ttu-id="addea-175">변경 내용을 네트워크에 적용하려면 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="addea-175">It will take a minute to apply to the network.</span></span>

## <a name="verify-the-rules"></a><span data-ttu-id="addea-176">규칙 확인</span><span class="sxs-lookup"><span data-stu-id="addea-176">Verify the rules</span></span>

<span data-ttu-id="addea-177">변경 내용의 유효성을 검사해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-177">Let's validate the change.</span></span>

1. <span data-ttu-id="addea-178">가상 머신의 **개요** 패널로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-178">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="addea-179">VM은 **모든 리소스** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-179">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="addea-180">**설정** 섹션에서 **네트워킹** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-180">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="addea-181">네트워크의 **개요** 패널에는 규칙을 평가하는 방법을 간략하게 확인할 수 있는 **효과적인 보안 규칙**의 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-181">In the **Overview** panel for the network, there is a link for **Effective security rules** that will quickly show you how rules are going to be evaluated.</span></span> <span data-ttu-id="addea-182">링크를 클릭하여 분석을 열고 새 규칙이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-182">Click the link to open the analysis and make sure you see your new rule.</span></span>

    ![네트워크에 대한 효과적인 보안 규칙](../media-drafts/8-effective-rules.png)

1. <span data-ttu-id="addea-184">물론 규칙이 모두 작동하는지 유효성을 검사하는 가장 좋은 방법은 서버에 대해 HTTP 요청을 실행해 보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="addea-184">Of course, the best way to validate it's all working is to hit our server with an HTTP request.</span></span> <span data-ttu-id="addea-185">해당 요청이 여전히 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-185">It should still work.</span></span> <span data-ttu-id="addea-186">**HTTP** 규칙을 삭제하여 보안 그룹 규칙이 적용되는지를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-186">You can even delete the **HTTP** rule to verify that the security group rules are now being applied.</span></span>

## <a name="one-more-thing"></a><span data-ttu-id="addea-187">추가 사항</span><span class="sxs-lookup"><span data-stu-id="addea-187">One more thing</span></span>

<span data-ttu-id="addea-188">보안 규칙은 올바로 이해하기가 까다롭습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-188">Security rules are tricky to get right.</span></span> <span data-ttu-id="addea-189">이 새 보안 그룹을 적용할 때 실수를 저질러 SSH에 액세스할 수 없게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-189">We made a mistake when we applied this new security group - we lost our SSH access!</span></span> <span data-ttu-id="addea-190">이 문제를 해결하려는 경우 보안 그룹에 다른 규칙을 추가하여 SSH 액세스를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-190">To fix this, you can add another rule to the security group to support SSH access.</span></span> <span data-ttu-id="addea-191">규칙에 대한 인바운드 TCP/IP 주소를 소유하는 주소로 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-191">Make sure to restrict the inbound TCP/IP addresses for the rule to be the ones you own.</span></span>

> [!WARNING]
> <span data-ttu-id="addea-192">항상 관리 액세스에 사용되는 포트를 잠그도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-192">Always make sure to lock down ports used for administrative access.</span></span> <span data-ttu-id="addea-193">더 나은 방법은 개인 네트워크에 가상 네트워크를 연결하고 해당 주소 범위에서 RDP 또는 SSH 요청만 허용하는 VPN을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="addea-193">An even better approach is to create a VPN to link the virtual network to your private network and only allow RDP or SSH requests from that address range.</span></span> <span data-ttu-id="addea-194">또한 SSH에서 사용하는 포트를 기본값 이외의 포트로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="addea-194">You can also change the port used by SSH to be something other than the default.</span></span> <span data-ttu-id="addea-195">포트 변경으로는 공격을 중지하는 데 충분하지 않으므로 검색을 조금 더 어렵게 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="addea-195">Keep in mind that changing ports is not sufficient to stop attacks, it simply makes it a little harder to discover.</span></span>