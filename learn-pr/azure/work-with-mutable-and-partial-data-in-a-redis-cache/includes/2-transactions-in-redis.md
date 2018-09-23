여러 작업의 동시 실행을 보장해야 하는 경우가 있습니다. 예를 들어, 인스턴트 메시징 응용 프로그램에서 사용자가 개별 사진, 개별 텍스트 메시지, 또는 사진과 텍스트 메시지를 한꺼번에 보낼 수 있습니다. 사용자가 사진과 텍스트 메시지를 한꺼번에 보내기로 하면 그룹의 다른 구성원이 동시에 이를 받을 수 있게 해야 합니다. 사진과 텍스트가 동시에 수신되지 않으면 별도의 메시지가 사진과 텍스트 메시지 사이에 전송될 수 있기 때문에 이렇게 하는 것이 중요합니다. 그러면 전체 대화에 혼동을 초래할 수 있습니다.

여기에서는 Azure Redis Cache에서 트랜잭션을 만들어 여러 작업이 함께 실행되게 보장하는 방법을 살펴보겠습니다.

## <a name="creating-and-running-transactions"></a>트랜잭션 만들기 및 실행

Redis의 트랜잭션은 그룹으로 실행될 여러 명령을 큐로 만들어서 작동합니다. 트랜잭션이 실행될 때 그 안에 큐 대기 중인 명령이(다른 클라이언트의 다른 명령이 인터리브되지 않고) 실행되도록 보장됩니다.

트랜잭션 블록을 시작하려면 `MULTI` 명령을 입력합니다. 추가 명령은 큐에 대기되며 즉시 실행되지 않습니다. `EXEC` 명령을 실행하면 큐에 대기 중인 모든 명령이 트랜잭션 단위로 실행합니다. 명령이 큐에 대기하고 있는 동안 열린 트랜잭션을 중단하기로 결정하는 경우 `DISCARD` 명령을 실행하면 큐에 대기하고 있는 _모든_ 명령을 실행하지 않고 트랜잭션 블록이 닫힙니다.

Redis 트랜잭션은 롤백 개념을 지원하지 않습니다. 구문이 잘못된 명령을 트랜잭션 블록에 큐로 대기시키면, 블록은 열린 상태로 유지되지만 `EXEC`을 사용하여 실행하려고 하면 자동으로 삭제됩니다. 실행 _중에_(`EXEC`가 호출된 후) 트랜잭션의 명령이 실패해도 트랜잭션이 중단되거나 롤백되지 않습니다. &mdash; Redis에서 모든 명령이 여전히 실행되고 트랜잭션이 성공적으로 완료된 것으로 간주됩니다.

## <a name="redis-transactions-with-servicestackredis"></a>ServiceStack.Redis를 사용한 Redis 트랜잭션

**ServiceStack.Redis**는 Azure Redis Cache와의 상호 작용을 위한 C# 클라이언트 라이브러리입니다.

ServiceStack.Redis의 트랜잭션은 `IRedisClient.CreateTransaction()`을 호출하여 생성됩니다. 반환되는 `IRedisTransaction` 개체에는 `QueueCommand()`를 통해 여러 명령이 큐로 대기될 수 있습니다. 트랜잭션 개체에서 `Commit()`을 호출하면 실행됩니다.

`IRedisTransaction` 개체는 삭제가 가능하며 `Commit()`을 호출하기 전에 삭제되면 `DISCARD` 명령을 자동으로 실행합니다. 이 기능은 C#의 `using` 블록에서 잘 작동합니다. 어떤 이유로든 트랜잭션을 커밋하지 않는 경우에는 Redis 연결을 계속 사용할 수 있도록 트랜잭션이 자동으로 삭제된다는 것을 신뢰할 수 있습니다.

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>C# 및 ServiceStack.Redis 클라이언트를 사용하여 트랜잭션 만들기

ServiceStack.Redis를 사용하여 그림 URL과 텍스트 메시지의 내용을 포함하는 메시지를 보낼 수 있는 트랜잭션을 만드는 예제는 다음과 같습니다.

```csharp
public bool SendPictureAndText(string groupChatID, string text, string pictureURL)
{
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, pictureURL));
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, text));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    return transactionResult;
}
```

트랜잭션은 사이에 다른 클라이언트의 작업 없이 여러 작업이 함께 실행되도록 보장합니다. 트랜잭션은 `MULTI` 명령을 사용하여 생성합니다. ServiceStack.Redis에서는 `CreateTransaction()` 명령을 사용합니다.