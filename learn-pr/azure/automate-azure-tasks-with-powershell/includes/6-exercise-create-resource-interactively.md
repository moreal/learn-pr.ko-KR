원래 시나리오는 CRM 소프트웨어를 테스트할 VM을 만드는 시나리오였습니다. 새로운 빌드가 나오면 깨끗한 이미지로 전체 설치 환경을 테스트할 수 있도록 새로운 VM을 가동하는 것이 좋습니다. 그런 다음, 테스트가 완료되면 VM을 삭제하는 것이 좋습니다.

VM을 만드는 데 사용되는 명령을 사용해 보겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm-with-azure-powershell"></a>Azure PowerShell을 사용하여 Linux VM 만들기

현재 Azure 샌드박스를 사용 중이므로 리소스 그룹을 만들 필요가 없습니다. 대신에 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 이라는 리소스 그룹을 사용합니다. 또한 위치 제한 사항도 알아두어야 합니다.

PowerShell로 새로운 Azure VM을 만들어 보겠습니다.

1. `New-AzureRmVm` cmdlet을 사용하여 VM을 만듭니다.
    - **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 이라는 리소스 그룹을 사용합니다.
    - VM에 이름을 지정합니다. 일반적으로 VM의 용도 위치 및 인스턴스 번호(여러 개인 경우)를 식별하는 의미 있는 이름을 사용하는 것이 좋습니다. "미국 동부의 테스트 VM, 인스턴스 1"을 의미하는 "testvm-eus-01"이라는 이름을 사용하도록 하겠습니다. VM을 배치할 위치에 따라 고유한 이름을 생각해 내세요.
    - Azure 샌드박스에 제공되는 다음 목록 중에서 자신과 가까운 위치를 선택합니다. 아래 명령 예제를 복사해서 붙여넣을 경우 값을 변경해야 합니다.

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - 이미지의 경우 "UbuntuLTS"를 사용합니다(이 예제의 경우 Ubuntu Linux).
    - `Get-Credential` cmdlet을 사용하고, `Credential` 매개 변수에 결과를 제공합니다.
    - `-OpenPorts` 매개 변수를 추가하고 "22"를 포트로 전달합니다. 그러면 머신에 SSH로 연결할 수 있습니다.
 
    ```powershell
    New-AzureRmVm -ResourceGroupName <rgn>[Sandbox resource group name]</rgn> -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image UbuntuLTS -OpenPorts 22
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
    
1. 작업을 완료하는 데 몇 분 정도 걸립니다. 완료되면 쿼리하고 변수에 VM 개체(`$vm`)를 할당할 수 있습니다.

    ```powershell
    $vm = Get-AzureRmVM -Name "testvm-eus-01" -ResourceGroupName <rgn>[Sandbox resource group name]</rgn>
    ```
    
1. 그런 다음, 이 값을 쿼리하여 VM에 대한 정보를 쏟아냅니다.

    ```powershell
    $vm
    ```

    다음과 유사한 결과가 표시됩니다.

    ```output
    ResourceGroupName : <rgn>[Sandbox resource group name]</rgn>
    Id                : /subscriptions/xxxxxxxx-xxxx-aaaa-bbbb-cccccccccccc/resourceGroups/<rgn>[Sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/testvm-eus-01
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
    
1. 점(".") 구문을 통해 복합 개체를 구현할 수 있습니다. 예를 들어 HardwareProfile 섹션과 연결된 `VMSize` 개체의 속성을 보려면 다음을 입력하면 됩니다.

    ```powershell
    $vm.HardwareProfile
    ```

1. 또는 디스크 중 하나에 대한 정보 가져오려면 다음을 입력하면 됩니다.

    ```powershell
    $vm.StorageProfile.OsDisk
    ```

1. 다른 cmdlet에 VM 개체를 전달할 수도 있습니다. 예를 들어 이렇게 하면 VM의 공용 IP 주소가 검색됩니다.

    ```powershell
    $vm | Get-AzureRmPublicIpAddress
    ```

1. 이 IP 주소를 사용하여 SSH로 VM에 연결할 수 있습니다. 예를 들어, 사용자 이름에 "bob"을 사용하고 IP 주소는 "205.22.16.5"라면 이 명령은 Linux 머신에 연결합니다.

```powershell
ssh bob@205.22.16.5
```

## <a name="delete-a-vm"></a>VM 삭제

더 많은 명령을 사용해 보기 위해 VM을 삭제하도록 하겠습니다. 먼저 VM을 종료하겠습니다.

```powershell
Stop-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

이제 `Remove-AzureRmVM` cmdlet을 사용하여 VM을 삭제하겠습니다.

```powershell
Remove-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

리소스 그룹의 모든 리소스를 나열하려면 이 명령을 실행합니다.

```powershell
Get-AzureRmResource -ResourceGroupName $vm.ResourceGroupName | ft
```

현재 존재하는 리소스(디스크, 가상 네트워크 등)가 표시됩니다. 

```output
Microsoft.Compute/disks
Microsoft.Network/networkInterfaces
Microsoft.Network/networkSecurityGroups
Microsoft.Network/publicIPAddresses
Microsoft.Network/virtualNetworks
```

`Remove-AzureRmVM` 명령은 _VM을 삭제하기만_ 하기 때문입니다. 다른 리소스는 정리하지 않습니다. 이제 리소스 그룹 자체를 삭제하고 끝내도록 하겠습니다. 연습 내용을 간략히 살펴보면서 필요한 부분을 직접 정리하도록 하겠습니다. 명령의 패턴이 보일 것입니다.

1. 네트워크 인터페이스를 삭제합니다.

    ```powershell
    $vm | Remove-AzureRmNetworkInterface –Force
    ```
    
1. 관리되는 OS 디스크 및 저장소 계정을 삭제합니다.

    ```powershell
    Get-AzureRmDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzureRmDisk -Force
    ```

1. 다음으로, 가상 네트워크를 삭제합니다.

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmVirtualNetwork -Force
    ```

1. 네트워크 보안 그룹을 삭제합니다.

    ```powershell
    Get-AzureRmNetworkSecurityGroup -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmNetworkSecurityGroup -Force
    ```

1. 그리고 마지막으로, 공용 IP 주소를 삭제합니다.

    ```powershell
    Get-AzureRmPublicIpAddress -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmPublicIpAddress -Force
    ```

생성된 모든 리소스가 삭제되어야 합니다. 리소스 그룹을 확인해 보세요. 여기에서는 많은 수동 명령을 실행했지만 나중에 이 논리를 재사용하여 VM을 만들거나 삭제할 수 있도록 _스크립트_를 작성하는 것이 더 좋은 방법입니다. PowerShell로 스크립팅하는 방법을 살펴보겠습니다.