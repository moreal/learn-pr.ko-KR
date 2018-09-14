신규 스타트업 기업을 위해 재무 관리 응용 프로그램을 개발한다고 가정해 보겠습니다. 이 응용 프로그램을 호스트 하는 서버의 모든 OS 및 데이터 디스크에서 Azure 디스크 암호화 (ADE)을 구현 하기로 결정 했으면 하므로 고객의 모든 데이터를 보호를 확인 해야 합니다. 또한 규정 준수 요구 사항의 일부분으로 자체 암호화 키도 관리해야 합다.

이 단위에 기존 Windows Vm에서 디스크를 암호화 하 고 Azure Key Vault를 사용 하 여 암호화 키를 관리 합니다.

> [!IMPORTANT] 
> 이 연습에서는 Azure PowerShell이 컴퓨터에 설치 되어 있는지 가정 합니다. 로 이동 [PowerShellGet 사용 하 여 Windows에서 Azure PowerShell 설치](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0) Azure PowerShell을 설치 하는 방법에 대 한 정보에 대 한 합니다.

## <a name="prepare-the-environment"></a>환경 준비

새 리소스 그룹에 Windows VM을 배포 하 여 시작 하 고 VM에 데이터 디스크를 추가 하겠습니다.

### <a name="deploy-windows-vm-using-the-azure-portal"></a>Azure portal을 사용 하 여 Windows VM 배포

여기 만들고 Windows VM을 배포 하는 Azure portal을 사용 합니다. 먼저 기본 VM 정보부터 정의합니다.

