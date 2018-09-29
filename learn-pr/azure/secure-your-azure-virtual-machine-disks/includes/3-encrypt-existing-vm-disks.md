<span data-ttu-id="f4770-101">회사에서 모든 VM에 ADE(Azure Disk Encryption)를 구현하기로 결정했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-101">Suppose your company has decided to implement Azure Disk Encryption (ADE) across all VMs.</span></span> <span data-ttu-id="f4770-102">기존 VM 볼륨에 암호화를 롤아웃하는 방법을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-102">You need to evaluate how to roll out encryption to existing VM volumes.</span></span> <span data-ttu-id="f4770-103">여기서는 ADE의 요구 사항과 기존 Linux 및 Windows VM의 디스크를 암호화하기 위한 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-103">Here, we'll look at the requirements for ADE, and the steps involved in encrypting disks on existing Linux and Windows VMs.</span></span>

## <a name="azure-disk-encryption-prerequisites"></a><span data-ttu-id="f4770-104">Azure Disk Encryption 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f4770-104">Azure Disk Encryption prerequisites</span></span>

<span data-ttu-id="f4770-105">VM 디스크를 암호화하려면 먼저 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-105">Before you can encrypt your VM disks, you need to:</span></span>

1. <span data-ttu-id="f4770-106">Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-106">Create a key vault.</span></span>
1. <span data-ttu-id="f4770-107">Key Vault 액세스 정책을 설정하여 디스크 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-107">Set the key vault access policy to support disk encryption.</span></span>
1. <span data-ttu-id="f4770-108">Key Vault를 사용하여 ADE에 대한 암호화 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-108">Use the key vault to store the encryption keys for ADE.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="f4770-109">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f4770-109">Azure Key Vault</span></span>

<span data-ttu-id="f4770-110">ADE에 사용되는 암호화 키를 Azure Key Vault에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-110">The encryption keys used by ADE can be stored in Azure Key Vault.</span></span> <span data-ttu-id="f4770-111">Azure Key Vault는 비밀을 안전하게 저장하고 액세스하기 위한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-111">Azure Key Vault is a tool for securely storing and accessing secrets.</span></span> <span data-ttu-id="f4770-112">비밀은 API 키, 암호 또는 인증서와 같이 액세스를 엄격하게 제어하려는 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-112">A secret is anything that you want to tightly control access to, such as API keys, passwords, or certificates.</span></span> <span data-ttu-id="f4770-113">비밀을 활용하는 경우 FIPS(Federal Information Processing Standard) 140-2 수준 2 유효성이 검사된 HSM(하드웨어 보안 모듈)에 정의된 대로 가용성과 확장성이 뛰어난 보안 저장소가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-113">This provides highly available and scalable secure storage, as defined in Federal Information Processing Standards (FIPS) 140-2 Level 2 validated Hardware Security Modules (HSMs).</span></span> <span data-ttu-id="f4770-114">Key Vault를 사용하면 데이터를 암호화하는 데 사용되는 키를 완벽하게 제어할 수 있으며 키 사용을 관리 및 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-114">Using Key Vault, you keep full control of the keys used to encrypt your data, and you can manage and audit your key usage.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4770-115">Azure Disk Encryption을 사용하려면 Key Vault와 VM이 같은 Azure 지역에 있어야 합니다. 그래야 암호화 비밀이 다른 지역에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-115">Azure Disk Encryption requires that your key vault and your VMs are in the same Azure region; this ensures that encryption secrets do not cross regional boundaries.</span></span>

<span data-ttu-id="f4770-116">다음을 사용하여 Key Vault를 구성하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-116">You can configure and manage your key vault with:</span></span>

#### <a name="powershell"></a><span data-ttu-id="f4770-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4770-117">Powershell</span></span>

```powershell
New-AzureRmKeyVault -Location <location> `
    -ResourceGroupName <resource-group> `
    -VaultName "myKeyVault" `
    -EnabledForDiskEncryption
