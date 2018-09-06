<span data-ttu-id="b22e0-101">지금까지 함수 앱을 만들었으므로 이제 함수를 빌드, 구성 및 실행하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-101">Now that we have a function app created, let's look at how to build, configure, and execute a function.</span></span>

### <a name="triggers"></a><span data-ttu-id="b22e0-102">트리거</span><span class="sxs-lookup"><span data-stu-id="b22e0-102">Triggers</span></span>

<span data-ttu-id="b22e0-103">함수는 이벤트로 구동됩니다. 즉, 이벤트에 대한 응답으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-103">Functions are event driven, which means they run in response to an event.</span></span>

<span data-ttu-id="b22e0-104">함수를 시작하는 이벤트 유형을 ‘트리거’라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-104">The type of event that starts the function is called a *trigger*.</span></span> <span data-ttu-id="b22e0-105">정확히 하나의 트리거로 함수를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-105">You must configure a function with exactly one trigger.</span></span>

<span data-ttu-id="b22e0-106">Azure는 다음 서비스에 대한 트리거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-106">Azure supports triggers for the following services.</span></span>

| <span data-ttu-id="b22e0-107">서비스</span><span class="sxs-lookup"><span data-stu-id="b22e0-107">Service</span></span>                 | <span data-ttu-id="b22e0-108">트리거 설명</span><span class="sxs-lookup"><span data-stu-id="b22e0-108">Trigger description</span></span>  |
|-------------------------|---------|
| <span data-ttu-id="b22e0-109">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b22e0-109">Blob storage</span></span>            | <span data-ttu-id="b22e0-110">새 BLOB 또는 업데이트된 BLOB이 검색될 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-110">Start a function when a new or updated blob is detected.</span></span>       |
| <span data-ttu-id="b22e0-111">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b22e0-111">Cosmos DB</span></span>               | <span data-ttu-id="b22e0-112">삽입 및 업데이트가 검색될 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-112">Start a function when inserts and updates are detected.</span></span>      |
| <span data-ttu-id="b22e0-113">Event Grid</span><span class="sxs-lookup"><span data-stu-id="b22e0-113">Event Grid</span></span>              | <span data-ttu-id="b22e0-114">Event Grid에서 이벤트를 수신할 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-114">Start a function when an event is received from Event Grid.</span></span>       |
| <span data-ttu-id="b22e0-115">HTTP</span><span class="sxs-lookup"><span data-stu-id="b22e0-115">HTTP</span></span>                    | <span data-ttu-id="b22e0-116">HTTP 요청으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-116">Start a function with an HTTP request.</span></span>      |
| <span data-ttu-id="b22e0-117">Microsoft Graph 이벤트</span><span class="sxs-lookup"><span data-stu-id="b22e0-117">Microsoft Graph Events</span></span>  | <span data-ttu-id="b22e0-118">Microsoft Graph에서 들어오는 웹후크에 대한 응답으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-118">Start a function in response to an incoming webhook from the Microsoft Graph.</span></span> <span data-ttu-id="b22e0-119">이 트리거의 각 인스턴스는 한 가지 Microsoft Graph 리소스 종류에 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-119">Each instance of this trigger can react to one Microsoft Graph resource type.</span></span>       |
| <span data-ttu-id="b22e0-120">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="b22e0-120">Queue storage</span></span>           | <span data-ttu-id="b22e0-121">큐에서 새 항목을 수신할 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-121">Start a function when a new item is received on a queue.</span></span> <span data-ttu-id="b22e0-122">큐 메시지는 함수에 입력으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-122">The queue message is provided as input to the function.</span></span>      |
| <span data-ttu-id="b22e0-123">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b22e0-123">Service Bus</span></span>             | <span data-ttu-id="b22e0-124">Service Bus 큐의 메시지에 대한 응답으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-124">Start a function in response to messages from a Service Bus queue.</span></span>       |
| <span data-ttu-id="b22e0-125">타이머</span><span class="sxs-lookup"><span data-stu-id="b22e0-125">Timer</span></span>                   | <span data-ttu-id="b22e0-126">일정에 따라 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-126">Start a function on a schedule.</span></span>       |
| <span data-ttu-id="b22e0-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="b22e0-127">Webhooks</span></span>                | <span data-ttu-id="b22e0-128">웹후크 요청으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-128">Start a function with a webhook request.</span></span>       |

