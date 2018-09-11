<span data-ttu-id="281df-101">지금까지 함수 앱을 만들었으므로 이제 Azure 함수를 빌드, 구성 및 실행하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-101">Now that we have a function app created, we'll learn how to build, configure and execute an Azure function.</span></span>

### <a name="triggers"></a><span data-ttu-id="281df-102">트리거</span><span class="sxs-lookup"><span data-stu-id="281df-102">Triggers</span></span>
<span data-ttu-id="281df-103">Azure 함수는 이벤트 기반이며, HTTP 요청 또는 큐에 메시지 추가 등의 이벤트에 응답하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-103">Azure functions are event driven and execute in response to an event, such as receiving an HTTP request or a message being added to a queue.</span></span> 

<span data-ttu-id="281df-104">함수를 시작하는 이벤트 유형을 트리거라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-104">The type of event that initiates the function is called a trigger.</span></span> <span data-ttu-id="281df-105">Azure 함수를 사용하려면 하나 이상의 트리거를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-105">Azure functions require at least one trigger to be configured.</span></span> <span data-ttu-id="281df-106">이것 외에는 함수를 실행하는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-106">Otherwise we'd have no way of running the function.</span></span>

 <span data-ttu-id="281df-107">Azure는 다음을 포함한 광범위한 트리거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-107">Azure supports a wide range of triggers, including:</span></span>
* <span data-ttu-id="281df-108">HTTPTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-108">HTTPTrigger</span></span>
* <span data-ttu-id="281df-109">TimerTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-109">TimerTrigger</span></span>
* <span data-ttu-id="281df-110">GitHub 웹후크</span><span class="sxs-lookup"><span data-stu-id="281df-110">GitHub webhook</span></span>
* <span data-ttu-id="281df-111">CosmosDBTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-111">CosmosDBTrigger</span></span>
* <span data-ttu-id="281df-112">BlobTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-112">BlobTrigger</span></span>
* <span data-ttu-id="281df-113">QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-113">QueueTrigger</span></span>
* <span data-ttu-id="281df-114">EventHubTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-114">EventHubTrigger</span></span>
* <span data-ttu-id="281df-115">ServiceBusQueueTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-115">ServiceBusQueueTrigger</span></span>
* <span data-ttu-id="281df-116">ServiceBusTopicTrigger</span><span class="sxs-lookup"><span data-stu-id="281df-116">ServiceBusTopicTrigger</span></span>

### <a name="bindings"></a><span data-ttu-id="281df-117">바인딩</span><span class="sxs-lookup"><span data-stu-id="281df-117">Bindings</span></span>
<span data-ttu-id="281df-118">Azure 함수 바인딩은 데이터를 함수에 프로그래밍 방식으로 연결하는 선언적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="281df-118">Azure function bindings are a declarative way to connect to data to your function programmatically.</span></span>

<span data-ttu-id="281df-119">바인딩은 데이터 서비스에 대한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="281df-119">Bindings are the connection to your data services.</span></span> <span data-ttu-id="281df-120">0, 1 또는 그 이상의 바인딩이 있는 Azure 함수를 사용하면 여러 데이터 원본에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-120">An Azure function with zero, one or more bindings allows you to access multiple data sources.</span></span> <span data-ttu-id="281df-121">이를 입력 또는 출력 바인딩으로 정의하거나 읽기 또는 쓰기 바인딩으로 생각할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-121">You also define them as input or output bindings, or you can think of them as read or write bindings.</span></span>

<span data-ttu-id="281df-122">Blob이 큐에 추가될 때 함수를 시작하는 QueueTrigger가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-122">Suppose you had a QueueTrigger that initiates a function when a blob is added to a queue.</span></span> <span data-ttu-id="281df-123">입력 Blob 바인딩은 Azure Blob Storage에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-123">An input blob binding would be used to connect to Azure Blob storage.</span></span> 

