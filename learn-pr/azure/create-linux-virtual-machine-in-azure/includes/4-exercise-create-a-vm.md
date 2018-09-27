<span data-ttu-id="15c07-101">이 연습의 목표는 Apache를 실행 중인 기존 Linux 서버를 Azure로 이동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-101">Recall that our goal is to move an existing Linux server running Apache to Azure.</span></span> <span data-ttu-id="15c07-102">이를 위해 먼저 Ubuntu Linux 서버를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-102">We'll start by creating an Ubuntu Linux server.</span></span>

## <a name="create-a-new-linux-virtual-machine"></a><span data-ttu-id="15c07-103">새 Linux 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="15c07-103">Create a new Linux virtual machine</span></span>

<span data-ttu-id="15c07-104">Azure Portal, Azure CLI 또는 Azure PowerShell을 사용하여 Linux VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-104">We can create Linux VMs with the Azure portal, the Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="15c07-105">Azure로 시작할 때 가장 쉬운 방법은 Azure Portal을 사용하는 것입니다. Azure Portal에서는 필요한 정보를 단계별로 안내하며 만드는 동안 힌트와 유용한 메시지를 제공하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-105">The easiest approach when you are starting with Azure is to use the portal because it walks you through the required information and provides hints and helpful messages during the creation:</span></span>

1. <span data-ttu-id="15c07-106">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-106">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="15c07-107">Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-107">Click **Create a resource** in the upper-left corner of the Azure portal.</span></span>

1. <span data-ttu-id="15c07-108">검색 상자에 **Ubuntu Server**를 입력하면 사용 가능한 여러 버전이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-108">In the search box, enter  **Ubuntu Server** to see the different versions available.</span></span> <span data-ttu-id="15c07-109">표시된 목록에서 **Ubuntu Server 18.04 LTS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-109">Select **Ubuntu Server 18.04 LTS** from the presented list.</span></span>

1. <span data-ttu-id="15c07-110">**만들기** 단추를 클릭하여 VM 구성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-110">Click the **Create** button to start configuring the VM.</span></span>

## <a name="configure-the-vm-settings"></a><span data-ttu-id="15c07-111">VM 설정 구성</span><span class="sxs-lookup"><span data-stu-id="15c07-111">Configure the VM settings</span></span>

<span data-ttu-id="15c07-112">포털의 VM 만들기 환경은 모든 VM 구성 영역을 단계별로 안내하는 마법사 형식으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-112">The VM creation experience in the portal is presented in a wizard format to walk you through all the configuration areas for the VM.</span></span> <span data-ttu-id="15c07-113">**다음** 단추를 클릭하면 구성 가능한 다음 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-113">Clicking the **Next** button will take you to the next configurable section.</span></span> <span data-ttu-id="15c07-114">그러나 각 부분을 식별하는 위쪽에서 실행되는 탭을 사용하여 원하는 대로 섹션 간에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-114">However, you can move between the sections at will with the tabs running across the top that identify each part.</span></span>

![Ubuntu Server 머신에 대한 가상 머신 만들기 블레이드를 처음으로 보여주는 Azure Portal의 스크린샷.](../media/3-azure-portal-create-vm.png)

<span data-ttu-id="15c07-116">필수 옵션(빨간색 별표로 식별됨)이 모두 채워지면 마법사 환경의 나머지 부분은 건너뛰고 아래쪽의 **검토 + 만들기** 단추를 통해 VM 만들기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-116">Once you fill in all the required options (identified with red asterisks), you can skip the remainder of the wizard experience and start creating the VM through the **Review + Create** button at the bottom.</span></span>

<span data-ttu-id="15c07-117">**기본 사항** 섹션부터 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-117">We'll start with the **Basics** section.</span></span>

### <a name="configure-basic-vm-settings"></a><span data-ttu-id="15c07-118">기본 VM 설정 구성</span><span class="sxs-lookup"><span data-stu-id="15c07-118">Configure basic VM settings</span></span>

1. <span data-ttu-id="15c07-119">**구독**의 경우 기본적으로 샌드박스 구독이 선택되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-119">For **Subscription**, the sandbox subscription should be selected for you by default.</span></span>

1. <span data-ttu-id="15c07-120">**리소스 그룹**의 경우 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 이라는 리소스 그룹이 기본적으로 선택되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-120">For **Resource group**, the resource group with the name **<rgn>[sandbox resource group name]</rgn>** should be selected for you by default.</span></span>

