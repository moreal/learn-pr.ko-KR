<span data-ttu-id="97a7b-101">이 단원에서는 Blob이 생성되거나 업데이트될 때 Blob의 이름과 크기를 표시하는 Azure 함수를 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-101">In this unit, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

## <a name="create-a-blob-trigger"></a><span data-ttu-id="97a7b-102">Blob 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="97a7b-102">Create a blob trigger</span></span>

<span data-ttu-id="97a7b-103">다시 기존 Azure Functions 응용 프로그램을 계속 사용하고 Blob 트리거를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-103">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="97a7b-104">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-104">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="97a7b-105">**함수**를 가리키고 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![함수를 가리키고 더하기 선택](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="97a7b-107">**사용자 지정 함수**를 선택한 이후 **Blob 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-107">Select **Custom Function** and then **Blob trigger**.</span></span>

1. <span data-ttu-id="97a7b-108">언어로 **C#** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="97a7b-109">**이름**은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="97a7b-110">**경로**는 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="97a7b-111">기존 Azure Storage 계정을 선택하거나, Azure에서 새 계정을 만들려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="create-a-blob-container"></a><span data-ttu-id="97a7b-112">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="97a7b-112">Create a blob container</span></span>

<span data-ttu-id="97a7b-113">이제 Blob 트리거를 만들었으므로 Storage 탐색기를 사용하여 Blob을 만들고 함수를 트리거해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-113">Now that we've created a blob trigger, let's use the Storage Explorer to create a blob and trigger the function.</span></span>

1. <span data-ttu-id="97a7b-114">사용하거나 만든 저장소 계정을 새 탭에서 엽니다. 이 작업을 쉽게 수행하는 방법은 새 Azure Portal 탭을 열고 사이드바에서 **저장소 계정**을 클릭하거나 사이드바에서 **모든 서비스**를 사용한 후 이름으로 필터링하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-114">Open the storage account you used (or created) in a new tab. An easy way to do this is to open a new Azure Portal tab and click on **Storage accounts** in the sidebar, or to use **All services** in the sidebar and then filter by the name.</span></span> <span data-ttu-id="97a7b-115">작업 중인 두 서비스 간에 전환할 수 있도록 새 탭을 사용하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-115">We want to use a new tab so we can switch between the two services we are working with.</span></span>

1. <span data-ttu-id="97a7b-116">**Storage 탐색기(미리 보기)** 섹션을 클릭합니다. 그러면 Blob 및 파일로 작업할 수 있는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-116">Click on the **Storage Explorer (preview)** section - this will open a new blade where you can work with blobs and files.</span></span>

<span data-ttu-id="97a7b-117">Blob 트리거는 **경로** 필드에 설명된 위치만 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-117">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="97a7b-118">기본적으로 경로는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-118">By default, our path should be:</span></span>

> <span data-ttu-id="97a7b-119">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="97a7b-119">samples-workitems/{name}</span></span>

<span data-ttu-id="97a7b-120">**samples-workitems**라는 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-120">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="97a7b-121">**Blob 컨테이너**를 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-121">Right-click **BLOB CONTAINERS** and select **Create blob container**.</span></span>

1. <span data-ttu-id="97a7b-122">**samples-workitems**를 이름으로 입력하고 액세스 수준을 기본 **개인** 설정으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-122">Enter **samples-workitems** as the name, leave the access level at the default **Private** setting.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="97a7b-123">Blob 트리거 켜기</span><span class="sxs-lookup"><span data-stu-id="97a7b-123">Turn on your blob trigger</span></span>

<span data-ttu-id="97a7b-124">이제 모니터링할 컨테이너를 만들었으므로 Blob을 만들 때 출력을 볼 수 있도록 함수를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-124">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="97a7b-125">Azure 함수 탭으로 다시 전환하거나 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-125">Switch back to the Azure Function tab (or reopen it).</span></span>

1. <span data-ttu-id="97a7b-126">Blob 트리거를 선택하여 코드 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-126">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="97a7b-127">**실행**을 선택하면 출력 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-127">Select **Run** - this will open the output window.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="97a7b-128">Blob 만들기</span><span class="sxs-lookup"><span data-stu-id="97a7b-128">Create a blob</span></span>

<span data-ttu-id="97a7b-129">이제 Blob 트리거가 시작되어 작업을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-129">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="97a7b-130">로그 메시지를 가져올지 확인하는 Blob을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-130">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="97a7b-131">Storage 탐색기에서 **samples-workitems** 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-131">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="97a7b-132">도구 모음에서 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-132">Select **Upload** from the toolbar.</span></span>

1. <span data-ttu-id="97a7b-133">컴퓨터에서 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-133">Select any file from your computer.</span></span>

1. <span data-ttu-id="97a7b-134">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-134">Select **Upload**.</span></span>

1. <span data-ttu-id="97a7b-135">Azure 함수 탭으로 다시 전환하고 출력 로그에서 업로드된 파일이 표시된 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-135">Switch back to the Azure Function tab and check the output logs for a message that displays what file was uploaded.</span></span>

## <a name="pause-the-function"></a><span data-ttu-id="97a7b-136">함수 일시 중지</span><span class="sxs-lookup"><span data-stu-id="97a7b-136">Pause the Function</span></span>

<span data-ttu-id="97a7b-137">추가 요청에 대해 요금이 청구되지 않도록 하려면 로그 창 위에 있는 **일시 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97a7b-137">To ensure that you aren't charged for additional requests, you can click **Pause** above the log window.</span></span>

![함수 일시 중지](../media-drafts/4-pause-timer.png)
