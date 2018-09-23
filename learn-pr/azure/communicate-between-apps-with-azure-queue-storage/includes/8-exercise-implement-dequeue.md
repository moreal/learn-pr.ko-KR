<span data-ttu-id="99ec5-101">이제 큐의 다음 메시지를 읽고, 처리한 후 큐에서 삭제하는 코드를 작성하여 응용 프로그램을 완료하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-101">Now we want to complete the application by writing code to read the next message in the queue, process it, and delete it from the queue.</span></span> 

<span data-ttu-id="99ec5-102">이 코드를 동일한 응용 프로그램에 배치하고, 매개 변수를 전달하지 않을 때 실행하려고 합니다. 그러나 지금 진행하는 뉴스 서비스 시나리오에서는 실제로 이 코드를 중간 계층 서버에 배치하여 기사를 처리할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-102">We're going to place this code into the same application and execute it when you don't pass any parameters, however in our news service scenario, we would really place this code into our middle-tier servers to process the stories.</span></span>

## <a name="dequeue-a-message"></a><span data-ttu-id="99ec5-103">큐에서 메시지 제거</span><span class="sxs-lookup"><span data-stu-id="99ec5-103">Dequeue a message</span></span>

<span data-ttu-id="99ec5-104">큐에서 다음 메시지를 검색하는 새 메서드를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-104">Let's add a new method that retrieves the next message from the queue.</span></span>

1. <span data-ttu-id="99ec5-105">편집기에서 `Program.cs` 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-105">Open the `Program.cs` source file in your editor.</span></span>

1. <span data-ttu-id="99ec5-106">매개 변수를 사용하지 않고 `Task<string>`을 반환하는 `ReceiveArticleAsync`라는 정적 메서드를 `Program` 클래스에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-106">Create a static method in the `Program` class named `ReceiveArticleAsync` that takes no parameters and returns a `Task<string>`.</span></span> <span data-ttu-id="99ec5-107">이 메서드를 사용하여 큐에서 뉴스 기사를 끌어와 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-107">We'll use this method to pull a news article from the queue and return it.</span></span>
    - <span data-ttu-id="99ec5-108">일부 비동기 `Task` 기반 메서드를 사용하게 되므로 계속 진행하면서 `async` 키워드를 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-108">Go ahead and add the `async` keyword to the method since we'll be using some asynchronous `Task`-based methods.</span></span>

    ```csharp
    static async Task<string> ReceiveArticleAsync()
    {
    }

1. All of the setup code to get a `CloudQueue` will be identical to what we did in the last exercise. Code duplication is a bad habit, even in samples so go ahead and, refactor the code that obtains the `CloudQueue` to a new method named `GetQueue` and change the `SendArticleAsync` to use your new method.
     - Make sure to leave the code that _creates_ the queue in the `SendArticleAsync` method; remember only the **publisher** should create the queue.

    ```csharp
    const string ConnectionString = ...;
    // ...

    static CloudQueue GetQueue()
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        return queueClient.GetQueueReference("newsqueue");
    }
    ```
    
1. <span data-ttu-id="99ec5-109">`ReceiveArticleAsync` 메서드에서 새 `GetQueue` 메서드를 호출하여 큐 참조를 가져온 후 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-109">In your `ReceiveArticleAsync` method, call the new `GetQueue` method to retrieve your queue reference and assign it to a variable.</span></span>

1. <span data-ttu-id="99ec5-110">그런 다음, `CloudQueue` 개체에 대해 `ExistsAsync` 메서드를 호출합니다. 그러면 큐가 만들어졌는지와 관계없이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-110">Next, call the `ExistsAsync` method on the `CloudQueue` object; this will return whether the queue has been created.</span></span> <span data-ttu-id="99ec5-111">존재하지 않는 큐에서 메시지를 검색하려고 하면 API가 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-111">If we attempt to retrieve a message from a non-existent queue, the API will throw an exception.</span></span>
    - <span data-ttu-id="99ec5-112">이 메서드는 비동기적이므로 `await`를 사용하여 반환 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-112">This method is asynchronous so use `await` to get the return value.</span></span>
    - <span data-ttu-id="99ec5-113">`ReceiveArticleAsync` 메서드에 `async` 키워드가 이미 있어야 하지만, 없으면 지금 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-113">You should already have the `async` keyword on the `ReceiveArticleAsync` method, but if not add it now.</span></span>


1. <span data-ttu-id="99ec5-114">`ExistsAsync`의 반환 값을 사용하는 `if` 블록을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-114">Add an `if` block that uses the return value from `ExistsAsync`.</span></span> <span data-ttu-id="99ec5-115">큐에서 블록으로 값을 읽는 코드를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-115">We'll add our code to read a value from the queue into the block.</span></span> <span data-ttu-id="99ec5-116">값을 읽지 못했음을 나타내는 마지막 반환 문자열을 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-116">Add a final return string to the method that indicates no value was read.</span></span> <span data-ttu-id="99ec5-117">메서드는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-117">Your method should be looking something like this:</span></span>

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
    }

    return "<queue empty or not created>";
}
```

