<span data-ttu-id="e5e7d-101">여러 작업의 동시 실행을 보장해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-101">There are times where you must guarantee that multiple operations execute together.</span></span> <span data-ttu-id="e5e7d-102">예를 들어, 인스턴트 메시징 응용 프로그램에서 사용자가 개별 사진, 개별 텍스트 메시지, 또는 사진과 텍스트 메시지를 한꺼번에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-102">For example, in your instant messaging application, users can send: an individual picture, an individual text message, or a picture and text message together.</span></span> <span data-ttu-id="e5e7d-103">사용자가 사진과 텍스트 메시지를 한꺼번에 보내기로 하면 그룹의 다른 구성원이 동시에 이를 받을 수 있게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-103">When the user chooses to send a picture and text message together, we must ensure that other members of the group receive them at the same time.</span></span> <span data-ttu-id="e5e7d-104">사진과 텍스트가 동시에 수신되지 않으면 별도의 메시지가 사진과 텍스트 메시지 사이에 전송될 수 있고 그에 따라 전체 대화에 혼동을 초래할 수 있기 때문에 이렇게 하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-104">This is important because if a picture and text message are not received together, it’s possible that a separate message could be sent in between the picture and text message, which could make the overall conversation confusing.</span></span>

<span data-ttu-id="e5e7d-105">여기에서는 Redis에서 트랜잭션을 만들어 여러 작업이 동시에 실행되게 보장하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-105">Here, we'll look at how to create a transaction in Redis to guarantee multiple operations are executed together.</span></span>

## <a name="how-to-create-a-transaction"></a><span data-ttu-id="e5e7d-106">트랜잭션을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e5e7d-106">How to create a transaction</span></span>

<span data-ttu-id="e5e7d-107">트랜잭션을 만들려면 트랜잭션 블록이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-107">To create a transaction, you need to have a transaction block.</span></span> <span data-ttu-id="e5e7d-108">이것은 함께 실행될 명령을 포함하는 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-108">This is a queue that contains the commands that will be executed together.</span></span> <span data-ttu-id="e5e7d-109">`MULTI` 명령은 트랜잭션 블록을 만드는 데 사용되며 이후의 모든 명령은 원자성 실행을 위해 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-109">The `MULTI` command is used to create a transaction block and all subsequent commands are queued for atomic execution.</span></span>

## <a name="how-to-execute-a-transaction"></a><span data-ttu-id="e5e7d-110">트랜잭션을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="e5e7d-110">How to execute a transaction</span></span>

<span data-ttu-id="e5e7d-111">트랜잭션 블록에서 명령을 실행하려면 `EXEC` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-111">To execute the commands in a transaction block, you use the `EXEC` command.</span></span> <span data-ttu-id="e5e7d-112">그러면 큐의 모든 명령을 실행하고 연결 상태를 정상으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-112">This will execute all queued commands and restore the connection state to normal.</span></span> <span data-ttu-id="e5e7d-113">트랜잭션을 실행하지 않기로 결정한 경우 `DISCARD` 명령을 사용하여 트랜잭션 블록을 지우고 연결 상태를 정상으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-113">If you decide you don't want to execute a transaction, you can use the `DISCARD` command, which will clear out the transaction block and set the connection state to normal.</span></span>

<span data-ttu-id="e5e7d-114">Redis 트랜잭션은 롤백을 지원하지 않는다는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-114">One important thing to understand about Redis transactions is that they don't support rollbacks.</span></span> <span data-ttu-id="e5e7d-115">즉 트랜잭션 내부의 명령에 실패해도 나머지 명령은 여전히 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-115">This means that if a command inside a transaction fails, the remaining commands will still be executed.</span></span>

## <a name="what-is-servicestackredis"></a><span data-ttu-id="e5e7d-116">ServiceStack.Redis란?</span><span class="sxs-lookup"><span data-stu-id="e5e7d-116">What is ServiceStack.Redis?</span></span>

<span data-ttu-id="e5e7d-117">이전 모듈 **Redis를 통해 읽기 전용 데이터를 캐시하여 웹 응용 프로그램 최적화**에서는 **StackExchange.Redis** 클라이언트를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-117">In the previous module, **Optimize your web application by caching read-only data with Redis** we used the **StackExchange.Redis** client.</span></span> <span data-ttu-id="e5e7d-118">여기서는 또 다른 인기 클라이언트인 **ServiceStack.Redis**를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-118">Here, we're going to try out another popular client, **ServiceStack.Redis**.</span></span>

<span data-ttu-id="e5e7d-119">**ServiceStack.Redis**는 Redis 캐시와의 상호 작용을 위한 C# 클라이언트 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-119">**ServiceStack.Redis** is a C# client library for interacting with a Redis cache.</span></span> <span data-ttu-id="e5e7d-120">즉 하위 수준 Redis 명령 대신 C# 클래스와 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-120">This means that instead of using low-level Redis commands, we can use C# classes and methods.</span></span>

<span data-ttu-id="e5e7d-121">예를 들어 트랜잭션을 만들려면 보통은 Redis `MULTI` 명령을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-121">For example, to create a transaction, we normally must use the Redis `MULTI` command.</span></span> <span data-ttu-id="e5e7d-122">그러나 **ServiceStack.Redis**에서는 `CreateTransaction()` 메서드를 사용하여 트랜잭션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-122">However, using **ServiceStack.Redis** we can create a transaction using the `CreateTransaction()` method.</span></span>

```csharp
var transaction = redisClient.CreateTransaction();
```

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a><span data-ttu-id="e5e7d-123">C# 및 ServiceStack.Redis 클라이언트를 사용하여 트랜잭션 만들기</span><span class="sxs-lookup"><span data-stu-id="e5e7d-123">Create a transaction using C# and the ServiceStack.Redis client</span></span>

<span data-ttu-id="e5e7d-124">**ServiceStack.Redis**를 사용하여 사진 및 텍스트를 포함하는 메시지를 보낼 수 있는 트랜잭션을 만드는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-124">Here's an example of using **ServiceStack.Redis** to create a transaction that can send a message that includes a picture and text.</span></span>

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
<span data-ttu-id="e5e7d-125">트랜잭션은 여러 작업을 함께 실행되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-125">Transactions ensure that multiple operations are executed together.</span></span> <span data-ttu-id="e5e7d-126">`MULTI` 명령으로 트랜잭션을 만들 수 있지만 **ServiceStack.Redis** 같은 클라이언트 라이브러리를 사용하면 `CreateTransaction()` 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e7d-126">You create a transaction using the `MULTI` command, however, using a client library like **ServiceStack.Redis**, you can use the `CreateTransaction()` method.</span></span>