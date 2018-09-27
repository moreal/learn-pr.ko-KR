<span data-ttu-id="e8ccf-101">이 연습에서는 가상 머신을 만든 다음, 포털 및 Azure PowerShell을 사용하여 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-101">In this exercise, you will create a virtual machine and then resize it using the portal and Azure PowerShell.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-vm-with-powershell"></a><span data-ttu-id="e8ccf-102">PowerShell을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e8ccf-102">Create a VM with PowerShell</span></span>

1. <span data-ttu-id="e8ccf-103">Azure PowerShell에서 `New-AzureRmVm` cmdlet을 사용하여 VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-103">Let's use the `New-AzureRmVm` cmdlet in Azure PowerShell to create a VM.</span></span>
    - <span data-ttu-id="e8ccf-104">리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-104">Use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span>
    - <span data-ttu-id="e8ccf-105">"my-test-vm"의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-105">Name it "my-test-vm".</span></span>
    - <span data-ttu-id="e8ccf-106">**크기** 매개 변수에 대해 _Standard_DS2_v2_를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-106">Pass in _Standard_DS2_v2_ for the **Size** parameter.</span></span>
    - <span data-ttu-id="e8ccf-107">Azure 샌드박스에서 사용할 수 있는 다음 목록 중에서 사용자에게 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-107">Select a location close to you from the following list available in the Azure sandbox.</span></span> <span data-ttu-id="e8ccf-108">복사해서 붙여넣을 경우 아래 명령 예제에서 값을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-108">Make sure to change the value in the below example command if you are using copy and paste.</span></span>

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - <span data-ttu-id="e8ccf-109">`Get-Credential` cmdlet을 사용하고, 아래에 표시된 대로 `Credential` 매개 변수에 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-109">Use the `Get-Credential` cmdlet and feed the results into the `Credential` parameter as shown below.</span></span>

       <span data-ttu-id="e8ccf-110">자격 증명을 입력하라는 메시지가 표시되면 LocalAdmin을 사용자 이름으로 사용하고, Adm1nPa$$word를 암호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-110">When prompted to enter credentials, use LocalAdmin as the user name and Adm1nPa$$word as the password.</span></span>

    ```powershell
    New-AzureRmVm `
        -ResourceGroupName <rgn>[sandbox resource group name]</rgn> `
        -Name my-test-vm `
        -Credential (Get-Credential) `
        -Size "Standard_DS2_v2" `
        -Location eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


1. <span data-ttu-id="e8ccf-111">배포가 완료될 때까지 기다린 후에 연습을 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-111">Wait until the deployment is complete before continuing the exercise.</span></span>

## <a name="resize-using-the-portal"></a><span data-ttu-id="e8ccf-112">포털을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e8ccf-112">Resize using the portal</span></span>

