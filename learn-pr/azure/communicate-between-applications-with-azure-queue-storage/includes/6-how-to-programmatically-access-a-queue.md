<span data-ttu-id="d4491-101">큐에는 송신기와 수신기에 해당 모양이 알려져 있는 데이터 패킷인 메시지가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-101">Queues hold messages - packets of data whose shape is known to the sender and receiver.</span></span> <span data-ttu-id="d4491-102">송신기는 큐를 만들고 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-102">The sender creates the queue and adds a message.</span></span> <span data-ttu-id="d4491-103">수신기는 메시지를 검색하여 처리한 후 큐에서 해당 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-103">The receiver retrieves a message, processes it, and then deletes the message from the queue.</span></span> <span data-ttu-id="d4491-104">다음 그림은 이 프로세스의 일반적인 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-104">The following illustration shows a typical flow of this process.</span></span>

![Azure 큐를 통한 일반적인 메시지 흐름을 보여 주는 그림입니다.](../media/6-message-flow.png)

<span data-ttu-id="d4491-106">`get` 및 `delete`는 별도의 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-106">Notice that `get` and `delete` are separate operations.</span></span> <span data-ttu-id="d4491-107">이 배열에서는 수신기의 잠재적 실패를 처리하고 _at-least-once delivery_(최소 1회 전송)라는 개념을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-107">This arrangement handles potential failures in the receiver and implements a concept called _at-least-once delivery_.</span></span> <span data-ttu-id="d4491-108">수신기가 메시지를 받은 후에도 해당 메시지는 큐에 남아 있지만 30초 동안 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-108">After the receiver gets a message, that message remains in the queue but is invisible for 30 seconds.</span></span> <span data-ttu-id="d4491-109">수신기는 처리 중 작동이 중단되거나 전원 장애가 발생하는 경우 큐에서 메시지를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-109">If the receiver crashes or experiences a power failure during processing, then it will never delete the message from the queue.</span></span> <span data-ttu-id="d4491-110">30초 후 메시지가 큐에 다시 표시되고 수신기의 다른 인스턴스는 완료될 때까지 메시지를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-110">After 30 seconds, the message will reappear in the queue and another instance of the receiver can process it to completion.</span></span>

## <a name="the-azure-storage-client-library-for-net"></a><span data-ttu-id="d4491-111">.NET용 Azure Storage 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d4491-111">The Azure Storage Client Library for .NET</span></span>

<span data-ttu-id="d4491-112">**.NET용 Azure Storage 클라이언트 라이브러리**는 다음과 같이 조작해야 할 각 개체를 나타내는 유형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-112">The **Azure Storage Client Library for .NET** provides types to represent each of the objects you need to interact with:</span></span>

- <span data-ttu-id="d4491-113">`CloudStorageAccount`는 Azure Storage 계정을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-113">`CloudStorageAccount` represents your Azure storage account.</span></span>
- <span data-ttu-id="d4491-114">`CloudQueueClient`는 Azure Queue Storage를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-114">`CloudQueueClient` represents Azure Queue storage.</span></span>
- <span data-ttu-id="d4491-115">`CloudQueue`는 큐 인스턴스 중 하나를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-115">`CloudQueue` represents one of your queue instances.</span></span>
- <span data-ttu-id="d4491-116">`CloudQueueMessage`는 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-116">`CloudQueueMessage` represents a message.</span></span>

<span data-ttu-id="d4491-117">이러한 클래스는 큐에 대한 프로그래밍 방식 액세스를 얻는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-117">You will use these classes to get programmatic access to your queue.</span></span> <span data-ttu-id="d4491-118">라이브러리에는 동기 메서드와 비동기 메서드가 둘 다 있습니다. 클라이언트 앱이 차단되지 않도록 비동기 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-118">The library has both synchronous and asynchronous methods; you should prefer to use the asynchronous versions to avoid blocking the client app.</span></span>

> [!NOTE]
> <span data-ttu-id="d4491-119">.NET용 Azure Storage 클라이언트 라이브러리는 **WindowsAzure.Storage** NuGet 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-119">The Azure Storage Client Library for .NET is available in the **WindowsAzure.Storage** NuGet package.</span></span> <span data-ttu-id="d4491-120">IDE, Azure CLI 또는 PowerShell `Install-Package WindowsAzure.Storage`를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-120">You can install it through an IDE, Azure CLI, or through PowerShell `Install-Package WindowsAzure.Storage`.</span></span>

## <a name="how-to-connect-to-a-queue"></a><span data-ttu-id="d4491-121">큐에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="d4491-121">How to connect to a queue</span></span>

<span data-ttu-id="d4491-122">큐에 연결하려면 먼저 연결 문자열을 사용하여 `CloudStorageAccount`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-122">To connect to a queue, you first create a `CloudStorageAccount` with your connection string.</span></span> <span data-ttu-id="d4491-123">그러면 결과 개체가 `CloudQueueClient`를 만들 수 있고, 여기서 다시 `CloudQueue` 인스턴스를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-123">The resulting object can then create a `CloudQueueClient`, which in turn can open a `CloudQueue` instance.</span></span> <span data-ttu-id="d4491-124">다음은 기본 코드 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-124">The basic code flow is shown below.</span></span>

```csharp
CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudQueueClient client = account.CreateCloudQueueClient();

CloudQueue queue = client.GetQueueReference("myqueue");
```