```

### <a name="azure-cli"></a><span data-ttu-id="f4770-118">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f4770-118">Azure CLI</span></span>

```azurecli
az keyvault create \
    --name "myKeyVault" \
    --resource-group <resource-group> \
    --location <location> \
    --enabled-for-disk-encryption True
```

### <a name="azure-portal"></a><span data-ttu-id="f4770-119">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f4770-119">Azure portal</span></span>

<span data-ttu-id="f4770-120">Azure Key Vault는 일반 리소스 생성 프로세스를 사용하여 Azure Portal에서 만들 수 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-120">An Azure Key Vault is a resource that can be created in the Azure portal using the normal resource creation process.</span></span>

1. <span data-ttu-id="f4770-121">왼쪽에 있는 사이드바에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-121">Click **Create a resource** in the sidebar on the left.</span></span>

1. <span data-ttu-id="f4770-122">"Key Vault"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-122">Search for "Key vault".</span></span> <span data-ttu-id="f4770-123">세부 정보 창에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-123">Click **Create** in the details window.</span></span>

    ![Azure Marketplace의 Key Vault를 보여 주는 스크린샷](../media/3-create-keyvault.png)

1. <span data-ttu-id="f4770-125">새 Key Vault에 대한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-125">Enter the details for the new Key Vault:</span></span>
    - <span data-ttu-id="f4770-126">Key Vault의 **이름** 입력</span><span class="sxs-lookup"><span data-stu-id="f4770-126">Enter a **Name** for the Key Vault</span></span>
    - <span data-ttu-id="f4770-127">배치할 구독을 선택합니다(현재 구독의 기본값).</span><span class="sxs-lookup"><span data-stu-id="f4770-127">Select the subscription to place it in (defaults to your current subscription).</span></span>
    - <span data-ttu-id="f4770-128">**리소스 그룹**를 선택하거나 Key Vault를 소유할 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-128">Select a **Resource Group**, or create a new resource group to own the Key Vault.</span></span>
    - <span data-ttu-id="f4770-129">Key Vault의 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-129">Select a **Location** for the Key Vault.</span></span> <span data-ttu-id="f4770-130">VM이 있는 위치를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-130">Make sure to select the location the VM is in.</span></span>
    - <span data-ttu-id="f4770-131">가격 책정 계층에 대해 표준 또는 프리미엄을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-131">You can choose either Standard or Premium for the pricing tier.</span></span> <span data-ttu-id="f4770-132">주요 차이점은 프리미엄 계층에서는 하드웨어 암호화 백업 키를 허용한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-132">The main difference is that the premium tier allows for Hardware-encryption backed keys.</span></span>

1. <span data-ttu-id="f4770-133">디스크 암호화를 지원하도록 액세스 정책을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-133">You must change the Access policies to support Disk Encryption.</span></span> <span data-ttu-id="f4770-134">기본적으로 _사용자_ 계정을 정책에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-134">By default it adds _your_ account to the policy.</span></span>
    - <span data-ttu-id="f4770-135">**액세스 정책** 선택</span><span class="sxs-lookup"><span data-stu-id="f4770-135">Select **Access policies**</span></span>
    - <span data-ttu-id="f4770-136">**고급 액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-136">Click **Advanced access policies**.</span></span>
    - <span data-ttu-id="f4770-137">**볼륨 암호화를 위한 Azure Disk Encryption 액세스 사용**을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-137">Check the **Enable access to Azure Disk Encryption for volume encryption**.</span></span>
    - <span data-ttu-id="f4770-138">원하는 경우 계정을 제거할 수 있으며, 디스크 암호화에 Key Vault만 사용하려는 경우에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-138">You can remove your account if you like, it's not necessary if you only intend to use the Key Vault for disk encryption.</span></span>
    - <span data-ttu-id="f4770-139">**확인**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-139">Click **OK** to save the changes.</span></span>

    ![Azure Disk Encryption 옵션을 선택하고 강조 표시한 Key Vault의 고급 속성을 보여 주는 스크린샷](../media/3-configure-access-policy.png)

1. <span data-ttu-id="f4770-141">**만들기**를 클릭하여 새 Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-141">Click **Create** to create the new Key Vault.</span></span>

## <a name="enabling-access-policies-in-the-key-vault"></a><span data-ttu-id="f4770-142">Key Vault에서 액세스 정책 사용</span><span class="sxs-lookup"><span data-stu-id="f4770-142">Enabling access policies in the key vault</span></span>
<span data-ttu-id="f4770-143">Azure는 VM을 부팅하고 볼륨을 해독할 수 있도록 Key Vault의 암호화 키 또는 비밀에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-143">Azure needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="f4770-144">위의 **고급 액세스 정책**을 변경했을 때 포털에서 이를 다루었습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-144">We covered this for the portal when we changed the **Advanced access policies** above.</span></span>

<span data-ttu-id="f4770-145">세 가지 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-145">There are three policies you can enable.</span></span>
1. <span data-ttu-id="f4770-146">**디스크 암호화** - Azure Disk Encryption에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-146">**Disk encryption** - Required for Azure Disk encryption.</span></span>
1. <span data-ttu-id="f4770-147">**배포** - (선택 사항) 이 Key Vault가 리소스를 만들 때(예: 가상 머신 만들 때) 참조되는 경우 Microsoft.Compute 리소스 공급자에서 이 Key Vault으로부터 비밀을 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-147">**Deployment** - (Optional) Enables the Microsoft.Compute resource provider to retrieve secrets from this key vault when this key vault is referenced in resource creation, for example when creating a virtual machine.</span></span>
1. <span data-ttu-id="f4770-148">**템플릿 배포** - (선택 사항) 이 Key Vault가 템플릿 배포에서 참조되는 경우 Azure Resource Manager에서 이 Key Vault으로부터 비밀을 가져올 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-148">**Template deployment** - (Optional) Enables Azure Resource Manager to get secrets from this key vault when this key vault is referenced in a template deployment.</span></span>

<span data-ttu-id="f4770-149">디스크 암호화 정책을 사용하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-149">Here's how to enable the disk encryption policy.</span></span> <span data-ttu-id="f4770-150">다른 두 개는 유사하지만 다른 플래그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-150">The other two are similar but use different flags.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <keyvault-name> -ResourceGroupName <resource-group> -EnabledForDiskEncryption
```

