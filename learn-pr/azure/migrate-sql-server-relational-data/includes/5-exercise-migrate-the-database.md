<span data-ttu-id="6e9cf-101">데이터베이스를 평가하고 보고된 오류를 수정했으므로 이제 데이터베이스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-101">Now that you have assessed your database and fixed any errors reported, you're ready to migrate your database.</span></span> <span data-ttu-id="6e9cf-102">이 연습에서는 SQL 데이터베이스를 Azure SQL로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-102">In this exercise, you will migrate your SQL database to Azure SQL.</span></span>

## <a name="setup"></a><span data-ttu-id="6e9cf-103">설정</span><span class="sxs-lookup"><span data-stu-id="6e9cf-103">Setup</span></span>

<span data-ttu-id="6e9cf-104">샘플 데이터를 아직 다운로드하지 않았으면 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-104">If you haven't already, download the sample data.</span></span>

1. <span data-ttu-id="6e9cf-105">인터넷 브라우저를 시작하여 https://docs.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-2017로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-105">Start an internet browser and navigate to https://docs.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

2. <span data-ttu-id="6e9cf-106">**OLTP 다운로드**에서 **AdventureWorks2008R2.bak**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-106">In **OLTP downloads**, click **AdventureWorks2008R2.bak**.</span></span>

3. <span data-ttu-id="6e9cf-107">Management Studio에서 *AdventureWorks 2008R2*를 기본 인스턴스로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-107">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="6e9cf-108">Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="6e9cf-108">Create an Azure SQL Database</span></span>

1. <span data-ttu-id="6e9cf-109">Azure Portal 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-109">Sign in to your Azure portal account.</span></span>

2. <span data-ttu-id="6e9cf-110">포털의 왼쪽 위 모서리에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-110">Click **Create a resource** in the upper left-hand corner of the portal.</span></span>

3. <span data-ttu-id="6e9cf-111">**데이터베이스** > **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-111">Click **Databases** > **SQL Database**.</span></span>

4. <span data-ttu-id="6e9cf-112">SQL Database 양식의 다음 필드에 내용을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-112">Enter the following fields on the SQL Database form:</span></span>

    |<span data-ttu-id="6e9cf-113">필드</span><span class="sxs-lookup"><span data-stu-id="6e9cf-113">Field</span></span>|<span data-ttu-id="6e9cf-114">설명</span><span class="sxs-lookup"><span data-stu-id="6e9cf-114">Description</span></span>|
    |-----|---|
    |<span data-ttu-id="6e9cf-115">데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="6e9cf-115">Database name</span></span>|<span data-ttu-id="6e9cf-116">데이터베이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-116">Enter a name for your database.</span></span> <span data-ttu-id="6e9cf-117">마이그레이션하려는 기존 데이터베이스의 이름이나 원하는 새 이름을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-117">This can be the name of your existing database that you're migrating, or any new name of your choice</span></span>|
    |<span data-ttu-id="6e9cf-118">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="6e9cf-118">Resource group</span></span>|<span data-ttu-id="6e9cf-119">리소스 그룹을 선택하거나 새 리소스 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-119">Select a resource group or enter a new resource group name</span></span>|
    |<span data-ttu-id="6e9cf-120">원본 선택</span><span class="sxs-lookup"><span data-stu-id="6e9cf-120">Select source</span></span>|<span data-ttu-id="6e9cf-121">*새 데이터베이스*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-121">Select *Blank database*</span></span>|

5. <span data-ttu-id="6e9cf-122">**서버**에서 기존 서버를 선택하거나 전역적으로 고유한 **서버 이름**, **서버 관리자 로그인**, **암호**(확인 필요) 및 **위치**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-122">Under **Server**, either select an existing server or, enter a globally unique **Server name**, a **Server admin login**, a **Password** (which you should confirm), and a **Location**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e9cf-123">서버 이름, 로그인 이름 및 암호를 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-123">You will use the server name, login name, and password to connect to your database.</span></span>

6. <span data-ttu-id="6e9cf-124">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-124">Click **Select**.</span></span>

7. <span data-ttu-id="6e9cf-125">**가격 책정 계층**에서는 성능이 더 우수한 데이터베이스를 선택할 수 있습니다. 하지만 이 자습서에서는 기본값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-125">In **Pricing tier** you can select a database with higher performance, but for this tutorial, select default.</span></span>

