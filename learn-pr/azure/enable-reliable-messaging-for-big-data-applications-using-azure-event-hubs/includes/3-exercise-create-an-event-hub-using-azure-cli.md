<span data-ttu-id="09a20-101">이제 새 이벤트 허브를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-101">You're now ready to create a new event hub.</span></span> <span data-ttu-id="09a20-102">이벤트 허브를 만든 후 Azure Portal을 사용하여 새 허브를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-102">After creating the event hub, you'll use the Azure portal to view your new hub.</span></span>

<span data-ttu-id="09a20-103">Azure CLI를 사용하여 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-103">You'll create an event hub using the Azure CLI.</span></span> <span data-ttu-id="09a20-104">이 연습에서는 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-104">For this exercise, use the Azure CLI 2.0.</span></span> 

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="09a20-105">Event Hubs 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="09a20-105">Create an Event Hubs namespace</span></span>

<span data-ttu-id="09a20-106">다음 단계를 수행하여 Azure Cloud Shell에서 지원하는 Bash 셸을 사용하여 Event Hubs 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-106">Use the following steps to create an Event Hubs namespace using Bash shell supported by Azure Cloud shell:</span></span>

1. <span data-ttu-id="09a20-107">Cloud Shell(Bash)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-107">Sign in to the Cloud Shell (Bash).</span></span>  

