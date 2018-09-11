<span data-ttu-id="3faf1-101">당사는 Windows VM에서 비디오 콘텐츠를 처리하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-101">Recall that our company processes video content on Windows VMs.</span></span> <span data-ttu-id="3faf1-102">신도시에서 교통 카메라를 처리하기 위해 당사와 계약했지만, 이 모델은 이전에 당사에서 사용한 경험이 없었던 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-102">A new city has contracted us to process their traffic cameras, but it's a model we've not worked with before.</span></span> <span data-ttu-id="3faf1-103">새 Windows VM을 만들고 몇 가지 독점적인 코덱을 설치하여 이미지 처리 및 분석을 시작할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-103">We need to create a new Windows VM and install some proprietary codecs so we can begin processing and analyzing their images.</span></span>

## <a name="create-a-new-windows-virtual-machine"></a><span data-ttu-id="3faf1-104">새 Windows 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="3faf1-104">Create a new Windows virtual machine</span></span>

<span data-ttu-id="3faf1-105">Windows VM은 Azure Portal, Azure CLI 또는 Azure PowerShell을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-105">We can create Windows VMs with the Azure portal, Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="3faf1-106">필요한 정보를 단계별로 안내하고 만드는 동안 힌트와 유용한 메시지를 제공하므로 포털이 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-106">The easiest approach is to the portal because it walks you through the required information and provides hints and helpful messages during the creation.</span></span>

1. <span data-ttu-id="3faf1-107">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-107">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="3faf1-108">Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-108">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="3faf1-109">검색 상자에서 **Windows Server 2016 Datacenter**를 입력한 다음, 제공된 목록에서 동일한 제목의 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-109">In the search box, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title in the presented list.</span></span>

1. <span data-ttu-id="3faf1-110">**만들기** 단추를 클릭하여 VM 구성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-110">Click the **Create** button to start configuring the VM.</span></span>

## <a name="configure-the-vm-settings"></a><span data-ttu-id="3faf1-111">VM 설정 구성</span><span class="sxs-lookup"><span data-stu-id="3faf1-111">Configure the VM settings</span></span>

<span data-ttu-id="3faf1-112">포털의 VM 만들기 환경은 모든 VM 구성 영역을 단계별로 안내하는 "마법사" 형식으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-112">The VM creation experience in the portal is presented in a "wizard" format to walk you through all the configuration areas for the VM.</span></span> <span data-ttu-id="3faf1-113">"다음" 단추를 클릭하면 구성 가능한 다음 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-113">Clicking the "Next" button will take you to the next configurable section.</span></span> <span data-ttu-id="3faf1-114">그러나 각 섹션을 식별하는 위쪽에서 실행되는 탭을 사용하여 원하는 대로 섹션 간에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-114">However, you can move between the sections at will with the tabs running across the top that identify each section.</span></span>

![Azure Portal에서 가상 머신 만들기](../media-drafts/3-azure-portal-create-vm.png)

<span data-ttu-id="3faf1-116">필요한 모든 옵션(빨간색 별표로 식별됨)이 채워지면 마법사 환경의 나머지 부분은 건너뛰고 아래쪽의 **검토 + 만들기** 단추를 통해 VM을 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-116">Once you fill in all the required options (identified with red stars), you can skip the remainder of the wizard experience and start creating the VM through the **Review + Create** button at the bottom.</span></span>

<span data-ttu-id="3faf1-117">**기본 사항** 섹션부터 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-117">We'll start with the **Basics** section.</span></span>

### <a name="configure-basic-vm-settings"></a><span data-ttu-id="3faf1-118">기본 VM 설정 구성</span><span class="sxs-lookup"><span data-stu-id="3faf1-118">Configure basic VM settings</span></span>

1. <span data-ttu-id="3faf1-119">VM 시간에 대해 요금을 청구해야 하는 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-119">Select the **Subscription** that should be billed for VM hours.</span></span>

1. <span data-ttu-id="3faf1-120">**리소스 그룹**에 대해 **새로 만들기**를 선택하고 리소스 그룹 이름으로 **ExerciseResources**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-120">For **Resource group**, select **Create new** and give the resource group the name **ExerciseResources**.</span></span>

