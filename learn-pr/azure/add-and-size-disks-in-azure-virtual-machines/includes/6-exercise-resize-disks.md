업로드의 크기가 얼마나 커질 수 있는지 과소평가했으며, 업로드 디스크 공간이 부족합니다. 여러분은 공간을 두 배로 늘리고 64GB에서 128GB로 업그레이드 하기로 결정합니다.

## <a name="resize-the-data-disk"></a>데이터 디스크 크기 조정

디스크 크기를 조정하려면 디스크 ID 또는 이름이 필요합니다. 이 예에서는 이름(uploadDataDisk1)을 이미 알고 있습니다. 그러나 이름이 기억 나지 않거나 다른 사용자가 이름을 만든 경우 `az disk list` 명령을 사용하여 디스크 목록을 가져올 수 있습니다.

1. 먼저 리소스 그룹의 관리 디스크 목록을 가져옵니다. 단일 리소스 그룹에서 여러 VM이 있는 경우 다른 디스크가 여기에 포함될 수 있습니다. 이 예에서는 우리가 만든 웹 서버만 있습니다.

    ```azurecli
    az disk list \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

1. 다음으로, `az vm deallocate` 명령을 사용하여 VM을 중지 및 할당 취소합니다. 

    ```azurecli
    az vm deallocate --name support-web-vm01
    ```
1. 이제 `az disk update` 명령을 사용하여 디스크 크기를 조정할 수 있습니다.

    ```azurecli
    az disk update --name uploadDataDisk1 --size-gb 128
    ```
    
1. 크기 조정 작업이 완료되면 VM을 다시 시작합니다.

    ```azurecli
    az vm start --name support-web-vm01
    ```

## <a name="expand-the-disk-partition"></a>디스크 파티션 확장

마지막 단계는 사용 가능한 공간에 대해 OS에 알려주는 것입니다. 앞서 수행한 분할 및 형식 단계와 마찬가지로, 이 프로세스는 온-프레미스 디스크 확장과 동일합니다. 

1. 먼저 VM의 공용 IP 주소를 가져옵니다. VM이 다시 부팅되었기 때문에 IP 주소도 변경되었을 가능성이 있습니다. 이번에는 다른 방법을 시도하고 필터에 `az vm show` 명령을 사용하여 공용 IP 주소를 반환하겠습니다.

    > [!TIP]
    > IP 주소는 기본적으로 동적입니다. Azure DNS가 IP 변경 내용을 자동으로 보정하지만, 고정 IP 주소를 사용하여 동작을 변경할 수도 있습니다.

    ```azurecli
    az vm show --name support-web-vm01 -d --query [publicIps] --o tsv
    ```
    
1. Linux 머신에 SSH로 연결합니다. 올바른 IP 주소를 입력해야 합니다.

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. 디스크를 분리합니다. 디스크는 `/dev/sdc1`였습니다.

    ```bash
    sudo umount /dev/sdc1
    ```

1. 관리자 권한 shell에서 `parted` 명령을 실행합니다.

    ```bash
    sudo parted /dev/sdc
    ```
    
1. `resizepart` 명령을 사용하여 파티션을 확장합니다. 파티션 1 및 새 크기(128GB)을 입력합니다.

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [64GB]? 128GB
    ```

    > [!WARNING]
    > 크기에 주의해야 합니다. 파티션 크기를 조정하여 파티션을 축소할 수 있으며, 이 경우 데이터가 손실됩니다.
    
1. `quit` 명령을 입력하여 도구를 종료합니다.

1. 파티션 도구가 자동으로 드라이브를 _다시 탑재_합니다. 포맷할 수 있도록 드라이브를 분리합니다.

    ```bash
    sudo umount /dev/sdc1
    ```
    
1. `e2fsck` 명령을 사용하여 파티션 일관성을 확인합니다. 이 단계는 반드시 필요하지만, 언제든지 디스크 볼륨의 크기를 변경하는 것이 좋습니다.

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

1. `resize2fs` 명령을 사용하여 파일 시스템 크기를 조정합니다.

    ```bash
    sudo resize2fs /dev/sdc1
    ```

1. 마지막으로, 드라이브를 탑재 지점에 다시 탑재합니다.

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```

OS 디스크 크기를 조정했는지 확인하려면 `df -h`을 사용합니다. 이제 드라이브가 128GB로 표시됩니다.
