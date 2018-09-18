여러 작업의 동시 실행을 보장해야 하는 경우가 있습니다. 예를 들어, 인스턴트 메시징 응용 프로그램에서 사용자가 개별 사진, 개별 텍스트 메시지, 또는 사진과 텍스트 메시지를 한꺼번에 보낼 수 있습니다. 사용자가 사진과 텍스트 메시지를 한꺼번에 보내기로 하면 그룹의 다른 구성원이 동시에 이를 받을 수 있게 해야 합니다. 사진과 텍스트가 동시에 수신되지 않으면 별도의 메시지가 사진과 텍스트 메시지 사이에 전송될 수 있고 그에 따라 전체 대화에 혼동을 초래할 수 있기 때문에 이렇게 하는 것이 중요합니다.

여기에서는 Redis에서 트랜잭션을 만들어 여러 작업이 동시에 실행되게 보장하는 방법을 살펴보겠습니다.

## <a name="how-to-create-a-transaction"></a>트랜잭션을 만드는 방법

트랜잭션을 만들려면 트랜잭션 블록이 있어야 합니다. 이것은 함께 실행될 명령을 포함하는 큐입니다. `MULTI` 명령은 트랜잭션 블록을 만드는 데 사용되며 이후의 모든 명령은 원자성 실행을 위해 큐에 배치됩니다.

## <a name="how-to-execute-a-transaction"></a>트랜잭션을 실행하는 방법

트랜잭션 블록에서 명령을 실행하려면 `EXEC` 명령을 사용합니다. 그러면 큐의 모든 명령을 실행하고 연결 상태를 정상으로 복원합니다. 트랜잭션을 실행하지 않기로 결정한 경우 `DISCARD` 명령을 사용하여 트랜잭션 블록을 지우고 연결 상태를 정상으로 설정할 수 있습니다.

Redis 트랜잭션은 롤백을 지원하지 않는다는 점을 이해하는 것이 중요합니다. 즉 트랜잭션 내부의 명령에 실패해도 나머지 명령은 여전히 실행됩니다.

## <a name="what-is-servicestackredis"></a>ServiceStack.Redis란?

이전 모듈 **Redis를 통해 읽기 전용 데이터를 캐시하여 웹 응용 프로그램 최적화**에서는 **StackExchange.Redis** 클라이언트를 사용했습니다. 여기서는 또 다른 인기 클라이언트인 **ServiceStack.Redis**를 사용해 보겠습니다.

**ServiceStack.Redis**는 Redis 캐시와의 상호 작용을 위한 C# 클라이언트 라이브러리입니다. 즉 하위 수준 Redis 명령 대신 C# 클래스와 메서드를 사용할 수 있습니다.

예를 들어 트랜잭션을 만들려면 보통은 Redis `MULTI` 명령을 사용해야 합니다. 그러나 **ServiceStack.Redis**에서는 `CreateTransaction()` 메서드를 사용하여 트랜잭션을 만들 수 있습니다.

```csharp
var transaction = redisClient.CreateTransaction();
```

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>C# 및 ServiceStack.Redis 클라이언트를 사용하여 트랜잭션 만들기

**ServiceStack.Redis**를 사용하여 사진 및 텍스트를 포함하는 메시지를 보낼 수 있는 트랜잭션을 만드는 예제는 다음과 같습니다.

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
트랜잭션은 여러 작업을 함께 실행되게 합니다. `MULTI` 명령으로 트랜잭션을 만들 수 있지만 **ServiceStack.Redis** 같은 클라이언트 라이브러리를 사용하면 `CreateTransaction()` 메서드를 사용할 수 있습니다.