이전 연습에서는 Azure Portal을 사용하여 다음 작업을 수행했습니다.

- OS 디스크 캐시 상태 보기
- OS 디스크 캐시 설정 변경
- VM에 데이터 디스크 추가
- 새 데이터 디스크의 캐싱 유형 변경

이제 Azure PowerShell을 사용하여 이러한 작업을 연습해 보겠습니다. 

> [!NOTE]
> Azure PowerShell을 사용하려고 하지만 콘솔 기반 도구와 유사한 기능을 제공하는 Azure CLI를 사용할 수도 있습니다. 이것은 macOS, Linux 및 Windows에서 실행됩니다. Azure CLI에 대해 자세히 알아보려면 **Azure CLI를 사용하여 가상 머신 관리** 모듈를 체크 아웃하세요.

이전 연습에서 만든 VM을 사용하겠습니다. 이 랩의 작업은 다음을 가정합니다.

- **fotoshareVM**이라고 하는 VM이 있습니다.
- VM은 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 이라는 리소스 그룹에 있습니다.

다른 이름 집합을 사용한 경우 이러한 값을 사용자 값으로 바꿉니다.

마지막 연습에서 VM 디스크의 현재 상태는 다음과 같습니다.

![둘 다 읽기 전용 캐싱으로 설정된 OS 및 데이터 디스크의 스크린샷입니다.](../media/disks-final-config-portal.PNG)

포털을 사용하여 OS 디스크와 데이터 디스크 모두에 대해 ***호스트 캐싱** 필드를 설정했습니다. 다음 단계를 진행하면서 이 초기 상태를 명심하세요.

### <a name="set-up-some-variables"></a>일부 변수 설정

먼저, 나중에 사용할 수 있도록 일부 리소스 이름을 저장하겠습니다.

1. 오른쪽에 있는 Azure Cloud Shell 터미널을 사용하여 다음 PowerShell 명령을 실행합니다.

    > [!NOTE]
    > 해당 명령을 실행하기 전에 Cloud Shell 세션을 **PowerShell**로 전환하세요.
    
    ```powershell
    $myRgName = "<rgn>[sandbox resource group name]</rgn>"
    $myVMName = "fotoshareVM"
    ```
    
    > [!TIP]
    > Cloud Shell 세션의 시간이 초과되면 이러한 변수를 다시 설정해야 합니다. 따라서 가능하다면 이 전체 랩을 단일 세션에서 작업합니다.
    
### <a name="get-info-about-our-vm"></a>VM에 대한 정보 가져오기

1. 다음 명령을 실행하여 VM의 속성을 다시 가져옵니다.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVmName
    ```
    
1. 응답을 `$myVM` 변수에 저장합니다. 출력을 `select-object` cmdlet으로 전달하여 디스플레이를 특정 속성으로 필터링할 수 있습니다.

    ```powershell
    $myVM | select-object -property ResourceGroupName, Name, Type, Location
    ```
    
1. 다음과 유사한 출력이 표시됩니다.

    ```output
    ResourceGroupName Name        Type                              Location
    ----------------- ----        ----                              --------
    <rgn>[sandbox resource group name]</rgn> fotoshareVM Microsoft.Compute/virtualMachines eastus
    ```
    
### <a name="view-os-disk-cache-status"></a>OS 디스크 캐시 상태 보기

1. 다음과 같이 `StorageProfile` 개체를 통해 캐싱 설정을 확인할 수 있습니다.

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching
    ```

    ```output
    ReadOnly
    ```
   
1. _ReadWrite_인 OS 디스크에 대한 기본값으로 다시 변경해 보겠습니다.

### <a name="change-the-cache-settings-of-the-os-disk"></a>OS 디스크 캐시 설정 변경

1. 다음과 같이 동일한 `StorageProfile` 개체를 사용하여 캐시 유형에 대한 값을 설정할 수 있습니다.

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
    ```
    
    이 명령은 빠르게 실행되며, 작업을 로컬로 수행하고 있음을 알려줍니다. 이 명령은 `myVM` 개체의 속성만 변경합니다. 다음 스크린샷에서 볼 수 있듯이 `Get-AzureRmVM` cmdlet을 사용하여 `$myVM` 변수를 다시 지정하여 새로 고치더라도 VM에서 캐싱 값이 변경되지 않습니다.

1. VM 자체를 변경하려면 다음과 같이 `Update-AzureRmVM`을 호출합니다.

    ```powershell
    Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
    이 호출은 완료하는 데 시간이 걸립니다. 이는 실제 VM을 업데이트하고 Azure에서 변경하기 위해 VM을 다시 시작하기 때문입니다.

    ```output
    RequestId IsSuccessStatusCode StatusCode ReasonPhrase
    --------- ------------------- ---------- ------------
                             True         OK OK
    ```
    
