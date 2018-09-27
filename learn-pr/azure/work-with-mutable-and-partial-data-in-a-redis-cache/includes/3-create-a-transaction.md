<span data-ttu-id="5535f-101">Azure Redis Cache 인스턴스를 만든 다음, 이 캐시에 두 개의 데이터 값을 삽입하는 간단한 트랜잭션을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-101">Let's start by creating an instance of Azure Redis Cache, and then create a simple transaction that inserts two data values into the cache.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="5535f-102">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="5535f-102">Create an Azure Redis Cache</span></span>

<span data-ttu-id="5535f-103">먼저 Azure CLI를 사용하여 Azure Redis Cache를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-103">Let's start by creating an Azure Redis Cache with the Azure CLI.</span></span> <span data-ttu-id="5535f-104">브라우저 창의 오른쪽에서 Cloud Shell을 사용하여 Azure와 상호작용합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-104">Use the Cloud Shell on the right side of the browser window to interact with Azure.</span></span>

<span data-ttu-id="5535f-105">`az redis create` 명령을 사용하여 새 Azure Redis Cache를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-105">We'll use the `az redis create` command to create a new Azure Redis Cache.</span></span> <span data-ttu-id="5535f-106">여러 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-106">It takes several parameters.</span></span> <span data-ttu-id="5535f-107">다음은 가장 일반적인 매개 변수입니다(전체 목록은 설명서 확인).</span><span class="sxs-lookup"><span data-stu-id="5535f-107">Here are the most common (to get a full list, check the documentation).</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="5535f-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5535f-108">Parameter</span></span> | <span data-ttu-id="5535f-109">설명</span><span class="sxs-lookup"><span data-stu-id="5535f-109">Description</span></span> |
> |-----------|-------------|
> | `--name`    | <span data-ttu-id="5535f-110">캐시 이름 - 글로벌로 고유해야 하며 문자, 숫자, 대시로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-110">The name of the cache - this must be globally unique and composed of letters, numbers, and dashes.</span></span> |
> | `--resource-group` | <span data-ttu-id="5535f-111">Azure 샌드박스에 포함된 미리 생성된 리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-111">Use the pre-created Resource Group **<rgn>[sandbox resource group name]</rgn>**, which is part of the Azure sandbox.</span></span> |
> | `--location` | <span data-ttu-id="5535f-112">캐시를 배치할 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-112">Specify the location where the cache should be located.</span></span> <span data-ttu-id="5535f-113">일반적으로 데이터 소비자와 가까운 위치를 선택하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-113">Normally, you will want to choose a location close to the data consumers.</span></span> <span data-ttu-id="5535f-114">이 경우 Azure 샌드박스에서 사용할 수 있는 위치로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-114">In this case, you are limited to the locations available in the Azure sandbox.</span></span> <span data-ttu-id="5535f-115">사용자에게 가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-115">Select the closest one to you.</span></span> |
> | `--size` | <span data-ttu-id="5535f-116">Azure Redis Cache의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-116">The size of the Azure Redis Cache.</span></span> <span data-ttu-id="5535f-117">유효한 값은 [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]입니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-117">Valid values are [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4].</span></span> |
> | `--sku` | <span data-ttu-id="5535f-118">Azure Redis Cache SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-118">The Azure Redis Cache SKU.</span></span> <span data-ttu-id="5535f-119">유효한 값은 [기본, 표준, 프리미엄]입니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-119">Valid values are [Basic, Standard, Premium].</span></span> |

### <a name="select-a-location"></a><span data-ttu-id="5535f-120">위치 선택</span><span class="sxs-lookup"><span data-stu-id="5535f-120">Select a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="5535f-121">다음 옵션을 사용하여 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-121">Create a cache using the following options:</span></span>
    - <span data-ttu-id="5535f-122">크기: C0</span><span class="sxs-lookup"><span data-stu-id="5535f-122">Size: C0</span></span>
    - <span data-ttu-id="5535f-123">SKU: 기본</span><span class="sxs-lookup"><span data-stu-id="5535f-123">SKU: Basic</span></span>

