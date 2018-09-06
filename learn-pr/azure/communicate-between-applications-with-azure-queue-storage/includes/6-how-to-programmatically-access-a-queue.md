큐에는 송신기와 수신기에 해당 모양이 알려져 있는 데이터 패킷인 메시지가 들어 있습니다. 송신기는 큐를 만들고 메시지를 추가합니다. 수신기는 메시지를 검색하여 처리한 후 큐에서 해당 메시지를 삭제합니다. 다음 그림은 이 프로세스의 일반적인 흐름을 보여 줍니다.

![Azure 큐를 통한 일반적인 메시지 흐름을 보여 주는 그림입니다.](../media/6-message-flow.png)

`get` 및 `delete`는 별도의 작업입니다. 이 배열에서는 수신기의 잠재적 실패를 처리하고 _at-least-once delivery_(최소 1회 전송)라는 개념을 구현합니다. 수신기가 메시지를 받은 후에도 해당 메시지는 큐에 남아 있지만 30초 동안 보이지 않습니다. 수신기는 처리 중 작동이 중단되거나 전원 장애가 발생하는 경우 큐에서 메시지를 삭제하지 않습니다. 30초 후 메시지가 큐에 다시 표시되고 수신기의 다른 인스턴스는 완료될 때까지 메시지를 처리할 수 있습니다.

## <a name="the-azure-storage-client-library-for-net"></a>.NET용 Azure Storage 클라이언트 라이브러리

**.NET용 Azure Storage 클라이언트 라이브러리**는 다음과 같이 조작해야 할 각 개체를 나타내는 유형을 제공합니다.

- `CloudStorageAccount`는 Azure Storage 계정을 나타냅니다.
- `CloudQueueClient`는 Azure Queue Storage를 나타냅니다.
- `CloudQueue`는 큐 인스턴스 중 하나를 나타냅니다.
- `CloudQueueMessage`는 메시지를 나타냅니다.

이러한 클래스는 큐에 대한 프로그래밍 방식 액세스를 얻는 데 사용됩니다. 라이브러리에는 동기 메서드와 비동기 메서드가 둘 다 있습니다. 클라이언트 앱이 차단되지 않도록 비동기 버전을 사용하는 것이 좋습니다.

> [!NOTE]
> .NET용 Azure Storage 클라이언트 라이브러리는 **WindowsAzure.Storage** NuGet 패키지에서 사용할 수 있습니다. IDE, Azure CLI 또는 PowerShell `Install-Package WindowsAzure.Storage`를 통해 설치할 수 있습니다.

## <a name="how-to-connect-to-a-queue"></a>큐에 연결하는 방법

큐에 연결하려면 먼저 연결 문자열을 사용하여 `CloudStorageAccount`를 만듭니다. 그러면 결과 개체가 `CloudQueueClient`를 만들 수 있고, 여기서 다시 `CloudQueue` 인스턴스를 열 수 있습니다. 다음은 기본 코드 흐름을 보여 줍니다.

```csharp
CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudQueueClient client = account.CreateCloudQueueClient();

CloudQueue queue = client.GetQueueReference("myqueue");
```

`CloudQueue`를 만드는 것이 반드시 _실제_ 저장소 큐가 있다는 것을 의미하지는 않습니다. 그러나 이 개체를 사용하여 기존 큐를 만들고, 삭제하고, 확인할 수 있습니다. 위에 언급한 대로, 모든 메서드는 동기 및 비동기 버전을 둘 다 지원하지만 여기서는 `Task` 기반 비동기 버전만 사용합니다.

## <a name="how-to-create-a-queue"></a>큐를 만드는 방법

큐 만들기에는 공통 패턴을 사용합니다. 항상 송신기 응용 프로그램이 큐 만들기를 담당해야 합니다. 이렇게 하면 응용 프로그램이 보다 자체 포함되고 관리 설정으로부터 더 독립적인 상태로 유지됩니다. 

만들기가 간소화되도록 클라이언트 라이브러리는 필요한 경우 큐를 만드는 `CreateIfNotExistsAsync` 메서드를 표시하거나 큐가 이미 있는 경우 `false`를 반환합니다. 

일반적인 코드는 다음과 같습니다.

```csharp
CloudQueue queue;
//...

await queue.CreateIfNotExistsAsync();
```

> [!NOTE]
> 이 API를 사용하려면 저장소 계정에 대한 `Write` 또는 `Create` 권한이 있어야 합니다. **액세스 키** 보안 모델을 사용하는 경우 항상 true이지만, 큐에 대해 읽기 작업만 허용하는 다른 방법을 사용하여 계정에 대한 권한을 잠글 수 있습니다.

## <a name="how-to-send-a-message"></a>메시지를 보내는 방법

메시지를 보내려면 `CloudQueueMessage` 개체를 인스턴스화합니다. 해당 클래스에는 데이터를 메시지로 로드하는 오버로드된 생성자가 몇 개 있습니다. `string`을 사용하는 생성자를 사용합니다. 메시지를 만든 후 `CloudQueue` 개체를 사용하여 보냅니다.

일반적인 예는 다음과 같습니다.

```csharp
var message = new CloudQueueMessage("your message here");

CloudQueue queue;
//...

await queue.AddMessageAsync(message);
```

> [!NOTE]
> 큐의 전체 크기는 최대 500TB일 수 있으나 포함된 개별 메시지의 크기는 최대 64KB(Base64 인코딩을 사용하는 경우 48KB)일 수 있습니다. 더 큰 페이로드가 필요한 경우 큐와 Blob을 결합하여 메시지로 해당 URL을 실제 데이터(Blob으로 저장됨)에 전달할 수 있습니다. 이 방식에서는 단일 항목에 대해 최대 200GB를 큐에 넣을 수 있습니다.

## <a name="how-to-receive-and-delete-a-message"></a>메시지 수신 및 삭제 방법

수신기에서 다음 메시지를 받고 처리한 후 처리가 성공하면 해당 메시지를 삭제합니다. 간단한 예는 다음과 같습니다.

```C#
CloudQueue queue;
//...

CloudQueueMessage message = await queue.GetMessageAsync();

if (message != null)
{
    // Process the message
    //...

    await queue.DeleteMessageAsync(message);
}
```

이제 응용 프로그램에 이 새로운 지식을 적용해 보겠습니다.