```azurecli
az keyvault update --name <keyvault-name> --resource-group <resource-group> --enabled-for-disk-encryption "true"
```

## <a name="encrypting-an-existing-vm-disk"></a><span data-ttu-id="f4770-151">기존 VM 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="f4770-151">Encrypting an existing VM disk</span></span>

<span data-ttu-id="f4770-152">Key Vault 설정이 완료되면 Azure CLI 또는 Azure PowerShell을 사용하여 VM을 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-152">Once you have the Key Vault setup, you can encrypt the VM using either Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="f4770-153">처음으로 Windows VM을 암호화할 때 모든 디스크 또는 OS 디스크만 암호화하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-153">The first time you encrypt a Windows VM, you can choose to encrypt either all disks or the OS disk only.</span></span> <span data-ttu-id="f4770-154">일부 Linux 배포에서는 데이터 디스크만 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-154">On some Linux distributions, only the data disks may be encrypted.</span></span> <span data-ttu-id="f4770-155">암호화를 받으려면 Windows 디스크가 NTFS 볼륨으로 포맷되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-155">To be eligible for encryption, your Windows disks must be formatted as NTFS volumes.</span></span>

> [!WARNING]
> <span data-ttu-id="f4770-156">암호화를 설정하려면 먼저 관리 디스크의 스냅숏 또는 백업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-156">You must take a snapshot or a backup of managed disks before you can turn on encryption.</span></span> <span data-ttu-id="f4770-157">아래에 지정된 `SkipVmBackup` 플래그는 관리 디스크에서 백업이 완료되었음을 도구에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-157">The `SkipVmBackup` flag specified below tells the tool that the backup is complete on managed disks.</span></span> <span data-ttu-id="f4770-158">백업 없이, 어떤 이유로 암호가 실패하면 VM을 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-158">Without the backup, you will be unable to recover the VM if the encryption fails for some reason.</span></span>