1. <span data-ttu-id="15c07-121">**인스턴스 세부 정보** 섹션에서 웹 서버 VM의 이름을 **test-web-eus-vm1**과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-121">In the **INSTANCE DETAILS** section, enter a name for your web server VM, such as **test-web-eus-vm1**.</span></span> <span data-ttu-id="15c07-122">이 이름은 환경(**test**), 역할(**web**), 위치(**미국 동부**), 서비스(**vm**) 및 인스턴스 번호(**1**)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-122">This indicates the environment (**test**), the role (**web**), location (**East US**), service (**vm**), and instance number (**1**).</span></span>
    - <span data-ttu-id="15c07-123">용도를 빠르게 식별할 수 있도록 리소스 이름을 표준화하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-123">It's a best practice to standardize your resource names, so you can quickly identify their purpose.</span></span> <span data-ttu-id="15c07-124">Linux VM 이름은 1-64자여야 하며 숫자, 문자 및 대시로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-124">Linux VM names must be between 1 and 64 characters and be comprised of numbers, letters, and dashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15c07-125">각 자유 텍스트 필드에서 설정과 탭을 변경하면 Azure에서 각 값의 유효성을 자동으로 검사하고 해당 값이 적절한 경우 옆에 녹색 확인 표시를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-125">As you change settings and tab out of each free-text field, Azure will validate each value automatically and place a green check mark next to it when it's good.</span></span> <span data-ttu-id="15c07-126">오류 표시기 위를 마우스로 가리키면 검색된 문제에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-126">You can hover over error indicators to get more information on issues it discovers.</span></span>

1. <span data-ttu-id="15c07-127">위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-127">Select a location.</span></span>

    <span data-ttu-id="15c07-128"><!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]</span><span class="sxs-lookup"><span data-stu-id="15c07-128"><!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]</span></span>

1. <span data-ttu-id="15c07-129">**가용성 옵션**을 **인프라 중복 필요 없음**으로 설정된 채로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-129">Leave **Availability options** as **No infrastructure redundancy required**.</span></span> <span data-ttu-id="15c07-130">이 옵션은 계획되거나 계획되지 않은 유지 관리 이벤트 또는 중단을 처리하기 위해 여러 VM을 하나의 집합으로 그룹화하여 VM의 가용성을 높이는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-130">This option is used to ensure the VM is highly available by grouping multiple VMs together as a set to deal with planned or unplanned maintenance events or outages.</span></span>

1. <span data-ttu-id="15c07-131">이미지가 **Ubuntu Server 18.04 LTS**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-131">Ensure that the image is set to **Ubuntu Server 18.04 LTS**.</span></span> <span data-ttu-id="15c07-132">드롭다운 목록을 열어 사용 가능한 모든 옵션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-132">You can open the drop-down list to see all the options available.</span></span>

1. <span data-ttu-id="15c07-133">**크기** 필드는 직접 편집할 수 없으며 기본 크기는 범용 컴퓨팅 선택 항목 중 하나인 **DS2_v3**입니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-133">The **Size** field is not directly editable and has a **DS2_v3** default size, which is one of the general-purpose computing selections.</span></span> <span data-ttu-id="15c07-134">이 선택 항목은 공용 웹 서버에 적합하지만, 다른 VM 크기를 살펴보려면 **크기 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-134">This choice is perfect for a public web server, but click the **Change size** link to explore other VM sizes.</span></span> <span data-ttu-id="15c07-135">결과 대화 상자에서 **vCPU의 #**, **이름** 및 **디스크 유형**에 따라 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-135">The resulting dialog allows you to filter based on **# of vCPUs**, **Name**, and **Disk Type**.</span></span> <span data-ttu-id="15c07-136">같은 **DS2_v3** 항목을 선택하면 vCPU 2개와 8GB RAM이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-136">Select the same **DS2_v3** choice, which gives you two vCPUs with 8 GB of RAM.</span></span>

    > [!TIP]
    > <span data-ttu-id="15c07-137">보기를 왼쪽으로 슬라이드하여 VM 설정(오른쪽의 새 창에서 열려 원래 창이 왼쪽으로 슬라이드됨)을 다시 표시하여 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-137">You can also slide the view to the left to get back to the VM settings as it opened a new window off to the right and slid the window over to view it.</span></span>

1. <span data-ttu-id="15c07-138">SSH에 로그인하는 데 사용할 **사용자 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-138">Enter a **username** you'll use to sign in with SSH.</span></span>

