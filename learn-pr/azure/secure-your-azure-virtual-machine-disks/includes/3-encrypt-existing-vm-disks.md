회사에서 모든 VM에 ADE(Azure Disk Encryption)를 구현하기로 결정했다고 가정해 보겠습니다. 기존 VM 볼륨에 암호화를 롤아웃하는 방법을 평가해야 합니다. 여기서는 ADE의 요구 사항과 기존 Linux 및 Windows VM의 디스크를 암호화하기 위한 단계를 살펴보겠습니다.

## <a name="azure-disk-encryption-prerequisites"></a>Azure Disk Encryption 필수 구성 요소

VM 디스크를 암호화하려면 먼저 다음을 수행해야 합니다.

1. Key Vault를 만듭니다.
1. Key Vault 액세스 정책을 설정하여 디스크 암호화를 지원합니다.
1. Key Vault를 사용하여 ADE에 대한 암호화 키를 저장합니다.

### <a name="azure-key-vault"></a>Azure Key Vault

ADE에 사용되는 암호화 키를 Azure Key Vault에 저장할 수 있습니다. Azure Key Vault는 비밀을 안전하게 저장하고 액세스하기 위한 도구입니다. 비밀은 API 키, 암호 또는 인증서와 같이 액세스를 엄격하게 제어하려는 모든 항목입니다. 비밀을 활용하는 경우 FIPS(Federal Information Processing Standard) 140-2 수준 2 유효성이 검사된 HSM(하드웨어 보안 모듈)에 정의된 대로 가용성과 확장성이 뛰어난 보안 저장소가 제공됩니다. Key Vault를 사용하면 데이터를 암호화하는 데 사용되는 키를 완벽하게 제어할 수 있으며 키 사용을 관리 및 감사할 수 있습니다. 

> [!NOTE]
> Azure Disk Encryption을 사용하려면 Key Vault와 VM이 같은 Azure 지역에 있어야 합니다. 그래야 암호화 비밀이 다른 지역에 노출되지 않습니다.

다음을 사용하여 Key Vault를 구성하고 관리할 수 있습니다.

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmKeyVault -Location <location> `
    -ResourceGroupName <resource-group> `
    -VaultName "myKeyVault" `
    -EnabledForDiskEncryption
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az keyvault create \
    --name "myKeyVault" \
    --resource-group <resource-group> \
    --location <location> \
    --enabled-for-disk-encryption True
```

### <a name="azure-portal"></a>Azure Portal

Azure Key Vault는 일반 리소스 생성 프로세스를 사용하여 Azure Portal에서 만들 수 있는 리소스입니다.

1. 왼쪽에 있는 사이드바에서 **리소스 만들기**를 클릭합니다.

1. "Key Vault"를 검색합니다. 세부 정보 창에서 **만들기**를 클릭합니다.

    ![Azure Marketplace의 Key Vault를 보여 주는 스크린샷](../media/3-create-keyvault.png)

1. 새 Key Vault에 대한 세부 정보를 입력합니다.
    - Key Vault의 **이름** 입력
    - 배치할 구독을 선택합니다(현재 구독의 기본값).
    - **리소스 그룹**를 선택하거나 Key Vault를 소유할 새 리소스 그룹을 만듭니다.
    - Key Vault의 **위치**를 선택합니다. VM이 있는 위치를 선택해야 합니다.
    - 가격 책정 계층에 대해 표준 또는 프리미엄을 선택할 수 있습니다. 주요 차이점은 프리미엄 계층에서는 하드웨어 암호화 백업 키를 허용한다는 것입니다.

1. 디스크 암호화를 지원하도록 액세스 정책을 변경해야 합니다. 기본적으로 _사용자_ 계정을 정책에 추가합니다.
    - **액세스 정책** 선택
    - **고급 액세스 정책**을 클릭합니다.
    - **볼륨 암호화를 위한 Azure Disk Encryption 액세스 사용**을 확인합니다.
    - 원하는 경우 계정을 제거할 수 있으며, 디스크 암호화에 Key Vault만 사용하려는 경우에는 필요하지 않습니다.
    - **확인**을 클릭하여 변경 내용을 저장합니다.

    ![Azure Disk Encryption 옵션을 선택하고 강조 표시한 Key Vault의 고급 속성을 보여 주는 스크린샷](../media/3-configure-access-policy.png)

1. **만들기**를 클릭하여 새 Key Vault를 만듭니다.

## <a name="enabling-access-policies-in-the-key-vault"></a>Key Vault에서 액세스 정책 사용
Azure는 VM을 부팅하고 볼륨을 해독할 수 있도록 Key Vault의 암호화 키 또는 비밀에 액세스해야 합니다. 위의 **고급 액세스 정책**을 변경했을 때 포털에서 이를 다루었습니다.

