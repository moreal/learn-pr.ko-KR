<span data-ttu-id="47d0c-101">데이터베이스를 평가하고 보고된 오류를 수정했으므로 이제 데이터베이스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-101">Now that you have assessed your database and fixed any errors reported, you're ready to migrate your database.</span></span> <span data-ttu-id="47d0c-102">이 단원에서는 SQL 데이터베이스를 Azure SQL Database로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-102">In this unit, you will migrate your SQL database to Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="47d0c-103">설정</span><span class="sxs-lookup"><span data-stu-id="47d0c-103">Setup</span></span>

<span data-ttu-id="47d0c-104">첫 번째 단계는 샘플 데이터를 다운로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-104">The first step is to download the sample data.</span></span> <span data-ttu-id="47d0c-105">데이터가 이미 로컬에 설치된 경우 이 설정을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-105">You can skip this setup if you already have the data installed locally.</span></span>

1. <span data-ttu-id="47d0c-106">인터넷 브라우저를 시작하여 https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-106">Start an internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="47d0c-107">**OLTP 다운로드**에서 **AdventureWorks2008R2.bak**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-107">In **OLTP downloads**, click **AdventureWorks2008R2.bak**.</span></span>

1. <span data-ttu-id="47d0c-108">Management Studio에서 **AdventureWorks 2008R2**를 기본 인스턴스로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-108">In Management Studio, restore **AdventureWorks 2008R2** to your default instance.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="47d0c-109">Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="47d0c-109">Create an Azure SQL Database</span></span>

1. <span data-ttu-id="47d0c-110">Azure Portal 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-110">Sign in to your Azure portal account.</span></span>

1. <span data-ttu-id="47d0c-111">포털의 왼쪽 위 모서리에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-111">Click **Create a resource** in the upper left-hand corner of the portal.</span></span>

1. <span data-ttu-id="47d0c-112">**데이터베이스** > **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-112">Click **Databases** > **SQL Database**.</span></span>

1. <span data-ttu-id="47d0c-113">SQL Database 양식의 다음 필드에 내용을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-113">Enter the following fields on the SQL Database form:</span></span>

    |<span data-ttu-id="47d0c-114">필드</span><span class="sxs-lookup"><span data-stu-id="47d0c-114">Field</span></span>|<span data-ttu-id="47d0c-115">설명</span><span class="sxs-lookup"><span data-stu-id="47d0c-115">Description</span></span>|
    |-----|---|
    |<span data-ttu-id="47d0c-116">데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="47d0c-116">Database name</span></span>|<span data-ttu-id="47d0c-117">데이터베이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-117">Enter a name for your database.</span></span> <span data-ttu-id="47d0c-118">마이그레이션하려는 기존 데이터베이스의 이름이나 원하는 새 이름을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-118">This can be the name of your existing database that you're migrating or any new name of your choice</span></span>|
    |<span data-ttu-id="47d0c-119">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="47d0c-119">Resource group</span></span>|<span data-ttu-id="47d0c-120">리소스 그룹을 선택하거나 새 리소스 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-120">Select a resource group or enter a new resource group name</span></span>|
    |<span data-ttu-id="47d0c-121">원본 선택</span><span class="sxs-lookup"><span data-stu-id="47d0c-121">Select source</span></span>|<span data-ttu-id="47d0c-122">*새 데이터베이스*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-122">Select *Blank database*</span></span>|

1. <span data-ttu-id="47d0c-123">**서버**에서 기존 서버를 선택하거나 전역적으로 고유한 **서버 이름**, **서버 관리자 로그인**, **암호**(확인 필요) 및 **위치**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-123">Under **Server**, either select an existing server or, enter a globally unique **Server name**, a **Server admin login**, a **Password** (which you should confirm), and a **Location**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="47d0c-124">서버 이름, 로그인 이름 및 암호를 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-124">You will use the server name, login name, and password to connect to your database.</span></span>

1. <span data-ttu-id="47d0c-125">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-125">Click **Select**.</span></span>

1. <span data-ttu-id="47d0c-126">**가격 책정 계층**에서는 성능이 더 우수한 데이터베이스를 선택할 수 있습니다. 하지만 이 자습서에서는 기본값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-126">In **Pricing tier**, you can select a database with higher performance, but for this tutorial, select default.</span></span>

1. <span data-ttu-id="47d0c-127">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-127">Click **Create**.</span></span> <span data-ttu-id="47d0c-128">데이터베이스가 프로비저닝될 때까지 기다렸다가 자습서를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-128">Wait until the database has been provisioned before continuing the tutorial.</span></span>

    <span data-ttu-id="47d0c-129">다음 스크린샷은 새 SQL 데이터베이스에 대해 가능한 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-129">The following screenshot shows a possible configuration for your new SQL database.</span></span>

    ![샘플 구성이 적용된 Azure Portal의 새 SQL 데이터베이스 블레이드 스크린샷.](../media-draft/5-create-azure-sql-db.png)

