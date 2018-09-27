신규 스타트업 기업을 위해 재무 관리 응용 프로그램을 개발한다고 가정해 보겠습니다. 모든 고객 데이터를 보호해야 하므로 이 응용 프로그램을 호스트할 서버의 모든 OS 및 데이터 디스크에서 ADE(Azure Disk Encryption)를 구현하기로 결정했습니다. 규정 준수 요구 사항의 일부분으로 고유한 암호화 키 관리도 담당해야 합니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

이 단원에서는 기존 가상 머신에서 디스크를 암호화하고 고유한 Azure Key Vault를 사용하여 암호화 키를 관리합니다.

## <a name="prepare-the-environment"></a>환경 준비

Azure Virtual Machine에서 새 Windows VM을 배포하기 시작하겠습니다.

### <a name="deploy-windows-vm"></a>Windows VM 배포

Azure PowerShell을 사용하여 Windows 가상 머신을 만들고 배포합니다.

1. 새 리소스를 배치하는 위치를 결정하여 시작합니다. 다음 목록에서 사용자에게 가까운 지역을 선택합니다.

    <!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]
    

1. 선택된 위치를 보유하도록 PowerShell 변수를 정의합니다. 여기에서 "미국 동부"로 정의되어 있으므로 원하는 위치로 변경합니다.

    ```powershell
    $location = "eastus"
    ```
    
    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. 다음으로, 몇 가지 편리한 변수를 정의하여 VM의 _이름_ 및 _리소스 그룹_을 캡처합니다. 여기에서 미리 만든 리소스 그룹을 사용합니다. 일반적으로 `New-AzureRmResourceGroup`을 사용하여 구독에서 _새_ 리소스 그룹을 만듭니다.

    ```powershell
    $vmName = "fmdata-vm01"
    $rgName = "<rgn>[sandbox Resource Group]</rgn>"
    ```
    
1. `New-AzureRmVm`을 사용하여 새 가상 머신을 만듭니다.
    
    ```powershell
    New-AzureRmVm `
        -ResourceGroupName $rgName `
        -Name $vmName `
        -Location $location `
        -OpenPorts 3389
    ```
    
    Cloud Shell에서 프롬프트가 표시되면 VM의 사용자 이름 및 암호를 입력합니다. 이 VM에 대해 만든 초기 계정으로 사용됩니다.
    
    > [!NOTE]
    > 다양한 옵션을 제공하지 않으므로 이 명령은 일부 기본값을 사용합니다. 특히 _Windows 2016 Server_ 이미지를 _Standard_DS1_v2_ 크기로 만듭니다. VM 크기를 지정하려는 경우 기본 계층 VM에서는 ADE를 지원하지 않습니다.

1. VM 배포가 완료되면 변수에서 VM 세부 정보를 캡처합니다. 이 변수를 사용하여 만들어진 내용을 탐색할 수 있습니다.

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```
    
1. VM에 연결된 OS 디스크를 확인할 수 있습니다.

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
        
1. OS 디스크(및 데이터 디스크)에서 암호화의 현재 상태를 확인합니다.

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  `
        -ResourceGroupName $rgName `
        -VMName $vmName
    ```

    확인했듯이 디스크는 현재 _암호화되지 않았습니다_. 

    ```output
    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : NotEncrypted
    OsVolumeEncryptionSettings :
    ProgressMessage            : No Encryption extension or metadata found on the VM
    ```
    
변경을 시작해봅시다.
    
## <a name="encrypt-the-vm-disks-with-azure-disk-encryption"></a>Azure Disk Encryption을 사용하여 VM 디스크 암호화

이 데이터를 보호해야 하므로 디스크를 암호화합니다. 수행해야 하는 일부 단계가 있습니다.

1. 키 자격 증명 모음을 만듭니다.
1. 키 자격 증명 모음을 설정하여 디스크 암호화를 지원합니다.
1. Key Vault에서 저장된 키를 사용하여 VM 디스크를 암호화하도록 Azure에 지시합니다.

> [!TIP]
> 개별적으로 단계를 설명하려고 하지만 고유한 구독에서 이 작업을 수행하는 경우 이 모듈의 요약에 연결된 유용한 PowerShell 스크립트를 사용할 수 있습니다.

### <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기

Azure Key Vault를 만들려면 구독에서 서비스를 사용하도록 설정해야 합니다. 이 설정은 한 번만 수행하면 됩니다.

> [!TIP]
> 구독에 따라 `Register-AzureRmResourceProvider` cmdlet을 사용하여 **Microsoft.KeyVault** 공급자를 사용하도록 설정할 수 있습니다. 이 작업은 Azure 샌드박스 구독에 필요하지 않습니다.

