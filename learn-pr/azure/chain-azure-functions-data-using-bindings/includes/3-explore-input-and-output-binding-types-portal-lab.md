<span data-ttu-id="6f368-101">다음은 이 연습에서 빌드할 대상에 대한 대략적인 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-101">The following is a high-level illustration of what we're going to build in this exercise.</span></span>

![HTTP 요청 및 응답과 각각의 req 및 res 바인딩 매개 변수를 보여주는 기본 HTTP 트리거의 일러스트레이션](../media/3-default-http-trigger-visual-small.PNG)

<span data-ttu-id="6f368-103">HTTP 요청을 받으면 시작되어 각 요청에 메시지를 보내 응답하는 함수를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-103">We'll create a function that will start when it receives an HTTP request and will respond to each request by sending back a message.</span></span> <span data-ttu-id="6f368-104">`req` 및 `res` 매개 변수는 각각 트리거 바인딩과 출력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-104">The parameters `req` and `res` are the trigger binding and output binding, respectively.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-function-app"></a><span data-ttu-id="6f368-105">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6f368-105">Create a function app</span></span>

<span data-ttu-id="6f368-106">이 모듈 전체에서 사용할 함수 앱을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-106">Let's create a function app that we'll use throughout this entire module.</span></span> <span data-ttu-id="6f368-107">함수 앱으로 함수를 논리 단위로 그룹화하여 리소스를 더욱 쉽게 관리, 배포 및 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-107">A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources.</span></span>

1. <span data-ttu-id="6f368-108">샌드박스를 활성화한 계정과 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-108">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="6f368-109">Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기** 단추를 선택한 다음, **계산** > **함수 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-109">Select the **Create a resource** button found on the upper left-hand corner of the Azure portal, then select **Compute** > **Function App**.</span></span>

