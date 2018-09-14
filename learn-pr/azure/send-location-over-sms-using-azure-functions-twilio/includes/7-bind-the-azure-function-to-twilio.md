<span data-ttu-id="1185a-101">이제 모바일 앱이 완성되었으며, 해당 앱은 데이터를 역직렬화할 수 있는 Azure 함수로 사용자의 위치와 전화번호 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-101">At this point, the mobile app is complete and it can send the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="1185a-102">이 단원에서는 Azure 함수를 Twilio에 바인딩하여 SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="1185a-103">Azure Functions를 다른 서비스 즉, Azure의 서비스나 타사 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="1185a-104">바인딩이라고 하는 이러한 연결은 입력 바인딩과 출력 바인딩이라는 두 가지 형태로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="1185a-105">입력 바인딩은 함수에 데이터를 제공하고 출력 바인딩은 함수에서 데이터를 가져와 다른 서비스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="1185a-106">바인딩에 대한 내용은 [Azure Functions 바인딩 문서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

<span data-ttu-id="1185a-107">Visual Studio에서 만들어진 Azure Functions에 대한 바인딩은 매개 변수를 사용하여 함수에 정의되고 특성으로 데코레이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="1185a-108">Twilio에 Azure 함수 바인딩</span><span class="sxs-lookup"><span data-stu-id="1185a-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="1185a-109">Twilio를 통해 SMS 메시지를 보내려면 계정 SID(구독 ID)와 인증 토큰으로 구성된 출력 바인딩이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="1185a-110">이전 단원에서 로컬 Azure Functions 런타임이 계속 실행 중인 경우 해당 런타임을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="1185a-111">“Microsoft.Azure.WebJobs.Extensions.Twilio” NuGet 패키지를 `ImHere.Functions` 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="1185a-112">이 NuGet 패키지에는 바인딩 관련 클래스가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-112">This NuGet package contains the relevant classes for the binding.</span></span>

1. <span data-ttu-id="1185a-113">`messages`라는 `SendLocation` 정적 클래스의 정적 `Run` 메서드에 새 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="1185a-114">이 매개 변수에는 `ICollector<SMSMessage>` 유형이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-114">This parameter will have a type of `ICollector<SMSMessage>`.</span></span> <span data-ttu-id="1185a-115">`Twilio` 네임스페이스에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-115">You'll need to add a using directive for the `Twilio` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

