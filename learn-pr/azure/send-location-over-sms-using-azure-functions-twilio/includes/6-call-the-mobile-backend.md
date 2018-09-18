<span data-ttu-id="6f084-101">모바일 앱이 실행되고 Azure 함수의 초기 버전이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="6f084-102">이 단원에서는 모바일 앱에서 Azure 함수를 호출하고 사용자 위치와 사용자가 SMS 메시지를 보내려는 전화 번호 목록을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="6f084-103">모바일 앱에서 Azure 함수 호출</span><span class="sxs-lookup"><span data-stu-id="6f084-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="6f084-104">`MainViewModel` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-104">Open the `MainViewModel`.</span></span>

1. <span data-ttu-id="6f084-105">이 클래스에서 `client`라는 전용 `HttpClient` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="6f084-106">`System.Net.Http` 네임스페이스에 대한 참조를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

1. <span data-ttu-id="6f084-107">함수의 기준 URL에 대한 상수 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="6f084-108">로컬 Azure Functions 런타임이 수신 대기 중인 주소로 이 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="6f084-109">Azure에 함수가 배포되면 이 상수를 Azure URL로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. <span data-ttu-id="6f084-110">`SendLocation` 메서드 내에서 위치를 찾은 후 해당 위치 및 사용자가 입력한 전화 번호 목록을 사용하여 `PostData`의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="6f084-111">`ImHere.Data` 네임스페이스에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > <span data-ttu-id="6f084-112">여기서는 전화 번호가 `Editor` 컨트롤에 줄당 하나씩 올바른 형식으로 입력되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="6f084-113">프로덕션 품질 앱에서는 하나 이상의 전화 번호가 올바른 형식으로 입력되었는지 확인하는 유효성 검사가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>

1. <span data-ttu-id="6f084-114">`PostData`를 JSON으로 직렬화하는 가장 쉬운 방법은 Newtonsoft.JSON NuGet 패키지를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.JSON NuGet package.</span></span> <span data-ttu-id="6f084-115">이전 단원에서 Xamarin.Essentials를 추가했을 때와 동일한 방식으로 `ImHere` 프로젝트에 이 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

1. <span data-ttu-id="6f084-116">`JsonConvert` 정적 클래스를 사용하여 `PostData`를 `string`으로 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="6f084-117">`Newtonsoft.Json` 네임스페이스에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="6f084-118">Azure 함수에 JSON으로 전달될 수 있도록 이 문자열을 `StringContent` 클래스로 인코드합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. <span data-ttu-id="6f084-119">이 데이터를 함수에 게시하고 결과를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="6f084-120">Azure 함수는 `/api/<function name>`을 사용하여 액세스하므로 로컬 Functions 런타임에서 선택한 포트가 7071이라고 가정하면 `SendLocation` 함수는 `http://localhost:7071/api/SendLocation`에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

1. <span data-ttu-id="6f084-121">결과에 따라 UI에 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="6f084-122">아래에는 새 필드 및 `SendLocation` 메서드의 전체 코드가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

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

## <a name="testing-it-out"></a><span data-ttu-id="6f084-123">테스트</span><span class="sxs-lookup"><span data-stu-id="6f084-123">Testing it out</span></span>

1. <span data-ttu-id="6f084-124">Azure 함수가 여전히 로컬에서 실행되고 있고 포트가 `SendLocation` 메서드와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

1. <span data-ttu-id="6f084-125">UWP 앱을 시작 앱으로 설정하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="6f084-126">**위치 보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-126">Click the **Send Location** button.</span></span> <span data-ttu-id="6f084-127">Functions 런타임 콘솔 창의 출력에 호출되는 함수가 표시되고 로깅에 생성된 URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![호출되는 함수 출력](../media/6-function-called.png)

1. <span data-ttu-id="6f084-129">URL 생성을 테스트하려면 콘솔에서 브라우저로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="6f084-130">현재 위치가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-130">It should show your current location.</span></span>

## <a name="summary"></a><span data-ttu-id="6f084-131">요약</span><span class="sxs-lookup"><span data-stu-id="6f084-131">Summary</span></span>

<span data-ttu-id="6f084-132">이 단원에서는 모바일 앱에서 Azure 함수를 호출하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-132">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="6f084-133">이 호출은 사용자 위치와 입력한 전화 번호를 JSON으로 전달했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-133">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="6f084-134">다음 단원에서는 Azure 함수를 Twilio에 바인딩하여 이 위치를 SMS 메시지로 보내겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f084-134">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>