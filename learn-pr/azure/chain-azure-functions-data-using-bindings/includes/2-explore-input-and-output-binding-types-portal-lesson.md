<span data-ttu-id="1d37f-101">데이터 액세스 및 처리는 많은 소프트웨어 솔루션의 핵심 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-101">Accessing and processing data are key tasks in many software solutions.</span></span> <span data-ttu-id="1d37f-102">다음과 같은 몇 가지 시나리오를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-102">Consider some of these scenarios:</span></span>

* <span data-ttu-id="1d37f-103">들어오는 데이터를 Blob 저장소에서 Azure Cosmos DB로 이동하는 방법을 구현하도록 요청 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-103">You've been asked to implement a way to move incoming data from Blob storage to Azure Cosmos DB.</span></span>
* <span data-ttu-id="1d37f-104">엔터프라이즈의 다른 구성 요소에서 처리하기 위해 들어오는 메시지를 큐에 게시하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-104">You want to post incoming messages to a queue for processing by another component in your enterprise.</span></span>
* <span data-ttu-id="1d37f-105">서비스에서는 큐의 게이머 점수를 포착하고 온라인 스코어보드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-105">Your service needs to grab gamer scores from a queue and update an online scoreboard.</span></span>

<span data-ttu-id="1d37f-106">이 예는 모두 데이터 이동과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-106">All of these examples are about moving data.</span></span> <span data-ttu-id="1d37f-107">데이터 원본 및 대상은 시나리오마다 다르지만 패턴은 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-107">The data source and destinations differ from scenario to scenario, but the pattern is similar.</span></span> <span data-ttu-id="1d37f-108">데이터 원본에 연결하고 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-108">You connect to a data source, and you read and write data.</span></span> <span data-ttu-id="1d37f-109">Azure Functions은 바인딩을 사용하여 데이터와 서비스를 통합할 수 있게 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-109">Azure Functions helps you integrate with data and services by using bindings.</span></span> 

## <a name="what-is-a-binding"></a><span data-ttu-id="1d37f-110">바인딩이란?</span><span class="sxs-lookup"><span data-stu-id="1d37f-110">What is a binding?</span></span>

<span data-ttu-id="1d37f-111">Azure Functions에서 바인딩은 코드 내에서 데이터에 연결하기 위한 선언적 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-111">In Azure Functions, bindings provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="1d37f-112">이렇게 하면 쉽게 함수에서 데이터 스트림을 일관되게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-112">They make it easier to integrate with data streams consistently in a function.</span></span> <span data-ttu-id="1d37f-113">다른 데이터 요소에 대한 액세스를 제공하는 여러 바인딩이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-113">You can have multiple bindings providing access to different data elements.</span></span> <span data-ttu-id="1d37f-114">이 바인딩은 특정한 연결 논리(예: 데이터베이스 연결 또는 웹 API 인터페이스)를 코딩하지 않고도 데이터 소스에 연결할 수 있기에 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-114">This is powerful because you can connect to your data sources without having to code specific connection logic (like database connections or web API interfaces).</span></span>

### <a name="types-of-bindings"></a><span data-ttu-id="1d37f-115">바인딩 형식</span><span class="sxs-lookup"><span data-stu-id="1d37f-115">Types of bindings</span></span>

<span data-ttu-id="1d37f-116">함수와 함께 사용할 수 있는 두 형식의 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-116">There are two kinds of bindings you can use with functions:</span></span>

1. <span data-ttu-id="1d37f-117">**입력 바인딩** 입력 바인딩은 데이터 **원본**에 대한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-117">**Input binding** An input binding is a connection to a data **source**.</span></span> <span data-ttu-id="1d37f-118">해당 함수는 이러한 입력에서 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-118">Our function can read data from these inputs.</span></span>

1. <span data-ttu-id="1d37f-119">**출력 바인딩** 출력 바인딩은 데이터 **대상**에 대한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-119">**Output binding** An output binding is a connection to a data **destination**.</span></span> <span data-ttu-id="1d37f-120">해당 함수는 이러한 대상에 데이터를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-120">Our function can write data to these destinations.</span></span>

