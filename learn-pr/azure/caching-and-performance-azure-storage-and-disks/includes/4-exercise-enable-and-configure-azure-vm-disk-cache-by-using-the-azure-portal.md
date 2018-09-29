
<span data-ttu-id="86484-101">SQL Server 및 사용자 지정 응용 프로그램을 실행하는 Azure VM(Virtual Machines)에 저장된 데이터를 사용하여 사진 공유 사이트를 실행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-101">Suppose you run a photo sharing site, with data stored on Azure virtual machines (VMs) running SQL Server and custom applications.</span></span> <span data-ttu-id="86484-102">다음 조정을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-102">You want to make the following adjustments:</span></span>

- <span data-ttu-id="86484-103">VM에서 디스크 캐시 설정을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-103">You need to change the disk cache settings on a VM.</span></span>
- <span data-ttu-id="86484-104">캐싱을 사용하도록 설정한 VM에 새 데이터 디스크를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-104">You want to add a new data disk to the VM with caching enabled.</span></span>

<span data-ttu-id="86484-105">Azure Portal을 통해 이렇게 변경하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-105">You've decided to make these changes through the Azure portal.</span></span>

<span data-ttu-id="86484-106">이 연습에서는 위에서 설명한 VM을 변경하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="86484-106">In this exercise, we'll walk through making the changes to a VM that we described above.</span></span> <span data-ttu-id="86484-107">먼저 포털에 로그인하고 VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-107">First, let's sign in to the portal and create a VM.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-virtual-machine"></a><span data-ttu-id="86484-108">가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="86484-108">Create a virtual machine</span></span>

<span data-ttu-id="86484-109">이 단계에서는 다음 속성을 사용하여 VM을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-109">In this step, we're going to create a VM with the following properties:</span></span>

| <span data-ttu-id="86484-110">속성</span><span class="sxs-lookup"><span data-stu-id="86484-110">Property</span></span>        | <span data-ttu-id="86484-111">값</span><span class="sxs-lookup"><span data-stu-id="86484-111">Value</span></span>   |
|-----------------|---------|
| <span data-ttu-id="86484-112">이미지</span><span class="sxs-lookup"><span data-stu-id="86484-112">Image</span></span>           | <span data-ttu-id="86484-113">**Windows Server 2016 Datacenter**</span><span class="sxs-lookup"><span data-stu-id="86484-113">**Windows Server 2016 Datacenter**</span></span> |
| <span data-ttu-id="86484-114">이름</span><span class="sxs-lookup"><span data-stu-id="86484-114">Name</span></span>            | <span data-ttu-id="86484-115">**fotoshareVM**</span><span class="sxs-lookup"><span data-stu-id="86484-115">**fotoshareVM**</span></span> |
| <span data-ttu-id="86484-116">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="86484-116">Resource group</span></span>  |   <span data-ttu-id="86484-117">**<rgn>[샌드박스 리소스 그룹 이름]</rgn>**</span><span class="sxs-lookup"><span data-stu-id="86484-117">**<rgn>[sandbox resource group name]</rgn>**</span></span> |
| <span data-ttu-id="86484-118">위치</span><span class="sxs-lookup"><span data-stu-id="86484-118">Location</span></span>        | <span data-ttu-id="86484-119">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86484-119">See below.</span></span> |

1. <span data-ttu-id="86484-120">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-120">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="86484-121">왼쪽에 있는 사이드바 메뉴에서 **리소스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-121">Select **Create a resource** in the sidebar menu on the left.</span></span>

1. <span data-ttu-id="86484-122">_Windows Server 2016 VM_은 **인기 있는** Marketplace 요소 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86484-122">_Windows Server 2016 VM_ should be in the list of **Popular** Marketplace elements.</span></span> <span data-ttu-id="86484-123">그렇지 않으면 위쪽의 검색 상자를 사용하여 "Windows Server 2016 DataCenter"를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="86484-123">If not, try searching for "Windows Server 2016 DataCenter" using the search box on the top.</span></span>

1. <span data-ttu-id="86484-124">Windows VM을 선택하고, **만들기**를 클릭하여 VM 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-124">Select the Windows VM and click **Create** to start the VM creation process.</span></span>

1. <span data-ttu-id="86484-125">**기본 사항** 패널에서 선택한 **구독**이 _컨시어지 구독_인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-125">In the **Basics** panel, verify the selected **Subscription** is _Concierge Subscription_.</span></span>

1. <span data-ttu-id="86484-126">**리소스 그룹**에서 **기존 리소스 그룹 사용**을 선택하고 _<rgn>[샌드박스 리소스 그룹 이름]</rgn>_ 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-126">Under **Resource Group**, select **Use Existing** and choose _<rgn>[sandbox resource group name]</rgn>_.</span></span>

1. <span data-ttu-id="86484-127">**가상 머신 이름** 상자에 _fotoshareVM_을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-127">In the **Virtual machine name** box, enter _fotoshareVM_.</span></span>

