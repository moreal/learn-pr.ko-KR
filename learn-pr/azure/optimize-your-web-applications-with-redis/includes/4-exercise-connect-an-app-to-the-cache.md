<span data-ttu-id="cdb2f-101">이 단원에서는 Azure Redis Cache 인스턴스를 만들어 일반적으로 사용되는 값을 저장하고 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-101">In this unit, you'll create an Azure Redis Cache instance to store and return commonly used values.</span></span>

## <a name="create-a-cache"></a><span data-ttu-id="cdb2f-102">캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="cdb2f-102">Create a cache</span></span>

1. <span data-ttu-id="cdb2f-103">Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-103">Sign in to the Azure portal.</span></span> <span data-ttu-id="cdb2f-104">그런 다음, **리소스 만들기**, **데이터베이스**, **Redis Cache**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-104">Then click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="cdb2f-105">다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조되어 있는 Azure Portal 데이터베이스 옵션을 보여 주는 스크린샷입니다.](../media/4-create-a-cache-1.png)

## <a name="configure-your-cache"></a><span data-ttu-id="cdb2f-107">캐시 구성</span><span class="sxs-lookup"><span data-stu-id="cdb2f-107">Configure your cache</span></span>

1. <span data-ttu-id="cdb2f-108">**DNS 이름:** **ContosoSportsApp1028**과 같이 전역적으로 고유한 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-108">**DNS Name:** Create a globally unique name such as **ContosoSportsApp1028**.</span></span>

1. <span data-ttu-id="cdb2f-109">**구독:** 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-109">**Subscription:** Select your subscription.</span></span>

1. <span data-ttu-id="cdb2f-110">**리소스 그룹:** 새 리소스 그룹을 만들고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-110">**Resource group:** Create a new resource group and give it a name.</span></span>

1. <span data-ttu-id="cdb2f-111">**위치:** 대부분의 고객이 뉴욕 지역에 있기 때문에 **미국 동부**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-111">**Location:** Because most of your customers are in the New York area, you should select **East US**.</span></span>

1. <span data-ttu-id="cdb2f-112">**가격 책정 계층:** **기본 C0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-112">**Pricing tier:** Select **Basic C0**.</span></span>

