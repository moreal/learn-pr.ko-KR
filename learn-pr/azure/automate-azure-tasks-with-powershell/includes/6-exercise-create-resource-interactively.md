<span data-ttu-id="92c64-101">원래 시나리오는 CRM 소프트웨어를 테스트할 VM을 만드는 시나리오였습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-101">Recall our original scenario - creating VMs to test our CRM software.</span></span> <span data-ttu-id="92c64-102">새로운 빌드가 나오면 깨끗한 이미지로 전체 설치 환경을 테스트할 수 있도록 새로운 VM을 가동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-102">When a new build is available, we want to spin up a new VM so we can test the full install experience from a clean image.</span></span> <span data-ttu-id="92c64-103">그런 다음, 테스트가 완료되면 VM을 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-103">Then when we are finished, we want to delete the VM.</span></span>

<span data-ttu-id="92c64-104">VM을 만드는 데 사용되는 명령을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-104">Let's try the commands you would use to create a VM.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm-with-azure-powershell"></a><span data-ttu-id="92c64-105">Azure PowerShell을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="92c64-105">Create a Linux VM with Azure PowerShell</span></span>

<span data-ttu-id="92c64-106">Azure 샌드박스를 사용하고 있으므로 리소스 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-106">Since we are using the Azure sandbox, you won't have to create a Resource Group.</span></span> <span data-ttu-id="92c64-107">대신, 리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-107">Instead, use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span> <span data-ttu-id="92c64-108">또한 위치 제한 사항도 알아두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-108">In addition, be aware of the location restrictions.</span></span>

<span data-ttu-id="92c64-109">PowerShell로 새로운 Azure VM을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-109">Let's create a new Azure VM with PowerShell.</span></span>

