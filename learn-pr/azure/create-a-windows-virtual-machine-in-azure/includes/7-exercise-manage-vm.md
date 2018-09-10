<span data-ttu-id="faac1-101">서버가 비디오 데이터를 처리할 준비가 되었습니다. 마지막으로 해야 할 작업은 교통 카메라가 비디오 파일을 서버에 업로드하는 데 사용할 포트를 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-101">Our server is ready to process video data; the last thing we need to do is open the ports that the traffic cameras will use to upload video files to our server.</span></span> 

## <a name="create-a-network-security-group"></a><span data-ttu-id="faac1-102">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="faac1-102">Create a network security group</span></span>

<span data-ttu-id="faac1-103">원격 데스크톱 액세스를 원한다고 표시했으므로 Azure에서 자동으로 보안 그룹을 만들었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-103">Azure should have created a security group for us because we indicated we wanted Remote Desktop access.</span></span> <span data-ttu-id="faac1-104">하지만 전체 프로세스를 진행할 수 있도록 새 보안 그룹을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-104">But let's create a new security group so you can walk through the entire process.</span></span> <span data-ttu-id="faac1-105">이 작업은 VM에 _앞서_ 가상 네트워크를 만들기로 결정한 경우에 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-105">This is particularly important if you decide to create your virtual network _before_ your VMs.</span></span> <span data-ttu-id="faac1-106">앞서 설명한 것처럼, 보안 그룹은 _선택 사항_이며 네트워크를 사용하여 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-106">As mentioned earlier, security groups are _optional_ and not necessarily created with the network.</span></span>

> [!NOTE]
> <span data-ttu-id="faac1-107">이 VM이 두 번째 VM일 _것이므로_ 이미 해당 네트워크에 적용할 보안 그룹이 있겠지만, 보안 그룹이 없다고 또는 이 VM에 대한 규칙이 다르다고 잠시 가정해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-107">Since this is _supposed_ to be the second VM, we would already have a security group to apply to our network, but let's pretend for a moment that we don't, or that the rules are different for this VM.</span></span>

