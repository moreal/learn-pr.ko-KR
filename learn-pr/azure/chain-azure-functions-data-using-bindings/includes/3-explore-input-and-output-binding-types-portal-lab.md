<span data-ttu-id="b843b-101">다음은 이 연습에서 작성할 대상에 대한 대략적인 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-101">The following is a high-level illustration of what we're going to build in this exercise.</span></span>

![HTTP 요청 및 응답과 관련 req 및 res 바인딩 매개 변수를 보여 주는 기본 HTTP 트리거의 시각적 표현입니다.](../media-draft/default-http-trigger-visual-small.PNG)

<span data-ttu-id="b843b-103">HTTP 요청을 받았을 때 시작되어 응답 메시지를 보내 각 요청에 응답하는 함수를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-103">We'll create a function that will start when it receives an HTTP request and will respond to each request by sending back a message.</span></span> <span data-ttu-id="b843b-104">`req` 및 `res` 매개 변수는 각각 트리거 바인딩과 출력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-104">The parameters `req` and `res` are the trigger binding and output binding respectively.</span></span> <span data-ttu-id="b843b-105">그럼 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-105">Let's get going!</span></span>

<span data-ttu-id="b843b-106">Azure 계정을 사용하여 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-106">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com?azure-portal=true) with your Azure account.</span></span>

### <a name="create-a-function-app"></a><span data-ttu-id="b843b-107">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b843b-107">Create a function app</span></span>

<span data-ttu-id="b843b-108">이 모듈 전체에서 사용할 함수 앱을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-108">Let's create a function app that we'll use throughout this entire module.</span></span> <span data-ttu-id="b843b-109">함수 앱을 통해 함수를 논리 단위로 그룹화하여 더욱 쉽게 관리, 배포 및 리소스 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-109">A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources.</span></span>

[!INCLUDE [resource-group-note](./rg-notice.md)]

