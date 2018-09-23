<span data-ttu-id="a4db3-101">이제 모든 요구 사항이 충족되었으므로 새 저장소 큐를 만들고 메시지를 추가하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-101">Now that all the requirements are in place, you can write code that creates a new storage queue and adds a message.</span></span> <span data-ttu-id="a4db3-102">일반적으로 이 코드를 데이터를 생성하는 프런트 엔드 앱에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-102">We would typically place this code in our front-end apps that generate the data.</span></span>

## <a name="add-the-client-library-for-azure-storage"></a><span data-ttu-id="a4db3-103">Azure Storage용 클라이언트 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="a4db3-103">Add the client library for Azure Storage</span></span>

<span data-ttu-id="a4db3-104">먼저 앱에 **.NET용 Azure Storage 클라이언트 라이브러리**를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-104">Let's start by adding the **Azure Storage Client Library for .NET** to our app.</span></span> <span data-ttu-id="a4db3-105">이 라이브러리는 NuGet(.NET 패키지 관리자)을 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-105">It can be installed with NuGet (a .NET package manager).</span></span> 

1. <span data-ttu-id="a4db3-106">`dotnet add package` 명령을 사용하여 `WindowsAzure.Storage` 패키지를 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-106">Install the `WindowsAzure.Storage` package to the project with the `dotnet add package` command.</span></span> <span data-ttu-id="a4db3-107">이 작업은 Cloud Shell _아래_ 터미널 창에서 수행하거나 로컬 컴퓨터를 사용하는 경우에는 프로젝트와 같은 폴더에 있는 터미널/콘솔 창에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-107">You can do this in the terminal window _below_ the Cloud Shell, or if you are working on your local computer, in a terminal/console window in the same folder as the project.</span></span>

```azurecli
dotnet add package WindowsAzure.Storage
```

## <a name="add-a-method-to-send-a-news-alert"></a><span data-ttu-id="a4db3-108">뉴스 알림을 전송하는 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="a4db3-108">Add a method to send a news alert</span></span>

<span data-ttu-id="a4db3-109">다음으로, 큐에 새 기사를 전송하는 새 메서드를 작성해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-109">Next, let's create a new method to send a news story into a queue.</span></span>

1. <span data-ttu-id="a4db3-110">코드 편집기에서 `Program.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-110">Open the `Program.cs` file in your code editor.</span></span>

1. <span data-ttu-id="a4db3-111">파일 맨 위에 다음 네임스페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-111">At the top of the file, add the following namespaces.</span></span> <span data-ttu-id="a4db3-112">이러한 두 네임스페이스를 사용해서 Azure Storage에 연결한 후 큐 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-112">We'll be using types from both of these to connect to Azure Storage and then to work with queues.</span></span>

    - `System.Threading.Tasks`
    - `Microsoft.WindowsAzure.Storage`
    - `Microsoft.WindowsAzure.Storage.Queue`

1. <span data-ttu-id="a4db3-113">`string`을 사용하고 `Task`를 반환하는 `SendArticleAsync`라는 정적 메서드를 `Program` 클래스에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-113">Create a static method in the `Program` class named `SendArticleAsync` that takes a `string` and returns a `Task`.</span></span> <span data-ttu-id="a4db3-114">이 메서드를 사용하여 서비스로 새 기사를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-114">We'll use this method to send a news article in to our service.</span></span> <span data-ttu-id="a4db3-115">아래와 같이 입력 매개 변수 이름을 `newsMessage`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-115">Name the input parameter `newsMessage` as shown below.</span></span>

    ```csharp
    ...
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Queue; 
    
    class Program
    {
        ...
    
        static async Task SendArticleAsync(string newsMessage)
        {
        }
    }
    ```
    
1. <span data-ttu-id="a4db3-116">새 메서드에서 정적 `CloudStorageAccount.Parse` 메서드를 사용하여 연결 문자열(상수 문자열에 배치함)을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-116">In your new method, use the static `CloudStorageAccount.Parse` method to parse your connection string (recall we placed it into a constant string).</span></span> <span data-ttu-id="a4db3-117">이 메서드는 변수에 저장해야 하는 `CloudStorageAccount` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-117">This method returns a `CloudStorageAccount` object that needs to be stored in a variable.</span></span>

1. <span data-ttu-id="a4db3-118">저장소 계정 개체에 대해 `CreateCloudQueueClient()` 메서드를 호출하여 클라이언트 개체를 가져온 후 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-118">Call the `CreateCloudQueueClient()` method on the storage account object to get a client object and store that in a variable.</span></span>

1. <span data-ttu-id="a4db3-119">그런 다음, 클라이언트 개체에 대해 `GetQueueReference` 메서드를 호출하고 큐 이름으로 "newsqueue" 문자열을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-119">Next, call `GetQueueReference` method on the client object and pass the string "newsqueue" for the queue name.</span></span> <span data-ttu-id="a4db3-120">이렇게 하면 큐 작업에 사용할 수 있는 `CloudQueue` 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-120">This returns a `CloudQueue` object that we can use to work with the queue.</span></span> <span data-ttu-id="a4db3-121">큐가 아직 없어도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-121">It's OK if the queue does not exist yet.</span></span>

1. <span data-ttu-id="a4db3-122">`CloudQueue` 개체에 대해 `CreateIfNotExistsAsync()`를 호출하여 큐를 사용할 준비가 되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-122">Call `CreateIfNotExistsAsync()` on the `CloudQueue` object to ensure the queue is ready for use.</span></span> <span data-ttu-id="a4db3-123">이렇게 하면 필요한 경우 큐가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-123">This will create the queue if necessary.</span></span>
    - <span data-ttu-id="a4db3-124">이것은 비동기 메서드이므로 C# `await` 키워드를 사용하여 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-124">Since this is an asynchronous method, use the C# `await` keyword to ensure we work properly with it.</span></span> <span data-ttu-id="a4db3-125">또한 `async` 키워드로 _메서드_를 데코레이팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-125">That also means you need to decorate the _method_ with the `async` keyword.</span></span> 
    - <span data-ttu-id="a4db3-126">`CreateIfNotExistsAsync`은 큐가 생성되면 `true`, 큐가 이미 존재하는 경우 `false`에 해당하는 `bool` 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-126">`CreateIfNotExistsAsync` returns a `bool` value that will be `true` if the queue was created and `false` if it already exists.</span></span> <span data-ttu-id="a4db3-127">큐를 만든 경우 콘솔에 메시지가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-127">Output a message to the console if we created the queue.</span></span>
    - <span data-ttu-id="a4db3-128">도움이 필요한 경우 다음과 같은 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4db3-128">Here's an example if you need some help.</span></span>

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        // Not Shown here - code from prior steps
        ...
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    }
    ```