### <a name="bindings"></a><span data-ttu-id="b22e0-129">바인딩</span><span class="sxs-lookup"><span data-stu-id="b22e0-129">Bindings</span></span>

<span data-ttu-id="b22e0-130">바인딩은 데이터와 서비스를 함수에 연결하는 선언적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-130">Bindings are a declarative way to connect data and services to your function.</span></span> <span data-ttu-id="b22e0-131">바인딩은 다른 서비스와 통신하는 방법을 알고 있으므로, 데이터 원본에 연결하고 연결을 관리하기 위해 함수에서 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-131">Bindings know how to talk to different services which means you don't have to write code in your function to connect to data sources and manage connections.</span></span> <span data-ttu-id="b22e0-132">플랫폼은 바인딩 코드의 일부로 복잡성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-132">The platform takes care that complexity for you as part of the binding code.</span></span> <span data-ttu-id="b22e0-133">각 바인딩에는 방향이 있습니다. 코드는 ‘입력’ 바인딩에서 데이터를 읽고 ‘출력’ 바인딩에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-133">Each binding has a direction - your code reads data from *input* bindings and writes data to *output* bindings.</span></span> <span data-ttu-id="b22e0-134">각 함수는 함수에 의해 처리된 입력 및 출력 데이터를 관리하기 위해 0개 이상의 바인딩을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-134">Each function can have zero or more bindings to manage the input and output data processed by the function.</span></span>

> [!NOTE]
> <span data-ttu-id="b22e0-135">기술적으로 트리거는 실행을 시작하는 추가 기능이 있는 특수한 형식의 입력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-135">Technically, a trigger is a special type of input binding that has the additional capability of initiating execution.</span></span>

