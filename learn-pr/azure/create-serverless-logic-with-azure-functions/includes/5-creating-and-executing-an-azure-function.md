<span data-ttu-id="8080f-101">지금까지 함수 앱을 만들었으므로 이제 Azure 함수를 빌드, 구성 및 실행하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-101">Now that we have a function app created, we'll learn how to build, configure, and execute an Azure function.</span></span>

### <a name="triggers"></a><span data-ttu-id="8080f-102">트리거</span><span class="sxs-lookup"><span data-stu-id="8080f-102">Triggers</span></span>

<span data-ttu-id="8080f-103">함수는 이벤트로 구동됩니다. 즉, 이벤트에 대한 응답으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-103">Functions are event driven, which means they run in response to an event.</span></span>

<span data-ttu-id="8080f-104">함수를 시작하는 이벤트 유형을 ‘트리거’라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-104">The type of event that starts the function is called a *trigger*.</span></span> <span data-ttu-id="8080f-105">정확히 하나의 트리거로 함수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-105">You configure a function with exactly one trigger.</span></span>

 <span data-ttu-id="8080f-106">Azure는 다음 서비스에 대한 트리거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-106">Azure supports triggers for the following services.</span></span>


|<span data-ttu-id="8080f-107">서비스</span><span class="sxs-lookup"><span data-stu-id="8080f-107">Service</span></span>  |<span data-ttu-id="8080f-108">트리거 설명</span><span class="sxs-lookup"><span data-stu-id="8080f-108">Trigger description</span></span>  |
|---------|---------|
|<span data-ttu-id="8080f-109">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="8080f-109">Blob storage</span></span>     |  <span data-ttu-id="8080f-110">새 BLOB 또는 업데이트된 BLOB이 검색될 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-110">Start a function when a new or updated blob is detected.</span></span>       |
|<span data-ttu-id="8080f-111">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8080f-111">Cosmos DB</span></span>     |  <span data-ttu-id="8080f-112">삽입 및 업데이트가 검색될 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-112">Start a function when inserts and updates are detected.</span></span>      |
|<span data-ttu-id="8080f-113">Event Grid</span><span class="sxs-lookup"><span data-stu-id="8080f-113">Event Grid</span></span>     |   <span data-ttu-id="8080f-114">Event Grid에서 이벤트를 수신할 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-114">Start a function when an event is received from Event Grid.</span></span>       |
|<span data-ttu-id="8080f-115">HTTP</span><span class="sxs-lookup"><span data-stu-id="8080f-115">HTTP</span></span>     |   <span data-ttu-id="8080f-116">HTTP 요청으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-116">Start a function with an HTTP request.</span></span>      |
|<span data-ttu-id="8080f-117">Microsoft Graph 이벤트</span><span class="sxs-lookup"><span data-stu-id="8080f-117">Microsoft Graph Events</span></span>     |  <span data-ttu-id="8080f-118">Microsoft Graph에서 들어오는 웹후크에 대한 응답으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-118">Start a function in response to an incoming webhook from the Microsoft Graph.</span></span> <span data-ttu-id="8080f-119">이 트리거의 각 인스턴스는 한 가지 Microsoft Graph 리소스 종류에 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-119">Each instance of this trigger can react to one Microsoft Graph resource type.</span></span>       |
|<span data-ttu-id="8080f-120">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="8080f-120">Queue storage</span></span>     |    <span data-ttu-id="8080f-121">큐에서 새 항목을 수신할 때 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-121">Start a function when a new item is received on a queue.</span></span> <span data-ttu-id="8080f-122">큐 메시지는 함수에 입력으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-122">The queue message is provided as input to the function.</span></span>      |
|<span data-ttu-id="8080f-123">Service Bus</span><span class="sxs-lookup"><span data-stu-id="8080f-123">Service Bus</span></span>     |  <span data-ttu-id="8080f-124">Service Bus 큐의 메시지에 대한 응답으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-124">Start a function in response to messages from a Service Bus queue.</span></span>       |
|<span data-ttu-id="8080f-125">타이머</span><span class="sxs-lookup"><span data-stu-id="8080f-125">Timer</span></span>     |  <span data-ttu-id="8080f-126">일정에 따라 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-126">Start a function on a schedule.</span></span>       |
|<span data-ttu-id="8080f-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="8080f-127">Webhooks</span></span>     |  <span data-ttu-id="8080f-128">웹후크 요청으로 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-128">Start a function with a webhook request.</span></span>       |