## <a name="create-a-new-migration-project"></a><span data-ttu-id="47d0c-131">새 마이그레이션 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="47d0c-131">Create a new migration project</span></span>

1. <span data-ttu-id="47d0c-132">**Data Migration Assistant**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-132">Start **Data Migration Assistant**.</span></span>

1. <span data-ttu-id="47d0c-133">**새로 만들기** 아이콘을 클릭하고 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-133">Click the **New** icon, and specify the following options:</span></span>

    - <span data-ttu-id="47d0c-134">**프로젝트 형식** - *마이그레이션* 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-134">**Project type** - Select  the *Migration* option.</span></span>
    - <span data-ttu-id="47d0c-135">**프로젝트 이름** - 프로젝트에 대해 기억하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-135">**Project name** - Enter a memorable name for your project.</span></span>
    - <span data-ttu-id="47d0c-136">**원본 서버 유형** - *SQL Server*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-136">**Source server type** - Select *SQL Server*.</span></span>
    - <span data-ttu-id="47d0c-137">**대상 서버 유형** - *Azure SQL Database*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-137">**Target server type** - Select *Azure SQL Database*.</span></span>
    - <span data-ttu-id="47d0c-138">**마이그레이션 범위** - *스키마 및 데이터*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-138">**Migration scope** - Select *Schema and data*.</span></span>

1. <span data-ttu-id="47d0c-139">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-139">Click **Create**.</span></span>

## <a name="specify-the-source-server-and-database"></a><span data-ttu-id="47d0c-140">원본 서버 및 데이터베이스 지정</span><span class="sxs-lookup"><span data-stu-id="47d0c-140">Specify the source server and database</span></span>

1. <span data-ttu-id="47d0c-141">**원본 서버에 연결**의 **서버 이름** 필드에 원본 SQL Server 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-141">Under **Connect to source server**, in the **Server name** field, enter the name of the source SQL Server instance.</span></span>

1. <span data-ttu-id="47d0c-142">원본 SQL Server 인스턴스에서 지원하는 **인증 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-142">Select the **Authentication type** supported by the source SQL Server instance.</span></span>
    > [!TIP]
    > <span data-ttu-id="47d0c-143">연결 속성 아래의 **연결 암호화** 확인란을 선택하여 연결을 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-143">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

1. <span data-ttu-id="47d0c-144">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-144">Select **Connect**.</span></span>

> [!NOTE]
> <span data-ttu-id="47d0c-145">IP 주소에서 사용 권한이 없기 때문에 서버 인증이 실패한 경우 **Azure Management Studio**에서 SQL Server 인스턴스를 열고 **방화벽 및 Virtual Network**로 이동하여 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-145">If authentication to the server fails because you do not have permission from your IP address, open the SQL Server instance in **Azure Management Studio**, go to **Firewalls and Virtual Networks** and add a rule.</span></span> <span data-ttu-id="47d0c-146">원하는 이름을 지정합니다(예: **Azure 허용**).</span><span class="sxs-lookup"><span data-stu-id="47d0c-146">Name it whatever you wish, for example, **Allow Azure**.</span></span> <span data-ttu-id="47d0c-147">이 인스턴스에 액세스할 수 있는 IP 주소의 범위를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-147">Set up a range of IP addresses that are allowed to access this instance.</span></span> <span data-ttu-id="47d0c-148">범위는 0.0.0.0 ~ 255.255.255.255가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-148">The range can be 0.0.0.0 to 255.255.255.255.</span></span> <span data-ttu-id="47d0c-149">이 새 규칙을 저장하면 Azure SQL Server 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-149">Save this new rule, and you should be able to access the Azure SQL Server instance.</span></span> 

1. <span data-ttu-id="47d0c-150">Azure SQL Database로 마이그레이션할 단일 원본 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-150">Select a single source database to migrate to Azure SQL Database and click **Next**.</span></span>

## <a name="specify-the-target-server-and-database"></a><span data-ttu-id="47d0c-151">대상 서버 및 데이터베이스 지정</span><span class="sxs-lookup"><span data-stu-id="47d0c-151">Specify the target server and database</span></span>

1. <span data-ttu-id="47d0c-152">**대상 서버에 연결**의 **서버 이름** 필드에 Azure SQL Database 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-152">Under **Connect to target server**, in the **Server name** field, enter the name of the Azure SQL Database instance.</span></span> <span data-ttu-id="47d0c-153">데이터베이스 인스턴스에 **database.windows.net**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-153">Add **.database.windows.net** to the database instance.</span></span>

1. <span data-ttu-id="47d0c-154">대상 Azure SQL Database 인스턴스에서 지원하는 인증 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-154">Select the Authentication type supported by the target Azure SQL Database instance.</span></span> <span data-ttu-id="47d0c-155">이 자습서에서는 **SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-155">For this tutorial, select **SQL Server Authentication**.</span></span>
    > [!TIP]
    > <span data-ttu-id="47d0c-156">연결 속성 아래의 **연결 암호화** 확인란을 선택하여 연결을 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-156">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