8. <span data-ttu-id="6e9cf-126">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-126">Click **Create**.</span></span> <span data-ttu-id="6e9cf-127">데이터베이스가 프로비저닝될 때까지 기다렸다가 자습서를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-127">Wait until the database has been provisioned before continuing the tutorial.</span></span>

    <span data-ttu-id="6e9cf-128">다음 스크린샷에는 새 SQL 데이터베이스에 사용할 수 있는 구성이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-128">The following screenshot shows a potential configuration for you new SQL database.</span></span>

    ![샘플 구성이 적용된 Azure Portal의 새 SQL 데이터베이스 블레이드 스크린샷.](../media-draft/5-create-azure-sql-db.png)

## <a name="create-a-new-migration-project"></a><span data-ttu-id="6e9cf-130">새 마이그레이션 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6e9cf-130">Create a new migration project</span></span>

1. <span data-ttu-id="6e9cf-131">**Data Migration Assistant**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-131">Start **Data Migration Assistant**.</span></span>

2. <span data-ttu-id="6e9cf-132">**새로 만들기** 아이콘을 클릭하고 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-132">Click the **New** icon, and specify the following options:</span></span>
    - <span data-ttu-id="6e9cf-133">**프로젝트 형식** - *마이그레이션* 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-133">**Project type** - Select  the *Migration* option.</span></span>
    - <span data-ttu-id="6e9cf-134">**프로젝트 이름** - 프로젝트에 대해 기억하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-134">**Project name** - Enter a memorable name for your project.</span></span>
    - <span data-ttu-id="6e9cf-135">**원본 서버 유형** - *SQL Server*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-135">**Source server type** - Select *SQL Server*.</span></span>
    - <span data-ttu-id="6e9cf-136">**대상 서버 유형** - *Azure SQL Database*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-136">**Target server type** - Select *Azure SQL Database*.</span></span>
    - <span data-ttu-id="6e9cf-137">**마이그레이션 범위** - *스키마 및 데이터*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-137">**Migration scope** - Select *Schema and data*.</span></span>

3. <span data-ttu-id="6e9cf-138">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-138">Click **Create**.</span></span>

## <a name="specify-the-source-server-and-database"></a><span data-ttu-id="6e9cf-139">원본 서버 및 데이터베이스 지정</span><span class="sxs-lookup"><span data-stu-id="6e9cf-139">Specify the source server and database</span></span>

1. <span data-ttu-id="6e9cf-140">**원본 서버에 연결**의 **서버 이름** 필드에 원본 SQL Server 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-140">Under **Connect to source server**, in the **Server name** field, enter the name of the source SQL Server instance.</span></span>

2. <span data-ttu-id="6e9cf-141">원본 SQL Server 인스턴스에서 지원하는 **인증 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-141">Select the **Authentication type** supported by the source SQL Server instance.</span></span>
    > [!TIP]
    > <span data-ttu-id="6e9cf-142">연결 속성 아래의 **연결 암호화** 확인란을 선택하여 연결을 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-142">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

3. <span data-ttu-id="6e9cf-143">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-143">Select **Connect**.</span></span>

4. <span data-ttu-id="6e9cf-144">Azure SQL Database로 마이그레이션할 단일 원본 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-144">Select a single source database to migrate to Azure SQL Database and click **Next**.</span></span>

## <a name="specify-the-target-server-and-database"></a><span data-ttu-id="6e9cf-145">대상 서버 및 데이터베이스 지정</span><span class="sxs-lookup"><span data-stu-id="6e9cf-145">Specify the target server and database</span></span>

1. <span data-ttu-id="6e9cf-146">**대상 서버에 연결**의 **서버 이름** 필드에 Azure SQL Database 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-146">Under **Connect to target server**, in the **Server name** field, enter the name of the Azure SQL Database instance.</span></span> <span data-ttu-id="6e9cf-147">데이터베이스 인스턴스에 **database.windows.net**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-147">Add **database.windows.net** to the database instance.</span></span>

2. <span data-ttu-id="6e9cf-148">대상 Azure SQL Database 인스턴스에서 지원하는 인증 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-148">Select the Authentication type supported by the target Azure SQL Database instance.</span></span> <span data-ttu-id="6e9cf-149">이 자습서에서는 **SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-149">For this tutorial, select **SQL Server Authentication**.</span></span>
    > [!TIP]
    > <span data-ttu-id="6e9cf-150">연결 속성 아래의 **연결 암호화** 확인란을 선택하여 연결을 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-150">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

3. <span data-ttu-id="6e9cf-151">Azure SQL Database를 만들 때 정의한 **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-151">Enter the **Username** and **Password** that you defined when you created the Azure SQL Database.</span></span>

