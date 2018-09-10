<span data-ttu-id="01e3f-101">이 연습에서는 Azure Portal을 사용하여 가상의 남부 캘리포니아 서핑 보고서 Web App에 적절한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-101">In this exercise, you will use the Azure portal to create a storage account that is appropriate for a fictitious southern California surf report Web App.</span></span>

## <a name="design-goals"></a><span data-ttu-id="01e3f-102">디자인 목표</span><span class="sxs-lookup"><span data-stu-id="01e3f-102">Design goals</span></span>

<span data-ttu-id="01e3f-103">서핑 보고서 사이트를 통해 사용자가 로컬 해변 조건의 사진 및 비디오를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-103">The surf-report site lets users upload photos and videos of their local beach conditions.</span></span> <span data-ttu-id="01e3f-104">보는 사람은 이 콘텐츠를 사용하여 가장 좋은 서핑 조건을 갖는 해변을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-104">Viewers will use the content to help them choose the beach with the best surfing conditions.</span></span> <span data-ttu-id="01e3f-105">디자인 및 기능 목표 목록을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-105">Your list of design and feature goals is:</span></span>

- <span data-ttu-id="01e3f-106">비디오 콘텐츠를 신속하게 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-106">Video content must load quickly</span></span>
- <span data-ttu-id="01e3f-107">사이트에서는 업로드 볼륨이 예기치 않게 급증하는 경우 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-107">The site must handle unexpected spikes in upload volume</span></span>
- <span data-ttu-id="01e3f-108">오래된 콘텐츠를 서핑 조건 변화에 따라 제거하므로 사이트는 항상 현재 조건을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-108">Outdated content will be removed as surf conditions change so the site always shows current conditions</span></span>

<span data-ttu-id="01e3f-109">처리를 위해 Azure Queue에 업로드된 콘텐츠를 버퍼링한 다음, 저장을 위해 Azure Blob Storage로 이동시키기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-109">You decide on an implementation that buffers uploaded content in an Azure Queue for processing and then moves it into an Azure Blob for storage.</span></span> <span data-ttu-id="01e3f-110">Queues와 Blob을 모두 저장할 수 있는 동시에 콘텐츠에 대한 대기 시간이 짧은 액세스를 제공하는 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-110">You need a storage account that can hold both Queues and Blobs while delivering low-latency access to your content.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="01e3f-111">연습 단계</span><span class="sxs-lookup"><span data-stu-id="01e3f-111">Exercise steps</span></span>

### <a name="launch-the-blade"></a><span data-ttu-id="01e3f-112">블레이드 시작</span><span class="sxs-lookup"><span data-stu-id="01e3f-112">Launch the blade</span></span>