### <a name="bindings"></a><span data-ttu-id="8080f-129">바인딩</span><span class="sxs-lookup"><span data-stu-id="8080f-129">Bindings</span></span>

<span data-ttu-id="8080f-130">Azure Functions 바인딩은 데이터와 서비스를 함수에 연결하는 선언적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-130">Azure Functions bindings are a declarative way to connect data and services to your function.</span></span> <span data-ttu-id="8080f-131">데이터 원본에 연결하고 연결을 관리하기 위해 함수에서 코드를 작성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-131">You don't have to write code in your function to connect to data sources and manage connections.</span></span> <span data-ttu-id="8080f-132">플랫폼은 복잡성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-132">The platform takes care that complexity for you.</span></span> <span data-ttu-id="8080f-133">바인딩에는 방향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-133">A binding has a direction.</span></span> <span data-ttu-id="8080f-134">코드는 ‘입력’ 바인딩에서 데이터를 읽고 ‘출력’ 바인딩에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-134">Your code reads data from *input* bindings and writes data to *output* bindings.</span></span> <span data-ttu-id="8080f-135">예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-135">Let's look at an example.</span></span>

<span data-ttu-id="8080f-136">Blob Storage에서 데이터를 읽으려면 *blob* 유형의 입력 바인딩을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-136">To read data from Blob storage, you configure an input binding of type *blob*.</span></span> <span data-ttu-id="8080f-137">Queue Storage에 메시지를 쓰려면 *queue* 유형의 출력 바인딩을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-137">To write a message to Queue storage, you configure an output binding of type *queue*.</span></span>