1. <span data-ttu-id="faac1-108">[Azure Portal](https://portal.azure.com?azure-portal=true)의 왼쪽 모서리 세로 막대에서 **리소스 만들기** 단추를 클릭하여 새 리소스 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-108">In the [Azure portal](https://portal.azure.com?azure-portal=true), click the **Create a resource** button in the left corner sidebar to start a new resource creation.</span></span>

1. <span data-ttu-id="faac1-109">필터 상자에 "네트워크 보안 그룹"을 입력하고 목록에서 일치하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-109">Type "Network security group" into the filter box and select the matching item in the list.</span></span>

1. <span data-ttu-id="faac1-110">**Resource Manager** 배포 모델을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-110">Make sure the **Resource Manager** deployment model is selected and click **Create**.</span></span>

1. <span data-ttu-id="faac1-111">보안 그룹의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-111">Provide a **Name** for your security group.</span></span> <span data-ttu-id="faac1-112">마찬가지로 여기서도 명명 규칙이 좋은 방법이므로, "비디오 프로세서 네트워크 보안 그룹 #2 테스트"에 "test-vp-nsg2"를 사용해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-112">Again, naming conventions are a good idea here, let's use "test-vp-nsg2" for "Test Video Processor Network Security Group #2".</span></span>

1. <span data-ttu-id="faac1-113">적절한 **구독**을 선택하고 기존 **리소스 그룹**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-113">Select the proper **Subscription** and use your existing **Resource group**.</span></span>

1. <span data-ttu-id="faac1-114">마지막으로, 리소스를 동일한 **위치**에 VM/Virtual Network로 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-114">Finally, put it into the same **Location** as the VM / Virtual Network.</span></span> <span data-ttu-id="faac1-115">이 작업이 중요한 것은 이 리소스가 다른 위치에 있는 경우 적용할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-115">This is important - you won't be able to apply this resource if it's in a different location.</span></span>

1. <span data-ttu-id="faac1-116">**만들기**를 클릭하여 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-116">Click **Create** to create the group.</span></span>

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a><span data-ttu-id="faac1-117">네트워크 보안 그룹에 새 인바운드 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="faac1-117">Add a new inbound rule to our Network Security Group</span></span>

<span data-ttu-id="faac1-118">배포를 신속하게 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-118">Deployment should complete quickly.</span></span>

1. <span data-ttu-id="faac1-119">새 보안 그룹 리소스를 찾아 Azure Portal에서 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-119">Find the new security group resource and select it in the Azure portal.</span></span>

1. <span data-ttu-id="faac1-120">개요 페이지에서 네트워크를 잠그기 위해 만든 몇 가지 기본 규칙을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-120">On the overview page, you'll find that it has some default rules created to lock down the network.</span></span>

    <span data-ttu-id="faac1-121">인바운드 측:</span><span class="sxs-lookup"><span data-stu-id="faac1-121">On the inbound side:</span></span>

    - <span data-ttu-id="faac1-122">한 VNet에서 다른 VNet으로의 모든 인바운드 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-122">All inbound traffic from one VNet to another is allowed.</span></span> <span data-ttu-id="faac1-123">이렇게 하면 VNet의 리소스가 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-123">This lets resources on the VNet talk to each other.</span></span>
    - <span data-ttu-id="faac1-124">Azure Load Balancer "프로브"가 VM이 활성화 상태인지 확인 요청</span><span class="sxs-lookup"><span data-stu-id="faac1-124">Azure Load balancer "probe" requests to ensure the VM is alive</span></span>
    - <span data-ttu-id="faac1-125">그 외의 인바운드 트래픽은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-125">All other inbound traffic is denied.</span></span>
    <span data-ttu-id="faac1-126">아웃바운드 측:</span><span class="sxs-lookup"><span data-stu-id="faac1-126">On the outbound side:</span></span>
    - <span data-ttu-id="faac1-127">VNet에서 모든 네트워크 내 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-127">All in-network traffic on the VNet is allowed.</span></span>
    - <span data-ttu-id="faac1-128">인터넷에 대한 모든 아웃바운드 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-128">All outbound traffic to the Internet is allowed.</span></span>
    - <span data-ttu-id="faac1-129">그 외의 아웃바운드 트래픽은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-129">All other outbound traffic is denied.</span></span>

> [!NOTE]
> <span data-ttu-id="faac1-130">이러한 기본 규칙에는 높은 우선 순위가 설정됩니다. 즉, 기본 규칙은 _마지막_으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-130">These default rules are set with high priority values, which means that they get evaluated _last_.</span></span> <span data-ttu-id="faac1-131">기본 규칙을 변경하거나 삭제할 수 없지만 사용자 트래픽을 우선 순위가 낮은 값과 일치하도록 보다 구체적인 규칙을 만들어 기본 규칙을 _재정의_할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-131">They cannot be changed or deleted, but you can _override_ them by creating more specific rules to match your traffic with a lower priority value.</span></span>

1. <span data-ttu-id="faac1-132">보안 그룹에 대한 **설정** 패널에서 **인바운드 보안 규칙** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-132">Click the **Inbound security rules** section in the **Settings** panel for the security group.</span></span>

1. <span data-ttu-id="faac1-133">**+ 추가**를 클릭하여 새 보안 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-133">Click **+ Add** to add a new security rule.</span></span>

    ![보안 규칙 추가](../media-drafts/8-add-rule.png)

    <span data-ttu-id="faac1-135">보안 규칙에 필요한 정보를 입력하는 방법은 기본 및 고급의 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-135">There are two ways to enter the information necessary for a security rule: basic and advanced.</span></span> <span data-ttu-id="faac1-136">"추가" 패널의 맨 위에 있는 단추를 클릭하여 두 가지 방법 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-136">You can switch between them by clicking the button at the top of the "add" panel.</span></span>

    ![기본 vs. 고급 규칙 입력](../media-drafts/8-advanced-create-rule.png)

    <span data-ttu-id="faac1-138">고급 모드는 규칙을 완전히 사용자 지정할 수 있는 기능을 제공하지만, 알려진 프로토콜을 구성해야 하는 경우 기본 모드가 사용하기에 조금 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-138">The advanced mode provides the ability to completely customize the rule, however, if you just need to configure a known protocol, the basic mode is a bit easier to work with.</span></span>

1. <span data-ttu-id="faac1-139">기본 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-139">Switch to the Basic mode.</span></span>

1. <span data-ttu-id="faac1-140">FTP 규칙에 대한 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-140">Add the information for our FTP rule.</span></span>

    - <span data-ttu-id="faac1-141">**서비스**를 FTP로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-141">Set the **Service** to be FTP.</span></span> <span data-ttu-id="faac1-142">이렇게 하면 사용자를 위한 포트 범위를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-142">This will set your port range up for you.</span></span>
    - <span data-ttu-id="faac1-143">**우선 순위**를 "1000"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-143">Set the **Priority** to "1000".</span></span> <span data-ttu-id="faac1-144">우선 순위 값은 기본 **거부** 규칙보다 작은 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-144">It has to be a lower number than the default **Deny** rule.</span></span> <span data-ttu-id="faac1-145">모든 값에서 범위를 시작할 수 있지만, 나중에 예외를 만들어야 할 경우를 대비하여 약간의 여유를 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-145">You can start the range at any value, but it's recommended you give yourself some space in case an exception needs to be created later.</span></span>
    - <span data-ttu-id="faac1-146">규칙의 이름을 "traffic-cam-ftp-upload-2"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-146">Give the rule a name, we'll use "traffic-cam-ftp-upload-2".</span></span>
    - <span data-ttu-id="faac1-147">규칙의 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-147">Give the rule a description.</span></span>

1. <span data-ttu-id="faac1-148">**고급** 모드로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-148">Switch back to the **Advanced** mode.</span></span> <span data-ttu-id="faac1-149">설정이 아직 그대로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-149">Notice that our settings are still present.</span></span> <span data-ttu-id="faac1-150">이 패널을 사용하여 더 세분화된 설정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-150">We can use this panel to create more fine-grained settings.</span></span> <span data-ttu-id="faac1-151">특히 **원본**을 특정 IP 주소 또는 카메라 관련 IP 주소 범위로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-151">In particular, we would likely restrict the **Source** to be a specific IP address or range of IP addresses specific to the cameras.</span></span> <span data-ttu-id="faac1-152">로컬 컴퓨터의 현재 IP 주소를 알고 있는 경우 제한을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-152">If you know the current IP address of your local computer, you can try that.</span></span> <span data-ttu-id="faac1-153">그렇지 않은 경우 설정을 "모두"로 두고 규칙을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-153">Otherwise, leave the setting as "Any" so you can test the rule.</span></span>

1. <span data-ttu-id="faac1-154">**추가**를 클릭하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-154">Click **Add** to create the rule.</span></span> <span data-ttu-id="faac1-155">이렇게 하면 우선 순위에 따라 인바운드 규칙 목록을 업데이트해서 해당 규칙을 검사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-155">This will update the list of inbound rules - notice they are in priority order, which is how they will be examined.</span></span>
    
## <a name="apply-the-security-group"></a><span data-ttu-id="faac1-156">보안 그룹 적용</span><span class="sxs-lookup"><span data-stu-id="faac1-156">Apply the security group</span></span>

<span data-ttu-id="faac1-157">단일 VM을 보호하기 위한 네트워크 인터페이스에 또는 서브넷의 모든 리소스에 적용되는 해당 서브넷에 보안 그룹을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-157">Recall that we can apply the security group to a network interface to guard a single VM, or to a subnet where it would apply to any resources on that subnet.</span></span> <span data-ttu-id="faac1-158">후자가 가장 일반적인 방법이므로 후자를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-158">The latter approach tends to be the most common so let's do that.</span></span> <span data-ttu-id="faac1-159">가상 네트워크 리소스를 통하거나 간접적으로 가상 네트워크를 사용하는 VM을 통해 Azure에서 이 리소스를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-159">We could get to this resource in Azure through either the virtual network resource or indirectly through the VM which is using the virtual network.</span></span>

1. <span data-ttu-id="faac1-160">가상 머신에 대한 **개요** 패널로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-160">Switch to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="faac1-161">VM은 **모든 리소스** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-161">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="faac1-162">**설정** 섹션에서 **네트워킹** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-162">Select the **Networking** item in the **Settings** section.</span></span>

    ![VM 설정의 네트워킹 항목](../media-drafts/8-network-settings.png)

1. <span data-ttu-id="faac1-164">네트워킹 속성에서는 **가상 네트워크/서브넷**(리소스로 이동하는 클릭 가능한 링크)을 포함하여 VM에 적용된 네트워킹에 대한</span><span class="sxs-lookup"><span data-stu-id="faac1-164">In the networking properties, you will find information about the networking applied to the VM including the **Virtual network/subnet**.</span></span> <span data-ttu-id="faac1-165">정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-165">This is a clickable link to get to the resource.</span></span> <span data-ttu-id="faac1-166">이 링크를 클릭하여 가상 네트워크를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-166">Click it to open the virtual network.</span></span> <span data-ttu-id="faac1-167">이 링크는 VM의 **개요** 패널_에서도_ 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-167">This link is _also_ available on the **Overview** panel of the VM.</span></span> <span data-ttu-id="faac1-168">이러한 링크 중 하나를 클릭하면 가상 네트워크의 **개요**가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-168">Either of these will open the **Overview** of the virtual network.</span></span>

1. <span data-ttu-id="faac1-169">**설정** 섹션에서 **서브넷** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-169">In the **Settings** section, select the **Subnets** item.</span></span>

1. <span data-ttu-id="faac1-170">앞에서 VM + 네트워크를 만들었을 때 단일 서브넷(기본값)이 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-170">We should have a single subnet defined (default) from when we created the VM + network earlier.</span></span> <span data-ttu-id="faac1-171">목록에서 항목을 클릭하여 세부 정보를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-171">Click the item in the list to open the details.</span></span>

1. <span data-ttu-id="faac1-172">**네트워크 보안 그룹** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-172">Click the **Network security group** entry.</span></span>

1. <span data-ttu-id="faac1-173">새 보안 그룹 **test-vp-nsg2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-173">Select your new security group: **test-vp-nsg2**.</span></span>

1. <span data-ttu-id="faac1-174">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-174">Click **Save** to save the change.</span></span> <span data-ttu-id="faac1-175">변경 내용을 네트워크에 적용하려면 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-175">It will take a minute to apply to the network.</span></span>

## <a name="verify-the-rules"></a><span data-ttu-id="faac1-176">규칙 확인</span><span class="sxs-lookup"><span data-stu-id="faac1-176">Verify the rules</span></span>

<span data-ttu-id="faac1-177">변경 내용의 유효성을 검사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-177">Let's validate the change.</span></span>

1. <span data-ttu-id="faac1-178">가상 머신의 **개요** 패널로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-178">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="faac1-179">VM은 **모든 리소스** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-179">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="faac1-180">**설정** 섹션에서 **네트워킹** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-180">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="faac1-181">네트워크에 대한 **개요** 패널에는 신속하게 규칙을 평가하는 방법을 보여주는 \*\*효과적인 보안 규칙에 대한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-181">In the **Overview** panel for the network, there is a link for \*\*Effective security rules that will quickly show you how rules are going to be evaluated.</span></span> <span data-ttu-id="faac1-182">링크를 클릭하여 분석을 열고 FTP 규칙이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-182">Click the link to open the analysis and make sure you see your FTP rule.</span></span>

    ![네트워크에 대한 효과적인 보안 규칙](../media-drafts/8-effective-rules.png)

1. <span data-ttu-id="faac1-184">FTP 서버 역할을 설치한 경우 이제 FTP 엔드포인트에 연결할 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-184">If you installed the FTP server role, you should be able to connect to the FTP endpoint now.</span></span> <span data-ttu-id="faac1-185">직접 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="faac1-185">Try it out.</span></span>

## <a name="one-more-thing"></a><span data-ttu-id="faac1-186">추가 사항</span><span class="sxs-lookup"><span data-stu-id="faac1-186">One more thing</span></span>

<span data-ttu-id="faac1-187">보안 규칙을 올바르게 이해하기는 쉽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-187">Security rules are tricky to get right.</span></span> <span data-ttu-id="faac1-188">실제로 우리는 이 새 보안 그룹을 적용할 때 실수를 하는 바람에 원격 데스크톱 액세스가 손실되었습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-188">We actually made a mistake when we applied this new security group - we lost our Remote Desktop access!</span></span> <span data-ttu-id="faac1-189">이 문제를 해결하려면 보안 그룹에 다른 규칙을 추가하여 RDP 액세스를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-189">To fix this, you can add another rule to the security group to support RDP access.</span></span> <span data-ttu-id="faac1-190">규칙에 대한 인바운드 TCP/IP 주소를 소유하는 주소로 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-190">Make sure to restrict the inbound TCP/IP addresses for the rule to be the ones you own.</span></span>

> [!WARNING]
> <span data-ttu-id="faac1-191">항상 관리 액세스에 사용되는 포트를 잠가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-191">Always make sure to lock down ports used for administrative access.</span></span> <span data-ttu-id="faac1-192">더 좋은 방법은 개인 네트워크에 가상 네트워크를 연결하고 해당 주소 범위에서 RDP 또는 SSH 요청만 허용하는 VPN을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-192">An even better approach is to create a VPN to link the virtual network to your private network and only allow RDP or SSH requests from that address range.</span></span> <span data-ttu-id="faac1-193">또한 RDP에서 사용하는 포트를 기본 포트인 3389 이외의 포트로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-193">You can also change the port used by RDP to be something other than the default 3389.</span></span> <span data-ttu-id="faac1-194">포트 변경으로는 공격을 막는 데 충분하지 않으므로 검색을 조금 더 어렵게 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="faac1-194">Keep in mind that changing ports is not sufficient to stop attacks, it simply makes it a little harder to discover.</span></span>