1. <span data-ttu-id="e8ccf-113">샌드박스를 활성화한 동일한 계정을 사용하여 [샌드박스용 Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-113">Sign into the [Azure portal for sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="e8ccf-114">왼쪽 사이드바에서 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-114">Select **Resource Groups** from the left side bar.</span></span>

1. <span data-ttu-id="e8ccf-115"><rgn>[샌드박스 리소스 그룹 이름]</rgn> 리소스 그룹을 선택하고, 개요에서 **my-test-vm** 가상 머신 개체를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-115">Select the <rgn>[sandbox resource group name]</rgn> resource group, and in the overview, click the **my-test-vm** virtual machine object.</span></span>

1. <span data-ttu-id="e8ccf-116">가상 머신의 **개요**에서 현재 VM 크기는 조금 전에 만든 대로 _표준 DS2 v2(2개 vCPU, 7GB 메모리)_ 입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-116">On the **Overview** of the virtual machine, notice that the current size of the VM is _Standard DS2 v2 (2 vcpus, 7 GB memory)_ which is what we created a moment ago.</span></span>

1. <span data-ttu-id="e8ccf-117">**설정** 섹션에서 **크기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-117">In the **Settings** section, select **Size**.</span></span>

1. <span data-ttu-id="e8ccf-118">**크기 선택** 블레이드에서 **F2s_v2** 크기를 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-118">On the **Choose a size** blade, try to find the **F2s_v2** size.</span></span> <span data-ttu-id="e8ccf-119">VM이 현재 실행 중이고 해당 크기는 다양한 제품군이 있으므로 사용 가능한 크기 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-119">You will not see it in the list of available sizes because the VM is currently running and that size is from a different family.</span></span> <span data-ttu-id="e8ccf-120">경우에 따라 사용 가능한 모든 VM 크기를 확인하기 위해 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-120">In some cases, you will need to stop the VM in order to see all available VM sizes.</span></span>

1. <span data-ttu-id="e8ccf-121">이 VM이 실행되는 동안 현재 사용할 수 있는 크기를 선택하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-121">Let's choose a size that is currently available while this VM is running.</span></span> <span data-ttu-id="e8ccf-122">**크기 선택** 블레이드에서 작업하는 동안 _DS3_v2 표준_을 선택한 다음, **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-122">While still on the **Choose a size** blade, select _DS3_v2 Standard_ and then click **Select**.</span></span> <span data-ttu-id="e8ccf-123">가상 머신의 크기 조정에 대한 알림을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-123">Notice the notification about resizing the virtual machine.</span></span>

1. <span data-ttu-id="e8ccf-124">**개요** 패널에서 VM의 크기가 _표준 DS3 v2(4개 vCPU, 14GB 메모리)_ 로 조정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-124">On the **Overview** panel, confirm that the VM has been resized to _Standard DS3 v2 (4 vcpus, 14 GB memory)_.</span></span>

## <a name="resize-using-powershell"></a><span data-ttu-id="e8ccf-125">PowerShell을 사용하여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e8ccf-125">Resize using PowerShell</span></span>

1. <span data-ttu-id="e8ccf-126">Azure Portal에 있는 위의 도구 모음에서 Cloud Shell 단추를 클릭하여 Azure Cloud Shell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-126">In the Azure portal, open Azure Cloud Shell by clicking the Cloud Shell button in the top toolbar.</span></span>

    <span data-ttu-id="e8ccf-127">Cloud Shell 창의 왼쪽 위에서 Bash가 아닌 PowerShell을 사용하도록 Cloud Shell이 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-127">Ensure that the Cloud Shell is set to use PowerShell and not Bash, in the top left of the Cloud Shell window.</span></span>

1. <span data-ttu-id="e8ccf-128">다음 cmdlet을 사용하여 사용 가능한 가상 머신 크기 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-128">Use the following cmdlet to get the list of available virtual machine sizes.</span></span>

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    ```

1. <span data-ttu-id="e8ccf-129">다음 cmdlet을 실행하여 가상 머신의 크기를 _DS2_v2_ 크기로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-129">Use the following cmdlet to resize the virtual machine back to a _DS2_v2_ size.</span></span>

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    $vm.HardwareProfile.VmSize = "Standard_DS2_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```

1. <span data-ttu-id="e8ccf-130">PowerShell 명령이 종료되기를 기다리는 동안 **my-test-vm** 블레이드에서 **새로 고침** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-130">Click the **Refresh** button in the **my-test-vm** blade while you are waiting for the PowerShell command to finish.</span></span> <span data-ttu-id="e8ccf-131">가상 머신이 크기 변경에 맞게 다시 시작되는지 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-131">You should notice that the virtual machine is restarting to accommodate the change in size.</span></span>

<span data-ttu-id="e8ccf-132">이 연습에서는 가상 머신을 만들고 두 개의 다른 도구를 사용하여 크기를 조정했습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-132">In this exercise, you created a virtual machine and resized it with two different tools.</span></span> <span data-ttu-id="e8ccf-133">가상 머신이 실행되는 동안에는 대상 크기를 사용할 수 없다는 점을 기억하는 것이 좋습니다. 가상 머신을 중지하면 더 많은 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ccf-133">A good tip to keep in mind is that the target size may not be available while the virtual machine is running; stopping the virtual machine lets you choose more sizes.</span></span>