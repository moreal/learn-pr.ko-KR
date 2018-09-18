<span data-ttu-id="e551c-101">Azure에서 Redis 캐시 인스턴스를 만든 다음, 캐시에 두 개의 데이터 값을 삽입하는 간단한 트랜잭션을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-101">Let's start by creating a Redis cache instance in Azure, then create a simple transaction that inserts two data values into the cache.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="e551c-102">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="e551c-102">Create an Azure Redis Cache</span></span>

<span data-ttu-id="e551c-103">먼저 Azure CLI를 사용하여 Azure Redis Cache를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-103">Let's start by creating an Azure Redis Cache with the Azure CLI.</span></span> <span data-ttu-id="e551c-104">브라우저 창의 오른쪽에서 Cloud Shell을 사용하여 Azure와 상호작용합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-104">Use the Cloud Shell on the right side of the browser window to interact with Azure.</span></span>

<span data-ttu-id="e551c-105">`azure rediscache create` 명령을 사용하여 새 Azure Redis Cache를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-105">We'll use the `azure rediscache create` command to create a new Azure Redis Cache.</span></span> <span data-ttu-id="e551c-106">여러 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-106">It takes several parameters.</span></span> <span data-ttu-id="e551c-107">다음은 가장 일반적인 매개 변수입니다(전체 목록은 설명서 확인).</span><span class="sxs-lookup"><span data-stu-id="e551c-107">Here are the most common (to get a full list, check the documentation).</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="e551c-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e551c-108">Parameter</span></span> | <span data-ttu-id="e551c-109">설명</span><span class="sxs-lookup"><span data-stu-id="e551c-109">Description</span></span> |
> |-----------|-------------|
> | `--name`    | <span data-ttu-id="e551c-110">캐시 이름 - 전역적으로 고유해야 하며 문자, 숫자, 대시로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-110">The name of the cache - this must be globally unique and composed of letters, numbers and dashes.</span></span> |
> | `--resource-group` | <span data-ttu-id="e551c-111">Azure 샌드박스의 일부인 미리 생성된 <rgn>[샌드박스 리소스 그룹 이름]</rgn> 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-111">Use the pre-created Resource Group <rgn>[Sandbox resource group name]</rgn> which is part of the Azure Sandbox.</span></span> |
> | `--location` | <span data-ttu-id="e551c-112">캐시를 배치할 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-112">Specify the location where the cache should be located.</span></span> <span data-ttu-id="e551c-113">일반적으로 데이터 소비자와 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-113">Normally, you will want to choose a location close to the data consumers.</span></span> <span data-ttu-id="e551c-114">이 예에서는 Azure 샌드박스에서 사용할 수 있는 위치로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-114">In this case, you are limited to the locations available in the Azure Sandbox.</span></span> <span data-ttu-id="e551c-115">가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-115">Select the closest one to you.</span></span> |
> | `--size` | <span data-ttu-id="e551c-116">Redis Cache의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-116">Size of the Redis Cache.</span></span> <span data-ttu-id="e551c-117">유효한 값 [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="e551c-117">Valid values are [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
> | `--sku` | <span data-ttu-id="e551c-118">Redis SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-118">Redis SKU.</span></span> <span data-ttu-id="e551c-119">유효한 값은 [기본, 표준, 프리미엄]</span><span class="sxs-lookup"><span data-stu-id="e551c-119">Valid values are [Basic, Standard, Premium]</span></span> |
> | `--enable-non-ssl-port` | <span data-ttu-id="e551c-120">캐시에 대해 비 SSL 포트를 사용하도록 설정하려는 경우 이 플래그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-120">Add this flag if you want to enable the Non SSL Port for your cache.</span></span> |

