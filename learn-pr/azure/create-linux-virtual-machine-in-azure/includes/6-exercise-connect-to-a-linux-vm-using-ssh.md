Linux VM을 배포하여 실행하기는 했지만, 해당 VM은 작업을 수행하도록 구성되지는 않은 상태입니다. VM을 SSH에 연결하고 Apache를 구성해 보겠습니다. 그러면 실행되는 웹 서버가 생성됩니다.

## <a name="connect-to-the-vm-with-ssh"></a>SSH를 사용하여 VM에 연결

Azure VM을 SSH 클라이언트와 연결하려면 다음 항목이 필요합니다.

- SSH 클라이언트 소프트웨어(대다수 최신 운영 체제에 포함되어 있음)
- VM의 공용 IP 주소(VM이 사용자 네트워크에 연결하도록 구성된 경우에는 개인 IP 주소)

### <a name="get-the-public-ip-address"></a>공용 IP 주소 가져오기

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에서 이전에 만든 가상 머신의 **개요** 패널이 열려 있는지 확인합니다. 해당 패널을 열어야 하는 경우 **모든 리소스** 아래에서 VM을 찾을 수 있습니다. 요약 패널에는 VM과 관련된 많은 정보가 표시됩니다.

    - VM이 실행 중인지도 확인할 수 있습니다.
    - VM 중지 또는 다시 시작
    - VM에 연결하기 위한 공용 IP 주소 가져오기
    - CPU, 디스크 및 네트워크의 활동 확인

1. 창 위쪽에서 **연결** 단추를 클릭합니다.

1. **가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인합니다. **SSH** 탭에는 VM에 연결하기 위해 로컬로 실행해야 하는 명령도 있습니다. 이 명령을 클립보드에 복사합니다.

<!-- TODO: This will be necessary if we ever have inline portal integration. 

### Open Azure Cloud Shell

Let's use Cloud Shell in the Azure portal. If you generated the SSH key locally, you need to use your local session since the private key won't be in your storage account:

1. Switch back to the **Dashboard** by clicking the **Dashboard** button in the Azure sidebar.

1. Open Cloud Shell by clicking the **shell** button in the top toolbar.

    ![Screenshot of the Azure portal top navigation bar with the Azure Cloud Shell button highlighted.](../media/6-cloud-shell.png)

1. Select **Bash** as the shell type. PowerShell is also available if you are a Windows administrator.

-->

## <a name="connect-with-ssh"></a>SSH를 사용하여 연결

1. SSH 탭에서 가져온 명령줄을 Azure Cloud Shell에 붙여넣습니다. 해당 명령줄은 다음과 같습니다. 하지만 실제 IP 주소는 다르며, **jim**을 사용하지 않았다면 사용자 이름도 다를 것입니다.

    ```bash
    ssh jim@137.117.101.249
    ```

1. 이 명령은 Secure Shell 연결을 열고 일반적인 Linux용 셸 명령 프롬프트를 표시합니다.

1. 몇 가지 Linux 명령을 실행해 보세요.
    - `ls -la /`: 디스크 루트 표시
    - `ps -l`: 실행 중인 모든 프로세스 표시
    - `dmesg`: 모든 커널 메시지 나열
    - `lsblk`: 모든 블록 장치 나열(여기에 드라이브가 표시됨)

드라이브 목록에서 더 자세히 살펴보아야 할 사항은 _누락_ 드라이브입니다. **데이터** 드라이브(`sdc`)가 있는데 파일 시스템에 탑재되어 있지는 않습니다. Azure에서 VHD를 추가했지만 초기화하지는 않았기 때문입니다.

## <a name="initialize-data-disks"></a>데이터 디스크 초기화

처음부터 작성하는 모든 추가 드라이브는 초기화하고 포맷해야 합니다. 이 과정을 수행하는 프로세스는 실제 디스크용 프로세스와 동일합니다.

1. 먼저 디스크를 식별합니다. 이 작업은 앞에서 수행했습니다. SCSI 장치용 커널의 모든 메시지를 나열하는 `dmesg | grep SCSI`를 사용할 수도 있습니다.

1. 드라이브(`sdc`)가 확인되면 초기화를 수행해야 합니다. `fdisk`를 사용하면 초기화를 수행할 수 있습니다. `sudo`를 포함해 명령을 실행하고 파티션을 지정할 디스크를 입력해야 합니다.

    ```bash
    sudo fdisk /dev/sdc
    ```