1. <span data-ttu-id="5535f-124">명령줄 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-124">Here's an example command line.</span></span> <span data-ttu-id="5535f-125">`[name]` 매개 변수를 고유한 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-125">Make sure to replace the `[name]` parameter with a unique name.</span></span> <span data-ttu-id="5535f-126">미국 동부 대신 다른 지역을 원하는 경우 위치를 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-126">You can replace the location if you want a different region than East US.</span></span>

    ```azurecli
    REDIS_NAME=[name]

    az redis create \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location eastus \
        --vm-size C0 \
        --sku Basic \
    ```

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="5535f-127">.NET Core 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="5535f-127">Create a .NET Core console application</span></span>

<span data-ttu-id="5535f-128">다음으로, Azure Redis Cache에 데이터 값을 삽입하는 데 사용할 .NET Core 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-128">Next, create a .NET Core console application, which will be used to insert data values into our Azure Redis Cache.</span></span>

1. <span data-ttu-id="5535f-129">창 오른쪽의 통합 Cloud Shell을 사용하여 새 .NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-129">Create a new .NET Core application using the integrated Cloud Shell on the right hand side of the window.</span></span> <span data-ttu-id="5535f-130">이름을 "RedisData"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-130">Name it "RedisData".</span></span>

    ```bash
    cd ~
    dotnet new console --name RedisData
    ```

1. <span data-ttu-id="5535f-131">앱에 대해 만든 새 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-131">Change into the new directory created for your app.</span></span>

    ```bash
    cd RedisData
    ```

1. <span data-ttu-id="5535f-132">응용 프로그램을 빌드하고 실행하면 "Hello World!"가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-132">Build and run the application - it should output "Hello World!"</span></span>

    ```bash
    dotnet run
    ```

## <a name="add-the-servicestackredis-nuget-package"></a><span data-ttu-id="5535f-133">ServiceStack.Redis NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="5535f-133">Add the ServiceStack.Redis NuGet package</span></span>

<span data-ttu-id="5535f-134">콘솔 응용 프로그램이 생겼으니, **ServiceStack.Redis** NuGet 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-134">Now that we have our console application, we need to add the **ServiceStack.Redis** NuGet package.</span></span> <span data-ttu-id="5535f-135">그러면 Azure Redis Cache에 연결하고 C#에서 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-135">This will allow us to connect to the Azure Redis Cache and issue commands in C#.</span></span>

1. <span data-ttu-id="5535f-136">터미널 셸을 사용하여 NuGet 패키지 **ServiceStack.Redis**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-136">Add the NuGet package **ServiceStack.Redis** using the terminal shell.</span></span>

    ```bash
    dotnet add package ServiceStack.Redis
    ```

1. <span data-ttu-id="5535f-137">응용 프로그램을 다시 빌드하고 실행하여 모두 컴파일되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-137">Build and run the application again to make sure it all compiles.</span></span> <span data-ttu-id="5535f-138">여전히 "Hello World!"가 출력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-138">It should still output "Hello World!"</span></span>

## <a name="get-your-azure-redis-cache-connection-string"></a><span data-ttu-id="5535f-139">Azure Redis Cache 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="5535f-139">Get your Azure Redis Cache connection string</span></span>

<span data-ttu-id="5535f-140">Azure Redis Cache에 연결하려면 암호 및 URL을 포함하고 있는 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-140">To connect to your Azure Redis Cache, you need a connection string that contains your password and URL.</span></span> <span data-ttu-id="5535f-141">**ServiceStack.Redis**는 `[password]@[hostname]:[sslport]?ssl=true` 형식의 고유한 연결 문자열을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-141">**ServiceStack.Redis** has its own connection string format: `[password]@[hostname]:[sslport]?ssl=true`.</span></span>