1. <span data-ttu-id="86484-128">**위치** 드롭다운 목록에서 다음 목록 중 가장 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-128">In the **Location** drop-down list, select the closest region to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="86484-129">VM **크기**에서 기본값은 **DS1 v2**이며 단일 CPU 및 3.5GB의 메모리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-129">For the VM **Size**, the default is **DS1 v2** which gives you a single CPU and 3.5 GB of memory.</span></span> <span data-ttu-id="86484-130">이 예제에서는 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-130">That's fine for this example.</span></span>

1. <span data-ttu-id="86484-131">**관리자 계정** 섹션에서 새 VM에서 관리자 계정의 **사용자 이름** 및 **암호**/**암호 확인**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-131">In **ADMINISTRATOR ACCOUNT** section, enter a **Username** and **Password**/**Confirm password** for an administrator account on the new VM.</span></span>

1. <span data-ttu-id="86484-132">작성 시 **기본 사항** 구성이 다음 이미지와 같이 표시될 수 있습니다. 나머지 탭 및 필드에 대한 기본값을 그대로 두고, **검토 + 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-132">The following image is an example of what the **Basics** configuration looks like when filled out. Leave the defaults for the remaining tabs and fields and click **Review + create**.</span></span>

    ![설명된 대로 채워진 일부 예제 기본 구성을 사용하여 가상 머신 만들기 블레이드를 보여주는 Azure Portal의 스크린샷](../media/4-basics-vm.png)

1. <span data-ttu-id="86484-134">새 VM 설정을 검토한 후에 **만들기**를 클릭하여 새 VM을 배포하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-134">After reviewing your new VM settings, click **Create** to start the deploying your new VM.</span></span>

<span data-ttu-id="86484-135">모든 다양한 리소스(저장소, 네트워크 인터페이스 등)를 만들어서 가상 머신을 지원하므로 VM을 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-135">VM creation can take a few minutes as it creates all the various resources (storage, network interface, etc.) to support the virtual machine.</span></span> <span data-ttu-id="86484-136">VM이 배포될 때까지 기다렸다가 연습을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-136">Wait until the VM has deployed before continuing with the exercise.</span></span>

## <a name="view-os-disk-cache-status-in-the-portal"></a><span data-ttu-id="86484-137">포털에서 OS 디스크 캐시 상태 보기</span><span class="sxs-lookup"><span data-stu-id="86484-137">View OS disk cache status in the portal</span></span>

<span data-ttu-id="86484-138">VM이 배포되면 다음 단계를 사용하여 OS 디스크의 캐싱 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-138">Once our VM is deployed, we can confirm the caching status of the OS disk using the following steps:</span></span>

1. <span data-ttu-id="86484-139">**fotoshareVM** 리소스를 선택하여 포털에서 VM 세부 정보를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="86484-139">Select the **fotoshareVM** resource to open the VM details in the portal.</span></span> <span data-ttu-id="86484-140">또는 왼쪽 사이드바에서 **모든 리소스**를 클릭한 다음, **fotoshareVM** VM을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-140">Alternatively, you can click **All resources** in the left sidebar, and then select your VM, **fotoshareVM**.</span></span>

1. <span data-ttu-id="86484-141">**설정**에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-141">Under **Settings**, select **Disks**.</span></span>

1. <span data-ttu-id="86484-142">**디스크** 창에서 VM에는 하나의 OS 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-142">On the **Disks** pane, the VM has one disk, the OS disk.</span></span> <span data-ttu-id="86484-143">캐시 형식은 현재 **읽기/쓰기**의 기본값으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-143">Its cache type is currently set to the default value of **Read/write**.</span></span>

