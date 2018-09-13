<span data-ttu-id="18353-101">이제 Azure Portal을 사용하여 대시보드를 만들고, 기본 JSON 파일을 직접 편집하여 대시보드를 수정하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-101">Next, let's look at how to create and modify dashboards using the Azure Portal, and by editing the underlying JSON file directly.</span></span>

## <a name="what-is-a-dashboard"></a><span data-ttu-id="18353-102">대시보드란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="18353-102">What is a dashboard?</span></span>

<span data-ttu-id="18353-103">_대시보드_는 Azure Portal에 표시되는 사용자 지정 가능한 UI 타일 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="18353-103">A _dashboard_ is a customizable collection of UI tiles displayed in the Azure portal.</span></span> <span data-ttu-id="18353-104">타일을 추가, 제거, 배치하여 원하는 정확한 뷰를 만들고 대시보드로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-104">You add, remove, and position tiles to create the exact view you want, and then save that view as a dashboard.</span></span> <span data-ttu-id="18353-105">여러 대시보드가 지원되며 필요에 따라 대시보드 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-105">Multiple dashboards are supported, and you can switch between them as needed.</span></span> <span data-ttu-id="18353-106">다른 팀 구성원과 대시보드를 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-106">You can even share your dashboards with other team members.</span></span>

<span data-ttu-id="18353-107">대시보드를 통해 Azure를 매우 유연하게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-107">Dashboards give you considerable flexibility regarding how you manage Azure.</span></span> <span data-ttu-id="18353-108">예를 들어 조직 내의 특정 역할에 대한 대시보드를 만든 후에 RBAC(역할 기반 액세스 제어)를 사용하여 이 대시보드에 누가 액세스할 수 있는 지를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-108">For example, you can create dashboards for specific roles within the organization, and then use role-based access control (RBAC) to control who can access that dashboard.</span></span> <span data-ttu-id="18353-109">따라서 데이터베이스 관리자는 SQL 데이터베이스 서비스의 뷰가 있는 대시보드를, Azure Active Directory 관리자는 Azure AD 내 사용자 및 그룹의 뷰가 있는 대시보드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-109">Hence, your database administrator would have a dashboard that contains views of the SQL database service, whereas your Azure Active Directory administrator would have views of the users and groups within Azure AD.</span></span> <span data-ttu-id="18353-110">관리하는 환경마다 특정 대시보드를 만들어서 프로덕션 환경과 개발 환경 사이에서 포털을 사용자 지정하는 것도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-110">You can even customize the portal between your production and development environments within the portal - creating a specific dashboard for each environment you are managing.</span></span>

<span data-ttu-id="18353-111">대시보드는 JSON(JavaScript Object Notation) 파일로 저장되기 때문에</span><span class="sxs-lookup"><span data-stu-id="18353-111">Dashboards are stored as JavaScript Object Notation (JSON) files.</span></span> <span data-ttu-id="18353-112">다른 컴퓨터에 업로드 및 다운로드되거나 Azure 디렉터리 멤버와 공유될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-112">This means they can be uploaded and downloaded to other computers, or shared with members of the Azure directory.</span></span> <span data-ttu-id="18353-113">Azure는 대시보드를 포털 내에서 관리할 수 있는 가상 머신이나 저장소 계정처럼 리소스 그룹 내에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-113">Azure stores dashboards within resource groups, just like virtual machines or storage accounts that you can manage within the portal.</span></span>

> [!TIP]
> <span data-ttu-id="18353-114">대시보드는 JSON 파일이므로 [프로그래밍 방식으로 사용자 지정](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically)하여 관리 도구로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-114">Because dashboards are JSON files, you can also [customize them programmatically](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically), making them compelling administrative tools.</span></span> <span data-ttu-id="18353-115">또한 일부 타일 유형은 쿼리 기반이라서 원본 데이터가 변경되면 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-115">Also, some tile types can be query-based, so they update automatically when the source data changes.</span></span>