1. 새 파티션을 추가하려면 `n` 명령을 사용합니다. 또한 이 예제에서는 주 파티션에 대해 **p**를 선택하고 나머지 기본값을 그대로 적용합니다. 출력은 다음 예제와 같습니다.   

    ```output
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x1f2d0c46.

    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-2145386495, default 2048):
    Last sector, +sectors or +size{K,M,G,T,P} (2048-2145386495, default 2145386495):

    Created a new partition 1 of type 'Linux' and of size 1023 GiB.
    ```

1. `p` 명령을 사용하여 파티션 테이블을 인쇄합니다. 인쇄한 내용은 다음과 같습니다.

    ```output
    Disk /dev/sdc: 1023 GiB, 1098437885952 bytes, 2145386496 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 4096 bytes
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
    Disklabel type: dos
    Disk identifier: 0x1f2d0c46

    Device     Boot Start        End    Sectors  Size Id Type
    /dev/sdc1        2048 2145386495 2145384448 1023G 83 Linux
    ```

1. `w` 명령을 사용하여 변경 내용을 씁니다. 그러면 도구가 종료됩니다.

1. 이제 `mkfs` 명령을 사용하여 파티션에 파일 시스템을 써야 합니다. 이렇게 하려면 `fdisk` 출력에서 가져온 파일 시스템 유형과 장치 이름을 지정해야 합니다.
    - `-t ext4`를 전달하여 _ext4_ 파일 시스템을 만듭니다.
    - 장치 이름은 `/dev/sdc`입니다.

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    이 명령을 완료하는 데 몇 분 정도 걸립니다.

    ```output
    mke2fs 1.44.1 (24-Mar-2018)
    Discarding device blocks: done
    Creating filesystem with 268173056 4k blocks and 67043328 inodes
    Filesystem UUID: e311c905-e0d9-43ab-af63-7f4ee4ef108e
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
            102400000, 214990848

    Allocating group tables: done
    Writing inode tables: done
    Creating journal (262144 blocks): done
    Writing superblocks and filesystem accounting information: done
    ```

1. 다음으로, 탑재 지점으로 사용할 디렉터리를 만듭니다. 여기서는 `data` 폴더가 있다고 가정합니다.

    ```bash
    sudo mkdir /data
    ```
1. 마지막으로 `mount`를 사용하여 탑재 지점에 디스크를 연결합니다.

    ```bash
    sudo mount /dev/sdc1 /data
    ```
    이제 `lsblk`를 사용하여 탑재된 드라이브를 확인할 수 있습니다.
    
    ```output
    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda       8:0    0   30G  0 disk
    ├─sda1    8:1    0 29.9G  0 part /
    ├─sda14   8:14   0    4M  0 part
    └─sda15   8:15   0  106M  0 part /boot/efi
    sdb       8:16   0   16G  0 disk
    └─sdb1    8:17   0   16G  0 part /mnt
    sdc       8:32   0 1023G  0 disk
    └─sdc1    8:33   0 1023G  0 part /data
    sr0      11:0    1  628K  0 rom
    ```

### <a name="mounting-the-drive-automatically"></a>드라이브 자동 탑재

다시 부팅 후 드라이브가 자동으로 다시 탑재되도록 하려면 `/etc/fstab` 파일에 드라이브를 추가해야 합니다. 또한 `/etc/fstab`에 UUID(Universally Unique Identifier)를 사용하여 장치 이름만 사용하는 대신 `/dev/sdc1`과 같이 드라이브를 가리키는 것이 좋습니다. 부팅하는 동안 OS에서 디스크 오류를 검색하는 경우 UUID를 사용하여 지정된 위치에 탑재되어 있는 잘못된 디스크를 회피합니다. 그런 다음 남아 있는 데이터 디스크를 동일한 장치 ID에 할당합니다. 새 드라이브의 UUID를 찾으려면 `blkid` 유틸리티를 사용합니다.

```bash
sudo -i blkid
```

그러면 다음과 같은 결과가 반환됩니다.

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. `/dev/sdc1` 드라이브의 UUID를 복사하고 텍스트 편집기에서 `/etc/fstab` 파일을 엽니다.

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> `/etc/fstab` 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다. 확실하지 않은 경우 배포 설명서에서 이 파일을 제대로 편집하는 방법에 대한 자세한 내용을 확인하세요. 또한 프로덕션 시스템에서 작업할 때는 편집하기 전에 파일의 백업을 만드는 것이 좋습니다.

1. **G** 키를 눌러 파일의 마지막 줄로 이동합니다.

1. **I** 키를 눌러 삽입 모드로 전환합니다. 화면 아래쪽에 모드가 표시됩니다.