1. `$myVM` 변수를 다시 새로 고치면 개체에 대한 변경 내용이 표시됩니다. 또한 포털에서 디스크를 살펴볼 때도 변경 내용이 표시됩니다. 

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVmName
    $myVM.StorageProfile.OsDisk.Caching
    ```
    
    ```output
    ReadWrite
    ```
    
### <a name="list-data-disk-info"></a>데이터 디스크 정보 나열

1. VM에 있는 데이터 디스크를 확인하려면 다음 명령을 실행합니다.

    ```powershell
    $myVM.StorageProfile.DataDisks
    ```
    
    ```output
    Name            : fotosharesVM-data
    DiskSizeGB      : 1023
    Lun             : 0
    Caching         : ReadOnly
    CreateOption    : Attach
    SourceImage     :
    VirtualHardDisk :
    ```
    
현재 하나의 데이터 디스크만 있습니다. `Lun` 필드가 중요합니다. 고유한 LUN(**논리** **단위** **번호**)입니다. 다른 데이터 디스크를 추가하는 경우 고유한 `Lun` 값을 지정합니다.

### <a name="add-a-new-data-disk-to-our-vm"></a>VM에 새 데이터 디스크 추가

1. 편의상 새 디스크 이름을 저장합니다.

    ```powershell
    $newDiskName = "fotoshareVM-data2"
    ```
    
1. 다음 `Add-AzureRmVMDataDisk` 명령을 실행하여 비어 있는 새 1GB 데이터 디스크를 새로 정의합니다.

    ```powershell
    Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
    ```
    다음과 같은 응답을 받게 됩니다.

    ```output
    ResourceGroupName  : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx
    Id                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxx-xxxxxxx/resourceGroups/<rgn>[sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/fotoshareVM
    VmId               : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx
    Name               : fotoshareVM
    Type               : Microsoft.Compute/virtualMachines
    Location           : eastus
    Tags               : {}
    DiagnosticsProfile : {BootDiagnostics}
    HardwareProfile    : {VmSize}
    NetworkProfile     : {NetworkInterfaces}
    OSProfile          : {ComputerName, AdminUsername, WindowsConfiguration, Secrets}
    ProvisioningState  : Succeeded
    StorageProfile     : {ImageReference, OsDisk, DataDisks}
        ```
    
1. We've given this disk a `Lun` value of `1` because it's not taken. We defined the disk we want to create, so it's time to run `Update-AzureRmVM` to make the actual change:

    ```powershell
    Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
1. 데이터 디스크 정보를 다시 살펴보겠습니다.

    ```powershell
    $myVM.StorageProfile.DataDisks
    ```
    
    ```output
    Name            : fotosharesVM-data
    DiskSizeGB      : 1023
    Lun             : 0
    Caching         : ReadOnly
    CreateOption    : Attach
    SourceImage     :
    VirtualHardDisk :
    
    Name            : fotoshareVM-data2
    DiskSizeGB      : 1
    Lun             : 1
    Caching         : None
    CreateOption    : Empty
    SourceImage     :
    VirtualHardDisk :
    ```

이제 두 개의 디스크가 있습니다. 새 디스크의 `Lun`은 `1`이며 `Caching`의 기본값은 `None`입니다. 해당 값을 변경해 보겠습니다.

### <a name="change-cache-settings-of-new-data-disk"></a>새 데이터 디스크의 캐시 설정 변경

1. 다음과 같이 `Set-AzureRmVMDataDisk` cmdlet을 사용하여 가상 머신 데이터 디스크의 속성을 수정합니다.

    ```powershell
    Set-AzureRmVMDataDisk -VM $myVM -Lun "1" -Caching ReadWrite
    ```
    
1. 언제나 그렇듯이 `Update-AzureRmVM`을 사용하여 변경 내용을 커밋합니다.

    ```powershell
    Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
다음은 이 연습에서 수행한 작업을 보여 주는 포털의 보기입니다. VM에는 이제 두 개의 데이터 디스크가 있고, 모든 **호스트 캐싱** 설정을 조정했습니다. 이 모든 작업은 단지 몇 가지 명령을 사용하여 수행했습니다. 이것이 Azure PowerShell의 능력입니다.

![두 데이터 디스크가 있는 VM 블레이드의 디스크 섹션을 보여주는 Azure Portal의 스크린샷.](../media/disks-final-config-portal2.png)
