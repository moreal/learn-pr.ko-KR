<span data-ttu-id="177c7-101">SQL Server 및 사용자 지정 응용 프로그램을 실행하는 Azure VM(Virtual Machines)에 저장된 데이터를 사용하여 사진 공유 사이트를 실행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-101">Suppose you run a photo sharing site, with data stored on Azure virtual machines (VMs) running SQL Server and custom applications.</span></span> <span data-ttu-id="177c7-102">다음 조정을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-102">You want to make the following adjustments.</span></span>

- <span data-ttu-id="177c7-103">VM에서 디스크 캐시 설정을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-103">You need change the disk cache settings on a VM</span></span>
- <span data-ttu-id="177c7-104">캐싱을 사용으로 설정한 VM에 새 데이터 디스크를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-104">You want dd a new data disk to the VM with caching enabled</span></span>

<span data-ttu-id="177c7-105">Azure Portal을 통해 이러한 변경 내용을 적용하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-105">You've decided to make these changes through the Azure portal.</span></span>

<span data-ttu-id="177c7-106">이 연습에서는 위에서 설명한 VM을 변경하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-106">In this exercise, we'll walk through making the changes to a VM that we described above.</span></span> <span data-ttu-id="177c7-107">먼저 포털에 로그인하고 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-107">First, let's sign in to the portal and create a VM.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="177c7-108">Azure Portal에 로그인</span><span class="sxs-lookup"><span data-stu-id="177c7-108">Sign in to the Azure portal</span></span>
<!---TODO: Update for sandbox?--->