### <a name="selecting-a-location"></a><span data-ttu-id="e551c-121">위치 선택</span><span class="sxs-lookup"><span data-stu-id="e551c-121">Selecting a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="e551c-122">다음 옵션을 사용하여 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-122">Create a cache using the following options:</span></span>
    - <span data-ttu-id="e551c-123">크기: C0</span><span class="sxs-lookup"><span data-stu-id="e551c-123">Size: C0</span></span>
    - <span data-ttu-id="e551c-124">SKU: 기본</span><span class="sxs-lookup"><span data-stu-id="e551c-124">SKU: Basic</span></span>
    - <span data-ttu-id="e551c-125">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="e551c-125">EnableNonSslPort</span></span>
    
1. <span data-ttu-id="e551c-126">다음 예제 명령줄에서 **[name]** 및 **[location]** 을 유효한 값으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-126">Here's an example command line, make sure to replace the **[name]** and **[location]** with valid values.</span></span>

    ```azurecli
    azure rediscache create \
        --name [name] \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location [location] \
        --size C0 --sku Basic
    ```

1. <span data-ttu-id="e551c-127">캐시가 생성될 때까지 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-127">It will take a few minutes to create the cache.</span></span>

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="e551c-128">.NET Core 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e551c-128">Create a .NET Core Console application</span></span>

<span data-ttu-id="e551c-129">다음으로, Azure Redis Cache에 데이터 값을 삽입하는 데 사용할 .NET Core C# 기반 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-129">Next, create a .NET Core C#-based console application, which will be used to insert data values into our Azure Redis Cache.</span></span>

1. <span data-ttu-id="e551c-130">창 오른쪽의 통합 Cloud Shell을 사용하여 새 .NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-130">Create a new .NET Core application using the integrated Cloud Shell on the right hand side of the window.</span></span> <span data-ttu-id="e551c-131">이름을 "RedisData"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-131">Name it "RedisData".</span></span>

    ```bash
    dotnet new console --name RedisData
    ```
    
1. <span data-ttu-id="e551c-132">앱에 대해 만든 새 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-132">Change into the new directory created for your app.</span></span>

    ```bash
    cd RedisData
    ```
    
1. <span data-ttu-id="e551c-133">프로젝트 파일 하나와 단일 **Program.cs** 소스 파일이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-133">You should find a project file, and a single **Program.cs** source file.</span></span>

1. <span data-ttu-id="e551c-134">응용 프로그램을 빌드하고 실행하면 "Hello, World!"가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-134">Build and run the application - it should output "Hello, World!".</span></span>

    ```bash
    dotnet run
    ```
    
## <a name="add-the-servicestackredis-nuget-package"></a><span data-ttu-id="e551c-135">ServiceStack.Redis NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="e551c-135">Add the ServiceStack.Redis NuGet package</span></span>

<span data-ttu-id="e551c-136">콘솔 응용 프로그램이 생겼으니, **ServiceStack.Redis** NuGet 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-136">Now that we have our console application, we need to add the **ServiceStack.Redis** NuGet package.</span></span> <span data-ttu-id="e551c-137">그러면 Redis Cache에 연결하고 C#에서 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-137">This will allow us to connect to the Redis Cache and issue commands in C#.</span></span>

1. <span data-ttu-id="e551c-138">터미널 셸을 사용하여 NuGet 패키지 **ServiceStack.Redis**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-138">Add the NuGet package **ServiceStack.Redis** using the terminal shell.</span></span>

    ```bash
    dotnet add package ServiceStack.Redis
    ```
    
1. <span data-ttu-id="e551c-139">응용 프로그램을 다시 빌드하고 실행하여 모두 컴파일되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-139">Build and run the application again to make sure it all compiles.</span></span> <span data-ttu-id="e551c-140">여전히 "Hello, World!"가 출력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-140">It should still output "Hello, World!"</span></span>

## <a name="get-your-azure-redis-cache-connection-string"></a><span data-ttu-id="e551c-141">Azure Redis Cache 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="e551c-141">Get your Azure Redis Cache connection string</span></span>