1. <span data-ttu-id="92c64-110">`New-AzureRmVm` cmdlet을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-110">Use the `New-AzureRmVm` cmdlet to create a VM.</span></span>
    - <span data-ttu-id="92c64-111">리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-111">Use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span>
    - <span data-ttu-id="92c64-112">VM에 이름을 지정합니다. 일반적으로 VM의 용도, 위치 및 인스턴스 번호(하나를 초과하는 경우)를 식별하는 의미 있는 이름을 사용하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-112">Give the VM a name - typically you want to use something meaningful that identifies the purposes of the VM, location, and (if there is more than one) instance number.</span></span> <span data-ttu-id="92c64-113">"미국 동부의 테스트 VM, 인스턴스 1"을 의미하는 "testvm-eus-01"이라는 이름을 사용하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-113">We'll use "testvm-eus-01" for "Test VM in East US, instance 1".</span></span> <span data-ttu-id="92c64-114">VM을 배치하는 위치에 따라 고유한 이름을 제안해보세요.</span><span class="sxs-lookup"><span data-stu-id="92c64-114">Come up with your own name based on where you place the VM.</span></span>
    - <span data-ttu-id="92c64-115">Azure 샌드박스에서 사용할 수 있는 다음 목록에서 사용자에게 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-115">Select a location close to you from the following list available in the Azure sandbox.</span></span> <span data-ttu-id="92c64-116">복사 및 붙여넣기를 사용하는 경우 아래 예제의 값을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-116">Make sure to change the value in the below example command if you are using copy and paste.</span></span>

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - <span data-ttu-id="92c64-117">이미지의 경우 "UbuntuLTS"를 사용합니다(이 예제의 경우 Ubuntu Linux).</span><span class="sxs-lookup"><span data-stu-id="92c64-117">Use "UbuntuLTS" for the image - this is Ubuntu Linux.</span></span>
    - <span data-ttu-id="92c64-118">`Get-Credential` cmdlet을 사용하고, `Credential` 매개 변수에 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-118">Use the `Get-Credential` cmdlet and feed the results into the `Credential` parameter.</span></span>
    - <span data-ttu-id="92c64-119">`-OpenPorts` 매개 변수를 추가하고 "22"를 포트로 전달합니다. 그러면 머신에 SSH로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-119">Add the `-OpenPorts` parameter and pass "22" as the port - this will let us SSH into the machine.</span></span>
 
    ```powershell
    New-AzureRmVm -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image UbuntuLTS -OpenPorts 22
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
    
1. <span data-ttu-id="92c64-120">작업을 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-120">This will take a few minutes to complete.</span></span> <span data-ttu-id="92c64-121">완료되면 쿼리하고 변수에 VM 개체(`$vm`)를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-121">Once it does, you can query it and assign the VM object to a variable (`$vm`).</span></span>

    ```powershell
    $vm = Get-AzureRmVM -Name "testvm-eus-01" -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```
    
1. <span data-ttu-id="92c64-122">그런 다음, 이 값을 쿼리하여 VM에 대한 정보를 쏟아냅니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-122">Then query the value to dump out the information about the VM:</span></span>

    ```powershell
    $vm
    ```

    <span data-ttu-id="92c64-123">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-123">You should see something like:</span></span>

    ```output
    ResourceGroupName : <rgn>[sandbox resource group name]</rgn>
    Id                : /subscriptions/xxxxxxxx-xxxx-aaaa-bbbb-cccccccccccc/resourceGroups/<rgn>[sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/testvm-eus-01
    VmId              : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    Name              : testvm-eus-01
    Type              : Microsoft.Compute/virtualMachines
    Location          : eastus
    Tags              : {}
    HardwareProfile   : {VmSize}
    NetworkProfile    : {NetworkInterfaces}
    OSProfile         : {ComputerName, AdminUsername, LinuxConfiguration, Secrets}
    ProvisioningState : Succeeded
    StorageProfile    : {ImageReference, OsDisk, DataDisks}
    ```
    
1. <span data-ttu-id="92c64-124">점(".") 구문을 통해 복합 개체를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-124">You can reach into complex objects through a dot (".") syntax.</span></span> <span data-ttu-id="92c64-125">예를 들어 HardwareProfile 섹션과 연결된 `VMSize` 개체의 속성을 보려면 다음을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-125">For example, to see the properties in the `VMSize` object associated with the HardwareProfile section you can type:</span></span>

    ```powershell
    $vm.HardwareProfile
    ```

1. <span data-ttu-id="92c64-126">또는 디스크 중 하나에 대한 정보 가져오려면 다음을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-126">Or to get information on one of the disks:</span></span>

    ```powershell
    $vm.StorageProfile.OsDisk
    ```

1. <span data-ttu-id="92c64-127">다른 cmdlet에 VM 개체를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-127">You can even pass the VM object into other cmdlets.</span></span> <span data-ttu-id="92c64-128">예를 들어 이렇게 하면 VM의 공용 IP 주소가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-128">For example, this will retrieve the public IP address of your VM:</span></span>

    ```powershell
    $vm | Get-AzureRmPublicIpAddress
    ```

1. <span data-ttu-id="92c64-129">이 IP 주소를 사용하여 SSH로 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-129">With the IP address, you can connect to the VM with SSH.</span></span> <span data-ttu-id="92c64-130">예를 들어, 사용자 이름에 "Bob"을 사용하고 IP 주소가 "205.22.16.5"라면 이 명령은 Linux 머신에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-130">For example, if you used the username "bob", and the IP address is "205.22.16.5", then this command would connect to the Linux machine:</span></span>

    ```powershell
    ssh bob@205.22.16.5
    ```

    <span data-ttu-id="92c64-131">계속해서 `exit`를 입력하여 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-131">Go ahead and log out by typing `exit`.</span></span>


## <a name="delete-a-vm"></a><span data-ttu-id="92c64-132">VM 삭제</span><span class="sxs-lookup"><span data-stu-id="92c64-132">Delete a VM</span></span>

<span data-ttu-id="92c64-133">더 많은 명령을 사용해 보기 위해 VM을 삭제하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-133">Just to try out some more commands, let's delete the VM.</span></span> <span data-ttu-id="92c64-134">먼저 VM을 종료하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-134">We'll shut it down first.</span></span>

```powershell
Stop-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

<span data-ttu-id="92c64-135">이제 `Remove-AzureRmVM` cmdlet을 사용하여 VM을 삭제하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-135">Now, let's delete the VM with the `Remove-AzureRmVM` cmdlet:</span></span>

```powershell
Remove-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

<span data-ttu-id="92c64-136">리소스 그룹의 모든 리소스를 나열하려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-136">Try this command to list all the resources in your resource group:</span></span>

```powershell
Get-AzureRmResource -ResourceGroupName $vm.ResourceGroupName | ft
```

<span data-ttu-id="92c64-137">현재 존재하는 리소스(디스크, 가상 네트워크 등)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-137">You should see a bunch of resources (disks, virtual networks, etc.) that all still exist.</span></span> 

```output
Microsoft.Compute/disks
Microsoft.Network/networkInterfaces
Microsoft.Network/networkSecurityGroups
Microsoft.Network/publicIPAddresses
Microsoft.Network/virtualNetworks
```

<span data-ttu-id="92c64-138">`Remove-AzureRmVM` 명령은 _VM을 삭제하기만_ 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-138">This is because the `Remove-AzureRmVM` command _just deletes the VM_.</span></span> <span data-ttu-id="92c64-139">다른 리소스는 정리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-139">It doesn't cleanup any of the other resources!</span></span> <span data-ttu-id="92c64-140">이제 리소스 그룹 자체를 삭제하고 끝내도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-140">At this point, we'd likely just delete the Resource Group itself and be done with it.</span></span> <span data-ttu-id="92c64-141">연습 내용을 간략히 살펴보면서 필요한 부분을 직접 정리하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-141">However, let's just run through the exercise to clean it up manually.</span></span> <span data-ttu-id="92c64-142">명령의 패턴이 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-142">You should see a pattern in the commands.</span></span>

1. <span data-ttu-id="92c64-143">네트워크 인터페이스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-143">Delete the Network Interface.</span></span>

    ```powershell
    $vm | Remove-AzureRmNetworkInterface –Force
    ```
    
1. <span data-ttu-id="92c64-144">관리되는 OS 디스크 및 저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-144">Delete the managed OS disks and storage account</span></span>

    ```powershell
    Get-AzureRmDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzureRmDisk -Force
    ```

1. <span data-ttu-id="92c64-145">다음으로, 가상 네트워크를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-145">Next, delete the virtual network.</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmVirtualNetwork -Force
    ```

1. <span data-ttu-id="92c64-146">네트워크 보안 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-146">Delete the network security group.</span></span>

    ```powershell
    Get-AzureRmNetworkSecurityGroup -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmNetworkSecurityGroup -Force
    ```

1. <span data-ttu-id="92c64-147">그리고 마지막으로, 공용 IP 주소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-147">And finally, the public IP address.</span></span>

    ```powershell
    Get-AzureRmPublicIpAddress -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmPublicIpAddress -Force
    ```

<span data-ttu-id="92c64-148">생성된 모든 리소스가 삭제되어야 합니다. 리소스 그룹을 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="92c64-148">We should have caught all the created resources; check the resource group just to be sure.</span></span> <span data-ttu-id="92c64-149">여기에서는 많은 수동 명령을 실행했지만 나중에 이 논리를 재사용하여 VM을 만들거나 삭제할 수 있도록 _스크립트_를 작성하는 것이 더 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-149">We did a lot of manual commands here but a better approach would have been to write a _script_ so we could reuse this logic later to create or delete a VM.</span></span> <span data-ttu-id="92c64-150">PowerShell로 스크립팅하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92c64-150">Let's look at scripting with PowerShell.</span></span>