<span data-ttu-id="ceead-101">이 연습에서는 가상 머신을 만들고 포털 및 Azure PowerShell을 사용하여 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-101">In this exercise, you will create a virtual machine and then resize it using the portal and Azure PowerShell.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="ceead-102">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ceead-102">Create a VM</span></span>

1. <span data-ttu-id="ceead-103">웹 브라우저에서 [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하고 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-103">In your web browser, navigate to the [Azure Portal](https://portal.azure.com?azure-portal=true) and sign into your account.</span></span>

1. <span data-ttu-id="ceead-104">Azure Portal에서 새 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-104">In the Azure portal, create a new resource.</span></span> <span data-ttu-id="ceead-105">**새로 만들기** 블레이드에서 검색 상자에 **가상 머신**를 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-105">In the **New** blade, type **virtual machine** in the search box, and then press ENTER.</span></span>

1. <span data-ttu-id="ceead-106">**모든 항목** 블레이드의 **결과** 아래에서 **Windows Server 2016 Datacenter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-106">In the **Everything** blade, under **Results**, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="ceead-107">**Windows Server 2016 Datacenter** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-107">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="ceead-108">**기본 사항** 블레이드에서 다음 정보를 사용하여 세부 정보를 작성한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-108">In the **Basics** blade, complete the details using the following information, and then click **OK**.</span></span>

    |<span data-ttu-id="ceead-109">설정</span><span class="sxs-lookup"><span data-stu-id="ceead-109">Setting</span></span>|<span data-ttu-id="ceead-110">값</span><span class="sxs-lookup"><span data-stu-id="ceead-110">Value</span></span>|
    |---|---|
    |<span data-ttu-id="ceead-111">이름</span><span class="sxs-lookup"><span data-stu-id="ceead-111">Name</span></span>|<span data-ttu-id="ceead-112">DB01</span><span class="sxs-lookup"><span data-stu-id="ceead-112">DB01</span></span>|
    |<span data-ttu-id="ceead-113">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="ceead-113">Username</span></span>|<span data-ttu-id="ceead-114">LocalAdmin</span><span class="sxs-lookup"><span data-stu-id="ceead-114">LocalAdmin</span></span>|
    |<span data-ttu-id="ceead-115">암호 및 암호 확인</span><span class="sxs-lookup"><span data-stu-id="ceead-115">Password and Confirm password</span></span>|<span data-ttu-id="ceead-116">Adm1nPa$$word</span><span class="sxs-lookup"><span data-stu-id="ceead-116">Adm1nPa$$word</span></span>|
    |<span data-ttu-id="ceead-117">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="ceead-117">Resource group</span></span>|<span data-ttu-id="ceead-118">ExerciseRG</span><span class="sxs-lookup"><span data-stu-id="ceead-118">ExerciseRG</span></span>|
    |<span data-ttu-id="ceead-119">위치</span><span class="sxs-lookup"><span data-stu-id="ceead-119">Location</span></span>|<span data-ttu-id="ceead-120">미국 중부</span><span class="sxs-lookup"><span data-stu-id="ceead-120">Central US</span></span>|

1. <span data-ttu-id="ceead-121">**크기 선택** 블레이드에서 **D2s_v3**을 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-121">On the **Choose a size** blade, select **D2s_v3**, and then click **Select**.</span></span>

1. <span data-ttu-id="ceead-122">**설정** 블레이드의 **공용 인바운드 포트 선택** 아래에서 **HTTP**, **HTTPS** 및 **RDP(3389)** 를 선택하고, **부트 진단** 아래에서 **사용 안 함**을 클릭하고, 모든 다른 설정을 기본값으로 유지한 후, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-122">On the **Settings** blade, under **Select public inbound ports** select **HTTP**, **HTTPS**, and **RDP (3389)**, under **Boot diagnostics** click **Disabled**, leave all other settings at the default value, and then click **OK**.</span></span>

1. <span data-ttu-id="ceead-123">**만들기** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-123">On the **Create** blade, click **Create**.</span></span>

1. <span data-ttu-id="ceead-124">배포가 완료될 때까지 기다린 후에 연습을 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="ceead-124">Wait until the deployment is complete before continuing the exercise.</span></span>

## <a name="resize-using-the-portal"></a><span data-ttu-id="ceead-125">포털을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="ceead-125">Resize using the portal</span></span>

1. <span data-ttu-id="ceead-126">Azure Portal에서 ExerciseRG 리소스 그룹으로 이동하고 **ExerciseRG** 블레이드에서 **DB01** 가상 머신 개체를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-126">In the Azure portal, browse to the ExerciseRG resource group, and in the **ExerciseRG** blade, click the **DB01** virtual machine object.</span></span>

1. <span data-ttu-id="ceead-127">**DB01** 블레이드에서 **크기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-127">On the **DB01** blade, click **Size**.</span></span> <span data-ttu-id="ceead-128">현재 강조 표시된 크기는 가상 머신을 만들 때 선택한 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-128">Note the currently highlighted size is the size you selected when creating the virtual machine.</span></span>

1. <span data-ttu-id="ceead-129">**크기 선택** 블레이드에서 **F2s_v2** 크기를 찾아보세요. VM이 현재 실행 중이고 해당 크기가 다른 패밀리에 속하므로 크기 목록에 이 크기가 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-129">On the **Choose a size** blade, try to find the **F2s_v2** size - it should not be available in the list of sizes because the VM is currently running and that size is from a different family.</span></span> <span data-ttu-id="ceead-130">**크기 선택** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-130">Close the **Choose a size** blade.</span></span>

1. <span data-ttu-id="ceead-131">**DB01** 블레이드에서 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-131">In the **DB01** blade, click **Stop**.</span></span> <span data-ttu-id="ceead-132">**이 가상 머신 중지** 대화 상자에서 **예**를 클릭하고 가상 머신 상태가 **중지됨(할당 취소됨)** 으로 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-132">In the **Stop this virtual machine** dialog box, click **Yes**, and wait for the virtual machine status to show **Stopped (deallocated)**.</span></span>

1. <span data-ttu-id="ceead-133">**DB01** 블레이드에서 **크기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-133">On the **DB01** blade, click **Size**.</span></span> <span data-ttu-id="ceead-134">**크기 선택** 블레이드에서 **F2s_v2**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-134">On the **Choose a size** blade, select **F2s_v2** and then click **Select**.</span></span> <span data-ttu-id="ceead-135">가상 머신의 크기 조정에 대한 알림을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ceead-135">Notice the notification about resizing the virtual machine.</span></span>

1. <span data-ttu-id="ceead-136">**DB01** 블레이드에서 **개요**를 클릭한 후 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-136">On the **DB01** blade, click **Overview**, then click **Start**.</span></span>

## <a name="resize-using-powershell"></a><span data-ttu-id="ceead-137">PowerShell을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="ceead-137">Resize using PowerShell</span></span>

1. <span data-ttu-id="ceead-138">Azure Portal에서 Cloud Shell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-138">In the Azure portal, open the Cloud Shell.</span></span>

1. <span data-ttu-id="ceead-139">다음 cmdlet을 사용하여 사용 가능한 가상 머신 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-139">Use the following cmdlet to get the list of available virtual machine sizes.</span></span>

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName ExerciseRG -VMName DB01
    ```

1. <span data-ttu-id="ceead-140">다음 cmdlet을 실행하여 가상 머신의 크기를 F4s_v2 크기로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-140">Use the following cmdlet to resize the virtual machine to an F4s_v2 size.</span></span>

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName ExerciseRG -VMName DB01
    $vm.HardwareProfile.VmSize = "Standard_F4s_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName ExerciseRG
    ```

1. <span data-ttu-id="ceead-141">PowerShell 명령이 완료될 때까지 기다리는 동안 DB01 블레이드에서 [새로 고침] 단추를 클릭합니다. 가상 머신이 변경된 크기를 적용하도록 다시 시작되고 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-141">Click the Refresh button in the DB01 blade while you are waiting for the PowerShell command to complete - you should notice that the virtual machine is restarting to accommodate the change in size.</span></span>

<span data-ttu-id="ceead-142">이 연습에서는 가상 머신을 만들고 두 개의 다른 도구로 크기를 조정했습니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-142">In this exercise, you created a virtual machine and resized it with two different tools.</span></span> <span data-ttu-id="ceead-143">가상 머신이 실행되는 동안에는 대상 크기를 사용할 수 없다는 점을 기억하는 것이 좋습니다. 가상 머신을 중지하면 더 많은 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceead-143">A good tip to keep in mind is that the target size may not be available while the virtual machine is running; stopping the virtual machine lets you choose more sizes.</span></span>