1. <span data-ttu-id="a4db3-129">`CloudQueueMessage`의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-129">Create an instance of a `CloudQueueMessage`.</span></span> 
    - <span data-ttu-id="a4db3-130">이 인스턴스는 `string` 매개 변수를 사용하고 메서드 매개 변수(`newsMessage`)를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-130">It takes a `string` parameter, pass in the method parameter (`newsMessage`).</span></span> <span data-ttu-id="a4db3-131">이것이 메시지의 _본문_이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-131">This will be the _body_ of the message.</span></span> <span data-ttu-id="a4db3-132">이진 메시지 페이로드를 만들 수 있는 명명된 정적 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-132">There is also a static method named  that can create a binary message payload.</span></span>

1. <span data-ttu-id="a4db3-133">`CloudQueue` 개체에 대해 `AddMessageAsync`를 호출하여 큐에 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-133">Call `AddMessageAsync` on the `CloudQueue` object to add the message to the queue.</span></span> <span data-ttu-id="a4db3-134">이것은 비동기 메서드이기도 하며, `await` 키워드를 사용하여 올바르게 상호 작용하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-134">This is also an asynchronous method and you will need to use the `await` keyword to ensure we properly interact with it.</span></span>

1. <span data-ttu-id="a4db3-135">파일을 저장하고 명령 창에 `dotnet build`를 입력하여 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-135">Save the file and build it by typing `dotnet build` into the command window.</span></span> <span data-ttu-id="a4db3-136">모든 오류를 수정합니다. 다음 코드를 사용하여 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-136">Fix any errors, you can use the following code to check your work.</span></span>

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    
        CloudQueue queue = queueClient.GetQueueReference("newsqueue");
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    
        CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
        await queue.AddMessageAsync(articleMessage);
    }
    ```

## <a name="add-code-to-send-a-message"></a><span data-ttu-id="a4db3-137">메시지를 보내는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="a4db3-137">Add code to send a message</span></span>

<span data-ttu-id="a4db3-138">새 send 메서드를 테스트할 수 있게 새 메서드에 수신된 매개 변수를 전달하도록 `Main` 메서드를 수정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-138">Let's modify the `Main` method to pass any parameters received into our new method so we can test our new send method.</span></span>

1. <span data-ttu-id="a4db3-139">`Main` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-139">Locate the `Main` method.</span></span>

1. <span data-ttu-id="a4db3-140">전달된 `args` 매개 변수를 확인하여 명령줄에 데이터가 전달되었는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-140">Check the passed `args` parameter to see if any data was passed to the command line.</span></span> <span data-ttu-id="a4db3-141">데이터가 전달되었으면 `String.Join`을 사용하여 공백을 구분 기호로 써서 모든 단어에서 단일 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-141">If so, use `String.Join` to create a single string from all the words using a space as the separator.</span></span>

1. <span data-ttu-id="a4db3-142">새 `SendArticleAsync` 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-142">Pass that to the new `SendArticleAsync` method.</span></span> 

1. <span data-ttu-id="a4db3-143">일단 반환되면 `Console.WriteLine`을 사용하여 보낸 메시지를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-143">Once it returns, use `Console.WriteLine` to output the message we sent.</span></span>

1. <span data-ttu-id="a4db3-144">파일을 저장하고 프로그램(`dotnet build`)을 빌드한 후 아래 코드를 사용하여 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-144">Save the file and build the program (`dotnet build`), you can use the code below to check your work.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a4db3-145">이 메서드는 기술적으로 비동기적이므로 `await` 키워드를 사용하지만, C# 7.1 이상을 사용하지 않으면 `Main` 메서드에서 해당 기능을 사용할 수 없습니다(새로운 기능).</span><span class="sxs-lookup"><span data-stu-id="a4db3-145">Since our method is technically asynchronous, we will want to use the `await` keyword, however that feature isn't available on your `Main` method unless you are using C# 7.1 or later.</span></span> <span data-ttu-id="a4db3-146">메서드에서 `Wait()`를 호출하여 메서드가 반환될 때까지 대기하는 실제로 차단합니다. 이것은 잠시 후에 수정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-146">Just call `Wait()` on the method to actually block waiting for the method to return, we'll fix that in a minute.</span></span>

    ```csharp
    static void Main(string[] args)
    {
        if (args.Length > 0)
        {
            string value = String.Join(" ", args);
            SendArticleAsync(value).Wait();
            Console.WriteLine($"Sent: {value}");
        }
    }
    ```

## <a name="execute-the-application"></a><span data-ttu-id="a4db3-147">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="a4db3-147">Execute the application</span></span>

<span data-ttu-id="a4db3-148">이제 응용 프로그램이 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-148">The application can now send messages.</span></span> <span data-ttu-id="a4db3-149">이를 테스트하려면 `dotnet run` 명령을 사용하여 명령줄에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-149">To test it, you can run it from the command line with the `dotnet run` command.</span></span> <span data-ttu-id="a4db3-150">추가 문자열이 응용 프로그램에 매개 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-150">Any additional strings are passed as parameters to the application.</span></span> 

> [!WARNING]
> <span data-ttu-id="a4db3-151">프로그램을 빌드하고 실행하기 전에 온라인 편집기에서 모든 파일을 저장했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-151">Make sure you have saved all the files in the online editor before you build and run the program.</span></span>

<span data-ttu-id="a4db3-152">예를 들어, 다음을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-152">As an example, you can type:</span></span>

```azurecli
dotnet run Send this message
```

<span data-ttu-id="a4db3-153">이렇게 하면 큐에 `"Send this message"` 문자열이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-153">This should add the string `"Send this message"` into the queue.</span></span>

## <a name="check-your-results"></a><span data-ttu-id="a4db3-154">결과 확인</span><span class="sxs-lookup"><span data-stu-id="a4db3-154">Check your results</span></span>

<span data-ttu-id="a4db3-155">**Storage 탐색기**를 사용하여 Azure Portal에서 큐를 확인할 수 있습니다. 해당 제품을 열면 사용자 소유의 각 저장소 계정에서 데이터를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-155">You can check queues in the Azure portal using the **Storage Explorer**, if you open that product it will let you explore the data in each storage account you own.</span></span>

<span data-ttu-id="a4db3-156">또는 Azure CLI 또는 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-156">Alternatively, you can use the Azure CLI or PowerShell.</span></span> <span data-ttu-id="a4db3-157">셸에서 `<connection-string>` 값을 특정 연결 문자열로 바꾸어 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-157">Try this command in the shell, replacing the `<connection-string>` value with your specific connection string:</span></span>

```azurecli
az storage message peek --queue-name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="a4db3-158">이렇게 하면 다음과 같은 메시지에 대한 정보가 덤프됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-158">This should dump the information for your message, which will look something like this:</span></span>

