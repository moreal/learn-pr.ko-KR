이 단원에서는 Linux 관리 도구를 만드는 회사의 예제를 계속 사용합니다. Linux VM을 사용하여 잠재 고객이 소프트웨어를 테스트하도록 할 계획입니다. 리소스 그룹이 준비되었고 이제 VM을 만들겠습니다.

회사는 대규모 Linux 무역 박람회에서 부스에 대한 비용을 지급했습니다. 별도의 Linux VM에 연결된 세 개의 터미널을 포함하는 데모 영역을 계획합니다. 매일 끝날 때 VM을 삭제하고 다시 만들어 매일 아침 새로 시작합니다. 피곤할 때 작업 후에 수동으로 VM을 만들면 오류가 발생할 수 있습니다. VM 만들기 프로세스를 자동화하기 위해 PowerShell 스크립트를 작성하려고 합니다.

## <a name="write-a-script-that-creates-virtual-machines"></a>Virtual Machines를 만드는 스크립트 작성

스크립트를 작성할 수 있는 권한을 얻으려면 Cloud Shell에서 다음 단계를 수행합니다.

1. Cloud Shell에서 홈 폴더로 전환합니다.

    ```powershell
    cd $HOME\clouddrive
    ```

1. **ConferenceDailyReset.ps1**이라는 새 텍스트 파일을 만듭니다.

    ```powershell
    touch "./ConferenceDailyReset.ps1"
    ```

1. 통합 편집기를 열고 **ConferenceDailyReset.ps1** 파일을 엽니다.

    ```powershell
    code "./ConferenceDailyReset.ps1"
    ```
    > [!TIP]
    > 통합 Cloud Shell에서는 vim, nano 및 emacs도 지원하므로 선호하는 편집기를 사용할 수 있습니다.

1. 입력 매개 변수를 변수로 캡처하여 시작합니다. 다음 줄을 스크립트에 추가합니다.

    ```powershell
    param([string]$resourceGroup)
    ```

    > [!NOTE]
    > 일반적으로 `Connect-AzureRmAccount`를 사용하여 자격 증명을 통해 Azure에서 인증해야 하며 스크립트에서 이 작업을 수행할 수 있습니다. 그러나 Cloud Shell 환경에서는 미리 인증이 되므로 이는 불필요한 작업입니다.

1. VM의 관리자 계정에 대한 사용자 이름과 암호를 묻는 메시지를 표시하고 결과를 변수로 캡처합니다.

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. 세 번 실행되는 루프를 만듭니다.

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

1. 루프 본문에서 각 VM의 이름을 만들고, 변수에 저장하고, 콘솔에 출력합니다.

    ```powershell
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    ```

1. 다음으로, `$vmName` 변수를 사용하여 VM을 만듭니다.

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
   ```

1. 파일을 저장합니다. 편집기의 오른쪽 위 모서리에서 "..." 메뉴를 사용할 수 있습니다. 저장을 위한 일반 액셀러레이터 키도 있습니다.

완료된 스크립트는 다음과 같이 표시됩니다.

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>스크립트 실행

"..." 상황에 맞는 메뉴를 통해 편집기를 닫습니다.

1. 스크립트를 실행합니다.

    ```powershell
    .\ConferenceDailyReset.ps1 <rgn>[Sandbox resource group name]</rgn>
    ```
    
스크립트를 완료하는 데는 몇 분 정도 걸릴 수 있습니다. 완료되면 리소스 그룹에 포함된 리소스를 확인하여 스크립트가 성공적으로 실행되었는지 확인합니다.

```powershell
Get-AzureRmResource -ResourceType Microsoft.Compute/virtualMachines
```

각각 고유한 이름을 가진 세 개의 VM이 표시됩니다.

스크립트 매개 변수로 표시된 리소스 그룹에서 세 개의 VM 만들기를 자동화하는 스크립트를 작성했습니다. 스크립트는 짧고 간단하지만 포털을 통해 수동으로 완료하는 데 시간이 오래 걸리는 프로세스를 자동화합니다.