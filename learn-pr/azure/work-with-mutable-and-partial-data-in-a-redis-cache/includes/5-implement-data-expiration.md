여기에서 Azure Redis Cache에서 데이터에는 만료 시간을 추가 합니다.

## <a name="add-an-expiration-time"></a>만료 시간을 추가 합니다.

마지막 연습에서부터의 다음 코드로 **Program.cs**합니다.

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

둘 다에 만료 시간 (15 초)을 추가 해 보겠습니다 **MyKey1** 하 고 **MyKey2**합니다.

트랜잭션을 커밋하기 전에 다음 코드를 추가 합니다.

    ```csharp
    //Add an expiration time
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
    ```

이 코드에서는 합니다 **만료** 메서드는 부분을 합니다 **RedisNativeClient**. 메서드에 액세스 하려면은 개체를 먼저 캐스팅 해야 했습니다.

## <a name="verify-the-expiration"></a>만료 확인

데이터를 만료 하는 코드에 추가 했습니다 프로그램을 실행 하 고 Azure Redis Cache에서 데이터 제거 되도록 확인 하겠습니다.

1. 프로그램을 실행합니다.

    ```bash
    dotnet run
    ```
    
1. Azure portal에서 Azure Redis Cache 콘솔로 다시 전환 합니다.

1. 데이터가 여전히 인지를 확인 하려면 다음 명령을 실행 합니다.

    ```
    get MyKey1
    ```

1. 15 초 후 명령을 다시 실행 합니다. 데이터는 더 이상 존재 하는 것이 나타납니다.

    ![Nil 되 MyKey1의 값을 보여 주는 Azure Redis Cache 콘솔 스크린샷](../media/6-redis-console-data-expiration.png)