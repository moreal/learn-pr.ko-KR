<span data-ttu-id="48166-101">여기서는 Azure Redis Cache의 데이터에 만료 시간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-101">Here, you'll add an expiration time to our data in the Azure Redis Cache.</span></span>

## <a name="add-an-expiration-time"></a><span data-ttu-id="48166-102">만료 시간 추가</span><span class="sxs-lookup"><span data-stu-id="48166-102">Add an expiration time</span></span>

<span data-ttu-id="48166-103">지난 연습에서는 **Program.cs**에 다음 코드를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="48166-103">In the last exercise, we left off with the following code in **Program.cs**.</span></span>

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

<span data-ttu-id="48166-104">이제 **MyKey1** 및 **MyKey2** 모두에 15초 만료를 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48166-104">Let’s add an expiration of 15 seconds to both **MyKey1** and **MyKey2**.</span></span>

1. <span data-ttu-id="48166-105">트랜잭션을 커밋하기 전에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-105">Add the following code before you commit the transaction</span></span>

    ```csharp
    //Add an expiration time
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
    ```

    <span data-ttu-id="48166-106">이 코드에서는 **Expire** 메서드가 **RedisNativeClient**의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="48166-106">In this code, the **Expire** method is a part of the **RedisNativeClient**.</span></span> <span data-ttu-id="48166-107">메서드에 액세스하려면 먼저 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-107">To access the method, we must first cast our object.</span></span>

## <a name="verify-the-expiration"></a><span data-ttu-id="48166-108">만료 확인</span><span class="sxs-lookup"><span data-stu-id="48166-108">Verify the expiration</span></span>

<span data-ttu-id="48166-109">이제 데이터 만료를 위해 코드를 추가했으므로 프로그램을 실행하고 데이터가 Redis에서 제거되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-109">Now that we added the code to expire our data, lets run the program and check that the data is removed from Redis.</span></span>

1. <span data-ttu-id="48166-110">프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-110">Run the program.</span></span>

    ```bash
    dotnet run
    ```
    
1. <span data-ttu-id="48166-111">Azure Portal에서 Azure Redis 콘솔로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-111">Switch back to the Azure Redis Console in the Azure portal.</span></span>

1. <span data-ttu-id="48166-112">데이터가 여전이 있는지 확인하기 위해 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-112">To verify that the data is still there, issue the following command:</span></span>

    ```
    get MyKey1
    ```

1. <span data-ttu-id="48166-113">15초 후 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48166-113">After 15 seconds, issue the command again.</span></span> <span data-ttu-id="48166-114">데이터가 더 이상 없을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48166-114">You should see that the data is no longer there.</span></span>

    ![MyKey1 값이 nil이 되는 것을 보여 주는 Azure Redis 콘솔 스크린샷](../media/6-redis-console-data-expiration.png)