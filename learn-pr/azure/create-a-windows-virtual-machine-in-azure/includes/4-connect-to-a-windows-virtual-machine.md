이제 Azure에 Windows VM이 생성되었으므로 다음으로는 트래픽 비디오 처리를 위해 응용 프로그램과 데이터를 해당 VM에 배치하겠습니다. 

하지만 Azure에 대해 사이트 간 VPN을 설정하지 않았다면 로컬 네트워크에서 Azure VM에 액세스할 수 없습니다. Azure 사용을 처음 시작하는 경우에는 사이트 간 VPN이 작동하지 않을 가능성이 높습니다. 그렇다면 Azure VM으로 어떻게 파일을 전송할 수 있을까요? 쉬운 방법 중 하나는 Azure의 원격 데스크톱 연결 기능을 사용하여 새 Azure VM과 로컬 드라이브를 공유하는 것입니다.

새 Windows 가상 머신을 생성했으므로 사용자 지정 소프트웨어를 해당 가상 머신에 설치해야 합니다. 이 경우 두 가지 방법을 사용할 수 있습니다.

- RDP(원격 데스크톱 프로토콜)
- 사용자 지정 스크립트
- 소프트웨어가 미리 설치된 사용자 지정 VM 이미지

그러면 Windows VM에서 사용할 수 있는 가장 간단한 방식인 원격 데스크톱에 대해 알아보겠습니다.

## <a name="what-is-the-remote-desktop-protocol"></a>원격 데스크톱 프로토콜이란 무엇인가요?

RDP(원격 데스크톱)는 Windows 기반 컴퓨터의 UI에 대한 원격 연결을 제공합니다. RDP를 사용하면 물리적 또는 가상 Windows 컴퓨터에 원격으로 로그인하여 마치 콘솔에서 작업하는 것처럼 해당 컴퓨터를 제어할 수 있습니다. RDP 연결을 사용하면 일부 전원 및 하드웨어 관련 기능을 제외하고는 물리적 컴퓨터의 콘솔에서 수행할 수 있는 작업을 대부분 수행할 수 있습니다.

RDP 연결에는 RDP 클라이언트가 필요합니다. Microsoft는 다음 운영 체제에 대해 RDP 클라이언트를 제공합니다.

- Windows(기본 제공)
- MacOS
- iOS
- Android

다음 스크린샷에는 Windows 10의 원격 데스크톱 프로토콜 클라이언트가 표시되어 있습니다.

![원격 데스크톱 프로토콜 클라이언트의 사용자 인터페이스 스크린샷.](../media/4-rdp-client.png)

Ubuntu 배포에서 Windows PC에 연결할 수 있도록 해주는 Remmina 같은 오픈 소스 Linux 클라이언트도 있습니다.

## <a name="connecting-to-an-azure-vm"></a>Azure VM에 연결

조금 전에 살펴본 것처럼 Azure VM은 가상 네트워크에서 통신을 합니다. 또한 공용 IP 주소(선택 사항)가 할당될 수도 있습니다. 공용 IP가 있으면 인터넷을 통해 VM과 통신할 수 있습니다. 온-프레미스 네트워크를 Azure에 연결하는 VPN(가상 사설망)을 설정할 수도 있습니다. 그러면 공용 IP를 표시하지 않고도 VM에 안전하게 연결할 수 있습니다. 이 방식에 대한 내용은 다른 모듈에 포함되어 있으며, 해당 옵션에 대해 살펴보려는 사용자를 위해 전체 설명이 문서로 작성되어 있습니다.

Azure에서 공용 IP 주소를 사용할 때 기억해야 할 한 가지 사항은, 공용 IP는 동적으로 할당되는 경우가 많다는 것입니다. 즉, 시간이 지나면 IP 주소가 변경될 수 있습니다. VM의 경우에는 VM을 다시 시작하면 IP 주소가 변경됩니다. 이름 대신 특정 IP 주소에 직접 연결하고 IP 주소가 변경되지 않도록 하려는 경우 추가 요금을 결제하고 고정 주소를 할당할 수 있습니다.

### <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a>Azure에서 RDP를 사용하여 VM에 연결하는 방법은 무엇인가요?

Azure에서 RDP를 사용하여 VM에 연결하는 작업은 간단한 프로세스입니다. Azure Portal에서 VM 속성으로 이동하여 맨 위에 있는 **연결**을 클릭합니다. 그러면 VM에 할당된 IP 주소가 표시되며, 미리 구성된 **.rdp** 파일을 다운로드하는 옵션이 제공됩니다. Windows는 RDP 클라이언트에서 이 파일을 엽니다. RDP 파일에서 VM의 공용 IP 주소를 통해 연결하도록 선택할 수 있습니다. VPN 또는 ExpressRoute를 통해 연결하는 경우에는 내부 IP 주소를 선택할 수 있습니다. 연결할 포트 번호도 선택할 수 있습니다.

VM의 정적 공용 IP 주소를 사용하는 경우 **.rdp** 파일을 데스크톱에 저장할 수 있습니다. 동적 IP 주소를 사용하는 경우에는 VM이 실행 중인 동안에만 **.rdp** 파일이 유효합니다. VM을 중지했다가 다시 시작하는 경우 다른 **.rdp** 파일을 다운로드해야 합니다.

> [!TIP]
> VM의 공용 IP 주소를 Windows RDP 클라이언트에 입력하고 **연결**을 클릭할 수도 있습니다.

연결하는 경우 일반적으로 두 개의 경고를 받게 됩니다. 해당 경고는 다음과 같습니다.

-**게시자 경고** - 공개적으로 서명되지 않은 **.rdp** 파일 때문에 발생합니다.
- **인증서 경고** - 신뢰할 수 없는 머신 인증서 때문에 발생합니다.

테스트 환경에서는 이러한 경고를 무시할 수 있습니다. 프로덕션 환경에서는 **RDPSIGN.EXE**를 사용하여 **.rdp** 파일에 서명하고 클라이언트의 **신뢰할 수 있는 루트 인증 기관** 저장소에 머신 인증서를 배치할 수 있습니다.

RDP를 사용하여 VM에 연결해 보겠습니다.