```json
[
  {
    "content": "U2VuZCB0aGlzIG1lc3NhZ2U=",
    "dequeueCount": 0,
    "expirationTime": "2018-09-05T02:43:40+00:00",
    "id": "b47cbe9f-a246-4a81-86ae-fa02ea8d98bc",
    "insertionTime": "2018-09-24T02:43:40+00:00",
    "popReceipt": null,
    "timeNextVisible": null
  }
]
```

<span data-ttu-id="a4db3-159">도구를 사용하여 시도할 수 있는 여러 다른 명령이 있습니다. `az storage queue --help` 및 `az storage message --help`를 확인하여 이러한 명령을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a4db3-159">There are several other commands available that you can try with the tools - check out both `az storage queue --help` and `az storage message --help` to explore them.</span></span>

> [!TIP]
> <span data-ttu-id="a4db3-160">`AZURE_STORAGE_CONNECTION_STRING`이라는 환경 변수에 연결 문자열을 추가하여 매번 `--connection-string` 매개 변수를 입력할 필요가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-160">Put your connection string value into an environment variable named `AZURE_STORAGE_CONNECTION_STRING` to save yourself from having to type the `--connection-string` parameter every time!</span></span>

## <a name="optional---use-the-async-versions-of-the-methods"></a><span data-ttu-id="a4db3-161">선택 사항 - 메서드의 비동기 버전 사용</span><span class="sxs-lookup"><span data-stu-id="a4db3-161">Optional - Use the async versions of the methods</span></span>