1. <span data-ttu-id="6f368-110">함수 앱 속성을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-110">Set the function app properties as follows:</span></span>

    | <span data-ttu-id="6f368-111">속성</span><span class="sxs-lookup"><span data-stu-id="6f368-111">Property</span></span>     | <span data-ttu-id="6f368-112">제안 값</span><span class="sxs-lookup"><span data-stu-id="6f368-112">Suggested value</span></span>  | <span data-ttu-id="6f368-113">설명</span><span class="sxs-lookup"><span data-stu-id="6f368-113">Description</span></span>  |
    |--------------|------------------|--------------|
    | <span data-ttu-id="6f368-114">**앱 이름**</span><span class="sxs-lookup"><span data-stu-id="6f368-114">**App name**</span></span> | <span data-ttu-id="6f368-115">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="6f368-115">Globally unique name</span></span> | <span data-ttu-id="6f368-116">새 함수 앱을 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-116">Name that identifies your new function app.</span></span> <span data-ttu-id="6f368-117">유효한 문자는 `a-z`, `0-9` 및 `-`입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-117">Valid characters are `a-z`, `0-9`, and `-`.</span></span>  |
    | <span data-ttu-id="6f368-118">**구독**</span><span class="sxs-lookup"><span data-stu-id="6f368-118">**Subscription**</span></span> | <span data-ttu-id="6f368-119">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="6f368-119">Your subscription</span></span> | <span data-ttu-id="6f368-120">이 새 함수 앱이 만들어질 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-120">The subscription under which this new function app is created.</span></span> |
    | <span data-ttu-id="6f368-121">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="6f368-121">**Resource Group**</span></span>|  <span data-ttu-id="6f368-122">**기존 리소스 그룹 사용**을 선택하고 _<rgn>[샌드박스 리소스 그룹 이름]</rgn>_ 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-122">Select **Use existing** and choose _<rgn>[sandbox resource group name]</rgn>_</span></span> | <span data-ttu-id="6f368-123">함수 앱을 만들 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-123">Name of the resource group in which to create your function app.</span></span> |
    | <span data-ttu-id="6f368-124">**OS**</span><span class="sxs-lookup"><span data-stu-id="6f368-124">**OS**</span></span> | <span data-ttu-id="6f368-125">Windows</span><span class="sxs-lookup"><span data-stu-id="6f368-125">Windows</span></span> | <span data-ttu-id="6f368-126">함수 앱을 호스트하는 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-126">The operating system that hosts the function app.</span></span>  |
    | <span data-ttu-id="6f368-127">**호스팅**</span><span class="sxs-lookup"><span data-stu-id="6f368-127">**Hosting**</span></span> |   <span data-ttu-id="6f368-128">소비 계획</span><span class="sxs-lookup"><span data-stu-id="6f368-128">Consumption plan</span></span> | <span data-ttu-id="6f368-129">함수 앱에 리소스가 할당되는 방법을 정의하는 호스팅 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-129">Hosting plan that defines how resources are allocated to your function app.</span></span> <span data-ttu-id="6f368-130">기본 **소비 계획**에서 함수의 필요에 따라 리소스가 동적으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-130">In the default **Consumption Plan**, resources are added dynamically as required by your functions.</span></span> <span data-ttu-id="6f368-131">이 서버리스 호스팅 모델에서는 함수가 실행되는 시간 만큼만 요금을 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-131">In this serverless hosting model, you only pay for the time your functions run.</span></span>   |
    | <span data-ttu-id="6f368-132">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="6f368-132">**Storage account**</span></span> |  <span data-ttu-id="6f368-133">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="6f368-133">Globally unique name</span></span> |  <span data-ttu-id="6f368-134">함수 앱에 사용된 새 저장소 계정의 이름.</span><span class="sxs-lookup"><span data-stu-id="6f368-134">Name of the new storage account used by your function app.</span></span> <span data-ttu-id="6f368-135">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-135">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="6f368-136">이 대화 상자는 여러분이 앱에 지정한 이름에서 파생된 고유한 이름으로 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-136">This dialog populates the field with a unique name that is derived from the name you gave the app.</span></span> <span data-ttu-id="6f368-137">하지만 다른 이름이나 심지어는 기존 계정을 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-137">However, feel free to use a different name or even an existing account.</span></span> |
    | <span data-ttu-id="6f368-138">**위치**</span><span class="sxs-lookup"><span data-stu-id="6f368-138">**Location**</span></span> | <span data-ttu-id="6f368-139">목록에서 선택</span><span class="sxs-lookup"><span data-stu-id="6f368-139">Select from the list</span></span> | <span data-ttu-id="6f368-140">아래에 나열된 사용 가능한 위치 중에서 가장 가까운 것을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-140">Choose the nearest one from the available locations listed below.</span></span> |

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="6f368-141">**만들기**를 선택하여 함수 앱을 프로비전하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-141">Select **Create** to provision and deploy the function app.</span></span>

1. <span data-ttu-id="6f368-142">포털의 오른쪽 위 모서리에서 [알림] 아이콘을 선택하고 다음 메시지와 비슷한 **배포 진행 중** 메시지가 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-142">Select the Notification icon in the upper-right corner of the portal and watch for a **Deployment in progress** message similar to the following message.</span></span>

    ![함수 앱 배포가 진행 중이라는 알림](../media/3-func-app-deploy-progress-small.PNG)

1. <span data-ttu-id="6f368-144">배포에 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-144">Deployment can take some time.</span></span> <span data-ttu-id="6f368-145">따라서 알림 허브에 계속 머물면서 다음 메시지와 비슷한 **배포 성공** 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-145">So, stay in the notification hub and  watch for a **Deployment succeeded** message similar to the following message.</span></span>

    ![함수 앱 배포가 완료되었다는 알림](../media/3-func-app-deploy-success-small.PNG)

 1. <span data-ttu-id="6f368-147">함수 앱을 배포한 후 포털에서 **모든 리소스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-147">Once the function app is deployed, go to **All resources** in the portal.</span></span> <span data-ttu-id="6f368-148">함수 앱이 **App Service** 형식으로 나열되며 사용자가 지정한 이름을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-148">The function app will be listed with type **App Service** and has the name you gave it.</span></span> <span data-ttu-id="6f368-149">목록에서 함수 앱을 선택하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-149">Select the function app from the list to open it.</span></span>

    >[!TIP]
    ><span data-ttu-id="6f368-150">포털에서 앱 함수를 찾는 데 문제가 있는 경우, [포털에서 즐겨찾기에 함수 앱을 추가](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite)하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-150">If you are having trouble finding your function apps in the portal, find out how to [add function apps to your favorites in the portal](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).</span></span>