1. 브라우저에서 [Azure Portal](http://portal.azure.com)로 이동하여 기본 자격 증명으로 로그인합니다.

1. 사이드바에서 **가상 머신**, **가상 머신 만들기**를 차례로 클릭합니다.

1. 계산 블레이드의 **권장** 섹션에서 **Windows Server**를 클릭합니다.

1. **Windows Server** 블레이드에서 **Windows Server 2016 Datacenter**를 클릭합니다.

1. **Windows Server 2016 Datacenter** 블레이드에서 **만들기**를 클릭합니다.

1. **기본 사항** 블레이드의 **이름** 상자에 **moneyappsvr01**을 입력합니다.

1. **사용자 이름** 및 **암호** 상자에 이 서버의 관리자 계정 이름과 암호를 입력합니다.

1. **구독** 상자에서 Azure 구독을 선택합니다.

1. 아래 **리소스 그룹**를 선택 **새로 만들기**합니다. 상자에서 입력 **moneyapprg**합니다.

1. **위치** 드롭다운 목록에서 인근 지역을 선택합니다.

1. **확인**을 클릭합니다.

### <a name="choose-a-size-for-the-vm-and-start-the-deployment"></a>VM의 크기를 선택하고 배포를 시작합니다.

> [!IMPORTANT]
> 기본 계층 Vm ADE를 지원 하지 않는 것을 기억 합니다.

1. 에 **크기 선택** 블레이드에서 **표준** SKU와 같은 **B1s**. 그런 다음, **선택**을 클릭합니다.

1. 에 **설정** 블레이드는 **공용 인바운드 포트를 선택** 목록에서 **RDP**합니다. 그런 다음 아래로 스크롤하여 클릭 **확인**합니다.

1. **만들기** 블레이드에서 **만들기**를 클릭합니다.

1. VM이 배포될 때까지 기다렸다가 연습을 계속 진행합니다.

### <a name="add-a-data-disk-to-the-vm"></a>VM에 데이터 디스크 추가

1. 왼쪽 메뉴에서 **모든 리소스**를 클릭한 다음, **moneyappsvr01**을 클릭합니다.

1. **가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.

1. **디스크** 블레이드에서 OS 디스크 암호화 상태가 현재 **사용 안 함**인지 확인한 후에 **데이터 디스크 추가**를 클릭합니다.

1. **이름** 목록을 클릭하고 **디스크 만들기**를 클릭합니다.

1. **관리 디스크 만들기** 블레이드의 **이름** 상자에 **moneyappsvr01_data**를 입력합니다.

1. **리소스 그룹**에서 **기존 항목 사용**을 선택한 다음 목록에서 **moneyapprg**를 선택합니다.

1. **만들기**를 클릭합니다.

1. 디스크가 만들어질 때까지 기다렸다가 계속 진행합니다.

1. **디스크** 블레이드에서 **저장**을 클릭합니다. 데이터 디스크 암호화 상태는 참고는 현재 **해제**합니다.

## <a name="configure-disk-encryption-prerequisites"></a>디스크 암호화 필수 구성 요소 구성

이제 Azure Disk Encryption 필수 구성 요소 구성 스크립트를 사용 하 여 모든 디스크 암호화 필수 구성 요소 구성 됩니다. 이 스크립트를 만들고 VM과 동일한 지역에 key vault를 준비 합니다.

### <a name="prepare-the-azure-disk-encryption-prerequisite-setup-script"></a>Azure Disk Encryption 필수 구성 요소 설치 스크립트를 준비 합니다.

1. 로 이동 합니다 [Azure Disk Encryption 필수 구성 요소 설치 스크립트](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) GitHub 페이지입니다.

1. GibHub 페이지에서 **원시**를 클릭합니다.

1. 페이지의 모든 텍스트를 선택한 다음 Ctrl + C를 사용 하 여 페이지의 모든 텍스트를 클립보드에 복사 하려면 Ctrl + A를 사용 합니다.

1. 컴퓨터에서 클릭 **시작**, 한 다음 **Windows PowerShell ISE**합니다.

1. 마우스 오른쪽 단추로 클릭 **Windows PowerShell ISE**, 클릭 **관리자 권한으로 실행**합니다.

1. 관리자에서: Windows PowerShell ISE 창 클릭 **뷰**를 클릭 하 고 **스크립트 창 표시**합니다.

1. 스크립트 창에 복사한 텍스트를 붙여넣습니다.

1. 스크립트 창에서 다음 코드 블록을 찾습니다.

    ```powershell
    [Parameter(Mandatory = $false,
            HelpMessage="Name of the AAD application that will be used to write secrets to KeyVault. A new application with this name will be created if one doesn't exist. If this app already exists, pass aadClientSecret parameter to the script")]
    [ValidateNotNullOrEmpty()]
    [string]$aadAppName,
    ```
1. 코드 블록에서 `$false`를 `$true`로 변경합니다.

1. **파일**, **다른 이름으로 저장**을 차례로 클릭한 다음 스크립트를 저장하는 데 사용할 폴더로 이동합니다.

1. **파일 이름** 상자에 **ADEPrereqScript.ps1**을 입력하고 **저장**을 클릭합니다.

### <a name="run-the-azure-disk-encryption-prerequisite-setup-script"></a>Azure Disk Encryption 필수 구성 요소 설치 스크립트를 실행 합니다.

1. PowerShell ISE에서 콘솔 창, 명령 입력 하 고 다음을 누릅니다 **Enter**:

   ```console
   cd <path to your folder containing ADEPrereqScript.ps1>
   ```

1. PowerShell ISE에서 콘솔 창, 명령 입력 하 고 다음을 누릅니다 **Enter**:

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

   **실행 규칙 변경** 대화 상자가 표시되면 **모두 예** 또는 **예**(_모두 예_ 옵션이 표시되지 않는 경우)를 클릭합니다.

1. PowerShell ISE에서 콘솔 창, 명령 입력 하 고 다음을 누릅니다 **Enter**:

   ```powershell
   Login-AzureRmAccount
   ```

1. Azure 자격 증명을 입력합니다.

1. **SubscriptionId** 문자열을 선택하여 클립보드에 복사합니다.

1. PowerShell ISE에서 클릭 **파일**를 클릭 하 고 **실행**합니다.

1. 콘솔 창에서에 **resourceGroupName:** 프롬프트에 입력 **moneyapprg**합니다. 누릅니다 **Enter**합니다.

1. 콘솔 창에서에 **keyVaultName:** 프롬프트에 입력 **moneyappkv**합니다. 누릅니다 **Enter**합니다.

1. 콘솔 창의 **location:** 프롬프트에 VM을 만들 때 사용한 위치를 입력합니다.

1. 콘솔 창의 **subscriptionId:** 프롬프트에 구독 ID를 붙여넣습니다.

1. 이렇게 하면 **moneyappkv** Key Vault가 만들어집니다. 이 작업이 완료되면 녹색 요약 텍스트를 선택하여 메모장에 복사합니다.

1. 키를 눌러 **Enter** 를 계속 합니다.

1. 콘솔 창에서에 **aadAppName:** 프롬프트에 입력 **moneyapp**합니다. 누릅니다 **Enter**합니다.

1. 이렇게 하면 **moneyapp** Azure AD 응용 프로그램이 만들어집니다. 이 작업이 완료되면 녹색 요약 텍스트를 선택하여 메모장에 복사합니다.

1. 키를 눌러 **Enter** 를 계속 합니다.

### <a name="encrypt-your-vm-disks-with-powershell"></a>PowerShell을 사용하여 VM 디스크 암호화

OS 및 데이터 디스크의 암호화 상태를 확인합니다.

1. PowerShell ISE에서 콘솔 창, 명령 입력 하 고 다음을 누릅니다 **Enter**:

    ```powershell
    $vmName = 'moneyappsvr01'
    ```

    > [!NOTE]
    > VM 이름은 작은따옴표로 묶어야 합니다.

1. PowerShell ISE 스크립트 창에서 다음을 입력 명령 및 키를 눌러 **Enter**:

    ```powershell
    Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
    ```

1. **VM에서 AzureDiskEncryption 사용** 대화 상자에서 **예**를 클릭하고 암호화를 완료하려면 10-15분이 걸린다는 메시지를 확인합니다.

>[!IMPORTANT]
> 이 명령은이 연습을 진행 하기 전에 완료 될 때까지 기다립니다.

### <a name="verify-the-encryption-status-of-your-vm-disks"></a>VM 디스크의 암호화 상태를 확인합니다.

Azure Portal로 전환합니다. 에 **디스크** 에 대 한 블레이드 **moneyappsvr01**, OS 및 데이터 디스크에 대 한 디스크 암호화 상태를 이제는 **Enabled**합니다.
