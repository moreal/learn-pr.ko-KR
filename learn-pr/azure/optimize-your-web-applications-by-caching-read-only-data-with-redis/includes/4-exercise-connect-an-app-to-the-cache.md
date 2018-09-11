이 연습에서는 Azure Redis Cache 인스턴스를 만들어 일반적으로 사용되는 값을 저장하고 반환합니다.

## <a name="create-a-cache"></a>캐시 만들기

1. Azure Portal에 로그인합니다. 그런 다음, **리소스 만들기**, **데이터베이스**, **Redis Cache**를 차례로 클릭합니다.

    다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여 줍니다.

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조되어 있는 Azure Portal 데이터베이스 옵션을 보여 주는 스크린샷입니다.](../media/4-create-a-cache-1.png)

## <a name="configure-your-cache"></a>캐시 구성

1. **DNS 이름:** **ContosoSportsApp1028**과 같이 전역적으로 고유한 이름을 만듭니다.
1. **구독:** 구독을 선택합니다.
1. **리소스 그룹:** 새 리소스 그룹을 만들고 이름을 지정합니다.
1. **위치:** 대부분의 고객이 뉴욕 지역에 있기 때문에 **미국 동부**를 선택해야 합니다.
1. **가격 책정 계층:** **기본 C0**을 선택합니다.
1. **만들기**를 클릭합니다.

    다음 스크린샷은 새 Redis Cache 리소스를 만드는 데 사용되는 대표적인 구성을 보여 줍니다.

    ![구성 DNS 이름, 구독, 새 리소스 그룹, 위치, 가격 책정 계층 예제가 채워져 있는, 새 Redis Cache 리소스를 만드는 경우의 Azure Portal 블레이드를 보여 주는 스크린샷입니다.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> 계속하기 전에 캐시가 배포될 때까지 기다려야 합니다. 이 프로세스는 시간이 약간 걸릴 수 있습니다.

## <a name="retrieve-the-access-keys-and-host-name"></a>액세스 키 및 호스트 이름 검색

1. Azure Portal에서 캐시를 찾아 **설정** > **액세스 키**를 선택합니다. **기본 연결 문자열(StackExchange.Redis)** 을 기록합니다.

    이 키는 사용 중인 StackExchange.Redis 패키지에 대한 응용 프로그램 설정 내에서 사용할 전체 연결 문자열에 기본 키와 호스트 이름을 포함하고 있습니다.

1. 컴퓨터에서 메모장이나 다른 텍스트 편집기를 시작합니다.
1. 다음 콘텐츠를 추가합니다.

    `<connection-string>`을 위에 있는 캐시의 기본 연결 문자열로 바꿉니다.

    ```xml
    <appSettings>
        <add key="CacheConnection" value="<connection-string>"/>
    </appSettings>
    ```

1. 샘플 응용 프로그램의 소스 코드에 포함되지 않는 위치에 파일을 저장합니다. 이 자습서에서는 파일을 `C:\AppSecrets\CacheSecrets.config`로 저장합니다.

## <a name="create-a-console-app"></a>콘솔 앱 만들기

1. Visual Studio를 시작하고 **파일** > **새로 만들기** > **프로젝트...** 메뉴 항목을 클릭합니다.
1. **Visual C#** > **Windows 데스크톱** > **콘솔 앱** 템플릿을 선택합니다.
1. 앱에 이름을 지정하고 **확인**을 클릭하여 새 콘솔 응용 프로그램을 만듭니다.

## <a name="configure-the-cache-client"></a>캐시 클라이언트 구성

이 섹션에서는 .NET용 **StackExchange.Redis** 클라이언트를 사용하도록 콘솔 응용 프로그램을 구성합니다.

1. Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 가리킨 후 **패키지 관리자 콘솔**을 클릭하고 패키지 관리자 콘솔 창에서 다음 명령을 실행합니다.

    ```powershell
    Install-Package StackExchange.Redis
    ```

설치가 완료되면 StackExchange.Redis 캐시 클라이언트를 프로젝트에 사용할 수 있습니다.

## <a name="connect-to-the-cache"></a>캐시에 연결

1. Visual Studio의 **솔루션 탐색기**에서 **App.config** 파일을 열고 **CacheSecrets.config** 파일을 참조하는 **appSettings** 파일 특성을 포함하도록 업데이트합니다.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.1" />
        </startup>

        <appSettings file="C:\AppSecrets\CacheSecrets.config"></appSettings>

    </configuration>
    ```

1. 솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가...** 를 클릭합니다. **어셈블리** > **프레임워크** 목록에서 **System.Configuration**을 선택하고 **확인**을 클릭합니다.

1. **Program.cs**에 다음 `using` 문을 추가합니다.

    ```csharp
    using StackExchange.Redis;
    using System.Configuration;
    ```

Azure Redis Cache에 대한 연결은 ConnectionMultiplexer 클래스에서 관리됩니다. 이 클래스는 클라이언트 응용 프로그램 전체에서 공유하고 다시 사용해야 합니다. 각 작업에 대해 새 연결을 만들지 마세요.

소스 코드에 자격 증명을 저장해서는 안 됩니다. 이 샘플을 단순하게 유지하기 위해 외부 비밀 구성 파일만을 사용합니다. 더 나은 방법은 인증서로 Azure Key Vault를 사용하는 것입니다.

1. **Program.cs**에서 콘솔 응용 프로그램의 Program 클래스에 다음 멤버를 추가합니다.

    ```csharp
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

응용 프로그램에서 ConnectionMultiplexer 인스턴스를 공유하는 이 방법은 연결된 인스턴스를 반환하는 정적 속성을 사용합니다. 이 코드에서는 연결된 단일 ConnectionMultiplexer 인스턴스만 초기화하는 스레드로부터 안전한 방법을 제공합니다. **abortConnect**는 false로 설정되며, 이는 Azure Redis Cache에 연결이 설정되지 않은 경우에도 호출이 성공한다는 것을 의미합니다. ConnectionMultiplexer의 한 가지 주요 기능은 네트워크 문제 또는 다른 원인이 해결되면 캐시에 연결이 자동으로 복원된다는 점입니다.

**CacheConnection** appSetting 값은 암호 매개 변수로 Azure Portal에서 캐시 연결 문자열을 참조하는 데 사용됩니다.
