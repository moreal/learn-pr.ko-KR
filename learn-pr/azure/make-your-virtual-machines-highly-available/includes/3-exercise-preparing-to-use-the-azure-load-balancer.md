<span data-ttu-id="2c0eb-101">이 연습에서는 Azure Portal을 사용하여 부하 분산 장치, 가상 네트워크 및 여러 개의 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-101">In this exercise, you will create a load balancer, a virtual network, and multiple virtual machines using the Azure portal.</span></span>

<span data-ttu-id="2c0eb-102">온라인 뱅킹 서비스를 시작하려는 신설 기업인 Woodgrove Bank에서 근무한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-102">Suppose you work for Woodgrove Bank, a startup that is about to launch online banking services.</span></span> <span data-ttu-id="2c0eb-103">이 부문은 경쟁이 치열하므로 99.99% 이상의 서비스 가용성을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-103">This sector is highly competitive, so you need to guarantee of a minimum of 99.99% service availability.</span></span> <span data-ttu-id="2c0eb-104">세 개의 가상 머신으로 구성된 풀이 있는 Azure Load Balancer를 통해 이 목표를 달성할 수 있을 것이라고 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-104">You have determined that an Azure Load Balancer with a pool of three virtual machines will meet this goal.</span></span>

## <a name="create-a-public-load-balancer"></a><span data-ttu-id="2c0eb-105">공용 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="2c0eb-105">Create a public load balancer</span></span>

