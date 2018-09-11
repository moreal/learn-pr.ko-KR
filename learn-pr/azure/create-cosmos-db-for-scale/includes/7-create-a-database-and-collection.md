<span data-ttu-id="0ef0a-101">이제 요청 단위를 사용하여 데이터베이스 처리량을 결정하는 방법과 파티션 키로 데이터베이스에 대한 규모 확장 전략을 만드는 방법을 이해했으므로 데이터베이스 및 컬렉션을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-101">Now that you understand how request units are used to determine database throughput and how the partition key creates the scale-out strategy for your database, you're ready to create your database and collection.</span></span>

## <a name="creating-your-database-and-collection"></a><span data-ttu-id="0ef0a-102">데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="0ef0a-102">Creating your database and collection</span></span>

1. <span data-ttu-id="0ef0a-103">Azure Portal의 Cosmos DB에서 **데이터 탐색기**를 선택한 다음, 도구 모음에서 **새 컬렉션** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-103">In the Azure Portal, select **Data Explorer** from your Cosmos DB resource and then click the **New Collection** button in the toolbar.</span></span>
    
    <span data-ttu-id="0ef0a-104">**컬렉션 추가** 영역이 맨 오른쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-104">The **Add Collection** area is displayed on the far right.</span></span> <span data-ttu-id="0ef0a-105">이 영역을 보려면 오른쪽으로 스크롤해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-105">You may need to scroll right to see it.</span></span>

    ![Azure Portal 데이터 탐색기, 컬렉션 추가 블레이드](../media/5-create-a-database-and-collection/azure-cosmosdb-data-explorer.png)

2. <span data-ttu-id="0ef0a-107">**컬렉션 추가** 페이지에서 새 컬렉션에 대한 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-107">In the **Add collection** page, enter the settings for the new collection.</span></span>

    <span data-ttu-id="0ef0a-108">설정</span><span class="sxs-lookup"><span data-stu-id="0ef0a-108">Setting</span></span> | <span data-ttu-id="0ef0a-109">제안 값</span><span class="sxs-lookup"><span data-stu-id="0ef0a-109">Suggested value</span></span> | <span data-ttu-id="0ef0a-110">설명</span><span class="sxs-lookup"><span data-stu-id="0ef0a-110">Description</span></span>
    --------|-----------------|-------------
    <span data-ttu-id="0ef0a-111">데이터베이스 ID</span><span class="sxs-lookup"><span data-stu-id="0ef0a-111">Database id</span></span>      | <span data-ttu-id="0ef0a-112">사용자</span><span class="sxs-lookup"><span data-stu-id="0ef0a-112">Users</span></span>         | <span data-ttu-id="0ef0a-113">새 데이터베이스의 이름으로 *Users*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-113">Enter *Users* as the name for the new database.</span></span> <span data-ttu-id="0ef0a-114">데이터베이스 이름은 1-255자여야 하며, /, \\, #,? 또는 후행 공백은 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-114">Database names must contain from 1 through 255 characters, and they cannot contain /, \\, #, ?, or a trailing space.</span></span>
    <span data-ttu-id="0ef0a-115">컬렉션 ID</span><span class="sxs-lookup"><span data-stu-id="0ef0a-115">Collection id</span></span>    | <span data-ttu-id="0ef0a-116">WebCustomers</span><span class="sxs-lookup"><span data-stu-id="0ef0a-116">WebCustomers</span></span>  | <span data-ttu-id="0ef0a-117">새 컬렉션의 이름으로 *WebCustomers*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-117">Enter *WebCustomers* as the name for your new collection.</span></span> <span data-ttu-id="0ef0a-118">컬렉션 ID에는 데이터베이스 이름과 동일한 문자 요구 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-118">Collection ids have the same character requirements as database names.</span></span>
    <span data-ttu-id="0ef0a-119">Storage 용량</span><span class="sxs-lookup"><span data-stu-id="0ef0a-119">Storage capacity</span></span> | <span data-ttu-id="0ef0a-120">Unlimited</span><span class="sxs-lookup"><span data-stu-id="0ef0a-120">Unlimited</span></span>     | <span data-ttu-id="0ef0a-121">기본값인 **Unlimited**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-121">Use the default value of **Unlimited**.</span></span> <span data-ttu-id="0ef0a-122">이 값은 데이터베이스의 저장소 용량이며 필요에 따라 데이터베이스의 규모를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-122">This value is the storage capacity of the database, and it enables your database to scale out as needed.</span></span>
    <span data-ttu-id="0ef0a-123">파티션 키</span><span class="sxs-lookup"><span data-stu-id="0ef0a-123">Partition key</span></span>    | <span data-ttu-id="0ef0a-124">UserId</span><span class="sxs-lookup"><span data-stu-id="0ef0a-124">UserId</span></span>        | <span data-ttu-id="0ef0a-125">수많은 쿼리가 고객 ID를 기준으로 하므로 UserID는 온라인 소매점 시나리오의 좋은 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-125">UserID is a good partition key for an online retail scenario, as so many queries are based around the customer ID.</span></span>
    <span data-ttu-id="0ef0a-126">처리량</span><span class="sxs-lookup"><span data-stu-id="0ef0a-126">Throughput</span></span>       |<span data-ttu-id="0ef0a-127">1000RU</span><span class="sxs-lookup"><span data-stu-id="0ef0a-127">1000 RU</span></span>        | <span data-ttu-id="0ef0a-128">처리량을 1000RU/s(초당 요청 단위)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-128">Change the throughput to 1000 request units per second (RU/s).</span></span> <span data-ttu-id="0ef0a-129">1000은 자동 크기 조정을 사용하도록 설정할 수 있는 최소 RU/s 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-129">1000 is the minimum RU/s value you can set to enable automatic scaling.</span></span>
    
    <span data-ttu-id="0ef0a-130">지금은 **프로비전 데이터베이스 처리량** 옵션을 확인하지 않고 컬렉션에 고유 키를 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-130">For now, don't check the **Provision database throughput** option, and don't add any unique keys to the collection.</span></span> 
    
3. <span data-ttu-id="0ef0a-131">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-131">Click **OK**.</span></span> <span data-ttu-id="0ef0a-132">데이터 탐색기는 새 데이터베이스 및 컬렉션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-132">The Data Explorer will display the new database and collection.</span></span>

    ![Azure Portal 데이터 탐색기, 새 데이터베이스 및 컬렉션 표시](../media/5-create-a-database-and-collection/azure-cosmos-db-new-collection.png)

## <a name="summary"></a><span data-ttu-id="0ef0a-134">요약</span><span class="sxs-lookup"><span data-stu-id="0ef0a-134">Summary</span></span>

<span data-ttu-id="0ef0a-135">이 단원에서는 파티션 키와 요청 단위에 대한 지식을 사용하여 비즈니스 요구 사항에 적합한 처리량 및 크기 조정 설정을 통해 데이터베이스 및 컬렉션을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ef0a-135">In this unit, you used your knowledge of partition keys and request units to create a database and collection with throughput and scaling settings appropriate for your business needs.</span></span>