## <a name="create-a-function"></a><span data-ttu-id="6f368-151">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="6f368-151">Create a function</span></span>

<span data-ttu-id="6f368-152">함수 앱이 생겼으니, 이제 함수를 만들 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-152">Now that we have a function app, it's time to create a function.</span></span> <span data-ttu-id="6f368-153">함수는 트리거를 통해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-153">A function is activated through a trigger.</span></span> <span data-ttu-id="6f368-154">이 모듈에서는 HTTP 트리거를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-154">In this module, we'll use an HTTP trigger.</span></span>

1. <span data-ttu-id="6f368-155">새 함수 앱을 펼친 다음, 함수 컬렉션 위를 마우스로 가리키고, **함수** 옆에 있는 추가(**+**) 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-155">Expand your new function app, then hover over the functions collection and select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="6f368-156">이 작업은 함수 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-156">This action starts the function creation process.</span></span> <span data-ttu-id="6f368-157">다음 애니메이션에서는 이 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-157">The following animation illustrates this action.</span></span>

    ![사용자가 함수 메뉴 항목을 마우스로 가리키면 표시되는 더하기 기호의 애니메이션.](../media/3-func-app-plus-hover-small.gif)

1. <span data-ttu-id="6f368-159">**신속하게 시작하기** 페이지에서 **직접 시작하기** 섹션 아래의 **사용자 지정 함수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-159">On the **Get started quickly** page, select **Custom function** under the **Get started on your own** section.</span></span>

1. <span data-ttu-id="6f368-160">이것은 모든 템플릿을 나열하고 **HTTP 트리거** 템플릿을 찾아 언어에 대한 JavaScript를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-160">This will list all the templates, find the **HTTP Trigger** template and select JavaScript for the language.</span></span>

    ![JavaScript 링크가 강조 표시된 HTTP 함수 생성 상자의 스크린샷](../media/3-http-function.png)

1. <span data-ttu-id="6f368-162">**새 함수** 블레이드에서, 원하는 경우 이름을 변경하고 **권한 부여 수준**을 _함수_로 두고 나서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-162">On the **New Function** blade, change the name if you want, leave the **Authorization level** as _Function_, and click **Create**.</span></span>

1. <span data-ttu-id="6f368-163">새 함수에서 오른쪽 맨 위에 있는 **</> 함수 URL 가져오기**를 클릭하고 **기본값(함수 키)** 을 선택한 다음, **복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-163">In your new function, click the **</> Get function URL** link at the top right, select **default (Function key)**, and then select **Copy**.</span></span>

1. <span data-ttu-id="6f368-164">브라우저에서 새 탭의 주소 표시줄에 복사한 함수 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-164">Paste the function URL you copied into the address bar of a new tab in your browser.</span></span>

1. <span data-ttu-id="6f368-165">이 URL의 끝에 쿼리 문자열 값 `&name=Azure`을 추가한 다음, 키보드에서 엔터 키를 눌러 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-165">Add the query string value `&name=Azure` to the end of this URL, and then press Enter on your keyboard to execute the request.</span></span> <span data-ttu-id="6f368-166">브라우저에 표시된 함수에 의해 반환된 다음의 응답과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-166">You should see a response similar to the following response returned by the function displayed in your browser.</span></span>

    ```output
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Hello Azure</string>
    ```

