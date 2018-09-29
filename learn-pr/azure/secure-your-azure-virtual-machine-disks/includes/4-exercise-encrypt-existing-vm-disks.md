<span data-ttu-id="f6742-101">신규 스타트업 기업을 위해 재무 관리 응용 프로그램을 개발한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-101">Suppose you are developing a financial management application for new business startups.</span></span> <span data-ttu-id="f6742-102">모든 고객 데이터를 보호해야 하므로 이 응용 프로그램을 호스트할 서버의 모든 OS 및 데이터 디스크에서 ADE(Azure Disk Encryption)를 구현하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-102">You want to ensure that all your customers' data is secured, so you have decided to implement Azure Disk Encryption (ADE) across all OS and data disks on the servers that will host this application.</span></span> <span data-ttu-id="f6742-103">규정 준수 요구 사항의 일부분으로 고유한 암호화 키 관리도 담당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-103">As part of your compliance requirements, you also need to be responsible for your own encryption key management.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="f6742-104">이 단원에서는 기존 가상 머신에서 디스크를 암호화하고 고유한 Azure Key Vault를 사용하여 암호화 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-104">In this unit, you'll encrypt disks on an existing virtual machine, and manage the encryption keys using your own Azure Key Vault.</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="f6742-105">환경 준비</span><span class="sxs-lookup"><span data-stu-id="f6742-105">Prepare the environment</span></span>

<span data-ttu-id="f6742-106">Azure Virtual Machine에서 새 Windows VM을 배포하기 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-106">We'll start by deploying a new Windows VM in an Azure Virtual Machine.</span></span>

### <a name="deploy-windows-vm"></a><span data-ttu-id="f6742-107">Windows VM 배포</span><span class="sxs-lookup"><span data-stu-id="f6742-107">Deploy Windows VM</span></span>

<span data-ttu-id="f6742-108">Azure PowerShell을 사용하여 Windows 가상 머신을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-108">Use the Azure PowerShell to create and deploy a new Windows virtual machine.</span></span>

1. <span data-ttu-id="f6742-109">새 리소스를 배치하는 위치를 결정하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-109">Start by deciding where to place the new resources.</span></span> <span data-ttu-id="f6742-110">다음 목록에서 사용자에게 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-110">Select a location near you from the following list.</span></span>

    <span data-ttu-id="f6742-111"><!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]</span><span class="sxs-lookup"><span data-stu-id="f6742-111"><!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]</span></span>
    

1. <span data-ttu-id="f6742-112">선택된 위치를 보유하도록 PowerShell 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-112">Define a PowerShell variable to hold the selected location.</span></span> <span data-ttu-id="f6742-113">여기에서 "미국 동부"로 정의되어 있으므로 원하는 위치로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-113">It's defined as "East US" here, change it to your preferred location.</span></span>

    ```powershell
    $location = "eastus"
    ```
    
    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="f6742-114">다음으로, 몇 가지 편리한 변수를 정의하여 VM의 _이름_ 및 _리소스 그룹_을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-114">Next, define a few more convenient variables to capture the _name_ of the VM and the _resource group_.</span></span> <span data-ttu-id="f6742-115">여기에서 미리 만든 리소스 그룹을 사용합니다. 일반적으로 `New-AzureRmResourceGroup`을 사용하여 구독에서 _새_ 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-115">Note that we are using the pre-created resource group here, normally you would create a _new_ resource group in your subscription using `New-AzureRmResourceGroup`.</span></span>

    ```powershell
    $vmName = "fmdata-vm01"
    $rgName = "<rgn>[sandbox Resource Group]</rgn>"
    ```
    
1. <span data-ttu-id="f6742-116">`New-AzureRmVm`을 사용하여 새 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-116">Use `New-AzureRmVm` to create a new virtual machine.</span></span>
    
    ```powershell
    New-AzureRmVm `
        -ResourceGroupName $rgName `
        -Name $vmName `
        -Location $location `
        -OpenPorts 3389
    ```
    
    <span data-ttu-id="f6742-117">Cloud Shell에서 프롬프트가 표시되면 VM의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-117">Enter a username and password for the VM when you are prompted by the Cloud Shell.</span></span> <span data-ttu-id="f6742-118">이 VM에 대해 만든 초기 계정으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-118">This will be used as the initial account created for the VM.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f6742-119">다양한 옵션을 제공하지 않으므로 이 명령은 일부 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-119">This command will use some defaults since we didn't supply a bunch of options.</span></span> <span data-ttu-id="f6742-120">특히 _Windows 2016 Server_ 이미지를 _Standard_DS1_v2_ 크기로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-120">Specifically, this will create a _Windows 2016 Server_ image with the size to _Standard_DS1_v2_.</span></span> <span data-ttu-id="f6742-121">VM 크기를 지정하려는 경우 기본 계층 VM에서는 ADE를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-121">Remember that the Basic tier VMs do not support ADE if you decide to specify the VM size.</span></span>