1. <span data-ttu-id="1185a-116">새 `messages` 매개 변수를 `TwilioSms` 특성으로 데코레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-116">Decorate the new `messages` parameter with the `TwilioSms` attribute.</span></span> <span data-ttu-id="1185a-117">이 특성에서는 세 가지 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-117">This attribute has three parameters you need to set.</span></span>

    | <span data-ttu-id="1185a-118">설정</span><span class="sxs-lookup"><span data-stu-id="1185a-118">Setting</span></span>      |  <span data-ttu-id="1185a-119">값</span><span class="sxs-lookup"><span data-stu-id="1185a-119">Value</span></span>   | <span data-ttu-id="1185a-120">설명</span><span class="sxs-lookup"><span data-stu-id="1185a-120">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="1185a-121">**AccountSidSetting**</span><span class="sxs-lookup"><span data-stu-id="1185a-121">**AccountSidSetting**</span></span> | <span data-ttu-id="1185a-122">“TwilioAccountSid”</span><span class="sxs-lookup"><span data-stu-id="1185a-122">"TwilioAccountSid"</span></span> | <span data-ttu-id="1185a-123">Twilio 계정의 SID.</span><span class="sxs-lookup"><span data-stu-id="1185a-123">The SID for your Twilio account.</span></span> <span data-ttu-id="1185a-124">SID를 직접 설정하지 않으며, 이 매개 변수는 SID를 검색하는 데 사용될 함수 앱 설정의 값 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-124">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> |
    | <span data-ttu-id="1185a-125">**AuthTokenSetting**</span><span class="sxs-lookup"><span data-stu-id="1185a-125">**AuthTokenSetting**</span></span> | <span data-ttu-id="1185a-126">“TwilioAuthToken”</span><span class="sxs-lookup"><span data-stu-id="1185a-126">"TwilioAuthToken"</span></span> | <span data-ttu-id="1185a-127">Twilio 계정의 인증 토큰.</span><span class="sxs-lookup"><span data-stu-id="1185a-127">The Auth Token for your Twilio account.</span></span> <span data-ttu-id="1185a-128">이 매개 변수는 인증 토큰을 직접 설정하기 보다는 이를 검색하는 데 사용될 함수 앱 설정의 값 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-128">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> |
    | <span data-ttu-id="1185a-129">**From**</span><span class="sxs-lookup"><span data-stu-id="1185a-129">**From**</span></span> | <span data-ttu-id="1185a-130">Twilio 전화 번호</span><span class="sxs-lookup"><span data-stu-id="1185a-130">Your Twilio phone number</span></span> | <span data-ttu-id="1185a-131">국가별 형식(+\<국가 코드\>\<전화 번호\>, 예를 들어 “+1555123456”)으로 SMS 메시지가 오는 Twilio 전화 번호.</span><span class="sxs-lookup"><span data-stu-id="1185a-131">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span> |

    <span data-ttu-id="1185a-132">Twilio 계정을 만들 때 메시지를 보낼 수 있는 전화 번호가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-132">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="1185a-133">이 전화 번호는 Twilio **전화 번호** 대시보드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-133">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span> <span data-ttu-id="1185a-134">Twilio 사이트 왼쪽 메뉴 아래쪽에 있는 줄임표를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-134">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="1185a-135">그런 다음, ‘슈퍼 네트워크->전화 번호’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-135">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="1185a-136">고정 아이콘을 사용하여 이 대시보드를 왼쪽 메뉴에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-136">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="1185a-137">Twilio 번호는 ‘번호 관리->활성 번호’ 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-137">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span> <span data-ttu-id="1185a-138">번호에서 공백을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-138">You'll need to remove any spaces from the number.</span></span>

    ![Twilio 번호 찾기](../media/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

1. <span data-ttu-id="1185a-140">함수 앱 설정은 `local.settings.json` 파일 내에서 로컬로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-140">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="1185a-141">`TwilioSMS` 특성에 전달된 설정 이름을 사용하여 이 JSON 파일에 Twilio 계정 SID 및 인증 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-141">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    <span data-ttu-id="1185a-142">\<SID\> 및 \<인증 토큰\>을 Twilio 대시보드의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-142">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > <span data-ttu-id="1185a-143">이러한 로컬 설정은 로컬에서 실행하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-143">These local settings will be only for running locally.</span></span> <span data-ttu-id="1185a-144">프로덕션 앱에서는 이러한 값이 로컬 개발 또는 테스트 계정 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-144">In a production app, these values would be your local development or test account credentials.</span></span> <span data-ttu-id="1185a-145">Azure에 Azure 함수가 배포되면 프로덕션 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-145">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>
    > <span data-ttu-id="1185a-146">코드를 소스 제어에 체크 인하는 경우 이러한 로컬 응용 프로그램 설정 값도 체크 인되므로 코드가 어떤 형식이든 오픈 소스이거나 공용인 경우 이러한 파일의 실제 값을 체크 인하지 않도록 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="1185a-146">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="1185a-147">SMS 메시지 만들기</span><span class="sxs-lookup"><span data-stu-id="1185a-147">Create the SMS messages</span></span>

<span data-ttu-id="1185a-148">`ICollector<SMSMessage>` 매개 변수는 `SMSMessage` 인스턴스 컬렉션이며 보낼 SMS 메시지를 수집하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-148">The `ICollector<SMSMessage>` parameter is a collection of `SMSMessage` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="1185a-149">함수 실행이 완료되면 이 컬렉션에 추가된 모든 `SMSMessage` 인스턴스가 Twilio에 전달되어 관련된 받는 사람에게 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-149">After the function has finished running, any instances of `SMSMessage` added to this collection are passed to Twilio and sent to the relevant recipients.</span></span>

1. <span data-ttu-id="1185a-150">`SendLocation` 함수에서 `PostData`의 전화 번호를 반복하는 코드를 추가하고 각각에 대한 SMS 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-150">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
    }
    ```

    <span data-ttu-id="1185a-151">메시지에는 보낼 전화 번호와 사용자의 위치에서 만들어진 Google Maps URL이 포함된 본문이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-151">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

1. <span data-ttu-id="1185a-152">각 메시지를 기록한 후에 `messages` 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-152">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="1185a-153">전체 `SendLocation` 메서드가 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-153">The complete `SendLocation` method is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                                AuthTokenSetting = "TwilioAuthToken",
                                                                From = "<your Twilio phone number>")]ICollector<SMSMessage> messages,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="test-it-out"></a><span data-ttu-id="1185a-154">테스트</span><span class="sxs-lookup"><span data-stu-id="1185a-154">Test it out</span></span>

1. <span data-ttu-id="1185a-155">`ImHere.Functions` 앱을 시작 프로젝트로 설정하고 디버깅 없이 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-155">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

1. <span data-ttu-id="1185a-156">`ImHere.UWP` 앱을 시작 프로젝트로 설정하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-156">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

1. <span data-ttu-id="1185a-157">고유한 전화 번호를 국가별 형식(+\<국가 코드\>\<전화 번호\>)으로 Xamarin.Forms 앱에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-157">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="1185a-158">Twilio 평가판 계정은 확인된 전화 번호로만 메시지를 보낼 수 있으므로 현재로서는 유료 계정으로 업그레이드하거나 다른 번호를 확인하지 않는 한 자신에게만 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-158">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

1. <span data-ttu-id="1185a-159">**위치 보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-159">Click the **Send Location** button.</span></span> <span data-ttu-id="1185a-160">SMS 메시지를 성공적으로 보낸 경우 Xamarin.Forms 앱에 “위치를 성공적으로 보냄” 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-160">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying, "Location sent successfully".</span></span>

    ![위치를 보냈음을 보여 주는 Xamarin.Forms 앱](../media/7-ui-location-sent.png)

1. <span data-ttu-id="1185a-162">Azure 함수 콘솔 로그에는 만들고 보내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-162">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="1185a-163">오류가 발생하면(예: 번호가 잘못된 형식인 경우) 여기에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-163">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![메시지를 보냈음을 보여 주는 Azure 함수 콘솔](../media/7-function-message-sent.png)

1. <span data-ttu-id="1185a-165">휴대폰에서 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-165">Check your phone for a message.</span></span> <span data-ttu-id="1185a-166">메시지의 링크를 따라 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-166">Follow the link in the message to see your location.</span></span>

    ![휴대폰에 수신된 SMS 메시지](../media/7-message-received.png)

## <a name="summary"></a><span data-ttu-id="1185a-168">요약</span><span class="sxs-lookup"><span data-stu-id="1185a-168">Summary</span></span>

<span data-ttu-id="1185a-169">이 단원에서는 Azure 함수에 대한 Twilio 바인딩을 만들고 사용자의 위치가 포함된 SMS 메시지를 로컬에서 실행되는 함수로 보내는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-169">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="1185a-170">다음 단원에서는 함수를 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1185a-170">In the next unit, you publish the function to Azure.</span></span>