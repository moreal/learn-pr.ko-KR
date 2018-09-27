<span data-ttu-id="8d4be-101">이제 새 Event Hub를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-101">You're now ready to create a new Event Hub.</span></span> <span data-ttu-id="8d4be-102">Event Hub를 만든 후 Azure Portal을 사용하여 새 허브를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-102">After creating the Event Hub, you'll use the Azure portal to view your new hub.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-some-defaults-in-the-azure-cli"></a><span data-ttu-id="8d4be-103">Azure CLI에서 일부 기본값 설정</span><span class="sxs-lookup"><span data-stu-id="8d4be-103">Set some defaults in the Azure CLI</span></span>

<span data-ttu-id="8d4be-104">Cloud Shell에서 Azure CLI에 대한 일부 기본 값을 제공하는 것으로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-104">Let's start by providing some default values for the Azure CLI in the Cloud Shell.</span></span> <span data-ttu-id="8d4be-105">이렇게 하면 매번 입력하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-105">This will keep you from having to type these in every time.</span></span> <span data-ttu-id="8d4be-106">특히 _리소스 그룹_ 및 _위치_를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-106">In particular, let's set the _resource group_ and _location_.</span></span> <span data-ttu-id="8d4be-107">다음 목록에서 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-107">Select a location from the following list.</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="8d4be-108">그런 다음, Azure CLI로 다음 명령을 입력하여 가까운 위치로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-108">Then type the following command into the Azure CLI, make sure to replace the location with one close to you.</span></span>

```azurecli
az configure --defaults group=<rgn>[sandbox Resource Group]</rgn> location=westus2
```

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="8d4be-109">Event Hubs 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="8d4be-109">Create an Event Hubs namespace</span></span>

<span data-ttu-id="8d4be-110">다음 단계를 수행하여 Azure Cloud Shell에서 지원하는 bash 셸을 사용하여 Event Hubs 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-110">Use the following steps to create an Event Hubs namespace using bash shell supported by Azure Cloud shell:</span></span>