1. <span data-ttu-id="15c07-139">**관리자 권한** 섹션에서 **인증 형식**으로 SSH 공개 키 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-139">In the **ADMINISTRATOR ACCESS** section, select the SSH public key option for **Authentication type**.</span></span>

1. <span data-ttu-id="15c07-140">공개 키 파일에서 SSH 키를 복사하여 **SSH 공개 키** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-140">Copy the SSH key from your public key file and paste it into the **SSH public key** field.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="15c07-141">Azure Portal에 공개 키를 복사할 때는 공백이나 줄 바꿈 문자를 더 추가하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-141">When you copy the public key into the Azure portal, make sure not to add any additional whitespace or line-feed characters.</span></span>

1. <span data-ttu-id="15c07-142">**인바운드 포트 규칙** 섹션에서 목록을 열고 **공용 인바운드 포트 없음**을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-142">In the **INBOUND PORT RULES** section, open the list and uncheck **No public inbound ports**.</span></span> <span data-ttu-id="15c07-143">이 VM은 Linux VM이므로 SSH를 사용하여 VM에 원격으로 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-143">Since this is a Linux VM, we want to be able to access the VM using SSH remotely.</span></span> <span data-ttu-id="15c07-144">필요한 경우 **SSH(22)** 를 찾을 때까지 목록을 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-144">Scroll the list if necessary until you find **SSH (22)** and select it.</span></span> <span data-ttu-id="15c07-145">UI의 참고 사항에서 언급한 대로 VM을 만든 후 네트워크 포트를 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-145">As the note in the UI indicates, we can also adjust the network ports after we create the VM.</span></span>

    ![SSH 액세스를 위해 Linux VM을 여는 방법에 대해 설명한 대로 관리자 계정 및 인바운드 포트 설정을 보여주는 Azure portal의 스크린샷.](../media/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a><span data-ttu-id="15c07-147">VM에 대한 디스크 구성</span><span class="sxs-lookup"><span data-stu-id="15c07-147">Configure disks for the VM</span></span>

1. <span data-ttu-id="15c07-148">**다음: 디스크 >** 를 클릭하여 **디스크** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-148">Click **Next: Disks >** to move to the **Disks** section.</span></span>

    ![가상 머신 만들기 블레이드의 디스크 섹션을 보여주는 Azure Portal의 스크린샷.](../media/3-configure-disks.png)

1. <span data-ttu-id="15c07-150">**OS 디스크 유형**에 대해 **프리미엄 SSD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-150">Choose **Premium SSD** for the **OS disk type**.</span></span>

1. <span data-ttu-id="15c07-151">저장소 계정을 사용하지 않도록 관리 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-151">Use managed disks, so we don't have to work with storage accounts.</span></span> <span data-ttu-id="15c07-152">원하는 경우 Azure에 필요한 정보의 차이를 보기 위해 GUI에서 스위치를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-152">You can flip the switch in the GUI to see the difference in information that Azure needs if you like.</span></span>

### <a name="create-a-data-disk"></a><span data-ttu-id="15c07-153">데이터 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="15c07-153">Create a data disk</span></span>

<span data-ttu-id="15c07-154">OS 디스크(/dev/sda)와 임시 디스크(/dev/sdb)를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-154">Recall that we will get an OS disk (/dev/sda) and a temporary disk (/dev/sdb).</span></span> <span data-ttu-id="15c07-155">데이터 디스크도 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-155">Let's add a data disk as well:</span></span>

1. <span data-ttu-id="15c07-156">**데이터 디스크** 섹션에서 **새 디스크 만들기 및 연결** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-156">Click the **Create and attach a new disk** link in the **DATA DISKS** section.</span></span>

    ![새 디스크 만들기 블레이드를 보여주는 Azure Portal의 스크린샷.](../media/3-add-data-disk.png)

1. <span data-ttu-id="15c07-158">여기서는 스냅숏 또는 Azure Blob 저장소를 사용하여 VHD를 만들 수 있지만 모든 기본값, 즉 프리미엄 SSD, 1023GB 및 **없음**(빈 디스크)을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-158">You can take all the defaults: Premium SSD, 1023 GB, and **None** (empty disk), although notice that here is where we could use a snapshot or Azure Blob storage to create a VHD.</span></span>

1. <span data-ttu-id="15c07-159">**확인**을 클릭하여 디스크를 만들고 **데이터 디스크** 섹션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-159">Click **OK** to create the disk and go back to the **DATA DISKS** section.</span></span>

1. <span data-ttu-id="15c07-160">이제 첫 번째 행에 새 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-160">There should now be a new disk in the first row.</span></span>

    ![VM 만들기 프로세스를 위해 새로 만든 데이터 디스크 줄을 보여주는 Azure Portal의 스크린샷.](../media/3-new-disk.png)

## <a name="configure-the-network"></a><span data-ttu-id="15c07-162">네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="15c07-162">Configure the network</span></span>

1. <span data-ttu-id="15c07-163">**다음: 네트워킹 >** 을 클릭하여 **네트워킹** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-163">Click **Next: Networking >** to move to the **Networking** section.</span></span>

1. <span data-ttu-id="15c07-164">이미 다른 구성 요소가 있는 프로덕션 시스템에서 _기존_ 가상 네트워크를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-164">In a production system where we already have other components, we'd want to utilize an _existing_ virtual network.</span></span> <span data-ttu-id="15c07-165">이렇게 하면 VM에서 솔루션의 다른 클라우드 서비스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-165">That way, our VM can communicate with the other cloud services in our solution.</span></span> <span data-ttu-id="15c07-166">이 위치에 정의된 가상 네트워크가 아직 없으면 여기서 만들고 다음 항목을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-166">If there isn't one defined in this location yet, we can create it here and configure the:</span></span>
    - <span data-ttu-id="15c07-167">**주소 공간**: 이 네트워크에서 사용할 수 있는 전체 IPV4 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-167">**Address space**: The overall IPV4 space available to this network.</span></span>
    - <span data-ttu-id="15c07-168">**서브넷 범위**: 주소 공간을 세분화할 첫 번째 서브넷이며, 정의된 주소 공간 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-168">**Subnet range**: The first subnet to subdivide the address space - it must fit within the defined address space.</span></span> <span data-ttu-id="15c07-169">VNet이 만들어지면 추가 서브넷을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-169">Once the VNet is created, you can add additional subnets.</span></span>

> [!NOTE]
> <span data-ttu-id="15c07-170">기본적으로 Azure는 VM에 대한 가상 네트워크, 네트워크 인터페이스 및 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-170">By default, Azure will create a virtual network, network interface, and public IP for your VM.</span></span> <span data-ttu-id="15c07-171">VM을 만든 후에 네트워킹 옵션을 변경하는 것은 쉽지 않으므로 Azure에서 만든 서비스에 대한 네트워크 할당을 항상 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-171">It's not trivial to change the networking options after the VM has been created, so always double-check the network assignments on services you create in Azure.</span></span>

## <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="15c07-172">VM 구성 완료 및 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="15c07-172">Finish configuring the VM and create the image</span></span>

<span data-ttu-id="15c07-173">나머지 옵션에는 적절한 기본값이 있으므로 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-173">The rest of the options have reasonable defaults, and there's no need to change any of them.</span></span> <span data-ttu-id="15c07-174">원하는 경우 다른 탭을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-174">You can explore the other tabs if you like.</span></span> <span data-ttu-id="15c07-175">개별 옵션 옆에는 해당 옵션을 설명하는 도움말 팁이 표시되는 `(i)` 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-175">The individual options have an `(i)` icon next to them that will show a help tip to explain the option.</span></span> <span data-ttu-id="15c07-176">이는 VM을 구성하는 데 사용할 수 있는 다양한 옵션에 대해 알아볼 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-176">This is a great way to learn about the various options you can use to configure the VM:</span></span>

1. <span data-ttu-id="15c07-177">패널 아래쪽에서 **검토 + 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-177">Click the **Review + create** button at the bottom of the panel.</span></span>

1. <span data-ttu-id="15c07-178">시스템에서 옵션의 유효성이 검사되고 생성되는 VM에 대한 세부 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-178">The system will validate your options and give you details about the VM being created.</span></span>

1. <span data-ttu-id="15c07-179">**만들기**를 클릭하여 VM을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-179">Click **Create** to create and deploy the VM.</span></span> <span data-ttu-id="15c07-180">Azure 대시보드에 배포 중인 VM이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-180">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="15c07-181">이 작업은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-181">This may take several minutes.</span></span>

<span data-ttu-id="15c07-182">VM이 배포되는 동안 이 VM으로 수행할 수 있는 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15c07-182">While that's deploying, let's look at what we can do with this VM.</span></span>