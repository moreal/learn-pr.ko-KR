<span data-ttu-id="f7c43-101">이 단원에서는 Blob이 생성되거나 업데이트될 때 Blob의 이름과 크기를 표시하는 Azure 함수를 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-101">In this unit, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="f7c43-102">Blob 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c43-102">Create a blob trigger</span></span>

<span data-ttu-id="f7c43-103">다시 기존 Azure Functions 응용 프로그램을 계속 사용하고 Blob 트리거를 추가해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-103">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="f7c43-104">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="f7c43-105">**모든 리소스** 화면으로 이동하고 함수 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-105">Navigate to the **All resources** screen and select your function app.</span></span>

1. <span data-ttu-id="f7c43-106">**Functions**를 가리키고 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-106">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="f7c43-107">**Blob 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="f7c43-108">언어로 **C#** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-108">Select **C#** as the language.</span></span>

1. <span data-ttu-id="f7c43-109">**이름**은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="f7c43-110">**경로**는 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="f7c43-111">**저장소 계정 연결** 드롭다운 옆의 _새_ 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-111">Select the _new_ link next to the **Storage account connection** dropdown.</span></span> <span data-ttu-id="f7c43-112">나타나는 블레이드에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-112">In the blade that pops up, click **Create new**.</span></span> <span data-ttu-id="f7c43-113">새 저장소 계정에 대한 고유한 이름을 입력하고 **확인**을 선택하여 저장소 계정을 만들고 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-113">Enter a unique name for the new storage account and select **OK** to create the storage account and close pane.</span></span>

1. <span data-ttu-id="f7c43-114">새 함수 화면으로 돌아가면 **만들기**를 선택하여 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-114">Once you have returned to the New Function screen, select **Create** to create the function.</span></span>

## <a name="create-a-blob-container"></a><span data-ttu-id="f7c43-115">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c43-115">Create a blob container</span></span>

<span data-ttu-id="f7c43-116">이제 Blob 트리거를 만들었으므로 Storage 탐색기를 사용하여 Blob을 만들고 함수를 트리거해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-116">Now that we've created a blob trigger, let's use the Storage Explorer to create a blob and trigger the function.</span></span>

1. <span data-ttu-id="f7c43-117">사용하거나 만든 저장소 계정을 새 탭에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-117">Open the storage account you used (or created) in a new tab.</span></span>

    > [!TIP]
    > <span data-ttu-id="f7c43-118">해당 탭을 마우스 오른쪽 단추로 클릭하고 나타나는 메뉴에서 **복제**를 선택하여 대부분의 브라우저에서 탭을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-118">You can duplicate a tab in most browsers by right-clicking on the tab in question and selecting **Duplicate** from the menu that appears.</span></span> <span data-ttu-id="f7c43-119">작업 중인 두 서비스 간에 전환할 수 있도록 새 탭을 사용하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-119">We want to use a new tab so we can switch between the two services we are working with.</span></span>

1. <span data-ttu-id="f7c43-120">사이드바에서 **저장소 계정**을 선택하거나 사이트바에서 **모든 리소스**를 선택한 다음, 이름으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-120">Select **Storage accounts** in the sidebar, or select **All resources** in the sidebar and then filter by the name.</span></span>

1. <span data-ttu-id="f7c43-121">**Storage 탐색기(미리 보기)** 섹션을 클릭하면 Blob 및 파일로 작업할 수 있는 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-121">Click on the **Storage Explorer (preview)** section - this will open a new panel where you can work with blobs and files.</span></span>

<span data-ttu-id="f7c43-122">Blob 트리거는 **경로** 필드에 설명된 위치만 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-122">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="f7c43-123">기본적으로 경로는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-123">By default, our path should be:</span></span>

> <span data-ttu-id="f7c43-124">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="f7c43-124">samples-workitems/{name}</span></span>

<span data-ttu-id="f7c43-125">**samples-workitems**라는 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-125">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="f7c43-126">**Blob 컨테이너**를 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-126">Right-click **BLOB CONTAINERS** and select **Create Blob Container**.</span></span>

1. <span data-ttu-id="f7c43-127">**samples-workitems**를 이름으로 입력하고 액세스 수준을 기본 **개인** 설정으로 그대로 두고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-127">Enter **samples-workitems** as the name, leave the access level at the default **Private** setting, and select **OK**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="f7c43-128">Blob 트리거 켜기</span><span class="sxs-lookup"><span data-stu-id="f7c43-128">Turn on your blob trigger</span></span>

<span data-ttu-id="f7c43-129">이제 모니터링할 컨테이너를 만들었으므로 Blob을 만들 때 출력이 표시될 수 있도록 함수를 실행해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-129">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="f7c43-130">Azure Function을 사용하여 브라우저 탭으로 다시 전환하거나 브라우저 탭을 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-130">Switch back to the browser tab with your Azure Function (or reopen it).</span></span>

1. <span data-ttu-id="f7c43-131">Blob 트리거를 선택하여 코드 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-131">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="f7c43-132">화면의 맨 아래에서 **로그** 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-132">Open the **Logs** tab at the bottom of the screen.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="f7c43-133">Blob 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c43-133">Create a blob</span></span>

<span data-ttu-id="f7c43-134">이제 Blob 트리거가 시작되어 작업을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-134">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="f7c43-135">로그 메시지를 가져올지 확인하기 위한 Blob을 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-135">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="f7c43-136">Storage 탐색기를 사용하여 브라우저 탭으로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-136">Switch back to the browser tab with Storage Explorer.</span></span>

1. <span data-ttu-id="f7c43-137">Storage 탐색기의 **BLOB CONTAINERS** 목록에서 **samples-workitems** 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-137">In Storage Explorer, select the **samples-workitems** container from the **BLOB CONTAINERS** list.</span></span>

1. <span data-ttu-id="f7c43-138">도구 모음에서 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-138">Select **Upload** from the toolbar.</span></span>

1. <span data-ttu-id="f7c43-139">컴퓨터에서 모든 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-139">Select any file from your computer.</span></span>

1. <span data-ttu-id="f7c43-140">**인증 유형**에서 **SAS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-140">Under **Authentication type**, select **SAS**.</span></span>

1. <span data-ttu-id="f7c43-141">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-141">Select **Upload**.</span></span>

1. <span data-ttu-id="f7c43-142">Azure 함수 탭으로 다시 전환하고 출력 로그에서 업로드된 파일이 표시되는 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c43-142">Switch back to the Azure Function tab and check the output logs for a message that displays what file was uploaded.</span></span>