<span data-ttu-id="b22e0-136">Azure는 다양한 저장소 및 메시징 서비스에 연결할 [많은 바인딩](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-136">Azure provides a [large number of bindings](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings) to connect to different storage and messaging services.</span></span>

### <a name="a-sample-binding-definition"></a><span data-ttu-id="b22e0-137">샘플 바인딩 정의</span><span class="sxs-lookup"><span data-stu-id="b22e0-137">A sample binding definition</span></span>

<span data-ttu-id="b22e0-138">입력 바인딩(트리거)과 출력 바인딩을 사용하여 함수를 구성하는 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-138">Let's look at an example of configuring a function with an input binding (trigger) and an output binding.</span></span> <span data-ttu-id="b22e0-139">Blob Storage의 데이터를 읽고, 함수에서 처리한 다음, 큐에 메시지를 기록하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-139">Let's say we want to read data from Blob storage, process it in our function, and then write a message to a queue.</span></span> <span data-ttu-id="b22e0-140">*Blob* 형식의 ‘입력 바인딩’과 *queue* 형식의 ‘출력’ 바인딩을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-140">You would configure an _input binding_ of type *blob* and an _output binding_ of type *queue*.</span></span>

<span data-ttu-id="b22e0-141">바인딩은 Azure Portal에서 정의될 수 있으며, 직접 편집할 수도 있는 JSON 파일로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-141">Bindings can be defined in the Azure portal, and are stored as JSON files which you can also edit directly.</span></span> <span data-ttu-id="b22e0-142">다음 JSON은 함수에 대한 트리거 및 바인딩의 샘플 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-142">The following JSON is sample definition of a trigger and binding for a function.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

<span data-ttu-id="b22e0-143">이 예제는 **myqueue-items**라는 큐에 추가되는 메시지에 의해 트리거되는 함수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-143">This example shows a function that is triggered by a message being added to a queue named **myqueue-items**.</span></span> <span data-ttu-id="b22e0-144">그런 다음, 함수의 반환 값을 Azure Table Storage의 **outTable** 테이블로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-144">It then sends the return value of the function to the **outTable** table in Azure Table storage.</span></span> <span data-ttu-id="b22e0-145">매우 간단한 예제이며, SendGrid 바인딩을 사용하여 출력을 메일로 변경하거나, 이벤트를 Service Bus에 넣어 아키텍처의 다른 구성 요소에 알리거나, 여러 출력 바인딩을 포함하여 데이터를 다양한 서비스에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-145">This is a very simple example, we could change the output to be an email using a SendGrid binding, or put an event onto a Service Bus to notify some other component in our architecture, or even have multiple output bindings to push data to various services.</span></span>

## <a name="creating-a-function-in-the-azure-portal"></a><span data-ttu-id="b22e0-146">Azure Portal에서 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="b22e0-146">Creating a function in the Azure portal</span></span>

<span data-ttu-id="b22e0-147">Azure는 일반적인 시나리오를 위해 여러 가지 미리 만든 함수 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-147">Azure provides several pre-made function templates for common scenarios.</span></span>

### <a name="quickstart-templates"></a><span data-ttu-id="b22e0-148">빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="b22e0-148">Quickstart templates</span></span>

<span data-ttu-id="b22e0-149">첫 번째 함수를 추가할 때 빠른 시작 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-149">When adding your first function, you are presented with the Quickstart screen.</span></span> <span data-ttu-id="b22e0-150">이 화면에서는 트리거 형식(HTTP, Timer 또는 Data) 및 프로그래밍 언어(C#, JavaScript, F# 또는 Java)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-150">This screen allows you to choose a trigger type (HTTP, Timer, or Data) and programming language (C#, JavaScript, F# or Java).</span></span> <span data-ttu-id="b22e0-151">그런 다음, 선택 사항에 따라 Azure는 로그에 수신된 입력 데이터를 표시하기 위해 제공된 일부 샘플 코드를 사용하여 함수 코드 및 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-151">Then, based on your selections, Azure will generate the function code and configuration for you with some sample code provided to display out the input data received in the log.</span></span> 
 
### <a name="custom-function-templates"></a><span data-ttu-id="b22e0-152">사용자 지정 함수 템플릿</span><span class="sxs-lookup"><span data-stu-id="b22e0-152">Custom function templates</span></span>

<span data-ttu-id="b22e0-153">빠른 시작 템플릿을 선택하여 가장 일반적인 시나리오에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-153">The selection of Quickstart templates provides easy access to the most common scenarios.</span></span> <span data-ttu-id="b22e0-154">그러나 Azure는 시작할 수 있는 30개 이상의 추가 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-154">However, Azure provides over 30 additional templates you can start with.</span></span> <span data-ttu-id="b22e0-155">이러한 템플릿은 후속 함수를 만들 때 템플릿 목록에서 선택하거나 빠른 시작 화면에서 **사용자 지정 함수** 옵션을 사용하여 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-155">These can be selected from the template list screen when creating subsequent functions or be selected by using the **Custom function** option on the Quickstart screen.</span></span>

- <span data-ttu-id="b22e0-156">C#, F# 또는 JavaScript를 사용한 HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="b22e0-156">HTTP trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="b22e0-157">C#, F# 또는 JavaScript를 사용한 타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="b22e0-157">Timer trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="b22e0-158">C#, F# 또는 JavaScript를 사용한 큐 트리거</span><span class="sxs-lookup"><span data-stu-id="b22e0-158">Queue trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="b22e0-159">C#, F# 또는 JavaScript를 사용한 Service Bus 큐 트리거</span><span class="sxs-lookup"><span data-stu-id="b22e0-159">Service Bus Queue trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="b22e0-160">C# 또는 JavaScript를 사용한 Cosmos DB 트리거</span><span class="sxs-lookup"><span data-stu-id="b22e0-160">Cosmos DB trigger w/ C# or JavaScript</span></span>
- <span data-ttu-id="b22e0-161">C#, F# 또는 JavaScript를 사용한 IoT Hub(이벤트 허브)</span><span class="sxs-lookup"><span data-stu-id="b22e0-161">IoT Hub (Event Hub) w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="b22e0-162">...기타 등등</span><span class="sxs-lookup"><span data-stu-id="b22e0-162">... and many more</span></span>

## <a name="navigating-to-your-function-and-files"></a><span data-ttu-id="b22e0-163">함수 및 파일 탐색</span><span class="sxs-lookup"><span data-stu-id="b22e0-163">Navigating to your function and files</span></span>

<span data-ttu-id="b22e0-164">템플릿에서 함수를 만들면 여러 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-164">When you create a function from a template, several files are created.</span></span> <span data-ttu-id="b22e0-165">예를 들어, JavaScript를 사용하는 웹후크 + API 빠른 시작을 사용하도록 선택하는 경우 구성 파일인 **function.json** 및 소스 코드 파일인 **index.js**가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-165">For example, if you opted to use the Webhook + API Quickstart using JavaScript, the files generated would be a configuration file, **function.json**, and a source code file, **index.js**.</span></span> <span data-ttu-id="b22e0-166">함수 앱에서 생성하는 함수는 함수 앱 포털의 **함수** 메뉴 항목 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-166">The functions you create in a function app appear under the **Functions** menu item in the function app portal.</span></span>

<span data-ttu-id="b22e0-167">함수 앱에서 함수를 선택하면 다음 스크린샷에 설명된 대로 코드 편집기가 열리고 함수에 대한 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-167">When you select a function in your function app, a code editor opens and displays the code for your function, as illustrated in the following screenshot.</span></span>

![함수 개발 속도를 높이기 위해 사용할 수 있는 템플릿 세트를 나열하는 함수 템플릿 선택 인터페이스입니다.](../media-draft/4-file-navigation.png)

<span data-ttu-id="b22e0-169">이전 스크린샷에서 볼 수 있듯이 오른쪽에 **파일 보기**에 대한 탭을 포함하는 플라이아웃 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-169">As you can see in the preceding screenshot,  there's a flyout menu on the right that includes a tab to **View files**.</span></span> <span data-ttu-id="b22e0-170">이 탭을 선택하면 함수를 구성하는 파일 구조가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-170">Selecting this tab shows the file structure that makes up your function.</span></span>  

## <a name="testing-your-azure-function"></a><span data-ttu-id="b22e0-171">Azure 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="b22e0-171">Testing your Azure function</span></span>

<span data-ttu-id="b22e0-172">함수가 생성되면 이를 테스트하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-172">Once you've created a function, you'll want to test it.</span></span> <span data-ttu-id="b22e0-173">수동 실행, Azure Portal 내에서 테스트 등 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-173">There are a couple of approaches: manual execution and testing from within the Azure portal itself.</span></span>

### <a name="manual-execution"></a><span data-ttu-id="b22e0-174">수동 실행</span><span class="sxs-lookup"><span data-stu-id="b22e0-174">Manual execution</span></span>

<span data-ttu-id="b22e0-175">구성된 트리거를 수동으로 트리거하여 함수를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-175">You can start a function by manually triggering the configured trigger.</span></span> <span data-ttu-id="b22e0-176">예를 들어 HTTP 트리거를 사용하는 경우 Postman이나 cURL과 같은 도구를 사용하여, HTTP 트리거 정의에서 사용할 수 있는(**함수 URL 가져오기**) 함수 엔드포인트 URL에 대한 HTTP 요청을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-176">For instance, if you are using an HTTP trigger - you can use a tool such as Postman or cURL to initiate an HTTP request to your function endpoint URL which is available from the HTTP trigger definition (**Get function URL**).</span></span>  

### <a name="testing-in-the-azure-portal"></a><span data-ttu-id="b22e0-177">Azure Portal에서 테스트</span><span class="sxs-lookup"><span data-stu-id="b22e0-177">Testing in the Azure portal</span></span>

<span data-ttu-id="b22e0-178">포털은 또한 함수를 테스트하는 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-178">The portal also provides a convenient way to test your functions.</span></span> <span data-ttu-id="b22e0-179">코드 창의 오른쪽에는 플라이아웃 탭 방식의 탐색 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-179">On the right side of the code window, there is a flyout tabbed navigation menu.</span></span> <span data-ttu-id="b22e0-180">이 메뉴에 **테스트** 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-180">This menu contains a **Test** item.</span></span> <span data-ttu-id="b22e0-181">메뉴를 확장하고 이 탭을 선택하면 함수를 실행하고 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-181">Expanding the menu and selecting this tab gives you another way to execute your function and view the result.</span></span> <span data-ttu-id="b22e0-182">이 테스트 창에서 **실행**을 클릭하면 결과가 상태 코드와 함께 출력 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-182">When you click **Run** in this test window, the results are displayed in the output window, along with a status code.</span></span> 

## <a name="monitoring-dashboard"></a><span data-ttu-id="b22e0-183">모니터링 대시보드</span><span class="sxs-lookup"><span data-stu-id="b22e0-183">Monitoring dashboard</span></span>

<span data-ttu-id="b22e0-184">함수를 모니터링하는 기능은 개발 과정과 프로덕션에서 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-184">The ability to monitor your functions is critical during development and in production.</span></span> <span data-ttu-id="b22e0-185">Application Insights 통합을 켜면 Azure Portal에서 모니터링 대시보드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-185">The Azure portal provides a monitoring dashboard available if you turn on the Application Insights integration.</span></span> <span data-ttu-id="b22e0-186">함수 앱 탐색 메뉴에서 함수 노드를 확장하면 **모니터** 메뉴 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-186">In the function app navigation menu, once you expand the function node you'll see a **Monitor** menu item.</span></span> <span data-ttu-id="b22e0-187">이 모니터 대시보드는 함수 실행의 기록을 보고 Application Insights에 의해 채워진 타임스탬프, 결과 코드, 기간 및 작업 ID를 표시하는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-187">This monitor dashboard provides a quick way to view the history of function executions and displays the timestamp, result code, duration, and operation ID populated by Application Insights.</span></span>

![함수에 대한 성공적인 호출 및 실패한 호출의 목록을 보여 주는 **모니터** 함수 메뉴 항목을 통해 시작된 모니터링 대시보드의 스크린샷입니다.](../media-draft/4-monitor-function.png)

## <a name="streaming-log-window"></a><span data-ttu-id="b22e0-189">스트리밍 로그 창</span><span class="sxs-lookup"><span data-stu-id="b22e0-189">Streaming log window</span></span>

<span data-ttu-id="b22e0-190">또한 Azure Portal에서 디버그하도록 함수에 로깅 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-190">You're also able to add logging statements to your function for debugging in the Azure portal.</span></span> <span data-ttu-id="b22e0-191">각 언어에 대한 호출된 메서드는 코드 창의 맨 아래에 있는 탭 플라이아웃 메뉴에 있는 로그 창에 정보를 기록하는 데 사용할 수 있는 “로깅” 개체에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-191">The called methods for each language are passed a "logging" object which may be used to log information to the log window located in a tabbed flyout menu located at the bottom of the code window.</span></span> 

<span data-ttu-id="b22e0-192">다음 JavaScript 코드 조각은 `context.log` 메서드를 사용하여 메시지를 로그하는 방법을 보여 줍니다(`context` 개체가 처리기에 전달됨).</span><span class="sxs-lookup"><span data-stu-id="b22e0-192">The following JavaScript code snippet shows how to log a message using the `context.log` method (the `context` object is passed to the handler).</span></span>

```javascript
  context.log('Enter your logging statement here');
```  

<span data-ttu-id="b22e0-193">`log.Info` 메서드를 사용하여 C#에서 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-193">We could the same thing in C# using the `log.Info` method.</span></span> <span data-ttu-id="b22e0-194">이 경우 `log` 개체는 함수를 처리하는 C# 메서드 처리로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-194">In this case, the `log` object is passed ot the C# method processing the function.</span></span>

```csharp
  log.Info("Enter your logging statement here");
```

### <a name="errors-and-warnings-window"></a><span data-ttu-id="b22e0-195">오류 및 경고 창</span><span class="sxs-lookup"><span data-stu-id="b22e0-195">Errors and warnings window</span></span>

<span data-ttu-id="b22e0-196">로그 창과 동일한 플라이아웃 메뉴에서 오류 및 경고 창 탭을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-196">You can locate the errors and warnings window tab in the same flyout menu as the log window.</span></span> <span data-ttu-id="b22e0-197">이 창에는 코드 내의 컴파일 오류 및 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b22e0-197">This window will show compilation errors and warnings within your code.</span></span>

