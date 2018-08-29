현재 앱은 사용자의 위치를 가져오기 위해 작업 중이며 Azure 함수로 보내질 준비가 되어 있습니다. 이 단원에서는 Azure 함수를 빌드합니다.

## <a name="create-an-azure-functions-project"></a>Azure Functions 프로젝트 만들기

1. `ImHere` 솔루션을 마우스 오른쪽 단추로 클릭하고 ‘추가->새 프로젝트...’를 선택하여 이 솔루션에 새 프로젝트를 추가합니다.

2. 왼쪽 트리에서 ‘Visual C#->클라우드’를 선택한 후에 가운데 패널에서 *Azure Functions*를 선택합니다.

3. 프로젝트를 “ImHere.Functions”로 이름 지정하고 **확인**을 클릭합니다.

    ![새 프로젝트 추가 대화 상자](../media/5-add-new-functions-project.png)

4. **새 프로젝트** 구성 대화 상자에서 Functions 버전 설정을 *Azure Functions v1(.NET Framework)* 로 유지합니다. ‘HTTP 트리거’를 선택하고, 저장소 계정 설정을 ‘저장소 에뮬레이터’로 유지하고, 액세스 권한을 ‘익명’으로 설정합니다. 그런 후 **OK**를 클릭합니다.

    ![Azure 함수 프로젝트 구성 대화 상자](../media/5-configure-trigger.png)

새 프로젝트가 만들어지고 `Function1`이라는 기본 함수가 있습니다.

> 이 함수는 익명 액세스 권한으로 만들어졌습니다. Azure에 게시된 후에는 URL을 아는 사람은 누구나 이 함수를 호출할 수 있습니다. 실제 시나리오에서는 [Azure App Service 인증](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) 또는 [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c) 같은 특정 형태의 인증을 사용하여 보호합니다.

## <a name="create-the-function"></a>함수 만들기

Azure Functions 프로젝트는 단일 HTTP 트리거 함수 `Function1`을 사용하여 만들어집니다. 함수 자체는 `Function1` 클래스에서 정적 `Run` 메서드로 구현됩니다.

1. 솔루션 탐색기에서 파일 이름을 “Function1.cs”에서 “SendLocation.cs”로 바꿉니다. 코드 요소 `Function1`에 대한 모든 참조의 이름을 바꾸라는 메시지가 표시되면 **예**를 클릭합니다.

2. 특성에서 함수 이름을 “SendLocation”으로 바꿉니다.

    ```cs
    [FunctionName("SendLocation")]
    ```

3. 로거 대상의 정보 메시지가 쓰인 첫 번째 줄을 제외하고 함수의 콘텐츠를 삭제합니다.

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>모바일 앱과 함수 간에 데이터를 공유할 클래스 만들기

데이터가 Azure 함수로 보내지는 경우 JSON으로 보내집니다. 모바일 앱은 JSON으로 데이터를 직렬화하고 함수는 JSON에서 역직렬화합니다. 모바일 앱과 함수 간에 이 데이터를 일관성 있게 유지하려면 위치 및 전화 번호 데이터를 보관할 클래스가 포함된 새 프로젝트를 만듭니다. 그러면 앱 및 함수에서 이 프로젝트가 참조됩니다.

1. `ImHere` 솔루션을 마우스 오른쪽 단추로 클릭하고 ‘추가->새 프로젝트...’를 선택하여 이 솔루션 아래에 새 프로젝트를 만듭니다.

2. 왼쪽 트리에서 ‘Visual C#->.NET Standard’를 선택한 후에 가운데 패널에서 ‘클래스 라이브러리(.NET Standard)’를 선택합니다.

3. 프로젝트를 “ImHere.Data”로 이름 지정하고 **확인**을 클릭합니다.

    ![새 프로젝트 추가 대화 상자](../media/5-add-new-net-standard-project.png)

4. 자동 생성된 “Class1.cs” 파일을 삭제합니다.

5. 프로젝트를 마우스 오른쪽 단추로 클릭하고 ‘추가->클래스...’를 선택하여 `ImHere.Data` 프로젝트에 `PostData`라는 새 클래스를 만듭니다. 새 클래스의 이름을 “PostData”로 지정하고 **확인**을 클릭합니다.

6. 위도 및 경도에 `double` 속성을 추가하고 보낼 전화 번호의 `string[]` 특성도 추가합니다.

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. 프로젝트를 마우스 오른쪽 단추로 클릭하고 ‘추가->참조...’를 선택하여 이 프로젝트에 대한 참조를 `ImHere.Functions` 및 `ImHere` 프로젝트에 추가합니다. 왼쪽에 있는 트리에서 ‘프로젝트’를 선택한 후에 *ImHere.Data* 옆에 있는 상자를 선택합니다.

    ![프로젝트 참조 구성](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>함수로 보낸 데이터 보기

Azure 함수에서 `req` 매개 변수에는 만든 HTTP 요청이 포함되며 이 요청 내 데이터는 JSON 직렬화된 `PostData` 개체가 됩니다.

1. `ImHere.Functions` 프로젝트에서 `SendLocation` 클래스를 엽니다.

2. `PostData` 개체에 대한 HTTP 요청 콘텐츠를 보고 `ImHere.Data` 네임스페이스에 대한 using 지시문을 추가합니다.

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. `PostData`의 위도와 경도를 사용하여 Google Maps URL을 구성합니다.

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. 해당 URL을 로그합니다.

    ```cs
    log.Info($"URL created - {url}");
    ```

5. 200 상태 코드를 반환하여 오류 없이 완료된 함수를 표시합니다.

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

전체 함수는 아래에 표시되어 있습니다.

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a>로컬에서 Azure 함수 실행

함수는 로컬 저장소 계정 및 로컬 Azure Functions 런타임을 사용하여 로컬로 실행할 수 있습니다. 이 로컬 런타임을 사용하면 함수를 Azure에 배포하기 전에 테스트할 수 있습니다.

1. 솔루션 탐색기에서 `ImHere.Functions` 프로젝트를 마우스 오른쪽 단추로 클릭하고 ‘시작 프로젝트로 설정’을 선택합니다.

2. ‘디버그’ 메뉴에서 ‘디버그하지 않고 시작’을 선택합니다. 로컬 Azure Functions 런타임은 콘솔 창 내에서 실행되며 함수를 시작하여 `localhost`의 사용 가능한 포트에서 청취합니다.

    ![로컬에서 실행되는 Azure 함수](../media/5-function-running-locally.png)

3. 함수가 청취하는 포트를 기록해 둡니다. 다음 단원에서 모바일 앱을 테스트하는 데 이 포트 정보가 필요합니다. 위의 이미지에서 함수는 **7071** 포트에서 청취합니다.

    ```sh
    Listening on http://localhost:7071/
    ```

4. 다음 단원에서 모바일 앱을 테스트할 수 있도록 함수를 실행 중인 상태로 둡니다.

## <a name="summary"></a>요약

이 단원에서는 Visual Studio에서 Azure Functions 프로젝트를 만들고, 모바일 앱과 함수 간에 공유될 데이터 개체가 포함된 공유 프로젝트를 추가하고, 전달되는 데이터를 역직렬화하는 함수의 기본 구현을 만드는 방법을 배웠습니다. Azure 함수를 로컬에서 실행하는 방법도 배웠습니다. 다음 단원에서는 모바일 앱에서 Azure 함수를 호출합니다.