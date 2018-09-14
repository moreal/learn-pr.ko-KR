이 연습에서는 Microsoft Azure의 가상 네트워크를 만듭니다. 그런 다음, 두 개의 가상 머신을 만들고 가상 네트워크를 사용하여 가상 머신을 서로 또는 인터넷에 연결합니다.

이 단위를 시작 하기 전에 로그인 해야 합니다 [Azure Cloud Shell](https://shell.azure.com) 평가판 구독 자격 증명을 사용 하 여 합니다. Azure Cloud Shell을 통해 Azure CLI 리소스 그룹, 가상 네트워크 및 가상 컴퓨터를 만들려면 사용 합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

1. 에 **Azure Cloud Shell 시작** 창에서 클릭 **Bash (Linux)** 합니다.

1. **탑재된 저장소가 없음** 화면에서 **저장소 만들기**를 클릭합니다.

1. Azure PowerShell 명령줄 프롬프트에서 다음 코드를 입력 하 고 Enter 키를 누릅니다. 대체는 `<myResourceGroup>` 나중에 만들어진 모든 리소스를 정리 하는 경우 기억 하기 쉽게 설명 하는 이름 사용 하 여 값입니다. 이 랩의 리셋이 이름을 사용 합니다.

    ```azurecli
    az group create --name <myResourceGroup> --location eastus
    ```

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기

1. 가상 네트워크를 만들려면 다음 명령을 입력하고 Enter 키를 누릅니다. 대체는 `<myVirtualNetwork>` 기억 하기 쉽게 설명 하는 이름 사용 하 여 값

    ```azurecli
    az network vnet create --name <myVirtualNetwork> --resource-group <myResourceGroup> --subnet-name default
    ```

## <a name="create-two-virtual-machines"></a>두 개의 가상 머신 만들기

1. 첫 번째 가상 컴퓨터를 만들려면 포트 3389 (원격 데스크톱)를 통해 액세스할 수 있는 공용 IP 주소를 사용 하 여 Windows VM을 만들려면 다음 명령을 실행 합니다. VM 이름을 `dataProcStage1`:

    ```azurecli
    az vm create --name dataProcStage1 --resource-group <myResourceGroup> --admin-username "DataAdmin" --image Win2016Datacenter
    ```

1. 프롬프트에서 암호의 값을 입력합니다. 이 암호를 적어 둡니다 서버에 액세스 하 나중에 필요 해야 합니다.

1. 이제 두 번째 VM을 만들 수 있습니다. 이 VM은 공용 IP 주소가 없습니다. Windows VM을 만들려면 다음 명령을 실행 **없이** 빈 문자열을 사용 하 여 공용 IP 주소입니다. VM 이름을 `dataProcStage2`:

    ```azurecli
    az vm create -n dataProcStage2 -g <myResourceGroup> --public-ip-address "" --admin-username "DataAdmin" --image Win2016Datacenter
    ```

1. 작업이 완료되면 두 번째 명령의 출력이 publicIpAddress의 값을 반환합니다.  

## <a name="connect-to-dataprocstage1-using-remote-desktop"></a>DataProcStage1 연결할 원격 데스크톱을 사용 하 여

1. 클라이언트 컴퓨터에서 Windows 로고 키를 누르고 RDP를 입력합니다.

1. 했는지 **원격 데스크톱 연결** 앱을 선택한 다음 Enter를 누릅니다.

1. 에 **원격 데스크톱 연결** 대화 상자의 **컴퓨터** 필드의 값을 입력 합니다 `dataProcStage1`PublicIPAddress, 고 클릭 **Connect**합니다.
    
    기록 되지 경우 원격 ip를 가져오는 지침

1. **이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.

1. 에 **Windows 보안** 대화 상자에 사용자 이름 및 암호를 만들 때 사용한 입력 `dataProcStage1`합니다. 

    여기에 프로필을 변경 해야 합니다.

1. **원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다.

1. Azure에서 원격 컴퓨터에 로그인합니다.

1. **네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.

1. 서버 관리자를 닫습니다.

1. 원격 세션에서 Windows 키를 마우스 오른쪽 단추로 클릭 하 고 클릭 **명령 프롬프트**합니다.

1. 명령 프롬프트 창에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    ```cmd
    ping dataProcStage2 -4
    ```

1. 응답이 없는 없어야 `dataProcStage2`합니다. 기본적으로 Windows 방화벽에서 ICMP 응답을 방지 하기 때문에 이것이 `dataProcStage2`합니다.

## <a name="connect-to-dataprocstage2-using-remote-desktop"></a>DataProcStage2 연결할 원격 데스크톱을 사용 하 여

Windows 방화벽을 구성한 것 `dataProcStage2` 새 원격 데스크톱 seesion를 사용 하 여 합니다. 그러나에서는 액세스할 수 없습니다. `dataProcStage2` 바탕 화면에서. 기억 `dataProcStage2` 는 공용 IP 주소가 없습니다. 원격 데스크톱을 사용 하면 `dataProcStage1` 연결할 `dataProcStage2`합니다.

1. `dataProcStage1`, Windows 키 및 형식은 키를 누릅니다 **RDP**합니다. **원격 데스크톱 연결** 앱을 선택하고, Enter 키를 누릅니다.

1. 에 **컴퓨터** 필드를 입력 합니다 `dataProcStage2`를 클릭 하 고 **Connect**합니다. 기본 네트워크 구성에 따라`dataProcStage1` 의 주소를 확인할 수 `dataProcStage2` 컴퓨터 이름을 사용 합니다.

1. **이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.

1. 에 **Windows 보안** 대화 상자에 사용자 이름 및 암호를 만들 때 사용한 입력 `dataProcStage2`합니다.

1. **원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다. 이제 Azure에서 원격 컴퓨터에 로그인합니다.

1. **네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.

1. 서버 관리자를 닫습니다.

1. 온 `dataProcStage2`, Windows 키를 형식 키를 누릅니다 **방화벽**, Enter 키를 누릅니다. **고급 보안이 포함된 Windows 방화벽** 콘솔이 표시됩니다.

1. 왼쪽 창에서 **인바운드 규칙**을 클릭합니다.

1. 오른쪽 창에서 아래로 스크롤하여 마우스 오른쪽 단추로 클릭 **파일 및 프린터 공유 (에코 요청-ICMPv4-In)** 를 클릭 하 고 **규칙 사용**합니다.

1. 전환의 `dataProcStage1` 콘솔 및 명령 프롬프트 창에서 다음 명령을 입력 한 다음 Enter 키를 누릅니다.

    ```cmd
    ping dataProcStage2 -4
    ```

1. `dataProcStage2` 두 Vm 간의 연결을 보여 주는 4 개의 응답을 사용 하 여 응답 합니다.

## <a name="summary"></a>요약

해당 가상 네트워크에 연결, Vm 중 하나에 연결 및 동일한 가상 네트워크 내의 다른 VM에 대 한 네트워크 연결을 표시 하는 두 개의 Vm을 만든 가상 네트워크를 만들었습니다. Azure 네트워크 내에서 리소스에 연결할 Azure 가상 네트워크를 사용할 수 있습니다. 그러나 이러한 리소스는 동일한 리소스 그룹 및 구독 내에 있어야 합니다. 다음으로, 다른 리소스 그룹, 구독 및 지리적 지역에서 가상 네트워크에 연결할 수 있도록 하는 VPN gateway를 살펴보겠습니다.
