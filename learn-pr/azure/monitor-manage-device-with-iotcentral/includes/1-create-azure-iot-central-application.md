 이 자습서에서는 문제 모니터링 및 관리를 위해 원격 커피 머신을 Azure IoT Central에 연결하는 시나리오를 진행합니다. 물 온도와 습도/머신 상태 등의 원격 분석을 모니터링하고, 최적 온도를 설정하고, 보증 상태를 수신하고, 커피 끓이기 시작 등의 명령을 전송할 수 있습니다. 보증 기간이 남아 있는 커피 머신의 물 온도가 특정 임계값을 초과하는 경우 Microsoft Flow에서 원격 기사의 모바일 장치로 모바일 알림을 전송합니다. 마찬가지로, 보증 기간이 만료된 커피 머신의 물 온도가 적정 범위를 벗어나면 추가 작업을 수행할 수 있도록 IoT Central의 이메일이 고객의 유지 관리 부서로 전송됩니다.

이 시나리오를 구현하려면 먼저 SaaS 솔루션인 Azure IoT Central에서 장치 템플릿을 만들어 측정(원격 분석 및 상태), 설정, 속성 및 명령을 정의합니다. 그런 다음 Azure IoT Central에 커피 머신을 연결하고, 물 온도가 최적 범위를 벗어날 때 유지 관리 알림을 보내도록 규칙을 구성합니다.

![커피 머신에서 IoT Central로의 데이터 흐름](../images/1-data-flow.png)

이 자습서에서는 다음 방법을 알아봅니다.
> [!div class="checklist"]
> * Azure IoT Central 사용자 지정 응용 프로그램 템플릿 만들기
> * 장치 템플릿 만들기 및 정의
> * 커피 머신 시뮬레이터에 응용 프로그램 연결
> * 연결 및 데이터 흐름의 유효성 검사
> * 유지 관리 알림을 전송하도록 규칙 구성
 
## <a name="sign-in-to-azure-iot-central"></a>Azure IoT Central 로그인

Azure IoT Central은 대규모 IoT 자산의 연결, 모니터링 및 관리를 도와주는, 완전히 관리되는 SaaS(Software-as-a-Service) 솔루션입니다. 이 모듈에서는 IoT Central에 로그인하여 새 사용자 지정 응용 프로그램을 만듭니다. Azure 계정에 등록할 때 평가판 사용 기간을 30일로 연장하도록 선택할 수 있습니다. Microsoft Flow를 사용하여 모바일 알림을 보낼 때 모듈 5를 완료하려면 30일 평가판이 필수 구성 요소로 필요합니다.

1. Azure IoT Central [응용 프로그램 관리자](https://aka.ms/iotcentral) 페이지로 이동합니다. 

1. Microsoft 계정에 액세스하는 데 사용하는 이메일 주소와 암호를 입력합니다.
![Microsoft 계정 액세스](../images/1-create-app-a.png)

## <a name="create-a-new-custom-application"></a>새 사용자 지정 응용 프로그램 만들기

1. 새 Azure IoT Central 응용 프로그램을 만들려면 **새 응용 프로그램**을 선택합니다. 
![Central 응용 프로그램 만들기](../images/1-create-app-b.png)

1. 새 Azure IoT Central 응용 프로그램을 만들려면:
* 결제 플랜으로 **무료**를 선택합니다.
* 응용 프로그램 템플릿으로 **사용자 지정 응용 프로그램**을 선택합니다.
* **Coffee Maker 01** 같은 친숙한 응용 프로그램 이름을 선택합니다. 
* Azure IoT Central에서 고유한 URL 접두사를 자동으로 생성합니다. **만들기**를 선택합니다.

![Central 응용 프로그램 플랜 선택](../images/1-create-app-c.png)

* 평가판은 필요한 경우 30일로 연장하면 됩니다. 하지만 모바일 알림을 전송하는 작업을 트리거하도록 Microsoft Flow를 통합하는 모듈을 완료하려면 평가판을 반드시 30일로 연장해야 합니다. 평가판을 30일로 연장하려면 사용할 Azure Active Directory 및 Azure 구독을 선택합니다. Azure 구독을 사용하여 Azure 서비스 인스턴스를 만들 수 있습니다. Azure IoT Central은 액세스 권한이 있는 모든 Azure 구독을 자동으로 찾아서 드롭다운에 표시합니다.
        
![평가판 연장](../images/1-create-app-d.png)
    
* Azure 구독이 아직 없는 경우 [Azure 등록 페이지](https://aka.ms/createazuresubscription)에서 만들 수 있습니다. Azure 구독을 만든 후 다시 **응용 프로그램 만들기** 페이지로 돌아갑니다. **Azure 구독** 드롭다운에 새 구독이 표시됩니다.
        
![구독 등록](../images/1-create-app-e.png)

## <a name="summary"></a>요약

이 모듈에서는 Azure IoT 사용자 지정 응용 프로그램을 만들었습니다. Azure 구독 등록도 선택했을 수 있습니다. 다음 모듈에서는 직접 만든 응용 프로그램 프레임워크에서 빌드를 계속 진행합니다. 