<span data-ttu-id="8080f-138">지원되는 바인딩 및 트리거에 대한 자세한 내용은 [Azure 설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8080f-138">For more information about the supported bindings and triggers, check out the [Azure documentation](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).</span></span>

### <a name="a-sample-trigger-and-binding-functionjson"></a><span data-ttu-id="8080f-139">샘플 트리거 및 바인딩(function.json)</span><span class="sxs-lookup"><span data-stu-id="8080f-139">A sample trigger and binding (function.json)</span></span>

<span data-ttu-id="8080f-140">다음 JSON은 함수에 대한 트리거 및 바인딩의 샘플 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-140">The following JSON is sample definition of a trigger and binding for a function.</span></span>

```javascript
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

<span data-ttu-id="8080f-141">앞에서 언급했듯이 각 바인딩에는 입력 바인딩인지 아니면 출력 바인딩인지를 정의하는 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-141">As we mentioned previously, each binding has a direction that defines whether it is an input or output binding.</span></span> <span data-ttu-id="8080f-142">트리거는 항상 입력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-142">Triggers are always input bindings.</span></span> <span data-ttu-id="8080f-143">이전 샘플은 **myqueue-items**라는 큐에 추가되는 메시지에 의해 트리거되는 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-143">The preceding sample shows a function that is triggered by a message being added to a queue named **myqueue-items**.</span></span> <span data-ttu-id="8080f-144">그런 다음, 함수의 반환 값을 Azure Table Storage의 **outTable** 테이블로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-144">It then sends the return value of the function to the **outTable** table in Azure Table storage.</span></span>

## <a name="creating-a-function-in-the-azure-portal"></a><span data-ttu-id="8080f-145">Azure Portal에서 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="8080f-145">Creating a function in the Azure portal</span></span>

<span data-ttu-id="8080f-146">Azure는 일반 Azure 함수 시나리오에 대해 미리 구성된 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-146">Azure provides pre-configured templates for common Azure function scenarios.</span></span>

### <a name="quickstart-templates"></a><span data-ttu-id="8080f-147">빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="8080f-147">Quickstart templates</span></span>

<span data-ttu-id="8080f-148">Azure 함수를 추가하려면 함수 앱을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-148">To add an Azure function, you must select a function app.</span></span> <span data-ttu-id="8080f-149">함수 앱은 꺾쇠괄호 아이콘 내의 번개 모양으로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-149">The function app can be identified by the lightning bolt within pointy brackets icon.</span></span>  
![리소스 그룹에서 선택된 함수 앱을 보여 주는 스크린샷입니다.](../images/5-function-icon.png)

<span data-ttu-id="8080f-151">첫 번째 Azure 함수를 추가할 때 빠른 시작 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-151">When adding your first Azure function, you are presented with the Quickstart screen.</span></span> <span data-ttu-id="8080f-152">이 화면에서는 트리거 유형 및 프로그래밍 언어를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-152">This screen allows you to choose a trigger type and programming language.</span></span> <span data-ttu-id="8080f-153">그런 다음, 선택 사항에 따라 Azure는 함수 코드 및 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-153">Then, based on your selections, Azure will generate the function code and configuration for you.</span></span> 
 
![함수 빠른 시작](../images/5-quickstart-form.png)

### <a name="function-templates"></a><span data-ttu-id="8080f-155">함수 템플릿</span><span class="sxs-lookup"><span data-stu-id="8080f-155">Function templates</span></span>

<span data-ttu-id="8080f-156">선택할 수 있는 템플릿은 빠른 시작에 표시되는 템플릿으로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-156">The selection of templates is not limited to the templates displayed in the Quickstart.</span></span> <span data-ttu-id="8080f-157">30개가 넘는 템플릿 중에서 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-157">You also have the option of choosing from over 30 different templates.</span></span> <span data-ttu-id="8080f-158">후속 함수를 만들거나 빠른 시작 화면에서 **사용자 지정 함수** 옵션을 선택하여 템플릿 목록 화면에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-158">You can access the template list screen while creating subsequent functions, or by selecting the **Custom function** option on the Quickstart screen.</span></span>  
<span data-ttu-id="8080f-159">![premade 함수를 빠르게 시작하는 데 도움이 되는 Azure Functions 빠른 시작 사용자 인터페이스의 스크린샷입니다.](../images/5-template-list.png)</span><span class="sxs-lookup"><span data-stu-id="8080f-159">![Screenshot of Azure Functions Quickstart user interface to help you get started quickly with a premade function.](../images/5-template-list.png)</span></span>

## <a name="navigating-to-your-function-and-files"></a><span data-ttu-id="8080f-160">함수 및 파일 탐색</span><span class="sxs-lookup"><span data-stu-id="8080f-160">Navigating to your function and files</span></span>

<span data-ttu-id="8080f-161">템플릿에서 함수를 만들면 여러 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-161">When you create a function from a template, several files are created.</span></span> <span data-ttu-id="8080f-162">예를 들어, JavaScript를 사용하는 웹후크+API 빠른 시작을 사용하도록 선택하는 경우 구성 파일, **function.json** 및 소스 코드 파일인 **index.js** 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-162">For example, if you opted to use the Webhook + API Quickstart using JavaScript, the files generated would be a configuration file, **function.json**, and a source code file, **index.js**.</span></span> <span data-ttu-id="8080f-163">함수 앱에서 생성하는 함수는 함수 앱 포털의 함수 메뉴 항목 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-163">The functions you create in a function app appear under the Functions menu item in the function app portal.</span></span>

<span data-ttu-id="8080f-164">함수 앱에서 함수를 선택하면 다음 스크린샷에 설명된 대로 코드 편집기가 열리고 함수에 대한 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-164">When you select a function in your function app, a code editor opens and displays the code for your function, as illustrated in the following screenshot.</span></span>

![함수 개발 속도를 높이기 위해 사용할 수 있는 템플릿 세트를 나열하는 함수 템플릿 선택 인터페이스를 보여 주는 스크린샷입니다.](../images/5-file-navigation.png)

<span data-ttu-id="8080f-166">이전 스크린샷에서 볼 수 있듯이 오른쪽에 **파일 보기**에 대한 탭을 포함하는 플라이아웃 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-166">As you can see in the preceding screenshot,  there's a flyout menu on the right that includes a tab to **View files**.</span></span> <span data-ttu-id="8080f-167">이 탭을 선택하면 함수를 구성하는 파일 구조가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-167">Selecting this tab shows the file structure that makes up your function.</span></span>  

## <a name="execution-options-for-testing-your-azure-function"></a><span data-ttu-id="8080f-168">Azure 함수 테스트를 위한 실행 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-168">Execution options for testing your Azure function</span></span>

<span data-ttu-id="8080f-169">함수가 생성되면 이를 테스트하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-169">Once you've created a function, you'll want to test it.</span></span> <span data-ttu-id="8080f-170">수동 실행, Azure Portal 내에서 테스트 등 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-170">There are a couple of approaches: manual execution and testing from within the Azure portal itself.</span></span>

### <a name="manual-execution-of-a-function"></a><span data-ttu-id="8080f-171">함수의 수동 실행</span><span class="sxs-lookup"><span data-stu-id="8080f-171">Manual execution of a function</span></span>

<span data-ttu-id="8080f-172">구성된 트리거를 수동으로 트리거하여 함수를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-172">You can start a function by manually triggering the configured trigger.</span></span> <span data-ttu-id="8080f-173">예를 들어 HttpTrigger를 사용하는 경우 Postman이나 cURL과 같은 도구를 사용하여 함수 엔드포인트 URL에 대한 HTTP 요청을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-173">For instance, if you are using an HttpTrigger - you can use a tool such as Postman or cURL to initiate an HTTP request to your function endpoint URL.</span></span>  

![<span data-ttu-id="8080f-174">URL 필드에 함수 URL이 입력되어 있고 요청 본문이 샘플 본문으로 채워진 Postman 응용 프로그램 인터페이스의 부분 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-174">Partial screenshot of the Postman application interface with a function URL typed into the url field and the request body filled out with a sample body.</span></span> ](../images/5-postman-execution.png)

<span data-ttu-id="8080f-175">엔드포인트 URL을 가져오려면 왼쪽 탐색에서 HTTP 트리거를 선택한 후 **함수 URL 가져오기**  단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-175">To get endpoint URL, select the HTTP Trigger from the left navigation, and then select the **Get function URL** button.</span></span>  

![함수 앱 포털에서 함수가 선택되어 있고 페이지 맨 위에서 *함수 URL 가져오기* 작업이 선택된 스크린샷입니다.](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a><span data-ttu-id="8080f-177">Azure Portal에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="8080f-177">Testing a function in the Azure portal</span></span>

<span data-ttu-id="8080f-178">포털은 또한 함수를 테스트하는 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-178">The portal also provides a convenient way to test your functions.</span></span> <span data-ttu-id="8080f-179">코드 창의 오른쪽에는 플라이아웃 탭 방식의 탐색 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-179">On the right side of the code window, there is a flyout tabbed navigation menu.</span></span> <span data-ttu-id="8080f-180">이 메뉴에 **테스트** 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-180">This menu contains a **Test** item.</span></span> <span data-ttu-id="8080f-181">메뉴를 확장하고 이 탭을 선택하면 함수를 실행하고 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-181">Expanding the menu and selecting this tab gives you another way to execute your function and view the result.</span></span> <span data-ttu-id="8080f-182">HttpTrigger 시나리오를 사용하여 HTTP 메서드를 설정하고 쿼리 문자열 매개 변수 및 HTTP 헤더를 요청에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-182">In keeping with the HttpTrigger scenario, you can set the HTTP method, and add query string parameters and HTTP headers to the request.</span></span> <span data-ttu-id="8080f-183">또한 추가 시나리오를 테스트하도록 요청 본문을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-183">You may also change the request body to test additional scenarios.</span></span> <span data-ttu-id="8080f-184">다음 예제에서 테스트는 이름이 *name*이라는 하나의 매개 변수가 포함된 요청 본문이 있는 HTTP POST 요청으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-184">In the following example, the test is configured as an HTTP POST request with a request body that has one parameter called *name*.</span></span>
 
![HTTP POST 요청 및 샘플 요청 본문을 표시하는 함수 앱 포털에 있는 테스트 창의 스크린샷입니다.](../images/5-portal-execution.png)

<span data-ttu-id="8080f-187">이 테스트 창에서 **실행**을 클릭하면 결과가 상태 코드와 함께 출력 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-187">When you click **Run** in this test window, the results are displayed in the output window, along with a status code.</span></span> 

## <a name="monitoring-an-azure-function"></a><span data-ttu-id="8080f-188">Azure 함수 모니터링</span><span class="sxs-lookup"><span data-stu-id="8080f-188">Monitoring an Azure function</span></span>

<span data-ttu-id="8080f-189">메시지를 로그하고 함수를 모니터하는 기능은 개발 과정과 프로덕션에서 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-189">The ability to log messages and monitor your functions is critical during development and in production.</span></span> <span data-ttu-id="8080f-190">Azure Portal은 모니터링 대시보드뿐만 아니라 Azure Functions에서 가져온 실행 로그 및 예외를 검토하는 방법도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-190">The Azure portal provides a monitoring dashboard as well as a way to review execution logs and exceptions obtained from your Azure functions.</span></span>

### <a name="log-window"></a><span data-ttu-id="8080f-191">로그 창</span><span class="sxs-lookup"><span data-stu-id="8080f-191">Log window</span></span>

<span data-ttu-id="8080f-192">또한 함수에 로그 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-192">You're also able to add log statements to your function.</span></span> <span data-ttu-id="8080f-193">이 문은 함수의 로그 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-193">These statements will appear in the log window of the function.</span></span> <span data-ttu-id="8080f-194">로그 창은 코드 창의 맨 아래에 있는 탭 방식의 플라이아웃 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-194">The log window is located in a tabbed flyout menu located at the bottom of the code window.</span></span> <span data-ttu-id="8080f-195">다음 JavaScript 코드 조각은 `context.log` 메서드를 사용하여 메시지를 로그하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-195">The following JavaScript code snippet shows how to log a message using the `context.log` method.</span></span>

```javascript
  context.log('Enter your logging statement here');
```  

![Azure Functions 사용자 인터페이스의 코드 편집기 섹션 스크린샷입니다.](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a><span data-ttu-id="8080f-198">오류 및 경고 창</span><span class="sxs-lookup"><span data-stu-id="8080f-198">Errors and warnings window</span></span>

<span data-ttu-id="8080f-199">로그 창과 동일한 플라이아웃 메뉴에서 오류 및 경고 창 탭을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-199">You can locate the errors and warnings window tab in the same flyout menu as the log window.</span></span> <span data-ttu-id="8080f-200">이 창에는 코드 내의 컴파일 오류 및 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-200">This window will show compilation errors and warnings within your code.</span></span> <span data-ttu-id="8080f-201">JavaScript는 동적이며 해석되는 언어이므로 다음 이미지는 C# 함수의 컴파일 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-201">As JavaScript is a dynamic and interpreted language, the following image shows a compilation error in a C# function.</span></span>  

![화면 맨 아래에서 **로그** 창이 강조 표시되어 있는 Azure Functions 사용자 인터페이스의 코드 편집기 섹션 스크린샷입니다.](../images/5-errors-window.png)

### <a name="monitoring-dashboard"></a><span data-ttu-id="8080f-203">모니터링 대시보드</span><span class="sxs-lookup"><span data-stu-id="8080f-203">Monitoring dashboard</span></span>

<span data-ttu-id="8080f-204">함수 앱 탐색 메뉴에서 함수 노드를 확장하면 **모니터** 메뉴 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-204">In the function app navigation menu, once you expand the function node - you will see a **Monitor** menu item.</span></span> <span data-ttu-id="8080f-205">모니터 대시보드는 함수 실행의 기록을 보기 위한 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-205">The monitor dashboard provides a quick way to view the history of function executions.</span></span> <span data-ttu-id="8080f-206">이 보기에는 성공적인 완료 여부는 물론 타임스탬프, 결과 코드, 지속 기간 및 작업 ID도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-206">This view displays the timestamp, result code, duration, and operation ID, as well as if it completed successfully.</span></span> <span data-ttu-id="8080f-207">Azure Application Insights를 통해 데이터가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="8080f-207">The data is populated via Azure Application Insights.</span></span>  

![함수에 대한 성공적인 호출 및 실패한 호출의 목록을 보여 주는 **모니터** 함수 메뉴 항목을 통해 실행된 모니터링 대시보드의 스크린샷입니다.](../images/5-monitor-function.png)
