<span data-ttu-id="f7b27-101">이 단원에서는 Data Migration Assistant를 사용하여 기존 데이터베이스를 평가하고, 로컬 SQL Server 인스턴스에서 사용되었지만 현재 Azure SQL Database에서는 지원되지 않는 기능을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-101">In this unit, you'll assess an existing database using the Data Migration Assistant and review any features used in the local SQL Server instance that aren't currently supported by Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="f7b27-102">설정</span><span class="sxs-lookup"><span data-stu-id="f7b27-102">Setup</span></span>

1. <span data-ttu-id="f7b27-103">[**Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595)를 아직 설치하지 않았으면 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-103">[Install the **Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595) if you haven't done so already.</span></span>

1. <span data-ttu-id="f7b27-104">SQL Server 인스턴스가 실행 중이어야 합니다. 연결 세부 정보를 사용할 수 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f7b27-104">You'll need a SQL Server instance running, ensure you have connection details available.</span></span>

<!-- 1. [**** likely replace with an LOD VM *****] TODO: -->

1. <span data-ttu-id="f7b27-105">인터넷 브라우저를 시작하여 https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-105">Start an Internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="f7b27-106">**OLTP 다운로드**에서 **AdventureWorks2008R2.bak**를 클릭하여 로컬 컴퓨터에 해당 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-106">In **OLTP downloads**, click **AdventureWorks2008R2.bak** and save it to your local machine.</span></span>

1. <span data-ttu-id="f7b27-107">Management Studio에서 *AdventureWorks 2008R2*를 기본 인스턴스로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-107">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-assessment"></a><span data-ttu-id="f7b27-108">평가 만들기</span><span class="sxs-lookup"><span data-stu-id="f7b27-108">Create an assessment</span></span>

1. <span data-ttu-id="f7b27-109">**Microsoft Data Migration Assistant**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-109">Start the **Microsoft Data Migration Assistant**.</span></span>

1. <span data-ttu-id="f7b27-110">앱의 왼쪽 탐색 영역에서 __+__ 를 클릭하여 새 Data Migration Assistant 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-110">In the app's left-hand navigation, click __+__ to create a new Data Migration Assistant project.</span></span>

1. <span data-ttu-id="f7b27-111">다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-111">Specify the following options:</span></span>

    - <span data-ttu-id="f7b27-112">**프로젝트 형식** - *평가*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-112">**Project type** - Select *Assessment*</span></span>
    - <span data-ttu-id="f7b27-113">**프로젝트 이름** - 프로젝트 이름을 "자전거 DB 평가"와 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-113">**Project name** - Enter a name for your project - for example, "Bicycle DB Assessment"</span></span>
    - <span data-ttu-id="f7b27-114">**원본 서버 유형** - *SQL Server*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-114">**Source server type** - Select *SQL Server*</span></span>
    - <span data-ttu-id="f7b27-115">**대상 서버 유형** - *Azure SQL Database*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-115">**Target server type** - Select *Azure SQL Database*</span></span>

1. <span data-ttu-id="f7b27-116">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-116">Click **Create**.</span></span>
    <span data-ttu-id="f7b27-117">![AdventureWorks SQL Server 데이터에 대해 설명한 구성이 적용된 Data Migration Assistant를 보여 주는 스크린샷.](../media-draft/3-create-assessment.png)</span><span class="sxs-lookup"><span data-stu-id="f7b27-117">![Screenshot showing the described configuration in the Data Migration Assistant for your AdventureWorks SQL Server data.](../media-draft/3-create-assessment.png)</span></span>

1. <span data-ttu-id="f7b27-118">평가 보고서 종류를 선택합니다. 다음 두 항목을 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-118">Select the assessment report type - check both:</span></span>
    - <span data-ttu-id="f7b27-119">데이터베이스 호환성 확인</span><span class="sxs-lookup"><span data-stu-id="f7b27-119">Check database compatibility</span></span>
    - <span data-ttu-id="f7b27-120">기능 패리티 확인</span><span class="sxs-lookup"><span data-stu-id="f7b27-120">Check feature parity</span></span>

1. <span data-ttu-id="f7b27-121">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-121">Click **Next**.</span></span>