> [!NOTE]
> <span data-ttu-id="3faf1-121">각 필드에서 설정과 탭을 변경하면 Azure에서 각 값의 유효성을 자동으로 검사하고 해당 값이 적절한 경우 옆에 녹색 확인 표시를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-121">As you change settings and tab out of each field Azure will validate each value automatically and place a green check-mark next to it when it's good.</span></span> <span data-ttu-id="3faf1-122">오류 표시기 위를 마우스로 가리키면 검색된 문제에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-122">You can hover over error indicators to get more information for issues it discovers.</span></span>

1. <span data-ttu-id="3faf1-123">**인스턴스 세부 정보** 섹션에서 VM 이름을 "test-vp-vm2"(비디오 프로세서 테스트 VM #2의 경우)와 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-123">In the **INSTANCE DETAILS** section, enter a name for your VM, such as "test-vp-vm2" (for Test Video Processor VM #2).</span></span>
    - <span data-ttu-id="3faf1-124">용도를 쉽게 식별할 수 있도록 리소스 이름을 표준화하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-124">It's best practice to standardize your resource names so you can easily identify their purpose.</span></span> <span data-ttu-id="3faf1-125">Windows VM 이름은 약간 제한됩니다. 즉 2-15자여야 하며, 숫자, 문자 및 대시로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-125">Windows VM names are a bit limited - they must be between 2 and 15 characters and be comprised of numbers, letters, and dashes.</span></span>

1. <span data-ttu-id="3faf1-126">가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-126">Select a region close to you.</span></span>

1. <span data-ttu-id="3faf1-127">**가용성 옵션**을 "없음"으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-127">Leave **Availability options** as "None".</span></span> <span data-ttu-id="3faf1-128">이 옵션은 계획되거나 계획되지 않은 유지 관리 이벤트 또는 중단을 처리하기 위해 여러 VM을 하나의 집합으로 그룹화하여 VM의 가용성을 높이는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-128">This option is used to ensure the VM is highly available by grouping multiple VMs together a set to deal with planned or unplanned maintenance events or outages.</span></span>

1. <span data-ttu-id="3faf1-129">이미지가 "Windows Server 2016 Datacenter"로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-129">Ensure the image is set to "Windows Server 2016 Datacenter".</span></span> <span data-ttu-id="3faf1-130">드롭다운 목록을 열어 사용 가능한 모든 옵션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-130">You can open the drop-down list to see all the options available.</span></span>

1. <span data-ttu-id="3faf1-131">**VM 디스크 유형** 필드에서 드롭다운 메뉴를 클릭하여 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-131">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="3faf1-132">**SSD**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-132">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="3faf1-133">**크기** 필드는 직접 편집할 수 없으며 DS1 기본 크기가 적용되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-133">The **Size** field is not directly editable and has a DS1 default size.</span></span> <span data-ttu-id="3faf1-134">**크기 변경** 링크를 클릭하여 다른 VM 크기를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-134">Click the **Change size** link to explore other VM sizes.</span></span> <span data-ttu-id="3faf1-135">결과 대화 상자에서 CPU 수, 이름 및 디스크 유형에 따라 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-135">The resulting dialog allows you to filter based on # of CPUs, Name, and Disk Type.</span></span> <span data-ttu-id="3faf1-136">완료되면 "표준 DS1 v2"(일반적으로 기본값)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-136">Select "Standard DS1 v2" (normally the default) when you are done.</span></span> <span data-ttu-id="3faf1-137">그러면 VM에 1개 CPU와 3.5GB 메모리가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-137">That will give the VM 1 CPU and 3.5 GB of memory.</span></span>

    > [!TIP]
    > <span data-ttu-id="3faf1-138">보기를 왼쪽으로 슬라이드하여 VM 설정(오른쪽의 새 창에서 열려 원래 창이 왼쪽으로 슬라이드됨)을 다시 표시한 다음 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-138">You can also just slide the view to the left to get back to the VM settings as it opened a new window off to the right and slid the window over to view it.</span></span>

1. <span data-ttu-id="3faf1-139">**관리자 액세스** 섹션에서 **사용자 이름** 필드를 VM에 로그인하는 데 사용할 사용자 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-139">In the **ADMINISTRATOR ACCESS** section, set the **Username** field to a username you will use to sign in to the VM.</span></span>

1. <span data-ttu-id="3faf1-140">**암호** 필드에 최소 12자 이상인 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-140">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="3faf1-141">소문자, 대문자, 숫자 및 특수 문자('\'' 또는 '-'이 아님) 중 세 가지가 하나씩 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-141">It must have three of the following: one lower case character, one uppercase character, one number, and one special character that is not '\' or '-'.</span></span> <span data-ttu-id="3faf1-142">나중에 필요하므로 기억하거나 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="3faf1-142">Use something you will remember or write it down, you will need it later.</span></span>

1. <span data-ttu-id="3faf1-143">**암호**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-143">Confirm the **password**.</span></span>

1. <span data-ttu-id="3faf1-144">**인바운드 포트 규칙** 섹션에서 목록을 열고 "없음"을 _선택 취소_합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-144">In the **INBOUND PORT RULES** section, open the list and _uncheck_ "None".</span></span> <span data-ttu-id="3faf1-145">Windows VM이므로 RDP를 사용하여 데스크톱에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-145">Since this is a Windows VM, we want to be able to access the desktop using RDP.</span></span> <span data-ttu-id="3faf1-146">필요한 경우 RDP(3389)를 찾을 때까지 목록을 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-146">Scroll the list if necessary until you find RDP (3389) and select it.</span></span> <span data-ttu-id="3faf1-147">UI의 참고 사항에서 언급한 대로 VM이 만들어지면 네트워크 포트를 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-147">As the note in the UI indicates, we can also adjust the network ports after we create the VM.</span></span>

    ![Windows VM에서 RDP 액세스를 위한 포트 열기](../media-drafts/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a><span data-ttu-id="3faf1-149">VM에 대한 디스크 구성</span><span class="sxs-lookup"><span data-stu-id="3faf1-149">Configure Disks for the VM</span></span>

1. <span data-ttu-id="3faf1-150">**다음**을 클릭하여 [디스크] 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-150">Click **Next** to move to the Disks section.</span></span>

    ![VM에 대한 디스크 구성](../media-drafts/3-configure-disks.png)

1. <span data-ttu-id="3faf1-152">**OS 디스크 유형**에 대해 "프리미엄 SSD"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-152">Choose "Premium SSD" for the **OS disk type**.</span></span>

1. <span data-ttu-id="3faf1-153">저장소 계정을 사용하지 않도록 관리 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-153">Use managed disks so we don't have to work with storage accounts.</span></span> <span data-ttu-id="3faf1-154">원하는 경우 Azure에 필요한 정보의 차이를 보기 위해 GUI에서 스위치를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-154">You can flip the switch in the GUI to see the difference in information that Azure needs if you like.</span></span>

### <a name="create-a-data-disk"></a><span data-ttu-id="3faf1-155">데이터 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="3faf1-155">Create a data disk</span></span>

<span data-ttu-id="3faf1-156">OS 디스크(C:)와 임시 디스크(D:)를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-156">Recall we will get an OS disk (C:) and Temporary disk (D:).</span></span> <span data-ttu-id="3faf1-157">데이터 디스크도 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-157">Let's add a data disk as well.</span></span>

1. <span data-ttu-id="3faf1-158">**데이터 디스크** 섹션에서 **새 디스크 만들기 및 연결** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-158">Click the **Create and attach a new disk** link in the **DATA DISKS** section.</span></span>

    ![포털에서 VM에 대한 데이터 디스크 만들기](../media-drafts/3-add-data-disk.png)

1. <span data-ttu-id="3faf1-160">여기서는 스냅숏 또는 Storage Blob을 사용하여 VHD를 만들 수 있지만 모든 기본값, 즉 프리미엄 SSD, 1023GB 및 없음(빈 디스크)을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-160">You can take all the defaults: Premium SSD, 1023 GB, and None (empty disk); although notice that here is where we could use a snapshot, or Storage Blob to create a VHD.</span></span>

1. <span data-ttu-id="3faf1-161">**확인**을 클릭하여 디스크를 만들고 **데이터 디스크** 섹션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-161">Click **OK** to create the disk and go back to the **DATA DISKS** section.</span></span>

1. <span data-ttu-id="3faf1-162">이제 첫 번째 행에 새 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-162">There should now be a new disk in the first row.</span></span>

    ![VM의 새 디스크](../media-drafts/3-new-disk.png)

## <a name="configure-the-network"></a><span data-ttu-id="3faf1-164">네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="3faf1-164">Configure the Network</span></span>

1. <span data-ttu-id="3faf1-165">**다음**을 클릭하여 [네트워킹] 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-165">Click **Next** to move to the Networking section.</span></span>

1. <span data-ttu-id="3faf1-166">이미 다른 구성 요소가 있는 프로덕션 시스템에서 _기존_ 가상 네트워크를 활용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-166">In a production system where we already have other components, we'd want to utilize an _existing_ virtual network.</span></span> <span data-ttu-id="3faf1-167">이렇게 하면 VM에서 솔루션의 다른 클라우드 서비스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-167">That way our VM can communicate with the other cloud services in our solution.</span></span> <span data-ttu-id="3faf1-168">이 위치에 정의된 가상 네트워크가 아직 없으면 여기서 만들고 다음 항목을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-168">If there isn't one defined in this location yet, we can create it here and configure the:</span></span>
    - <span data-ttu-id="3faf1-169">**주소 공간**: 이 네트워크에서 사용할 수 있는 전체 IPV4 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-169">**Address space**: the overall IPV4 space available to this network.</span></span>
    - <span data-ttu-id="3faf1-170">**서브넷 범위**: 주소 공간을 세분화할 첫 번째 서브넷이며,  정의된 주소 공간 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-170">**Subnet range**: the first subnet to subdivide the address space - it must fit within the defined address space.</span></span> <span data-ttu-id="3faf1-171">VNet이 만들어지면 추가 서브넷을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-171">Once the VNet is created you can add additional subnets.</span></span>

1. <span data-ttu-id="3faf1-172">`172.xxx` IP 주소 공간을 사용하도록 기본 범위를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-172">Let's change the default ranges to use the `172.xxx` IP address space.</span></span>
    - <span data-ttu-id="3faf1-173">**주소 공간** 필드를 `172.16.0.0/16`으로 변경하여 전체 주소 범위를 지정합니다</span><span class="sxs-lookup"><span data-stu-id="3faf1-173">Change the **Address space** field to be `172.16.0.0/16` to give it the full range of addresses</span></span>
    - <span data-ttu-id="3faf1-174">**서브넷 범위** 필드를 `172.16.1.0/24`로 변경하여 256개의 IP 주소 공간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-174">Change the **Subnet range** field to be `172.16.1.0/24` to give it 256 IP addresses of the space.</span></span>

> [!NOTE]
> <span data-ttu-id="3faf1-175">기본적으로 Azure는 VM에 대한 가상 네트워크, 네트워크 인터페이스 및 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-175">By default, Azure will create a virtual network, network interface, and public IP for your VM.</span></span> <span data-ttu-id="3faf1-176">VM을 만든 후에 네트워킹 옵션을 변경하는 것은 쉽지 않으므로 Azure에서 만든 서비스에 대한 네트워크 할당을 항상 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-176">It's not trivial to change the networking options after the VM has been created so always double-check the network assignments on services you create in Azure.</span></span>

## <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="3faf1-177">VM 구성 완료 및 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="3faf1-177">Finish configuring the VM and create the image</span></span>

<span data-ttu-id="3faf1-178">나머지 옵션에는 적절한 기본값이 있으므로 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-178">The rest of the options have reasonable defaults and there's no need to change any of them.</span></span> <span data-ttu-id="3faf1-179">원하는 경우 다른 탭을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-179">You can explore the other tabs if you like.</span></span> <span data-ttu-id="3faf1-180">개별 옵션 옆에는 해당 옵션을 설명하는 풍선형 도움말이 표시되는 `(i)` 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-180">The individual options have an `(i)` icon next to them that will show a help bubble to explain the option.</span></span> <span data-ttu-id="3faf1-181">이는 VM을 구성하는 데 사용할 수 있는 다양한 옵션에 대해 알아볼 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-181">This is a great way to learn about the various options you can use to configure the VM.</span></span>

1. <span data-ttu-id="3faf1-182">패널 아래쪽에서 **검토 + 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-182">Click the **Review + create** button at the bottom of the panel.</span></span>

1. <span data-ttu-id="3faf1-183">시스템에서 옵션의 유효성을 검사하고 만드는 VM에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-183">The system will validate your options and give you details about the VM being created.</span></span>

1. <span data-ttu-id="3faf1-184">**만들기**를 클릭하여 VM을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-184">Click **Create** to create and deploy the VM.</span></span> <span data-ttu-id="3faf1-185">Azure 대시보드에 배포 중인 VM이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-185">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="3faf1-186">이 작업은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-186">This may take several minutes.</span></span>

<span data-ttu-id="3faf1-187">VM이 배포되는 동안 이 VM으로 수행할 수 있는 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3faf1-187">While that's deploying, let's look at what we can do with this VM.</span></span>