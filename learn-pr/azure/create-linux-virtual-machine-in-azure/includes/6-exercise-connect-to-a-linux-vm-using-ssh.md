Linux VM을 배포하여 실행하고 있지만 작업을 수행하도록 구성되어 있지 않았습니다. VM을 SSH에 연결하고 Apache를 구성해 보겠습니다. 그러면 실행되는 웹 서버가 생성됩니다.

## <a name="connect-to-the-vm-with-ssh"></a>SSH로 VM에 연결

Azure VM을 SSH 클라이언트와 연결하려면 다음 항목이 필요합니다.

- SSH 클라이언트 소프트웨어(대부분의 최신 운영 체제에 포함되어 있음)
- VM의 공용 IP 주소(VM이 사용자 네트워크에 연결하도록 구성된 경우에는 개인 IP 주소)

### <a name="get-the-public-ip-address"></a>공용 IP 주소 가져오기

1. [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에서 이전에 만든 가상 머신의 **개요** 패널이 열려 있는지 확인합니다. 해당 패널을 열어야 하는 경우 **모든 리소스** 아래에서 VM을 찾을 수 있습니다. 요약 패널에는 VM과 관련된 많은 정보가 표시됩니다.

    - VM을 실행 중인지 확인할 수 있습니다.
    - 중지 또는 다시 시작
    - VM에 연결하기 위한 공용 IP 주소 가져오기
    - CPU, 디스크 및 네트워크의 활동 확인

1. 창 위쪽에서 **연결** 단추를 클릭합니다.

1. **가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인합니다. **SSH** 탭에는 VM에 연결하기 위해 로컬로 실행해야 하는 명령도 있습니다. 이것을 클립보드에 복사합니다.

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

1. 드라이브(`sdc`)가 확인되면 초기화를 수행해야 합니다. `fdisk`를 사용하면 초기화를 수행할 수 있습니다. `sudo`를 포함해 명령을 실행하고 파티션을 지정할 디스크를 입력해야 합니다. 다음 명령을 사용하여 새로운 주 파티션을 만들 수 있습니다.

    ```bash
    (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
    ```

1. 이제 `mkfs` 명령을 사용하여 파티션에 파일 시스템을 써야 합니다.

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```

1. 마지막으로, 파일 시스템에 드라이브를 탑재해야 합니다. 여기서는 `data` 폴더가 있다고 가정합니다. 탑재 지점 폴더를 만들고 드라이브를 탑재하겠습니다.

    ```bash
    sudo mkdir /data & sudo mount /dev/sdc1 /data
    ```

    > [!TIP]
    > 디스크를 초기화하고 탑재했습니다. 이 프로세스에 대해 좀 더 자세히 알아보려면 **Azure 가상 머신에서 디스크 추가 및 크기 지정** 모듈을 참조하세요. 이 작업에 대해 자세히 설명되어 있습니다.

## <a name="install-software-onto-the-vm"></a>VM에 소프트웨어 설치

보시다시피 SSH를 사용하면 Linux VM을 로컬 컴퓨터처럼 사용할 수 있습니다. 이 VM을 다른 Linux 컴퓨터처럼 관리하면서 소프트웨어를 설치하고, 역할을 구성하고, 기능 및 기타 일상적인 작업을 조정할 수 있습니다. 잠시 소프트웨어 설치에 대해 살펴보겠습니다.

VM에 소프트웨어를 설치하는 옵션은 여러 가지가 있습니다. 먼저, 앞에서 설명한 것처럼 `scp`를 사용하여 머신의 로컬 파일을 VM에 복사할 수 있습니다. 이렇게 하면 데이터 또는 실행하려는 사용자 지정 응용 프로그램을 복사할 수 있습니다.

Secure Shell을 통해 소프트웨어를 설치할 수도 있습니다. Azure 머신은 기본적으로 인터넷에 연결됩니다. 표준 명령을 사용하여 표준 리포지토리에서 인기 소프트웨어 패키지를 직접 설치할 수 있습니다. 이 방식을 사용하여 Apache를 설치해 보겠습니다.

### <a name="install-the-apache-web-server"></a>Apache 웹 서버 설치

Apache는 Ubuntu의 기본 소프트웨어 리포지토리 내에서 제공되므로 기존 패키지 관리 도구를 사용하여 설치하겠습니다.

1. 먼저 최신 업스트림 변경 내용을 반영하도록 로컬 패키지 인덱스를 업데이트합니다.

    ```bash
    sudo apt-get update
    ```

1. 그런 다음, Apache를 설치합니다.

    ```bash
    sudo apt-get install apache2 -y
    ```

1. 설치는 자동으로 시작됩니다. `systemctl`을 사용하면 상태를 확인할 수 있습니다.

    ```bash
    sudo systemctl status apache2 --no-pager
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
    > 이와 같은 명령을 실행하는 것은 간단한 일이지만 이러한 프로세스는 수동으로 수행해야 하므로 많은 소프트웨어를 항상 설치해야 한다면 스크립트를 작성해 프로세스를 자동화할 수 있습니다.

1. 마지막으로 공용 IP 주소를 통해 기본 페이지를 검색해 볼 수 있습니다. 그러나 VM에서 웹 서버를 실행하는 경우에도 유효한 연결 또는 응답을 얻을 수는 없습니다. 이유를 알고 계세요?

웹 서버와 상호 작용할 수 있도록 하려면 한 단계를 더 수행해야 합니다. 가상 네트워크는 인바운드 요청을 차단하고 있으며, 이는 기본 동작입니다. 이는 구성을 통해 변경할 수 있습니다. 이에 대해서는 다음에 살펴보겠습니다.