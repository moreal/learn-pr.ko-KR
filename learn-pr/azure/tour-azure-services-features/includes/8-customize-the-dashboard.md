<span data-ttu-id="780ad-101">여기에서는 포털 UI를 사용하고 기본 JSON 파일을 직접 편집하여 대시보드를 만들고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-101">Here, you will create and modify dashboards using the portal UI and by editing the underlying JSON file directly.</span></span>

## <a name="what-is-a-dashboard"></a><span data-ttu-id="780ad-102">대시보드란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="780ad-102">What is a Dashboard?</span></span>

<span data-ttu-id="780ad-103">_대시보드_는 Azure Portal에 표시되는 사용자 지정 가능한 UI 타일 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-103">A _dashboard_ is a customizable collection of UI tiles displayed in the Azure portal.</span></span> <span data-ttu-id="780ad-104">타일을 추가, 제거 및 배치하여 원하는 뷰를 만들고 해당 뷰를 대시보드로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-104">You add, remove, and position tiles to create the exact view you want, then save that view as a dashboard.</span></span> <span data-ttu-id="780ad-105">여러 대시보드가 지원되며 필요에 따라 대시보드 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-105">Multiple dashboards are supported and you can switch between them as needed.</span></span> <span data-ttu-id="780ad-106">다른 팀 구성원과 대시보드를 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-106">You can even share your dashboards with other team members.</span></span>

<span data-ttu-id="780ad-107">대시보드는 Azure 관리 방법 측면에서 상당한 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-107">Dashboards give you considerable flexibility in terms of how you manage Azure.</span></span> <span data-ttu-id="780ad-108">예를 들어 조직 내의 특정 역할에 대한 대시보드를 만들고 RBAC(역할 기반 액세스 제어)를 사용하여 해당 대시보드에 액세스할 수 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-108">For example, you can create dashboards for specific roles within the organization, then use Role-Based Access Control (RBAC) to control who can access that dashboard.</span></span> <span data-ttu-id="780ad-109">따라서 데이터베이스 관리자에게는 SQL 데이터베이스 서비스 뷰가 있는 대시보드가 있고 Azure Active Directory 관리자에게는 Azure AD 내 사용자 및 그룹에 대한 뷰가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-109">Hence, your database administrator would have a dashboard that contains views of the SQL database service, whereas your Azure Active Directory administrator would have views of the users and groups within Azure AD.</span></span>

<span data-ttu-id="780ad-110">대시보드는 .JSON(JavaScript Object Notation) 파일로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-110">Dashboards are stored as JavaScript Object Notation (.JSON) files.</span></span> <span data-ttu-id="780ad-111">다른 컴퓨터에 업로드 및 다운로드되거나 Azure 디렉터리 멤버와 공유될 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-111">This means they can be uploaded and downloaded to other computers, or shared with members of the Azure directory.</span></span> <span data-ttu-id="780ad-112">Azure는 포털 내에서 관리할 수 있는 가상 머신이나 저장소 계정과 같이 리소스 그룹 내에 대시보드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-112">Azure stores dashboards within resource groups, just like virtual machines or storage accounts that you can manage within the portal.</span></span>

<span data-ttu-id="780ad-113">대시보드는 .JSON 파일이므로 대시보드를 프로그래밍 방식으로 사용자 지정하여 강력한 관리 도구를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-113">Because dashboards are .JSON files, you can can also customize dashboards programmatically, making them very powerful administrative tools.</span></span> <span data-ttu-id="780ad-114">또한 일부 타일 유형은 원본 데이터가 변경되면 자동으로 업데이트되도록 쿼리를 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-114">In addition, some tile types can be query-based so they update automatically when the source data changes.</span></span>

## <a name="default-dashboard"></a><span data-ttu-id="780ad-115">기본 대시보드</span><span class="sxs-lookup"><span data-stu-id="780ad-115">Default Dashboard</span></span>

<span data-ttu-id="780ad-116">기본 대시보드는 간단히 대시보드로 이름이 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-116">The default Dashboard is simply named Dashboard.</span></span> <span data-ttu-id="780ad-117">포털에 로그인하면 5개의 웹 파트가 포함된 이 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-117">When you log into the portal, you are presented with this dashboard containing five web parts.</span></span>

![기본 웹 파트](../images/4-dashboard-default-webparts.png)

<span data-ttu-id="780ad-119">기본 웹 파트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-119">These default web parts are</span></span>