1. <span data-ttu-id="2c0eb-106">브라우저에서 [Azure Portal](https://portal.azure.com/?azure-portal=true)로 이동하고, 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-106">In a browser, navigate to the [Azure portal](https://portal.azure.com/?azure-portal=true) and sign in to your account.</span></span>

1. <span data-ttu-id="2c0eb-107">세로 막대에서 **리소스 만들기**를 클릭하고, **새로 만들기** 블레이드에서 **네트워킹**을 클릭한 다음, **부하 분산 장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-107">In the sidebar, click **Create a resource**, then in the **New** blade, click **Networking**, and then click **Load Balancer**.</span></span>

1. <span data-ttu-id="2c0eb-108">[부하 분산 장치 만들기] 블레이드에서 다음 정보를 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-108">In the Create load balancer blade, enter or select the following information:</span></span>
    - <span data-ttu-id="2c0eb-109">이름: **woodgrove LB**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-109">Name: **woodgrove-LB**</span></span>
    - <span data-ttu-id="2c0eb-110">유형: **공용**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-110">Type: **Public**</span></span>
    - <span data-ttu-id="2c0eb-111">SKU: **기본**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-111">SKU: **Basic**</span></span>
    - <span data-ttu-id="2c0eb-112">공용 IP 주소: **새로 만들기**를 선택하고, 텍스트 상자에서 **woodgrove-LB-ip**를 입력하고, [할당]은 **동적**으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-112">Public IP address: Select **Create new** and in the text box, type **woodgrove-LB-ip** in the text box, and leave the Assignment as **Dynamic**</span></span>
    - <span data-ttu-id="2c0eb-113">리소스 그룹: **새로 만들기**를 선택하고, 상자에서 **woodgrove-RG**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-113">Resource group: Select **Create new**, and in the box, type **woodgrove-RG**</span></span>
    - <span data-ttu-id="2c0eb-114">위치: 사용자에게 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-114">Location: Select a region near you</span></span>

1. <span data-ttu-id="2c0eb-115">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-115">Click **Create**.</span></span>

1. <span data-ttu-id="2c0eb-116">부하 분산 장치가 배포될 때까지 기다린 후에 연습을 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-116">Wait until the load balancer has deployed before continuing with the exercise.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="2c0eb-117">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="2c0eb-117">Create a Virtual Network</span></span>

1. <span data-ttu-id="2c0eb-118">왼쪽 메뉴에서 **리소스 만들기**를 클릭하고, **새로 만들기** 블레이드에서 **네트워킹**을 클릭한 다음, **가상 네트워크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-118">In the left menu, click **Create a resource**, then in the **New** blade, click **Networking**, and then click **Virtual network**.</span></span>

1. <span data-ttu-id="2c0eb-119">**가상 네트워크 만들기** 블레이드에서 다음 정보를 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-119">In the **Create virtual network** blade, enter or select the following information:</span></span>
    - <span data-ttu-id="2c0eb-120">이름: **woodgrove VNET**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-120">Name: **woodgrove-VNET**</span></span>
    - <span data-ttu-id="2c0eb-121">주소 공간: **172.20.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-121">Address space: **172.20.0.0/16**</span></span>
    - <span data-ttu-id="2c0eb-122">리소스 그룹: **기존 항목 사용**, **woodgrove-RG**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-122">Resource group: Select **Use existing**, and select **woodgrove-RG**.</span></span>
    - <span data-ttu-id="2c0eb-123">서브넷: **backendSubnet**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-123">Subnet: **backendSubnet**</span></span>
    - <span data-ttu-id="2c0eb-124">주소 공간: **172.20.0.0/24**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-124">Address space: **172.20.0.0/24**</span></span>
    - <span data-ttu-id="2c0eb-125">DDoS 보호: **기본**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-125">DDoS protection: **Basic**</span></span>
    - <span data-ttu-id="2c0eb-126">서비스 엔드포인트: **사용 안 함**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-126">Service endpoints: **Disabled**</span></span>

1. <span data-ttu-id="2c0eb-127">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-127">Click **Create**.</span></span>

1. <span data-ttu-id="2c0eb-128">가상 네트워크가 배포될 때까지 기다렸다가 연습을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-128">Wait until the virtual network has deployed before continuing with the exercise.</span></span>

## <a name="create-a-vm-template"></a><span data-ttu-id="2c0eb-129">VM 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="2c0eb-129">Create a VM template</span></span>

<span data-ttu-id="2c0eb-130">먼저 기본 VM 정보를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-130">Start by defining the basic VM information:</span></span>

1. <span data-ttu-id="2c0eb-131">Azure Portal의 왼쪽 메뉴에서 **가상 머신**, **가상 머신 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-131">In the Azure portal, in the left menu, click **Virtual machines**, and then click **Create virtual machine**.</span></span>

1. <span data-ttu-id="2c0eb-132">[계산] 블레이드의 **권장** 섹션에서 **Windows Server**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-132">On the Compute blade, in the **Recommended** section, click **Windows Server**.</span></span>

1. <span data-ttu-id="2c0eb-133">**Windows Server** 블레이드에서 **Windows Server 2016 Datacenter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-133">In the **Windows Server** blade, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="2c0eb-134">**Windows Server 2016 Datacenter** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-134">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="2c0eb-135">**기본 사항** 블레이드의 **이름** 상자에서 **woodgrove-SVR01**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-135">In the **Basics** blade, in the **Name** box, type **woodgrove-SVR01**.</span></span>

1. <span data-ttu-id="2c0eb-136">**사용자 이름** 및 **암호** 상자에서 이 서버의 관리자 계정에 대한 보안 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-136">In the **Username** and **Password boxes**, type a secure name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="2c0eb-137">**구독** 상자에서 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-137">In the **Subscription** box, select your Azure subscription.</span></span>

1. <span data-ttu-id="2c0eb-138">**리소스 그룹** 아래에서 **기존 항목 사용**을 선택한 다음, 목록에서 **woodgrove-RG**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-138">Under **Resource group**, select **Use existing**, and in the list, select **woodgrove-RG**.</span></span>

1. <span data-ttu-id="2c0eb-139">**위치** 드롭다운 목록에서 사용자에게 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-139">In the **Location** drop-down list, select a region near you.SAME</span></span>

1. <span data-ttu-id="2c0eb-140">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-140">Click **OK**.</span></span>

<span data-ttu-id="2c0eb-141">다음과 같이 VM 크기를 선택하고 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-141">Choose a size for the VM and configure settings:</span></span>

1. <span data-ttu-id="2c0eb-142">**크기 선택** 블레이드에서 **표준** SKU(예: **D2s_v3**)를 선택한 다음, **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-142">On the **Choose a size** blade, select a **Standard** SKU, such as **D2s_v3**, and then click **Select**.</span></span>

1. <span data-ttu-id="2c0eb-143">**설정** 블레이드에서 **가용성 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-143">On the **Settings** blade, click **Availability set**.</span></span>

1. <span data-ttu-id="2c0eb-144">**가용성 집합 변경** 블레이드에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-144">On the **Change availability set** blade, click **Create new**.</span></span>

1. <span data-ttu-id="2c0eb-145">**새로 만들기** 블레이드의 **이름** 상자에서 **woodgrove-AS**를 입력한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-145">On the **Create new** blade, in the **Name** box, type **woodgrove-AS**, and then click **OK**.</span></span>

1. <span data-ttu-id="2c0eb-146">**설정** 블레이드의 **네트워크 보안 그룹** 아래에서 **고급**을 클릭한 다음, 새 항목인 **woodgrove-SVR01-nsg**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-146">On the **Settings** blade, under **Network Security Group**, click **Advanced**, and then click **(new) woodgrove-SVR01-nsg**.</span></span>

1. <span data-ttu-id="2c0eb-147">**네트워크 보안 그룹 만들기** 블레이드의 **이름** 상자에서 이름을 **woodgrove-NSG**로 변경한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-147">On the **Create network Security group** blade, in the **Name** box, change the name to **woodgrove-NSG**, and then click **OK**.</span></span>

1. <span data-ttu-id="2c0eb-148">**설정** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-148">On the **Settings** blade, click **OK**.</span></span>

<span data-ttu-id="2c0eb-149">여러 VM을 쉽게 배포할 수 있도록 설정을 템플릿에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-149">Save the settings to a template, so that you easily deploy multiple VMs.</span></span>

1. <span data-ttu-id="2c0eb-150">**만들기** 블레이드에서 **템플릿 및 매개 변수 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-150">On the **Create** blade, click **Download template and parameters**.</span></span>

1. <span data-ttu-id="2c0eb-151">**템플릿** 블레이드에서 **라이브러리에 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-151">On the **Template** blade, click **Add to library**.</span></span>

1. <span data-ttu-id="2c0eb-152">**템플릿 저장** 블레이드의 **이름** 및 **설명** 상자에서 **woodgrove-server-template**을 입력한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-152">On the **Save template** blade, in the **Name** and **Description** boxes, type **woodgrove-server-template**, and then click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="2c0eb-153">이 템플릿을 찾으려면 왼쪽 메뉴에서 **모든 서비스**를 클릭하고, 필터 상자에서 **템플릿**을 입력한 다음, **템플릿(미리 보기)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-153">If you need to find this template, click **All services** in the left menu, type **template** in the filter box, and then click **Templates (PREVIEW)**.</span></span>

## <a name="use-the-template-to-provision-the-first-vm"></a><span data-ttu-id="2c0eb-154">템플릿을 사용하여 첫 번째 VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="2c0eb-154">Use the template to provision the first VM</span></span>

1. <span data-ttu-id="2c0eb-155">**템플릿** 블레이드에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-155">On the **Template** blade, click **Deploy**.</span></span>

1. <span data-ttu-id="2c0eb-156">**사용자 지정 배포** 블레이드의 **리소스 그룹** 아래에서 **기존 항목 사용**을 선택하고, 목록에서 **woodgrove-RG**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-156">On the **Custom deployment** blade, under **Resource Group**, select **Use existing**, and in the list, select **woodgrove-RG**.</span></span>

1. <span data-ttu-id="2c0eb-157">**사용자 지정 배포** 블레이드의 **관리자 암호** 상자에서 이전에 사용한 것과 동일한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-157">On the **Custom deployment** blade, in the **Admin password** box, type the same password that you used previously.</span></span>

1. <span data-ttu-id="2c0eb-158">**사용자 지정 배포** 블레이드에서 **사용 약관에 동의합니다.** 확인란을 선택한 다음, **구매**를 클릭합니다(비용은 VM 가격 책정 계층에 따라 달라지는 일반 Azure 계산 요금임).</span><span class="sxs-lookup"><span data-stu-id="2c0eb-158">On the **Custom deployment** blade, select the **I agree to the terms and conditions** check box, and then click **Purchase** (the cost is the regular Azure compute charge, which depends on the VM pricing tier).</span></span>

1. <span data-ttu-id="2c0eb-159">VM이 배포될 때까지 기다린 후에 연습을 계속 진행하세요. 그러면 템플릿을 사용하여 추가 VM을 프로비전하기 전에 해당 템플릿이 올바르게 구성되었는지와 모든 관련 리소스가 만들어졌는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-159">Wait until the VM has deployed before continuing with the exercise; this is so you can be sure the template is correctly configured before you use it to provision additional VMs, and all the associated resources have been created.</span></span>

## <a name="use-the-template-to-provision-two-additional-vms"></a><span data-ttu-id="2c0eb-160">템플릿을 사용하여 두 개의 추가 VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="2c0eb-160">Use the template to provision two additional VMs</span></span>

1. <span data-ttu-id="2c0eb-161">Azure Portal의 **템플릿** 블레이드에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-161">In the Azure portal, on the **Template** blade, click **Deploy**.</span></span>

1. <span data-ttu-id="2c0eb-162">**사용자 지정 배포** 블레이드의 **리소스 그룹** 아래에서 **기존 항목 사용**을 선택하고, 목록에서 **woodgrove-RG**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-162">On the **Custom deployment** blade, under **Resource Group**, select **Use existing**, and in the list, select **woodgrove-RG**.</span></span>

1. <span data-ttu-id="2c0eb-163">**사용자 지정 배포** 블레이드의 **Virtual Machine 이름** 상자에서 이름을 **woodgrove-SVR02**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-163">On the **Custom deployment** blade, in the **Virtual Machine Name** box, change the name to **woodgrove-SVR02**.</span></span>

1. <span data-ttu-id="2c0eb-164">**사용자 지정 배포** 블레이드의 **네트워크 인터페이스 이름** 상자에서 이름을 **woodgrovesvr02222**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-164">On the **Custom deployment** blade, in the **Network Interface Name** box, change the name to **woodgrovesvr02222**.</span></span>

1. <span data-ttu-id="2c0eb-165">**사용자 지정 배포** 블레이드의 **관리자 암호** 상자에서 이전에 사용한 것과 동일한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-165">On the **Custom deployment** blade, in the **Admin password** box, type the same password that you used previously.</span></span>

1. <span data-ttu-id="2c0eb-166">**사용자 지정 배포** 블레이드의 **공용 IP 주소 이름** 상자에서 이름을 **woodgrove-SVR02-ip**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-166">On the **Custom deployment** blade, in the **Public Ip Address Name** box, change the name to **woodgrove-SVR02-ip**.</span></span>

1. <span data-ttu-id="2c0eb-167">**사용자 지정 배포** 블레이드에서 **사용 약관에 동의합니다.** 확인란을 선택한 다음, **구매**를 클릭합니다(비용은 VM 가격 책정 계층에 따라 달라지는 일반 Azure 계산 요금임).</span><span class="sxs-lookup"><span data-stu-id="2c0eb-167">On the **Custom deployment** blade, select the **I agree to the terms and conditions** check box, and then click **Purchase** (the cost is the regular Azure compute charge, which depends on the VM pricing tier).</span></span>

1. <span data-ttu-id="2c0eb-168">다음 정보를 사용하여 1-7단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-168">Repeat steps 1 - 7, using the following information:</span></span>
    - <span data-ttu-id="2c0eb-169">Virtual Machine 이름: **woodgrove SVR03**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-169">Virtual Machine Name: **woodgrove-SVR03**</span></span>
    - <span data-ttu-id="2c0eb-170">네트워크 인터페이스 이름: **woodgrovesvr03333**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-170">Network Interface Name: **woodgrovesvr03333**</span></span>
    - <span data-ttu-id="2c0eb-171">공용 IP 주소 이름: **woodgrove-SVRr03-ip**</span><span class="sxs-lookup"><span data-stu-id="2c0eb-171">Public Ip Address Name: **woodgrove-SVRr03-ip**</span></span>

1. <span data-ttu-id="2c0eb-172">VM이 배포될 때까지 기다린 후에 연습을 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-172">Wait until the VMs have deployed before continuing with the exercise.</span></span>

<span data-ttu-id="2c0eb-173">이제 공용 부하 분산 장치를 구성하고 이 부하 분산 장치에서 세 개의 VM을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2c0eb-173">You now have a public load balancer ready to configure, and three VMs ready to use with this load balancer.</span></span>