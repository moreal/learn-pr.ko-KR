여러 작업을 함께 실행를 보장 해야 하는 경우가 있습니다. 예를 들어, 인스턴트 메시징 응용 프로그램에서 사용자 또는 보낼 수 있습니다 개별 그림, 개별 텍스트 메시지를 그림 및 텍스트 메시지를 함께 합니다. 그림 및 텍스트 메시지를 함께 보내려면을 선택 하는 경우에 그룹의 다른 구성원이 받도록 동시에 확인 해야 합니다. 이것이 중요 한 그림 및 텍스트 메시지를 함께 수신 되지 않은 경우이 가능 하므로 그림 및 텍스트 메시지 사이 별도 메시지를 보낼 수 없습니다. 혼란 스러운 전체 대화를 할 수는 있습니다.

여기에서 여러 작업을 함께 실행 됨을 보장 하기 위해 Azure Redis Cache에는 트랜잭션을 만드는 방법을 살펴보겠습니다.

## <a name="how-to-create-a-transaction"></a>트랜잭션을 만드는 방법

트랜잭션을 만들려면 트랜잭션 블록이 있고 해야 합니다. 이것이 함께 실행 될 명령을 포함 하는 큐입니다. `MULTI` 트랜잭션 블록을 만들려면 명령이 사용 되 고 이후의 모든 명령은 원자성 실행에 대 한 큐에 대기 됩니다.

## <a name="how-to-execute-a-transaction"></a>트랜잭션을 실행 하는 방법

사용할 트랜잭션 블록의 명령을 실행 하는 `EXEC` 명령입니다. 모든 큐에 대기 중인된 명령을 실행 되 고 연결 상태를 정상으로 복원 됩니다. 트랜잭션을 실행 하지 않을 경우 사용할 수는 `DISCARD` 명령인 트랜잭션 블록을 지우고 연결 상태가 정상으로 설정 됩니다.

Azure Redis Cache 트랜잭션에 대 한 알아야 할 중요 한 사항은 롤백 지원 하지 않는다는 것. 즉,이 트랜잭션 내에서 명령이 실패 하면 나머지 명령은 여전히 실행 됩니다.

## <a name="what-is-servicestackredis"></a>ServiceStack.Redis 란?

**ServiceStack.Redis** Azure Redis Cache를 사용 하 여 상호 작용 하기 위한 C# 클라이언트 라이브러리입니다. 즉, 하위 수준의 Azure Redis Cache 명령을 사용 하는 대신 사용할 수 있다는 C# 클래스 및 메서드. 예를 들어, 사용 하는 대신를 `MULTI` 및 `EXEC` 사용 하 여 트랜잭션을 실행 하는 명령 **ServiceStack.Redis** 을 만들겠습니다.는 `IRedisTransaction` 를 사용 하 여 개체를 `CreateTransaction()` 메서드.

```csharp
var transaction = redisClient.CreateTransaction();
```

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>C# 및 ServiceStack.Redis 클라이언트를 사용 하 여 트랜잭션을 만들려면

사용 예제는 다음과 같습니다 **ServiceStack.Redis** 그림 및 텍스트를 포함 하는 메시지를 보낼 수 있는 트랜잭션을 만들어야 합니다.

```csharp
public bool SendPictureAndText(string groupChatID, string text, string pictureURL)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, pictureURL));
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, text));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        return transactionResult;
    }
}
```
트랜잭션은 여러 작업을 함께 실행 됨을 확인 합니다. 사용 하 여 트랜잭션을 만든를 `MULTI` 명령입니다. 와 같은 클라이언트 라이브러리를 사용 하는 경우 **ServiceStack.Redis**를 사용할 수는 `CreateTransaction()` 메서드.