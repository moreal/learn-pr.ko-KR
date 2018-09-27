이제 모바일 앱이 완성되었으며, 해당 앱은 데이터를 역직렬화할 수 있는 Azure 함수로 사용자의 위치와 전화번호 목록을 보낼 수 있습니다. 이 단원에서는 Azure 함수를 Twilio에 바인딩하여 SMS 메시지를 보냅니다.

Azure Functions를 다른 서비스 즉, Azure의 서비스나 타사 서비스에 연결할 수 있습니다. 바인딩이라고 하는 이러한 연결은 입력 바인딩과 출력 바인딩이라는 두 가지 형태로 존재합니다. 입력 바인딩은 함수에 데이터를 제공하고 출력 바인딩은 함수에서 데이터를 가져와 다른 서비스로 보냅니다. 바인딩에 대한 내용은 [Azure Functions 바인딩 문서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true)에서 확인할 수 있습니다.

Visual Studio에서 만들어진 Azure Functions에 대한 바인딩은 매개 변수를 사용하여 함수에 정의되고 특성으로 데코레이트됩니다.

## <a name="bind-the-azure-function-to-twilio"></a>Twilio에 Azure 함수 바인딩

Twilio를 통해 SMS 메시지를 보내려면 계정 SID(구독 ID)와 인증 토큰으로 구성된 출력 바인딩이 필요합니다.

1. 이전 단원에서 로컬 Azure Functions 런타임이 계속 실행 중인 경우 해당 런타임을 중지합니다.

1. “Microsoft.Azure.WebJobs.Extensions.Twilio” NuGet v3.0.0-rc1 패키지를 `ImHere.Functions` 프로젝트에 추가합니다. **안정적인 버전에는 Twilio 바인딩과 관련된 버그가 있으므로 3.0.0 버전이 아닌 3.0.0-rc1 버전을 사용하세요**. 이 NuGet 패키지에는 바인딩 관련 클래스가 들어 있습니다.

1. `messages`라는 `SendLocation` 정적 클래스의 정적 `Run` 메서드에 새 매개 변수를 추가합니다. 이 매개 변수에는 `ICollector<CreateMessageOptions>` 유형이 포함됩니다. `Twilio.Rest.Api.V2010.Account` 네임스페이스에 `using` 지시문을 추가해야 합니다.

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,"get", "post", Route = null)]HttpRequestMessage req,
                                                ICollector<CreateMessageOptions> messages,
                                                ILogger log)
    ```

1. 다음과 같이 새 `messages` 매개 변수를 `TwilioSms` 특성으로 데코레이트합니다. 

      ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",AuthTokenSetting = "TwilioAuthToken", From = "+1xxxxxxxxx")]ICollector<CreateMessageOptions> messages,
    ```
    이 특성에서는 세 가지 매개 변수를 설정해야 합니다.

    * **AccountSidSetting** - `"TwilioAccountSid"`로 설정
  
        이는 이 모듈에서 앞서 기록한 Twilio 계정의 SID입니다. SID를 직접 설정하지 않으며, 이 매개 변수는 SID를 검색하는 데 사용될 함수 앱 설정의 값 이름입니다.

    * **AuthTokenSetting** - `"TwilioAuthToken"`로 설정

       이는 이 모듈에서 앞서 기록한 Twilio 계정의 인증 토큰입니다. 이 매개 변수는 인증 토큰을 직접 설정하기 보다는 이를 검색하는 데 사용될 함수 앱 설정의 값 이름입니다.

    * **From** - 이 모듈에서 앞서 기록한 Twilio 활성 전화 번호로 설정.

        국가별 형식(+\<국가 번호\>\<전화 번호\>, 예를 들어 “+1555123456”)으로 SMS 메시지가 오는 Twilio 전화 번호.

    > [!IMPORTANT]
    > 전화 번호에서 모든 공백을 제거해야 합니다.


1. 함수 앱 설정은 `local.settings.json` 파일 내에서 로컬로 구성할 수 있습니다. `TwilioSMS` 특성에 전달된 설정 이름을 사용하여 이 JSON 파일에 Twilio 계정 SID 및 인증 토큰을 추가합니다.

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "FUNCTIONS_WORKER_RUNTIME": "dotnet",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    \<SID\> 및 \<인증 토큰\>을 Twilio 대시보드의 값으로 바꿉니다.

    > [!NOTE]
    > 이러한 로컬 설정은 로컬에서 실행하는 경우에만 사용됩니다. 프로덕션 앱에서는 이러한 값이 로컬 개발 또는 테스트 계정 자격 증명입니다. Azure에 Azure 함수가 배포되면 프로덕션 값을 구성할 수 있습니다.

     > [!NOTE]
    > 코드를 소스 제어에 체크 인하는 경우 이러한 로컬 응용 프로그램 설정 값도 체크 인되므로 코드가 어떤 형식이든 오픈 소스이거나 공용인 경우 이러한 파일의 실제 값을 체크 인하지 않도록 주의하세요.
    