1. <span data-ttu-id="780ad-120">모든 리소스</span><span class="sxs-lookup"><span data-stu-id="780ad-120">All resources</span></span>
2. <span data-ttu-id="780ad-121">빠른 시작 + 자습서</span><span class="sxs-lookup"><span data-stu-id="780ad-121">Quickstarts + tutorials</span></span>
3. <span data-ttu-id="780ad-122">서비스 상태</span><span class="sxs-lookup"><span data-stu-id="780ad-122">Service Health</span></span>
4. <span data-ttu-id="780ad-123">Marketplace</span><span class="sxs-lookup"><span data-stu-id="780ad-123">Marketplace</span></span>
5. <span data-ttu-id="780ad-124">Azure 시작</span><span class="sxs-lookup"><span data-stu-id="780ad-124">Azure Getting Started</span></span>

## <a name="creating-and-managing-dashboards"></a><span data-ttu-id="780ad-125">대시보드 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="780ad-125">Creating and Managing Dashboards</span></span>

<span data-ttu-id="780ad-126">대시보드 맨 위에는 대시보드를 만들고, 업로드하고, 다운로드하고, 편집하고, 공유할 수 있는 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-126">Along the top of the dashboard are the controls that enable you to create, upload, download, edit, and share a dashboard.</span></span> <span data-ttu-id="780ad-127">대시보드를 전체 화면으로 전환하거나 복제하거나 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-127">You can also switch a dashboard to full screen, clone it, or delete it.</span></span>

