<span data-ttu-id="62fd5-101">데이터가 항상 영구적인 것은 아니며 특정 시점에는 삭제하고 싶을 때도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-101">Data is not always permanent, and there are times you would like to delete it at a specific time.</span></span> <span data-ttu-id="62fd5-102">예를 들어 인스턴트 메시징 응용 프로그램에서 사용자가 그룹 채팅의 표시 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-102">For example, in your instant messaging application, users can set the display name of the group chat.</span></span> <span data-ttu-id="62fd5-103">그러나 한 시간 뒤 이 이름을 재설정하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-103">However, you want the name to reset after one hour.</span></span> <span data-ttu-id="62fd5-104">시간 타이머를 설정하고 이름을 삭제하는 자체 서버 측 논리를 작성하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-104">You could accomplish this by writing your own server-side logic that set an hour timer and deleted the name.</span></span> <span data-ttu-id="62fd5-105">그러나 Azure Redis Cache는 추가 논리 작성 없이 자동으로 이를 수행하는 기능인 데이터 만료를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-105">However, Azure Redis Cache supports data expiration, which is a feature that does this automatically without writing additional logic.</span></span>

<span data-ttu-id="62fd5-106">여기에서 데이터 만료를 구현하는 일반적인 Redis 명령에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-106">Here, you'll learn about the common Redis commands to implement data expiration.</span></span>

## <a name="what-is-data-expiration"></a><span data-ttu-id="62fd5-107">데이터 만료란?</span><span class="sxs-lookup"><span data-stu-id="62fd5-107">What is data expiration?</span></span>

<span data-ttu-id="62fd5-108">데이터 만료는 일정 시간 후 캐시에서 자동으로 키와 값을 삭제할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-108">Data expiration is a feature that can automatically delete a key and value in the cache after a set amount of time.</span></span>

## <a name="why-use-data-expiration"></a><span data-ttu-id="62fd5-109">데이터 만료를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="62fd5-109">Why use data expiration?</span></span>

<span data-ttu-id="62fd5-110">데이터 만료는 일반적으로 저장하는 데이터가 짧은 기간 동안만 유효한 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-110">Data expiration is commonly used in situations where the data you're storing is short-lived.</span></span>  <span data-ttu-id="62fd5-111">이 데이터 만료는 Azure Redis Cache가 메모리 내 데이터베이스이고 디스크에 저장하는 것만큼 사용할 가용 메모리가 없기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-111">This is important because Azure Redis Cache is an in-memory database and you don't have as much memory available to use as you would if you were storing on disk.</span></span> <span data-ttu-id="62fd5-112">Azure Redis Cache에서는 저장소가 제한되므로 중요한 데이터만 저장하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-112">Since you have limited storage with Azure Redis Cache, you want to make sure you're only storing data that is important.</span></span> <span data-ttu-id="62fd5-113">오래 지속될 필요가 없는 데이터의 경우 만료를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-113">If the data doesn't need to be around for a long time, make sure you set an expiration.</span></span>

## <a name="how-to-use-data-expiration-in-azure-redis-cache"></a><span data-ttu-id="62fd5-114">Azure Redis Cache에서 데이터 만료를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="62fd5-114">How to use data expiration in Azure Redis Cache</span></span>

<span data-ttu-id="62fd5-115">Azure Redis Cache에서 데이터 만료를 구현 및 관리할 다양한 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-115">There are different commands to implement and manage data expiration in Azure Redis Cache:</span></span>

- <span data-ttu-id="62fd5-116">`EXPIRE`: 키 제한 시간(초) 설정</span><span class="sxs-lookup"><span data-stu-id="62fd5-116">`EXPIRE`: Sets the timeout of a key in seconds</span></span>
- <span data-ttu-id="62fd5-117">`PEXPIRE`: 키 제한 시간(밀리초) 설정</span><span class="sxs-lookup"><span data-stu-id="62fd5-117">`PEXPIRE`: Sets the timeout of a key in milliseconds</span></span>
- <span data-ttu-id="62fd5-118">`EXPIREAT`: 절대 Unix 타임스탬프를 사용하여 키 제한 시간(초) 설정</span><span class="sxs-lookup"><span data-stu-id="62fd5-118">`EXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in seconds</span></span>
- <span data-ttu-id="62fd5-119">`PEXPIREAT`: 절대 Unix 타임스탬프를 사용하여 키 제한 시간(밀리초) 설정</span><span class="sxs-lookup"><span data-stu-id="62fd5-119">`PEXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in milliseconds</span></span>
- <span data-ttu-id="62fd5-120">`TTL`: 키가 만료되기 전까지 남은 시간(초) 반환</span><span class="sxs-lookup"><span data-stu-id="62fd5-120">`TTL`: Returns the remaining time a key has to live in seconds</span></span>
- <span data-ttu-id="62fd5-121">`PTTL`: 키가 만료되기 전까지 남은 시간(밀리초) 반환</span><span class="sxs-lookup"><span data-stu-id="62fd5-121">`PTTL`: Returns the remaining time a key has to live in milliseconds</span></span>
- <span data-ttu-id="62fd5-122">`PERSIST`: 키가 만료되지 않음</span><span class="sxs-lookup"><span data-stu-id="62fd5-122">`PERSIST`: Makes a key never expire</span></span>

<span data-ttu-id="62fd5-123">가장 일반적인 명령은 `EXPIRE`이며 이 모듈 전체에서 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-123">The most common command is `EXPIRE`, and we'll use it throughout this module.</span></span>

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a><span data-ttu-id="62fd5-124">C# 및 ServiceStack.Redis를 사용한 데이터 만료의 예</span><span class="sxs-lookup"><span data-stu-id="62fd5-124">Example of data expiration using C# and ServiceStack.Redis</span></span>

<span data-ttu-id="62fd5-125">**ServiceStack.Redis** 같은 클라이언트 라이브러리를 사용할 때는 낮은 수준의 Azure Redis Cache 명령에 대해서는 염려할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-125">Remember, when using a client library like **ServiceStack.Redis**, we don't have to worry about remembering the low-level Azure Redis Cache commands.</span></span> <span data-ttu-id="62fd5-126">대신 간단한 C# 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-126">Instead, we can use simple C# methods.</span></span>

```csharp
public static void SetGroupChatName(string groupChatID, string chatName)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create a key for group chat display names
        string key = groupChatID + "displayName";

        //Set the group chat display name
        redisClient.SetValue(key, chatName);

        //Set the expiration for one hour
        redisClient.Expire(key, 3600);
    }
}
```

<span data-ttu-id="62fd5-127">Azure Redis Cache를 사용하면 데이터 만료를 통해 일정 시간이 지난 후 데이터를 자동으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-127">Azure Redis Cache allows you to delete data automatically after a set amount of time using data expiration.</span></span> <span data-ttu-id="62fd5-128">이 데이터 만료는 Azure Redis Cache가 메모리 내 데이터베이스이고 디스크에 데이터를 저장하는 것만큼의 가용 메모리가 없기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-128">This is important because Azure Redis Cache is an in-memory database, and you don't have as much memory available as you would with storing data on disk.</span></span> <span data-ttu-id="62fd5-129">저장할 데이터가 오랜 시간 동안 지속될 필요가 없는 경우 만료를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62fd5-129">If the data you're storing doesn't need to be around for a long time, make sure you set an expiration.</span></span>