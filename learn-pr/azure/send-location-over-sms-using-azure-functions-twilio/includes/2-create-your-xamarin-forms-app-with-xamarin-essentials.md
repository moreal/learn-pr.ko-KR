빌드 중인 응용 프로그램은 Azure 함수와 통신하여 사용자 위치를 공유하는 플랫폼 간 모바일 앱입니다. 이 단원에서는 Visual Studio를 사용하여 빈 모바일 앱을 만들고 사용자의 위치를 가져오는 데 사용되는 API가 있는 NuGet 패키지를 설치합니다.

## <a name="create-the-xamarinforms-project"></a>Xamarin.Forms 프로젝트 만들기

1. Visual Studio에서 ‘파일->새로 만들기->프로젝트...’를 차례로 선택합니다.

1. 왼쪽 트리에서 ‘Visual C#->플랫폼 간’을 선택하고 가운데 패널에서 ‘모바일 앱(Xamarin.Forms)’을 선택합니다.

1. 솔루션 이름을 “ImHere”로 지정합니다.

1. 솔루션에 적합한 위치를 선택합니다.

1. **확인**을 클릭합니다.

    ![새 솔루션 대화 상자](../media/2-new-solution-dialog.png)

1. **새 플랫폼 간 앱** 대화 상자에서 ‘빈 앱’ 템플릿을 선택합니다.

1. 이 모듈에서는 UWP 앱을 빌드하므로 iOS 및 Android는 선택을 취소하고 UWP는 선택된 상태로 둡니다.

1. *코드 공유 전략*에 **.NET Standard**를 선택합니다.

1. **확인**을 클릭합니다.

    ![새 솔루션 구성 대화 상자](../media/2-configure-solution-dialog.png)

Visual Studio에서는 두 개의 프로젝트, `ImHere.UWP`라는 UWP 앱과 .NET Standard 라이브러리 `ImHere`를 만듭니다. Xamarin.Forms 앱은 하나 이상의 플랫폼별 앱 프로젝트와 하나 이상의 .NET Standard 라이브러리 두 부분으로 구성되어 있습니다. 플랫폼별 앱 프로젝트에는 관련 플랫폼에서 앱을 실행하는 데 필요한 플랫폼별 코드가 포함되어 있습니다. 그러면 이러한 프로젝트에서 플랫폼 간 .NET Standard 라이브러리에 정의된 Xamarin.Forms 앱을 시작합니다. 앱은 플랫폼 간 코드로 빌드하고 만들어진 모든 사용자 인터페이스는 런타임 시 관련 플랫폼별 UI 구성 요소로 변환됩니다.

## <a name="adding-xamarinessentials"></a>Xamarin.Essentials 추가

UWP, Android 및 iOS 플랫폼은 운영 체제와 하드웨어를 활용하는 여러 유사한 기능을 제공합니다. 이러한 유사성에도 불구하고 API는 서로 매우 다릅니다. 플랫폼 간 코드에서 이러한 API를 사용하려면 .NET Standard 라이브러리에 노출하는 앱 프로젝트에 플랫폼별 코드를 작성해야 합니다. [Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true)는 이러한 API 중 다수에 대한 플랫폼 간 추상화를 지원하는 NuGet 패키지이므로 플랫폼별 코드를 작성할 필요가 없습니다. 여기에는 앱에서 사용자의 위치를 가져오는 데 사용할 지리적 위치 API가 포함됩니다.

1. Visual Studio 솔루션 탐색기에서 `ImHere` 솔루션(`ImHere` .NET Standard 프로젝트가 아닌 최상위 수준의 솔루션)을 마우스 오른쪽 단추로 클릭하고 *솔루션에 대한 NuGet 패키지 관리...* 를 선택합니다.

1. **찾아보기** 탭을 선택하고 “Xamarin.Essentials”를 검색합니다. 이 패키지는 현재 시험판 NuGet 패키지로 사용할 수 있으므로 ‘시험판 포함’ 상자를 선택합니다.

    > [!TIP]
    > Xamarin.Essentials NuGet 패키지가 표시되지 않는 경우 *시험판 포함*이 선택되어 있는지 다시 한 번 확인합니다. 

1. **Xamarin.Essentials** NuGet 패키지를 선택합니다.

1. 오른쪽 프로젝트 목록에서 모든 프로젝트를 선택합니다.

1. **설치** 단추를 클릭하여 NuGet 패키지를 설치합니다. 계속하려면 라이선스에 동의해야 합니다.

    ![솔루션의 모든 프로젝트에 Xamarin.Essentials NuGet 패키지 추가](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a>앱 빌드 및 실행

1. 솔루션 탐색기에서 `ImHere.UWP` 프로젝트를 마우스 오른쪽 단추로 클릭하고 ‘시작 프로젝트로 설정’을 선택합니다.

1. 빌드 구성은 **디버그**로, 플랫폼은 **x86**으로 설정하고 장치는 **로컬 머신**에서 실행되도록 설정합니다.

    ![디버그 x86 구성이 로컬 장치에서 실행되도록 설정](../media/2-debug-configuration.png)

1. 앱 디버그를 시작합니다.

    ![실행 중인 앱](../media/2-debuging-app.png)

## <a name="summary"></a>요약

이 단원에서는 새 Xamarin.Forms 플랫폼 간 모바일 앱을 만들고 Xamarin.Essentials NuGet 패키지를 추가했습니다. 다음에는 모바일 앱 UI 및 논리를 빌드하는 방법을 배웁니다.