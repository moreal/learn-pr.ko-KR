이 연습에서는 Microsoft Azure에서 Virtual Network를 만듭니다. 그런 다음, 두 개의 가상 머신을 만들고 가상 네트워크를 사용하여 가상 머신을 서로 또는 인터넷에 연결합니다.

이 연습을 시작하기 전에 평가판 구독 자격 증명을 사용하여 [Azure Cloud Shell](https://shell.azure.com)에 로그인해야 합니다. Azure Cloud Shell을 사용하여 리소스 그룹, 가상 네트워크 및 가상 머신을 만듭니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

1. **Azure Cloud Shell 시작** 창에서 **PowerShell(Linux)** 을 클릭합니다.

1. **탑재된 저장소가 없음** 화면에서 **저장소 만들기**를 클릭합니다.

1. PS Azure:\> 프롬프트에서 다음 코드를 입력하고, Enter 키를 누릅니다.

```PowerShell
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-network"></a>Virtual Network 만들기

1. 가상 네트워크를 만들려면 다음 명령을 입력하고 Enter 키를 누릅니다.

```PowerShell
az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default
```

## <a name="create-two-virtual-machines"></a>두 개의 가상 머신 만들기

1. 첫 번째 가상 머신을 만들려면 포트 3389(원격 데스크톱)를 통해 액세스할 수 있는 공용 IP 주소를 사용하여 Windows VM을 만드는 다음 명령을 실행합니다.

    ``` PowerShell
    az vm create --name dataProcessingStage1 --resource-group MyResourceGroup --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. 프롬프트에서 암호의 값을 입력합니다.

1. 다음 명령을 실행하여 공용 IP 주소 없이 Windows VM을 만듭니다.

    ```PowerShell
    az vm create -n dataProcessingStage2 -g MyResourceGroup --public-ip-address '' --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. 작업이 완료되면 두 번째 명령의 출력이 publicIpAddress의 값을 반환합니다. 

## <a name="connect-to-dataprocessingstage1-using-remote-desktop"></a>원격 데스크톱을 사용하여 dataProcessingStage1에 연결

1. 클라이언트 컴퓨터에서 Windows 로고 키를 누르고 RDP를 입력합니다.

1. **원격 데스크톱 연결** 앱을 선택했는지 확인한 다음, Enter 키를 누릅니다.

1. **원격 데스크톱 연결** 대화 상자의 **컴퓨터** 필드에 dataProcessingStage1PublicIPAddress 값을 입력한 다음, **연결**을 클릭합니다.

1. **이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.

1. **Windows 보안** 대화 상자에 dataProcessingStage1을 만들 때 사용한 사용자 이름 및 암호를 입력합니다.

1. **원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다.

1. Azure에서 원격 컴퓨터에 로그인합니다.

1. **네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.

1. 서버 관리자를 닫습니다.

1. 원격 세션에서 Windows 로고 키를 마우스 오른쪽 단추로 클릭하고, **명령 프롬프트**를 클릭합니다.

1. 명령 프롬프트 창에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. 원격 컴퓨터에서 응답이 없어야 합니다. 기본적으로 Windows 방화벽이 ICMP 응답을 차단하기 때문입니다.

## <a name="connect-to-dataprocessingstage2-using-remote-desktop"></a>원격 데스크톱을 사용하여 dataProcessingStage2에 연결

1. 클라이언트 컴퓨터에서 Windows 로고 키를 누르고 **RDP**를 입력합니다. **원격 데스크톱 연결** 앱을 선택하고, Enter 키를 누릅니다.

1. **컴퓨터** 필드에 dataProcessingStage2PublicIPAddress 값을 입력한 다음, **연결**을 클릭합니다.

1. **이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.

1. **Windows 보안** 대화 상자에 dataProcessingStage2를 만들 때 사용한 사용자 이름 및 암호를 입력합니다.

1. **원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다. 이제 Azure에서 원격 컴퓨터에 로그인합니다.

1. **네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.

1. 서버 관리자를 닫습니다.

1. dataProcessingStage2에서 Windows 로고 키를 누른 다음, **방화벽**을 입력하고, Enter 키를 누릅니다. **고급 보안이 포함된 Windows 방화벽** 콘솔이 표시됩니다.

1. 왼쪽 창에서 **인바운드 규칙**을 클릭합니다.

1. 오른쪽 창에서 아래로 스크롤하여 **파일 및 프린터 공유(에코 요청 - ICMPv4-In)** 를 마우스 오른쪽 단추로 클릭한 다음, **규칙 사용**을 클릭합니다.

1. dataProcessingStage1 콘솔로 다시 전환하고, 명령 프롬프트 창에 다음 명령을 입력하고, Enter 키를 누릅니다.

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. dataProcessingStage2는 두 개의 VM 간에 연결을 보여주는 네 개의 회신을 사용하여 응답합니다.

## <a name="summary"></a>요약

성공적으로 vNet을 만들고, 해당 VNet에 연결된 두 개의 VM을 만들고, VM 중 하나에 연결하고, 동일한 vNet 내의 다른 VM에 대한 네트워크 연결을 표시했습니다. Azure vNet을 사용하여 Azure 네트워크 내에서 리소스에 연결할 수 있습니다. 그러나 이러한 리소스는 동일한 리소스 그룹 및 구독 내에 있어야 합니다. 다음으로, 다른 리소스 그룹, 구독 및 지리적 지역에 있는 vNet에 연결할 수 있도록 하는 VPN Gateway를 살펴보겠습니다.