<span data-ttu-id="1d37f-121">트리거도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-121">There are also triggers.</span></span> <span data-ttu-id="1d37f-122">트리거는 함수를 실행하게 하는 특별한 형식의 입력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-122">Triggers are special types of input bindings that cause a function to execute.</span></span> <span data-ttu-id="1d37f-123">예를 들어 Azure Event Grid 알림은 트리거로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-123">For example, an Azure Event Grid notification can be configured as a trigger.</span></span> <span data-ttu-id="1d37f-124">이벤트가 발생하면 함수가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-124">When an event occurs, the function will run.</span></span>

### <a name="types-of-supported-bindings"></a><span data-ttu-id="1d37f-125">지원되는 바인딩 형식</span><span class="sxs-lookup"><span data-stu-id="1d37f-125">Types of supported bindings</span></span>

<span data-ttu-id="1d37f-126">바인딩 *형식*은 데이터를 읽거나 보내는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-126">The *type* of binding defines where we are reading or sending data.</span></span> <span data-ttu-id="1d37f-127">웹 요청에 대응하는 바인딩 및 다양한 Azure 서비스 및 타사 서비스와 직접 상호 작용하는 여러 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-127">There is a binding to respond to web requests and a large selection of bindings to interact directly with various Azure services as well as third-party services.</span></span>

<span data-ttu-id="1d37f-128">바인딩 형식은 입력, 출력 또는 둘 다로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-128">A binding type can be used as an input, an output or both.</span></span> <span data-ttu-id="1d37f-129">예를 들어 함수는 Azure Blob Storage 출력 바인딩에 작성할 수 있지만 Blob 저장소 업데이트는 다른 함수를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-129">For example, a function can write to Azure Blob Storage output binding, but a blob storage update could trigger another function.</span></span>

<span data-ttu-id="1d37f-130">몇몇 일반적인 바인딩 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-130">Some common binding types are listed below:</span></span>
- <span data-ttu-id="1d37f-131">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1d37f-131">Blob Storage</span></span>
- <span data-ttu-id="1d37f-132">Azure Service Bus 큐</span><span class="sxs-lookup"><span data-stu-id="1d37f-132">Azure Service Bus Queues</span></span>
- <span data-ttu-id="1d37f-133">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1d37f-133">Azure Cosmos DB</span></span>
- <span data-ttu-id="1d37f-134">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1d37f-134">Azure Event Hubs</span></span>
- <span data-ttu-id="1d37f-135">외부 파일</span><span class="sxs-lookup"><span data-stu-id="1d37f-135">External Files</span></span>
- <span data-ttu-id="1d37f-136">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="1d37f-136">External Tables</span></span>
- <span data-ttu-id="1d37f-137">HTTP 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="1d37f-137">HTTP endpoints</span></span>

<span data-ttu-id="1d37f-138">이러한 형식은 샘플일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-138">These types are just a sample.</span></span> <span data-ttu-id="1d37f-139">이외에도 플러스 함수에는 더 많은 바인딩을 추가하는 확장성 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-139">There are more, plus functions have an extensibility model to add more bindings.</span></span>

### <a name="binding-properties"></a><span data-ttu-id="1d37f-140">바인딩 속성</span><span class="sxs-lookup"><span data-stu-id="1d37f-140">Binding properties</span></span>

<span data-ttu-id="1d37f-141">모든 바인딩에 세 가지 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-141">Three properties are required in all bindings.</span></span> <span data-ttu-id="1d37f-142">사용하는 저장소 및 바인딩의 형식에 따라 추가적인 속성을 제공해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-142">You may have to supply additional properties based on the type of binding and storage you are using.</span></span>

1. <span data-ttu-id="1d37f-143">**이름**은 데이터에 액세스하는 데 사용하는 함수 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-143">**Name** Defines the function parameter through which you access the data.</span></span> <span data-ttu-id="1d37f-144">예를 들어 큐 입력 바인딩에서 이 이름은 큐 메시지 콘텐츠를 수신하는 함수 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-144">For example, in a queue input binding, this is the name of the function parameter that receives the queue message content.</span></span> 

1. <span data-ttu-id="1d37f-145">**형식**은 바인딩 형식, 즉 상호 작용하려는 데이터나 서비스의 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-145">**Type** Identifies the type of binding, i.e., the type of data or service we want to interact with.</span></span>