<span data-ttu-id="5535f-142">Azure Portal 또는 명령줄을 사용하여 암호를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-142">You can retrieve your password with the Azure portal, or with the command line.</span></span> <span data-ttu-id="5535f-143">"Redis로 읽기 전용 데이터를 캐시하여 웹 응용 프로그램 최적화"에서 포털을 사용했으니, 여기서는 명령줄을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-143">Let's use the latter here, since we used the portal approach in the "Optimize your web applications by caching read-only data with Redis" module.</span></span>

<span data-ttu-id="5535f-144">`az redis list-keys` 명령을 사용하여 액세스 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-144">Use the `az redis list-keys` command to get the access keys.</span></span> <span data-ttu-id="5535f-145">다음 명령을 실행하여 기본 키를 가져오고, `REDIS_KEY` 변수에 저장하고, 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-145">Run these commands to get the primary key, store it in a variable called `REDIS_KEY`, and display it:</span></span>

```azurecli
REDIS_KEY=$(az redis list-keys \
    --name "$REDIS_NAME" \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query primaryKey \
    --output tsv)

echo $REDIS_KEY
```

<span data-ttu-id="5535f-146">다음으로, 이 명령을 실행하여 연결 문자열을 결합하 고 명령줄에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-146">Next, run this command to put the connection string together and display it on the command line.</span></span> <span data-ttu-id="5535f-147">호스트 이름은 `.redis.cache.windows.net` 다음의 캐시 이름이고, 포트는 기본 Redis SSL 포트인 **6380**입니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-147">Note that the hostname is the name of the cache followed by `.redis.cache.windows.net`, and the port is **6380**, the default Redis SSL port.</span></span>

```bash
echo "$REDIS_KEY"@"$REDIS_NAME".redis.cache.windows.net:6380?ssl=true
```

<span data-ttu-id="5535f-148">다음 단계에서 사용할 연결 문자열을 &mdash; 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-148">Copy the connection string to the clipboard &mdash; you'll be using it in the next step.</span></span>

## <a name="add-the-connection-string-to-your-app"></a><span data-ttu-id="5535f-149">앱에 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="5535f-149">Add the connection string to your app</span></span>

1. <span data-ttu-id="5535f-150">응용 프로그램 폴더에서 Cloud Shell 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-150">Open the Cloud Shell editor from the application folder.</span></span>

    ```bash
    cd ~/RedisData
    code .
    ```

1. <span data-ttu-id="5535f-151">**Program.cs** 소스 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-151">Select the **Program.cs** source file.</span></span>

1. <span data-ttu-id="5535f-152">`Program` 클래스에 다음 필드를 만들고 연결 문자열에 값으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-152">Create the following field in the `Program` class and paste in your connection string as the value.</span></span>

    ```csharp
    static string redisConnectionString = "<connection string>";
    ```

    <span data-ttu-id="5535f-153">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-153">Here's an example:</span></span>

    ```csharp
    static string redisConnectionString = "ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6380?ssl=true";
    ```

## <a name="insert-two-data-values-into-your-azure-redis-cache"></a><span data-ttu-id="5535f-154">Azure Redis Cache에 두 개의 데이터 값을 삽입</span><span class="sxs-lookup"><span data-stu-id="5535f-154">Insert two data values into your Azure Redis Cache</span></span>

<span data-ttu-id="5535f-155">마지막으로, Azure Redis Cache에 데이터를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-155">Finally, we're going to add data into your Azure Redis Cache.</span></span>

1. <span data-ttu-id="5535f-156">**Program.cs** 파일 위쪽에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-156">Add the following `using` statement to the top of the **Program.cs** file.</span></span>

    ```csharp
    using ServiceStack.Redis;
    ```