<span data-ttu-id="d4491-125">`CloudQueue`를 만드는 것이 반드시 _실제_ 저장소 큐가 있다는 것을 의미하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-125">Creating a `CloudQueue` doesn't necessarily mean the _actual_ storage queue exists.</span></span> <span data-ttu-id="d4491-126">그러나 이 개체를 사용하여 기존 큐를 만들고, 삭제하고, 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-126">However, you can use this object to create, delete, and check for an existing queue.</span></span> <span data-ttu-id="d4491-127">위에 언급한 대로, 모든 메서드는 동기 및 비동기 버전을 둘 다 지원하지만 여기서는 `Task` 기반 비동기 버전만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-127">As mentioned above, all methods support both synchronous and asynchronous versions, but we will only be using the `Task`-based asynchronous versions.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="d4491-128">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="d4491-128">How to create a queue</span></span>

<span data-ttu-id="d4491-129">큐 만들기에는 공통 패턴을 사용합니다. 항상 송신기 응용 프로그램이 큐 만들기를 담당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-129">You will use a common pattern for queue creation: the sender application should always be responsible for creating the queue.</span></span> <span data-ttu-id="d4491-130">이렇게 하면 응용 프로그램이 보다 자체 포함되고 관리 설정으로부터 더 독립적인 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-130">This keeps your application more self-contained and less dependent on administrative set-up.</span></span> 

<span data-ttu-id="d4491-131">만들기가 간소화되도록 클라이언트 라이브러리는 필요한 경우 큐를 만드는 `CreateIfNotExistsAsync` 메서드를 표시하거나 큐가 이미 있는 경우 `false`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-131">To make the creation simple, the client library exposes a `CreateIfNotExistsAsync` method that will create the queue if necessary, or return `false` if the queue already exists.</span></span> 

<span data-ttu-id="d4491-132">일반적인 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-132">Typical code is shown below.</span></span>

```csharp
CloudQueue queue;
//...

await queue.CreateIfNotExistsAsync();
```

> [!NOTE]
> <span data-ttu-id="d4491-133">이 API를 사용하려면 저장소 계정에 대한 `Write` 또는 `Create` 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-133">You must have `Write` or `Create` permissions for the storage account to use this API.</span></span> <span data-ttu-id="d4491-134">**액세스 키** 보안 모델을 사용하는 경우 항상 true이지만, 큐에 대해 읽기 작업만 허용하는 다른 방법을 사용하여 계정에 대한 권한을 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-134">This is always true if you use the **Access Key** security model, but you can lock down permissions to the account with other approaches that will only allow read operations against the queue.</span></span>

## <a name="how-to-send-a-message"></a><span data-ttu-id="d4491-135">메시지를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="d4491-135">How to send a message</span></span>

<span data-ttu-id="d4491-136">메시지를 보내려면 `CloudQueueMessage` 개체를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-136">To send a message, you instantiate a `CloudQueueMessage` object.</span></span> <span data-ttu-id="d4491-137">해당 클래스에는 데이터를 메시지로 로드하는 오버로드된 생성자가 몇 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-137">The class has a few overloaded constructors that load your data into the message.</span></span> <span data-ttu-id="d4491-138">`string`을 사용하는 생성자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-138">We will use the constructor that takes a `string`.</span></span> <span data-ttu-id="d4491-139">메시지를 만든 후 `CloudQueue` 개체를 사용하여 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-139">After creating the message, you use a `CloudQueue` object to send it.</span></span>

<span data-ttu-id="d4491-140">일반적인 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-140">Here's a typical example:</span></span>

```csharp
var message = new CloudQueueMessage("your message here");

CloudQueue queue;
//...

await queue.AddMessageAsync(message);
```

> [!NOTE]
> <span data-ttu-id="d4491-141">큐의 전체 크기는 최대 500TB일 수 있으나 포함된 개별 메시지의 크기는 최대 64KB(Base64 인코딩을 사용하는 경우 48KB)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-141">While the total queue size can be up to 500 TB, the individual messages in it can only be up to 64 KB in size (48 KB when using Base64 encoding).</span></span> <span data-ttu-id="d4491-142">더 큰 페이로드가 필요한 경우 큐와 Blob을 결합하여 메시지로 해당 URL을 실제 데이터(Blob으로 저장됨)에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-142">If you need a larger payload you can combine queues and blobs – passing the URL to the actual data (stored as a Blob) in the message.</span></span> <span data-ttu-id="d4491-143">이 방식에서는 단일 항목에 대해 최대 200GB를 큐에 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-143">This approach would allow you to enqueue up to 200 GB for a single item.</span></span>

## <a name="how-to-receive-and-delete-a-message"></a><span data-ttu-id="d4491-144">메시지 수신 및 삭제 방법</span><span class="sxs-lookup"><span data-stu-id="d4491-144">How to receive and delete a message</span></span>

<span data-ttu-id="d4491-145">수신기에서 다음 메시지를 받고 처리한 후 처리가 성공하면 해당 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-145">In the receiver, you get the next message, process it, and then delete it after processing succeeds.</span></span> <span data-ttu-id="d4491-146">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-146">Here's a simple example:</span></span>

```C#
CloudQueue queue;
//...

CloudQueueMessage message = await queue.GetMessageAsync();

if (message != null)
{
    // Process the message
    //...

    await queue.DeleteMessageAsync(message);
}
```

<span data-ttu-id="d4491-147">이제 응용 프로그램에 이 새로운 지식을 적용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d4491-147">Let's now apply this new knowledge to our application!</span></span>