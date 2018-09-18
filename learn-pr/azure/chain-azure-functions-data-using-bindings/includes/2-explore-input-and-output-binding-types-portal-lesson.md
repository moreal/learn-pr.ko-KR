<span data-ttu-id="af0ae-101">데이터 액세스 및 처리는 많은 소프트웨어 솔루션의 핵심 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-101">Accessing and processing data are key tasks in many software solutions.</span></span> <span data-ttu-id="af0ae-102">다음과 같은 몇 가지 시나리오를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-102">Consider some of these scenarios:</span></span>

* <span data-ttu-id="af0ae-103">들어오는 데이터를 Blob 저장소에서 Azure Cosmos DB로 이동하는 방법을 구현하도록 요청 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-103">You've been asked to implement a way to move incoming data from blob storage to Azure Cosmos DB.</span></span>
* <span data-ttu-id="af0ae-104">엔터프라이즈의 다른 구성 요소에서 처리하기 위해 들어오는 데이터를 큐에 게시하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-104">You want to post incoming messages to a queue for processing by another component in your enterprise.</span></span>
* <span data-ttu-id="af0ae-105">서비스에서는 큐의 게이머 점수를 포착하고 온라인 스코어보드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-105">Your service needs to grab gamer scores from a queue and update an online scoreboard.</span></span>

<span data-ttu-id="af0ae-106">이 예는 모두 데이터 이동과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-106">All of these examples are about moving data.</span></span> <span data-ttu-id="af0ae-107">데이터 원본 및 대상은 시나리오마다 다르지만 패턴은 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-107">The data source and destinations differ from scenario to scenario, but the pattern is similar.</span></span> <span data-ttu-id="af0ae-108">데이터 원본에 연결하고 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-108">You connect to a data source, you read and write data.</span></span> <span data-ttu-id="af0ae-109">Azure Functions를 사용하면 바인딩으로 데이터와 서비스를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-109">Azure Functions helps you integrate with data and services using bindings.</span></span> 

## <a name="what-is-a-binding"></a><span data-ttu-id="af0ae-110">바인딩이란?</span><span class="sxs-lookup"><span data-stu-id="af0ae-110">What is a binding?</span></span>

<span data-ttu-id="af0ae-111">함수에서 바인딩은 코드에서 데이터에 연결하기 위한 선언적 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-111">In functions, bindings provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="af0ae-112">이렇게 하면 쉽게 함수에서 데이터 스트림을 일관되게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-112">They make it easier to integrate with data streams consistently in a function.</span></span> <span data-ttu-id="af0ae-113">트리거는 함수가 호출되는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-113">A trigger defines how a function is invoked.</span></span> <span data-ttu-id="af0ae-114">트리거는 하나만 가능하지만 함수에서 바인딩은 여럿일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-114">You can only have one trigger, but you can have multiple bindings in a function.</span></span> <span data-ttu-id="af0ae-115">예를 들어 *연결 문자열*처럼, 값을 하드 코드하지 않고도 데이터 원본에 연결할 수 있으므로 매우 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-115">This is powerful because you can connect to your data sources without having to hard code the values, like for instance, the *connection string*.</span></span>

### <a name="two-kinds-of-bindings"></a><span data-ttu-id="af0ae-116">두 가지 바인딩</span><span class="sxs-lookup"><span data-stu-id="af0ae-116">Two kinds of bindings</span></span>

<span data-ttu-id="af0ae-117">두 종류의 바인딩을 함수에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-117">There are two kinds of bindings you can use for your functions:</span></span>

1. <span data-ttu-id="af0ae-118">**입력 바인딩** 입력 바인딩은 데이터 **원본**에 대한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-118">**Input binding** An input binding is a connection to a data **source**.</span></span> <span data-ttu-id="af0ae-119">이 함수는 이 원본에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-119">Our function reads data from this source.</span></span>

1. <span data-ttu-id="af0ae-120">**출력 바인딩** 출력 바인딩은 데이터 **대상**에 대한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-120">**Output binding** An output binding is a connection to a data **destination**.</span></span> <span data-ttu-id="af0ae-121">함수는 이 대상에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-121">Our function writes data to this destination.</span></span>

### <a name="types-of-supported-bindings"></a><span data-ttu-id="af0ae-122">지원되는 바인딩 형식</span><span class="sxs-lookup"><span data-stu-id="af0ae-122">Types of supported bindings</span></span>

<span data-ttu-id="af0ae-123">바인딩 *형식*은 읽거나 보내는 데이터의 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-123">The *type* of binding defines where we are reading or sending data.</span></span> <span data-ttu-id="af0ae-124">웹 요청에 응답하는 바인딩과, 저장 장치와 상호 작용하는 많은 바인딩 선택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-124">There is a binding to respond to web requests and a large selection of bindings to interact with storage.</span></span>

<span data-ttu-id="af0ae-125">자주 사용되는 바인딩 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-125">Here's a list of commonly used bindings:</span></span>
- <span data-ttu-id="af0ae-126">Blob</span><span class="sxs-lookup"><span data-stu-id="af0ae-126">Blob</span></span>
- <span data-ttu-id="af0ae-127">큐</span><span class="sxs-lookup"><span data-stu-id="af0ae-127">Queue</span></span>
- <span data-ttu-id="af0ae-128">CosmosDB</span><span class="sxs-lookup"><span data-stu-id="af0ae-128">CosmosDB</span></span>
- <span data-ttu-id="af0ae-129">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="af0ae-129">Event Hubs</span></span>
- <span data-ttu-id="af0ae-130">외부 파일</span><span class="sxs-lookup"><span data-stu-id="af0ae-130">External Files</span></span>
- <span data-ttu-id="af0ae-131">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="af0ae-131">External Tables</span></span>
- <span data-ttu-id="af0ae-132">HTTP</span><span class="sxs-lookup"><span data-stu-id="af0ae-132">HTTP</span></span>