![대시보드 컨트롤 사용자 지정](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a><span data-ttu-id="780ad-129">대시보드 선택</span><span class="sxs-lookup"><span data-stu-id="780ad-129">Select Dashboard</span></span>

<span data-ttu-id="780ad-130">왼쪽에는 대시보드 선택 드롭다운 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-130">To the left is the Select Dashboard drop-down control.</span></span> <span data-ttu-id="780ad-131">이 컨트롤을 클릭하면 계정에 대해 이미 정의한 대시보드 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-131">Clicking this control enables you to select from dashboards that you have already defined for your account.</span></span> <span data-ttu-id="780ad-132">이 컨트롤을 사용하면 다양한 용도의 여러 대시보드를 간단히 정의한 후에 그때그때 수행하는 작업에 따라 수시로 한 대시보드에서 다른 대시보드로 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-132">This control makes it simple for you to define multiple dashboards for different purposes, then simply switch from one to another and back again, depending on what you are trying to do at the time.</span></span>

<span data-ttu-id="780ad-133">자신이 만드는 대시보드는 처음에는 비공개 상태입니다. 따라서, 자신만 해당 대시보드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-133">Note that any dashboards that you create will initially be private; that is, only you can see them.</span></span> <span data-ttu-id="780ad-134">대시보드를 엔터프라이즈 전체에서 사용할 수 있게 하려면 대시보드를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-134">To make a dashboard avaiable across your enterprise, you need to share it.</span></span> <span data-ttu-id="780ad-135">대시보드 공유/공유 해제에 대한 자세한 내용은 이후 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="780ad-135">See the later section on sharing/unsharing dashboards for more information.</span></span>

### <a name="create-a-new-dashboard"></a><span data-ttu-id="780ad-136">새 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="780ad-136">Create a new dashboard</span></span>

<span data-ttu-id="780ad-137">새 대시보드를 만들려면 간단히 **새 대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-137">To create a new dashboard, simply click **New dashboard**.</span></span> <span data-ttu-id="780ad-138">타일이 없는 대시보드 작업 영역이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-138">The dashboard workspace appears, with no tiles present.</span></span> <span data-ttu-id="780ad-139">이제 이 단원의 뒷 부분에 나오는 사용자 인터페이스를 통한 대시보드 편집 섹션에 자세히 설명된 대로 타일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-139">You can now add tiles, as detailed in the later section on Edit a Dashboard through the User Interface later in this unit.</span></span> <span data-ttu-id="780ad-140">타일 추가 및 조정을 완료하고 대시보드 이름을 변경했으면 간단히 **사용자 지정 완료**를 클릭하여 저장하고 해당 대시보드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-140">When you have completed adding and adjusting tiles, and changed the name of the dashboard, simply click **Done customizing** to save and switch to that dashboard.</span></span>

### <a name="upload-and-download"></a><span data-ttu-id="780ad-141">업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="780ad-141">Upload and Download</span></span>

<span data-ttu-id="780ad-142">**업로드** 및 **다운로드** 단추를 사용하면 현재 대시보드를 .JSON 파일로 다운로드하고 사용자 지정하여 배포 및 업로드할 수도 있고, 다른 사용자가 해당 파일을 Azure Portal에 다시 업로드하여 해당 사용자의 현재 대시보드를 바꾸도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-142">The **Upload** and **Download** buttons enable you to download your current dashboard as a .JSON file, customize it, then distribute it and upload it or have someone else upload that file back to the Azure Portal, thereby replacing their current dashboard.</span></span>

<span data-ttu-id="780ad-143">**다운로드**를 클릭하면 현재 대시보드가 기본 다운로드 폴더로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-143">If you click **Download**, the current dashboard downloads into your default Downloads folder.</span></span> <span data-ttu-id="780ad-144">다운로드한 파일을 열면 .JSON 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-144">Opening the downloaded file then shows the .JSON code.</span></span>

![대시보드 JSON 코드](../images/7-dashboard-json-code.PNG)

<span data-ttu-id="780ad-146">그러면 타일 크기 변경과 같이 수동으로 해당 코드를 편집하고 **업로드** 단추를 클릭하여 Azure에 다시 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-146">You can then edit that code manually, for example, by changing tile sizes, and then upload it back to Azure by clicking the **Upload** button.</span></span>

### <a name="edit-a-dashboard"></a><span data-ttu-id="780ad-147">대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="780ad-147">Edit a Dashboard</span></span>

<span data-ttu-id="780ad-148">이 항목에 대한 자세한 내용은 사용자 인터페이스를 통한 대시보드 편집 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="780ad-148">See the Edit a Dashboard through the User Interface topic for more information on this topic.</span></span>

### <a name="shareunshare-a-dashboard"></a><span data-ttu-id="780ad-149">대시보드 공유/공유 해제</span><span class="sxs-lookup"><span data-stu-id="780ad-149">Share/Unshare a Dashboard</span></span>

<span data-ttu-id="780ad-150">새 대시보드를 정의하면 해당 대시보드는 비공개 상태이며 자신의 계정에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-150">When you define a new dashboard, it is private and only visible to your account.</span></span> <span data-ttu-id="780ad-151">다른 사람에게 표시되도록 하려면 대시보드를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-151">To make it visible to others, you need to share a dashboard.</span></span> <span data-ttu-id="780ad-152">그러나 다른 모든 Azure 리소스와 마찬가지로 공유 대시보드를 저장할 리소스 그룹을 지정(또는 기존 리소스 그룹을 사용)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-152">However, like any other Azure resource, you need to specify a Resource Group (or use an existing resource group) to store shared dashboards in.</span></span> <span data-ttu-id="780ad-153">기존 리소스 그룹이 없는 경우 Azure는 사용자가 지정하는 위치에 ‘대시보드’ 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-153">If you do not have an existing resource group, Azure will create a 'dashboards' resource group in whichever Location you specify.</span></span> <span data-ttu-id="780ad-154">기존 리소스 그룹이 있는 경우 해당 리소스 그룹에 대시보드를 저장하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-154">If you have existing resource groups, then you can specify that resource group to store the dashboards.</span></span>

![공유 및 액세스 제어 1](../images/7-share-dashboards-default.PNG)

<span data-ttu-id="780ad-156">템플릿을 공유한 경우 두 번째 **공유 + 액세스 제어** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-156">When you have shared the template, you will see a second **Sharing + access control** blade.</span></span>

![공유 및 액세스 제어 2](../images/7-share-dashboards-access-control.PNG)

<span data-ttu-id="780ad-158">그러면 **사용자 관리**를 클릭하여 해당 대시보드에 액세스할 수 있는 사용자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-158">You can then click **Manage users** to specify the users who have access to that dashboard.</span></span>

### <a name="switching-to-a-shared-dashboard"></a><span data-ttu-id="780ad-159">공유 대시보드로 전환</span><span class="sxs-lookup"><span data-stu-id="780ad-159">Switching to a shared dashboard</span></span>

<span data-ttu-id="780ad-160">공유 대시보드로 전환하려면 대시보드 목록을 클릭한 후에 **모든 대시보드 찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-160">To switch to a shared dashboard, you click on the list of dashboards, then click **Browse all dashboards**.</span></span>

![모든 대시보드 찾아보기](../images/7-browse-dashboards.PNG)

<span data-ttu-id="780ad-162">이제 모든 공유 대시보드의 이름이 나와 있는 모든 대시보드 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-162">You will now see the All dashboards blade, with the names of any shared dashboards displayed.</span></span> <span data-ttu-id="780ad-163">간단히 대시보드를 클릭하여 Azure Portal에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-163">Simply click on a dashboard to apply it to the Azure portal.</span></span>

![공유 대시보드](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a><span data-ttu-id="780ad-165">대시보드를 전체 화면으로 표시</span><span class="sxs-lookup"><span data-stu-id="780ad-165">Display a Dashboard as a Full Screen</span></span>

<span data-ttu-id="780ad-166">대시보드를 최대 크기로 표시하려면 **전체 화면** 단추를 클릭하여 브라우저 메뉴 없이 현재 대시보드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-166">If you really want the largest dashboard real estate, click the **Full screen** button to display your current dashboard without any browser menus.</span></span> <span data-ttu-id="780ad-167">화면 표시 경계를 벗어나는 타일이 있는 경우 화면 오른쪽과 아래쪽에 슬라이더 막대가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-167">If you have any tiles that are outside the boundaries of your screen display, then slider bars will appear at the right and bottom of your screen.</span></span>

<span data-ttu-id="780ad-168">전체 화면 모드에서 작업을 완료한 경우 Esc 키를 누르거나 화면 맨 위에 있는 대시보드 이름 옆의 **전체 화면 끝내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-168">When you have finished working in full screen mode, press the Escape key or click **Exit Full Screen** next to the Dashboard name at the top of the screen.</span></span>

### <a name="clone-a-dashboard"></a><span data-ttu-id="780ad-169">대시보드 복제</span><span class="sxs-lookup"><span data-stu-id="780ad-169">Clone a Dashboard</span></span>

<span data-ttu-id="780ad-170">대시보드를 복제하기만 하면 “(대시보드 이름) 복제본”이라는 인스턴트 복사본이 만들어지고 해당 복사본이 현재 대시보드로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-170">Cloning a dashboard simply creates an instant copy called "Clone of (dashboard name)" and switches to that copy as the current dashboard.</span></span> <span data-ttu-id="780ad-171">복제를 사용하면 쉽게 대시보드를 만든 다음, 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-171">Cloning is also an easy way to create dashboards prior to sharing them.</span></span> <span data-ttu-id="780ad-172">예를 들어 원하는 것과 거의 동일한 대시보드가 있는 경우 해당 대시보드를 복제하고 필요한 내용을 변경한 후에 공유하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-172">For example, if you have a dashboard that is almost as you want it, simply clone it, then make the changes that you need, and then share it.</span></span>

### <a name="delete-a-dashboard"></a><span data-ttu-id="780ad-173">대시보드 삭제</span><span class="sxs-lookup"><span data-stu-id="780ad-173">Delete a Dashboard</span></span>

<span data-ttu-id="780ad-174">대시보드를 삭제하면 사용 가능한 대시보드 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-174">Deleting a dashboard removes it from your list of available dashboards.</span></span> <span data-ttu-id="780ad-175">대시보드를 삭제할 것인지 확인하는 메시지가 표시되지만 삭제된 대시보드를 복구하는 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-175">You are prompted to confirm that you want to delete the dashboard, but there is no facility to recover a dashboard that has been deleted.</span></span>

## <a name="edit-a-dashboard-through-the-user-interface"></a><span data-ttu-id="780ad-176">사용자 인터페이스를 통한 대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="780ad-176">Edit a Dashboard through the User Interface</span></span>

<span data-ttu-id="780ad-177">.JSON 파일을 다운로드하여 파일의 값을 변경하고 파일을 다시 Azure에 업로드하여 대시보드를 편집할 수는 있지만 이러한 방식은 사용자 인터페이스 설계에 사용하기가 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-177">Although you can edit a dashboard by downloading the .JSON file, changing values in the file, and uploading the file back to Azure, that approach isn't terribly intuitive for designing a user interface.</span></span> <span data-ttu-id="780ad-178">GUI를 사용하여 현재 대시보드를 구성하려면 **편집** 단추를 클릭하거나 대시보드를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-178">To use the GUI to configure your current dashboard, click the **Edit** button or right-click on the dashboard and click **Edit**.</span></span> <span data-ttu-id="780ad-179">대시보드가 편집 모드로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-179">The dashboard switches to edit mode.</span></span>

![대시보드 편집](../images/7-edit-dashboard.PNG)

<span data-ttu-id="780ad-181">왼쪽에 타일 갤러리가 표시되고 아래에 여러 타일이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-181">On the left-hand side appears the Tile Gallery, with a number of tiles below.</span></span> <span data-ttu-id="780ad-182">타일 갤러리는 다음과 같은 기준으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-182">You can filter the Tile Gallery by the following criteria:</span></span>

* <span data-ttu-id="780ad-183">일반</span><span class="sxs-lookup"><span data-stu-id="780ad-183">General</span></span>
* <span data-ttu-id="780ad-184">type</span><span class="sxs-lookup"><span data-stu-id="780ad-184">Type</span></span>
* <span data-ttu-id="780ad-185">검색</span><span class="sxs-lookup"><span data-stu-id="780ad-185">Search</span></span>
* <span data-ttu-id="780ad-186">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="780ad-186">Resource Group</span></span>
* <span data-ttu-id="780ad-187">태그</span><span class="sxs-lookup"><span data-stu-id="780ad-187">Tag</span></span>

![타일 갤러리](../images/7-tile-gallery.png)

<span data-ttu-id="780ad-189">이러한 각 옵션을 Azure Active Directory, 사물 인터넷, Microsoft Intune 등과 같은 범주별로 더 구체화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-189">You can also further refine each of these options by category, for example, Azure Active Directory, Internet of Things, Microsoft Intune, and so on.</span></span>

<span data-ttu-id="780ad-190">타일을 추가하려면 간단히 왼쪽 목록에서 타일을 선택하여 작업 영역으로 끌어서 놓기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-190">Adding tiles is simply a question of selecting the tile from the list on the left, then dragging it and dropping it onto the work area.</span></span> <span data-ttu-id="780ad-191">그런 다음, 각 타일을 이동하거나 크기를 조정하거나 표시되는 데이터를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-191">You can then move each tile about, resize it, or change the data that it displays.</span></span>

<span data-ttu-id="780ad-192">작업 영역이 편집 모드인 경우 사각형으로 나뉘어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-192">The work area in edit mode is divided into squares.</span></span> <span data-ttu-id="780ad-193">타일마다 하나 이상의 사각형을 사용해야 하며 타일은 가장 가까운 최대 타일 구분선 집합에 맞춰집니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-193">Each tile must occuppy at least one square, and tiles will snap to the nearest largest set of tile dividers.</span></span> <span data-ttu-id="780ad-194">겹치는 타일은 방해되지 않도록 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-194">Any overlapping tiles are moved out of the way.</span></span> <span data-ttu-id="780ad-195">한 타일을 작게 만들면 주변 타일이 해당 타일에 맞춰 다시 위로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-195">When you make a tile smaller, the surrounding tiles will move back up against it.</span></span>

### <a name="change-tile-sizes"></a><span data-ttu-id="780ad-196">타일 크기 변경</span><span class="sxs-lookup"><span data-stu-id="780ad-196">Change tile sizes</span></span>

<span data-ttu-id="780ad-197">일부 타일은 설정된 크기가 있으므로 프로그래밍 방식으로만 크기를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-197">Some tiles have a set size and you can only edit their size programatically.</span></span> <span data-ttu-id="780ad-198">그러나 오른쪽 아래 회색 모서리가 있는 타일은 모서리 표시기를 끌어서 놓는 방법으로 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-198">However, tiles with a grey bottom right-hand corner you can edit by dragging and dropping the corner indicator.</span></span>

![크기 조정 가능한 타일](../images/7-resizable-tile.png)

<span data-ttu-id="780ad-200">또는 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭하고 원하는 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-200">Alternatively, right-click the context menu and specify the size you want.</span></span>

![타일 크기](../images/7-tile-size.png)

<span data-ttu-id="780ad-202">대시보드를 만들려면 타일 갤러리에서 작업 영역으로 타일을 끌어온 후에 다시 정렬하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-202">To create your dashboard, simply pull tiles from the Tile Gallery onto the workspace and then rearrange them.</span></span>

### <a name="change-tile-settings"></a><span data-ttu-id="780ad-203">타일 설정 변경</span><span class="sxs-lookup"><span data-stu-id="780ad-203">Change tile settings</span></span>

<span data-ttu-id="780ad-204">일부 타일에는 편집 가능한 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-204">Some tiles have editable settings.</span></span> <span data-ttu-id="780ad-205">예를 들어 시계 타일을 작업 영역으로 끌어오면 **시계 편집** 타일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-205">For example, with the clock tile, when you drag it onto the workspace, it opens up the **Edit clock** tile.</span></span> <span data-ttu-id="780ad-206">그러면 표시되는 표준 시간대를 설정하고 시간 표시도 12시간 형식인지 24시간 형식인지 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-206">You can then set the time zone  which it displays and also whether it displays in 12 or 24-hour format.</span></span>

![시계 편집](../images/7-edit-clock.png)

<span data-ttu-id="780ad-208">여러 국가 또는 여러 대륙에서 운영되는 기업의 경우 서로 다른 시간대의 시계를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-208">For multi-national or transcontinental companies, you can add further clocks, each in different time zones.</span></span>

### <a name="accepting-your-edits"></a><span data-ttu-id="780ad-209">편집 수락</span><span class="sxs-lookup"><span data-stu-id="780ad-209">Accepting your edits</span></span>

<span data-ttu-id="780ad-210">타일을 원하는 대로 정렬한 경우 **사용자 지정 완료**를 클릭하거나 마우스 오른쪽 단추를 클릭하고 **사용자 지정 완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-210">When you have arranged the tiles as you want them, either click **Done customizing**, or right-click and click **Done customizing**.</span></span>

## <a name="edit-a-dashboard-by-changing-the-json-file"></a><span data-ttu-id="780ad-211">.JSON 파일을 변경하여 대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="780ad-211">Edit a Dashboard by changing the .JSON file</span></span>

<span data-ttu-id="780ad-212">.JSON 파일을 변경하여 대시보드를 편집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-212">You can also edit a dashboard by changing the .JSON file.</span></span> <span data-ttu-id="780ad-213">이 방법은 더 많은 설정 변경 옵션을 제공하지만 파일을 Azure로 다시 업로드할 때까지 변경 내용을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-213">This approach provides more options for changing settings, but you cannot see the changes until you upload the file back into Azure.</span></span>

![JSON 설정](../images/7-json-code.png)

<span data-ttu-id="780ad-215">위의 예에서 타일 크기를 변경하려면 colSpan 및 rowSpan 변수를 편집한 후 파일을 저장하고 Azure에 다시 해당 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-215">In the example above, to change the size of the tile, edit the colSpan and rowSpan variables, then save the file and upload it back to Azure.</span></span> <span data-ttu-id="780ad-216">파일을 다른 사용자에게 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-216">You can also distribute the file to other users.</span></span>

## <a name="reset-a-dashboard"></a><span data-ttu-id="780ad-217">대시보드 다시 설정</span><span class="sxs-lookup"><span data-stu-id="780ad-217">Reset a dashboard</span></span>

<span data-ttu-id="780ad-218">모든 대시보드를 기본 스타일로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-218">You can reset any dashboard to the default style.</span></span> <span data-ttu-id="780ad-219">편집 모드에서 마우스 오른쪽 단추를 클릭하고 **Reset to default state**(기본 상태로 다시 설정)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-219">In edit mode, right-click and select **Reset to default state**.</span></span> <span data-ttu-id="780ad-220">해당 대시보드를 다시 설정할 것인지 확인하는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-220">A dialog box will ask you to confirm that you want to reset that dashboard.</span></span>

## <a name="summary"></a><span data-ttu-id="780ad-221">요약</span><span class="sxs-lookup"><span data-stu-id="780ad-221">Summary</span></span>

<span data-ttu-id="780ad-222">대시보드는 포털을 통해 Azure 서비스의 다양한 측면을 관리하는 데 사용되는 유연한 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-222">Dashboards provides a flexible tool for managing different aspects of Azure services through the Portal.</span></span> <span data-ttu-id="780ad-223">대시보드를 통해 편리하게 서비스 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-223">They make it convenient to monitor the state of your services.</span></span> <span data-ttu-id="780ad-224">대시보드는 공유할 수 있으므로 팀의 모든 구성원이 동일한 데이터를 보고 중요한 구성 요소의 상태를 계속 인식하고 있도록 하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="780ad-224">Because they are sharable, they help ensure that everyone on your team sees the same data and stays aware of the state of your critical components.</span></span>