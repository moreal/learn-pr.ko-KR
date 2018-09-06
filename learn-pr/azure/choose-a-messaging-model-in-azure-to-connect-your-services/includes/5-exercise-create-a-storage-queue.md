<span data-ttu-id="cc1fd-101">이 연습에서는 Azure 구독에서 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-101">In this exercise, you will create a new storage account in your Azure subscription.</span></span> <span data-ttu-id="cc1fd-102">그런 다음, Azure Cloud Shell을 사용하여 새 큐를 만들고 이 큐에 메시지를 추가한 후 해당 메시지를 읽고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-102">You will then use Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="cc1fd-103">이는 분산 응용 프로그램 내의 구성 요소가 수행하는 것과 동일한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="cc1fd-104">예를 들어 모바일 앱은 메시지를 큐에 추가할 수 있으며 여기서 웹 서비스가 메시지를 검색하고 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="cc1fd-105">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cc1fd-105">Create a storage account</span></span>

<span data-ttu-id="cc1fd-106">Azure Storage 큐는 Azure 범용 저장소 계정의 일부이므로 먼저 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-106">Since Azure Storage queues are part of Azure general purpose storage accounts, you must start by creating a storage account:</span></span>

1. <span data-ttu-id="cc1fd-107">브라우저에서 [Azure Portal](http://portal.azure.com)로 이동하여 기본 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-107">In a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="cc1fd-108">왼쪽 위에서 **모든 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-108">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="cc1fd-109">아래로 스크롤하여 **저장소** 섹션으로 이동한 후 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-109">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="cc1fd-110">**저장소 계정** 블레이드의 왼쪽 위에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-110">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![추가를 강조 표시한 저장소 계정 블레이드 스크린샷](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="cc1fd-112">**이름** 텍스트 상자에 저장소 계정의 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-112">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="cc1fd-113">**배포 모델**에서 **리소스 관리자**가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-113">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="cc1fd-114">**계정 종류** 드롭다운 목록에서 **저장소(범용 v2)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-114">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="cc1fd-115">**위치** 드롭다운 목록에서 인근 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-115">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="cc1fd-116">**복제** 드롭다운 목록에서 **LRS(로컬 중복 저장소)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-116">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="cc1fd-117">**성능**에서 **표준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-117">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="cc1fd-118">**액세스 계층**에서 **쿨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-118">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="cc1fd-119">**보안 전송 필요**에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-119">Under **Secure transfer required**, select **Disabled**.</span></span>
1. <span data-ttu-id="cc1fd-120">**구독** 아래에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-120">Under **Subscription**, select your subscription.</span></span>

    ![저장소 계정 만들기 대화 상자 스크린샷](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="cc1fd-122">**리소스 그룹**에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-122">Under **Resource group**, select **Create new**.</span></span> <span data-ttu-id="cc1fd-123">텍스트 상자에 **MusicSharingResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-123">In the text box, type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="cc1fd-124">**가상 네트워크**에서 **사용 안 함**을 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-124">Under **Virtual networks**, select **Disabled**, and then click **Create**.</span></span>

    ![만들기를 강조 표시한 저장소 계정 만들기 대화 상자의 스크린샷](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="cc1fd-126">Azure가 새 저장소 계정과 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="cc1fd-127">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="cc1fd-127">Create a queue</span></span>

<span data-ttu-id="cc1fd-128">이제 저장소 계정을 만들었으므로 이 계정에 새 큐를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-128">Now that the storage account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="cc1fd-129">PowerShell 명령을 사용하여 큐를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="cc1fd-130">포털의 오른쪽 위에서 **Cloud Shell** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Cloud Shell 아이콘을 강조 표시한 Azure Portal 스크린샷](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="cc1fd-132">**Azure Cloud Shell 시작** 화면에서 **PowerShell(Linux)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="cc1fd-133">**You have no storage mounted**(탑재된 저장소가 없음) 화면이 나타나는 경우 **저장소 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="cc1fd-134">`PS Azure` 프롬프트가 나타날 때 저장소 계정을 얻으려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command.</span></span> <span data-ttu-id="cc1fd-135">`<storageaccountname>`을 저장소 계정의 고유 이름으로 대체한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-135">Substitute `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="cc1fd-136">저장소 계정의 컨텍스트를 가져오려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-136">To obtain the context of the storage account, type the following command, and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="cc1fd-137">새 큐를 만들려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-137">To create a new queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="cc1fd-138">큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="cc1fd-138">Add a message to the queue</span></span>

<span data-ttu-id="cc1fd-139">이제 저장소 계정에서 큐를 만들었으므로, 이 큐에 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-139">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="cc1fd-140">새 메시지를 작성하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-140">To create a new message, type the following command, and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="cc1fd-141">새 메시지를 새 큐에 추가하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-141">To add the new message to the new queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="cc1fd-142">Azure Portal의 왼쪽 탐색에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-142">In the Azure portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="cc1fd-143">리소스 목록에서 앞부분에서 만든 저장소 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-143">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="cc1fd-144">저장소 계정 블레이드에서 **저장소 탐색기(미리 보기)** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-144">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="cc1fd-145">저장소 탐색기의 **QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-145">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="cc1fd-146">방금 추가한 메시지가 저장소 탐색기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-146">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="cc1fd-147">메시지 검색 및 제거</span><span class="sxs-lookup"><span data-stu-id="cc1fd-147">Retrieve and remove the message</span></span>

<span data-ttu-id="cc1fd-148">저장소 큐의 메시지에 대한 대상 구성 요소는 큐의 맨 앞에 있는 메시지를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-148">A destination component for a message in a Storage queue must retrieve the message at the front of the queue.</span></span> <span data-ttu-id="cc1fd-149">그런 다음, 대상 구성 요소는 메시지를 처리하고 다른 구성 요소가 이를 검색하지 않도록 큐에서 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-149">Then the destination component must process the message, and delete it from the queue so that other components do not retrieve it.</span></span>

1. <span data-ttu-id="cc1fd-150">Cloud Shell에서 큐의 맨 앞에 있는 메시지를 가져오려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-150">In Cloud Shell, to get the message at the front of the queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="cc1fd-151">메시지를 표시하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-151">To display the message, type the following command, and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="cc1fd-152">메시지의 모든 속성을 표시하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-152">To display all the properties of the message, type the following command, and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="cc1fd-153">큐에서 메시지를 제거하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-153">To remove the message from the queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="cc1fd-154">Azure Portal에서 큐 표시를 새로 고치려면 저장소 계정 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-154">In the Azure portal, to refresh the queue display, go to the Storage Account blade.</span></span> <span data-ttu-id="cc1fd-155">**개요**를 클릭한 후 **Storage 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-155">Click **Overview**, and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="cc1fd-156">**QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-156">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="cc1fd-157">유일한 메시지를 제거했기 때문에, 저장소 탐색기는 큐가 비어 있음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-157">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="cc1fd-158">정리</span><span class="sxs-lookup"><span data-stu-id="cc1fd-158">Cleanup</span></span>

<span data-ttu-id="cc1fd-159">이 연습 중에 생성한 모든 리소스를 제거하려면 Cloud Shell에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-159">To remove all resources created during this exercise, enter the following command in Cloud Shell:</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="cc1fd-160">요약</span><span class="sxs-lookup"><span data-stu-id="cc1fd-160">Summary</span></span>

<span data-ttu-id="cc1fd-161">여기서는 Azure 구독에서 저장소 계정을 만들고 이 계정에서 새 큐를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-161">Here, you created a storage account in your Azure subscription, and created a new queue in it.</span></span> <span data-ttu-id="cc1fd-162">또한 PowerShell을 사용하여 큐에 메시지를 추가한 후 이 메시지를 검색 및 제거함으로써 분산 응용 프로그램 구성 요소의 작업을 시뮬레이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-162">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue, and then retrieving and removing it.</span></span>

<span data-ttu-id="cc1fd-163">저장소 계정 큐는 배포 응용 프로그램의 구성 요소 간에 메시지를 전달하려는 경우에 유용한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-163">Storage account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="cc1fd-164">이벤트를 게시하려는 경우에는 저장소 큐를 선택하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cc1fd-164">Do not choose Storage queues when you want to publish events.</span></span>