1. 새 키 자격 증명 모음의 이름을 지정합니다. 이름은 고유해야 하며, 숫자, 영문자 및 대시로 구성된 3-24자 사이이면 됩니다. 끝에 몇 가지 임의의 숫자를 추가하여 아래의 "1234"를 바꿉니다.

    ```powershell
    $keyVaultName = "mvmdsk-kv-1234"
    ```
        
1. `New-AzureRmKeyVault`를 사용하여 Azure Key Vault를 만듭니다.
    - VM과 동일한 리소스 그룹 _및_ 위치에 배치해야 합니다.
    - 디스크 암호화에 사용할 Key Vault를 사용하도록 설정합니다. 
    - 고유한 Key Vault 이름을 지정합니다.

    ```powershell
    New-AzureRmKeyVault -VaultName $keyVaultName `
        -Location $location `
        -ResourceGroupName $rgName `
        -EnabledForDiskEncryption
    ```

    이 명령에서 액세스 권한이 없는 사용자에 대한 경고가 발생합니다.

    ```output
    WARNING: Access policy is not set. No user or application have access permission to use this vault. This can happen if the vault was created by a service principal. Please use Set-AzureRmKeyVaultAccessPolicy to set access policies.
    ```

    자격 증명 모음을 사용하여 VM의 암호화 키를 저장하고 있으므로 문제가 발생하지 않으며 사용자는 이 데이터에 액세스할 필요가 없습니다.

### <a name="encrypt-the-disk"></a>디스크 암호화

디스크를 암호화할 준비가 거의 다 되었습니다. 수행하기 전에 백업 만들기에 대한 경고가 발생합니다.

> [!IMPORTANT]
> 프로덕션 시스템인 경우 Azure Backup을 사용하거나 스냅숏을 만들어서 관리 디스크의 백업을 수행해야 합니다. Azure Portal 또는 명령줄을 통해 스냅숏을 만들 수 있습니다. PowerShell에서 `New-AzureRmSnapshot` cmdlet을 사용합니다. 이 간단한 연습이 완료되면 이 데이터를 throw하므로 이 단계를 건너뛰도록 하겠습니다. 

1. Key Vault 정보를 보유하도록 변수를 정의하기 시작합니다.

    ```powershell
    $keyVault = Get-AzureRmKeyVault `
        -VaultName $keyVaultName `
        -ResourceGroupName $rgName
    ```

1. 그런 다음, `Set-AzureRmVmDiskEncryptionExtension` cmdlet을 사용하여 VM 디스크를 암호화합니다.
    - `VolumeType` 매개 변수를 사용하면 암호화할 디스크를 지정할 수 있습니다. [_모두_ | _OS_ | _데이터_] _모두_로 초기화됩니다. 일부 Linux 배포에 대한 데이터 디스크만 암호화할 수 있습니다.
    - 관리 디스크의 `SkipVmBackup` 플래그를 제공해야 합니다. 그렇지 않으면 스냅숏이 없으므로 명령이 실패합니다.

    ```powershell
    Set-AzureRmVmDiskEncryptionExtension `
        -ResourceGroupName $rgName `
        -VMName $vmName `
        -VolumeType All `
        -DiskEncryptionKeyVaultId $keyVault.ResourceId `
        -DiskEncryptionKeyVaultUrl $keyVault.VaultUri `
        -SkipVmBackup
    ```

1. cmdlet에서는 VM이 오프라인 상태로 전환되고 작업을 완료하는 데 몇 분 정도가 걸릴 수 있다고 경고합니다. 계속 진행합니다.

    ```output
    Enable AzureDiskEncryption on the VM
    This cmdlet prepares the VM and enables encryption which may reboot the machine and takes 10-15 minutes to
    finish. Please save your work on the VM before confirming. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
    ```
    
1. 작업이 완료되면 암호화 상태를 다시 확인합니다.

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
    ```

    이제 OS 디스크가 암호화되어야 합니다. Windows에 표시되는 연결된 데이터 디스크가 암호화됩니다.

    ```output
    OsVolumeEncrypted          : Encrypted
    DataVolumesEncrypted       : NoDiskFound
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : Provisioning succeeded
    ```

> [!NOTE]        
> 암호화를 자동으로 암호화하지 _않으면_ 새 디스크가 추가되었습니다. `Set-AzureRmVMDiskEncryptionExtension` cmdlet을 다시 실행하여 새 디스크를 암호화할 수 있습니다. 이미 디스크를 암호화한 VM에 디스크를 추가하는 경우 새 시퀀스 번호를 입력해야 합니다. 또한 운영 체제에 표시되지 않는 디스크를 암호화하지 않습니다. 디스크를 제대로 분할하고, 포맷하고, 탑재하여 Bitlocker 확장에서 표시해야 합니다.