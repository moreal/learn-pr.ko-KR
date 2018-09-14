이전 연습에서는 Azure portal을 사용 하 여 다음 작업을 수행 했습니다.

- 디스크 캐시 상태 보기 운영 체제
- OS 디스크의 캐시 설정을 변경 합니다.
- VM에 데이터 디스크 추가
- 새 데이터 디스크에 대 한 캐싱 유형을 변경 합니다.

Azure PowerShell을 사용 하 여 이러한 작업을 연습해 보겠습니다. 이전 연습에서 만든 VM을 사용 하겠습니다. 이 랩에서 작업을 가정합니다.

- VM이 있고 라고 **fotoshareVM**
- VM 이라는 리소스 그룹에 상주  **<rgn>[샌드박스 리소스 그룹 이름]</rgn>**

이름 집합을 다른를 완료 한 경우 방금 사용자를 사용 하 여 이러한 값을 대체 합니다.

마지막 연습에서 VM 디스크의 현재 상태는 다음과 같습니다.

![OS 및 데이터 디스크의 스크린샷, 모두 읽기 전용 캐시를 설정 합니다.](../media/disks-final-config-portal.PNG)

설정 하려면 포털을 사용 하는 것은 **호스트 캐싱을** OS 및 데이터 디스크에 대 한 필드입니다. 다음 단계를 안내 하는 대로이 초기 상태를 염두에 두십시오.

### <a name="set-up-some-variables"></a>일부 변수 설정

먼저 나중에 사용할 수 있도록 몇 가지 리소스 이름을 저장 합니다.

다음 PowerShell 명령을 실행 하려면 오른쪽에 Azure Cloud Shell 터미널을 사용 합니다.

> [!NOTE]
> Cloud Shell 세션을 전환 **PowerShell** 있지 않은 경우 다음이 명령을 시도 하기 전에 합니다.

```powershell
$myRgName = "<rgn>[Sandbox resource group name]</rgn>"
$myVMName = "fotoshareVM"
```

> [!TIP]
> Cloud Shell 세션 시간이 초과 되 면 이러한 변수를 다시 설정 해야 합니다. 따라서 가능 하면 진행이 전체 랩 단일 세션에서.

### <a name="get-info-about-our-vm"></a>VM에 대 한 정보 가져오기

