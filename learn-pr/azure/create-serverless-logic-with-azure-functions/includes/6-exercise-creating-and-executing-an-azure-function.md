<span data-ttu-id="40965-101">이 연습에서는 기어 드라이브 예를 계속 사용하여 온도 서비스의 로직을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="40965-102">특히 HTTP 요청에서 데이터를 수신하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="40965-103">함수 요구 사항</span><span class="sxs-lookup"><span data-stu-id="40965-103">Function requirements</span></span>
<span data-ttu-id="40965-104">논리에 대한 몇 가지 요구 사항을 다음과 같이 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="40965-105">0-25 사이의 온도를 **OK**로 플래그 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="40965-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="40965-106">26-50 사이의 온도를 **CAUTION**으로 플래그를 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="40965-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="40965-107">50을 넘는 온도를 **DANGER**로 플래그 지정해야 함</span><span class="sxs-lookup"><span data-stu-id="40965-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="add-a-function-to-an-azure-function-app"></a><span data-ttu-id="40965-108">Azure 함수 앱에 함수 추가</span><span class="sxs-lookup"><span data-stu-id="40965-108">Add a function to an Azure function app</span></span>

<span data-ttu-id="40965-109">이전 단원에서 설명한 바와 같이, Azure는 함수 빌드를 시작하는 데 도움이 되는 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-109">As we discussed in the preceding unit, Azure provides templates that help you get started building functions.</span></span> <span data-ttu-id="40965-110">이 연습에서는 HttpTrigger 템플릿을 사용하여 온도 서비스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-110">In this exercise, we'll use the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="40965-111">Azure 계정을 사용하여 [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-111">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true) using your Azure account.</span></span>
1. <span data-ttu-id="40965-112">왼쪽 메뉴에서 **모든 리소스**를 선택한 후 **escalator-functions-group**을 선택하여 첫 번째 연습에서 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-112">Select the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="40965-113">그러면 그룹의 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40965-113">The resources for the group will then be displayed.</span></span> <span data-ttu-id="40965-114">**escalator-functions-xxxxxxx** 항목(번개 모양 아이콘으로도 표시됨)을 선택하여 이전 연습에서 만든 함수 앱에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-114">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="40965-115">![escalator-functions-group 및 생성한 함수 앱을 강조 표시하는 포털의 모든 리소스 스크린샷입니다.](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="40965-115">![Screenshot of All Resources in the portal highlighting the escalator-functions-group and the function app we created.](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="40965-116">왼쪽 메뉴에는 함수 앱 이름과 하위 메뉴가 표시되며, 하위 메뉴에는 ‘함수’, ‘프록시’ 및 ‘슬롯’의 세 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-116">The left-side menu displays your function app name and a submenu with three items - *Functions*, *Proxies*, and *Slots*.</span></span>  <span data-ttu-id="40965-117">첫 번째 함수 만들기를 시작하려면 탐색 트리에서 **함수** 위로 마우스를 이동할 때 나타나는 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-117">To start creating our first function, move your mouse over **Functions** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="40965-118">![클릭하면 함수 만들기 절차가 시작되는 함수 메뉴 항목 위로 마우스를 이동할 때 더하기 기호가 표시되는 스크린샷입니다.](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="40965-118">![Screenshot showing plus sign when you hover over the Functions menu item that, when clicked, starts the function creation procedure.](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="40965-119">다음 스크린샷에 나와 있는 것처럼, 빠른 시작 화면에서 **직접 만든 함수로 시작** 섹션에 있는 **사용자 지정 함수** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-119">In the Quickstart screen, select the **Custom function** link in the **Get started on your own** section as shown in the following screenshot.</span></span>
  <span data-ttu-id="40965-120">![“사용자 지정 함수” 단추가 강조 표시된 빠른 시작 화면 스크린샷입니다.](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="40965-120">![Screenshot of Quickstart screen with the "Custom function" button highlighted.](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="40965-121">다음 스크린샷에 나와 있는 것처럼, 화면에 표시된 템플릿 목록에서 HTTP 트리거 템플릿의 JavaScript 구현을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-121">From the list of templates displayed on the screen, select the JavaScript implementation of the HTTP trigger template as shown in the following screenshot.</span></span>
  <span data-ttu-id="40965-122">![HTTP 트리거 및 JavaScript 옵션이 강조 표시된 템플릿 목록의 스크린샷입니다.](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="40965-122">![Screenshot of template list, with the HTTP trigger and JavaScript option highlighted.](../images/6-httptrigger-template.png)</span></span>
1.  <span data-ttu-id="40965-123">나타나는 **새 함수** 대화 상자의 이름 필드에 **DriveGearTemperatureService**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-123">Enter **DriveGearTemperatureService** in the name field of the **New Function** dialog that appears.</span></span> <span data-ttu-id="40965-124">함수 이름을 지정했으면 다음 스크린샷에 설명된 대로 **생성** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40965-124">After you have named your function, press the **Create** button, as illustrated in te following screenshot.</span></span>
  <span data-ttu-id="40965-125">![이름 필드가 강조 표시되고 값이 “DriveGearTemperatureService”로 설정된 새 함수 양식의 스크린샷입니다.](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="40965-125">![Screenshot of New Function form, showing Name field highlighted and set with the value "DriveGearTemperatureService"](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="40965-126">함수 만들기가 완료되면 *index.js* 코드 파일의 내용과 함께 코드 편집기가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="40965-126">When your function creation completes, the code editor opens with the contents of the *index.js* code file.</span></span> <span data-ttu-id="40965-127">템플릿이 생성한 기본 코드가 다음 코드 조각에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-127">The default code that the template generated for us is listed in the following snippet.</span></span>

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

<span data-ttu-id="40965-128">함수는 HTTP 요청 쿼리 문자열을 통해 또는 요청 본문의 일부로 이름이 전달될 것이라고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-128">Our function expects a name to be passed in either through the HTTP request query string or as part of the request body.</span></span> <span data-ttu-id="40965-129">이 함수는 **Hello, {name}** 메시지를 반환하고, 요청에서 보낸 이름을 다시 에코하여 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-129">The function responds by returning the message  **Hello, {name}**, echoing back the name that was sent in the request.</span></span>

1. <span data-ttu-id="40965-130">소스 보기의 오른쪽에 두 개의 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40965-130">On the right-hand side of the source view, you'll see two tabs.</span></span> <span data-ttu-id="40965-131">\*\* 보기 파일에는 함수에 대한 코드 및 구성 파일이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="40965-131">The \*\*View file lists the code and config file for your function.</span></span>  <span data-ttu-id="40965-132">함수의 구성을 보려면 **function.json**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-132">Select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="40965-133">다음 코드 조각은 **function.json** 파일의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40965-133">The following snippet shows the contents of the **function.json** file.</span></span> <span data-ttu-id="40965-134">이 구성은 HTTP 요청을 수신할 때 함수가 실행되도록 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-134">This configuration declares that the function is runs when it receives an HTTP request.</span></span> <span data-ttu-id="40965-135">출력 바인딩은 응답이 HTTP 응답으로 전송될 것임을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-135">The output binding declares that the response will be sent as an HTTP response.</span></span>

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
> [!TIP]
> <span data-ttu-id="40965-136">이전 JSON 파일에서 트리거가 바인딩의 배열에 정의되어 있다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="40965-136">Notice in the preceding JSON file that the trigger is defined in an array of bindings.</span></span> <span data-ttu-id="40965-137">따라서 트리거는 실제로 특별한 유형의 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="40965-137">So, a trigger is actually a special type of binding.</span></span>

## <a name="run-our-function"></a><span data-ttu-id="40965-138">함수 실행</span><span class="sxs-lookup"><span data-stu-id="40965-138">Run our function</span></span>

> [!TIP]
> <span data-ttu-id="40965-139">**cURL**은 파일을 주고받는 데 사용할 수 있는 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="40965-139">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="40965-140">cURL.exe는 HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 등과 같은 많은 프로토콜을 지원합니다. 자세한 내용은 아래 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40965-140">cURL.exe supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 etc. For more information please refer the below links:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

<span data-ttu-id="40965-141">함수를 테스트하려면 명령줄에서 cURL을 사용하여 함수 URL로 HTTP 요청을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-141">To test our function, you can send an HTTP request to the function URL using cURL on the command line.</span></span> <span data-ttu-id="40965-142">함수의 엔드포인트 URL을 찾으려면 다음 스크린샷에 나와 있는 대로 함수 코드로 돌아가서 **함수 URL 가져오기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-142">To find the endpoint URL of the function, return to your function code and select the **Get function URL** link, as shown in the following screenshot.</span></span> <span data-ttu-id="40965-143">이 링크를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-143">Copy this link to your clipboard.</span></span>  

 ![포털의 함수 앱 섹션에 있는 코드 편집기의 스크린샷입니다.](../images/6-get-function-url.png)

<span data-ttu-id="40965-146">이 함수 URL을 사용하여 명령줄에서 다음 cURL 명령을 실행하고 URL을 자신의 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="40965-146">Using this function URL, run the following cURL command from your command line, replacing the URL with your own.</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

<span data-ttu-id="40965-147">다음 스크린샷은 명령줄의 기본 구현에서 수신한 응답의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40965-147">The following screenshot shows an example of the response you receive from the default implementation in the command line.</span></span>

![명령줄의 샘플 cUrl 명령 및 응답 스크린샷입니다.](../images/6-premadefunction-curl.png)

## <a name="add-business-logic-to-the-function"></a><span data-ttu-id="40965-149">함수에 비즈니스 논리 추가</span><span class="sxs-lookup"><span data-stu-id="40965-149">Add business logic to the function</span></span>

<span data-ttu-id="40965-150">이제 수신하는 온도 값을 확인하고 각각의 상태를 설정하는 함수에 비즈니스 논리를 추가할 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="40965-150">It's time to add the logic to the function that checks temperature readings that it receives and sets a status for each.</span></span>

<span data-ttu-id="40965-151">만든 함수는 다양한 온도 값을 수신할 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="40965-151">Our function is expecting an array of temperature readings.</span></span> <span data-ttu-id="40965-152">다음 JSON 코드 조각은 함수에 전송할 요청 본문의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="40965-152">The following JSON snippet is an example of the request body that we'll send to our function.</span></span> <span data-ttu-id="40965-153">각 `reading` 항목에는 ID, 타임스탬프 및 온도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-153">Each `reading` entry has an ID, timestamp, and temperature.</span></span>

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

<span data-ttu-id="40965-154">이번에는 함수의 기본 코드를 비즈니스 논리를 구현하는 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="40965-154">Next, we'll replace the default code in our function with the following code that implements our business logic.</span></span> 

1. <span data-ttu-id="40965-155">**index.js** 파일을 열고 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="40965-155">Open the **index.js** file, and replace it with the following code.</span></span>

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        req.body.readings.forEach(function(reading) {
            
            if(reading.temperature<=25) {
                reading.status = 'OK';
            } else if (reading.temperature<=50) {
                reading.status = 'CAUTION';
            } else {
                reading.status = 'DANGER'
            }
            context.log('Reading is ' + reading.status);
        });

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
<span data-ttu-id="40965-156">추가한 논리는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-156">The logic we added is straightforward.</span></span> <span data-ttu-id="40965-157">값의 배열을 반복하고 온도 필드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-157">We iterate over the array of readings and check the temperature field.</span></span> <span data-ttu-id="40965-158">해당 필드의 값에 따라 **OK**, **CAUTION** 또는 **DANGER**의 상태를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-158">Depending on the value of that field, we set a status of **OK**, **CAUTION**, or **DANGER**.</span></span> <span data-ttu-id="40965-159">그런 다음, 각 항목에 추가된 상태 필드와 함께 값의 배열을 다시 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-159">We then send back the array of readings with a status field added to each entry.</span></span>

<span data-ttu-id="40965-160">로그 문을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-160">Notice the log statements.</span></span> <span data-ttu-id="40965-161">함수가 실행되면 로그 창에 메시지가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="40965-161">When the function runs, these statements will add messages in the log window.</span></span>

## <a name="test-our-business-logic"></a><span data-ttu-id="40965-162">비즈니스 논리 테스트</span><span class="sxs-lookup"><span data-stu-id="40965-162">Test our business logic</span></span>

<span data-ttu-id="40965-163">이 경우 포털의 **테스트** 창을 사용하여 함수를 테스트해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-163">In this case, we're going to use the **Test** pane in the portal to test our function.</span></span>

1. <span data-ttu-id="40965-164">오른쪽 플라이아웃 메뉴에서 **테스트** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="40965-164">Open the **Test** window from the right-hand side flyout menu.</span></span>
1. <span data-ttu-id="40965-165">위의 샘플 요청을 요청 본문 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-165">Paste the sample request from above into the request body text box.</span></span> 
1. <span data-ttu-id="40965-166">**실행**을 선택하고 출력 창에서 응답을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40965-166">Select **Run** and view the response in the output pane.</span></span> <span data-ttu-id="40965-167">로그 메시지를 보려면 페이지의 맨 아래 플라이아웃에서 **로그** 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="40965-167">To see log messages, open the **Logs** tab in the bottom flyout of the page.</span></span> <span data-ttu-id="40965-168">다음 스크린샷은 출력 창의 예제 응답 및 **로그** 창의 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40965-168">The following screenshot shows an example response in the output pane and messages in the  **Logs** pane.</span></span>

![포털의 함수 인터페이스에 있는 “테스트” 및 “로그” 탭의 스크린샷입니다.](../images/6-portal-testing.png)

<span data-ttu-id="40965-171">상태 필드가 각 값에 올바르게 추가되었음을 출력 창에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-171">You can see in the output pane that our status field has been correctly added to each of the readings.</span></span>

<span data-ttu-id="40965-172">**모니터** 대시보드로 이동하면 Application Insights에 요청이 로그되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40965-172">If you navigate to the **Monitor** dashboard, you'll see that the request has been logged to Application Insights.</span></span>

![함수의 성공 메시지를 보여 주는 “모니터” 대시보드 일부분의 스크린샷입니다.](../images/6-app-insights.png)