<span data-ttu-id="6f368-167">지금까지 이 연습에서 확인한 것처럼 함수를 만들 때는 트리거 형식을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-167">As you can see from this exercise so far, you have to select a trigger type when you create a function.</span></span> <span data-ttu-id="6f368-168">모든 함수에는 하나의 트리거만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-168">Every function has one and only one trigger.</span></span> <span data-ttu-id="6f368-169">이 예제에서는 HTTP 트리거를 사용하기 때문에 HTTP 요청을 받아야 함수가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-169">In this example, we're using an HTTP trigger, which means that our function starts when it receives an HTTP request.</span></span> <span data-ttu-id="6f368-170">다음의 JavaScript 스크린샷에서 보이는 기본 구현은 쿼리 문자열이나 요청 본문에서 수신한 *이름* 매개 변수 값에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-170">The default implementation, shown in the following screenshot in JavaScript, responds with the value of the parameter *name* it received in the query string or body of the request.</span></span> <span data-ttu-id="6f368-171">문자열이 제공되지 않은 경우, 함수는 호출하는 모든 상대에게 이름 값 제공을 요청하는 메시지로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-171">If no string was provided, the function responds with a message that asks whomever is calling to supply a name value.</span></span>

![HTTP에서 트리거한 Azure 함수의 기본 JavaScript 구현 스크린샷](../media/3-default-http-trigger-implementation-small.PNG)

<span data-ttu-id="6f368-173">이 코드는 모두 이 함수 폴더의 **index.js** 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-173">All of this code is in the **index.js** file in this function's folder.</span></span> <span data-ttu-id="6f368-174">함수의 다른 파일인 **function.json** 구성 파일을 간단하게 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="6f368-174">Let's look briefly at the function's other file, the **function.json** config file.</span></span> <span data-ttu-id="6f368-175">구성 데이터는 다음 JSON 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-175">This configuration data is shown in the following JSON listing.</span></span>

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

<span data-ttu-id="6f368-176">보이는 것처럼 이 함수에는 `httpTrigger` 형식인 **req** 트리거 바인딩과 `HTTP` 형식인 **res** 출력 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-176">As you can see, this function has a trigger binding named **req** of type `httpTrigger` and an output binding named **res**  of type `HTTP`.</span></span> <span data-ttu-id="6f368-177">함수의 앞 코드에서는 **req** 매개 변수를 통해 수신되는 HTTP 요청의 페이로드에 액세스하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-177">In the preceding code for our function, we saw how we accessed the payload of the incoming HTTP request through our **req** parameter.</span></span> <span data-ttu-id="6f368-178">마찬가지로, **res** 매개 변수를 설정하여 간단하게 HTTP 응답을 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-178">Similarly, we sent an HTTP response simply by setting our **res** parameter.</span></span> <span data-ttu-id="6f368-179">바인딩은 일부 어려운 작업을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-179">Bindings really do take care of some of the heavy lifting for us.</span></span>

>[!TIP]
><span data-ttu-id="6f368-180">Azure Portal에서 함수 패널 오른쪽의 **파일 보기** 메뉴를 확장하면 **index.js** 및 **function.json** 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-180">You can see the **index.js** and **function.json** files by expanding the **View Files** menu at the right of the function panel in the Azure portal.</span></span>

### <a name="explore-binding-types"></a><span data-ttu-id="6f368-181">바인딩 형식 살펴보기</span><span class="sxs-lookup"><span data-stu-id="6f368-181">Explore binding types</span></span>

1. <span data-ttu-id="6f368-182">함수 항목에는 다음 스크린샷처럼 메뉴 항목 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-182">Notice under the function entry there is a set of menu items as shown in the following screenshot.</span></span>

    ![함수 앱 블레이드에서 함수 아래 표시된 메뉴 항목의 스크린샷](../media/3-func-menu-small.PNG)

1. <span data-ttu-id="6f368-184">통합 메뉴 항목을 선택하여 이 함수에 대한 통합 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-184">Select the Integrate menu item to open the integration tab for our function.</span></span> <span data-ttu-id="6f368-185">이 단위를 계속 진행해 온 경우 통합 탭이 다음 스크린샷과 매우 유사하게 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-185">If you have been following along with this unit, the integrate tab should look very similar to the following screenshot.</span></span>

    ![통합 UI 또는 탭의 스크린샷.](../media/3-func-integrate-tab-small.PNG)

    > [!NOTE]
    > <span data-ttu-id="6f368-187">이 스크린샷에서 보이는 것처럼 트리거와 출력 바인딩이 이미 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-187">We have already defined a trigger and an output binding, as shown in the screenshot.</span></span> <span data-ttu-id="6f368-188">또한 _둘_ 이상의 트리거는 추가할 수 없음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-188">You can see that we can't add more than _one_ trigger.</span></span> <span data-ttu-id="6f368-189">사실, 함수에 대한 트리거를 변경하려면 트리거를 먼저 삭제하고 새로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-189">In fact, to change the trigger for our function we would have to first delete the trigger and create a new one.</span></span> <span data-ttu-id="6f368-190">그러나 이 UI의 **입력**과 **출력** 섹션에서는 더 많은 바인딩을 추가하기 위해 더하기 기호(+)를 표시하므로 둘 이상의 입력 값을 수락하고 둘 이상의 출력 값을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-190">However, the **Inputs** and **Outputs** sections of this UI display a plus sign (+) to add more bindings so we can accept more than one input value and emit more than one output value.</span></span>