## <a name="add-databases-to-assess"></a><span data-ttu-id="f7b27-122">평가할 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="f7b27-122">Add databases to assess</span></span>

1. <span data-ttu-id="f7b27-123">**원본 추가**를 클릭하여 연결 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-123">Click **Add Sources** to open the connection menu.</span></span>

1. <span data-ttu-id="f7b27-124">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-124">Do the following:</span></span>

    - <span data-ttu-id="f7b27-125">기존 SQL server 인스턴스 이름 입력</span><span class="sxs-lookup"><span data-stu-id="f7b27-125">Enter your existing SQL server instance name</span></span>
    - <span data-ttu-id="f7b27-126">**인증 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-126">Select the **Authentication** type</span></span>
    - <span data-ttu-id="f7b27-127">서버의 연결 속성 지정</span><span class="sxs-lookup"><span data-stu-id="f7b27-127">Specify the connection properties for your server</span></span>

1. <span data-ttu-id="f7b27-128">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-128">CLick **Connect**.</span></span>

1. <span data-ttu-id="f7b27-129">**원본 추가**에서 평가할 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-129">In **Add sources**, select the databases to assess.</span></span> <span data-ttu-id="f7b27-130">이 연습에서는 **AdventureWorks2008R2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-130">For this exercise, select **AdventureWorks2008R2**.</span></span>

1. <span data-ttu-id="f7b27-131">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-131">Click **Add**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="f7b27-132">여러 SQL Server 인스턴스에서 데이터베이스를 추가하려면 **원본 추가** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-132">To add databases from multiple SQL Server instances, use the **Add Sources** button.</span></span> <span data-ttu-id="f7b27-133">여러 데이터베이스를 제거하려면 Shift+Ctrl을 누른 상태로 제거할 데이터베이스를 선택한 다음 **원본 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-133">To remove multiple databases, hold the SHIFT+CTRL keys to select the databases you want to remove, then click **Remove Sources**.</span></span>

1. <span data-ttu-id="f7b27-134">**평가 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-134">Click **Start Assessment**.</span></span>

## <a name="view-results"></a><span data-ttu-id="f7b27-135">결과 보기</span><span class="sxs-lookup"><span data-stu-id="f7b27-135">View results</span></span>

<span data-ttu-id="f7b27-136">데이터베이스가 여러 개이면 각 데이터베이스의 결과가 사용 가능해지는 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-136">If there are multiple databases, the results for each database appears as soon as it is available.</span></span> <span data-ttu-id="f7b27-137">모든 데이터베이스 평가가 완료될 때까지 기다릴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-137">You don't need to wait for all database assessments to complete.</span></span>

1. <span data-ttu-id="f7b27-138">**AdventureWorks**의 평가가 완료되면 **호환성 문제** 및 **기능 권장 사항**을 클릭하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-138">Once the assessment for **AdventureWorks** is complete, click **Compatibility issues** and **Feature recommendations** to view the results.</span></span>

    - <span data-ttu-id="f7b27-139">SQL Server 기능 패리티 범주에는 완전히 지원되지 않을 수도 있는 기능과 이러한 문제를 해결하기 위한 단계가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-139">The SQL Server feature parity category lists features that might not be fully supported and steps to remedy these issues.</span></span> <span data-ttu-id="f7b27-140">기능 패리티 문제가 있어도 마이그레이션이 중지되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-140">Feature parity issues will not stop a migration.</span></span>
    - <span data-ttu-id="f7b27-141">호환성 문제 범주에는 마이그레이션을 차단하는 기능과 이러한 문제를 해결하기 위한 단계가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-141">The Compatibility issues category lists features that would block a migration and steps to remedy these issues.</span></span>

## <a name="summary"></a><span data-ttu-id="f7b27-142">요약</span><span class="sxs-lookup"><span data-stu-id="f7b27-142">Summary</span></span>

<span data-ttu-id="f7b27-143">이 단원에서는 로컬에 설치된 SQL Server 데이터베이스를 평가하여 Azure SQL Database로 해당 데이터베이스를 마이그레이션하면 사용할 수 없는 기능이 있는지를 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b27-143">In this unit, you assessed a locally installed SQL Server database to verify if any features would be unavailable when you migrate the database to Azure SQL Database.</span></span>