1. <span data-ttu-id="01e3f-113">웹 브라우저에서 [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하고 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-113">In your web browser, navigate to the [Azure Portal](https://portal.azure.com?azure-portal=true) and sign into your account.</span></span>

1. <span data-ttu-id="01e3f-114">왼쪽 세로 막대에서 **리소스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-114">In the left sidebar, select **Create a resource**.</span></span>

1. <span data-ttu-id="01e3f-115">Azure Marketplace의 **저장소** 제목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-115">Select the **Storage** heading in the Azure Marketplace.</span></span>

1. <span data-ttu-id="01e3f-116">**저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-116">Select **Storage account**.</span></span> <span data-ttu-id="01e3f-117">포털에는 **저장소 계정 만들기** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-117">The portal will display the **Create storage account** blade.</span></span>

### <a name="configure-the-basic-options"></a><span data-ttu-id="01e3f-118">기본 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="01e3f-118">Configure the basic options</span></span>

1. <span data-ttu-id="01e3f-119">블레이드의 맨 위에 있는 **기본 사항** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-119">Select the **Basics** tab at the top of the blade.</span></span>

1. <span data-ttu-id="01e3f-120">**구독**: 구독 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-120">**Subscription**: Select one of your subscriptions.</span></span>

1. <span data-ttu-id="01e3f-121">**리소스 그룹**: **SurfReportResourceGroup**이라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-121">**Resource group**: Create a new resource group named **SurfReportResourceGroup**.</span></span>

1. <span data-ttu-id="01e3f-122">**저장소 계정 이름**: `surfreport` + 사용자 이니셜 + 숫자와 같은 전세계에 고유한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-122">**Storage account name**: Enter a globally-unique value like `surfreport` + your initials + a number.</span></span>

 1. <span data-ttu-id="01e3f-123">**위치**: **미국 서부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-123">**Location**: Select **West US**.</span></span>

    <span data-ttu-id="01e3f-124">이유: 해당 응용 프로그램이 캘리포니아 남부의 사용자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-124">Rationale: The application is intended for users in southern California.</span></span> <span data-ttu-id="01e3f-125">비디오를 로드할 때 대기 시간을 최소화하려면 이러한 사용자에게 가까운 Blob을 호스팅해야 합니다. 따라서 **미국 서부**를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-125">To minimize latency when loading videos, the Blobs should be hosted close to these users; this makes **West US** a good choice.</span></span>

1. <span data-ttu-id="01e3f-126">**배포 모델**: **Resource Manager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-126">**Deployment model**: Select **Resource manager**.</span></span>
    
    <span data-ttu-id="01e3f-127">이유: **Resource Manager**를 통해 리소스 그룹을 사용하여 응용 프로그램에 대한 Web App, 저장소 계정 등을 관리할 수 있기 때문에 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-127">Rationale: **Resource manager** is appropriate because it will let you use a resource group to manage the Web App, storage account, etc. for the application.</span></span>

1. <span data-ttu-id="01e3f-128">**성능**: **표준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-128">**Performance**: Select **Standard**.</span></span>

    <span data-ttu-id="01e3f-129">이유: 페이지 Blob로 저장소 계정을 제한하기 때문에 **프리미엄** 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-129">Rationale: You cannot use the **Premium** option because it would limit the storage account to page Blobs.</span></span> <span data-ttu-id="01e3f-130">비디오 및 큐에 대한 Blob을 모두 버퍼링하기 위해 차단해야 하는 경우 **표준** 옵션에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-130">You need block Blobs for your videos and a Queue for buffering both of which are only available in the **Standard** option.</span></span>

1. <span data-ttu-id="01e3f-131">**계정 종류**: **StorageV2(범용 v2)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-131">**Account kind**: Select **StorageV2 (general purpose v2)**.</span></span>

    <span data-ttu-id="01e3f-132">이유: **StorageV2(범용 v2)** 가 여기에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-132">Rationale: **StorageV2 (general purpose v2)** is the right choice here.</span></span> <span data-ttu-id="01e3f-133">Blob 및 Queue를 조합해야 하므로 **Blob Storage** 옵션이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-133">You need a mix of Blobs and a Queue, so the **Blob storage** option will not work.</span></span> <span data-ttu-id="01e3f-134">이 응용 프로그램의 경우 **저장소(범용 v1)** 계정을 선택하는 혜택이 있을 수 없습니다. 그러면 액세스할 수 있는 기능을 제한하고 예상된 워크로드의 비용을 줄일 가능성이 적기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-134">For this application, there would be no benefit to choosing a **Storage (general purpose v1)** account since that would limit the features you could access and would be unlikely to reduce the cost of your expected workload.</span></span>

1. <span data-ttu-id="01e3f-135">**복제**: **LRS(로컬 중복 저장소)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-135">**Replication**: Select **Locally-redundant storage (LRS)**.</span></span>

    <span data-ttu-id="01e3f-136">이유: 이미지와 비디오는 빠르게 만료되고 사이트에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-136">Rationale: The images and videos quickly become out-of-date and are removed from the site.</span></span> <span data-ttu-id="01e3f-137">즉, 글로벌 백업을 위해 추가 비용을 지불하는 것은 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-137">This means there is little value to paying extra for global redundancy.</span></span> <span data-ttu-id="01e3f-138">재해로 인해 데이터 손실이 발생한 경우 사용자의 최신 콘텐츠를 사용하여 사이트를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-138">If a catastrophic event results in data loss, you can restart the site with fresh content from your users.</span></span>

1. <span data-ttu-id="01e3f-139">**액세스 계층(기본값)**: **핫**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-139">**Access tier (default)**: Select **Hot**.</span></span>
   
    <span data-ttu-id="01e3f-140">이유: 비디오를 신속하게 로드하려면 Blob에 대해 고성능 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-140">Rationale: You want the videos to load quickly so you will use the high-performance option for your Blobs.</span></span>
   
<span data-ttu-id="01e3f-141">다음 스크린샷에서는 **기본 사항** 탭에 대해 완성된 설정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-141">The following screenshot shows the completed settings for the **Basics** tab.</span></span>

![**기본 사항** 탭을 선택한 저장소 계정 만들기 블레이드 스크린샷](../media-drafts/5-create-storage-account-basics.png)

### <a name="configure-the-advanced-options"></a><span data-ttu-id="01e3f-143">고급 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="01e3f-143">Configure the advanced options</span></span>

1. <span data-ttu-id="01e3f-144">블레이드의 맨 위에 있는 **고급** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-144">Select the **Advanced** tab at the top of the blade.</span></span>

1. <span data-ttu-id="01e3f-145">**보안 전송 필요**: **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-145">**Secure transfer required**: Select **Enabled**.</span></span>

    <span data-ttu-id="01e3f-146">이유: 네트워크를 통한 Https는 일반적으로 모범 사례로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-146">Rationale: Https across the wire is generally considered best practice.</span></span>

1. <span data-ttu-id="01e3f-147">**가상 네트워크**: **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-147">**Virtual Networks**: Select **Disabled**.</span></span>

    <span data-ttu-id="01e3f-148">이유: 콘텐츠가 공용이므로 공용 클라이언트에서 액세스할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-148">Rationale: The content is public facing and you need to allow access from public clients.</span></span>

<span data-ttu-id="01e3f-149">다음 스크린샷에서는 **고급** 탭에 대해 완성된 설정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-149">The following screenshot shows the completed settings for the **Advanced** tab.</span></span>

![**고급** 탭을 선택한 저장소 계정 만들기 블레이드 스크린샷](../media-drafts/5-create-storage-account-advanced.png)

### <a name="create"></a><span data-ttu-id="01e3f-151">만들기</span><span class="sxs-lookup"><span data-stu-id="01e3f-151">Create</span></span>

1. <span data-ttu-id="01e3f-152">블레이드 아래쪽에서 **검토 + 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-152">Click the **Review + create** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="01e3f-153">다음 화면의 블레이드 아래쪽에서 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-153">On the next screen, click the **Create** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="01e3f-154">리소스가 생성될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-154">Wait for the resource to be created.</span></span>

### <a name="verify"></a><span data-ttu-id="01e3f-155">확인</span><span class="sxs-lookup"><span data-stu-id="01e3f-155">Verify</span></span>

1. <span data-ttu-id="01e3f-156">왼쪽 세로 막대에서 **저장소 계정** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-156">Select the **Storage accounts** link in the left sidebar.</span></span>

1. <span data-ttu-id="01e3f-157">생성에 성공했는지 확인하려면 목록에서 새 저장소 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-157">Locate the new storage account in the list to verify that creation succeeded.</span></span>

### <a name="clean-up"></a><span data-ttu-id="01e3f-158">정리</span><span class="sxs-lookup"><span data-stu-id="01e3f-158">Clean up</span></span>

1. <span data-ttu-id="01e3f-159">왼쪽 세로 막대에서 **리소스 그룹** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-159">Select the **Resource groups** link in the left sidebar.</span></span>

1. <span data-ttu-id="01e3f-160">목록에서 **SurfReportResourceGroup**을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-160">Locate **SurfReportResourceGroup** in the list.</span></span>

1. <span data-ttu-id="01e3f-161">**SurfReportResourceGroup** 항목을 마우스 오른쪽 단추로 클릭하고, 팝업 메뉴에서 **리소스 그룹 삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-161">Right-click on the **SurfReportResourceGroup** entry and select **Delete resource group** from the context menu.</span></span>

1. <span data-ttu-id="01e3f-162">확인 필드에 리소스 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-162">Type the resource group name into the confirmation field.</span></span>

1. <span data-ttu-id="01e3f-163">**삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-163">Click the **Delete** button.</span></span>

## <a name="summary"></a><span data-ttu-id="01e3f-164">요약</span><span class="sxs-lookup"><span data-stu-id="01e3f-164">Summary</span></span>

<span data-ttu-id="01e3f-165">비즈니스 요구 사항에 기반한 설정을 사용하여 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-165">You created a storage account with settings driven by your business requirements.</span></span> <span data-ttu-id="01e3f-166">예를 들어 고객이 주로 남부 캘리포니아에 있기 때문에 미국 서부 데이터 센터를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-166">For example, you selected a West US datacenter because your customers were primarily located in southern California.</span></span> <span data-ttu-id="01e3f-167">일반적인 흐름은 다음과 같습니다. 먼저 데이터 및 목표를 분석한 다음, 맞는 저장소 계정 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="01e3f-167">This is a typical flow: first analyze your data and goals and then configure the storage account options to match.</span></span>