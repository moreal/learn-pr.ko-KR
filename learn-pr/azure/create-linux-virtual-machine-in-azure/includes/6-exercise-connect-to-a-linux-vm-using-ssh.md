Linux VM을 배포하여 실행하고 있지만 작업을 수행하도록 구성되어 있지 않았습니다. SSH로 연결하고 Apache를 구성하여 웹 서버가 실행되도록 하겠습니다.

## <a name="connect-to-the-vm-with-ssh"></a>SSH로 VM에 연결

SSH 클라이언트로 Azure VM에 연결하려면 다음 항목이 필요합니다.

- SSH 클라이언트 소프트웨어(대부분의 최신 운영 체제에 포함되어 있음)
- VM의 공용 IP 주소(VM이 사용자 네트워크에 연결하도록 구성된 경우에는 개인 IP 주소)

### <a name="get-the-public-ip-address"></a>공용 IP 주소 가져오기

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에서 이전에 만든 가상 머신의 **개요** 패널이 열려 있는지 확인합니다. 해당 패널을 열어야 하는 경우 **모든 리소스** 아래에서 VM을 찾을 수 있습니다. 개요 패널에는 VM에 대해 많은 정보가 있습니다.

    - VM이 실행 중인지도 확인할 수 있습니다.
    - 중지 또는 다시 시작
    - VM에 연결하기 위한 공용 IP 주소 가져오기
    - CPU, 디스크 및 네트워크의 활동 확인

1. 창 위쪽에서 **연결** 단추를 클릭합니다.

1. **가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인합니다. **SSH** 탭에는 VM에 연결하기 위해 로컬에서 실행해야 하는 명령도 있습니다. 이것을 클립보드에 복사합니다.

## <a name="connect-with-ssh"></a>SSH를 사용하여 연결

1. Azure Cloud Shell에 SSH 탭에서 가져온 명령줄을 붙여 넣습니다. 같이 않으면 같아야 합니다. 그러나 다른 IP 주소를 갖게 (및 아마도 다른 사용자 이름을 사용 하지 않았으면 **jim**!).

    ```bash
    ssh jim@137.117.101.249
    ```

1. 이 명령은 보안 셸 연결을 열고 Linux에 대 한 일반적인 셸 명령 프롬프트에서 배치 됩니다.

1. 몇 가지 Linux 명령을 실행해 보세요.
    - `ls -la /`: 디스크 루트 표시
    - `ps -l`: 실행 중인 모든 프로세스 표시
    - `dmesg`: 모든 커널 메시지 나열
    - `lsblk`: 모든 블록 장치 나열(여기에 드라이브가 표시됨)

드라이브 목록에서 주목해야 할 사항은 _누락된_ 드라이브입니다. **데이터** 드라이브(`sdc`)가 있지만 파일 시스템에 탑재되어 있지 않습니다. Azure가 VHD를 추가했지만 초기화하지 않았습니다.

## <a name="initialize-data-disks"></a>데이터 디스크 초기화

처음부터 새로 만드는 모든 추가 드라이브는 초기화되고 포맷되어야 합니다. 이 수행 하는 프로세스는 실제 디스크와 동일:

1. 먼저 디스크를 식별합니다. 이 작업은 앞에서 수행했습니다. 사용할 수도 있습니다 `dmesg | grep SCSI`, 커널 SCSI 장치에 대 한 모든 메시지를 표시 합니다.

1. 드라이브(`sdc`)가 확인되면 초기화를 수행해야 합니다. `fdisk`를 사용하면 초기화를 수행할 수 있습니다. 사용 하 여 명령을 실행 해야 `sudo` 분할할 디스크를 제공 합니다.

    ```bash
    sudo fdisk /dev/sdc
    ```
1. 새 파티션을 추가하려면 `n` 명령을 사용합니다. 이 예에서는 수도 **p** 기본 파티션 및 기본 값의 나머지입니다. 다음 예제와 유사하게 출력됩니다.   

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

1. `p` 명령을 사용하여 파티션 테이블을 인쇄합니다. 다음과 같이 표시됩니다.

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

1. 이제 `mkfs` 명령을 사용하여 파티션에 파일 시스템을 써야 합니다. 이름을 지정 하는 파일 시스템 형식 및 장치에서 가져온 해야는 `fdisk` 출력:
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

1. 다음으로 탑재 지점으로 사용 하는 디렉터리를 만듭니다. 가 있다고 가정 된 `data` 폴더:

    ```bash
    sudo mkdir /data
    ```
1. 마지막으로 사용 하 여 `mount` 탑재 지점에 디스크를 연결 하려면:

    ```bash
    sudo mount /dev/sdc1 /data
    ```
    사용할 수 있어야 `lsblk` 이제 탑재 된 드라이브를 확인 하려면:
    
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