1. <span data-ttu-id="cdb2f-113">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-113">Click **Create**.</span></span>

    <span data-ttu-id="cdb2f-114">다음 스크린샷은 새 Redis Cache 리소스를 만드는 데 사용되는 대표적인 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-114">The following screenshot shows a representative configuration used to create a new Redis Cache resource.</span></span>

    ![구성 DNS 이름, 구독, 새 리소스 그룹, 위치, 가격 책정 계층 예제가 채워져 있는, 새 Redis Cache 리소스를 만드는 경우의 Azure Portal 블레이드를 보여 주는 스크린샷입니다.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> <span data-ttu-id="cdb2f-116">계속하기 전에 캐시가 배포될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-116">You will have to wait until the cache is deployed before continuing.</span></span> <span data-ttu-id="cdb2f-117">이 프로세스는 시간이 약간 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-117">This process might take some time.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="cdb2f-118">액세스 키 및 호스트 이름 검색</span><span class="sxs-lookup"><span data-stu-id="cdb2f-118">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="cdb2f-119">Azure Portal에서 캐시를 찾아 **설정** > **액세스 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-119">In the Azure portal, browse to your cache and select **Settings** > **Access keys**.</span></span> <span data-ttu-id="cdb2f-120">**기본 연결 문자열(StackExchange.Redis)** 을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-120">Write down the **Primary connection string (StackExchange.Redis)**.</span></span>

    <span data-ttu-id="cdb2f-121">이 키는 사용 중인 StackExchange.Redis 패키지에 대한 응용 프로그램 설정 내에서 사용할 전체 연결 문자열에 기본 키와 호스트 이름을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-121">This key includes your primary key and host name in a complete connection string for use within your application settings for the StackExchange.Redis package we are using.</span></span>

1. <span data-ttu-id="cdb2f-122">컴퓨터에서 메모장이나 다른 텍스트 편집기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-122">Start Notepad or another text editor on your computer.</span></span>

1. <span data-ttu-id="cdb2f-123">다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-123">Add the following contents:</span></span>

    <span data-ttu-id="cdb2f-124">`<connection-string>`을 위에 있는 캐시의 기본 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-124">Replace `<connection-string>` with your cache's primary connection string from above.</span></span>

    ```xml
    <appSettings>
        <add key="CacheConnection" value="<connection-string>"/>
    </appSettings>
    ```

1. <span data-ttu-id="cdb2f-125">샘플 응용 프로그램의 소스 코드에 포함되지 않는 위치에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-125">Save the file in a location where it won't be included within the source code of your sample application.</span></span> <span data-ttu-id="cdb2f-126">이 자습서에서는 파일을 `C:\AppSecrets\CacheSecrets.config`로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-126">For this tutorial, we will save the file as `C:\AppSecrets\CacheSecrets.config`.</span></span>

## <a name="create-a-console-app"></a><span data-ttu-id="cdb2f-127">콘솔 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="cdb2f-127">Create a console app</span></span>

1. <span data-ttu-id="cdb2f-128">Visual Studio를 시작하고 **파일** > **새로 만들기** > **프로젝트...** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-128">Start Visual Studio and click the **File** > **New** > **Project...** menu item.</span></span>

1. <span data-ttu-id="cdb2f-129">**Visual C#** > **Windows 데스크톱** > **콘솔 앱** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-129">Select the **Visual C#** > **Windows Desktop** > **Console App** template.</span></span>

1. <span data-ttu-id="cdb2f-130">앱에 이름을 지정하고 **확인**을 클릭하여 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-130">Give your app a name and click **OK** to create a new console application.</span></span>

## <a name="configure-the-cache-client"></a><span data-ttu-id="cdb2f-131">캐시 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="cdb2f-131">Configure the cache client</span></span>

<span data-ttu-id="cdb2f-132">이 섹션에서는 .NET용 **StackExchange.Redis** 클라이언트를 사용하도록 콘솔 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-132">In this section, you will configure the console application to use the **StackExchange.Redis** client for .NET.</span></span>

1. <span data-ttu-id="cdb2f-133">Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 가리킨 후 **패키지 관리자 콘솔**을 클릭하고 패키지 관리자 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-133">In Visual Studio, click **Tools**, point to **NuGet Package Manager**, click **Package Manager Console**, and run the following command from the Package Manager Console window:</span></span>

    ```powershell
    Install-Package StackExchange.Redis
    ```

<span data-ttu-id="cdb2f-134">설치가 완료되면 StackExchange.Redis 캐시 클라이언트를 프로젝트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-134">Once the installation is completed, the StackExchange.Redis cache client is available to use with your project.</span></span>

## <a name="connect-to-the-cache"></a><span data-ttu-id="cdb2f-135">캐시에 연결</span><span class="sxs-lookup"><span data-stu-id="cdb2f-135">Connect to the cache</span></span>

1. <span data-ttu-id="cdb2f-136">Visual Studio의 **솔루션 탐색기**에서 **App.config** 파일을 열고 **CacheSecrets.config** 파일을 참조하는 **appSettings** 파일 특성을 포함하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-136">In Visual Studio, open the **App.config** file within the **Solution Explorer** and update it to include an **appSettings** file attribute that references the **CacheSecrets.config** file.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.1" />
        </startup>

        <appSettings file="C:\AppSecrets\CacheSecrets.config"></appSettings>

    </configuration>
    ```

1. <span data-ttu-id="cdb2f-137">솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가...** 를 클릭합니다. **어셈블리** > **프레임워크** 목록에서 **System.Configuration**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-137">In Solution Explorer, right-click **References** and click **Add Reference...**. Select **System.Configuration** from the **Assemblies** > **Framework** list and click **OK**.</span></span>

1. <span data-ttu-id="cdb2f-138">**Program.cs**에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-138">Add the following `using` statements to **Program.cs**:</span></span>

    ```csharp
    using StackExchange.Redis;
    using System.Configuration;
    ```

<span data-ttu-id="cdb2f-139">Azure Redis Cache에 대한 연결은 ConnectionMultiplexer 클래스에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-139">The connection to Azure Redis Cache is managed by the ConnectionMultiplexer class.</span></span> <span data-ttu-id="cdb2f-140">이 클래스는 클라이언트 응용 프로그램 전체에서 공유하고 다시 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-140">This class should be shared and reused throughout your client application.</span></span> <span data-ttu-id="cdb2f-141">각 작업에 대해 새 연결을 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-141">Do not create a new connection for each operation.</span></span>

<span data-ttu-id="cdb2f-142">소스 코드에 자격 증명을 저장해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-142">Never store credentials in source code.</span></span> <span data-ttu-id="cdb2f-143">이 샘플을 단순하게 유지하기 위해 외부 비밀 구성 파일만을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-143">To keep this sample simple, we're only using an external secrets config file.</span></span> <span data-ttu-id="cdb2f-144">더 나은 방법은 인증서로 Azure Key Vault를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-144">A better approach would be to use Azure Key Vault with certificates.</span></span>

1. <span data-ttu-id="cdb2f-145">**Program.cs**에서 콘솔 응용 프로그램의 Program 클래스에 다음 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-145">In **Program.cs**, add the following members to the Program class of your console application:</span></span>

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

<span data-ttu-id="cdb2f-146">응용 프로그램에서 ConnectionMultiplexer 인스턴스를 공유하는 이 방법은 연결된 인스턴스를 반환하는 정적 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-146">This approach to sharing a ConnectionMultiplexer instance in your application uses a static property that returns a connected instance.</span></span> <span data-ttu-id="cdb2f-147">이 코드에서는 연결된 단일 ConnectionMultiplexer 인스턴스만 초기화하는 스레드로부터 안전한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-147">The code provides a thread-safe way to initialize only a single connected ConnectionMultiplexer instance.</span></span> <span data-ttu-id="cdb2f-148">**abortConnect**는 false로 설정되며, 이는 Azure Redis Cache에 연결이 설정되지 않은 경우에도 호출이 성공한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-148">**abortConnect** is set to false, which means that the call succeeds even if a connection to Azure Redis Cache is not established.</span></span> <span data-ttu-id="cdb2f-149">ConnectionMultiplexer의 한 가지 주요 기능은 네트워크 문제 또는 다른 원인이 해결되면 캐시에 연결이 자동으로 복원된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-149">One key feature of ConnectionMultiplexer is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

<span data-ttu-id="cdb2f-150">**CacheConnection** appSetting 값은 암호 매개 변수로 Azure Portal에서 캐시 연결 문자열을 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdb2f-150">The value of the **CacheConnection** appSetting value is used to reference the cache connection string from the Azure portal as the password parameter.</span></span>