1. <span data-ttu-id="5535f-157">`Main` 메서드의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-157">Replace the contents of the `Main` method with the following code.</span></span> <span data-ttu-id="5535f-158">이렇게 하면 트랜잭션을 사용하여 두 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-158">This will use a transaction to add two values.</span></span>

    ```csharp
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    if (transactionResult)
    {
        Console.WriteLine("Transaction committed");
    }
    else
    {
        Console.WriteLine("Transaction failed to commit");
    }
    ```

1. <span data-ttu-id="5535f-159">응용 프로그램을 빌드하고 실행하기 전에, Redis 캐시가 완전하게 프로비전되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-159">Before building and running the application, check to make sure that the Redis cache has been fully provisioned.</span></span> <span data-ttu-id="5535f-160">`az redis create` 명령이 완료된 후 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-160">It can sometimes take a few minutes after `az redis create` completes.</span></span> <span data-ttu-id="5535f-161">다음 명령을 실행하여 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-161">Run the following command to check the status.</span></span>

    ```azcli
    az redis show \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --query provisioningState
    ```

    <span data-ttu-id="5535f-162">상태가 `Creating`이면 몇 분 후에 다시 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5535f-162">If the status is `Creating`, try checking again in a couple of minutes.</span></span> <span data-ttu-id="5535f-163">완료되면 `Succeeded`로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-163">It will show `Succeeded` when finished.</span></span>

1. <span data-ttu-id="5535f-164">응용 프로그램을 실행하고 콘솔에 **트랜잭션 커밋됨**으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-164">Run the application and verify that the console says **Transaction committed**.</span></span>

    ```bash
    dotnet run
    ```

## <a name="verify-your-data"></a><span data-ttu-id="5535f-165">데이터 확인</span><span class="sxs-lookup"><span data-stu-id="5535f-165">Verify your data</span></span>

<span data-ttu-id="5535f-166">마지막 마무리로, 추가한 데이터가 Azure Redis Cache에 있는지 확인하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-166">To finish off, let's verify that the data we added is in our Azure Redis Cache.</span></span>

1. <span data-ttu-id="5535f-167">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-167">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="5535f-168">왼쪽 사이드바에서 **모든 리소스**를 선택하여 Azure Redis Cache를 찾은 다음, 왼쪽의 필터 상자를 사용하여 Azure Redis Cache 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-168">Locate your Azure Redis Cache by selecting **All Resources** in the left-hand sidebar, and using the filter box on the left to select Azure Redis Cache instances.</span></span> <span data-ttu-id="5535f-169">또는 맨 위에 있는 검색 상자를 사용하여 캐시 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-169">Alternatively, you can use the search box at the top, and type the name of the cache.</span></span>

1. <span data-ttu-id="5535f-170">Azure Redis Cache 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-170">Select your Azure Redis Cache instance.</span></span>

1. <span data-ttu-id="5535f-171">Azure Redis Cache의 **개요** 블레이드에서 **콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-171">In the **Overview** blade for your Azure Redis Cache, select **Console**.</span></span> <span data-ttu-id="5535f-172">하위 수준 Azure Redis Cache 명령을 입력할 수 있는 Azure Redis Cache 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-172">This will open an Azure Redis Cache console, which allows you to enter low-level Azure Redis Cache commands.</span></span>

1. <span data-ttu-id="5535f-173">**get MyKey1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-173">Type **get MyKey1**.</span></span> <span data-ttu-id="5535f-174">반환된 값이 **MyValue1**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-174">Verify that the value returned is **MyValue1**.</span></span>

1. <span data-ttu-id="5535f-175">**get MyKey2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-175">Type **get MyKey2**.</span></span> <span data-ttu-id="5535f-176">반환된 값이 **MyValue2**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5535f-176">Verify that the value returned is **MyValue2**.</span></span>

    ![값 MyKey1 및 MyKey2를 보여주는 Azure Redis Cache 콘솔 스크린샷.](../media/4-redis-console.png)