![OS 디스크가 표시되고 읽기 전용 캐싱로 설정된 VM 블레이드의 디스크 섹션을 보여주는 Azure Portal의 스크린샷](../media/4-os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a><span data-ttu-id="86484-145">포털에서 OS 디스크의 캐시 설정 변경</span><span class="sxs-lookup"><span data-stu-id="86484-145">Change the cache settings of the OS disk in the portal</span></span>

1. <span data-ttu-id="86484-146">**디스크** 창의 화면 왼쪽 위에 있는 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-146">On the **Disks** pane, select **Edit** in the upper left of the screen.</span></span>

1. <span data-ttu-id="86484-147">드롭다운 목록을 사용하여 OS 디스크의 **호스트 캐싱** 값을 **읽기 전용**으로 변경한 다음, 화면 왼쪽 위에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-147">Change the **HOST CACHING** value for the OS disk to **Read-only** using the drop-down list, and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="86484-148">이 업데이트에 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-148">This update can take some time.</span></span> <span data-ttu-id="86484-149">그 이유는 Azure 디스크의 캐시 설정이 변경되면 대상 디스크를 분리하고 다시 연결하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="86484-149">The reason is that changing the cache setting of an Azure disk detaches and reattaches the target disk.</span></span> <span data-ttu-id="86484-150">운영 체제 디스크인 경우 VM도 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="86484-150">If it's the operating system disk, the VM is also restarted.</span></span> <span data-ttu-id="86484-151">작업이 완료되면 VM 디스크가 업데이트되었다는 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86484-151">When the operation completes, you'll get a notification saying the VM disks have been updated.</span></span>

1. <span data-ttu-id="86484-152">작업이 완료되면 OS 디스크 캐시 형식이 **읽기 전용**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="86484-152">Once complete, the OS disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="86484-153">데이터 디스크 캐시 구성으로 이동하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-153">Let's move on to data disk cache configuration.</span></span> <span data-ttu-id="86484-154">디스크를 구성하려면 먼저 디스크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-154">To configure a disk, we'll need first to create one.</span></span>

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a><span data-ttu-id="86484-155">VM에 데이터 디스크 추가 및 캐싱 형식 설정</span><span class="sxs-lookup"><span data-stu-id="86484-155">Add a data disk to the VM and set caching type</span></span>

1. <span data-ttu-id="86484-156">포털에서 VM의 **디스크** 보기로 돌아가서 **데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-156">Back on the **Disks** view of our VM in the portal, go ahead and click **Add data disk**.</span></span> <span data-ttu-id="86484-157">필드가 비어 있을 수 없음을 알리는 오류가 **이름** 필드에 바로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86484-157">An error immediately appears in the **Name** field, telling us that the field can't be empty.</span></span> <span data-ttu-id="86484-158">아직 데이터 디스크가 없으므로 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-158">We don't have a data disk yet, so let's create one.</span></span>

1. <span data-ttu-id="86484-159">**이름** 목록을 클릭하고 **디스크 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-159">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="86484-160">**관리 디스크 만들기** 창의 **이름** 상자에 **fotosharesVM-data**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-160">In the **Create managed disk** pane, in the **Name** box, type **fotosharesVM-data**.</span></span>

1. <span data-ttu-id="86484-161">**리소스 그룹**에서 **기존 항목 사용**을 선택하고 _<rgn>[샌드박스 리소스 그룹 이름]</rgn>_ 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-161">Under **Resource Group**, select **Use existing**, and select _<rgn>[sandbox resource group name]</rgn>_.</span></span>

1. <span data-ttu-id="86484-162">나머지 필드의 기본값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="86484-162">Note the defaults for the remaining fields:</span></span>
    - <span data-ttu-id="86484-163">프리미엄 SSD</span><span class="sxs-lookup"><span data-stu-id="86484-163">Premium SSD</span></span>
    - <span data-ttu-id="86484-164">크기 1023GB</span><span class="sxs-lookup"><span data-stu-id="86484-164">1023 GB in size</span></span>
    - <span data-ttu-id="86484-165">VM과 동일한 위치(변경할 수 없음)</span><span class="sxs-lookup"><span data-stu-id="86484-165">In the same location as the VM (not changeable).</span></span>
    - <span data-ttu-id="86484-166">IOPS 제한 - 5000</span><span class="sxs-lookup"><span data-stu-id="86484-166">IOPS limit - 5000</span></span>
    - <span data-ttu-id="86484-167">처리량 제한(MB/s) - 200</span><span class="sxs-lookup"><span data-stu-id="86484-167">Throughput limit (MB/s) - 200</span></span>

1. <span data-ttu-id="86484-168">화면의 맨 아래에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-168">Click **Create** at the bottom of the screen.</span></span>

    <span data-ttu-id="86484-169">디스크가 만들어질 때까지 기다렸다가 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-169">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="86484-170">드롭다운 목록을 사용하여 새 데이터 디스크의 **호스트 캐싱** 값을 **읽기 전용**으로 변경한 다음(이미 설정되었을 수 있음), 화면 왼쪽 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86484-170">Change the **HOST CACHING** value for our new data disk to **Read-only** using the drop-down list (it might be set already), and then click **Save** in the upper left of the screen.</span></span>

    <span data-ttu-id="86484-171">VM이 새 데이터 디스크의 업데이트를 완료할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="86484-171">Wait for the VM to finish updating the new data disk.</span></span> <span data-ttu-id="86484-172">작업이 완료되면 가상 머신에 새 데이터 디스크가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="86484-172">Once complete, you will have a new data disk on your virtual machine.</span></span>

<span data-ttu-id="86484-173">이 연습에서는 Azure Portal을 사용하여 새 VM에서 캐싱을 구성하고, 기존 디스크에서 캐시 설정을 변경하고, 새 데이터 디스크에서 캐싱을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="86484-173">In this exercise, we used the Azure portal to configure caching on a new VM, change cache settings on an existing disk, and configure caching on a new data disk.</span></span> <span data-ttu-id="86484-174">다음 스크린샷은 최종 구성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="86484-174">The following screenshot shows the final configuration:</span></span>

![읽기 전용 캐싱로 설정된 VM 블레이드의 디스크 섹션의 OS 디스크 및 새 데이터 디스크를 보여주는 Azure Portal의 스크린샷](../media/disks-final-config-portal.PNG)