1. <span data-ttu-id="8d4be-111">`az eventhubs namespace create` 명령을 사용하여 Event Hubs 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-111">Create the Event Hubs namespace using the `az eventhubs namespace create` command.</span></span> <span data-ttu-id="8d4be-112">다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-112">Use the following parameters.</span></span>

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="8d4be-113">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8d4be-113">Parameter</span></span>      |<span data-ttu-id="8d4be-114">설명</span><span class="sxs-lookup"><span data-stu-id="8d4be-114">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="8d4be-115">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-115">--name (required)</span></span>      |<span data-ttu-id="8d4be-116">Event Hubs 네임스페이스에 대한 6-50자 길이의 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-116">Enter a 6-50 characters-long unique name for your Event Hubs namespace.</span></span> <span data-ttu-id="8d4be-117">이 이름에는 문자, 숫자 및 하이픈만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-117">The name should contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="8d4be-118">문자로 시작해야 하고 문자 또는 숫자로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-118">It should start with a letter and end with a letter or number.</span></span>|
    > |<span data-ttu-id="8d4be-119">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-119">--resource-group (required)</span></span> | <span data-ttu-id="8d4be-120">이 이름은 기본값에서 제공되는 미리 만들어진 Azure 샌드박스 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-120">This will be the pre-created Azure sandbox resource group supplied from the defaults.</span></span> |
    > |<span data-ttu-id="8d4be-121">--l(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8d4be-121">--l (optional)</span></span>     |<span data-ttu-id="8d4be-122">가장 가까운 Azure 데이터 센터의 위치를 입력합니다(기본값이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="8d4be-122">Enter the location of your nearest Azure datacenter, this will use your default.</span></span>|
    > |<span data-ttu-id="8d4be-123">--sku(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8d4be-123">--sku (optional)</span></span> | <span data-ttu-id="8d4be-124">네임스페이스의 가격 책정 계층[기본</span><span class="sxs-lookup"><span data-stu-id="8d4be-124">The pricing tier for the namespace [Basic</span></span> | <span data-ttu-id="8d4be-125">표준]은 기본값이 _표준_입니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-125">Standard], defaults to _Standard_.</span></span> <span data-ttu-id="8d4be-126">이는 연결 및 소비자 임계값을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-126">This determines the connections and consumer thresholds.</span></span> |

    <span data-ttu-id="8d4be-127">재사용할 수 있도록 이름을 환경 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-127">Set the name into an environment variable so we can reuse it.</span></span>

    ```azurecli
    NS_NAME=myEvt-HubNs1
    ````

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```azurecli
    az eventhubs namespace create --name $NS_NAME
    ```

    > [!NOTE]
    > <span data-ttu-id="8d4be-128">Azure는 이름에 대해 매우 까다로우며 CLI에서 이름이 존재하거나 유효하지 않은 경우 **잘못된 요청**을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-128">Azure is very picky about the name and the CLI returns **Bad Request** if the name exists or is invalid.</span></span> <span data-ttu-id="8d4be-129">환경 변수를 변경하고 명령을 다시 실행하여 다른 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-129">Try a different name by changing your environment variable and reissuing the command.</span></span>


1. <span data-ttu-id="8d4be-130">다음 명령을 사용하여 Event Hubs 네임스페이스에 대한 연결 문자열을 페치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-130">Fetch the connection string for your Event Hubs namespace using the following command.</span></span> <span data-ttu-id="8d4be-131">Event Hub를 사용하여 메시지를 보내고 받도록 응용 프로그램을 구성하려면 이 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-131">You'll need this to configure applications to send and receive messages using your Event Hub.</span></span>

    ```azurecli
    az eventhubs namespace authorization-rule keys list --name RootManageSharedAccessKey --namespace-name $NS_NAME
    ```

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="8d4be-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8d4be-132">Parameter</span></span>      |<span data-ttu-id="8d4be-133">설명</span><span class="sxs-lookup"><span data-stu-id="8d4be-133">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="8d4be-134">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-134">--resource-group (required)</span></span>  | <span data-ttu-id="8d4be-135">이 이름은 기본값에서 제공되는 미리 만들어진 Azure 샌드박스 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-135">This will be the pre-created Azure sandbox resource group supplied from the defaults.</span></span> |
    > |<span data-ttu-id="8d4be-136">--namespace-name(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-136">--namespace-name (required)</span></span>  | <span data-ttu-id="8d4be-137">만든 네임스페이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-137">Enter the name of the namespace you created.</span></span> |

    <span data-ttu-id="8d4be-138">이 명령은 나중에 게시자 및 소비자 응용 프로그램을 구성하는 데 사용할 Event Hubs 네임스페이스에 대한 연결 문자열이 포함된 JSON 블록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-138">This command returns a JSON block with the connection string for your Event Hubs namespace that you'll use later to configure your publisher and consumer applications.</span></span> <span data-ttu-id="8d4be-139">나중에 사용할 수 있도록 다음 키의 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-139">Save the value of the following keys for later use.</span></span>

    - <span data-ttu-id="8d4be-140">**primaryConnectionString**</span><span class="sxs-lookup"><span data-stu-id="8d4be-140">**primaryConnectionString**</span></span>
    - <span data-ttu-id="8d4be-141">**primaryKey**</span><span class="sxs-lookup"><span data-stu-id="8d4be-141">**primaryKey**</span></span>

## <a name="create-an-event-hub"></a><span data-ttu-id="8d4be-142">Event Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="8d4be-142">Create an Event Hub</span></span>

<span data-ttu-id="8d4be-143">다음 단계에 따라 새 Event Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-143">Use the following steps to create your new Event Hub:</span></span>

1. <span data-ttu-id="8d4be-144">`eventhub create` 명령을 사용하여 새 Event Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-144">Create a new Event Hub using the `eventhub create` command.</span></span> <span data-ttu-id="8d4be-145">다음 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-145">It needs the following parameters:</span></span>

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="8d4be-146">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8d4be-146">Parameter</span></span>      |<span data-ttu-id="8d4be-147">설명</span><span class="sxs-lookup"><span data-stu-id="8d4be-147">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="8d4be-148">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-148">--name (required)</span></span>  |<span data-ttu-id="8d4be-149">Event Hub 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-149">Enter a name for your Event Hub.</span></span>|
    > |<span data-ttu-id="8d4be-150">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-150">--resource-group (required)</span></span>  |<span data-ttu-id="8d4be-151">리소스 그룹 소유자.</span><span class="sxs-lookup"><span data-stu-id="8d4be-151">Resource group owner.</span></span>|
    > |<span data-ttu-id="8d4be-152">--namespace-name(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-152">--namespace-name (required)</span></span>      |<span data-ttu-id="8d4be-153">만든 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-153">Enter the namespace you created.</span></span>|

    <span data-ttu-id="8d4be-154">먼저 환경 변수에 Event Hub 이름을 정의해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-154">Let's define the Event Hub name in an environment variable first.</span></span>

    ```azurecli
    HUB_NAME=[name]
    ```

    ```azurecli
    az eventhubs eventhub create --name $HUB_NAME --namespace-name $NS_NAME
    ```

1. <span data-ttu-id="8d4be-155">`eventhub show` 명령을 사용하여 Event Hub의 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-155">View the details of your Event Hub using the `eventhub show` command.</span></span> <span data-ttu-id="8d4be-156">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-156">It takes:</span></span>

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="8d4be-157">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8d4be-157">Parameter</span></span>      |<span data-ttu-id="8d4be-158">설명</span><span class="sxs-lookup"><span data-stu-id="8d4be-158">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="8d4be-159">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-159">--resource-group (required)</span></span>  |<span data-ttu-id="8d4be-160">리소스 그룹 소유자.</span><span class="sxs-lookup"><span data-stu-id="8d4be-160">Resource group owner.</span></span>|
    > |<span data-ttu-id="8d4be-161">--namespace-name(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-161">--namespace-name (required)</span></span>      |<span data-ttu-id="8d4be-162">만든 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-162">Enter the namespace you created.</span></span>|
    > |<span data-ttu-id="8d4be-163">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="8d4be-163">--name  (required)</span></span>|<span data-ttu-id="8d4be-164">Event Hub의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-164">Name of the Event Hub.</span></span>|

    ```azurecli
    az eventhubs eventhub show --namespace-name $NS_NAME --name $HUB_NAME
    ```

## <a name="view-the-event-hub-in-the-azure-portal"></a><span data-ttu-id="8d4be-165">Azure Portal에서 Event Hub 보기</span><span class="sxs-lookup"><span data-stu-id="8d4be-165">View the Event Hub in the Azure portal</span></span>

<span data-ttu-id="8d4be-166">그런 다음, Azure Portal에서 어떻게 표시하는지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-166">Next, let's see what this looks like in the Azure portal.</span></span>

1. <span data-ttu-id="8d4be-167">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-167">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="8d4be-168">포털의 위쪽에 있는 검색 창을 사용하여 Event Hubs 네임스페이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-168">Find your Event Hubs namespace using the Search bar at the top of portal.</span></span>

1. <span data-ttu-id="8d4be-169">네임스페이스를 선택하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-169">Select your namespace to open it.</span></span>

1. <span data-ttu-id="8d4be-170">**엔터티** 섹션 아래에서 **Event Hubs 네임스페이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-170">Select **Event Hubs namespace** under the **ENTITIES** section.</span></span>

1. <span data-ttu-id="8d4be-171">**Event Hubs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-171">Click **Event Hubs**.</span></span>

    <span data-ttu-id="8d4be-172">Event Hub에 대한 **활성** 상태와 기본값 **메시지 보존**(*7*) 및 **파티션 개수**(*4*)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-172">Your Event Hub displays with a status of **Active**, and default values for **Message Retention** (*7*) and **Partition Count** of (*4*).</span></span>

    ![Azure Portal에 표시된 Event Hub](../media/3-event-hub.png)

## <a name="summary"></a><span data-ttu-id="8d4be-174">요약</span><span class="sxs-lookup"><span data-stu-id="8d4be-174">Summary</span></span>

<span data-ttu-id="8d4be-175">이제 새 Event Hub를 만들었으며 게시자 및 소비자 응용 프로그램을 구성하는 데 필요한 모든 정보가 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d4be-175">You've now created a new Event Hub, and you've all the necessary information ready to configure your publisher and consumer applications.</span></span>