<span data-ttu-id="e551c-142">Azure Redis Cache에 연결하려면 암호 및 URL을 포함하고 있는 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-142">To connect to your Azure Redis Cache, you need a connection string that contains your password and URL.</span></span> <span data-ttu-id="e551c-143">이 연결 문자열은 **ServiceStack.Redis**에 대해 고유하며 `[password]@[host name]:[port]` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-143">This connection string is unique to **ServiceStack.Redis** and is in the form of: `[password]@[host name]:[port]`</span></span>

<span data-ttu-id="e551c-144">Azure Portal 또는 명령줄을 사용하여 이 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-144">You can retrieve this key with the Azure portal, or with the command line.</span></span> <span data-ttu-id="e551c-145">**Redis로 읽기 전용 데이터를 캐시하여 웹 응용 프로그램 최적화**에서 포털을 사용했으니, 여기서는 명령줄을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-145">Let's use the latter here since we used the portal approach in the **Optimize your web applications by caching read-only data with Redis** module.</span></span>

<span data-ttu-id="e551c-146">`azure rediscache list-keys` 명령을 사용하여 액세스 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-146">Use the `azure rediscache list-keys` command to get the access keys.</span></span> <span data-ttu-id="e551c-147">아래와 같이 이름 및 리소스 그룹을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-147">You will need to supply the name and resource group as shown below:</span></span>