다시 부팅 후 드라이브가 자동으로 다시 탑재되도록 하려면 `/etc/fstab` 파일에 드라이브를 추가해야 합니다. UUID (universally unique identifier)에 사용 되는 또한 적극 권장 `/etc/fstab` 장치 이름 대신 드라이브를 가리키도록 (같은 `/dev/sdc1`). OS가 부팅하는 동안 디스크 오류를 감지하는 경우 UUID를 사용하면 잘못된 디스크가 지정된 위치에 탑재되는 것을 방지할 수 있습니다. 나머지 데이터 디스크에는 동일한 장치 ID가 할당됩니다. 새 드라이브의 UUID를 찾으려면 `blkid` 유틸리티를 사용합니다.

```bash
sudo -i blkid
```

그러면 다음과 같은 결과가 반환됩니다.

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. 에 대 한 UUID를 복사 합니다 `/dev/sdc1` 연 드라이브는 `/etc/fstab` 텍스트 편집기에서 파일:

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> `/etc/fstab` 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 될 수 있습니다. 확실하지 않은 경우 배포판의 설명서에서 이 파일을 올바르게 편집하는 방법에 대한 자세한 내용을 확인하세요. 또한 프로덕션 시스템에서 작업할 때는 편집하기 전에 파일의 백업을 만드는 것이 좋습니다.

1. **G** 키를 눌러 파일의 마지막 줄로 이동합니다.

1. **I** 키를 눌러 삽입 모드로 전환합니다. 화면 아래쪽에 모드가 표시됩니다.

1. **End** 키를 눌러 줄 맨 끝으로 이동합니다. 화살표 키를 사용할 수도 있습니다. **Enter** 키를 눌러 새 줄로 이동합니다.

1. 편집기에 다음 줄을 입력합니다. 값은 공백이나 탭으로 구분할 수 있습니다. 각 열에 대 한 자세한 내용은 설명서를 확인 합니다.

    ```output
    UUID=<uuid-goes-here>    /data    ext4    defaults,nofail    1    2
    ```
1. **Esc** 키를 누르고 **:w!** 를 입력하여 파일을 작성 하 고 **: q** 편집기를 종료 합니다.

1. 마지막으로, OS가 탑재 지점 새로 고침을 요청 하 여이 항목은 올바른 되도록 확인해 보겠습니다.

    ```bash
    sudo mount -a
    ```

    오류가 반환되면 파일을 편집하여 문제를 찾습니다.

> [!TIP]
> 일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM을 지원합니다. 이 기능은 Azure 디스크에서 사용할 수 있으며 큰 파일을 만든 다음, 삭제하면 비용을 절약할 수 있습니다. 설명서에서 [이 기능을 설정](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure)하는 방법을 확인하세요.

## <a name="install-software-onto-the-vm"></a>VM에 소프트웨어 설치

보시다시피 SSH를 사용하면 Linux VM을 로컬 컴퓨터처럼 사용할 수 있습니다. 다른 Linux 컴퓨터와 마찬가지로이 VM을 관리할 수 있습니다: 소프트웨어를 설치, 구성 역할, 기능 및 기타 일상적인 작업을 조정 합니다. 잠시 소프트웨어 설치에 대해 살펴보겠습니다.

VM에 소프트웨어를 설치하는 옵션은 여러 가지가 있습니다. 먼저, 앞에서 설명한 것처럼 `scp`를 사용하여 머신의 로컬 파일을 VM에 복사할 수 있습니다. 이렇게 하면 데이터 또는 실행 하려면 사용자 지정 응용 프로그램을 복사할 수 있습니다.

또한 Secure Shell을 통해 소프트웨어를 설치할 수 있습니다. 기본적으로 인터넷에 연결 된 azure machines 있습니다. 표준 명령을 사용하여 표준 리포지토리에서 인기 소프트웨어 패키지를 직접 설치할 수 있습니다. 이 방식으로 Apache를 설치해 보겠습니다.

### <a name="install-the-apache-web-server"></a>Apache 웹 서버 설치

Apache는 기본 패키지 관리 도구를 사용 하 여 설치 되므로 Ubuntu의 기본 소프트웨어 리포지토리 내에서 제공 됩니다.

1. 업스트림 최신 변화를 반영 하도록 로컬 패키지 인덱스를 업데이트 하 여 시작 합니다.

    ```bash
    sudo apt-get update
    ```
    
1. 그런 다음 Apache를 설치 합니다.

    ```bash
    sudo apt-get install apache2 -y
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
    > [!NOTE]
    > 인이 같은 명령을 실행 하 여 간단한 항상 일부 소프트웨어를 설치 해야 하는 경우 이것은 수동 프로세스-해야 할 프로세스를 자동화 스크립팅을 사용 하 여 합니다.
    
1. 마지막으로 공용 IP 주소를 통해 기본 페이지를 검색해 볼 수 있습니다. 그러나 웹 서버에서 vm을 실행 하는 경우에 받지 유효한 연결 또는 응답 합니다. 이유를 알 수 있을까요?

웹 서버와 상호 작용할 수를 하나 더 많은 단계를 수행 해야 합니다. 가상 네트워크 내에서 인바운드 요청을 차단-기본 동작입니다. 구성을 통해 변경할 수 있습니다. 다음에 살펴보겠습니다.