## <a name="explore-the-default-dashboard"></a><span data-ttu-id="18353-116">기본 대시보드 탐색</span><span class="sxs-lookup"><span data-stu-id="18353-116">Explore the default dashboard</span></span>

<span data-ttu-id="18353-117">기본 대시보드는 이름은 “대시보드”입니다.</span><span class="sxs-lookup"><span data-stu-id="18353-117">The default dashboard is named "Dashboard".</span></span> <span data-ttu-id="18353-118">포털에 로그인하면 이 대시보드가 표시되며, 여기에는 5개의 웹 파트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-118">When you log into the portal, you are presented with this dashboard containing five web parts.</span></span>

![기본 웹 파트](../media-draft/8-dashboard-default-webparts.png)

<span data-ttu-id="18353-120">기본 웹 파트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-120">These default web parts are</span></span>

1. <span data-ttu-id="18353-121">모든 리소스</span><span class="sxs-lookup"><span data-stu-id="18353-121">All resources</span></span>

1. <span data-ttu-id="18353-122">빠른 시작 + 자습서</span><span class="sxs-lookup"><span data-stu-id="18353-122">Quickstarts + tutorials</span></span>

1. <span data-ttu-id="18353-123">서비스 상태</span><span class="sxs-lookup"><span data-stu-id="18353-123">Service Health</span></span>

1. <span data-ttu-id="18353-124">Marketplace</span><span class="sxs-lookup"><span data-stu-id="18353-124">Marketplace</span></span>

1. <span data-ttu-id="18353-125">Azure 시작</span><span class="sxs-lookup"><span data-stu-id="18353-125">Azure Getting Started</span></span>

## <a name="creating-and-managing-dashboards"></a><span data-ttu-id="18353-126">대시보드 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="18353-126">Creating and managing dashboards</span></span>

<span data-ttu-id="18353-127">대시보드 맨 위에는 대시보드를 만들고, 업로드하고, 다운로드하고, 편집하고, 공유할 수 있는 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-127">Along the top of the dashboard are the controls that enable you to create, upload, download, edit, and share a dashboard.</span></span> <span data-ttu-id="18353-128">대시보드를 전체 화면으로 전환하거나 복제하거나 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-128">You can also switch a dashboard to full screen, clone it, or delete it.</span></span>

![대시보드 컨트롤 사용자 지정](../media-draft/8-customise-dashboard-controls.png)

