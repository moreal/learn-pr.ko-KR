Visual Studio는 거의 모든 종류의 소프트웨어 전문 작업을 위한 완전한 기능의 풍부한 IDE(통합 개발 환경)입니다. Visual Studio에는 Microsoft Azure에서 응용 프로그램을 개발하기 위해 특별히 고안된 전체 도구 및 기능 집합이 포함되어 있습니다. Visual Studio에 견고히 통합되었다는 것은 Azure 배포, 디버깅 및 개발 도구가 최고 수준임을 의미합니다. Mac용 Visual Studio도 다르지 않습니다. 이 단원에서는 이러한 두 버전과 해당 버전이 Azure 개발에 사용될 때의 강점을 소개합니다.

## <a name="visual-studio"></a>Visual Studio

Visual Studio는 Windows, Android, iOS, 웹 및 Azure용 응용 프로그램을 개발하는 데 사용되는 완전한 기능의 IDE입니다.

Visual Studio를 설치할 때 몇 가지 워크로드가 사용 가능하다는 것을 알 수 있습니다. 워크로드는 설치할 수 있는 기능 영역을 정의하는 라이브러리 및 구성 요소의 컬렉션입니다. 상호 간의 종속성을 알고 기억하면서 단일 개별 구성 요소를 설치하는 대신, 워크로드를 사용하여 “테마가 지정된” 설치를 수행할 수 있습니다. 이렇게 하면 필요한 모든 구성 요소가 포함됩니다.

Visual Studio의 기본 설치에는 Azure 개발을 위한 도구나 라이브러리가 포함되어 있지 않습니다. 이를 위해 Azure 개발 워크로드를 포함해야 합니다. 여기에는 Azure에서 응용 프로그램 및 환경 생성을 시작하는 데 필요한 Azure SDK, 도구 및 템플릿 프로젝트가 포함됩니다.

Visual Studio를 설치하려면 설치 관리자를 다운로드합니다. 이 설치 관리자는 설치할 워크로드를 묻습니다. 그러면 Azure 개발 워크로드를 지정합니다. 필요한 추가 기능이 있으면 NuGet 또는 Visual Studio 확장을 통해 사용할 수 있습니다.

## <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

Mac용 Visual Studio는 기본적으로 macOS용으로 디자인되어 개발된 IDE입니다. Android 및 iOS, 웹, .NET Core 솔루션에서 모바일 앱용 응용 프로그램을 만들기 위한 최고 수준의 개발자 환경을 제공합니다. 또한 Azure에서 응용 프로그램을 만드는 데에도 아주 적합합니다.

Mac용 Visual Studio의 기본 설치에는 Azure 도구의 컨텍스트 통합이 제공됩니다. 예를 들어, Android용 Xamarin 앱을 빌드하는 경우 연결된 서비스 워크로드가 Azure App Service에서 모바일 백 엔드를 만들기 위한 링크를 제공합니다. Azure 함수를 만들려는 경우 클라우드 범주 아래의 프로젝트 템플릿이 여기에 해당합니다.

기본 설치에 없는 Azure 기능 및 함수에 대한 도구가 필요한 경우 NuGet이 적합합니다. NuGet 패키지 관리자에는 Mac용 Visual Studio의 기능과 도구를 확장하는 다양한 Azure 패키지가 있습니다.

Mac용 Visual Studio를 설치하려면 설치 관리자를 다운로드합니다. 설치 관리자는 시스템을 검사하여 필요하거나 업데이트해야 하는 구성 요소를 확인합니다. 시스템에서 누락된 것으로 확인된 구성 요소 중에서 설치할 구성 요소를 사용자 지정할 수 있습니다. 기본 설치에는 Azure 도구가 포함됩니다. 필요한 추가 기능이 있으면 NuGet 또는 Mac용 Visual Studio 확장을 통해 사용할 수 있습니다.

> [!NOTE]
> 특정 구성 요소의 경우 설치하기 위해 머신에 관리자 자격 증명을 입력하라는 메시지가 표시될 수 있습니다.

## <a name="summary"></a>요약

이 단원에서는 Windows 또는 macOS에 Visual Studio를 설치했습니다.

Windows의 경우 설치 관리자 환경에서 Azure 개발 워크로드를 선택했습니다. 그런 후에 Azure 응용 프로그램을 빌드하고 Azure 리소스를 생성하는 데 필요한 모든 도구가 설치되었습니다. 이제 탐색기 도구 또는 리소스 참조를 통해 구독의 모든 Azure 리소스에 액세스할 수 있습니다.

Mac용 Visual Studio의 기본 설치에는 일부 Azure 도구가 기본적으로 제공되며, NuGet을 통해 여러 추가 기능을 사용할 수 있습니다. 이를 통해 Azure 구독의 리소스 및 서비스에도 액세스할 수 있습니다.
