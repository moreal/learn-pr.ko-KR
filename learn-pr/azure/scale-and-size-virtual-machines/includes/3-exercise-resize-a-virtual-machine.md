이 연습에서는 가상 머신을 만든 다음, 포털 및 Azure PowerShell을 사용하여 크기를 조정합니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-vm-with-powershell"></a>PowerShell을 사용하여 VM 만들기

1. Azure PowerShell에서 `New-AzureRmVm` cmdlet을 사용하여 VM을 만들겠습니다.
    - 리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.
    - "my-test-vm"의 이름을 지정합니다.
    - **크기** 매개 변수에 대해 _Standard_DS2_v2_를 전달합니다.
    - Azure 샌드박스에서 사용할 수 있는 다음 목록 중에서 사용자에게 가까운 위치를 선택합니다. 복사해서 붙여넣을 경우 아래 명령 예제에서 값을 변경해야 합니다.

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - `Get-Credential` cmdlet을 사용하고, 아래에 표시된 대로 `Credential` 매개 변수에 결과를 제공합니다.

       자격 증명을 입력하라는 메시지가 표시되면 LocalAdmin을 사용자 이름으로 사용하고, Adm1nPa$$word를 암호로 사용합니다.

    ```powershell
    New-AzureRmVm `
        -ResourceGroupName <rgn>[sandbox resource group name]</rgn> `
        -Name my-test-vm `
        -Credential (Get-Credential) `
        -Size "Standard_DS2_v2" `
        -Location eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


1. 배포가 완료될 때까지 기다린 후에 연습을 계속 진행하세요.

## <a name="resize-using-the-portal"></a>포털을 사용하여 크기 조정

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [샌드박스용 Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. 왼쪽 사이드바에서 **리소스 그룹**을 선택합니다.

1. <rgn>[샌드박스 리소스 그룹 이름]</rgn> 리소스 그룹을 선택하고, 개요에서 **my-test-vm** 가상 머신 개체를 클릭합니다.

1. 가상 머신의 **개요**에서 현재 VM 크기는 조금 전에 만든 대로 _표준 DS2 v2(2개 vCPU, 7GB 메모리)_ 입니다.

1. **설정** 섹션에서 **크기**를 선택합니다.

1. **크기 선택** 블레이드에서 **F2s_v2** 크기를 찾으려고 합니다. VM이 현재 실행 중이고 해당 크기는 다양한 제품군이 있으므로 사용 가능한 크기 목록에 표시되지 않습니다. 경우에 따라 사용 가능한 모든 VM 크기를 확인하기 위해 VM을 중지해야 합니다.

1. 이 VM이 실행되는 동안 현재 사용할 수 있는 크기를 선택하겠습니다. **크기 선택** 블레이드에서 작업하는 동안 _DS3_v2 표준_을 선택한 다음, **선택**을 클릭합니다. 가상 머신의 크기 조정에 대한 알림을 확인하세요.

1. **개요** 패널에서 VM의 크기가 _표준 DS3 v2(4개 vCPU, 14GB 메모리)_ 로 조정되었는지 확인합니다.

## <a name="resize-using-powershell"></a>PowerShell을 사용하여 크기 조정

1. Azure Portal에 있는 위의 도구 모음에서 Cloud Shell 단추를 클릭하여 Azure Cloud Shell을 엽니다.

    Cloud Shell 창의 왼쪽 위에서 Bash가 아닌 PowerShell을 사용하도록 Cloud Shell이 설정되었는지 확인합니다.

1. 다음 cmdlet을 사용하여 사용 가능한 가상 머신 크기 목록을 가져옵니다.

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    ```

1. 다음 cmdlet을 실행하여 가상 머신의 크기를 _DS2_v2_ 크기로 조정합니다.

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    $vm.HardwareProfile.VmSize = "Standard_DS2_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```

1. PowerShell 명령이 종료되기를 기다리는 동안 **my-test-vm** 블레이드에서 **새로 고침** 단추를 클릭합니다. 가상 머신이 크기 변경에 맞게 다시 시작되는지 유의해야 합니다.

이 연습에서는 가상 머신을 만들고 두 개의 다른 도구를 사용하여 크기를 조정했습니다. 가상 머신이 실행되는 동안에는 대상 크기를 사용할 수 없다는 점을 기억하는 것이 좋습니다. 가상 머신을 중지하면 더 많은 크기를 선택할 수 있습니다.