<span data-ttu-id="f4770-159">PowerShell을 통해 `Set-AzureRmVmDiskEncryptionExtension` cmdlet을 사용하여 암호화를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-159">With PowerShell, use the `Set-AzureRmVmDiskEncryptionExtension` cmdlet to enable encryption.</span></span>

```powershell

Set-AzureRmVmDiskEncryptionExtension `
    -ResourceGroupName <resource-group> `
    -VMName <vm-name> `
    -VolumeType [All | OS | Data]
    -DiskEncryptionKeyVaultId <keyVault.ResourceId> `
    -DiskEncryptionKeyVaultUrl <keyVault.VaultUri> `
     -SkipVmBackup
```

<span data-ttu-id="f4770-160">Azure CLI의 경우 `az vm encryption enable` 명령을 사용하여 암호화를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-160">For the Azure CLI, use the `az vm encryption enable` command to enable encryption.</span></span>

```azurecli
az vm encryption enable \
    --resource-group <resource-group> \
    --name <vm-name> \
    --disk-encryption-keyvault <keyvault-name> \
    --volume-type [all | os | data] \
    --skipvmbackup
```

## <a name="viewing-the-status-of-the-disk"></a><span data-ttu-id="f4770-161">디스크 상태 보기</span><span class="sxs-lookup"><span data-stu-id="f4770-161">Viewing the status of the disk</span></span>

<span data-ttu-id="f4770-162">특정 디스크가 암호화되었는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-162">You can check whether specific disks are encrypted or not.</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName <resource-group> -VMName <vm-name>
```

```azurecli
az vm encryption status --resource-group <resource-group> --name <vm-name>
```

<span data-ttu-id="f4770-163">이 두 명령은 모두 지정된 VM에 연결된 각 디스크의 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-163">Both of these commands will return the status of each disk attached to the specified VM.</span></span>

## <a name="decrypting-drives"></a><span data-ttu-id="f4770-164">드라이브 암호 해독</span><span class="sxs-lookup"><span data-stu-id="f4770-164">Decrypting drives</span></span>

<span data-ttu-id="f4770-165">`Disable-AzureRmVMDiskEncryption`을 사용하여 PowerShell을 통해 암호화를 반대로 할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="f4770-165">You can reverse the encryption through PowerShell using `Disable-AzureRmVMDiskEncryption`.</span></span>

```powershell
Disable-AzureRmVMDiskEncryption -ResourceGroupName <resource-group> -VMName <vm-name>
```

<span data-ttu-id="f4770-166">Azure CLI의 경우 `vm encryption disable` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-166">For the Azure CLI, use the `vm encryption disable` command.</span></span>

```azurecli
az vm encryption disable --resource-group <resource-group> --name <vm-name>
```

<span data-ttu-id="f4770-167">이러한 명령은 지정된 가상 머신에 대해 모든 형식의 볼륨에 대한 암호화를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-167">These commands disable encryption for volumes of type all for the specified virtual machine.</span></span> <span data-ttu-id="f4770-168">암호화 버전과 마찬가지로 `-VolumeType` 매개 변수 `[All | OS | Data]`를 지정하여 암호를 해독할 디스크를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-168">Just like the encrypt version, you can specify a `-VolumeType` parameter `[All | OS | Data]` to decide what disks to decrypt.</span></span> <span data-ttu-id="f4770-169">제공되지 않는 경우 기본값은 `All`입니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-169">It defaults to `All` if not supplied.</span></span>

> [!WARNING]
> <span data-ttu-id="f4770-170">OS와 데이터 디스크가 모두 암호화되었을 때 Windows VM에서 데이터 디스크 암호화를 비활성화하면 예상대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-170">Disabling data disk encryption on Windows VM when both OS and data disks have been encrypted doesn't work as expected.</span></span> <span data-ttu-id="f4770-171">대신 모든 디스크에서 암호화를 비활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-171">You must disable encryption on all disks instead.</span></span>

<span data-ttu-id="f4770-172">새 VM에서 이러한 명령 중 일부를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4770-172">Let's try some of these commands out on a new VM.</span></span>