1. <span data-ttu-id="99ec5-118">`CloudQueue` 개체에 대해 `GetMessageAsync`를 호출하여 큐에서 첫 번째 `CloudQueueMessage`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-118">Call `GetMessageAsync` on the `CloudQueue` object to get the first `CloudQueueMessage` from the queue.</span></span> <span data-ttu-id="99ec5-119">큐가 비어 있으면 반환 값은 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-119">The return value will be `null` if the queue is empty.</span></span>

1. <span data-ttu-id="99ec5-120">Null이 아니면 `CloudQueueMessage` 개체에 `AsString` 속성을 사용하여 메시지 내용을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-120">If it's non-null, use the `AsString` property on the `CloudQueueMessage` object to get the contents of the message.</span></span>

1. <span data-ttu-id="99ec5-121">`CloudQueue` 개체에 대해 `DeleteMessageAsync`를 호출하여 큐에서 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-121">Call `DeleteMessageAsync` on the `CloudQueue` object to delete the message from the queue.</span></span>

<span data-ttu-id="99ec5-122">최종 메서드 구현은 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-122">The final method implementation should resemble:</span></span>

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
        CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
        if (retrievedArticle != null)
        {
            string newsMessage = retrievedArticle.AsString;
            await queue.DeleteMessageAsync(retrievedArticle);
            return newsMessage;
        }
    }

    return "<queue empty or not created>";
}
```

## <a name="call-the-receivearticleasync-method"></a><span data-ttu-id="99ec5-123">ReceiveArticleAsync 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="99ec5-123">Call the ReceiveArticleAsync method</span></span>

<span data-ttu-id="99ec5-124">마지막으로, 새 메서드를 호출하는 지원을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-124">Finally, let's add support to invoke our new method.</span></span> <span data-ttu-id="99ec5-125">프로그램에 매개 변수를 전달하지 않을 때 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-125">We'll do this when we don't pass any parameters into the program.</span></span>

1. <span data-ttu-id="99ec5-126">`Main` 메서드와 매개 변수를 찾기 위해 이전에 추가한 `if` 블록을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-126">Locate the `Main` method and specifically the `if` block you added earlier to look for parameters.</span></span>

1. <span data-ttu-id="99ec5-127">`else` 조건을 추가하고 `ReceiveArticleAsync` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-127">Add an `else` condition and call the `ReceiveArticleAsync` method.</span></span> 

1. <span data-ttu-id="99ec5-128">비동기이므로 `await` 키워드를 사용하여 결과를 검색하고 콘솔 창에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-128">Since it's asynchronous, use the `await` keyword to retrieve the result and print it to the console window.</span></span> <span data-ttu-id="99ec5-129">앱을 C# 7.1로 변환하지 않은 경우 반환 작업에서 `Result` 속성을 사용하여 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-129">If you didn't convert your app to C# 7.1, you can get the value using the `Result` property from the returning task.</span></span>

<span data-ttu-id="99ec5-130">코드는 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-130">Your code should look something like:</span></span>

```csharp
if (args.Length > 0)
{
    // ...
}
else
{
    string value = await ReceiveArticleAsync();
    Console.WriteLine($"Received {value}");
}
```

## <a name="execute-the-application"></a><span data-ttu-id="99ec5-131">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="99ec5-131">Execute the application</span></span>

<span data-ttu-id="99ec5-132">이제 코드가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-132">The code is now complete.</span></span> <span data-ttu-id="99ec5-133">이제 메시지를 보내고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-133">It can now send and retrieve messages.</span></span> 

> [!WARNING]
> <span data-ttu-id="99ec5-134">프로그램을 빌드하고 실행하기 전에 온라인 편집기에서 모든 파일을 저장했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-134">Make sure you have saved all the files in the online editor before you build and run the program.</span></span>

<span data-ttu-id="99ec5-135">이를 테스트하려면 `dotnet run`을 사용하고 매개 변수를 전달하여 메시지를 전송하고, 매개 변수를 삭제하여 단일 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-135">To test it, use `dotnet run` and pass parameters to send messages, and leave off parameters to read a single message.</span></span>

<span data-ttu-id="99ec5-136">큐가 없을 때 테스트하려면 Azure CLI를 사용하여 큐(및 모든 데이터)를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-136">If you want to test when a queue doesn't exist, you can delete the queue (and all the data) with the Azure CLI.</span></span> <span data-ttu-id="99ec5-137">`<connection-string>` 매개 변수를 바꾸어야 합니다(또는 환경 변수 설정).</span><span class="sxs-lookup"><span data-stu-id="99ec5-137">Make sure to replace the `<connection-string>` parameter (or set the environment variable).</span></span>

```azurecli
az storage queue delete --name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="99ec5-138">다음번에 메시지를 추가할 때 큐가 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-138">The next time you add a message, the queue should be re-created.</span></span>

> [!NOTE]
> <span data-ttu-id="99ec5-139">삭제 작업은 실제로 비동기적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-139">The delete operation actually occurs asynchronously.</span></span> <span data-ttu-id="99ec5-140">완료되지 않았다면 큐를 다시 만들려고 할 때 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99ec5-140">If it has not completed you may get an exception when you attempt to re-create the queue.</span></span>