1. <span data-ttu-id="f6742-122">VM 배포가 완료되면 변수에서 VM 세부 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-122">Once the VM finishes deploying, capture the VM details in a variable.</span></span> <span data-ttu-id="f6742-123">이 변수를 사용하여 만들어진 내용을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-123">You can use this variable to explore what was created.</span></span>

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```
    
1. <span data-ttu-id="f6742-124">VM에 연결된 OS 디스크를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-124">You can see the OS disk attached to the VM:</span></span>

    ```powershell
    $vm.StorageProfile.OSDisk
    ```

    ```output
    OsType                  : Windows
    EncryptionSettings      :
    Name                    : fmdata-vm01_OsDisk_1_6bcf8dcd49794aa785bad45221ec4433
    Vhd                     :
    Image                   :
    Caching                 : ReadWrite
    WriteAcceleratorEnabled :
    CreateOption            : FromImage
    DiskSizeGB              : 127
    ManagedDisk             : Microsoft.Azure.Management.Compute.Models.ManagedDiskP
                              arameters
    ```
        
1. <span data-ttu-id="f6742-125">OS 디스크(및 데이터 디스크)에서 암호화의 현재 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-125">Check the current status of encryption on the OS disk (and any data disks).</span></span>

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  `
        -ResourceGroupName $rgName `
        -VMName $vmName
    ```

    <span data-ttu-id="f6742-126">확인했듯이 디스크는 현재 _암호화되지 않았습니다_.</span><span class="sxs-lookup"><span data-stu-id="f6742-126">As you can see the disks are current _unencrypted_.</span></span> 

    ```output
    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : NotEncrypted
    OsVolumeEncryptionSettings :
    ProgressMessage            : No Encryption extension or metadata found on the VM
    ```
    
<span data-ttu-id="f6742-127">변경을 시작해봅시다.</span><span class="sxs-lookup"><span data-stu-id="f6742-127">Let's change that.</span></span>
    
## <a name="encrypt-the-vm-disks-with-azure-disk-encryption"></a><span data-ttu-id="f6742-128">Azure Disk Encryption을 사용하여 VM 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="f6742-128">Encrypt the VM disks with Azure Disk Encryption</span></span>

<span data-ttu-id="f6742-129">이 데이터를 보호해야 하므로 디스크를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-129">We need to protect this data, so let's encrypt the disks.</span></span> <span data-ttu-id="f6742-130">수행해야 하는 일부 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-130">Recall that there are several steps we need to perform:</span></span>

1. <span data-ttu-id="f6742-131">키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-131">Create a key vault.</span></span>
1. <span data-ttu-id="f6742-132">키 자격 증명 모음을 설정하여 디스크 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-132">Set the key vault up to support disk encryption.</span></span>
1. <span data-ttu-id="f6742-133">Key Vault에서 저장된 키를 사용하여 VM 디스크를 암호화하도록 Azure에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-133">Tell Azure to encrypt the VM disks using the key stored in the Key Vault.</span></span>

> [!TIP]
> <span data-ttu-id="f6742-134">개별적으로 단계를 설명하려고 하지만 고유한 구독에서 이 작업을 수행하는 경우 이 모듈의 요약에 연결된 유용한 PowerShell 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-134">We're going to walk through the steps individually, but when you're doing this task in your own subscription, you can use a handy PowerShell script which is linked in the Summary of this module.</span></span>

### <a name="create-a-key-vault"></a><span data-ttu-id="f6742-135">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="f6742-135">Create a key vault</span></span>

<span data-ttu-id="f6742-136">Azure Key Vault를 만들려면 구독에서 서비스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-136">To create an Azure Key Vault, we need to enable the service in our subscription.</span></span> <span data-ttu-id="f6742-137">이 설정은 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-137">This is a one-time requirement.</span></span>

