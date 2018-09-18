여기서는 Azure Redis Cache의 데이터에 만료 시간을 추가합니다.

## <a name="add-an-expiration-time"></a>만료 시간 추가

지난 연습에서는 **Program.cs**에 다음 코드를 만들었습니다.

```csharp
using (RedisClient redisClient = new RedisClient(redisConnectionString))
{
    //Create the transaction
    var transaction = redisClient.CreateTransaction();

    //Add multiple operations to the transaction
    transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
    transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

    //Commit and get result of transaction
    var transactionResult = transaction.Commit();

    if(transactionResult)
        Console.WriteLine("Transaction committed");
    else
        Console.WriteLine("Transaction failed to commit");
}
```

이제 **MyKey1** 및 **MyKey2** 모두에 15초 만료를 추가할 것입니다.

1. 트랜잭션을 커밋하기 전에 다음 코드를 추가합니다.

    ```csharp
    //Add an expiration time
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
    ```

    이 코드에서는 **Expire** 메서드가 **RedisNativeClient**의 일부입니다. 메서드에 액세스하려면 먼저 개체를 만들어야 합니다.

## <a name="verify-the-expiration"></a>만료 확인

이제 데이터 만료를 위해 코드를 추가했으므로 프로그램을 실행하고 데이터가 Redis에서 제거되는지 확인합니다.

1. 프로그램을 실행합니다.

    ```bash
    dotnet run
    ```
    
1. Azure Portal에서 Azure Redis 콘솔로 다시 전환합니다.

1. 데이터가 여전이 있는지 확인하기 위해 다음 명령을 실행합니다.

    ```
    get MyKey1
    ```

1. 15초 후 명령을 다시 실행합니다. 데이터가 더 이상 없을 것입니다.

    ![MyKey1 값이 nil이 되는 것을 보여 주는 Azure Redis 콘솔 스크린샷](../media/6-redis-console-data-expiration.png)