### <a name="binding-properties"></a><span data-ttu-id="af0ae-133">바인딩 속성</span><span class="sxs-lookup"><span data-stu-id="af0ae-133">Binding properties</span></span>

<span data-ttu-id="af0ae-134">모든 바인딩에는 4가지 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-134">There are four properties that are required in all bindings.</span></span> <span data-ttu-id="af0ae-135">바인딩 및/또는 사용하는 저장소의 형식에 따라 추가적인 속성을 제공해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-135">You may have to supply additional properties based on the type of binding and/or storage you are using.</span></span>

- <span data-ttu-id="af0ae-136">**이름** `name` 속성은 데이터를 액세스하는 데 사용하는 함수 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-136">**Name** The `name` property defines the function parameter through which you access the data.</span></span> <span data-ttu-id="af0ae-137">예를 들어 큐 입력 바인딩에서는 큐 메시지 콘텐츠를 수신하는 함수 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-137">For example, in a queue input binding, this is the name of the function parameter that receives the queue message content.</span></span> 

- <span data-ttu-id="af0ae-138">**형식** `type` 속성은 바인딩 형식, 즉 상호 작용하려는 데이터나 서비스의 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-138">**Type** The `type` property identifies the type of binding, i.e., the type of data or service we want to interact with.</span></span>

- <span data-ttu-id="af0ae-139">**방향** `direction` 속성은 데이터가 흐르는 방향을 식별합니다. 즉 입력 또는 출력 바인딩이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-139">**Direction** The `direction` property identifies the direction data is flowing ie. is it an input or output binding?</span></span>

- <span data-ttu-id="af0ae-140">**연결** `connection` 속성은 연결 문자열 자체가 아닌 연결 문자열을 포함하는 앱 설정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-140">**Connection** The `connection` property is the name of an app setting that contains the connection string, not the connection string itself.</span></span> <span data-ttu-id="af0ae-141">바인딩은 function.json에 서비스 비밀이 포함되지 않은 모범 사례를 실행하기 위해 앱 설정에 저장된 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-141">Bindings use connection strings stored in app settings to enforce the best practice that function.json does not contain service secrets.</span></span>

## <a name="create-a-binding"></a><span data-ttu-id="af0ae-142">바인딩 만들기</span><span class="sxs-lookup"><span data-stu-id="af0ae-142">Create a binding</span></span>

<span data-ttu-id="af0ae-143">바인딩은 JSON에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-143">Bindings are defined in JSON.</span></span> <span data-ttu-id="af0ae-144">바인딩은 함수의 구성 파일에서 구성되며 이름이 `function.json`이고 함수 코드와 동일한 폴더에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-144">A binding is configured in your function's configuration file, which is named `function.json` and lives in the same folder as your function code.</span></span>

 <span data-ttu-id="af0ae-145">*입력 바인딩* 예제를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-145">Let's examine a sample of an *input binding*:</span></span>

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

<span data-ttu-id="af0ae-146">이 바인딩을 만들려면</span><span class="sxs-lookup"><span data-stu-id="af0ae-146">To create this binding we:</span></span>

1. <span data-ttu-id="af0ae-147">`function.json` 파일에서 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-147">Create a binding in our `function.json` file.</span></span>

1. <span data-ttu-id="af0ae-148">`name` 변수의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-148">Provide the value for the `name` variable.</span></span> <span data-ttu-id="af0ae-149">이 예제에서는 변수가 Blob 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-149">In this example, the variable will hold the blob data.</span></span>

1. <span data-ttu-id="af0ae-150">`type` 저장소를 제공합니다. 앞의 예제에서는 Blob 저장소 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-150">Provide the storage `type`, in the preceding example, we are using Blob storage.</span></span>

1. <span data-ttu-id="af0ae-151">컨테이너와, 그 안에 들어갈 항목 이름을 지정하는 `path`를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-151">Provide the `path`, which specifies the container and the item name which goes in it.</span></span> <span data-ttu-id="af0ae-152">`path` 속성은 Blob에 대해 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-152">The `path` property is required for Blobs.</span></span>

1. <span data-ttu-id="af0ae-153">응용 프로그램의 설정 파일에서 정의한 `connection` 문자열 설정 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-153">Provide the `connection` string setting name defined in the application's settings file.</span></span> <span data-ttu-id="af0ae-154">저장소 연결을 위한 연결 문자열을 찾는 조회로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-154">It's used as a lookup to find the connection string to connect to your storage.</span></span>

1. <span data-ttu-id="af0ae-155">`direction`을 `in`으로 정의하면 Blob에서 데이터를 읽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-155">Define the `direction` as `in`, it will read data from the Blob.</span></span>

<span data-ttu-id="af0ae-156">바인딩은 함수에서 데이터 연결에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-156">Bindings are used to connect to data into your function.</span></span> <span data-ttu-id="af0ae-157">여기서 살펴본 예에서는 함수에서 축소판 그림으로 처리되는 사용자 이미지를 연결하는 입력 바인딩을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="af0ae-157">In the example we looked at, we used an input binding to connect user images to be processed by our function as thumbnails.</span></span>