1. <span data-ttu-id="b843b-110">Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기** 단추를 선택한 다음, **계산** > **함수 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-110">Select the **Create a resource** button found on the upper left-hand corner of the Azure portal, then select **Compute** > **Function App**.</span></span>
1. <span data-ttu-id="b843b-111">함수 앱 속성을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-111">Set the function app properties as follows:</span></span>


    | <span data-ttu-id="b843b-112">속성</span><span class="sxs-lookup"><span data-stu-id="b843b-112">Property</span></span>      | <span data-ttu-id="b843b-113">제안 값</span><span class="sxs-lookup"><span data-stu-id="b843b-113">Suggested value</span></span>  | <span data-ttu-id="b843b-114">설명</span><span class="sxs-lookup"><span data-stu-id="b843b-114">Description</span></span>                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="b843b-115">**앱 이름**</span><span class="sxs-lookup"><span data-stu-id="b843b-115">**App name**</span></span> | <span data-ttu-id="b843b-116">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="b843b-116">Globally unique name</span></span> | <span data-ttu-id="b843b-117">새 함수 앱을 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-117">Name that identifies your new function app.</span></span> <span data-ttu-id="b843b-118">유효한 문자는 `a-z`, `0-9` 및 `-`입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-118">Valid characters are `a-z`, `0-9`, and `-`.</span></span>  | 
    | <span data-ttu-id="b843b-119">**구독**</span><span class="sxs-lookup"><span data-stu-id="b843b-119">**Subscription**</span></span> | <span data-ttu-id="b843b-120">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="b843b-120">Your subscription</span></span> | <span data-ttu-id="b843b-121">이 새 함수 앱이 만들어질 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-121">The subscription under which this new function app is created.</span></span> | 
    | <span data-ttu-id="b843b-122">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="b843b-122">**Resource Group**</span></span>|  [!INCLUDE [resource-group-name](./rg-name.md)] | <span data-ttu-id="b843b-123">함수 앱을 만들 새 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-123">Name for the new resource group in which to create your function app.</span></span> | 
    | <span data-ttu-id="b843b-124">**OS**</span><span class="sxs-lookup"><span data-stu-id="b843b-124">**OS**</span></span> | <span data-ttu-id="b843b-125">Windows</span><span class="sxs-lookup"><span data-stu-id="b843b-125">Windows</span></span> | <span data-ttu-id="b843b-126">함수 앱을 호스트하는 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-126">The operating system that hosts the function app.</span></span>  |
    | <span data-ttu-id="b843b-127">**호스팅**</span><span class="sxs-lookup"><span data-stu-id="b843b-127">**Hosting**</span></span> |   <span data-ttu-id="b843b-128">소비 계획</span><span class="sxs-lookup"><span data-stu-id="b843b-128">Consumption plan</span></span> | <span data-ttu-id="b843b-129">함수 앱에 리소스가 할당되는 방법을 정의하는 호스팅 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-129">Hosting plan that defines how resources are allocated to your function app.</span></span> <span data-ttu-id="b843b-130">기본 **소비 계획**에서 함수의 필요에 따라 리소스가 동적으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-130">In the default **Consumption Plan**, resources are added dynamically as required by your functions.</span></span> <span data-ttu-id="b843b-131">[서버 없는](https://azure.microsoft.com/overview/serverless-computing/) 호스팅에서는 함수가 실행되는 시간 만큼만 요금을 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-131">In this [serverless](https://azure.microsoft.com/overview/serverless-computing/) hosting, you only pay for the time your functions run.</span></span>   |
    | <span data-ttu-id="b843b-132">**위치**</span><span class="sxs-lookup"><span data-stu-id="b843b-132">**Location**</span></span> | <span data-ttu-id="b843b-133">서유럽</span><span class="sxs-lookup"><span data-stu-id="b843b-133">West Europe</span></span> | <span data-ttu-id="b843b-134">사용자 근처 또는 함수가 액세스할 기타 서비스에 가까운 [지역](https://azure.microsoft.com/regions/)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-134">Choose a [region](https://azure.microsoft.com/regions/) near you or near other services your functions access.</span></span> |
    | <span data-ttu-id="b843b-135">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="b843b-135">**Storage account**</span></span> |  <span data-ttu-id="b843b-136">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="b843b-136">Globally unique name</span></span> |  <span data-ttu-id="b843b-137">함수 앱에 사용된 새 저장소 계정의 이름.</span><span class="sxs-lookup"><span data-stu-id="b843b-137">Name of the new storage account used by your function app.</span></span> <span data-ttu-id="b843b-138">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-138">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="b843b-139">이 대화 상자는 여러분이 앱에 지정한 이름에서 파생된 고유한 이름으로 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-139">This dialog populates the field with a unique name that is derived from the name you gave the app.</span></span> <span data-ttu-id="b843b-140">하지만 자유롭게 다른 이름을 사용해도 되고, 심지어 기존 계정을 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-140">However, feel free to use a different name or even an existing account.</span></span> |


3. <span data-ttu-id="b843b-141">**만들기**를 선택하여 함수 앱을 프로비전하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-141">Select **Create** to provision and deploy the function app.</span></span>

4. <span data-ttu-id="b843b-142">포털의 오른쪽 위 모서리에서 [알림] 아이콘을 선택하고 다음 메시지와 비슷한 **배포 진행 중** 메시지가 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-142">Select the Notification icon in the upper-right corner of the portal and watch for a **Deployment in progress** message similar to the following message.</span></span>

![함수 앱 배포가 진행 중이라는 알림](../media-draft/func-app-deploy-progress-small.PNG)

5. <span data-ttu-id="b843b-144">배포에 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-144">Deployment can take some time.</span></span> <span data-ttu-id="b843b-145">따라서 알림 허브에 계속 머물면서 다음 메시지와 비슷한 **배포 성공** 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-145">So, stay in the notification hub and  watch for a **Deployment succeeded** message similar to the following message.</span></span>

![함수 앱 배포가 완료되었다는 알림](../media-draft/func-app-deploy-success-small.PNG)

6. <span data-ttu-id="b843b-147">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="b843b-147">Congratulations!</span></span> <span data-ttu-id="b843b-148">함수 앱을 만들고 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-148">You've created and deployed your function app.</span></span> <span data-ttu-id="b843b-149">**리소스로 이동**을 선택하여 함수 앱을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-149">Select **Go to resource** to view your new function app.</span></span>

>[!TIP]
><span data-ttu-id="b843b-150">포털에서 앱 함수를 찾는 데 문제가 있는 경우 [포털에서 즐겨찾기에 함수 앱을 추가](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite) 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-150">If you are having trouble finding your function apps in the portal, find out how to [add Function Apps to your favorites in the portal](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).</span></span>

### <a name="create-a-function"></a><span data-ttu-id="b843b-151">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="b843b-151">Create a function</span></span>

<span data-ttu-id="b843b-152">함수 앱이 생겼으니, 이제 함수를 만들 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-152">Now that we have a function app, it's time to create a function.</span></span> <span data-ttu-id="b843b-153">함수는 트리거를 통해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-153">A function is activated through a trigger.</span></span> <span data-ttu-id="b843b-154">이 모듈에서는 HTTP 트리거를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-154">In this module, we'll use an HTTP trigger.</span></span>

1. <span data-ttu-id="b843b-155">새 함수 앱을 펼친 다음, 함수 컬렉션 위를 마우스로 가리키고, **함수** 옆에 있는 추가(**+**) 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-155">Expand your new function app, then hover over the functions collection and select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="b843b-156">이 작업은 함수 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-156">This action starts the function creation process.</span></span> <span data-ttu-id="b843b-157">다음 애니메이션에서는 이 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-157">The following animation illustrates this action.</span></span>

![사용자가 함수 메뉴 항목을 마우스로 가리키면 표시되는 더하기 기호의 애니메이션](../media-draft/func-app-plus-hover-small.gif)

2. <span data-ttu-id="b843b-159">**빨리 시작하기** 페이지에서 **WebHook + API**를 선택한 후 함수에 대한 언어를 선택하고 **이 함수 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-159">In the **Get started quickly** page, select **WebHook + API**, select a language for your function, and click **Create this function**.</span></span>

3. <span data-ttu-id="b843b-160">함수는 HTTP 트리거 함수에 대한 템플릿을 사용하여 선택한 언어로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-160">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="b843b-161">이 연습에서는 JavaScript 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-161">In this exercise, we'll create a JavaScript function.</span></span>

### <a name="try-it-out"></a><span data-ttu-id="b843b-162">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="b843b-162">Try it out</span></span>

<span data-ttu-id="b843b-163">다음과 같은 방법으로 지금까지 우리가 가진 테스트해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-163">Let's test what we have so far by doing the following:</span></span>

1. <span data-ttu-id="b843b-164">새 함수에서 오른쪽 맨 위에 있는 **</> 함수 URL 가져오기**를 클릭하고 **기본값(함수 키)** 를 선택한 후 **복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-164">In your new function, click **</> Get function URL** at the top right, select **default (Function key)**, and then click **Copy**.</span></span>

2. <span data-ttu-id="b843b-165">복사한 함수 URL을 브라우저의 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-165">Paste the function URL you copied into your browser's address bar.</span></span> <span data-ttu-id="b843b-166">이 URL의 끝에 `&name=<yourname>` 쿼리 문자열 값을 추가하고, 키보드에서 `Enter` 키를 눌러 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-166">Add the query string value `&name=<yourname>` to the end of this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="b843b-167">브라우저에 표시된 함수가 반환한 다음 응답과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-167">You should see a response similar to the following response returned by the function displayed in your browser.</span></span>  

<span data-ttu-id="b843b-168">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-168">Nice work!</span></span> <span data-ttu-id="b843b-169">이제 함수 앱에 HTTP 트리거 함수를 추가하고 예상대로 작동하는지 테스트를 마쳤습니다!</span><span class="sxs-lookup"><span data-stu-id="b843b-169">You have now added a HTTP-triggered function to your function app and tested to make sure it is working as expected!</span></span>

![함수 호출이 성공할 때 표시되는 응답 메시지의 스크린샷](../media-draft/default-http-trigger-response-small.PNG)

<span data-ttu-id="b843b-171">지금까지 이 연습에서 확인한 것처럼 함수를 만들 때는 트리거 유형을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-171">As you can see from this exercise so far, you have to select a trigger type when creating a function.</span></span> <span data-ttu-id="b843b-172">모든 함수에는 하나의 트리거만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-172">Every function has one, and only one trigger.</span></span> <span data-ttu-id="b843b-173">이 예제에서는 HTTP 트리거를 사용하므로 함수가 HTTP 요청을 받아야 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-173">In this example, we're using an HTTP trigger, which means our function starts when it receives an HTTP request.</span></span> <span data-ttu-id="b843b-174">다음 JavaScript 스크린샷에서의 기본 구현은 쿼리 문자열이나 요청 본문에서 수신한 *name* 매개 변수의 값에 답합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-174">The default implementation, shown in the following screenshot in JavaScript, responds with the value of a parameter *name* it received in the query string  or body of the request.</span></span> <span data-ttu-id="b843b-175">문자열이 제공되지 않은 경우 함수는 호출하는 상대에게 이름 값 제공을 요청하는 메시지로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-175">If no string was provided, the function responds with a message asking whoever is calling to supply a name value.</span></span>

![HTTP에서 트리거한 Azure 함수의 기본 JavaScript 구현 스크린샷](../media-draft/default-http-trigger-implementation-small.PNG)

<span data-ttu-id="b843b-177">이 코드는 모두 이 함수 폴더의 *index.js* 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-177">All of this code is in the *index.js* file in this function's folder.</span></span> <span data-ttu-id="b843b-178">함수의 다른 파일인 *function.json* 구성 파일을 간단하게 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="b843b-178">Let's look briefly at the function's other file, the *function.json* config file.</span></span> <span data-ttu-id="b843b-179">구성 데이터는 다음 JSON 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-179">This configuration data is shown in the following JSON listing.</span></span>

```json
{
  "disabled": false,
  "bindings": [
    {
      "authLevel": "function",
      "type": "httpTrigger",
      "direction": "in",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ]
}
```

<span data-ttu-id="b843b-180">보이는 것처럼 이 함수에는 `httpTrigger` 형식인 **req** 트리거 바인딩과 `HTTP` 형식인 **res** 출력 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-180">As you can see, this function has a trigger binding named **req** of type `httpTrigger` and an output binding named **res**  of type `HTTP`.</span></span> <span data-ttu-id="b843b-181">함수의 앞 코드에서는 **req** 매개 변수를 통해 수신되는 HTTP 요청의 페이로드에 액세스하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-181">In the preceding code for our function, we saw how we accessed the payload of the incoming HTTP request through our **req** parameter.</span></span> <span data-ttu-id="b843b-182">마찬가지로, **res** 매개 변수를 설정하여 간단하게 HTTP 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-182">Similarly, we sent an HTTP response simply by setting our **res** parameter.</span></span> <span data-ttu-id="b843b-183">바인딩은 일부 어려운 작업을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-183">Bindings really do take care of some of the heavy lifting for us!</span></span>

>[!TIP]
><span data-ttu-id="b843b-184">Azure Portal의 함수 패널 오른쪽에서 **파일 보기** 메뉴를 확장하여 index.js 및 function.json을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-184">You can see index.js and function.json by expanding the **View Files** menu on the right of the function panel in the Azure portal.</span></span>  

### <a name="explore-binding-types"></a><span data-ttu-id="b843b-185">바인딩 형식 살펴보기</span><span class="sxs-lookup"><span data-stu-id="b843b-185">Explore binding types</span></span>

1. <span data-ttu-id="b843b-186">함수 항목에는 다음 스크린샷처럼 메뉴 항목 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-186">Notice under the function entry there is a set of menu items as shown in the following screenshot.</span></span>

![함수 앱 블레이드에서 함수 아래 표시된 메뉴 항목의 스크린샷](../media-draft/func-menu-small.PNG)

2. <span data-ttu-id="b843b-188">통합 메뉴 항목을 선택하여 이 함수에 대한 통합 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-188">Select the Integrate menu item to open the integration tab for our function.</span></span> <span data-ttu-id="b843b-189">이 단위를 계속 진행해 온 경우 통합 탭이 다음 스크린샷과 매우 유사하게 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-189">If you have been following along with this unit, the integrate tab should look very similar to the following screenshot.</span></span>

![통합 UI 또는 탭의 스크린샷](../media-draft/func-integrate-tab-small.PNG)

<span data-ttu-id="b843b-191">이 스크린샷에서는 이미 트리거와 출력 바인딩이 정의되어 있는 것이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-191">Notice that we have already defined a trigger and an output binding as shown in this screenshot.</span></span> <span data-ttu-id="b843b-192">또한 둘 이상의 트리거는 추가할 수 없음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-192">You can also see that we can't add more than one trigger.</span></span> <span data-ttu-id="b843b-193">사실 함수에 대한 트리거를 변경하려면 먼저 트리거를 삭제하고 새로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-193">In fact, to change the trigger for our function we would have to first delete the trigger and create a new one.</span></span>

<span data-ttu-id="b843b-194">반면 이 양식의 **입력** 및 **출력** 섹션은 다른 바인딩 추가를 위한 더하기 `+` 기호를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-194">On the other hand, the **Inputs** and **Outputs** sections of this form display a plus `+` sign to add more bindings.</span></span>

3. <span data-ttu-id="b843b-195">**입력** 열에서 **+ 새 입력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-195">Select **+ New Input** under the **Inputs** column.</span></span> <span data-ttu-id="b843b-196">다음 스크린샷에 표시된 것처럼 모든 가능한 입력 바인딩 형식 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-196">A list of all possible input binding types is displayed as shown in the following screenshot.</span></span>

![가능한 입력 바인딩 목록을 표시하는 스크린샷](../media-draft/func-input-bindings-selector-small.PNG)

<span data-ttu-id="b843b-198">잠시 각 입력 바인딩과, 솔루션에서 어떻게 사용할지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-198">Take a moment to consider each of these input bindings and how you might use them in a solution.</span></span> <span data-ttu-id="b843b-199">선택은 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-199">There are a lot to choose from.</span></span> <span data-ttu-id="b843b-200">다른 데이터 원본의 지원을 계속하고 있기 때문에 이 모듈을 읽은 시점에는 목록이 바뀌었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-200">This list may even have changed by the time you read this module as we continue to support more data sources.</span></span>

4. <span data-ttu-id="b843b-201">이 목록을 해제하려면 **취소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-201">Select **Cancel** to dismiss this list.</span></span>

5. <span data-ttu-id="b843b-202">**출력** 열 아래에서 **+ 새 출력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-202">Select **+ New Output** under the **Outputs** column.</span></span> <span data-ttu-id="b843b-203">다음 스크린샷에 표시된 것처럼 모든 가능한 출력 바인딩 형식 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-203">A list of all possible output binding types is displayed as shown in the following screenshot.</span></span>

![가능한 출력 바인딩 목록을 표시하는 스크린샷](../media-draft/func-output-bindings-selector-small.PNG)

<span data-ttu-id="b843b-205">이 스크린샷의 오른쪽에 스크롤바가 필요할 만큼 여기에도 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-205">Again, you have lots of options here, as shown by the need for a scroll bar to the right in this screenshot.</span></span>

>[!TIP]
><span data-ttu-id="b843b-206">지원되는 바인딩에 대한 자세한 내용은 Azure Functions 설명서의 [지원되는 바인딩 목록](https://docs.microsoft.com/azure/azure-functions/functions-versions)을 참조하십시오. </span><span class="sxs-lookup"><span data-stu-id="b843b-206">To learn more details about the bindings that are supported, check out the [list of supported bindings](https://docs.microsoft.com/azure/azure-functions/functions-versions) in the Azure Functions documentation.</span></span>

<span data-ttu-id="b843b-207">지금까지 함수 앱을 만들고 함수를 추가하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-207">So far we've learned how to create a function app and add a function to it.</span></span> <span data-ttu-id="b843b-208">HTTP 요청이 수행되면 실행되는 간단한 함수의 작동을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-208">We've seen a simple function in action that runs when an HTTP request is made to it.</span></span> <span data-ttu-id="b843b-209">또한 함수에서 사용할 수 있는 입력 및 출력 바인딩의 포털 UI와 형식도 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-209">We've also explored the portal UI and types of input and output binding that are available to our functions.</span></span> <span data-ttu-id="b843b-210">다음 단위에서는 데이터베이스로부터 텍스트를 읽기 위해 입력 바인딩을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b843b-210">In the next unit, we'll use an input binding to read text from a a database.</span></span>