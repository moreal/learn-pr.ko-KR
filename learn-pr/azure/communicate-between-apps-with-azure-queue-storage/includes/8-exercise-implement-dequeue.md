이제 큐의 다음 메시지를 읽고, 처리한 후 큐에서 삭제하는 코드를 작성하여 응용 프로그램을 완료하려고 합니다. 

이 코드를 동일한 응용 프로그램에 배치하고, 매개 변수를 전달하지 않을 때 실행하려고 합니다. 그러나 지금 진행하는 뉴스 서비스 시나리오에서는 실제로 이 코드를 중간 계층 서버에 배치하여 기사를 처리할 것입니다.

## <a name="dequeue-a-message"></a>큐에서 메시지 제거

큐에서 다음 메시지를 검색하는 새 메서드를 추가해 보겠습니다.

1. Cloud Shell에서 `QueueApp` 폴더로 전환하고 `code .`를 입력하여 온라인 편집기를 엽니다.
 
1. `Program.cs` 소스 파일을 엽니다.

1. 매개 변수를 사용하지 않고 `Task<string>`을 반환하는 `ReceiveArticleAsync`라는 정적 메서드를 `Program` 클래스에 만듭니다. 이 메서드를 사용하여 큐에서 뉴스 기사를 끌어와 반환합니다.
    - 일부 비동기 `Task` 기반 메서드를 사용하게 되므로 계속 진행하면서 `async` 키워드를 메서드에 추가합니다.

    ```csharp
    static async Task<string> ReceiveArticleAsync()
    {
    }

1. All of the setup code to get a `CloudQueue` will be identical to what we did in the last exercise. Code duplication is a bad habit, even in samples so go ahead and, refactor the code that obtains the `CloudQueue` to a new method named `GetQueue` and change the `SendArticleAsync` to use your new method.
     - Make sure to leave the code that _creates_ the queue in the `SendArticleAsync` method; remember only the **publisher** should create the queue.

    ```csharp
    const string ConnectionString = ...;
    // ...

    static CloudQueue GetQueue()
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        return queueClient.GetQueueReference("newsqueue");
    }
    ```
    
1. `ReceiveArticleAsync` 메서드에서 새 `GetQueue` 메서드를 호출하여 큐 참조를 가져온 후 변수에 할당합니다.

1. 그런 다음, `CloudQueue` 개체에 대해 `ExistsAsync` 메서드를 호출합니다. 그러면 큐가 만들어졌는지와 관계없이 반환됩니다. 존재하지 않는 큐에서 메시지를 검색하려고 하면 API가 예외를 throw합니다.
    - 이 메서드는 비동기적이므로 `await`를 사용하여 반환 값을 가져옵니다.
    - `ReceiveArticleAsync` 메서드에 `async` 키워드가 이미 있어야 하지만, 없으면 지금 추가합니다.


1. `ExistsAsync`의 반환 값을 사용하는 `if` 블록을 추가합니다. 큐에서 블록으로 값을 읽는 코드를 추가하겠습니다. 값을 읽지 못했음을 나타내는 마지막 반환 문자열을 메서드에 추가합니다. 메서드는 다음과 같아야 합니다.

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
    }

    return "<queue empty or not created>";
}
```

1. `CloudQueue` 개체에 대해 `GetMessageAsync`를 호출하여 큐에서 첫 번째 `CloudQueueMessage`를 가져옵니다. 큐가 비어 있으면 반환 값은 `null`입니다.

1. Null이 아니면 `CloudQueueMessage` 개체에 `AsString` 속성을 사용하여 메시지 내용을 가져옵니다.

1. `CloudQueue` 개체에 대해 `DeleteMessageAsync`를 호출하여 큐에서 메시지를 삭제합니다.

최종 메서드 구현은 다음과 유사해야 합니다.

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
        CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
        if (retrievedArticle != null)
        {
            string newsMessage = retrievedArticle.AsString;
            await queue.DeleteMessageAsync(retrievedArticle);
            return newsMessage;
        }
    }

    return "<queue empty or not created>";
}
```

## <a name="call-the-receivearticleasync-method"></a>ReceiveArticleAsync 메서드 호출

마지막으로, 새 메서드를 호출하는 지원을 추가하겠습니다. 프로그램에 매개 변수를 전달하지 않을 때 이 작업을 수행합니다.

1. `Main` 메서드와 매개 변수를 찾기 위해 이전에 추가한 `if` 블록을 찾습니다.

1. `else` 조건을 추가하고 `ReceiveArticleAsync` 메서드를 호출합니다. 

1. 이 메서드는 비동기적이므로 일반적으로는 `await`를 사용하려고 합니다. 그러나 앞서 설명한 것처럼 모든 버전의 C#에서 작동하는 것은 아니므로 `Result` 속성을 사용하여 반환 값을 가져온 후 콘솔 창에 출력합니다.

코드는 다음과 유사해야 합니다.

```csharp
if (args.Length > 0)
{
    // ...
}
else
{
    string value = ReceiveArticleAsync().Result;
    Console.WriteLine($"Received {value}");
}
```

## <a name="execute-the-application"></a>응용 프로그램 실행

이제 코드가 완료되었습니다. 이제 메시지를 보내고 검색할 수 있습니다. 이를 테스트하려면 `dotnet run`을 사용하고 매개 변수를 전달하여 메시지를 전송하고, 매개 변수를 삭제하여 단일 메시지를 읽습니다.

큐가 없을 때 테스트하려면 Azure CLI를 사용하여 큐(및 모든 데이터)를 삭제할 수 있습니다. `<connection-string>` 매개 변수를 바꾸어야 합니다(또는 환경 변수 설정).

```azurecli
az storage queue delete --name newsqueue --connection-string <connection-string> 
```

다음번에 메시지를 추가할 때 큐가 다시 생성됩니다.