> [!TIP]
> <span data-ttu-id="f6742-138">구독에 따라 `Register-AzureRmResourceProvider` cmdlet을 사용하여 **Microsoft.KeyVault** 공급자를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-138">Depending on your subscription, you might need to enable the **Microsoft.KeyVault** provider with the `Register-AzureRmResourceProvider` cmdlet.</span></span> <span data-ttu-id="f6742-139">이 작업은 Azure 샌드박스 구독에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-139">This is not necessary in the Azure sandbox subscription.</span></span>

1. <span data-ttu-id="f6742-140">새 키 자격 증명 모음의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-140">Decide on a name for your new key vault.</span></span> <span data-ttu-id="f6742-141">이름은 고유해야 하며, 숫자, 영문자 및 대시로 구성된 3-24자 사이이면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-141">It must be unique and can be between 3 and 24 characters, composed of numbers, letters, and and dashes.</span></span> <span data-ttu-id="f6742-142">끝에 몇 가지 임의의 숫자를 추가하여 아래의 "1234"를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-142">Try adding some random numbers to the end, replacing the "1234" below.</span></span>

    ```powershell
    $keyVaultName = "mvmdsk-kv-1234"
    ```
        
1. <span data-ttu-id="f6742-143">`New-AzureRmKeyVault`를 사용하여 Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-143">Create an Azure Key Vault with `New-AzureRmKeyVault`.</span></span>
    - <span data-ttu-id="f6742-144">VM과 동일한 리소스 그룹 _및_ 위치에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-144">Make sure it's placed in the same resource group _and_ location as your VM.</span></span>
    - <span data-ttu-id="f6742-145">디스크 암호화에 사용할 Key Vault를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-145">Enable the Key Vault for use with disk encryption.</span></span> 
    - <span data-ttu-id="f6742-146">고유한 Key Vault 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-146">Specify a unique Key Vault name.</span></span>

    ```powershell
    New-AzureRmKeyVault -VaultName $keyVaultName `
        -Location $location `
        -ResourceGroupName $rgName `
        -EnabledForDiskEncryption
    ```

    <span data-ttu-id="f6742-147">이 명령에서 액세스 권한이 없는 사용자에 대한 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-147">You will get a warning from this command about no users having access.</span></span>

    ```output
    WARNING: Access policy is not set. No user or application have access permission to use this vault. This can happen if the vault was created by a service principal. Please use Set-AzureRmKeyVaultAccessPolicy to set access policies.
    ```

    <span data-ttu-id="f6742-148">자격 증명 모음을 사용하여 VM의 암호화 키를 저장하고 있으므로 문제가 발생하지 않으며 사용자는 이 데이터에 액세스할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-148">This is ok since we are just using the vault to store the encryption keys for the VM and users won't need to access this data.</span></span>

### <a name="encrypt-the-disk"></a><span data-ttu-id="f6742-149">디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="f6742-149">Encrypt the disk</span></span>

<span data-ttu-id="f6742-150">디스크를 암호화할 준비가 거의 다 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-150">We are almost ready to encrypt the disks.</span></span> <span data-ttu-id="f6742-151">수행하기 전에 백업 만들기에 대한 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-151">Before we do, a warning about creating backups.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6742-152">프로덕션 시스템인 경우 Azure Backup을 사용하거나 스냅숏을 만들어서 관리 디스크의 백업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-152">If this were a production system, we would need to perform a backup of the managed disks - either using Azure Backup, or by creating a snapshot.</span></span> <span data-ttu-id="f6742-153">Azure Portal 또는 명령줄을 통해 스냅숏을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-153">You can create snapshots in the Azure portal, or through the command line.</span></span> <span data-ttu-id="f6742-154">PowerShell에서 `New-AzureRmSnapshot` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-154">In PowerShell, use the `New-AzureRmSnapshot` cmdlet.</span></span> <span data-ttu-id="f6742-155">이 간단한 연습이 완료되면 이 데이터를 throw하므로 이 단계를 건너뛰도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-155">Since this is a simple exercise and we're going to throw this data away when you're done, we're going to skip this step.</span></span> 

1. <span data-ttu-id="f6742-156">Key Vault 정보를 보유하도록 변수를 정의하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-156">Start by defining a variable to hold the Key Vault information.</span></span>

    ```powershell
    $keyVault = Get-AzureRmKeyVault `
        -VaultName $keyVaultName `
        -ResourceGroupName $rgName
    ```

1. <span data-ttu-id="f6742-157">그런 다음, `Set-AzureRmVmDiskEncryptionExtension` cmdlet을 사용하여 VM 디스크를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-157">Then, use the `Set-AzureRmVmDiskEncryptionExtension` cmdlet to encrypt the VM disks.</span></span>
    - <span data-ttu-id="f6742-158">`VolumeType` 매개 변수를 사용하면 암호화할 디스크를 지정할 수 있습니다. [_모두_ | _OS_ | _데이터_]</span><span class="sxs-lookup"><span data-stu-id="f6742-158">The `VolumeType` parameter allows you to specify which disks to encrypt: [_All_ | _OS_ | _Data_].</span></span> <span data-ttu-id="f6742-159">_모두_로 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-159">It will default to _All_.</span></span> <span data-ttu-id="f6742-160">일부 Linux 배포에 대한 데이터 디스크만 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-160">You can only encrypt data disks for some distributions of Linux.</span></span>
    - <span data-ttu-id="f6742-161">관리 디스크의 `SkipVmBackup` 플래그를 제공해야 합니다. 그렇지 않으면 스냅숏이 없으므로 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-161">You have to supply the `SkipVmBackup` flag for managed disks or the command will fail because there is no snapshot.</span></span>

    ```powershell
    Set-AzureRmVmDiskEncryptionExtension `
        -ResourceGroupName $rgName `
        -VMName $vmName `
        -VolumeType All `
        -DiskEncryptionKeyVaultId $keyVault.ResourceId `
        -DiskEncryptionKeyVaultUrl $keyVault.VaultUri `
        -SkipVmBackup
    ```

1. <span data-ttu-id="f6742-162">cmdlet에서는 VM이 오프라인 상태로 전환되고 작업을 완료하는 데 몇 분 정도가 걸릴 수 있다고 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-162">The cmdlet will warn you that the VM must be taken offline, and that the task may take several minutes to complete.</span></span> <span data-ttu-id="f6742-163">계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-163">Go ahead and let it continue.</span></span>

    ```output
    Enable AzureDiskEncryption on the VM
    This cmdlet prepares the VM and enables encryption which may reboot the machine and takes 10-15 minutes to
    finish. Please save your work on the VM before confirming. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
    ```
    
1. <span data-ttu-id="f6742-164">작업이 완료되면 암호화 상태를 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-164">Once it's complete, check the encryption status again.</span></span>

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
    ```

    <span data-ttu-id="f6742-165">이제 OS 디스크가 암호화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-165">Now the OS disk should be encrypted.</span></span> <span data-ttu-id="f6742-166">Windows에 표시되는 연결된 데이터 디스크가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-166">Any attached data disks that are visible to Windows will also be encrypted.</span></span>

    ```output
    OsVolumeEncrypted          : Encrypted
    DataVolumesEncrypted       : NoDiskFound
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : Provisioning succeeded
    ```

> [!NOTE]        
> <span data-ttu-id="f6742-167">암호화를 자동으로 암호화하지 _않으면_ 새 디스크가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-167">New disks added after encryption will _not_ be automatically encrypted.</span></span> <span data-ttu-id="f6742-168">`Set-AzureRmVMDiskEncryptionExtension` cmdlet을 다시 실행하여 새 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-168">You can re-run the `Set-AzureRmVMDiskEncryptionExtension` cmdlet to encrypt new disks.</span></span> <span data-ttu-id="f6742-169">이미 디스크를 암호화한 VM에 디스크를 추가하는 경우 새 시퀀스 번호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-169">Make sure to provide a new sequence number if you add disks to a VM that has already had disks encrypted.</span></span> <span data-ttu-id="f6742-170">또한 운영 체제에 표시되지 않는 디스크를 암호화하지 않습니다. 디스크를 제대로 분할하고, 포맷하고, 탑재하여 Bitlocker 확장에서 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6742-170">In addition, disks that are not visible to the operating system will not be encrypted - the disk must be properly partitioned, formatted, and mounted to be seen by the Bitlocker extension.</span></span>