세 가지 정책을 사용할 수 있습니다.
1. **디스크 암호화** - Azure Disk Encryption에 필요합니다.
1. **배포** - (선택 사항) 이 Key Vault가 리소스를 만들 때(예: 가상 머신 만들 때) 참조되는 경우 Microsoft.Compute 리소스 공급자에서 이 Key Vault으로부터 비밀을 검색할 수 있도록 합니다.
1. **템플릿 배포** - (선택 사항) 이 Key Vault가 템플릿 배포에서 참조되는 경우 Azure Resource Manager에서 이 Key Vault으로부터 비밀을 가져올 수 있도록 합니다.

디스크 암호화 정책을 사용하는 방법은 다음과 같습니다. 다른 두 개는 유사하지만 다른 플래그를 사용합니다.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <keyvault-name> -ResourceGroupName <resource-group> -EnabledForDiskEncryption
```

```azurecli
az keyvault update --name <keyvault-name> --resource-group <resource-group> --enabled-for-disk-encryption "true"
```

## <a name="encrypting-an-existing-vm-disk"></a>기존 VM 디스크 암호화

Key Vault 설정이 완료되면 Azure CLI 또는 Azure PowerShell을 사용하여 VM을 암호화할 수 있습니다. 처음으로 Windows VM을 암호화할 때 모든 디스크 또는 OS 디스크만 암호화하도록 선택할 수 있습니다. 일부 Linux 배포에서는 데이터 디스크만 암호화할 수 있습니다. 암호화를 받으려면 Windows 디스크가 NTFS 볼륨으로 포맷되어야 합니다.

> [!WARNING]
> 암호화를 설정하려면 먼저 관리 디스크의 스냅숏 또는 백업을 수행해야 합니다. 아래에 지정된 `SkipVmBackup` 플래그는 관리 디스크에서 백업이 완료되었음을 도구에 알려줍니다. 백업 없이, 어떤 이유로 암호가 실패하면 VM을 복구할 수 없습니다.

PowerShell을 통해 `Set-AzureRmVmDiskEncryptionExtension` cmdlet을 사용하여 암호화를 활성화합니다.

```powershell

Set-AzureRmVmDiskEncryptionExtension `
    -ResourceGroupName <resource-group> `
    -VMName <vm-name> `
    -VolumeType [All | OS | Data]
    -DiskEncryptionKeyVaultId <keyVault.ResourceId> `
    -DiskEncryptionKeyVaultUrl <keyVault.VaultUri> `
     -SkipVmBackup
```

Azure CLI의 경우 `az vm encryption enable` 명령을 사용하여 암호화를 활성화합니다.

```azurecli
az vm encryption enable \
    --resource-group <resource-group> \
    --name <vm-name> \
    --disk-encryption-keyvault <keyvault-name> \
    --volume-type [all | os | data] \
    --skipvmbackup
```

## <a name="viewing-the-status-of-the-disk"></a>디스크 상태 보기

특정 디스크가 암호화되었는지 여부를 확인할 수 있습니다.

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName <resource-group> -VMName <vm-name>
```

```azurecli
az vm encryption status --resource-group <resource-group> --name <vm-name>
```

이 두 명령은 모두 지정된 VM에 연결된 각 디스크의 상태를 반환합니다.

## <a name="decrypting-drives"></a>드라이브 암호 해독

`Disable-AzureRmVMDiskEncryption`을 사용하여 PowerShell을 통해 암호화를 반대로 할 수 있습니다

```powershell
Disable-AzureRmVMDiskEncryption -ResourceGroupName <resource-group> -VMName <vm-name>
```

Azure CLI의 경우 `vm encryption disable` 명령을 사용합니다.

```azurecli
az vm encryption disable --resource-group <resource-group> --name <vm-name>
```

이러한 명령은 지정된 가상 머신에 대해 모든 형식의 볼륨에 대한 암호화를 비활성화합니다. 암호화 버전과 마찬가지로 `-VolumeType` 매개 변수 `[All | OS | Data]`를 지정하여 암호를 해독할 디스크를 결정할 수 있습니다. 제공되지 않는 경우 기본값은 `All`입니다.

> [!WARNING]
> OS와 데이터 디스크가 모두 암호화되었을 때 Windows VM에서 데이터 디스크 암호화를 비활성화하면 예상대로 작동하지 않습니다. 대신 모든 디스크에서 암호화를 비활성화해야 합니다.

새 VM에서 이러한 명령 중 일부를 사용해 보겠습니다.