1. <span data-ttu-id="6f368-191">**입력** 열에서 **+ 새 입력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-191">Select **+ New Input** under the **Inputs** column.</span></span> <span data-ttu-id="6f368-192">다음 스크린샷에 표시된 것처럼 모든 가능한 입력 바인딩 형식 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-192">A list of all possible input binding types is displayed as shown in the following screenshot.</span></span>

    ![가능한 입력 바인딩 목록을 표시하는 스크린샷](../media/3-func-input-bindings-selector-small.PNG)

   <span data-ttu-id="6f368-194">잠시 각 입력 바인딩과, 솔루션에서 어떻게 사용할지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-194">Take a moment to consider each of these input bindings and how you might use them in a solution.</span></span> <span data-ttu-id="6f368-195">선택할 수 있는 목록이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-195">There are a lot to choose from.</span></span> <span data-ttu-id="6f368-196">더 많은 데이터 원본이 계속 지원되므로, 이 모듈을 읽은 시점에는 목록이 바뀌었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-196">This list might even have changed by the time you read this module, as we continue to support more data sources.</span></span>

1. <span data-ttu-id="6f368-197">나중에 모듈 뒷부분의 입력 바인딩 추가하기로 돌아가겠지만, 지금은 **취소**를 선택하여 이 목록을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-197">We'll get back to adding input bindings later in the module but, for now, select **Cancel** to dismiss this list.</span></span>

1. <span data-ttu-id="6f368-198">**출력** 열에서 **+ 새 출력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-198">Select **+ New Output** under the **Outputs** column.</span></span> <span data-ttu-id="6f368-199">다음의 스크린샷에서 보이는 것처럼 가능한 모든 출력 바인딩 형식 목록이 표시됩니다.\\</span><span class="sxs-lookup"><span data-stu-id="6f368-199">A list of all possible output binding types is displayed as shown in the following screenshot.\\</span></span>

    ![가능한 출력 바인딩 목록을 표시하는 스크린샷.](../media/3-func-output-bindings-selector-small.PNG)

   <span data-ttu-id="6f368-201">보이는 것처럼 여러 출력 바인딩 형식을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-201">As you can see, there are several output binding types at your disposal.</span></span> <span data-ttu-id="6f368-202">나중에 모듈 뒷부분의 출력 바인딩 추가하기로 돌아가겠지만, 지금은 **취소**를 선택하여 이 목록을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-202">We'll get back to adding output bindings later in the module but, for now, select **Cancel** to dismiss this list.</span></span>

<span data-ttu-id="6f368-203">지금까지 함수 앱을 만들어 함수를 추가하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-203">So far, we've learned how to create a function app and add a function to it.</span></span> <span data-ttu-id="6f368-204">HTTP 요청이 수행되면 실행되는 간단한 함수의 작동을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-204">We've seen a simple function in action, one that runs when an HTTP request is made to it.</span></span> <span data-ttu-id="6f368-205">Azure Portal UI와 함수를 사용할 수 있는 입력 및 출력 바인딩 형식도 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-205">We've also explored the Azure portal UI and types of input and output binding that are available to our functions.</span></span> <span data-ttu-id="6f368-206">다음 단원에서는 입력 바인딩을 사용해 데이터베이스에서 텍스트를 읽어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f368-206">In the next unit, we'll use an input binding to read text from a database.</span></span>