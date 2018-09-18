### <a name="connect-to-the-data-science-vm"></a>Data Science VM에 연결

이 단원에서는 이전 연습에서 만든 VM의 Ubuntu 데스크톱에 원격으로 연결합니다. 이를 수행하려면 Linux용 경량 데스크톱 환경인 [Xfce](https://xfce.org/)를 지원하는 클라이언트가 필요합니다. 배경 정보 및 DSVM(Data Science Virtual Machine)에 연결할 수 있는 다양한 방법에 대한 개요를 보려면 [Linux용 Data Science Virtual Machine에 액세스하는 방법](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro#how-to-access-the-data-science-virtual-machine-for-linux)을 참조하세요.

1. 아직 Xfce 클라이언트가 설치되지 않은 경우 이 연습을 계속하기 전에 [X2Go 클라이언트](https://wiki.x2go.org/doku.php/download:start)를 다운로드하고 설치하세요. X2Go는 Windows 및 OS X를 비롯한 다양한 운영 체제에서 작동하는 무료 오픈 소스 Xfce 솔루션입니다. 이 단원의 지침에서는 사용자가 X2Go를 사용하고 있다고 가정하지만 Xfce를 지원하는 다른 클라이언트를 사용할 수도 있습니다.

1. Azure Portal에서 **data-science-rg** 리소스 그룹으로 돌아갑니다. **data-science-vm** 리소스를 클릭하여 포털에서 엽니다.

    ![Data Science VM 열기](../media/2-open-data-science-vm.png)

1. VM에 대해 표시된 IP 주소 위로 마우스를 가져가고, 나타나는 **복사** 단추를 클릭하여 IP 주소를 클립보드로 복사합니다.

    ![VM의 IP 주소 복사](../media/2-copy-ip-address.png)

1. X2Go 클라이언트를 시작하고 클립보드의 IP 주소와 이전 연습에서 지정한 사용자 이름을 사용하여 Data Science VM에 연결합니다. 포트 **22**(SSH 연결에 사용되는 표준 포트)를 통해 연결하고 세션 유형으로 **XFCE**를 지정합니다. **확인** 단추를 클릭하여 기본 설정을 확인합니다.

    ![X2Go를 사용하여 연결](../media/2-new-session-1.png)

1. 오른쪽의 "새 세션" 패널에서 원격 데스크톱에 사용할 해상도를 선택합니다. 그런 다음, 패널 위쪽에서 **새 세션**을 클릭합니다.

    ![새 세션 시작](../media/2-new-session-2.png)

1. 지난 단원에서 지정한 암호를 입력한 다음, **확인** 단추를 클릭합니다. 호스트 키를 신뢰할 것인지 묻는 메시지가 표시되면 **예**로 응답합니다. 또한 SSH 디먼을 시작할 수 없음을 알려주는 오류 메시지도 무시합니다.

    ![VM에 로그인](../media/2-new-session-3.png)

1. 원격 데스크톱이 표시될 때까지 기다리고 아래와 유사한지 확인합니다.

    > 데스크톱의 텍스트와 아이콘이 너무 크면 세션을 종료합니다. “새 세션” 패널의 오른쪽 아래에 있는 아이콘을 클릭하고 메뉴에서 **세션 기본 설정...** 을 선택합니다. “새 세션” 대화 상자의 “입/출력” 탭으로 이동한 후 디스플레이 DPI를 조정하고 새 세션을 시작합니다. 96 DPI로 시작하고 필요에 따라 조정합니다.

    ![연결되었습니다.](../media/2-ubuntu-desktop.png)

이제 연결되었으므로 잠시 데스크톱의 바로 가기를 탐색합니다. [Jupyter](http://jupyter.org/), [R Studio](https://www.rstudio.com/) 및 [Microsoft Azure Storage 탐색기](https://azure.microsoft.com/features/storage-explorer/)를 포함하여 VM에 미리 설치된 다양한 데이터 과학 도구에 대한 바로 가기가 제공됩니다.