1. <span data-ttu-id="47d0c-157">Azure SQL Database를 만들 때 정의한 **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-157">Enter the **Username** and **Password** that you defined when you created the Azure SQL Database.</span></span>

1. <span data-ttu-id="47d0c-158">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-158">Click **Connect**.</span></span>

1. <span data-ttu-id="47d0c-159">원본 데이터베이스를 마이그레이션할 단일 대상 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-159">Select a single target database to which to migrate.</span></span>
    > <span data-ttu-id="47d0c-160">[참고] Windows 사용자를 마이그레이션하려는 경우 **대상 외부 사용자 도메인 이름** 필드에 대상 외부 사용자 도메인 이름이 올바르게 지정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-160">[NOTE] If you intend to migrate Windows users, in the **Target external user domain name** field, make sure that the target external user domain name is specified correctly.</span></span>

1. <span data-ttu-id="47d0c-161">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-161">Click **Next**.</span></span>

## <a name="select-schema-objects"></a><span data-ttu-id="47d0c-162">스키마 개체 선택</span><span class="sxs-lookup"><span data-stu-id="47d0c-162">Select schema objects</span></span>

1. <span data-ttu-id="47d0c-163">Azure SQL Database로 마이그레이션할 원본 데이터베이스에서 스키마 개체를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-163">Select the schema objects from the source database that you want to migrate to Azure SQL Database.</span></span>

    > [!NOTE]
    > <span data-ttu-id="47d0c-164">그대로 변환할 수 없는 일부 개체의 경우 자동 수정 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-164">Some of the objects that cannot be converted as-is are presented with automatic fix opportunities.</span></span> <span data-ttu-id="47d0c-165">왼쪽 창에서 이러한 개체를 클릭하면 오른쪽 창에 수정 제안 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-165">Clicking these objects on the left pane displays the suggested fixes on the right pane.</span></span> <span data-ttu-id="47d0c-166">해당 수정 내용을 검토하고 개체별로 모든 변경 내용을 적용하거나 무시하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-166">Review the fixes and choose to either apply or ignore all changes, object by object.</span></span> <span data-ttu-id="47d0c-167">개체 하나에 대해 모든 변경을 적용하거나 무시해도 다른 데이터베이스 개체의 변경 내용에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-167">Note that applying or ignoring all changes for one object does not affect changes to other database objects.</span></span> <span data-ttu-id="47d0c-168">변환하거나 자동으로 수정할 수 없는 문은 대상 데이터베이스로 재현되어 주석 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-168">Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.</span></span>

    ![AdventureWorks SQL Server 데이터에 영향을 주는 마이그레이션 문제 목록을 보여 주는 Data Migration Assistant 스크린샷("저장 프로시저: dbo.uspSearchCandidateResumes" 문제가 선택되고 문제 세부 정보가 표시됨).](../media-draft/5-suggested-fix.png)

1. <span data-ttu-id="47d0c-170">**SQL 스크립트 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-170">Click **Generate SQL script**.</span></span>

## <a name="deploy-schema"></a><span data-ttu-id="47d0c-171">스키마 배포</span><span class="sxs-lookup"><span data-stu-id="47d0c-171">Deploy schema</span></span>

1. <span data-ttu-id="47d0c-172">**스키마 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-172">Click **Deploy schema**.</span></span>

1. <span data-ttu-id="47d0c-173">스키마 배포 결과를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-173">Review the results of the schema deployment.</span></span>

## <a name="migrate-data"></a><span data-ttu-id="47d0c-174">데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="47d0c-174">Migrate data</span></span>

1. <span data-ttu-id="47d0c-175">**데이터 마이그레이션**을 클릭하여 데이터 마이그레이션 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-175">Click **Migrate data** to start the data migration process.</span></span>

1. <span data-ttu-id="47d0c-176">마이그레이션할 데이터가 포함된 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-176">Select the tables with the data you want to migrate.</span></span>

1. <span data-ttu-id="47d0c-177">**데이터 마이그레이션 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-177">Click **Start data migration**.</span></span>

<span data-ttu-id="47d0c-178">마지막 화면에 전체 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-178">The final screen shows the overall status.</span></span>

## <a name="summary"></a><span data-ttu-id="47d0c-179">요약</span><span class="sxs-lookup"><span data-stu-id="47d0c-179">Summary</span></span>

<span data-ttu-id="47d0c-180">이 단원에서는 빈 Azure SQL Database를 만들고 로컬 SQL Server 데이터베이스를 이 새 데이터베이스로 마이그레이션했습니다.</span><span class="sxs-lookup"><span data-stu-id="47d0c-180">In this unit, you created an empty Azure SQL Database and migrated a local SQL Server database to this new database.</span></span>