- [<span data-ttu-id="18353-130">대시보드 선택</span><span class="sxs-lookup"><span data-stu-id="18353-130">Select dashboard</span></span>](#select-dashboard)
- [<span data-ttu-id="18353-131">새 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="18353-131">Create a new dashboard</span></span>](#create-new)
- [<span data-ttu-id="18353-132">업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="18353-132">Upload and Download</span></span>](#upload-download)
- [<span data-ttu-id="18353-133">편집</span><span class="sxs-lookup"><span data-stu-id="18353-133">Edit</span></span>](#edit-dashboard)
- [<span data-ttu-id="18353-134">공유</span><span class="sxs-lookup"><span data-stu-id="18353-134">Share</span></span>](#share-dashboard)
- [<span data-ttu-id="18353-135">전체 화면</span><span class="sxs-lookup"><span data-stu-id="18353-135">Full screen</span></span>](#full-screen)
- [<span data-ttu-id="18353-136">복제</span><span class="sxs-lookup"><span data-stu-id="18353-136">Clone</span></span>](#clone-dashboard)
- [<span data-ttu-id="18353-137">삭제</span><span class="sxs-lookup"><span data-stu-id="18353-137">Delete</span></span>](#delete-dashboard)

<a name="select-dashboard"></a>

## <a name="select-dashboard"></a><span data-ttu-id="18353-138">대시보드 선택</span><span class="sxs-lookup"><span data-stu-id="18353-138">Select dashboard</span></span>

<span data-ttu-id="18353-139">도구 모음의 왼쪽 끝에는 **대시보드 선택** 드롭다운 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-139">To the far left of the toolbar is the **Select Dashboard** drop-down control.</span></span> <span data-ttu-id="18353-140">이 컨트롤을 클릭하면 계정에 대해 이미 정의한 대시보드 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-140">Clicking this control enables you to select from dashboards that you have already defined for your account.</span></span> <span data-ttu-id="18353-141">이 컨트롤을 사용하면 다양한 용도의 여러 대시보드를 정의한 후에 그때그때 수행하는 작업에 따라 원하는 대시보드로 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-141">This control makes it simple for you to define multiple dashboards for different purposes and then switch from one to another and back again, depending on what you are trying to do at the time.</span></span>

<span data-ttu-id="18353-142">대시보드를 만들면 처음에는 비공개 상태입니다. 즉, 만든 사람만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-142">Note that any dashboards that you create will initially be private; that is, only you can see them.</span></span> <span data-ttu-id="18353-143">대시보드를 엔터프라이즈 전체에서 사용하도록 하려면 대시보드를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-143">To make a dashboard available across your enterprise, you need to share it.</span></span> <span data-ttu-id="18353-144">이 옵션도 곧 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-144">We'll look at that option shortly.</span></span>

<a name="create-new"></a>

## <a name="create-a-new-dashboard"></a><span data-ttu-id="18353-145">새 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="18353-145">Create a new dashboard</span></span>

<span data-ttu-id="18353-146">새 대시보드를 만들려면 **새 대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-146">To create a new dashboard, click **New dashboard**.</span></span> <span data-ttu-id="18353-147">타일이 없는 대시보드 작업 영역이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-147">The dashboard workspace appears, with no tiles present.</span></span> <span data-ttu-id="18353-148">이제 원하는 어떤 방법으로든 타일을 추가, 제거 및 조정할 수 있습니다. 이 내용은 나중에 좀 더 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-148">You can then add, remove and adjust tiles however you like - we'll look more at this in a bit.</span></span> <span data-ttu-id="18353-149">대시보드 사용자 지정이 끝나면 **사용자 지정 완료**를 클릭하여 저장하고 해당 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-149">When you are finished customizing the dashboard, click **Done customizing** to save and switch to that dashboard.</span></span>

<a name="upload-download"></a>

## <a name="upload-and-download"></a><span data-ttu-id="18353-150">업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="18353-150">Upload and Download</span></span>

<span data-ttu-id="18353-151">**업로드** 및 **다운로드** 단추를 사용하면 현재 대시보드를 JSON 파일로 다운로드하고 사용자 지정하여 배포 및 업로드할 수도 있고, 다른 사용자가 해당 파일을 Azure Portal에 다시 업로드하여 해당 사용자의 현재 대시보드를 바꾸도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-151">The **Upload** and **Download** buttons enable you to download your current dashboard as a JSON file, customize it, and then distribute it and upload it or have someone else upload that file back to the Azure portal, thereby replacing their current dashboard.</span></span>

<span data-ttu-id="18353-152">**다운로드**를 클릭하면 현재 대시보드가 기본 다운로드 폴더로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-152">If you click **Download**, the current dashboard downloads into your default Downloads folder.</span></span> <span data-ttu-id="18353-153">다운로드한 파일을 열면 JSON 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-153">Opening the downloaded file then shows the JSON code.</span></span>

![대시보드 JSON 코드](../media-draft/8-dashboard-json-code.png)

<span data-ttu-id="18353-155">그러면 수동으로 해당 코드를 편집하고(예: 타일 크기 변경) **업로드** 단추를 클릭하여 Azure에 다시 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-155">You can then edit that code manually (for example, by changing tile sizes) and then upload it back to Azure by clicking the **Upload** button.</span></span>

<a name="edit-dashboard"></a>

### <a name="edit-a-dashboard"></a><span data-ttu-id="18353-156">대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="18353-156">Edit a dashboard</span></span>

<span data-ttu-id="18353-157">JSON 파일을 다운로드하여 파일의 값을 변경하고 파일을 Azure에 다시 업로드하여 대시보드를 편집할 수는 있지만 이러한 방식은 사용자 인터페이스를 설계하는 데 직관적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-157">Although you can edit a dashboard by downloading the JSON file, changing values in the file, and uploading the file back to Azure, that approach isn't intuitive for designing a user interface.</span></span> <span data-ttu-id="18353-158">GUI를 사용하여 현재 대시보드를 구성하기 위해 여러 가지 방법으로 편집 모드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-158">To use the GUI to configure your current dashboard you can enter edit mode in several ways:</span></span>

1. <span data-ttu-id="18353-159">**편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-159">Click the **Edit** button</span></span>
1. <span data-ttu-id="18353-160">대시보드를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-160">Right-click on the dashboard and click **Edit**.</span></span> 
1. <span data-ttu-id="18353-161">대시보드에서 타일을 마우스로 가리키면 맨 위/오른쪽 모서리에 `...` 메뉴가 편집 옵션과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="18353-161">Hover over a tile on the dashboard - a `...` menu will appear on the top/right corner with edit options.</span></span>

<span data-ttu-id="18353-162">대시보드가 편집 모드로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-162">The dashboard switches to edit mode.</span></span>

![대시보드 편집](../media-draft/8-edit-dashboard.png)

<span data-ttu-id="18353-164">왼쪽에는 사용 가능한 일부 타일을 포함하는 타일 갤러리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-164">On the left-hand side appears the Tile Gallery, with several possible tiles.</span></span> <span data-ttu-id="18353-165">타일 갤러리는 다음과 같은 기준으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-165">You can filter the Tile Gallery by the following criteria:</span></span>

- <span data-ttu-id="18353-166">일반</span><span class="sxs-lookup"><span data-stu-id="18353-166">General</span></span>
- <span data-ttu-id="18353-167">type</span><span class="sxs-lookup"><span data-stu-id="18353-167">Type</span></span>
- <span data-ttu-id="18353-168">검색</span><span class="sxs-lookup"><span data-stu-id="18353-168">Search</span></span>
- <span data-ttu-id="18353-169">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="18353-169">Resource Group</span></span>
- <span data-ttu-id="18353-170">태그</span><span class="sxs-lookup"><span data-stu-id="18353-170">Tag</span></span>

![타일 갤러리](../media-draft/8-tile-gallery.png)

<span data-ttu-id="18353-172">이러한 각 옵션을 Azure Active Directory, IoT(사물 인터넷), Microsoft Intune 등과 같은 범주별로 더 세분화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-172">You can also further refine each of these options by category (for example, Azure Active Directory, Internet of Things [IoT], Microsoft Intune, and so on).</span></span>

<span data-ttu-id="18353-173">타일 추가하기는 왼쪽의 목록에서 타일을 선택한 다음 작업 영역으로 끌어오는 것만큼 쉽습니다</span><span class="sxs-lookup"><span data-stu-id="18353-173">Adding tiles is as easy as selecting the tile from the list on the left and then dragging it to the work area.</span></span> <span data-ttu-id="18353-174">그런 다음, 각 타일을 이동하거나 크기를 조정하거나 표시되는 데이터를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-174">You can then move each tile about, resize it, or change the data that it displays.</span></span>

> [!TIP]
> <span data-ttu-id="18353-175">많은 사람들이 모르는 한 가지 멋진 기능은 하위 블레이드에 요소를 가져 와서 대시보드에 배치할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="18353-175">One cool feature a lot of people are unaware of is that you can take elements on child blades and put them on your dashboard.</span></span> <span data-ttu-id="18353-176">항목에 마우스를 올리고 `...` 타일 편집 메뉴를 찾습니다. 여기에는 “대시보드에 고정” 옵션이 있어서 서비스에서 타일을 가져와서 대시보드에 신속하게 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-176">Just hover over the item and look for the `...` tile edit menu - this will have a "Pin to Dashboard" option which lets you quickly grab a tile from a service and put it onto the dashboard.</span></span>

<span data-ttu-id="18353-177">편집 모드의 작업 영역은 사각형으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-177">The work area in edit mode is divided into squares.</span></span> <span data-ttu-id="18353-178">타일마다 하나 이상의 사각형을 사용해야 하며 타일은 가장 가까운 최대 타일 구분선 집합에 맞춰집니다.</span><span class="sxs-lookup"><span data-stu-id="18353-178">Each tile must occupy at least one square, and tiles will snap to the nearest largest set of tile dividers.</span></span> <span data-ttu-id="18353-179">겹치는 타일은 방해되지 않도록 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-179">Any overlapping tiles are moved out of the way.</span></span> <span data-ttu-id="18353-180">한 타일을 작게 만들면 주변 타일이 해당 타일에 맞춰 다시 위로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-180">When you make a tile smaller, the surrounding tiles will move back up against it.</span></span>

#### <a name="change-tile-sizes"></a><span data-ttu-id="18353-181">타일 크기 변경</span><span class="sxs-lookup"><span data-stu-id="18353-181">Change tile sizes</span></span>

<span data-ttu-id="18353-182">일부 타일은 크기가 설정되어 있으며 프로그래밍 방식으로만 크기를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-182">Some tiles have a set size, and you can edit their size only programmatically.</span></span> <span data-ttu-id="18353-183">그러나 오른쪽 아래 회색 모서리가 있는 타일은 모서리 표시기를 끌어다 놓아서 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-183">However, you can edit tiles with a gray bottom right-hand corner by dragging the corner indicator.</span></span>

![크기 조정 가능한 타일](../media-draft/8-resizable-tile.png)

<span data-ttu-id="18353-185">또는 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭하고 원하는 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-185">Alternatively, right-click the context menu and specify the size you want.</span></span>

![타일 크기](../media-draft/8-tile-size.png)

<span data-ttu-id="18353-187">대시보드를 만들려면 타일 갤러리에서 작업 영역으로 타일을 끌어온 후에 다시 배열하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-187">To create your dashboard, pull tiles from the Tile Gallery onto the workspace and then rearrange them.</span></span>

#### <a name="change-tile-settings"></a><span data-ttu-id="18353-188">타일 설정 변경</span><span class="sxs-lookup"><span data-stu-id="18353-188">Change tile settings</span></span>

<span data-ttu-id="18353-189">일부 타일에는 편집 가능한 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-189">Some tiles have editable settings.</span></span> <span data-ttu-id="18353-190">예를 들어 시계 타일을 작업 영역으로 끌어오면 **시계 편집** 타일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="18353-190">For example, with the clock tile, when you drag it onto the workspace, it opens the **Edit clock** tile.</span></span> <span data-ttu-id="18353-191">그러면 표시되는 표준 시간대를 설정하고 시간 표시도 12시간 형식인지 24시간 형식인지 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-191">You can then set the time zone, which it displays, and also set whether it displays in 12- or 24-hour format.</span></span>

![시계 편집](../media-draft/8-edit-clock.png)

<span data-ttu-id="18353-193">여러 국가 또는 여러 대륙에서 운영되는 기업의 경우 서로 다른 표준 시간대의 시계를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-193">For multi-national or transcontinental companies, you can add clocks, each in a different time zone.</span></span>

#### <a name="accepting-your-edits"></a><span data-ttu-id="18353-194">편집 수락</span><span class="sxs-lookup"><span data-stu-id="18353-194">Accepting your edits</span></span>

<span data-ttu-id="18353-195">타일을 원하는 대로 정렬한 경우 **사용자 지정 완료**를 클릭하거나 마우스 오른쪽 단추를 클릭하고 **사용자 지정 완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-195">When you have arranged the tiles as you want them, either click **Done customizing**, or right-click and then click **Done customizing**.</span></span>

## <a name="edit-a-dashboard-by-changing-the-json-file"></a><span data-ttu-id="18353-196">JSON 파일을 변경하여 대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="18353-196">Edit a dashboard by changing the JSON file</span></span>

<span data-ttu-id="18353-197">JSON 파일을 변경하여 대시보드를 편집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-197">You can also edit a dashboard by changing the JSON file.</span></span> <span data-ttu-id="18353-198">이 방법은 더 많은 설정 변경 옵션을 제공하지만 파일을 Azure로 다시 업로드할 때까지 변경 내용을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-198">This approach provides more options for changing settings, but you cannot see the changes until you upload the file back into Azure.</span></span>

![JSON 설정](../media-draft/8-json-code.png)

<span data-ttu-id="18353-200">위의 예에서 타일 크기를 변경하려면 **colSpan** 및 **rowSpan** 변수를 편집한 후 파일을 저장하고 Azure에 다시 해당 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-200">In the example above, to change the size of the tile, edit the **colSpan** and **rowSpan** variables, then save the file and upload it back to Azure.</span></span> <span data-ttu-id="18353-201">파일을 다른 사용자에게 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-201">You can also distribute the file to other users.</span></span>

## <a name="reset-a-dashboard"></a><span data-ttu-id="18353-202">대시보드 다시 설정</span><span class="sxs-lookup"><span data-stu-id="18353-202">Reset a dashboard</span></span>

<span data-ttu-id="18353-203">모든 대시보드를 기본 스타일로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-203">You can reset any dashboard to the default style.</span></span> <span data-ttu-id="18353-204">편집 모드에서 마우스 오른쪽 단추를 클릭하고 **Reset to default state**(기본 상태로 다시 설정)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-204">In edit mode, right-click and select **Reset to default state**.</span></span> <span data-ttu-id="18353-205">대화 상자에 대시보드를 다시 설정할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-205">A dialog box will ask you to confirm that you want to reset that dashboard.</span></span>

<a name="share-dashboard"></a>

## <a name="share-or-unshare-a-dashboard"></a><span data-ttu-id="18353-206">대시보드 공유 또는 공유 해제</span><span class="sxs-lookup"><span data-stu-id="18353-206">Share or unshare a dashboard</span></span>

<span data-ttu-id="18353-207">새 대시보드를 정의하면 해당 대시보드는 비공개 상태이며 자신의 계정에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-207">When you define a new dashboard, it is private and visible only to your account.</span></span> <span data-ttu-id="18353-208">다른 사람에게 표시되도록 하려면 대시보드를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-208">To make it visible to others, you need to share a dashboard.</span></span> <span data-ttu-id="18353-209">그러나 다른 모든 Azure 리소스와 마찬가지로 공유 대시보드를 저장할 리소스 그룹을 지정(또는 기존 리소스 그룹을 사용)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-209">However, as with any other Azure resource, you need to specify a resource group (or use an existing resource group) to store shared dashboards in.</span></span> <span data-ttu-id="18353-210">기존 리소스 그룹이 없는 경우 Azure는 사용자가 지정하는 위치에 ‘대시보드’ 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18353-210">If you do not have an existing resource group, Azure will create a *dashboards* resource group in whichever location you specify.</span></span> <span data-ttu-id="18353-211">기존 리소스 그룹이 있는 경우 해당 리소스 그룹에 대시보드를 저장하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-211">If you have existing resource groups, you can specify that resource group to store the dashboards.</span></span>

![공유 및 액세스 제어 1](../media-draft/8-share-dashboards-default.png)

<span data-ttu-id="18353-213">템플릿을 공유한 경우 두 번째 **공유 + 액세스 제어** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-213">When you have shared the template, you will see a second **Sharing + access control** blade.</span></span>

![공유 및 액세스 제어 2](../media-draft/8-share-dashboards-access-control.png)

<span data-ttu-id="18353-215">그러면 **사용자 관리**를 클릭하여 해당 대시보드에 액세스할 수 있는 사용자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-215">You can then click **Manage users** to specify the users who have access to that dashboard.</span></span>

### <a name="switching-to-a-shared-dashboard"></a><span data-ttu-id="18353-216">공유 대시보드로 전환</span><span class="sxs-lookup"><span data-stu-id="18353-216">Switching to a shared dashboard</span></span>

<span data-ttu-id="18353-217">공유 대시보드로 전환하려면 대시보드 목록을 클릭한 후에 **모든 대시보드 찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-217">To switch to a shared dashboard, you click on the list of dashboards, and then click **Browse all dashboards**.</span></span>

![모든 대시보드 찾아보기](../media-draft/8-browse-dashboards.png)

<span data-ttu-id="18353-219">이제 공유 대시보드의 이름이 있는 **모든 대시보드** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-219">You will now see the **All dashboards** blade, with the names of any shared dashboards displayed.</span></span> <span data-ttu-id="18353-220">대시보드를 클릭하기만 하면 Azure Portal에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-220">Just click on a dashboard to apply it to the Azure portal.</span></span>

![공유 대시보드](../media-draft/8-select-shared-dashboard.png)

<a name="full-screen"></a>

## <a name="display-a-dashboard-as-a-full-screen"></a><span data-ttu-id="18353-222">대시보드를 전체 화면으로 표시</span><span class="sxs-lookup"><span data-stu-id="18353-222">Display a dashboard as a full screen</span></span>

<span data-ttu-id="18353-223">대시보드를 최대 크기로 표시하려는 경우에는 **전체 화면** 단추를 클릭하면 현재 대시보드가 브라우저 메뉴 없이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-223">If you want the largest dashboard real estate, click the **Full screen** button to display your current dashboard without any browser menus.</span></span> <span data-ttu-id="18353-224">화면 표시 경계 외부에 타일이 있으면 화면 오른쪽과 아래쪽에 슬라이더 막대가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="18353-224">If you have any tiles outside the boundaries of your screen display, slider bars will appear at the right and bottom of your screen.</span></span>

<span data-ttu-id="18353-225">전체 화면 모드에서 작업을 완료한 경우 Esc 키를 누르거나 화면 맨 위에 있는 대시보드 이름 옆의 **전체 화면 끝내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-225">When you have finished working in full-screen mode, press the ESC key or click **Exit Full Screen** next to the Dashboard name at the top of the screen.</span></span>

<a name="clone-dashboard"></a>

## <a name="clone-a-dashboard"></a><span data-ttu-id="18353-226">대시보드 복제</span><span class="sxs-lookup"><span data-stu-id="18353-226">Clone a dashboard</span></span>

<span data-ttu-id="18353-227">대시보드를 복제하면 “\<대시보드 이름> 복제본”이라는 인스턴트 복사본이 만들어지고 해당 복사본이 현재 대시보드로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-227">Cloning a dashboard creates an instant copy called "Clone of \<dashboard name>" and switches to that copy as the current dashboard.</span></span> <span data-ttu-id="18353-228">복제는 대시보드를 공유하기 전에 대시보드를 만들 수 있는 쉬운 방법이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="18353-228">Cloning is also an easy way to create dashboards before sharing them.</span></span> <span data-ttu-id="18353-229">예를 들어 원하는 것에 거의 가까운 대시보드가 있는 경우에는 이 대시보드를 복제하고 필요한 내용을 변경한 후에 공유하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-229">For example, if you have a dashboard that is almost as you want it, clone it, make the changes that you need, and then share it.</span></span>

<a name="delete-dashboard"></a>

## <a name="delete-a-dashboard"></a><span data-ttu-id="18353-230">대시보드 삭제</span><span class="sxs-lookup"><span data-stu-id="18353-230">Delete a dashboard</span></span>

<span data-ttu-id="18353-231">대시보드를 삭제하면 사용 가능한 대시보드 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="18353-231">Deleting a dashboard removes it from your list of available dashboards.</span></span> <span data-ttu-id="18353-232">대시보드를 삭제할 것인지 확인하는 메시지가 표시되지만 삭제된 대시보드를 복구하는 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-232">You are prompted to confirm that you want to delete the dashboard, but there is no facility to recover a dashboard that has been deleted.</span></span>

<span data-ttu-id="18353-233">새 대시보드를 만들어서 이러한 옵션 중 일부를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18353-233">Let's try out some of these options by creating a new dashboard.</span></span>