1. <span data-ttu-id="1d37f-146">**방향**은 데이터가 흐르는 방향을 나타냅니다. 즉 입력 또는 출력 바인딩입니까?</span><span class="sxs-lookup"><span data-stu-id="1d37f-146">**Direction** Indicates the direction data is flowing, i.e., is it an input or output binding?</span></span>

<span data-ttu-id="1d37f-147">또한 대부분의 바인딩 형식은 네 번째 속성도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-147">Additionally, most binding types also need a fourth property:</span></span> 

4. <span data-ttu-id="1d37f-148">**연결**은 연결 문자열을 포함하는 앱 설정 키의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-148">**Connection** Provides the name of an app setting key that contains the connection string.</span></span> <span data-ttu-id="1d37f-149">바인딩은 앱 설정에 저장된 연결 문자열을 사용하여 함수 코드의 비밀을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-149">Bindings use connection strings stored in app settings to keep secrets out of the function code.</span></span> <span data-ttu-id="1d37f-150">이렇게 하면 코드를 더욱 구성 가능하고 안전하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-150">This makes your code more configurable and secure.</span></span>

## <a name="create-a-binding"></a><span data-ttu-id="1d37f-151">바인딩 만들기</span><span class="sxs-lookup"><span data-stu-id="1d37f-151">Create a binding</span></span>

<span data-ttu-id="1d37f-152">바인딩은 JSON에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-152">Bindings are defined in JSON.</span></span> <span data-ttu-id="1d37f-153">바인딩은 함수의 구성 파일에서 구성되며 이 파일은 *function.json*이라고 하며 함수 코드와 동일한 폴더에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-153">A binding is configured in your function's configuration file, which is named *function.json* and lives in the same folder as your function code.</span></span>

 <span data-ttu-id="1d37f-154">*입력 바인딩* 예제를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-154">Let's examine a sample *input binding*:</span></span>

```json
    ...
    {
      "name": "headshotBlob",
      "type": "blob",
      "path": "thumbnail-images/{filename}",
      "connection": "HeadshotStorageConnection",
      "direction": "in"
    },
    ...
```

<span data-ttu-id="1d37f-155">이 바인딩을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-155">To create this binding, we:</span></span>

1. <span data-ttu-id="1d37f-156">*function.json* 파일에서 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-156">Create a binding in our *function.json* file.</span></span>

1. <span data-ttu-id="1d37f-157">`name` 변수의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-157">Provide the value for the `name` variable.</span></span> <span data-ttu-id="1d37f-158">이 예제에서는 변수가 Blob 데이터를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-158">In this example, the variable holds the blob data.</span></span>

1. <span data-ttu-id="1d37f-159">`type` 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-159">Provide the storage `type`.</span></span> <span data-ttu-id="1d37f-160">앞의 예제에서는 Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-160">In the preceding example, we are using Blob storage.</span></span>

1. <span data-ttu-id="1d37f-161">컨테이너 및 컨테이너에 포함되는 항목 이름을 지정하는 `path`를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-161">Provide the `path`, which specifies the container and the item name that goes in it.</span></span> <span data-ttu-id="1d37f-162">`path` 속성은 Blob에 대해 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-162">The `path` property is required for blobs.</span></span>

1. <span data-ttu-id="1d37f-163">응용 프로그램의 설정 파일에서 정의한 `connection` 문자열 설정 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-163">Provide the `connection` string setting name defined in the application's settings file.</span></span> <span data-ttu-id="1d37f-164">이 이름은 저장소 계정에 연결하기 위한 연결 문자열을 찾는 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-164">It's used as a key to find the connection string to connect to your storage account.</span></span>

1. <span data-ttu-id="1d37f-165">`direction`을 `in`으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-165">Define the `direction` as `in`.</span></span> <span data-ttu-id="1d37f-166">Blob에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-166">It reads data from the blob.</span></span>

<span data-ttu-id="1d37f-167">바인딩은 함수에서 데이터 연결에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-167">Bindings are used to connect to data in your function.</span></span> <span data-ttu-id="1d37f-168">이 예에서는 함수에서 썸네일로 처리되는 사용자 이미지에 연결하는 입력 바인딩을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="1d37f-168">In this example, we used an input binding to connect user images to be processed by our function as thumbnails.</span></span>
