<span data-ttu-id="92b73-101">Azure Redis Cache는 메모리 내 데이터베이스이므로 메모리가 가장 중요한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-101">Memory is the most critical resource for Azure Redis Cache, because it's an in-memory database.</span></span> <span data-ttu-id="92b73-102">사용 가능한 메모리 크기를 초과하는 데이터를 추가하기 시작하면 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-102">You can run into problems when you begin adding data that exceeds the amount of memory available.</span></span> <span data-ttu-id="92b73-103">Azure Redis Cache는 메모리가 부족할 때 데이터를 처리하는 방법을 나타내는 제거 정책을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-103">Azure Redis Cache supports eviction policies, which indicate how data should be handled when you run out of memory.</span></span>

<span data-ttu-id="92b73-104">여기서는 최대 메모리 크기를 초과했을 때 데이터가 수행해야 할 작업을 결정하는 제거 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-104">Here, you'll set an eviction policy to determine what your data should do when you exceed the maximum amount of memory.</span></span>

## <a name="what-is-an-eviction-policy"></a><span data-ttu-id="92b73-105">제거 정책이란?</span><span class="sxs-lookup"><span data-stu-id="92b73-105">What is an eviction policy?</span></span>

<span data-ttu-id="92b73-106">제거 정책은 사용 가능한 최대 메모리 크기를 초과했을 때 데이터를 관리하는 방식을 결정하는 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-106">An eviction policy is a plan that determines how your data should be managed when you exceed the maximum amount of memory available.</span></span> <span data-ttu-id="92b73-107">예를 들어 제거 정책을 사용하여 Azure Redis Cache에 임의의 키를 삭제하도록 지시하여 새 데이터를 삽입할 공간을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-107">For example, using an eviction policy, you could tell Azure Redis Cache to delete a random key to make room for the new data being inserted.</span></span>

### <a name="types-of-eviction-policies"></a><span data-ttu-id="92b73-108">제거 정책 유형</span><span class="sxs-lookup"><span data-stu-id="92b73-108">Types of eviction policies</span></span>

<span data-ttu-id="92b73-109">Azure Redis Cache는 여섯 가지 제거 정책을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-109">There are six different eviction policies provided by Azure Redis Cache.</span></span> <span data-ttu-id="92b73-110">메모리 부족 시 데이터 삽입을 시도하면 이러한 모든 값이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-110">All of these values perform an action when you attempt to insert data when you're out of memory.</span></span>

* <span data-ttu-id="92b73-111">**noeviction:** 제거 정책이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-111">**noeviction:** No eviction policy.</span></span> <span data-ttu-id="92b73-112">데이터를 삽입하려고 하면 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-112">Returns an error message if you attempt to insert data.</span></span>

* <span data-ttu-id="92b73-113">**allkeys lru:** 가장 오래 전에 사용한 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-113">**allkeys-lru:** Removes the least recently used key.</span></span>

* <span data-ttu-id="92b73-114">**allkeys-random:** 임의의 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-114">**allkeys-random:** Removes a random key.</span></span>

* <span data-ttu-id="92b73-115">**volatile-lru:** 만료 설정이 있는 모든 키 중에 가장 오래 전에 사용한 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-115">**volatile-lru:** Removes the least recently used key out of all the keys with an expiration set.</span></span>

* <span data-ttu-id="92b73-116">**volatile-ttl:** 만료 설정을 기준으로 가장 짧은 시간을 갖는 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-116">**volatile-ttl:** Removes the key with the shortest time to live based on the expiration set for it.</span></span>

* <span data-ttu-id="92b73-117">**volatile-random:** 만료 설정이 있는 임의의 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-117">**volatile-random:** Removes a random key that has an expiration set.</span></span>

## <a name="how-to-set-an-eviction-policy"></a><span data-ttu-id="92b73-118">제거 정책 설정 방법</span><span class="sxs-lookup"><span data-stu-id="92b73-118">How to set an eviction policy</span></span>

<span data-ttu-id="92b73-119">Azure는 Azure Redis Cache에 대해 제거 정책을 설정하는 간단한 드롭다운 메뉴를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-119">Azure provides a simple drop-down menu to set the eviction policy for Azure Redis Cache.</span></span> <span data-ttu-id="92b73-120">**고급 설정**을 선택하고 **maxmemory-policy** 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-120">Select **Advanced Settings**, and use the **maxmemory-policy** drop-down menu.</span></span>

<span data-ttu-id="92b73-121">Azure Redis Cache에는 메모리가 중요하기 때문에 제거 정책을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-121">Since memory is critical to Azure Redis Cache, there is support for eviction policies.</span></span> <span data-ttu-id="92b73-122">제거 정책은 메모리가 부족할 때 새 데이터 삽입을 시도하면 기존 데이터를 어떻게 처리할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="92b73-122">An eviction policy determines what should be done with existing data when you're out of memory and attempt to insert new data.</span></span>