<span data-ttu-id="a4db3-162">위의 send 메서드에서 `Wait()`를 사용했지만 이렇게 하면 계산 리소스가 효율적으로 사용되지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-162">We used `Wait()` on the send method above but that's not an efficient use of our computing resources.</span></span> <span data-ttu-id="a4db3-163">대신 C# `async` 및 `await` 메서드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-163">Instead, we want to use the C# `async` and `await` methods.</span></span> <span data-ttu-id="a4db3-164">하지만 **Main** 메서드에 이러한 키워드를 적용하려면 C# 7.1 _이상_을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-164">However, we will need to be using _at least_ C# 7.1 to be able to apply these keywords to our **Main** method.</span></span>

### <a name="switch-to-c-71"></a><span data-ttu-id="a4db3-165">C# 7.1로 전환</span><span class="sxs-lookup"><span data-stu-id="a4db3-165">Switch to C# 7.1</span></span>

<span data-ttu-id="a4db3-166">C#의 `async` 및 `await` 키워드는 C# 7.1까지는 **Main** 메서드에서 유효한 키워드가 아니었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-166">C#'s `async` and `await` keywords were not valid keywords in **Main** methods until C# 7.1.</span></span> <span data-ttu-id="a4db3-167">**.csproj** 파일의 플래그를 통해 해당 컴파일러로 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-167">We can easily switch to that compiler through a flag in the **.csproj** file.</span></span>

1. <span data-ttu-id="a4db3-168">편집기에서 **QueueApp.csproj** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-168">Open the **QueueApp.csproj** file in the editor.</span></span>

1. <span data-ttu-id="a4db3-169">빌드 파일에서 첫 번째 `PropertyGroup`에 `<LangVersion>7.1</LangVersion>`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-169">Add `<LangVersion>7.1</LangVersion>` into the first `PropertyGroup` in the build file.</span></span> <span data-ttu-id="a4db3-170">완성된 최종 상태는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-170">It should look like the following when you are finished.</span></span>
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a><span data-ttu-id="a4db3-171">비동기 키워드 적용</span><span class="sxs-lookup"><span data-stu-id="a4db3-171">Apply the async keyword</span></span>

<span data-ttu-id="a4db3-172">다음으로, **Main** 메서드에 `async` 키워드를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-172">Next, apply the `async` keyword to the **Main** method.</span></span> <span data-ttu-id="a4db3-173">세 가지를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-173">We will have to do three things.</span></span>

1. <span data-ttu-id="a4db3-174">**Main** 메서드 서명에 `async` 키워드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-174">Add the `async` keyword onto the **Main** method signature.</span></span>
1. <span data-ttu-id="a4db3-175">반환 형식을 `void`에서 `Task`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-175">Change the return type from `void` to `Task`.</span></span>
1. <span data-ttu-id="a4db3-176">`SendArticleAsync`에 대한 호출에서 `Wait()`에 대한 호출을 제거하고 `await`로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-176">Remove the call to `Wait()` on the call to `SendArticleAsync` and replace it with `await`.</span></span>

<span data-ttu-id="a4db3-177">앱을 다시 실행해봅니다. 이전과 똑같이 실행되겠지만 현재 코드는 메시지가 큐에 추가되기를 기다리는 동안 스레드를 .NET 스레드 풀로 다시 릴리스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-177">Try running the app again - it should still work exactly as before, but now the code is able to release the thread back to the .NET threadpool while we wait for the message to be queued.</span></span>

<span data-ttu-id="a4db3-178">메시지를 보냈으면, 마지막 단계는 메시지를 _수신_하기 위한 지원을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a4db3-178">Now that we have sent a message, the last step is to add support to _receive_ the message.</span></span>