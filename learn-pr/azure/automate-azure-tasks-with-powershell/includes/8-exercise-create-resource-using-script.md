이 연습에서는 Linux 관리 도구를 만드는 회사의 예제를 계속 사용합니다. Linux VM을 사용하여 잠재 고객이 소프트웨어를 테스트하도록 할 계획입니다. 리소스 그룹이 준비되었고 이제 VM을 만들겠습니다.

회사는 대규모 Linux 무역 박람회에서 부스에 대한 비용을 지급했습니다. 별도의 Linux VM에 연결된 세 개의 터미널을 포함하는 데모 영역을 계획합니다. 매일 끝날 때 VM을 삭제하고 다시 만들어 매일 아침 새로 시작합니다. 피곤할 때 작업 후에 수동으로 VM을 만들면 오류가 발생할 수 있습니다. VM 만들기 프로세스를 자동화하기 위해 PowerShell 스크립트를 작성하려고 합니다.

## <a name="write-a-script-that-creates-virtual-machines"></a>가상 머신을 만드는 스크립트 작성

다음 단계를 수행하여 스크립트를 작성합니다.

1. **ConferenceDailyReset.ps1**이라는 새 텍스트 파일을 만듭니다.

2. 매개 변수를 변수로 캡처합니다.

    ```powershell
    param([string]$resourceGroup)
    ```

3. 자격 증명을 사용하여 Azure로 인증합니다.

    ```powershell
    Connect-AzureRmAccount
    ```

4. VM의 관리자 계정에 대한 사용자 이름 및 암호를 묻는 메시지를 표시하고 결과를 변수로 캡처합니다.

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. 세 번 실행되는 루프를 만듭니다.

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. 루프 본문에서 각 VM의 이름을 만들고 변수에 저장합니다.

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. 다음으로 `$vmName` 변수를 사용하여 VM을 만듭니다.

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. 파일을 저장합니다.

완료된 스크립트는 다음과 같이 표시됩니다.

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>스크립트 실행

PowerShell을 시작하고 스크립트 파일을 저장한 디렉터리로 변경합니다. 스크립트를 실행하려면 다음 명령을 실행합니다.

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

스크립트를 완료하는 데 몇 분이 걸릴 수 있습니다. 완료되면 성공적으로 실행되었는지 확인합니다.

1. 브라우저에서 Azure Portal에 로그인합니다.
2. 왼쪽 탐색에서 **리소스 그룹**을 클릭합니다.
3. 리소스 그룹 목록에서 **TrialsResourceGroup**을 클릭합니다. 리소스 목록에 새로 만든 VM 및 연결된 리소스가 표시됩니다.

## <a name="summary"></a>요약
스크립트 매개 변수로 표시된 리소스 그룹에서 세 개의 VM 만들기를 자동화하는 스크립트를 작성했습니다. 스크립트는 짧고 간단하지만 포털을 통해 수동으로 완료하는 데 시간이 오래 걸리는 프로세스를 자동화합니다.