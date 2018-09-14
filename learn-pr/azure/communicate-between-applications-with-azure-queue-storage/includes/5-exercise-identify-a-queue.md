큐를 사용할 클라이언트 응용 프로그램을 만들어 보겠습니다. 그런 다음, 코드에 연결 문자열을 추가합니다.

## <a name="create-the-application"></a>응용 프로그램 만들기

Linux, macOS 또는 Windows에서 실행할 수 있는 .NET Core 응용 프로그램을 만듭니다. 이름을 **QueueApp**으로 지정하겠습니다. 간단히 하기 위해 큐를 통해 메시지를 보내고 받을 수 있는 단일 앱을 사용합니다.

1. `dotnet new` 명령을 사용하여 이름이 **QueueApp**인 새 콘솔 앱을 만듭니다. 오른쪽의 Cloud Shell에 명령을 입력하거나, 로컬로 작업하는 경우 터미널/콘솔 창에 명령을 입력할 수 있습니다. 그러면 단일 소스 파일(`Program.cs`)이 있는 단순 앱이 생성됩니다.

    ```azurecli
    dotnet new console -n QueueApp
    ```

1. 새로 생성된 `QueueApp` 폴더로 전환하고 앱을 빌드하여 문제가 없는지 확인합니다.

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a>연결 문자열 가져오기

앞서 말한 것처럼 연결 문자열은 Azure Portal에 있는 저장소 계정의 **설정 > 액세스 키** 섹션에서 사용할 수 있습니다.

Azure CLI 또는 PowerShell 도구를 통해 연결 문자열을 검색할 수도 있습니다. Azure CLI 명령을 사용해 보겠습니다. `<name>`을 만든 저장소 계정의 특정 이름으로 바꾸어야 합니다. 미리 알림이 필요한 경우 `az storage account list`를 사용할 수 있습니다.

```azurecli
az storage account show-connection-string --name <name> --resource-group ExerciseResources
```

이 명령은 연결 문자열이 포함된 JSON 블록을 반환합니다. 여기에는 저장소 계정 이름과 계정 키가 포함됩니다.

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a>응용 프로그램에 연결 문자열 추가

마지막으로 앱에서 저장소 계정에 액세스할 수 있도록 연결 문자열을 추가하겠습니다.

> [!WARNING]
> 간단히 하기 위해 **Program.cs** 파일에 연결 문자열을 배치합니다. 프로덕션 응용 프로그램에서는 이 연결 문자열을 안전한 위치에 저장해야 합니다. 서버 쪽에서는 Azure Key Vault를 사용하는 것이 좋습니다.

1. 터미널에서 `code .`을 입력하여 온라인 코드 편집기를 엽니다. 또는 사용자 고유의 작업을 수행 중인 경우에는 원하는 IDE를 사용할 수 있습니다. 뛰어난 플랫폼 간 IDE인 Visual Studio Code를 사용하는 것이 좋습니다.

1. 프로젝트에서 `Program.cs` 소스 파일을 엽니다.

1. `Program` 클래스에서 연결 문자열을 보유할 `const string` 값을 추가합니다. 이 값(텍스트 **DefaultEndpointsProtocol**로 시작)만 있으면 됩니다.

1. 파일을 저장합니다. 클라우드 편집기의 오른쪽 모서리에 있는 줄임표 “...”를 클릭하면 바로 가기 키도 표시됩니다.

코드는 다음과 유사해야 합니다(문자열 값이 사용자 계정에 고유함).

```csharp
...
namespace QueueApp
{
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https; ...";
        
        ...
    }
}
```

이제 이 시작 프로젝트 설정이 완료되었으므로 코드에서 큐로 작업을 수행하는 방법을 살펴보겠습니다. 모두가 _messages_로 시작됩니다.