4. <span data-ttu-id="6e9cf-152">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-152">Click **Connect**.</span></span>

5. <span data-ttu-id="6e9cf-153">원본 데이터베이스를 마이그레이션할 단일 대상 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-153">Select a single target database to which to migrate.</span></span>
    > <span data-ttu-id="6e9cf-154">[참고] Windows 사용자를 마이그레이션하려는 경우 대상 외부 사용자 도메인 이름 텍스트 상자에 대상 외부 사용자 도메인 이름이 올바르게 지정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-154">[NOTE] If you intend to migrate Windows users, in the Target external user domain name text box, make sure that the target external user domain name is specified correctly.</span></span>

6. <span data-ttu-id="6e9cf-155">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-155">Click **Next**.</span></span>

## <a name="select-schema-objects"></a><span data-ttu-id="6e9cf-156">스키마 개체 선택</span><span class="sxs-lookup"><span data-stu-id="6e9cf-156">Select schema objects</span></span>

1. <span data-ttu-id="6e9cf-157">Azure SQL Database로 마이그레이션할 원본 데이터베이스에서 스키마 개체를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-157">Select the schema objects from the source database that you want to migrate to Azure SQL Database.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e9cf-158">그대로 변환할 수 없는 일부 개체의 경우 자동 수정 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-158">Some of the objects that cannot be converted as-is are presented with automatic fix opportunities.</span></span> <span data-ttu-id="6e9cf-159">왼쪽 창에서 이러한 개체를 클릭하면 오른쪽 창에 수정 제안 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-159">Clicking these objects on the left pane displays the suggested fixes on the right pane.</span></span> <span data-ttu-id="6e9cf-160">해당 수정 내용을 검토하고 개체별로 모든 변경 내용을 적용하거나 무시하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-160">Review the fixes and choose to either apply or ignore all changes, object by object.</span></span> <span data-ttu-id="6e9cf-161">개체 하나에 대해 모든 변경을 적용하거나 무시해도 다른 데이터베이스 개체의 변경 내용에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-161">Note that applying or ignoring all changes for one object does not affect changes to other database objects.</span></span> <span data-ttu-id="6e9cf-162">변환하거나 자동으로 수정할 수 없는 문은 대상 데이터베이스로 재현되어 주석 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-162">Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.</span></span>

    ![AdventureWorks SQL Server 데이터에 영향을 주는 마이그레이션 문제 목록을 보여 주는 Data Migration Assistant 스크린샷("저장 프로시저: dbo.uspSearchCandidateResumes" 문제가 선택되고 문제 세부 정보가 표시됨).](../media-draft/5-suggested-fix.png)

2. <span data-ttu-id="6e9cf-164">**SQL 스크립트 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-164">Click **Generate SQL script**.</span></span>

## <a name="deploy-schema"></a><span data-ttu-id="6e9cf-165">스키마 배포</span><span class="sxs-lookup"><span data-stu-id="6e9cf-165">Deploy schema</span></span>

1. <span data-ttu-id="6e9cf-166">**스키마 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-166">Click **Deploy schema**.</span></span>

2. <span data-ttu-id="6e9cf-167">스키마 배포 결과를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-167">Review the results of the schema deployment.</span></span>

## <a name="migrate-data"></a><span data-ttu-id="6e9cf-168">데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="6e9cf-168">Migrate data</span></span>

1. <span data-ttu-id="6e9cf-169">**데이터 마이그레이션**을 클릭하여 데이터 마이그레이션 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-169">Click **Migrate data** to start the data migration process.</span></span>

2. <span data-ttu-id="6e9cf-170">마이그레이션할 데이터가 포함된 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-170">Select the tables with the data you want to migrate.</span></span>

3. <span data-ttu-id="6e9cf-171">**데이터 마이그레이션 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-171">Click **Start data migration**.</span></span>

<span data-ttu-id="6e9cf-172">마지막 화면에 전체 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-172">The final screen shows the overall status.</span></span>

## <a name="summary"></a><span data-ttu-id="6e9cf-173">요약</span><span class="sxs-lookup"><span data-stu-id="6e9cf-173">Summary</span></span>

<span data-ttu-id="6e9cf-174">이 연습에서는 빈 Azure SQL Database를 만들고 로컬 SQL Server 데이터베이스를 이 새 데이터베이스로 마이그레이션했습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9cf-174">In this exercise, you created an empty Azure SQL Database and migrated a local SQL Server database to this new database.</span></span>