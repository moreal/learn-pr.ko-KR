<span data-ttu-id="c96c6-101">이 연습에서는 기어 드라이브 예를 계속 사용하여 온도 서비스의 로직을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="c96c6-102">특히 HTTP 요청에서 데이터를 수신하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="c96c6-103">함수 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c96c6-103">Function requirements</span></span>
<span data-ttu-id="c96c6-104">논리에 대한 몇 가지 요구 사항을 다음과 같이 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="c96c6-105">0-25 사이의 온도를 **OK**로 플래그 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="c96c6-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="c96c6-106">26-50 사이의 온도를 **CAUTION**으로 플래그를 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="c96c6-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="c96c6-107">50을 넘는 온도를 **DANGER**로 플래그 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="c96c6-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="adding-a-function-to-an-azure-function-app"></a><span data-ttu-id="c96c6-108">Azure 함수 앱에 함수 추가</span><span class="sxs-lookup"><span data-stu-id="c96c6-108">Adding a function to an Azure function app</span></span>

<span data-ttu-id="c96c6-109">이미 배운 것처럼, Azure는 Azure Functions를 사용하는 방법을 학습할 때 도움을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-109">As we have already learned, Azure provides a helping hand when you're learning how to work with Azure Functions.</span></span> <span data-ttu-id="c96c6-110">Functions를 처음 사용할 수 있는 한 가지 훌륭한 기능은 다수의 템플릿 중 하나를 사용하여 함수를 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-110">One great feature to get your feet wet with Functions is to generate one using one of many templates.</span></span> <span data-ttu-id="c96c6-111">이 연습에서는 HttpTrigger 템플릿을 사용하여 온도 서비스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-111">In this exercise, you will be using the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="c96c6-112">Azure 계정을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-112">Sign in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
1. <span data-ttu-id="c96c6-113">왼쪽 메뉴에서 **모든 리소스**를 선택한 후 **escalator-functions-group**을 선택하여 첫 번째 연습에서 만든 리소스 그룹에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-113">Access the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="c96c6-114">그러면 그룹의 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-114">The resources for the group will then be displayed.</span></span> <span data-ttu-id="c96c6-115">**escalator-functions-xxxxxxx** 항목(번개 아이콘으로도 표시됨)을 선택하여 이전 연습에서 만든 함수 앱에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-115">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="c96c6-116">![함수 앱 액세스](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-116">![Access the function app](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="c96c6-117">블레이드에 함수 앱의 개요가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-117">The blade will show an overview of your function app.</span></span> <span data-ttu-id="c96c6-118">또한 왼쪽에는 정의된 함수, 프록시 또는 슬롯을 표시하는 탐색 트리도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-118">There is also a navigation tree on the left that shows any functions, proxies or slots that are defined.</span></span> <span data-ttu-id="c96c6-119">아직 함수가 없으므로 트리는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-119">We don't have a function yet, so this  will be empty.</span></span> <span data-ttu-id="c96c6-120">함수를 만들려면 탐색 트리에서 마우스를 **함수** 위에 놓았을 때 나타나는 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-120">To create a function, move your mouse over **Function** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="c96c6-121">![함수 탐색 추가](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-121">![Add function navigation](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="c96c6-122">기본으로 제공되는 빠른 시작 함수 양식에서 **직접 만든 함수로 시작** 섹션의 **사용자 지정 함수** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-122">In the quickstart premade function form, select the **Custom function** link in the **Get started on your own** section.</span></span>
  <span data-ttu-id="c96c6-123">![기본 제공 함수 양식](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-123">![Premade function form](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="c96c6-124">이제 템플릿 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-124">You are now presented with a list of templates.</span></span> <span data-ttu-id="c96c6-125">HTTP 트리거 템플릿의 JavaScript 구현을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-125">Select the JavaScript implementation of the HTTP trigger template.</span></span>
  <span data-ttu-id="c96c6-126">![HTTP 트리거 템플릿](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-126">![HTTP trigger template](../images/6-httptrigger-template.png)</span></span>
1. <span data-ttu-id="c96c6-127">블레이드가 나타나며, 여기서 생성할 템플릿을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-127">A blade will appear, allowing you to define what the template will generate.</span></span> <span data-ttu-id="c96c6-128">이 연습에서는 **DriveGearTemperatureService**라는 JavaScript 함수를 생성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-128">In this case, you are interested in generating a JavaScript function named **DriveGearTemperatureService**.</span></span> <span data-ttu-id="c96c6-129">함수 이름을 지정한 후에 **만들기** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-129">After you have named your function, press the **Create** button.</span></span>
  <span data-ttu-id="c96c6-130">![HTTP 트리거 양식 만들기](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-130">![Create HTTP trigger form](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="c96c6-131">잠시 후 함수에 대한 템플릿 소스 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-131">After a few moments, you will be presented with the templated source code for your function.</span></span> <span data-ttu-id="c96c6-132">기본 제공 함수는 이름이 전달되기를 기다렸다가 **안녕하세요, {name} 님**을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-132">The premade function expects a name to be passed in, and it will return **Hello, {name}**.</span></span>

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');

        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

1. <span data-ttu-id="c96c6-133">소스 뷰의 오른쪽에는 두 개의 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-133">On the right-hand side of the source view, you will see two tabs.</span></span> <span data-ttu-id="c96c6-134">함수를 지원하는 모든 파일을 **파일 보기** 탭에서 볼 수 있습니다. **function.json**을 선택하여 함수의 구성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-134">You are able to view all the files supporting the function in the **View files** tab. You can select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="c96c6-135">여기서는 출력 바인딩뿐만 아니라 정의된 httpTrigger를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-135">Here you can see the httpTrigger defined, as well as the output binding.</span></span> <span data-ttu-id="c96c6-136">이 구성은 함수가 HTTP 요청에 따라 시작된다는 것을 설명하고, 출력 바인딩은 응답이 HTTP 응답으로 전송됨을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-136">This configuration describes that the function is initiated by an HTTP request, and the output binding describes that the response will be sent as an HTTP response.</span></span>

    ```javascript
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

## <a name="running-the-premade-azure-function"></a><span data-ttu-id="c96c6-137">기본 제공 Azure 함수 실행</span><span class="sxs-lookup"><span data-stu-id="c96c6-137">Running the premade Azure function</span></span>

<span data-ttu-id="c96c6-138">함수를 실행하려면 명령 프롬프트에서 cURL의 HTTP 요청을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-138">To run the function, you can initiate an HTTP request from cURL from a command prompt.</span></span> <span data-ttu-id="c96c6-139">엔드포인트 URL을 찾으려면 함수 코드로 돌아가서 **함수 URL 가져오기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-139">To find the endpoint URL, return to your function code and select the **Get function URL** link.</span></span> <span data-ttu-id="c96c6-140">이 링크를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-140">Copy this link to your clipboard.</span></span>  <span data-ttu-id="c96c6-141">URL은 다음과 유사해야 합니다. https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![엔드포인트 URL 가져오기](../images/6-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-141">Your URL should look something similar to the following: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Get endpoint URL](../images/6-get-function-url.png)</span></span>

<span data-ttu-id="c96c6-142">이 URL로 cURL 명령을 실행하여 함수를 시작합니다(URL을 고유한 URL로 바꾸기).</span><span class="sxs-lookup"><span data-stu-id="c96c6-142">With that URL, run a cURL command to initiate your function (replacing the URL with your own):</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![기본 제공 함수 cURL 응답](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a><span data-ttu-id="c96c6-144">함수에 비즈니스 논리 추가</span><span class="sxs-lookup"><span data-stu-id="c96c6-144">Adding business logic to the function</span></span>

<span data-ttu-id="c96c6-145">만든 함수는 고객으로부터 다양한 온도 값을 받을 것을 예상하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-145">Our function is expecting an array of temperature readings from the customer.</span></span> <span data-ttu-id="c96c6-146">다음은 요청 본문의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-146">This is an example of the request body:</span></span>

```javascript
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

<span data-ttu-id="c96c6-147">기본 제공 함수 코드를 수정하여 필요한 비즈니스 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-147">Modify the premade function code to implement the required business logic.</span></span> <span data-ttu-id="c96c6-148">index.js 파일을 열고 다음 목록으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-148">Open the index.js file, and replace it with the following listing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        for(var i=0; i<req.body.readings.length; i++){
            var reading = req.body.readings[i];
            if(reading.temperature<=25){
                context.log('Reading is OK');
                reading.status = 'OK';
                continue;
            }
            if(reading.temperature<=50){
                context.log('Reading is CAUTION');
                reading.status = 'CAUTION';
                continue;
            }
            context.log('Reading is DANGER');
            reading.status = 'DANGER'
        }
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

<span data-ttu-id="c96c6-149">로그 문을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-149">Notice the log statements.</span></span> <span data-ttu-id="c96c6-150">함수가 실행되면 로그 창에 메시지가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-150">When the function runs, they will add messages in the log window.</span></span>

## <a name="testing-your-business-logic"></a><span data-ttu-id="c96c6-151">비즈니스 논리 테스트</span><span class="sxs-lookup"><span data-stu-id="c96c6-151">Testing your business logic</span></span>

<span data-ttu-id="c96c6-152">오른쪽 플라이아웃 메뉴에서 테스트 창을 열고 위의 샘플 요청을 요청 본문 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-152">Open the test window from the right-hand side flyout menu, and paste the sample request from above into the request body text box.</span></span> <span data-ttu-id="c96c6-153">**실행** 단추를 누르고 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-153">Press the **Run** button and view the output.</span></span> <span data-ttu-id="c96c6-154">맨 아래 플라이아웃 메뉴에서 로그 창을 열어 로그에 로깅 문을 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-154">You can also open the log window from the bottom flyout menu to see the logging statements in the log.</span></span>
<span data-ttu-id="c96c6-155">![비즈니스 논리 테스트](../images/6-portal-testing.png) 출력 창의 JSON 데이터를 통해, 온도 상태 필드가 각 표시 값에 올바르게 추가되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-155">![Testing the business Logic](../images/6-portal-testing.png) You can see from the JSON data in the output window that our temperature status field has been added to each of the readings correctly.</span></span> <span data-ttu-id="c96c6-156">또한 모니터 대시보드를 방문하여 Application Insights에 요청이 기록되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96c6-156">You may also visit the Monitor dashboard to see that the request has been logged to Application Insights.</span></span>
<span data-ttu-id="c96c6-157">![Application Insights의 요청](../images/6-app-insights.png)</span><span class="sxs-lookup"><span data-stu-id="c96c6-157">![Request in Application Insights](../images/6-app-insights.png)</span></span>
