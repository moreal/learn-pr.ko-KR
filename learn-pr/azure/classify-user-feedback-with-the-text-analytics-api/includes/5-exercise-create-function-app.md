<span data-ttu-id="953b6-101">솔루션을 빌드하려면 몇 가지 코드를 호스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-101">To build our solution, we'll need to host some code.</span></span>  <span data-ttu-id="953b6-102">Azure Functions 함수 앱은 논리를 호스트하기에 좋은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-102">An Azure Functions function app is a good place to host our logic.</span></span> 

## <a name="create-a-function-app-to-host-our-function"></a><span data-ttu-id="953b6-103">함수를 호스트할 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="953b6-103">Create a Function App to host our function</span></span>

[!INCLUDE [resource-group-note](./rg-notice.md)]

1. <span data-ttu-id="953b6-104">Azure 계정을 사용하여 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-104">Make sure you are signed in to the Azure portal at [https://portal.azure.com](https://portal.azure.com?azure-portal=true) with your Azure account.</span></span>

1. <span data-ttu-id="953b6-105">Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기** 단추를 선택한 다음, **계산** > **함수 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-105">Select the **Create a resource** button found on the upper left-hand corner of the Azure portal, then select **Compute** > **Function App**.</span></span>

1. <span data-ttu-id="953b6-106">다음 표에 지정된 대로 함수 앱 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-106">Enter the function app settings as specified in the following table.</span></span>


    | <span data-ttu-id="953b6-107">설정</span><span class="sxs-lookup"><span data-stu-id="953b6-107">Setting</span></span>      | <span data-ttu-id="953b6-108">제안 값</span><span class="sxs-lookup"><span data-stu-id="953b6-108">Suggested value</span></span>  | <span data-ttu-id="953b6-109">설명</span><span class="sxs-lookup"><span data-stu-id="953b6-109">Description</span></span>                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="953b6-110">**앱 이름**</span><span class="sxs-lookup"><span data-stu-id="953b6-110">**App name**</span></span> | <span data-ttu-id="953b6-111">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="953b6-111">Globally unique name</span></span> | <span data-ttu-id="953b6-112">새 함수 앱을 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-112">Name that identifies your new function app.</span></span> <span data-ttu-id="953b6-113">유효한 문자는 `a-z`, `0-9` 및 `-`입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-113">Valid characters are `a-z`, `0-9`, and `-`.</span></span>  | 
    | <span data-ttu-id="953b6-114">**구독**</span><span class="sxs-lookup"><span data-stu-id="953b6-114">**Subscription**</span></span> | <span data-ttu-id="953b6-115">본인의 구독</span><span class="sxs-lookup"><span data-stu-id="953b6-115">Your subscription</span></span> | <span data-ttu-id="953b6-116">새 함수 앱이 만들어질 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-116">The subscription under which this new function app is created.</span></span> | 
    | <span data-ttu-id="953b6-117">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="953b6-117">**Resource Group**</span></span>|  [!INCLUDE [resource-group-name](./rg-name.md)] | <span data-ttu-id="953b6-118">함수 앱을 만들 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-118">Name for the  resource group in which to create your function app.</span></span><br/><br/><span data-ttu-id="953b6-119">**기존 항목 사용**을 선택하고 마지막 연습에서 만든 리소스 그룹을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-119">Make sure to select **Use existing** and use the resource group that we created in the last exercise.</span></span> <span data-ttu-id="953b6-120">이렇게 하면 이 모듈에서 만든 모든 리소스가 함께 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-120">That way, all resource we made in this module are kept together.</span></span> | 
    | <span data-ttu-id="953b6-121">**OS**</span><span class="sxs-lookup"><span data-stu-id="953b6-121">**OS**</span></span> | <span data-ttu-id="953b6-122">Windows</span><span class="sxs-lookup"><span data-stu-id="953b6-122">Windows</span></span> | <span data-ttu-id="953b6-123">함수 앱을 호스트하는 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-123">The operating system that hosts the function app.</span></span>  |
    | <span data-ttu-id="953b6-124">**호스팅**</span><span class="sxs-lookup"><span data-stu-id="953b6-124">**Hosting**</span></span> |   <span data-ttu-id="953b6-125">소비 계획</span><span class="sxs-lookup"><span data-stu-id="953b6-125">Consumption plan</span></span> | <span data-ttu-id="953b6-126">함수 앱에 리소스가 할당되는 방법을 정의하는 호스팅 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-126">Hosting plan that defines how resources are allocated to your function app.</span></span> <span data-ttu-id="953b6-127">기본 **소비 계획**에서 함수의 요구에 따라 리소스가 동적으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-127">In the default **Consumption Plan**, resources are added dynamically as required by your functions.</span></span> <span data-ttu-id="953b6-128">[서버리스](https://azure.microsoft.com/overview/serverless-computing/) 호스팅에서는 함수가 실행되는 시간만큼만 요금을 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-128">In this [serverless](https://azure.microsoft.com/overview/serverless-computing/) hosting, you only pay for the time your functions run.</span></span>   |
    | <span data-ttu-id="953b6-129">**위치**</span><span class="sxs-lookup"><span data-stu-id="953b6-129">**Location**</span></span> | <span data-ttu-id="953b6-130">미국 서부</span><span class="sxs-lookup"><span data-stu-id="953b6-130">West US</span></span> | <span data-ttu-id="953b6-131">여러분과 가까운 또는 함수가 액세스하는 다른 서비스와 가까운 [지역](https://azure.microsoft.com/regions/)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-131">Choose a [region](https://azure.microsoft.com/regions/) near you or near other services your functions access.</span></span><br/><br/><span data-ttu-id="953b6-132">마지막 연습에서 텍스트 분석 API 계정을 만들 때 사용한 지역과 동일한 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-132">Select the same region that you used when creating the Text Analytics API account in the last exercise.</span></span> |
    | <span data-ttu-id="953b6-133">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="953b6-133">**Storage account**</span></span> |  <span data-ttu-id="953b6-134">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="953b6-134">Globally unique name</span></span> |  <span data-ttu-id="953b6-135">함수 앱에서 사용하는 새 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-135">Name of the new storage account used by your function app.</span></span> <span data-ttu-id="953b6-136">저장소 계정 이름은 3~24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-136">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="953b6-137">이 대화 상자는 여러분이 앱에 지정한 이름에서 파생된 고유한 이름으로 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-137">This dialog populates the field with a unique name that is derived from the name you gave the app.</span></span> <span data-ttu-id="953b6-138">하지만 자유롭게 다른 이름을 사용해도 되고, 심지어 기존 계정을 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-138">However, feel free to use a different name or even an existing account.</span></span> |

3. <span data-ttu-id="953b6-139">**만들기**를 선택하여 함수 앱을 프로비전하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-139">Select **Create** to provision and deploy the function app.</span></span>

4. <span data-ttu-id="953b6-140">포털의 오른쪽 위 모서리에서 [알림] 아이콘을 선택하고 다음 메시지와 비슷한 **배포 진행 중** 메시지가 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-140">Select the Notification icon in the upper-right corner of the portal and watch for a **Deployment in progress** message similar to the following message.</span></span>

![함수 앱 배포가 진행 중이라는 알림](../media-draft/func-app-deploy-progress-small.PNG)

5. <span data-ttu-id="953b6-142">배포에 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-142">Deployment can take some time.</span></span> <span data-ttu-id="953b6-143">따라서 알림 허브에 계속 머물면서 다음 메시지와 비슷한 **배포 성공** 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-143">So, stay in the notification hub and  watch for a **Deployment succeeded** message similar to the following message.</span></span>

![함수 앱 배포가 완료되었다는 알림](../media-draft/func-app-text-analytics-deploy-success.png)

6. <span data-ttu-id="953b6-145">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="953b6-145">Congratulations!</span></span> <span data-ttu-id="953b6-146">함수 앱을 만들고 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-146">You've created and deployed your function app.</span></span> <span data-ttu-id="953b6-147">**리소스로 이동**을 선택하여 함수 앱을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-147">Select **Go to resource** to view your new function app.</span></span>

>[!TIP]
><span data-ttu-id="953b6-148">포털에서 앱 함수를 찾는 데 문제가 있는 경우 [Azure Portal에서 즐겨찾기에 함수 앱을 추가](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite)합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-148">Having trouble finding your function apps in the portal, try [adding Function Apps to your favorites in the Azure portal](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).</span></span>

## <a name="create-a-function-to-hold-our-logic"></a><span data-ttu-id="953b6-149">논리를 보관할 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="953b6-149">Create a function to hold our logic</span></span>

<span data-ttu-id="953b6-150">함수 앱이 생겼으니, 이제 함수를 만들 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-150">Now that we have a function app, it's time to create a function.</span></span> <span data-ttu-id="953b6-151">함수는 트리거를 통해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-151">A function is activated through a trigger.</span></span> <span data-ttu-id="953b6-152">이 모듈에서는 큐 트리거를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-152">In this module, we'll use a Queue trigger.</span></span> <span data-ttu-id="953b6-153">런타임에서는 큐를 폴링하고 이 함수를 시작하여 새 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-153">The runtime will poll a queue and start this function to process a new message.</span></span>

1. <span data-ttu-id="953b6-154">새 함수 앱을 확장한 다음, 마우스 커서를 **함수** 컬렉션 위로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-154">Expand your new function app, then hover over the **Functions** collection.</span></span> <span data-ttu-id="953b6-155">추가(**+**) 단추가 나타나면 추가 단추를 선택하여 함수 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-155">Select the Add (**+**) button when it appears to start the function creation process.</span></span>

![사용자가 함수 메뉴 항목을 마우스로 가리키면 나타나는 더하기 기호 애니메이션.](../media-draft/func-app-plus-hover-small.gif)

2. <span data-ttu-id="953b6-157">나타나는 **신속하게 시작** 페이지에서 **사용자 지정 함수**를 선택합니다. 그러면 사용 가능한 함수 템플릿 목록이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-157">In the **Get started quickly** page that now appears, select **Custom function**, which loads the list of available function templates.</span></span> 

1. <span data-ttu-id="953b6-158">**큐 트리거** 템플릿 목록 항목에서 **JavaScript**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-158">Select **JavaScript** on the **Queue trigger** template list entry.</span></span>

![큐 트리거 항목에서 JavaScript를 선택한 Azure Functions 템플릿의 스크린샷.](../media-draft/quickstart-select-queue-trigger.png)

1. <span data-ttu-id="953b6-160">나타나는 **새 함수** 대화 상자에서 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-160">In the **New Function** dialog that appears, enter the following values.</span></span>


|<span data-ttu-id="953b6-161">속성</span><span class="sxs-lookup"><span data-stu-id="953b6-161">Property</span></span>  |<span data-ttu-id="953b6-162">값</span><span class="sxs-lookup"><span data-stu-id="953b6-162">Value</span></span>  |
|---------|---------|
|<span data-ttu-id="953b6-163">언어</span><span class="sxs-lookup"><span data-stu-id="953b6-163">Language</span></span>     |   <span data-ttu-id="953b6-164">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="953b6-164">**JavaScript**</span></span>      |
|<span data-ttu-id="953b6-165">이름</span><span class="sxs-lookup"><span data-stu-id="953b6-165">Name</span></span>     |   <span data-ttu-id="953b6-166">**discover-sentiment-function**</span><span class="sxs-lookup"><span data-stu-id="953b6-166">**discover-sentiment-function**</span></span>      |
|<span data-ttu-id="953b6-167">큐 이름</span><span class="sxs-lookup"><span data-stu-id="953b6-167">Queue name</span></span>     |   <span data-ttu-id="953b6-168">**new-feedback-q**</span><span class="sxs-lookup"><span data-stu-id="953b6-168">**new-feedback-q**</span></span>      |
|<span data-ttu-id="953b6-169">저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="953b6-169">Storage account connection</span></span>        |  <span data-ttu-id="953b6-170">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="953b6-170">**AzureWebJobsDashboard**</span></span>       |

![큐 트리거 항목에서 JavaScript를 선택한 Azure Functions 템플릿의 스크린샷.](../media-draft/new-function-dialog.png)

5. <span data-ttu-id="953b6-172">**만들기**를 선택하여 함수 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-172">Select **Create** to begin the function creation process.</span></span>

1. <span data-ttu-id="953b6-173">큐 트리거 함수 템플릿을 사용하여 선택한 언어로 함수가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-173">A function is created in your chosen language using the Queue Trigger function template.</span></span> <span data-ttu-id="953b6-174">이 모듈에서는 JavaScript로 함수를 구현하지만, [지원되는 모든 언어](https://docs.microsoft.com/azure/azure-functions/supported-languages)로 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-174">While we'll implement the function in JavaScript in this module, you can create a function in any [supported language](https://docs.microsoft.com/azure/azure-functions/supported-languages).</span></span>

<span data-ttu-id="953b6-175">만들기 프로세스가 완료되면 포털에서 코드 편집기가 열리고 *index.js* 페이지가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-175">When the create process is complete, the code editor opens in the portal and loads the *index.js* page.</span></span> <span data-ttu-id="953b6-176">이 파일은 함수 논리를 작성하는 코드 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-176">This file is the code file where we write our function logic.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="953b6-177">사용해보기</span><span class="sxs-lookup"><span data-stu-id="953b6-177">Try it out</span></span>

<span data-ttu-id="953b6-178">지금까지 만든 부분을 테스트해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-178">Let's test what we have so far.</span></span> <span data-ttu-id="953b6-179">아직 코드를 작성하지 않았기 때문에 지금까지 구성한 내용이 실행되는지 확인하는 것이 테스트의 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-179">We haven't written any code yet, so this test is to make sure what we've configured so far, runs.</span></span>

1. <span data-ttu-id="953b6-180">코드 편집기 맨 위에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-180">Click **Run** at the top of the code editor.</span></span>

2. <span data-ttu-id="953b6-181">화면의 맨 아래에서 열리는 **로그** 탭을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-181">Observe the **Logs** tab that opens at the bottom of the screen.</span></span> <span data-ttu-id="953b6-182">모든 것이 계획대로 작동하면 다음 메시지와 유사한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-182">If everything works as planned, you'll see a message similar to the following message.</span></span>
<span data-ttu-id="953b6-183">![함수 호출이 성공할 때 표시되는 응답 메시지의 스크린샷.](../media-draft/func-default-run.PNG)</span><span class="sxs-lookup"><span data-stu-id="953b6-183">![Screenshot of response message of a successful call to our function.](../media-draft/func-default-run.PNG)</span></span>

<span data-ttu-id="953b6-184">**실행** 단추는 함수를 시작하고 기본 텍스트인 *샘플 큐 데이터*를 **테스트** 요청 창에서 함수로 전달했습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-184">The **Run** button started our function and passed *sample queue data*, the default text from the **Test** request window to our function.</span></span>

<span data-ttu-id="953b6-185">잘하셨습니다!</span><span class="sxs-lookup"><span data-stu-id="953b6-185">Nice work!</span></span> <span data-ttu-id="953b6-186">성공적으로 함수 앱에 큐 트리거 함수를 추가하고 예상대로 작동하는지 테스트를 마쳤습니다!</span><span class="sxs-lookup"><span data-stu-id="953b6-186">You've successfully added a Queue-triggered function to your function app and tested to make sure it's working as expected!</span></span> <span data-ttu-id="953b6-187">그 다음 연습에서는 함수에 기능을 더 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-187">We'll add more functionality to the function in the next exercise.</span></span>

 <span data-ttu-id="953b6-188">함수의 다른 파일인 *function.json* 구성 파일을 간단하게 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="953b6-188">Let's look briefly at the function's other file, the *function.json* config file.</span></span> <span data-ttu-id="953b6-189">이 파일의 구성 데이터는 다음 JSON 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-189">The configuration data from this file is shown in the following JSON listing.</span></span>

```json
{
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "new-feedback-q",
      "connection": "AzureWebJobsDashboard"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="953b6-190">보시다시피, 이 함수는 `queueTrigger` 형식의 **myQueueItem**이라는 트리거 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-190">As you can see, this function has a trigger binding named **myQueueItem** of type `queueTrigger`.</span></span> <span data-ttu-id="953b6-191">**new-feedback-q**라고 이름을 붙인 큐에 새 메시지가 도착하면 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-191">When a new message arrives in the queue we've named **new-feedback-q**, our function is called.</span></span> <span data-ttu-id="953b6-192">여기서는 myQueueItem 바인딩 매개 변수를 통해 새 메시지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-192">We reference the new message through the myQueueItem binding parameter.</span></span> <span data-ttu-id="953b6-193">바인딩은 일부 어려운 작업을 자동으로 처리합니다!</span><span class="sxs-lookup"><span data-stu-id="953b6-193">Bindings really do take care of some of the heavy lifting for us!</span></span>

<span data-ttu-id="953b6-194">그 다음 단계에서는 텍스트 분석 API 서비스를 호출하는 코드를 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-194">In the next step, we'll add code to call the Text Analytics API service.</span></span>

>[!TIP]
><span data-ttu-id="953b6-195">Azure Portal의 함수 패널 오른쪽에서 **파일 보기** 메뉴를 확장하여 index.js 및 function.json을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-195">You can see index.js and function.json by expanding the **View Files** menu on the right of the function panel in the Azure portal.</span></span> 

<span data-ttu-id="953b6-196">이 연습에서는 Azure Functions 인프라를 준비하는 방법을 다루었습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-196">This exercise was all about getting our Azure Functions infrastructure in place.</span></span> <span data-ttu-id="953b6-197">큐에 새 메시지가 도착하면 실행되는 [!INCLUDE [input-q](./q-name-input.md)] 함수를 만들어서 함수 앱에 호스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-197">We have a working function hosted in a function app that runs when a new message arrives in our queue that we've named [!INCLUDE [input-q](./q-name-input.md)].</span></span> <span data-ttu-id="953b6-198">진짜 재미있는 부분은 그 다음 연습에서 감정을 분석하는 Microsoft Cognitive 서비스를 호출할 때 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="953b6-198">The real fun begins in the next exercise, when we add code to call a Microsoft Cognitive Service to do sentiment analysis.</span></span>