```azurecli
azure rediscache list-keys \
    --name [name] \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

<span data-ttu-id="e551c-148">그러면 다음과 같은 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-148">This will return something like</span></span>

```output
Primary Key   : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
Secondary Key : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
```

1. <span data-ttu-id="e551c-149">**기본 키**를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-149">Copy your **Primary** key to the clipboard.</span></span>

1. <span data-ttu-id="e551c-150">캐시를 만들 때 캐시 이름에 `.redis.cache.windows.net` 접미사를 붙여서 지정한 이름이 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-150">The hostname will be the name you gave to the cache when you created it with the suffix `.redis.cache.windows.net`.</span></span>

1. <span data-ttu-id="e551c-151">포트는 **6379**입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-151">The port should be **6379**.</span></span>

1. <span data-ttu-id="e551c-152">이 모든 정보는 콘솔에서 `azure rediscache list` 명령을 사용하여 확인할 수 있습니다. 이 명령은 활성 구독(여기서는 Azure 샌드박스)의 모든 Redis 캐시 인스턴스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-152">You can verify all of that information in the console with the `azure rediscache list` command which will show you all the Redis cache instances in your active subscription (in this case, the Azure Sandbox).</span></span>

## <a name="add-the-connection-string-to-your-app"></a><span data-ttu-id="e551c-153">앱에 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="e551c-153">Add the connection string to your app</span></span>

1. <span data-ttu-id="e551c-154">앱 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-154">Make sure you are in the app folder.</span></span> <span data-ttu-id="e551c-155">`ls` 또는 `dir`을 입력하는 경우 **Program.cs**가 현재 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-155">The **Program.cs** should be in the current folder if you type `ls` or `dir`.</span></span>

1. <span data-ttu-id="e551c-156">앱 폴더에서 `code .`를 입력하여 기본 제공 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-156">Open the built-in editor by typing `code .` in the app folder.</span></span>

1. <span data-ttu-id="e551c-157">**Program.cs** 소스 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-157">Select the **Program.cs** source file.</span></span>

1. <span data-ttu-id="e551c-158">`Program` 클래스에서 다음 필드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-158">Create the following field in the `Program` class.</span></span>

    ```csharp
    static string redisConnectionString = "";
    ```

1. <span data-ttu-id="e551c-159">방금 만든 **redisConnectionString** 필드의 연결 문자열에 붙여넣고 포트 번호로 **6379**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-159">Paste in your connection string in the **redisConnectionString** field you just created and use **6379** as your port number.</span></span> <span data-ttu-id="e551c-160">기억하세요. 연결 문자열은 `[password]@[host name]:[port]` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-160">Remember, your connection string is in the form of: `[password]@[host name]:[port]`</span></span>

<span data-ttu-id="e551c-161">예제 연결 문자열은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-161">An example connection string would look something like this:</span></span>

```output
ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6379
```
    
## <a name="insert-two-data-values-into-your-azure-redis-cache"></a><span data-ttu-id="e551c-162">Azure Redis Cache에 두 개의 데이터 값을 삽입</span><span class="sxs-lookup"><span data-stu-id="e551c-162">Insert two data values into your Azure Redis Cache</span></span>

<span data-ttu-id="e551c-163">마지막으로, Azure Redis Cache에 데이터를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-163">Finally, we're going to add data into your Azure Redis Cache.</span></span>

1. <span data-ttu-id="e551c-164">**Program.cs** 파일 맨 위에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-164">Add the following using statement to the top of the **Program.cs** file.</span></span>

    ```csharp
    using ServiceStack.Redis;
    ```

1. <span data-ttu-id="e551c-165">**Main** 메서드에 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-165">Add the following snippet of code in your **Main** method.</span></span> <span data-ttu-id="e551c-166">두 값이 일시적으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-166">This will add two values transitionally.</span></span>

    ```csharp
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        if(transactionResult)
            Console.WriteLine("Transaction committed");
        else
            Console.WriteLine("Transaction failed to commit");
    }
    ```
1. <span data-ttu-id="e551c-167">편집기 창 맨 아래에 있는 명령 프롬프트를 통해 응용 프로그램을 실행하고 콘솔에 **트랜잭션 커밋됨**이라고 나오는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-167">Run the application through the command prompt at the bottom of the editor window and verify that the console says **Transaction committed**.</span></span> 

    ```bash
    dotnet run
    ```
    
## <a name="verify-your-data"></a><span data-ttu-id="e551c-168">데이터 확인</span><span class="sxs-lookup"><span data-stu-id="e551c-168">Verify your data</span></span>

<span data-ttu-id="e551c-169">마지막 마무리로, 추가한 데이터가 Azure Redis Cache에 있는지 확인하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-169">To finish off, let's verify that the data we added is in our Azure Redis Cache.</span></span>

1. <span data-ttu-id="e551c-170">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-170">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="e551c-171">왼쪽 사이드바에서 **모든 리소스**를 선택하여 Redis 캐시를 찾은 다음, 왼쪽의 필터 상자를 사용하여 Redis Cache 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-171">Locate your Redis cache by selecting **All Resources** in the left-hand sidebar and using the filter box on the left to select Redis Cache instances.</span></span> <span data-ttu-id="e551c-172">또는 맨 위에 있는 검색 상자를 사용하여 캐시 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-172">Alternatively, you can use the search box at the top and type the name of the cache.</span></span>

1. <span data-ttu-id="e551c-173">Redis 캐시 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-173">Select your Redis cache instance.</span></span>

1. <span data-ttu-id="e551c-174">Redis Cache의 **개요** 블레이드에서 **콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-174">In the **Overview** blade for your Redis Cache, select **Console**.</span></span> <span data-ttu-id="e551c-175">하위 수준 Redis 명령을 입력할 수 있는 Redis 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-175">This will open a Redis console, which allows you to enter low-level Redis commands.</span></span>

1. <span data-ttu-id="e551c-176">**get MyKey1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-176">Type **get MyKey1**.</span></span> <span data-ttu-id="e551c-177">반환된 값이 **MyValue1**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-177">Verify that the value returned is **MyValue1**.</span></span>

1. <span data-ttu-id="e551c-178">**get MyKey2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-178">Type **get MyKey2**.</span></span> <span data-ttu-id="e551c-179">반환된 값이 **MyValue2**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e551c-179">Verify that the value returned is **MyValue2**.</span></span>

    ![값 MyKey1 및 MyKey2를 보여주는 Azure Redis 콘솔 스크린샷.](../media/4-redis-console.png)