<span data-ttu-id="281df-124">출력 바인딩은 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-124">Output bindings are used to store data.</span></span> <span data-ttu-id="281df-125">예를 들어 함수의 반환 값을 Azure Table Storage로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="281df-125">For instance, they send the return value of the function to Azure Table storage.</span></span>

<span data-ttu-id="281df-126">사용 가능한 바인딩의 전체 목록은 [Azure 설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-126">A full list of available bindings is available in the [Azure documentation](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).</span></span>

### <a name="a-sample-trigger-and-binding-functionjson"></a><span data-ttu-id="281df-127">샘플 트리거 및 바인딩(function.json)</span><span class="sxs-lookup"><span data-stu-id="281df-127">A sample trigger and binding (function.json)</span></span>
<span data-ttu-id="281df-128">이는 함수에 대한 트리거 및 바인딩의 샘플 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="281df-128">This is a sample definition of a trigger and binding for a function.</span></span> <span data-ttu-id="281df-129">설명하는 바인딩 유형에 따라 설정해야 하는 속성 값이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="281df-129">You will note that depending on the type of binding you are describing, there are different property values that need to be set.</span></span> <span data-ttu-id="281df-130">각 바인딩에는 입력 바인딩인지 아니면 출력 바인딩인지를 정의하는 지침도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-130">Each binding also has a direction that defines whether it is an input or output binding.</span></span> <span data-ttu-id="281df-131">트리거는 항상 입력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="281df-131">Triggers are always input bindings.</span></span> <span data-ttu-id="281df-132">이 샘플은 **myqueue-items**라는 큐에 추가되는 메시지에 의해 트리거되는 함수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="281df-132">This sample shows a function that is triggered by a message being added to a queue named **myqueue-items**.</span></span> <span data-ttu-id="281df-133">그런 다음, 함수의 반환 값을 Azure Table Storage의 **outTable** 테이블로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="281df-133">It then sends the return value of the function to the **outTable** table in Azure Table storage.</span></span>

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
## <a name="premade-functions-and-templates"></a><span data-ttu-id="281df-134">기본 제공 함수 및 템플릿</span><span class="sxs-lookup"><span data-stu-id="281df-134">Premade functions and templates</span></span>
<span data-ttu-id="281df-135">Azure는 일반 Azure 함수 시나리오에 대해 미리 구성된 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-135">Azure provides pre-configured templates for common Azure function scenarios.</span></span>

### <a name="quickstart-templates"></a><span data-ttu-id="281df-136">빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="281df-136">Quickstart templates</span></span>
<span data-ttu-id="281df-137">Azure 함수를 추가하려면 함수 앱을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-137">To add an Azure function, you must select a function app.</span></span> <span data-ttu-id="281df-138">함수 앱은 꺾쇠괄호 아이콘 내의 번개 모양으로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-138">The function app can be identified by the lightning bolt within pointy brackets icon.</span></span>  
![함수 아이콘](../images/5-function-icon.png)

<span data-ttu-id="281df-140">첫 번째 Azure 함수를 추가할 때 빠른 시작 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-140">When adding your first Azure function, you are presented with the Quickstart screen.</span></span> <span data-ttu-id="281df-141">이 화면에서 원하는 트리거 유형 및 프로그래밍 언어를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-141">This screen allows you to make a selection on your desired trigger type and programming language.</span></span> <span data-ttu-id="281df-142">그런 다음, 선택 사항에 따라 Azure는 함수 코드 및 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-142">Then, based on your selections, Azure will generate the function code and configuration for you.</span></span>  
![함수 빠른 시작](../images/5-quickstart-form.png)

### <a name="function-templates"></a><span data-ttu-id="281df-144">함수 템플릿</span><span class="sxs-lookup"><span data-stu-id="281df-144">Function templates</span></span>
<span data-ttu-id="281df-145">사용할 수 있는 템플릿은 빠른 시작에서 제공하는 것으로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-145">The selection of templates is not limited to those available in the Quickstart.</span></span> <span data-ttu-id="281df-146">30개가 넘는 템플릿 중에서 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-146">You also have the option of choosing from over 30 different templates.</span></span> <span data-ttu-id="281df-147">후속 함수를 만들거나 빠른 시작 화면에서 **사용자 지정 함수** 옵션을 선택하여 템플릿 목록 화면에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-147">You can access the template list screen while creating subsequent functions, or by selecting the **Custom function** option on the Quickstart screen.</span></span>  
<span data-ttu-id="281df-148">![함수 템플릿](../images/5-template-list.png)</span><span class="sxs-lookup"><span data-stu-id="281df-148">![Function templates](../images/5-template-list.png)</span></span>

## <a name="navigating-to-your-function-and-files"></a><span data-ttu-id="281df-149">함수 및 파일 탐색</span><span class="sxs-lookup"><span data-stu-id="281df-149">Navigating to your function and files</span></span>
<span data-ttu-id="281df-150">템플릿에서 함수를 만들면 여러 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-150">After you create a function from a template, several files are created.</span></span> <span data-ttu-id="281df-151">JavaScript와 함께 Webhook + API 빠른 시작을 사용하기로 선택했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-151">Suppose you opted to use the Webhook + API Quickstart using JavaScript.</span></span> <span data-ttu-id="281df-152">이 경우 구성 파일, **function.json** 및 소스 코드 파일인 **index.js**가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-152">The files generated would be a configuration file, **function.json**, and a source code file, **index.js**.</span></span> <span data-ttu-id="281df-153">함수 앱에 액세스하면, 앱에서 만들어진 함수를 보여주는 메뉴 트리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-153">When accessing the function app, you will be presented with a menu tree displaying the functions that have been created in the app.</span></span> <span data-ttu-id="281df-154">메뉴 트리는 함수 앱에 함수를 추가할 수 있는 이 **함수** 메뉴 항목에도 표시됩니다(메뉴 항목 위로 마우스를 이동하면 더하기(+) 아이콘이 나타남).</span><span class="sxs-lookup"><span data-stu-id="281df-154">It is also on this **Functions** menu item that you are able to add additional functions to the function app (a plus + icon will appear when you're hovering over the menu item).</span></span>  
<span data-ttu-id="281df-155">![함수 추가 단추](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="281df-155">![Add Function button](../images/5-function-add-button.png)</span></span> 

<span data-ttu-id="281df-156">위에서 언급한 이 빠른 시작의 경우 트리 뷰에서 **함수**를 확장하면 기본 이름인 **HttpTriggerJS1**과 함께 하나의 함수가 표시됩니다(함수 f 아이콘으로도 표시됨).</span><span class="sxs-lookup"><span data-stu-id="281df-156">In the case of this Quickstart mentioned above, when you expand **Functions** in the tree view, you will see one function with a default name of **HttpTriggerJS1** (also indicated by the function f icon).</span></span> <span data-ttu-id="281df-157">이 함수를 선택하면 코드 창이 열리고 **index.js** 소스 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-157">Selecting this function will open up a code window and display the **index.js** source file.</span></span> <span data-ttu-id="281df-158">코드 창의 오른쪽에는 **파일 보기**에 대한 탭이 포함된 플라이아웃 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-158">On the right-hand side of the code window, there is a flyout menu that includes a tab to **View files**.</span></span> <span data-ttu-id="281df-159">이 탭을 선택하면 함수를 구성하는 파일 구조(저장소에서 모방됨)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-159">Selecting this tab will show you the file structure (mimicked in storage) that makes up your function.</span></span>  
<span data-ttu-id="281df-160">![함수 템플릿](../images/5-file-navigation.png)</span><span class="sxs-lookup"><span data-stu-id="281df-160">![Function templates](../images/5-file-navigation.png)</span></span>

## <a name="execution-options-for-testing-your-azure-function"></a><span data-ttu-id="281df-161">Azure 함수 테스트를 위한 실행 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="281df-161">Execution options for testing your Azure function</span></span>
<span data-ttu-id="281df-162">Azure 함수가 생성되면 테스트 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-162">Once you have an Azure function created, you will need to know how to test it.</span></span> <span data-ttu-id="281df-163">수동 실행, Azure Portal 내에서 테스트 등 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-163">There are a couple of approaches: manual execution and testing from within the Azure portal itself.</span></span>

### <a name="manual-execution-of-a-function"></a><span data-ttu-id="281df-164">함수의 수동 실행</span><span class="sxs-lookup"><span data-stu-id="281df-164">Manual execution of a function</span></span>
<span data-ttu-id="281df-165">구성된 트리거를 수동으로 트리거하여 함수 실행을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-165">You can initiate the execution of a function by manually triggering the configured trigger.</span></span> <span data-ttu-id="281df-166">예를 들어 HttpTrigger를 사용하는 경우 Postman이나 cURL과 같은 도구를 사용하여 함수 엔드포인트 URL에 대한 HTTP 요청을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-166">For instance, if you are using an HttpTrigger - you can use a tool such as Postman or cURL to initiate an HTTP request to your function endpoint URL.</span></span>  
<span data-ttu-id="281df-167">![함수의 Postman 실행](../images/5-postman-execution.png) 왼쪽 탐색 창에서 HTTP 트리거를 선택한 후에 **함수 URL 가져오기** 단추를 선택하여 엔드포인트 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-167">![Postman execution of a function](../images/5-postman-execution.png) You can obtain the endpoint URL by selecting your HTTP Trigger from the left navigation, and then selecting the **Get function URL** button.</span></span>  
<span data-ttu-id="281df-168">![함수 URL 가져오기](../images/5-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="281df-168">![Get function URL](../images/5-get-function-url.png)</span></span>

### <a name="testing-a-function-in-the-azure-portal"></a><span data-ttu-id="281df-169">Azure Portal에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="281df-169">Testing a function in the Azure portal</span></span>
<span data-ttu-id="281df-170">Azure Portal에서도 함수를 테스트하는 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-170">Alternatively, the Azure portal also provides a convenient way to test your functions.</span></span> <span data-ttu-id="281df-171">코드 창의 오른쪽에는 플라이아웃 탭 방식의 탐색 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-171">On the right side of the code window, there is a flyout tabbed navigation menu.</span></span> <span data-ttu-id="281df-172">이 메뉴에 **테스트** 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-172">This menu contains a **Test** item.</span></span> <span data-ttu-id="281df-173">메뉴를 확장하고 이 탭을 선택하면 함수를 실행하고 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-173">Expanding the menu and selecting this tab gives you another way to execute your function and view the result.</span></span> <span data-ttu-id="281df-174">HttpTrigger 시나리오를 사용하여 HTTP 메서드를 설정하고 querystring 매개 변수 및 HTTP 헤더를 요청에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-174">In keeping with the HttpTrigger scenario, you can set the HTTP method, and add querystring parameters and HTTP headers to the request.</span></span> <span data-ttu-id="281df-175">또한 추가 시나리오를 테스트하도록 요청 본문을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-175">You may also change the request body to test additional scenarios.</span></span> <span data-ttu-id="281df-176">출력 창에 함수의 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-176">The output window shows the result of the function.</span></span>  
<span data-ttu-id="281df-177">![함수의 Portal 실행](../images/5-portal-execution.png)</span><span class="sxs-lookup"><span data-stu-id="281df-177">![Portal execution of a function](../images/5-portal-execution.png)</span></span>

## <a name="monitoring-an-azure-function"></a><span data-ttu-id="281df-178">Azure 함수 모니터링</span><span class="sxs-lookup"><span data-stu-id="281df-178">Monitoring an Azure function</span></span>
<span data-ttu-id="281df-179">Azure 함수 개발 중 메시지를 기록하고 예외 시나리오를 확인하는 기능은 프로덕션 환경에서 사용하도록 함수를 준비하는 과정에서 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-179">During Azure function development, being able to log messages and determine exception scenarios is critical to ensuring that you are getting your functions production-ready.</span></span> <span data-ttu-id="281df-180">이는 소스 결함을 추적하는 프로덕션 시나리오에서와 마찬가지로 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-180">This is just as important in a production scenario, when you are tracking down the source of a defect.</span></span> <span data-ttu-id="281df-181">Azure Portal의 사용자 인터페이스는 모니터링 대시보드뿐만 아니라 Azure 함수에서 가져온 실행 로그 및 예외를 검토하는 방법도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-181">The Azure portal gives us a user interface that provides a monitoring dashboard as well as a way to review execution logs and exceptions obtained from your Azure functions.</span></span>

### <a name="monitoring-dashboard"></a><span data-ttu-id="281df-182">모니터링 대시보드</span><span class="sxs-lookup"><span data-stu-id="281df-182">Monitoring dashboard</span></span>
<span data-ttu-id="281df-183">함수 앱 탐색 메뉴에서 함수 노드를 확장하면 **모니터** 메뉴 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-183">In the function app navigation menu, once you expand the function node - you will see a **Monitor** menu item.</span></span> <span data-ttu-id="281df-184">모니터 대시보드는 함수 실행의 기록을 보기 위한 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-184">The monitor dashboard provides a quick way to view the history of function executions.</span></span> <span data-ttu-id="281df-185">이 보기에는 성공적인 완료 여부는 물론 타임스탬프, 결과 코드, 지속 기간 및 작업 ID도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-185">This view displays the timestamp, result code, duration, and operation ID, as well as if it completed successfully.</span></span> <span data-ttu-id="281df-186">Azure Application Insights를 통해 데이터가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="281df-186">The data is populated via Azure Application Insights.</span></span>  
<span data-ttu-id="281df-187">![함수 모니터](../images/5-monitor-function.png)</span><span class="sxs-lookup"><span data-stu-id="281df-187">![Function monitor](../images/5-monitor-function.png)</span></span>

### <a name="log-window"></a><span data-ttu-id="281df-188">로그 창</span><span class="sxs-lookup"><span data-stu-id="281df-188">Log window</span></span>
<span data-ttu-id="281df-189">또한 함수에 로그 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-189">You are also able to add log statements to your function.</span></span> <span data-ttu-id="281df-190">이 문은 함수의 로그 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-190">These statements will appear in the log window of the function.</span></span> <span data-ttu-id="281df-191">로그 창은 코드 창의 맨 아래에 있는 탭 방식의 플라이아웃 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-191">The log window is located in a tabbed flyout menu located at the bottom of the code window.</span></span> <span data-ttu-id="281df-192">JavaScript 기반 함수를 사용하는 경우 다음 구문을 사용하여 로그 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-192">When using a JavaScript-based function, you would add a log statement using the following syntax:</span></span>
```javascript
  context.log('Enter your logging statement here');
```  
![로그 창](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a><span data-ttu-id="281df-194">오류 및 경고 창</span><span class="sxs-lookup"><span data-stu-id="281df-194">Errors and warnings window</span></span>
<span data-ttu-id="281df-195">로그 창과 동일한 플라이아웃 메뉴에서 오류 및 경고 창 탭을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="281df-195">You can locate the errors and warnings window tab in the same flyout menu as the log window.</span></span> <span data-ttu-id="281df-196">이 창에는 코드 내의 컴파일 오류 및 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="281df-196">This window will show compilation errors and warnings within your code.</span></span> <span data-ttu-id="281df-197">JavaScript는 동적이며 해석되는 언어이므로 다음 이미지는 C# 함수의 컴파일 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="281df-197">As JavaScript is a dynamic and interpreted language, the following image shows a compilation error in a C# function.</span></span>  
![오류 및 경고 창](../images/5-errors-window.png)