## <a name="create-the-sms-messages"></a>SMS 메시지 만들기

`ICollector<CreateMessageOptions>` 매개 변수는 `CreateMessageOptions` 인스턴스 컬렉션이며 보낼 SMS 메시지를 수집하는 데 사용됩니다. 함수 실행이 완료되면 이 컬렉션에 추가된 모든 `CreateMessageOptions` 인스턴스가 Twilio에 전달되고, 관련된 받는 사람에게 전송되는 메시지를 작성하는 데 사용됩니다.

1. `SendLocation` 함수에서 `PostData`의 전화 번호를 반복하는 코드를 추가하고 각각에 대한 SMS 메시지를 만듭니다. `Twilio.Types`에 using 지시문을 추가해야 합니다.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        PhoneNumber number = new PhoneNumber(toNo);
        CreateMessageOptions message = new CreateMessageOptions(number)
        {
            Body = $"I'm here! {url}"
        };
    }
    ```

    메시지에는 보낼 전화 번호와 사용자의 위치에서 만들어진 Google Maps URL이 포함된 본문이 있어야 합니다.

1. 각 메시지를 기록한 후에 `messages` 컬렉션에 추가합니다.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

전체 `SendLocation` 메서드가 아래에 나와 있습니다. `From` 매개 변수의 자리 표시자를 활성 전화 번호로 바꾸어야 합니다.

```cs
[FunctionName("SendLocation")]
public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                         "get", "post",
                                                         Route = null)]HttpRequest req,
                                            [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                       AuthTokenSetting = "TwilioAuthToken",
                                                       From = "+1xxxxxxxxx")] ICollector<CreateMessageOptions> messages,
                                            ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.LogInformation($"URL created - {url}");

    foreach (string toNo in data.ToNumbers)
    {
        PhoneNumber number = new PhoneNumber(toNo);
        CreateMessageOptions message = new CreateMessageOptions(number)
        {
            Body = $"I'm here! {url}"
        };
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }

    return new OkResult();
}
```

## <a name="test-it-out"></a>테스트

1. `ImHere.Functions` 앱을 시작 프로젝트로 설정하고 디버깅 없이 시작합니다.

1. `ImHere.UWP` 앱을 시작 프로젝트로 설정하고 실행합니다.

1. 고유한 전화 번호를 국가별 형식(+\<국가 코드\>\<전화 번호\>)으로 Xamarin.Forms 앱에 입력합니다. Twilio 평가판 계정은 확인된 전화 번호로만 메시지를 보낼 수 있으므로 현재로서는 유료 계정으로 업그레이드하거나 다른 번호를 확인하지 않는 한 자신에게만 메시지를 보낼 수 있습니다.

1. **위치 보내기** 단추를 클릭합니다. SMS 메시지를 성공적으로 보낸 경우 Xamarin.Forms 앱에 “위치를 성공적으로 보냄” 메시지가 표시됩니다.

    ![위치를 보냈음을 보여 주는 Xamarin.Forms 앱](../media/7-ui-location-sent.png)

1. Azure 함수 콘솔 로그에는 만들고 보내는 메시지가 표시됩니다. 오류가 발생하면(예: 번호가 잘못된 형식인 경우) 여기에 기록됩니다.

    ![메시지를 보냈음을 보여 주는 Azure 함수 콘솔](../media/7-function-message-sent.png)

1. 휴대폰에서 메시지를 확인합니다. 메시지의 링크를 따라 위치를 확인합니다.

    ![휴대폰에 수신된 SMS 메시지](../media/7-message-received.png)

    > [!TIP]
    > 표시되는 위치는 앱이 실행되고 있는 위치이므로 VM을 실행 중인 데이터 센터에서 가까워야 합니다. 로컬 장치에서 이 앱을 실행 중인 경우 사용자의 위치가 표시됩니다.

## <a name="summary"></a>요약

이 단원에서는 Azure 함수에 대한 Twilio 바인딩을 만들고 사용자의 위치가 포함된 SMS 메시지를 로컬에서 실행되는 함수로 보내는 방법을 배웠습니다. 다음 단원에서는 함수를 Azure에 게시합니다.
