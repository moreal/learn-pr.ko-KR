<span data-ttu-id="bf9cd-101">이 연습에서는 Azure 구독에서 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-101">In this exercise, you will create a new storage account in your Azure subscription.</span></span> <span data-ttu-id="bf9cd-102">그런 다음, Azure Cloud Shell을 사용하여 새 큐를 만들고 이 큐에 메시지를 추가한 후 해당 메시지를 읽고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-102">You will then use Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="bf9cd-103">이는 분산 응용 프로그램 내의 구성 요소가 수행하는 것과 동일한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="bf9cd-104">예를 들어 모바일 앱은 메시지를 큐에 추가할 수 있으며 여기서 웹 서비스가 메시지를 검색하고 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="bf9cd-105">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="bf9cd-105">Create a storage account</span></span>

<span data-ttu-id="bf9cd-106">Azure Storage 큐는 Azure 범용 저장소 계정의 일부이므로 먼저 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-106">Since Azure Storage queues are part of Azure general-purpose storage accounts, you must start by creating a storage account:</span></span>

1. <span data-ttu-id="bf9cd-107">브라우저에서 [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하여 기본 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-107">In a browser, navigate to the [Azure portal](https://portal.azure.com?azure-portal=true), and sign in with your normal credentials.</span></span>

2. <span data-ttu-id="bf9cd-108">왼쪽 위에서 **모든 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-108">In the top left, click **All services**.</span></span>

3. <span data-ttu-id="bf9cd-109">아래로 스크롤하여 **저장소** 섹션으로 이동한 후 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-109">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>

4. <span data-ttu-id="bf9cd-110">**저장소 계정** 블레이드의 왼쪽 위에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-110">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

  ![추가를 강조 표시한 저장소 계정 블레이드 스크린샷](../media-draft/4-create-a-storage-account-1.png)

5. <span data-ttu-id="bf9cd-112">결과 대화 상자에서 다음 정보를 입력하면 포털의 각 옵션에 `(i)` 아이콘이 표시되며, 이 아이콘을 사용하여 옵션의 기능에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-112">In the resulting dialog, enter the following information, each of these options has a `(i)` icon in the portal which you can use to get more information about what the option does.</span></span>
    - <span data-ttu-id="bf9cd-113">**이름** 텍스트 상자에 저장소 계정의 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-113">In the **Name** text box, type a unique name for the storage account.</span></span>
    - <span data-ttu-id="bf9cd-114">**배포 모델**에서 **Resource Manager**가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
    - <span data-ttu-id="bf9cd-115">**계정 종류** 드롭다운 목록에서 **저장소(범용 v2)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
    - <span data-ttu-id="bf9cd-116">**위치** 드롭다운 목록에서 인근 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-116">In the **Location** drop-down list, select a region near you.</span></span>
    - <span data-ttu-id="bf9cd-117">**복제** 드롭다운 목록에서 **LRS(로컬 중복 저장소)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
    - <span data-ttu-id="bf9cd-118">**성능**에서 **표준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-118">Under **Performance**, select **Standard**.</span></span>
    - <span data-ttu-id="bf9cd-119">**액세스 계층**에서 **쿨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-119">Under **Access tier**, select **Cool**.</span></span>
    - <span data-ttu-id="bf9cd-120">**보안 전송 필요**에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-120">Under **Secure transfer required**, select **Disabled**.</span></span>
    - <span data-ttu-id="bf9cd-121">**구독** 아래에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-121">Under **Subscription**, select your subscription.</span></span>
    - <span data-ttu-id="bf9cd-122">**리소스 그룹**에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-122">Under **Resource group**, select **Create new**.</span></span> <span data-ttu-id="bf9cd-123">텍스트 상자에 **MusicSharingResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-123">In the text box, type **MusicSharingResourceGroup**.</span></span>
    - <span data-ttu-id="bf9cd-124">**가상 네트워크**에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-124">Under **Virtual networks**, select **Disabled**,</span></span> 

    ![저장소 계정 만들기 대화 상자 스크린샷](../media-draft/4-create-a-storage-account-2.png)

6. <span data-ttu-id="bf9cd-126">**만들기**를 클릭하면 Azure가 새 리소스 그룹 및 새 리소스 그룹과 연결된 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-126">Click **Create** - Azure will create a new resource group and a new storage account associated with it.</span></span>

    ![만들기를 강조 표시한 저장소 계정 만들기 대화 상자의 스크린샷](../media-draft/4-create-a-storage-account-3.png)

## <a name="create-a-queue"></a><span data-ttu-id="bf9cd-128">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="bf9cd-128">Create a queue</span></span>

<span data-ttu-id="bf9cd-129">이제 저장소 계정을 만들었으므로 이 계정에 새 큐를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-129">Now that the storage account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="bf9cd-130">PowerShell 명령을 사용하여 큐를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-130">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="bf9cd-131">포털의 오른쪽 위에서 **Cloud Shell** 링크 `(>)`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-131">In the top right of the portal, click the **Cloud Shell** link `(>)`.</span></span>

    ![Cloud Shell 아이콘을 강조 표시한 Azure Portal 스크린샷](../media-draft/4-create-a-storage-queue-1.png)

2. <span data-ttu-id="bf9cd-133">**Azure Cloud Shell 시작** 화면에서 **PowerShell(Linux)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-133">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>

3. <span data-ttu-id="bf9cd-134">**You have no storage mounted**(탑재된 저장소가 없음) 화면이 나타나는 경우 **저장소 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-134">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>

4. <span data-ttu-id="bf9cd-135">`PS Azure` 프롬프트가 나타날 때 저장소 계정을 얻으려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-135">When the `PS Azure` prompt appears, to obtain the storage account, type the following command.</span></span> <span data-ttu-id="bf9cd-136">`<storageaccountname>`을 위에서 만든 저장소 계정의 고유 이름으로 바꾸고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-136">Substitute `<storageaccountname>` with the unique name of your storage account you created above, and then press **Enter**.</span></span> <span data-ttu-id="bf9cd-137">결과 개체를 `$storageaccount`라는 변수에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-137">We want to assign the resulting object to a variable named `$storageaccount`.</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

5. <span data-ttu-id="bf9cd-138">다음으로 저장소 계정 _컨텍스트_를 가져와야 하는데, 이것은 반환된 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-138">Next, we need to get the storage account _context_ - this is a property on the returned object.</span></span> <span data-ttu-id="bf9cd-139">`$context`라는 다른 변수에 할당하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-139">Let's assign it to another variable named `$context`.</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

6. <span data-ttu-id="bf9cd-140">이제 큐를 만들 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-140">Now we are ready to create the queue.</span></span> <span data-ttu-id="bf9cd-141">`New-AzureStorageQueue` 명령을 사용하여 `$messageQueue` 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-141">Use the `New-AzureStorageQueue` command and assign it to a `$messageQueue` variable.</span></span>
    - <span data-ttu-id="bf9cd-142">`musicsharingmessages` 값을 사용하여 `-Name` 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-142">Pass a `-Name` parameter with the value `musicsharingmessages`</span></span>
    - <span data-ttu-id="bf9cd-143">이전 단계에서 검색한 값을 사용하여 `-Context` 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-143">Pass a `-Context` parameter with the value you retrieved in the previous step.</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="bf9cd-144">큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="bf9cd-144">Add a message to the queue</span></span>

<span data-ttu-id="bf9cd-145">이제 저장소 계정에서 큐를 만들었으므로, 이 큐에 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-145">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="bf9cd-146">새 메시지를 만들려면 `New-Object` 메서드를 사용하여 문자열 기반 인수로 .NET `CloudQueueMessage`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-146">To create a new message, use the `New-Object` method to create a .NET `CloudQueueMessage` with a string-based argument:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

2. <span data-ttu-id="bf9cd-147">새 메시지를 새 큐에 추가하려면 앞에서 만든 `CloudQueueMessage`를 `$messageQueue` 큐의 `AddMessageAsync` 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-147">To add the new message to the new queue, pass the created `CloudQueueMessage` to the `AddMessageAsync` method on your `$messageQueue` queue.</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

## <a name="verify-the-message-was-queued"></a><span data-ttu-id="bf9cd-148">메시지가 큐에 추가되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="bf9cd-148">Verify the message was queued</span></span>

<span data-ttu-id="bf9cd-149">**Storage 탐색기**를 사용하여 큐를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-149">We can use the **Storage Explorer** to work with our queue.</span></span> <span data-ttu-id="bf9cd-150">다음과 같은 두 가지 변형을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-150">There are to variations available:</span></span>

- <span data-ttu-id="bf9cd-151">다운로드할 수 있는 Linux, macOS 및 Windows용 플랫폼 간 데스크톱 앱.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-151">A cross-platform desktop app for Linux, macOS, and Windows that you can download.</span></span>
- <span data-ttu-id="bf9cd-152">Azure Portal의 미리 보기 웹 버전.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-152">A preview web version in the Azure portal.</span></span> <span data-ttu-id="bf9cd-153">여기서는 이 방법을 사용하지만, 원한다면 데스크톱 버전을 설치해도 되며 설치 방법도 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-153">This is the one we will use here, but you can install the desktop version if you prefer - the instructions are very similar.</span></span>

1. <span data-ttu-id="bf9cd-154">Azure Portal의 왼쪽 탐색에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-154">In the Azure portal, in the navigation on the left, click **All resources**.</span></span>

2. <span data-ttu-id="bf9cd-155">리소스 목록에서 앞부분에서 만든 저장소 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-155">In the list of resources, click the storage account you created earlier.</span></span>

3. <span data-ttu-id="bf9cd-156">저장소 계정 블레이드에서 **저장소 탐색기(미리 보기)** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-156">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>

4. <span data-ttu-id="bf9cd-157">저장소 탐색기의 **QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-157">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="bf9cd-158">방금 추가한 메시지가 Storage 탐색기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-158">The Storage Explorer should display the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="bf9cd-159">메시지 검색 및 제거</span><span class="sxs-lookup"><span data-stu-id="bf9cd-159">Retrieve and remove the message</span></span>

<span data-ttu-id="bf9cd-160">저장소 큐의 메시지에 대한 대상 구성 요소는 큐의 맨 앞에 있는 메시지를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-160">A destination component for a message in a Storage queue must retrieve the message at the front of the queue.</span></span> <span data-ttu-id="bf9cd-161">그런 다음, 대상 구성 요소는 메시지를 처리하고 다른 구성 요소가 이를 검색하지 않도록 큐에서 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-161">Then the destination component must process the message and delete it from the queue so that other components do not retrieve it.</span></span>

1. <span data-ttu-id="bf9cd-162">큐에서 `GetMessageAsync` 메서드를 사용하여 PowerShell의 첫 번째 사용 가능 메시지를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-162">We can retrieve the first available message in PowerShell using the `GetMessageAsync` method on our queue.</span></span> <span data-ttu-id="bf9cd-163">이것은 비동기 .NET 메서드입니다. `Result` 속성을 사용하여 반환 값을 가져올 수 있을 때까지 기다려야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-163">This is an asynchronous .NET method, since we want to wait for it we can just use the `Result` property to get the return value.</span></span> <span data-ttu-id="bf9cd-164">이렇게 하면 매개 변수에 할당할 수 있는 메시지를 나타내는 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-164">This returns an object representing the message which we can assign to a parameter.</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

2. <span data-ttu-id="bf9cd-165">`AsString`을 호출하여 메시지의 텍스트 버전을 얻을 수 있으며, 콘솔에 값이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-165">We can get a textual version of the message by calling `AsString` - this will output the value on the console.</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

3. <span data-ttu-id="bf9cd-166">또는 간단하게 변수 이름을 입력하고 **Enter** 키를 눌러서 메시지의 모든 속성을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-166">Or, we can display all the properties of the message by just typing the variable name and pressing **Enter**.</span></span>

    ```powershell
    $retrievedMessage
    ```

4. <span data-ttu-id="bf9cd-167">`GetMessageAsync`는 메시지를 제거하지 *않고* 단순히 반환합니다. 즉, 메시지를 다시 처리할 수는 있다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-167">`GetMessageAsync` does *not* remove the message - it simply returns it, which means we could process it again.</span></span> <span data-ttu-id="bf9cd-168">큐에서 메시지를 제거하려면 큐에서 `DeleteMessageAsync` 메서드를 사용하면 됩니다. 이렇게 하려면 제거하려는 메시지를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-168">To remove the message from the queue, we can use the `DeleteMessageAsync` method on the queue - this requires that we pass in the message we want to remove.</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

5. <span data-ttu-id="bf9cd-169">메시지가 사라졌는지 확인하려면 Storage 계정 블레이드로 이동한 후 **개요 > Storage 탐색기**를 선택하여 Azure Portal에서 큐 표시를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-169">To verify that the message is gone, refresh the queue display in the Azure portal by navigating to the Storage Account blade and selecting **Overview > Storage Explorer**.</span></span> <span data-ttu-id="bf9cd-170">**QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-170">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="bf9cd-171">유일한 메시지를 제거했기 때문에, Storage 탐색기는 큐가 비어 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-171">The Storage Explorer should now show that the queue is empty because you removed the only message.</span></span>


## <a name="summary"></a><span data-ttu-id="bf9cd-172">요약</span><span class="sxs-lookup"><span data-stu-id="bf9cd-172">Summary</span></span>
<span data-ttu-id="bf9cd-173">저장소 계정 큐는 배포 응용 프로그램의 구성 요소 간에 _메시지_를 전달하려는 경우에 유용한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-173">Storage account queues are a good solution when you want to pass _messages_ between the components of a distributed application.</span></span> <span data-ttu-id="bf9cd-174">전송을 보장하거나 보낸 순서대로 메시지가 전송되게 만들려는 경우에 적합한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-174">This is a great choice if you want to guarantee delivery or to ensure that messages are delivered in the same order you sent them.</span></span> <span data-ttu-id="bf9cd-175">그러나 큐는 발신자와 수신자가 전달되는 데이터의 형식을 이해함을 나타내며, 발신자와 수신자 사이에는 통신 서비스 간에 약간의 "결합"을 추가하는 암시적 데이터 계약이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-175">However, queues imply that the sender and receiver understand the format of the data being passed - there's an implied data contract between them which adds a bit of "coupling" between the two communicating services.</span></span>

<span data-ttu-id="bf9cd-176">모든 아키텍처가 포맷된 데이터 블록을 전달할 필요는 없으며, 일부 아키텍처는 메시지 처리 방법을 알 필요 없이 파이어 앤 포켓 방식의 간단한 메시지만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-176">Not all architectures need to pass formatted blocks of data, some really just need simple messages which we want to fire-and-forget without any knowledge of what will handle the message.</span></span> <span data-ttu-id="bf9cd-177">이러한 시나리오에서는 큐가 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-177">In these scenarios, a queue isn't a great choice.</span></span> <span data-ttu-id="bf9cd-178">이 유형의 통신과 잘 어울리는 다른 메시지 전략을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-178">Let's look at another messaging strategy which is more suited to this style of communication.</span></span>