1. <span data-ttu-id="177c7-109">[Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-109">Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="177c7-110">가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="177c7-110">Create a virtual machine</span></span>

<span data-ttu-id="177c7-111">이 단계에서는 다음 속성을 사용하여 VM을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-111">In this step, we're going to create a VM with the following properties.</span></span>

|<span data-ttu-id="177c7-112">속성</span><span class="sxs-lookup"><span data-stu-id="177c7-112">Property</span></span>  |<span data-ttu-id="177c7-113">값</span><span class="sxs-lookup"><span data-stu-id="177c7-113">Value</span></span>  |
|---------|---------|
|<span data-ttu-id="177c7-114">이미지</span><span class="sxs-lookup"><span data-stu-id="177c7-114">Image</span></span>     |   <span data-ttu-id="177c7-115">**Windows Server 2016 Datacenter**</span><span class="sxs-lookup"><span data-stu-id="177c7-115">**Windows Server 2016 Datacenter**</span></span>      |
|<span data-ttu-id="177c7-116">이름</span><span class="sxs-lookup"><span data-stu-id="177c7-116">Name</span></span>     |   <span data-ttu-id="177c7-117">**fotoshareVM**</span><span class="sxs-lookup"><span data-stu-id="177c7-117">**fotoshareVM**</span></span>     |
|<span data-ttu-id="177c7-118">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="177c7-118">Resource group</span></span>     |   <span data-ttu-id="177c7-119">**fotoshare-rg**</span><span class="sxs-lookup"><span data-stu-id="177c7-119">**fotoshare-rg**</span></span>      |


1. <span data-ttu-id="177c7-120">포털의 왼쪽 메뉴에서 **가상 머신**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-120">In the left menu of the portal, select **Virtual machines**</span></span>

1. <span data-ttu-id="177c7-121">이제 **가상 머신** 화면의 왼쪽 위에 있는 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-121">Now select **+ Add** in the top left of the **Virtual machines** screen.</span></span> <span data-ttu-id="177c7-122">이 작업은 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-122">This action starts the creation process.</span></span>

1. <span data-ttu-id="177c7-123">사용 가능한 VM 이미지를 나열하는 [계산] 패널에서 검색 상자에 *Windows Server 2016 Datacenter*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-123">On the Compute panel that lists available VM images, type *Windows Server 2016 Datacenter* into the search box.</span></span>

1. <span data-ttu-id="177c7-124">검색 결과에서 **Windows Server 2016 Datacenter**를 선택한 후 **만들기**를 선택하여 VM 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-124">Select **Windows Server 2016 Datacenter** from the search results and then select **Create** to start the VM creation process.</span></span>

1. <span data-ttu-id="177c7-125">**기본 사항** 패널의 **이름** 상자에 **fotoshareVM**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-125">In the **Basics** panel, in the **Name** box, enter **fotoshareVM**</span></span>

1. <span data-ttu-id="177c7-126">**사용자 이름** 및 **암호** 상자에 이 서버의 관리자 계정 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-126">In the **Username** and **Password boxes**, enter a name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="177c7-127">**구독** 드롭다운에서 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-127">In the **Subscription** dropdown, select your Azure subscription.</span></span>

1. <span data-ttu-id="177c7-128">**리소스 그룹**에서 **새로 만들기**를 선택하고 상자에 **fotoshare-rg**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-128">Under **Resource Group**, select **Create new**, and in the box, type **fotoshare-rg**.</span></span>

1. <span data-ttu-id="177c7-129">**위치** 드롭다운 목록에서 인근 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-129">In the **Location** drop-down list, select a region near you.</span></span>

<span data-ttu-id="177c7-130">작성 시 **기본 사항** 구성이 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-130">The following is an example of what the **Basics** configuration looks like when filled out.</span></span>

![작성된 VM 기본 사항 구성의 스크린샷입니다.](../media-draft/vm-basics-settings.PNG)

1. <span data-ttu-id="177c7-132">**확인**을 선택하여 다음 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-132">Select **OK** to move onto the next step.</span></span>

<span data-ttu-id="177c7-133">이제 VM의 크기를 선택한 후 배포를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-133">You now need to choose a size for the VM, and then start the deployment:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="177c7-134">L 시리즈 및 B 시리즈 가상 머신에 대한 디스크 캐싱은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-134">Remember that disk caching can't be changed for L-Series and B-series virtual machines.</span></span> <span data-ttu-id="177c7-135">다른 크기를 선택하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-135">We'll select a different size.</span></span>

1. <span data-ttu-id="177c7-136">**크기 선택** 섹션에서 **표준** SKU(예: **F1s**)를 선택하고 **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-136">In the **Choose a size** section, select a **Standard** SKU, such as **F1s**, and then choose **Select**.</span></span>

1. <span data-ttu-id="177c7-137">**설정** 창을 아래로 스크롤하여 디스크 캐싱을 구성할 옵션이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-137">Scroll down the **Settings** pane and observe that there is no option to configure disk caching.</span></span> <span data-ttu-id="177c7-138">이 단계의 기본값을 그대로 사용하고 창의 맨 아래에서 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-138">Let's accept the defaults on this step and choose **OK** at the bottom of the pane.</span></span>

1. <span data-ttu-id="177c7-139">**만들기** 패널에서 요약을 검토한 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-139">On the **Create** panel, review the summary, and then choose **Create**.</span></span>

1. <span data-ttu-id="177c7-140">VM 만들기는 시간이 어느 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-140">VM creation can take a while.</span></span> <span data-ttu-id="177c7-141">VM이 배포될 때까지 기다렸다가 연습을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-141">Wait until the VM has deployed before continuing with the exercise.</span></span> <span data-ttu-id="177c7-142">프로세스가 완료되면 알림 허브에 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-142">You'll get a message in the Notification hub when the process is complete.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="177c7-143">다음 단원에서는 이 VM을 사용하므로 잠시 동안 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-143">We'll use this VM in the next lesson, so keep it around for a while!</span></span>

## <a name="view-os-disk-cache-status-in-the-portal"></a><span data-ttu-id="177c7-144">포털에서 OS 디스크 캐시 상태 보기</span><span class="sxs-lookup"><span data-stu-id="177c7-144">View OS disk cache status in the portal</span></span>

<span data-ttu-id="177c7-145">VM이 배포되면 다음 단계를 사용하여 OS 디스크의 캐싱 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-145">Once our VM is deployed, we can confirm the caching status of the OS disk using the following steps.</span></span>

1. <span data-ttu-id="177c7-146">왼쪽 메뉴에서 **모든 리소스**를 클릭한 후 VM **fotoshareVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-146">In the left menu, click **All resources**, and then select your VM,  **fotoshareVM**.</span></span>

1. <span data-ttu-id="177c7-147">**가상 머신** 화면의 **설정** 아래에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-147">On the **Virtual machine** screen, under **SETTINGS**, select **Disks**.</span></span>

1. <span data-ttu-id="177c7-148">**디스크** 창에서 VM에는 하나의 OS 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-148">On the **Disks** pane, the VM has one disk, the OS disk.</span></span> <span data-ttu-id="177c7-149">캐시 유형은 현재 기본값 **읽기/쓰기**로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-149">Its cache type is currently set to the default value of **Read/write**.</span></span>

![둘 다 읽기 전용 캐싱으로 설정된 OS 및 데이터 디스크의 스크린샷입니다.](../media-draft/os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a><span data-ttu-id="177c7-151">포털에서 OS 디스크의 캐시 설정 변경</span><span class="sxs-lookup"><span data-stu-id="177c7-151">Change the cache settings of the OS disk in the portal</span></span>

1. <span data-ttu-id="177c7-152">**디스크** 창의 화면 왼쪽 위에 있는 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-152">On the **Disks** pane, select **Edit** in the upper left of the screen.</span></span>

1. <span data-ttu-id="177c7-153">드롭다운을 사용하여 OS 디스크의 **호스트 캐싱** 값을 **읽기 전용**으로 변경한 후 화면 왼쪽 위에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-153">Change the **HOST CACHING** value for the OS disk to **Read-only** using the dropdown and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="177c7-154">이 업데이트는 시간이 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-154">This update takes a while.</span></span> <span data-ttu-id="177c7-155">그 이유는 Azure 디스크의 캐시 설정이 변경되면 대상 디스크를 분리하고 다시 연결하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-155">The reason is that changing the cache setting of an Azure disk detaches and reattaches the target disk.</span></span> <span data-ttu-id="177c7-156">운영 체제 디스크인 경우 VM도 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-156">If it's the operating system disk, the VM is also restarted.</span></span> <span data-ttu-id="177c7-157">업데이트가 완료되면 다음 알림과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-157">You'll get a message similar to the following notification when the update has finished.</span></span>

![캐시 설정 업데이트가 완료될 때 표시되는 알림의 예입니다.](../media-draft/vm-disk-update-complete.PNG)

4. <span data-ttu-id="177c7-159">완료된 후 OS 디스크 캐시 유형이 **읽기 전용**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-159">Once complete, the OS disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="177c7-160">데이터 디스크 캐시 구성으로 이동하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-160">Let's move on to data disk cache configuration.</span></span> <span data-ttu-id="177c7-161">디스크를 구성하려면 먼저 디스크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-161">To configure a disk, we'll need to first create one.</span></span>

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a><span data-ttu-id="177c7-162">VM에 데이터 디스크 추가 및 캐싱 유형 설정</span><span class="sxs-lookup"><span data-stu-id="177c7-162">Add a data disk to the VM and set caching type</span></span>

1. <span data-ttu-id="177c7-163">포털에서 VM의 **디스크** 보기로 돌아가서 **데이터 디스크 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-163">Back on the **Disks** view of our VM in the portal, go ahead and select **Add data disk**.</span></span> <span data-ttu-id="177c7-164">필드가 비어 있을 수 없음을 알리는 오류가 **이름** 필드에 바로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-164">An error immediately appears in the **Name** field telling us that the field can't be empty.</span></span> <span data-ttu-id="177c7-165">아직 데이터 디스크가 없으므로 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-165">We don't have a data disk yet, so let's create one.</span></span>

1. <span data-ttu-id="177c7-166">**이름** 목록을 클릭하고 **디스크 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-166">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="177c7-167">**관리 디스크 만들기** 창의 **이름** 상자에 **fotosharesVM-data**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-167">In the **Create managed disk** pane, in the **Name** box, type **fotosharesVM-data**.</span></span>

1. <span data-ttu-id="177c7-168">**리소스 그룹** 아래에서 **기존 항목 사용**을 선택하고 드롭다운 메뉴에서 **fotoshare-rg**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-168">Under **Resource Group**, select **Use existing**, and select **fotoshare-rg** from the dropdown menu.</span></span>

1. <span data-ttu-id="177c7-169">화면 아래쪽에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-169">Select **Create** at the bottom of the screen.</span></span>

1. <span data-ttu-id="177c7-170">디스크가 만들어질 때까지 기다렸다가 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-170">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="177c7-171">드롭다운을 사용하여 새 데이터 디스크의 **호스트 캐싱** 값을 **읽기 전용**으로 변경한 후 화면 왼쪽 위에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-171">Change the **HOST CACHING** value for our new data disk to **Read-only** using the dropdown and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="177c7-172">VM이 업데이트될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-172">Wait for the VM to update.</span></span> <span data-ttu-id="177c7-173">Azure가 이 설정을 변경하기 위해 데이터 디스크를 분리했다가 다시 연결하기 때문에 업데이트는 시간이 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-173">Updating takes a while because Azure detaches and reattaches the data disk to change this setting.</span></span>

1. <span data-ttu-id="177c7-174">완료된 후 데이터 디스크 캐시 유형이 **읽기 전용**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-174">Once complete, the data disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="177c7-175">이 연습에서는 Azure Portal을 사용하여 새 VM에서 캐싱을 구성하고, 기존 디스크에서 캐시 설정을 변경하고, 새 데이터 디스크에서 캐싱을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-175">In this exercise, we used the Azure portal to configure caching on a new VM, change cache settings on an existing disk, and to configure caching on a new data disk.</span></span> <span data-ttu-id="177c7-176">다음 스크린샷은 최종 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="177c7-176">The following screenshot shows the final configuration.</span></span> 

![둘 다 읽기 전용 캐싱으로 설정된 OS 및 데이터 디스크의 스크린샷입니다.](../media-draft/disks-final-config-portal.PNG)