2. <span data-ttu-id="09a20-108">다음 명령을 사용하여 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-108">Create an Azure resource group using the following command:</span></span>
    ```azurecli
        az group create --name <resource group name> --location <location>
    ```
    |<span data-ttu-id="09a20-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="09a20-109">Parameter</span></span>      |<span data-ttu-id="09a20-110">설명</span><span class="sxs-lookup"><span data-stu-id="09a20-110">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="09a20-111">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-111">--name (required)</span></span>      |<span data-ttu-id="09a20-112">새 리소스 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-112">Enter a new resource group name.</span></span>|
    |<span data-ttu-id="09a20-113">--location(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-113">--location (required)</span></span>     |<span data-ttu-id="09a20-114">가장 가까운 Azure 데이터 센터의 위치를 입력합니다(예: westus).</span><span class="sxs-lookup"><span data-stu-id="09a20-114">Enter the location of your nearest Azure datacenter, for example, westus.</span></span>|
3. <span data-ttu-id="09a20-115">다음 명령을 사용하여 Event Hubs 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-115">Create the Event Hubs namespace using the following command:</span></span>
    ```azurecli
        az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <resource group name> -l <location>
    ```
    |<span data-ttu-id="09a20-116">매개 변수</span><span class="sxs-lookup"><span data-stu-id="09a20-116">Parameter</span></span>      |<span data-ttu-id="09a20-117">설명</span><span class="sxs-lookup"><span data-stu-id="09a20-117">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="09a20-118">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-118">--name (required)</span></span>      |<span data-ttu-id="09a20-119">Event Hubs 네임스페이스에 대한 6-50자 길이의 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-119">Enter a 6-50 characters-long unique name for your Event Hubs namespace.</span></span> <span data-ttu-id="09a20-120">이 이름에는 문자, 숫자 및 하이픈만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-120">The name should contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="09a20-121">문자로 시작해야 하고 문자 또는 숫자로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-121">It should start with a letter and end with a letter or number.</span></span>|
    |<span data-ttu-id="09a20-122">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-122">--resource-group (required)</span></span>  |<span data-ttu-id="09a20-123">1단계에서 만든 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-123">Enter the resource group you created in step 1.</span></span>
    |<span data-ttu-id="09a20-124">--l(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="09a20-124">--l (optional)</span></span>     |<span data-ttu-id="09a20-125">가장 가까운 Azure 데이터 센터의 위치를 입력합니다(예: westus).</span><span class="sxs-lookup"><span data-stu-id="09a20-125">Enter the location of your nearest Azure datacenter, for example, westus.</span></span>|
4. <span data-ttu-id="09a20-126">다음 명령을 사용하여 Event Hubs 네임스페이스에 대한 연결 문자열을 페치합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-126">Fetch the connection string for your Event Hubs namespace using the following command.</span></span> <span data-ttu-id="09a20-127">이벤트 허브를 사용하여 메시지를 보내고 받도록 응용 프로그램을 구성하려면 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-127">You'll need this to configure applications to send and receive messages using your event hub.</span></span>
    ```azurecli
        az eventhubs namespace authorization-rule keys list --resource-group <resource group name> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```
    |<span data-ttu-id="09a20-128">매개 변수</span><span class="sxs-lookup"><span data-stu-id="09a20-128">Parameter</span></span>      |<span data-ttu-id="09a20-129">설명</span><span class="sxs-lookup"><span data-stu-id="09a20-129">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="09a20-130">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-130">--resource-group (required)</span></span>  |<span data-ttu-id="09a20-131">1단계에서 만든 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-131">Enter the resource group you created in step 1.</span></span>|
    |<span data-ttu-id="09a20-132">--namespace-name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-132">--namespace-name (required)</span></span>      |<span data-ttu-id="09a20-133">2단계에서 만든 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-133">Enter the namespace you created in step 2.</span></span>|

    <span data-ttu-id="09a20-134">이 명령은 나중에 게시자 및 소비자 응용 프로그램을 구성하는 데 사용할 Event Hubs 네임스페이스에 대한 연결 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-134">This command returns the connection string for your Event Hubs namespace that you'll use later to configure your publisher and consumer applications.</span></span> <span data-ttu-id="09a20-135">나중에 사용할 수 있도록 다음 키의 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-135">Save the value of the following keys for later use.</span></span>
    - <span data-ttu-id="09a20-136">**primaryConnectionString**</span><span class="sxs-lookup"><span data-stu-id="09a20-136">**primaryConnectionString**</span></span>
    - <span data-ttu-id="09a20-137">**primaryKey**</span><span class="sxs-lookup"><span data-stu-id="09a20-137">**primaryKey**</span></span>

## <a name="create-an-event-hub"></a><span data-ttu-id="09a20-138">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="09a20-138">Create an event hub</span></span>

<span data-ttu-id="09a20-139">다음 단계에 따라 새 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-139">Use the following steps to create your new event hub:</span></span>

1. <span data-ttu-id="09a20-140">다음 명령을 사용하여 새 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-140">Create a new event hub using the following command:</span></span>
    ```azurecli
        az eventhubs eventhub create --name <event hub name> --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name>
    ```
    |<span data-ttu-id="09a20-141">매개 변수</span><span class="sxs-lookup"><span data-stu-id="09a20-141">Parameter</span></span>      |<span data-ttu-id="09a20-142">설명</span><span class="sxs-lookup"><span data-stu-id="09a20-142">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="09a20-143">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-143">--name (required)</span></span>  |<span data-ttu-id="09a20-144">이벤트 허브 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-144">Enter a name for your event hub.</span></span>|
    |<span data-ttu-id="09a20-145">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-145">--resource-group (required)</span></span>  |<span data-ttu-id="09a20-146">이전 절차에서 만든 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-146">Enter the resource group you created in the previous procedure.</span></span>|
    |<span data-ttu-id="09a20-147">--namespace-name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-147">--namespace-name (required)</span></span>      |<span data-ttu-id="09a20-148">이전 절차에서 만든 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-148">Enter the namespace you created in the previous procedure.</span></span>|
2. <span data-ttu-id="09a20-149">다음 명령을 사용하여 이벤트 허브의 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-149">View the details of your event hub using the following command:</span></span> 
    ```azurecli
        az eventhubs eventhub show --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name> --name <event hub name>
    ```
    |<span data-ttu-id="09a20-150">매개 변수</span><span class="sxs-lookup"><span data-stu-id="09a20-150">Parameter</span></span>      |<span data-ttu-id="09a20-151">설명</span><span class="sxs-lookup"><span data-stu-id="09a20-151">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="09a20-152">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-152">--resource-group (required)</span></span>  |<span data-ttu-id="09a20-153">이전 절차에서 만든 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-153">Enter the resource group that you created in the previous procedure.</span></span>|
    |<span data-ttu-id="09a20-154">--namespace-name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-154">--namespace-name (required)</span></span>      |<span data-ttu-id="09a20-155">이전 절차에서 만든 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-155">Enter the namespace you created in the previous procedure.</span></span>|
    |<span data-ttu-id="09a20-156">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="09a20-156">--name  (required)</span></span>|<span data-ttu-id="09a20-157">1단계에서 만든 이벤트 허브의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-157">Enter the name of the event hub you created in step 1.</span></span>|

## <a name="view-the-event-hub-in-the-azure-portal"></a><span data-ttu-id="09a20-158">Azure Portal에서 이벤트 허브 보기</span><span class="sxs-lookup"><span data-stu-id="09a20-158">View the event hub in the Azure portal</span></span>

<span data-ttu-id="09a20-159">다음 단계를 수행하여 Azure Portal에서 이벤트 허브를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-159">Use the following steps view your event hub in the Azure portal.</span></span>

1. <span data-ttu-id="09a20-160">[Azure Portal](https://portal.azure.com?azure-portal=true)의 위쪽에 있는 검색 창을 사용하여 Event Hubs 네임스페이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-160">Find your Event Hubs namespace using the Search bar at the top of the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="09a20-161">네임스페이스를 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-161">Click your namespace to open it.</span></span>
1. <span data-ttu-id="09a20-162">**Event Hubs 네임스페이스** > **엔터티**에서 **Event Hubs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-162">From **Event Hubs Namespace** > **ENTITIES**, click **Event Hubs**.</span></span>
    <span data-ttu-id="09a20-163">이벤트 허브에 대한 **활성** 상태와 기본값 **메시지 보존**(*7*) 및 **파티션 개수**(*4*)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-163">Your event hub displays with a status of **Active**, and default values for **Message Retention** (*7*) and **Partition Count** of (*4*).</span></span>

    ![Azure Portal에 표시된 이벤트 허브](../media-draft/3-event-hub.png)

## <a name="summary"></a><span data-ttu-id="09a20-165">요약</span><span class="sxs-lookup"><span data-stu-id="09a20-165">Summary</span></span>

<span data-ttu-id="09a20-166">이제 새 이벤트 허브를 만들었으며 게시자 및 소비자 응용 프로그램을 구성하는 데 필요한 모든 정보가 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="09a20-166">You've now created a new event hub, and you've all the necessary information ready to configure your publisher and consumer applications.</span></span>
