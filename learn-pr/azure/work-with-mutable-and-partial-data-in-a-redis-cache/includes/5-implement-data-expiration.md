여기서는 Azure Redis Cache의 데이터에 만료 시간을 추가합니다.

## <a name="add-an-expiration-time"></a>만료 시간 추가

지난 연습에서는 **Program.cs**에 다음 코드를 만들었습니다.

```csharp
bool transactionResult = false;

using (RedisClient redisClient = new RedisClient(redisConnectionString))
using (var transaction = redisClient.CreateTransaction())
{
    //Add multiple operations to the transaction
    transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
    transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

    //Commit and get result of transaction
    transactionResult = transaction.Commit();
}

if(transactionResult)
{
    Console.WriteLine("Transaction committed");
}
else
{
    Console.WriteLine("Transaction failed to commit");
}
```

이제 **MyKey1** 및 **MyKey2** 모두에 15초 만료를 추가해 보겠습니다.

트랜잭션을 커밋하기 전에 다음 코드를 추가합니다.

```csharp
//Add an expiration time
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
```

이 코드에서는 **Expire** 메서드가 **RedisNativeClient**의 일부입니다. 메서드에 액세스하려면 먼저 개체를 만들어야 합니다.

## <a name="verify-the-expiration"></a>만료 확인

이제 데이터를 만료시키는 코드를 추가했으므로 프로그램을 실행하고 데이터가 Azure Redis Cache에서 제거되는지 확인합니다.

1. 프로그램을 실행합니다.

    ```bash
    dotnet run
    ```

1. Azure Portal에서 Azure Redis Cache 콘솔로 다시 전환합니다.

1. 데이터가 여전이 있는지 확인하려면 다음 명령을 실행합니다.

    ```console
    get MyKey1
    ```

1. 15초 후 명령을 다시 실행합니다. 데이터가 더 이상 표시되지 않아야 합니다.

    ![MyKey1 값이 nil임을 보여주는 Azure Redis Cache 콘솔 스크린샷](../media/6-redis-console-data-expiration.png)