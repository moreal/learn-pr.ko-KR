Azure는 VHD 이미지를 Azure Storage 계정의 페이지 Blob으로 저장합니다. 관리 디스크를 사용하는 Azure는 사용자 대신 저장소를 관리합니다. 이는 관리 디스크를 선택하는 가장 좋은 이유 중 하나입니다.

VM을 만들 때 OS 디스크의 크기를 선택합니다. 특정 크기는 선택한 이미지를 기반으로 합니다. Linux에서는 대게 약 30GB이고, Windows에서는 약 127GB입니다.

추가 저장소 공간을 제공하기 위해 데이터 디스크를 추가할 수 있지만 기존 디스크를 확장할 수도 있습니다. 아마도 레거시 응용 프로그램은 드라이브 간에 데이터를 분할할 수 없거나 실제 PC의 드라이브를 Azure로 마이그레이션하고 더 큰 OS 드라이브가 필요할 수 있습니다.

> [!NOTE]
> 디스크 크기를 _큰_ 크기로만 조정할 수 있습니다. 관리 디스크 축소는 현재 지원되지 않습니다.

디스크의 크기를 변경하면 디스크 수준도 변경할 수 있습니다(예: P10에서 P20으로). 이는 성능 업그레이드에 유용할 수 있지만 프리미엄 계층으로 이동할수록 더 많은 비용이 소요됨을 명심하세요.

## <a name="vm-size-vs-disk-size"></a>VM 크기 대 디스크 크기

VM을 만들 때 선택하는 VM 크기에 따라 할당할 수 있는 리소스 수가 결정됩니다. 저장소의 경우 크기는 VM에 추가할 수 있는 디스크 수와 각 디스크의 최대 크기를 제어됩니다. 

이전 단원에서 언급했듯이 일부 VM 크기는 표준 저장소 드라이브만 지원하므로 I/O 성능이 제한됩니다.

VM 크기가 허용하는 것보다 많은 저장소가 필요한 경우 VM 크기를 변경할 수 있습니다. 해당 항목은 **Azure Virtual Machines 소개** 모듈에서 다룹니다.

## <a name="expanding-a-disk-using-the-azure-cli"></a>Azure CLI를 사용하여 디스크 확장

> [!WARNING]
> 디스크 크기 조정 작업을 수행하기 전에 항상 데이터를 백업해야 합니다.

VM 실행 중에 VHD에 대한 작업을 수행할 수 없습니다. 첫 번째 단계는 VM 이름과 리소스 그룹 이름을 제공하는 `az vm deallocate`가 있는 VM을 중지 및 할당 취소하는 것입니다.

_중지_와 달리 VM을 할당 취소하면 VM은 관련 컴퓨팅 리소스를 해제하고 Azure가 가상화된 하드웨어의 구성을 변경할 수 있습니다.

```azurecli
az vm deallocate --resource-group <resource-group-name> --name <vm-name>
```

그런 다음, 디스크 크기를 조정하려면 `az disk update`를 사용하여 디스크 이름, 리소스 그룹 이름 및 새로 요청한 크기를 전달합니다. 관리 디스크를 확장하면 지정된 크기가 가장 가까운 관리 디스크 크기에 매핑됩니다.

```azurecli
az disk update \
    --resource-group <resource-group-name> \
    --name <disk-name> \
    --size-gb 200
```

마지막으로 `az vm start`를 사용하여 VM을 다시 시작합니다.

```azurecli
az vm start --resource-group <resource-group-name> --name <vm-name>
```

## <a name="expanding-a-disk-using-the-azure-portal"></a>Azure Portal을 사용하여 디스크 확장

Azure Portal을 사용하여 디스크를 확장하는 것이 훨씬 쉽습니다.

1. VM의 **개요** 보기에 있는 도구 모음에서 **중지** 단추를 사용하여 VM을 중지합니다.

1. **설정** 섹션에서 **디스크**를 클릭합니다.

1. 크기를 조정할 데이터 디스크를 선택합니다.

    ![강조 표시된 항목을 편집하려는 VHD가 있는 VM의 디스크 섹션을 보여 주는 스크린샷](../media/5-portal-disks.png)

1. 디스크 세부 정보에서 현재 크기보다 _큰_ 크기를 입력합니다. 여기서 프리미엄에서 표준 (또는 그 반대로)으로 변경할 수 있습니다. 이러한 설정은 예측된 IOPS 섹션에 표시된 대로 성능을 조정됩니다.

    ![새 크기 필드가 강조 표시된 VHD 편집 화면을 보여 주는 스크린샷](../media/5-resize-disk.png)

1. **저장**을 클릭하여 변경 내용을 저장합니다.

1. VM을 다시 시작합니다.


### <a name="expanding-the-partition"></a>파티션 확장

새 데이터 디스크를 추가하는 것처럼 확장된 디스크는 파티션과 파일 시스템을 확장할 때까지 사용 가능한 공간을 추가하지 않습니다. 이 작업은 VM에서 사용할 수 있는 OS 도구를 통해 수행해야 합니다. 

Windows에서는 디스크 관리자 도구 또는 `diskpart` 명령줄 도구를 사용합니다.

Linux에서는 `parted` 및 `resize2fs`를 사용합니다.

이러한 명령 중 일부를 사용해 보겠습니다.