1. **End** 키를 눌러 줄 맨 끝으로 이동합니다. 화살표 키를 사용할 수도 있습니다. **Enter** 키를 눌러 새 줄로 이동합니다.

1. 편집기에 다음 줄을 입력합니다. 값은 공백이나 탭으로 구분할 수 있습니다. 각 열에 대한 자세한 내용은 설명서를 확인하세요.

    ```output
    UUID=<uuid-goes-here>    /data    ext4    defaults,nofail    1    2
    ```
1. **ESC** 키를 누른 다음, **:w!** 를 입력하여 파일을 작성하고 **:q**를 입력하여 편집기를 종료합니다.

1. 마지막으로 OS가 탑재 지점을 새로 고치도록 하여 입력 내용이 정확한지 확인해 보겠습니다.

    ```bash
    sudo mount -a
    ```

    오류가 반환되면 파일을 편집하여 문제를 찾습니다.

> [!TIP]
> 일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM을 지원합니다. Azure 디스크에서 제공되는 이 기능을 사용하면 큰 파일을 만들었다가 삭제하는 경우 비용을 절약할 수 있습니다. 설명서에서 [이 기능을 설정](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure)하는 방법을 확인하세요.

## <a name="install-software-onto-the-vm"></a>VM에 소프트웨어 설치

여러 가지 옵션을 통해 VM에 소프트웨어를 설치할 수 있습니다. 먼저, 앞에서 설명한 것처럼 `scp`를 사용하여 머신의 로컬 파일을 VM에 복사할 수 있습니다. 이렇게 하면 데이터 또는 실행하려는 사용자 지정 응용 프로그램을 복사할 수 있습니다.

Secure Shell을 통해 소프트웨어를 설치할 수도 있습니다. Azure 머신은 기본적으로 인터넷에 연결됩니다. 표준 명령을 사용하여 표준 리포지토리에서 인기 소프트웨어 패키지를 직접 설치할 수 있습니다. 이 방식을 사용하여 Apache를 설치해 보겠습니다.

### <a name="install-the-apache-web-server"></a>Apache 웹 서버 설치

Apache는 Ubuntu의 기본 소프트웨어 리포지토리 내에서 제공되므로 기존 패키지 관리 도구를 사용하여 설치하겠습니다.

1. 먼저 최신 업스트림 변경 내용을 반영하도록 로컬 패키지 인덱스를 업데이트합니다.

    ```bash
    sudo apt-get update
    ```
    
1. 그런 다음, Apache를 설치합니다.

    ```bash
    sudo apt-get install apache2
    ```

1. 설치는 자동으로 시작됩니다. `systemctl`을 사용하면 상태를 확인할 수 있습니다.

    ```bash
    sudo systemctl status apache2
    ```

    그러면 다음과 같은 결과가 반환됩니다.

    ```output
    apache2.service - The Apache HTTP Server
       Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
      Drop-In: /lib/systemd/system/apache2.service.d
               └─apache2-systemd.conf
       Active: active (running) since Mon 2018-09-03 21:00:03 UTC; 1min 34s ago
     Main PID: 11156 (apache2)
        Tasks: 55 (limit: 4915)
       CGroup: /system.slice/apache2.service
               ├─11156 /usr/sbin/apache2 -k start
               ├─11158 /usr/sbin/apache2 -k start
               └─11159 /usr/sbin/apache2 -k start

    test-web-eus-vm1 systemd[1]: Starting The Apache HTTP Server...
    test-web-eus-vm1 apachectl[11129]: AH00558: apache2: Could not reliably determine the server's fully qua
    test-web-eus-vm1 systemd[1]: Started The Apache HTTP Server.
    ```

1. 마지막으로 공용 IP 주소를 통해 기본 페이지를 검색해 볼 수 있습니다. 그러면 기본 페이지가 반환되어야 합니다.

    ![새 Linux VM의 IP에서 호스팅되는 Apache 기본 웹 페이지를 보여주는 웹 브라우저의 스크린샷.](../media/6-apache-works.png)

보시다시피 SSH를 사용하면 Linux VM을 로컬 컴퓨터처럼 사용할 수 있습니다. 이 VM을 다른 Linux 컴퓨터처럼 관리하면서 소프트웨어를 설치하고, 역할을 구성하고, 기능 및 기타 일상적인 작업을 조정할 수 있습니다. 하지만 이러한 프로세스는 수동으로 수행해야 하므로 소프트웨어를 많이 설치해야 한다면 스크립트를 작성해 프로세스를 자동화할 수 있습니다.
