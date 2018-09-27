> [!TIP]
> VM에 로그인하는 데 필요한 사용자 이름 및 암호는 **리소스** 탭에 위치합니다.

> [!NOTE]
> Mac을 사용 하는 경우 VM을 시작한 후 도구 모음에서 번개 아이콘이나, VM의 잠금을 해제하는 지침 옆에 있는 **리소스** 탭에서 **Ctrl+Alt+Delete** 옵션을 사용해야 할 수 있습니다.


이 모듈에서는 서버리스 백 엔드를 사용하여 플랫폼 간 Xamarin.Forms 앱을 만듭니다. 이 앱은 사용자의 장치에서 사용자 위치를 가져와 전화 번호 목록과 함께 Azure 함수로 보냅니다. 그러면 해당 함수가 타사 서비스(Twilio)에 대한 바인딩을 사용하여 사용자 위치를 제공된 모든 전화 번호에 SMS 메시지로 보냅니다.

이 프로세스는 다음 단계를 포함합니다.

1. 앱은 장치별 위치 API에 대한 추상화로 Xamarin.Essentials를 사용하여 위치를 캡처합니다.

1. 위치 및 전화 번호는 JSON 페이로드로 패키지되어 Azure 함수로 보내집니다.

1. Azure 함수는 JSON 페이로드를 디코딩하고 SMS 메시지를 만듭니다.

1. SMS 메시지는 [Twilio](https://www.twilio.com/?azure-portal=true)를 통해 보내집니다.

다음 일러스트레이션은 이 프로세스의 개요를 보여줍니다.

![문자 메시지를 통해 위치를 공유하는 프로세스의 대략적인 아키텍처를 보여 주는 그림.](../media/1-architecture.png)

## <a name="create-a-twilio-account"></a>Twilio 계정 만들기

Azure 함수에서 SMS 메시지를 보내려면 Twilio 계정이 필요합니다. 체험 계정만 있어도 충분히 시작할 수 있습니다.

1. [twilio.com](https://www.twilio.com?azure-portal=true)으로 이동합니다.

1. 오른쪽 위에 있는 빨간색 **등록** 단추를 클릭합니다.

1. 세부 정보를 입력하고 **시작**을 클릭합니다.

1. 사용자는 전화 번호를 확인해야 합니다. Twilio 체험 계정을 사용하면 확인된 전화 번호로만 메시지를 보내 전화 번호가 스팸에 사용되지 않도록 방지할 수 있습니다. Twilio는 사용자가 전화 확인을 위해 입력해야 하는 확인 코드를 전송합니다.

1. **제품** 탭을 선택하고 **프로그래밍 가능한 SMS**을 클릭한 다음, **계속**을 클릭합니다.

1. 첫 번째 프로젝트 이름(예: “I’m here”)을 지정한 다음, **계속**을 클릭합니다.

1. 팀 동료를 초대하는 단계를 건너뜁니다.

1. Twilio 메시징 대시보드에서 **프로젝트 정보** 패널을 확장합니다.

1. **계정 SID** 및 **인증 토큰** 값은 나중에 필요하므로 기록해 둡니다.

    Twilio 계정을 만들 때 메시지를 보낼 수 있는 전화 번호가 할당됩니다. 이 전화 번호는 Twilio **전화 번호** 대시보드에서 찾을 수 있습니다.

1. Twilio 사이트 왼쪽 메뉴 아래쪽에 있는 줄임표를 선택합니다. 그런 다음, ‘슈퍼 네트워크->전화 번호’를 선택합니다. 고정 아이콘을 사용하여 이 대시보드를 왼쪽 메뉴에 고정할 수 있습니다. Twilio 번호는 *번호 관리->활성 번호* 아래에 있습니다.

    ![Twilio 번호 찾기](../media/7-twilio-find-number.png)

    > [!TIP]
    > 활성 번호가 아직 없는 경우 활성 번호 페이지에서 **시작**을 선택하여 번호를 만드는 프로세스를 시작합니다.

1. 활성 전화 번호를 기록해 둡니다. 이 번호는 나중에 이 모듈에서 사용됩니다.


> [!NOTE]
> 등록하면 SMS 메시지를 보내는 데 사용할 Twilio 전화 번호가 할당됩니다. 일부 국가에서는 이러한 번호를 통해 SMS 메시지를 보낼 수 없습니다. Twilio 설명서는 [제한이 있는 국가](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true)를 나열하고, [국가별 번호 또는 영숫자로 된 보낸 사람 ID](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true)를 사용하여 SMS 메시지를 전송하는 방법을 보여줍니다.

## <a name="launch-visual-studio"></a>Visual Studio 시작

이 모듈에서는 Visual Studio 2017을 사용하여 가상 머신에서 사용할 수 있는 모바일 앱과 Azure Functions 앱을 개발합니다. Xamarin.Forms 앱은 iOS, Android 및 UWP(유니버설 Windows 플랫폼)에서 실행되도록 빌드될 수 있지만 이 모듈에서는 랩 가상 머신 내에서 작동하도록 UWP에만 집중하겠습니다.

VM의 시작 메뉴 또는 바탕 화면 바로 가기에서 Visual Studio 2017을 시작합니다.

## <a name="summary"></a>요약

이 단원에서는 SMS 메시지를 보내는 데 사용할 Twilio 계정을 만들었고 Visual Studio를 시작했습니다. 다음에는 Xamarin.Forms 앱을 만들고 Xamarin.Essentials NuGet 패키지를 추가하는 방법에 대해 알아봅니다.

> [!IMPORTANT]
> 이 단원에서 수집한 Twilio **계정 SID**, **인증 토큰** 및 **활성 전화 번호** 값은 나중에 필요하므로 기록해 둡니다.
