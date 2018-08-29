<span data-ttu-id="267c8-101">이 연습에서는 만들거나 업데이트될 때 Blob의 이름과 크기를 표시하는 Azure 함수를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="267c8-102">이 연습을 완료하려면 유효한 계정으로 [Azure Portal](https://portal.azure.com/)에 로그인했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="267c8-102">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="267c8-103">Blob 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="267c8-103">Create a blob trigger</span></span>

<span data-ttu-id="267c8-104">다시 기존 Azure Functions 응용 프로그램을 계속 사용하고 Blob 트리거를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="267c8-105">**함수**를 가리키고 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![함수를 가리키고 더하기 선택](../media/4-hover-function.png)

1. <span data-ttu-id="267c8-107">**Blob 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="267c8-108">언어로 **C#** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="267c8-109">**이름**은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="267c8-110">**경로**는 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="267c8-111">기존 Azure Storage 계정을 선택하거나, Azure에서 새 계정을 만들려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="download-storage-explorer"></a><span data-ttu-id="267c8-112">Storage 탐색기 다운로드</span><span class="sxs-lookup"><span data-stu-id="267c8-112">Download Storage explorer</span></span>

<span data-ttu-id="267c8-113">이제 Blob 트리거를 만들었으므로 Blob을 쉽게 만들 수 있는 Storage 탐색기를 다운로드해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-113">Now that we've created a blob trigger, let's download Storage explorer, which will allow us to easily create a blob.</span></span>

- <span data-ttu-id="267c8-114">[Storage 탐색기](http://storageexplorer.com)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-114">Download [Storage explorer](http://storageexplorer.com).</span></span>

## <a name="connect-to-your-azure-storage-account"></a><span data-ttu-id="267c8-115">Azure Storage 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="267c8-115">Connect to your Azure Storage account</span></span>

<span data-ttu-id="267c8-116">이제 Storage 탐색기를 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-116">We now have Storage explorer downloaded.</span></span> <span data-ttu-id="267c8-117">제공된 자격 증명을 사용하여 로그인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-117">Let's sign in using the credentials that were supplied.</span></span>

1. <span data-ttu-id="267c8-118">Storage 탐색기에서 왼쪽에 있는 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-118">In Storage explorer, select the plus (+) icon on the left.</span></span>

1. <span data-ttu-id="267c8-119">**저장소 계정 이름 및 키 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-119">Select **Use a storage account name and key**.</span></span>

1. <span data-ttu-id="267c8-120">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-120">Select **Next**.</span></span>

1. <span data-ttu-id="267c8-121">Azure의 Blob 트리거 아래에서 **통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-121">In Azure, under your blob trigger, select **Integrate**.</span></span>

1. <span data-ttu-id="267c8-122">**문서**를 선택하여 보기를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-122">Select **Documentation** to expand the view.</span></span>

1. <span data-ttu-id="267c8-123">**계정 이름** 및 **계정 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-123">Copy the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="267c8-124">Storage 탐색기로 돌아가 **계정 이름** 및 **계정 키**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-124">Back in Storage explorer, paste in the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="267c8-125">**표시 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-125">Enter a **Display name**.</span></span> <span data-ttu-id="267c8-126">이 값은 Storage 탐색기의 연결 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-126">This value is the name of the connection in Storage explorer.</span></span>

1. <span data-ttu-id="267c8-127">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-127">Select **Next**.</span></span>

1. <span data-ttu-id="267c8-128">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-128">Select **Connect**.</span></span> 

## <a name="create-a-blob-container"></a><span data-ttu-id="267c8-129">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="267c8-129">Create a blob container</span></span>

<span data-ttu-id="267c8-130">Azure Storage 계정에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-130">We aren't connected to our Azure Storage account.</span></span> <span data-ttu-id="267c8-131">Blob 트리거는 **경로** 필드에 설명된 위치만 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-131">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="267c8-132">기본적으로 경로는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-132">By default, our path should be:</span></span>

> <span data-ttu-id="267c8-133">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="267c8-133">samples-workitems/{name}</span></span>

<span data-ttu-id="267c8-134">**samples-workitems**라는 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-134">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="267c8-135">Storage 탐색기에서 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-135">In Storage explorer, expand your storage account.</span></span> <span data-ttu-id="267c8-136">이름은 연결 프로세스 중에 제공한 **표시 이름**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-136">The name should be the **Display name** that you provided during the connection process.</span></span>

1. <span data-ttu-id="267c8-137">**Blob 컨테이너**를 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-137">Right-click **Blob Containers** and select **Create blob container**.</span></span>

1. <span data-ttu-id="267c8-138">**samples-workitems**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-138">Enter **samples-workitems**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="267c8-139">Blob 트리거 켜기</span><span class="sxs-lookup"><span data-stu-id="267c8-139">Turn on your blob trigger</span></span>

<span data-ttu-id="267c8-140">이제 모니터링할 컨테이너를 만들었으므로 Blob을 만들 때 출력을 볼 수 있도록 함수를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-140">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="267c8-141">Blob 트리거를 선택하여 코드 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-141">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="267c8-142">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-142">Select **Run**.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="267c8-143">Blob 만들기</span><span class="sxs-lookup"><span data-stu-id="267c8-143">Create a blob</span></span>

<span data-ttu-id="267c8-144">이제 Blob 트리거가 시작되어 작업을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-144">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="267c8-145">로그 메시지를 가져올지 확인하는 Blob을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-145">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="267c8-146">Storage 탐색기에서 **samples-workitems** 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-146">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="267c8-147">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-147">Select **Upload**.</span></span> 

1. <span data-ttu-id="267c8-148">**파일 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-148">Select **Upload Files**.</span></span>

1. <span data-ttu-id="267c8-149">컴퓨터에서 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-149">Select any file from your computer.</span></span>

1. <span data-ttu-id="267c8-150">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-150">Select **Upload**.</span></span>

1. <span data-ttu-id="267c8-151">Azure로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-151">Go back to Azure.</span></span> <span data-ttu-id="267c8-152">로그에서 업로드된 파일을 표시하는 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-152">Check your logs for a message that displays what file was uploaded.</span></span>

## <a name="clean-up"></a><span data-ttu-id="267c8-153">정리</span><span class="sxs-lookup"><span data-stu-id="267c8-153">Clean up</span></span>

<span data-ttu-id="267c8-154">이 함수에 대해 요금이 청구되지 않도록 하려면 로그 창 위에 있는 **일시 중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="267c8-154">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![일시 중지](../media/4-pause-timer.png)


