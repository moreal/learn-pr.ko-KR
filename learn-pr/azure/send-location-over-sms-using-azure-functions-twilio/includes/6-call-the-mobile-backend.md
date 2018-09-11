모바일 앱이 실행되고 Azure 함수의 초기 버전이 생성되었습니다. 이 단원에서는 모바일 앱에서 Azure 함수를 호출하고 사용자 위치와 사용자가 SMS 메시지를 보내려는 전화 번호 목록을 전달합니다.

## <a name="calling-the-azure-function-from-the-mobile-app"></a>모바일 앱에서 Azure 함수 호출

1. `MainViewModel` 파일을 엽니다.

1. 이 클래스에서 `client`라는 전용 `HttpClient` 필드를 추가합니다. `System.Net.Http` 네임스페이스에 대한 참조를 추가해야 합니다.

    ```cs
    HttpClient client = new HttpClient();
    ```

1. 함수의 기준 URL에 대한 상수 필드를 추가합니다. 로컬 Azure Functions 런타임이 수신 대기 중인 주소로 이 필드를 설정합니다. Azure에 함수가 배포되면 이 상수를 Azure URL로 변경할 수 있습니다.

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. `SendLocation` 메서드 내에서 위치를 찾은 후 해당 위치 및 사용자가 입력한 전화 번호 목록을 사용하여 `PostData`의 새 인스턴스를 만듭니다. `ImHere.Data` 네임스페이스에 대해 using 지시문을 추가해야 합니다.

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > 여기서는 전화 번호가 `Editor` 컨트롤에 줄당 하나씩 올바른 형식으로 입력되었다고 가정합니다. 프로덕션 품질 앱에서는 하나 이상의 전화 번호가 올바른 형식으로 입력되었는지 확인하는 유효성 검사가 있습니다.

1. `PostData`를 JSON으로 직렬화하는 가장 쉬운 방법은 Newtonsoft.JSON NuGet 패키지를 사용하는 것입니다. 이전 단원에서 Xamarin.Essentials를 추가했을 때와 동일한 방식으로 `ImHere` 프로젝트에 이 NuGet 패키지를 추가합니다.

1. `JsonConvert` 정적 클래스를 사용하여 `PostData`를 `string`으로 직렬화합니다. `Newtonsoft.Json` 네임스페이스에 대해 using 지시문을 추가해야 합니다. Azure 함수에 JSON으로 전달될 수 있도록 이 문자열을 `StringContent` 클래스로 인코드합니다.

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. 이 데이터를 함수에 게시하고 결과를 다시 가져옵니다.

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   Azure 함수는 `/api/<function name>`을 사용하여 액세스하므로 로컬 Functions 런타임에서 선택한 포트가 7071이라고 가정하면 `SendLocation` 함수는 `http://localhost:7071/api/SendLocation`에서 액세스할 수 있습니다.

1. 결과에 따라 UI에 메시지를 표시합니다.

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

아래에는 새 필드 및 `SendLocation` 메서드의 전체 코드가 나와 있습니다.

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a>테스트

1. Azure 함수가 여전히 로컬에서 실행되고 있고 포트가 `SendLocation` 메서드와 일치하는지 확인합니다.

1. UWP 앱을 시작 앱으로 설정하고 실행합니다. **위치 보내기** 단추를 클릭합니다. Functions 런타임 콘솔 창의 출력에 호출되는 함수가 표시되고 로깅에 생성된 URL이 표시됩니다.

    ![호출되는 함수 출력](../media-drafts/6-function-called.png)

1. URL 생성을 테스트하려면 콘솔에서 브라우저로 붙여넣습니다. 현재 위치가 표시되어야 합니다.

## <a name="summary"></a>요약

이 단원에서는 모바일 앱에서 Azure 함수를 호출하는 방법을 배웠습니다. 이 호출은 사용자 위치와 입력한 전화 번호를 JSON으로 전달했습니다. 다음 단원에서는 Azure 함수를 Twilio에 바인딩하여 이 위치를 SMS 메시지로 보내겠습니다.