VM의 속성을 다시 가져오려면 다음 명령을 실행 합니다.

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVmName
```

응답을 저장 하는 `$myVM` 변수입니다. 수만 여기에서 지정한 속성을 표시 하려면 다음 명령을 실행 합니다.

```powershell
$myVM | select-object -property ResourceGroupName, Name, Type, Location
```

다음 스크린샷에서 볼 수 있듯이,이 VM은 실제로 살펴볼 VM. 따라서 살펴보겠습니다.

![Azure PowerShell 콘솔을 마지막 4 명령의 결과 보여 주는 스크린샷.](../media/6-ps-commands-1.PNG)

### <a name="view-os-disk-cache-status"></a>디스크 캐시 상태 보기 운영 체제

캐싱 설정을 통해 확인할 수 있습니다는 `StorageProfile` 개체를 다음과 같이 합니다.

```powershell
$myVM.StorageProfile.OsDisk.Caching
```

이 예제에서는 현재 값이 `None`합니다. OS 디스크에 대 한 기본값으로 다시 변경해 보겠습니다.

![캐싱 값이 "none" OS 디스크를 보여 주는 Azure PowerShell 콘솔의 스크린샷.](../media/6-ps-oscaching-none.PNG)

### <a name="change-the-cache-settings-of-the-os-disk"></a>OS 디스크의 캐시 설정을 변경 합니다.

동일한를 사용 하 여 캐시 유형에 대 한 값을 설정할 수 있습니다 `StorageProfile` 개체를 다음과 같이 합니다.

```powershell
$myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
```

이 명령은 알려 주어 야 무언가 로컬로 수행 하는 신속 하 고 실행 합니다. 명령에만 속성을 변경 합니다 `myVM` 개체입니다. 다음 스크린 샷에 표시를 새로 고치는 경우로 `$myVM` 변수에 캐싱 값 않습니다 변경한 VM에서:

![Azure PowerShell 콘솔은 "myVM" 개체를 새로 고칠 것을 보여 주는 스크린샷 VM을 실제로 업데이트 되지 않는 것 때문에 "none" 캐시를 다시 설정 합니다.](../media/6-ps-commands-2.PNG)

VM 자체에 변경을 호출 `Update-AzureRmVM`, 다음과 같습니다.

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

이 호출은 완료 하는 데는 알 수 있습니다. 실제 VM을 업데이트 하 고 되었다가 Azure VM이 변경 때문입니다.

![캐싱 값이 "none" OS 디스크를 보여 주는 Azure PowerShell 콘솔의 스크린샷.](../media/6-ps-oscaching-rw.PNG)

새로 고치는 경우는 `$myVM` 변수를 다시 표시 변경 개체입니다. 포털에서 디스크를 볼 수도 표시 됩니다 변경 있습니다. 에 대해 알아 보며는 새 데이터 디스크를 만들고 있습니다.

### <a name="list-data-disk-info"></a>목록 데이터 디스크 정보

VM에 대 한 어떤 데이터 디스크를 확인 하려면 다음 명령을 실행 합니다.

```powershell
$myVM.StorageProfile.DataDisks
```

현재 데이터 디스크를 하나만 있습니다. `Lun` 필드는 것이 중요 합니다. 고유 **L**논리 **U**nit **N**수 (). 다른 데이터 디스크를 추가할 때 제공 고유한 `Lun` 값입니다.

### <a name="add-a-new-data-disk-to-our-vm"></a>새 데이터 디스크를 VM에 추가

편의 위해이 새 디스크 이름을 저장 합니다.

```powershell
$newDiskName = "fotoshareVM-data2"
```

다음 실행 `Add-AzureRmVMDataDisk` 새 디스크를 정의 하는 명령:

```powershell
Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
```

이 디스크에 지정한 것을 `Lun` 의 값 `1` 때문이 작성 되지 않습니다. 실행 시간 이므로 만들려면 원하는 디스크를 정의한 `Update-AzureRmVM` 실제 변경 작업을 수행 합니다.

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

살펴보겠습니다 우리의 데이터 디스크 정보 다시 합니다.

```powershell
$myVM.StorageProfile.DataDisks
```

![두 개의 데이터 디스크를 보여 주는 Azure PowerShell 콘솔의 스크린샷.](../media/2-data-disks-part1.png)

이제 두 개의 디스크가 있습니다. 새 디스크에는 `Lun` 의 `1` 에 대 한 기본값 `Caching` 는 `None`합니다. 해당 값을 변경해 보겠습니다.

### <a name="change-cache-settings-of-new-data-disk"></a>새 데이터 디스크의 캐시 설정 변경

사용 하 여 가상 머신 데이터 디스크의 속성 수정 된 `Set-AzureRmVMDataDisk` 다음과 같은 cmdlet:

```powershell
Set-AzureRmVMDataDisk -VM $myVM -Lun "1" -Caching ReadWrite
```

항상 사용 하 여 변경 내용을 커밋 `Update-AzureRmVM`:

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

이 연습에서 완료 한에서는 새로운 포털에서 보기는 다음과 같습니다. 이제는 VM이 두 개의 데이터 디스크 및 모든 것이 조정한 **호스트 캐싱을** 설정 합니다. 몇 가지 명령을 사용 하 여 모든 했습니다. Azure PowerShell의 기능입니다.

![두 개의 데이터 디스크를 사용 하 여이 VM 블레이드의 디스크 섹션을 보여 주는 Azure portal의 스크린샷.](../media/disks-final-config-portal2.png)
