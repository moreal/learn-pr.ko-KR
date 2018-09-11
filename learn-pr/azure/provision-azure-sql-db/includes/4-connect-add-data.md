<span data-ttu-id="a67f0-101">데이터베이스를 앱에 연결하기 전에 연결할 수 있는지 확인하고, 기본 테이블을 추가하고, 샘플 데이터로 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-101">Before you connect the database to your app, you want to check that you can connect to it, add a basic table, and work with sample data.</span></span>

<span data-ttu-id="a67f0-102">Microsoft는 Azure SQL Database에 대한 인프라, 소프트웨어 업데이트 및 패치를 유지 관리하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-102">We maintain the infrastructure, software updates, and patches for your Azure SQL Database.</span></span> <span data-ttu-id="a67f0-103">또한 다른 SQL Server 설치와 마찬가지로 Azure SQL Database를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-103">Beyond that, you can treat your Azure SQL Database like you would any other SQL Server installation.</span></span> <span data-ttu-id="a67f0-104">예를 들어, Visual Studio, SQL Server Management Studio 또는 기타 도구를 사용하여 Azure SQL Database를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-104">For example, you can use Visual Studio, SQL Server Management Studio, or other tools to manage your Azure SQL Database.</span></span>

<span data-ttu-id="a67f0-105">데이터베이스에 액세스한 후 앱에 연결할 때는 사용자가 원하는 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-105">How you access your database and connect it to your app is up to you.</span></span> <span data-ttu-id="a67f0-106">그러나 여기서는 데이터베이스로 여러 작업을 수행해보기 위해 포털에서 직접 연결하고, 테이블을 만들고, 몇 가지 기본 CRUD 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-106">But to get some experience working with your database, here you'll connect to it directly from the portal, create a table, and run a few basic CRUD operations.</span></span> <span data-ttu-id="a67f0-107">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-107">You'll learn:</span></span>

* <span data-ttu-id="a67f0-108">Cloud Shell의 정의 및 포털에서 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="a67f0-108">What Cloud Shell is and how to access it from the portal.</span></span>
* <span data-ttu-id="a67f0-109">Azure CLI에서 연결 문자열을 비롯한 데이터베이스에 대한 정보에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="a67f0-109">How to access information about your database from the Azure CLI, including connection strings.</span></span>
* <span data-ttu-id="a67f0-110">`sqlcmd`를 사용하여 데이터베이스에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="a67f0-110">How to connect to your database using `sqlcmd`.</span></span>
* <span data-ttu-id="a67f0-111">기본 테이블 및 일부 샘플 데이터를 사용하여 데이터베이스를 초기화하는 방법</span><span class="sxs-lookup"><span data-stu-id="a67f0-111">How to initialize your database with a basic table and some sample data.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="a67f0-112">Azure Cloud Shell은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="a67f0-112">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="a67f0-113">Azure Cloud Shell은 Azure 리소스를 관리 및 개발하기 위한 브라우저 기반 셸 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-113">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span> <span data-ttu-id="a67f0-114">Cloud Shell을 클라우드에서 실행되는 대화형 콘솔로 생각하세요.</span><span class="sxs-lookup"><span data-stu-id="a67f0-114">Think of Cloud Shell as an interactive console that runs in the cloud.</span></span>

<span data-ttu-id="a67f0-115">내부적으로, Cloud Shell은 Linux에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-115">Behind the scenes, Cloud Shell runs on Linux.</span></span> <span data-ttu-id="a67f0-116">그러나 Linux 또는 Windows 중에서 어떤 환경을 선호하는지에 따라 Bash 및 PowerShell 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-116">But depending on whether you prefer a Linux or Windows environment, you have two experiences to choose from: Bash and PowerShell.</span></span>

<span data-ttu-id="a67f0-117">Cloud Shell은 어디에서나 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-117">The Cloud Shell is accessible from anywhere.</span></span> <span data-ttu-id="a67f0-118">포털 외에도 [shell.azure.com](https://shell.azure.com/), Azure 모바일 앱 또는 Visual Studio Code에서 Cloud Shell에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-118">Besides the portal, you can also access Cloud Shell from [shell.azure.com](https://shell.azure.com/), the Azure mobile app, or from Visual Studio Code.</span></span>

<span data-ttu-id="a67f0-119">Cloud Shell에는 인기 있는 도구 및 텍스트 편집기가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-119">Cloud Shell includes popular tools and text editors.</span></span> <span data-ttu-id="a67f0-120">현재 작업에 사용할 세 가지 도구인 `az`, `jq` 및 `sqlcmd`의 대략적인 모습은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-120">Here's a brief look at `az`, `jq`, and `sqlcmd`, three tools you'll use for our current task.</span></span>

* <span data-ttu-id="a67f0-121">`az`를 Azure CLI라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-121">`az` is also known as the Azure CLI.</span></span> <span data-ttu-id="a67f0-122">Azure 리소스로 작업하기 위한 명령줄 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-122">It's the command-line interface for working with Azure resources.</span></span> <span data-ttu-id="a67f0-123">이 도구를 사용하여 연결 문자열을 포함하여 데이터베이스에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-123">You'll use this to get information about your database, including the connection string.</span></span>
* <span data-ttu-id="a67f0-124">`jq`는 명령줄 JSON 파서입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-124">`jq` is a command-line JSON parser.</span></span> <span data-ttu-id="a67f0-125">`az` 명령의 출력을 이 도구로 파이프하여 JSON 출력에서 중요한 필드를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-125">You'll pipe output from `az` commands to this tool to extract important fields from JSON output.</span></span>
* <span data-ttu-id="a67f0-126">`sqlcmd`를 사용하여 SQL Server에서 문을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-126">`sqlcmd` enables you to execute statements on SQL Server.</span></span> <span data-ttu-id="a67f0-127">`sqlcmd`를 사용하여 Azure SQL Database와의 대화형 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-127">You'll use `sqlcmd` to create an interactive session with your Azure SQL Database.</span></span>

## <a name="get-information-about-your-azure-sql-database"></a><span data-ttu-id="a67f0-128">Azure SQL Database에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a67f0-128">Get information about your Azure SQL Database</span></span>

<span data-ttu-id="a67f0-129">데이터베이스에 연결하기 전에 해당 데이터베이스가 존재하는지와 온라인 상태인지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-129">Before you connect to your database, it's a good idea to verify it exists and is online.</span></span>

<span data-ttu-id="a67f0-130">여기서는 Cloud Shell을 불러온 후 `az` 유틸리티를 사용하여 데이터베이스를 나열하고, 최대 크기 및 상태를 비롯한 **Logistics** 데이터베이스 관련 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-130">Here, you bring up Cloud Shell and use the `az` utility to list your databases and show some information about the **Logistics** database, including its maximum size and status.</span></span>

1. <span data-ttu-id="a67f0-131">포털 맨 위에서 **Cloud Shell**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-131">From the portal, at the top, click **Cloud Shell**.</span></span> 
    <span data-ttu-id="a67f0-132">![Cloud Shell 열기](../media-draft/open-cloud-shell.png)</span><span class="sxs-lookup"><span data-stu-id="a67f0-132">![Opening Cloud Shell](../media-draft/open-cloud-shell.png)</span></span>
1. <span data-ttu-id="a67f0-133">실행할 `az` 명령에는 리소스 그룹의 이름과 Azure SQL 논리 서버의 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-133">The `az` commands you'll run require the name of your resource group and the name of your Azure SQL logical server.</span></span> <span data-ttu-id="a67f0-134">나중에 다시 입력하지 않으려면 이 `azure configure` 명령을 실행하여 기본값으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-134">To save typing, run this `azure configure` command to specify them as default values.</span></span>
    <span data-ttu-id="a67f0-135">`contoso-logistics`를 Azure SQL 논리 서버의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-135">Replace `contoso-logistics` with the name of your Azure SQL logical server.</span></span>
    ```azurecli
    az configure --defaults group=logistics-db-rg sql-server=contoso-logistics
    ```
1. <span data-ttu-id="a67f0-136">`az sql db list`를 실행하여 Azure SQL 논리 서버의 모든 데이터베이스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-136">Run `az sql db list` to list all databases on your Azure SQL logical server.</span></span>
    ```azurecli
    az sql db list
    ```
    <span data-ttu-id="a67f0-137">JSON의 대형 블록이 출력으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-137">You see a large block of JSON as output.</span></span> 
1. <span data-ttu-id="a67f0-138">데이터베이스 이름만 필요하면 이 명령을 한 번 더 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-138">Since we want just the database names, run the command a second time.</span></span> <span data-ttu-id="a67f0-139">이번에는 출력을 `jq`로 파이프하여 이름 필드만 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-139">This time, pipe the output to `jq` to print out only the name fields.</span></span>
    ```azurecli
    az sql db list | jq '[.[] | {name: .name}]'
    ```
    <span data-ttu-id="a67f0-140">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-140">You see this.</span></span>
    ```console
    [
      {
        "name": "Logistics"
      },
      {
        "name": "master"
      }
    ]
    ```
    <span data-ttu-id="a67f0-141">**Logistics**는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-141">**Logistics** is your database.</span></span> <span data-ttu-id="a67f0-142">SQL Server와 마찬가지로 **master**에는 로그온 계정 및 시스템 구성 설정과 같은 서버 메타데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-142">Like SQL Server, **master** includes server metadata such as logon accounts and system configuration settings.</span></span>
1. <span data-ttu-id="a67f0-143">이 `az sql db show` 명령을 실행하여 **Logistics** 데이터베이스에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-143">Run this `az sql db show` command to get details about the **Logistics** database.</span></span> 
    ```azurecli
    az sql db show --name Logistics
    ```
    <span data-ttu-id="a67f0-144">앞의 경우처럼 JSON의 대형 블록이 출력으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-144">As before, you see a large block of JSON as output.</span></span>
1. <span data-ttu-id="a67f0-145">이 명령을 한 번 더 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-145">Run the command a second time.</span></span> <span data-ttu-id="a67f0-146">이번에는 출력을 `jq`로 파이프하여 출력을 **Logistics** 데이터베이스의 이름, 최대 크기 및 상태로만 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-146">This time, pipe the output to `jq` to limit output to only the name, maximum size, and status of the **Logistics** database.</span></span>
    ```azurecli
    az sql db show --name Logistics | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
    ```
    <span data-ttu-id="a67f0-147">데이터베이스가 온라인 상태이며 약 2GB의 데이터를 보유할 수 있다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-147">You see that the database is online and can hold around 2 GB of data.</span></span>
    ```console
    {
      "name": "Logistics",
      "maxSizeBytes": 2147483648,
      "status": "Online"
    }
    ```

## <a name="connect-to-your-database"></a><span data-ttu-id="a67f0-148">데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="a67f0-148">Connect to your database</span></span>

<span data-ttu-id="a67f0-149">데이터베이스를 어느 정도 이해했으므로 `sqlcmd`를 사용하여 연결하고, 운송 기사에 대한 정보를 포함하는 테이블을 만들고, 몇 가지 기본 CRUD 작업을 수행해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-149">Now that you understand a bit about your database, let's connect to it using `sqlcmd`, create a table that holds information about transportation drivers, and perform a few basic CRUD operations.</span></span>

<span data-ttu-id="a67f0-150">CRUD는 **만들기**, **읽기**, **업데이트** 및 **삭제**를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-150">Remember that CRUD stands for **create**, **read**, **update**, and **delete**.</span></span> <span data-ttu-id="a67f0-151">이것은 테이블 데이터에 대해 수행하는 작업을 나타내며, 앱에 필요한 네 가지 기본 작업에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-151">These refer to operations you perform on table data, and are the four basic operations you need for your app.</span></span> <span data-ttu-id="a67f0-152">이제 각 작업을 수행할 수 있는지 확인해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-152">Now's a good time to verify you can perform each of them.</span></span>

1. <span data-ttu-id="a67f0-153">이 `az sql db show-connection-string` 명령을 실행하여 연결 문자열을 `sqlcmd`에서 사용할 수 있는 형식으로 **Logistics** 데이터베이스에 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-153">Run this `az sql db show-connection-string` command to get the connection string to the **Logistics** database in a format that `sqlcmd` can use.</span></span>
    ```azurecli
    az sql db show-connection-string --client sqlcmd --name Logistics
    ```
    <span data-ttu-id="a67f0-154">출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-154">Your output resembles this.</span></span>
    ```console
    "sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U <username> -P <password> -N -l 30"
    ```
1. <span data-ttu-id="a67f0-155">이전 단계의 `sqlcmd` 문을 실행하여 대화형 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-155">Run the `sqlcmd` statement from the previous step to create an interactive session.</span></span>
    <span data-ttu-id="a67f0-156">따옴표를 제거하고 `<username>` 및 `<password>`를 사용자가 데이터베이스를 만들 때 지정한 사용자 이름과 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-156">Remove the surrounding quotes and replace `<username>` and `<password>` with the username and password you specified when you created your database.</span></span> <span data-ttu-id="a67f0-157">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-157">Here's an example.</span></span>
    ```console
    sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U martina -P "password1234$" -N -l 30
    ```
    > [!TIP]
    > <span data-ttu-id="a67f0-158">“&” 및 기타 특수 문자가 처리 명령으로 해석되지 않도록 암호를 따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-158">Place your password in quotes so that "&" and other special characters aren't interpreted as processing instructions.</span></span>
1. <span data-ttu-id="a67f0-159">`sqlcmd` 세션에서 `Drivers`라는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-159">From your `sqlcmd` session, create a table named `Drivers`.</span></span>
    ```sql
    CREATE TABLE Drivers (DriverID int, LastName varchar(255), FirstName varchar(255), OriginCity varchar(255) );
    GO
    ```
    <span data-ttu-id="a67f0-160">이 테이블에는 4개의 열인 고유 ID, 기사의 이름과 성, 기사의 출생 도시가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-160">The table contains four columns: a unique identifier, the driver's last and first name, and the driver's city of origin.</span></span>
    > [!NOTE]
    > <span data-ttu-id="a67f0-161">여기에 표시되는 언어는 Transact-SQL 또는 T-SQL입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-161">The language you see here is Transact-SQL, or T-SQL.</span></span>
1. <span data-ttu-id="a67f0-162">`Drivers` 테이블이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-162">Verify that the `Drivers` table exists.</span></span>
    ```sql
    SELECT name FROM sys.tables;
    GO
    ```
    <span data-ttu-id="a67f0-163">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-163">You see this.</span></span>
    ```console
    name
    --------------------------------------------------------------------------------------------------------------------------------
    Drivers
    
    (1 rows affected)
    ```
1. <span data-ttu-id="a67f0-164">이 `INSERT` T-SQL 문을 실행하여 테이블에 샘플 행을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-164">Run this `INSERT` T-SQL statement to add a sample row to the table.</span></span> <span data-ttu-id="a67f0-165">이것은 **만들기** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-165">This is the **create** operation.</span></span>
    ```sql
    INSERT INTO Drivers (DriverID, LastName, FirstName, OriginCity) VALUES (123, 'Orton', 'Erick', 'Springfield');
    GO
    ```
    <span data-ttu-id="a67f0-166">작업이 성공했음을 나타내는 다음 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-166">You see this to indicate the operation succeeded.</span></span>
    ```console
    (1 rows affected)
    ```
1. <span data-ttu-id="a67f0-167">이 `SELECT` T-SQL 문을 실행하여 테이블의 모든 행에 있는 `DriverID` 열을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-167">Run this `SELECT` T-SQL statement list the `DriverID` column from all rows in the table.</span></span> <span data-ttu-id="a67f0-168">이것은 **읽기** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-168">This is the **read** operation.</span></span>
    ```sql
    SELECT DriverID FROM Drivers;
    GO
    ```
    <span data-ttu-id="a67f0-169">하나의 결과, 즉 이전 단계에서 만든 행에 대한 `DriverID`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-169">You see one result, the `DriverID` for the row you created in the previous step.</span></span>
    ```console
    DriverID
    -----------
            123
    
    (1 rows affected)
    ```
1. <span data-ttu-id="a67f0-170">이 `UPDATE` T-SQL 문을 실행하여 `DriverID`가 123인 기사의 출생 도시를 “Springfield”에서 “Springfield, OR”로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-170">Run this `UPDATE` T-SQL statement to change the city of origin from "Springfield" to "Springfield, OR" for the driver with a `DriverID` of 123.</span></span> <span data-ttu-id="a67f0-171">이것은 **업데이트** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-171">This is the **update** operation.</span></span>
    ```sql
    UPDATE Drivers SET OriginCity='Springfield, OR' WHERE DriverID=123;
    GO
    ```
    <span data-ttu-id="a67f0-172">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-172">You see this.</span></span>
    ```console
    (1 rows affected)
    ```
1. <span data-ttu-id="a67f0-173">이 `DELETE` T-SQL 문을 실행하여 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-173">Run this `DELETE` T-SQL statement to delete the record.</span></span> <span data-ttu-id="a67f0-174">이것은 **삭제** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-174">This is the **delete** operation.</span></span>
    ```sql
    DELETE FROM Drivers WHERE DriverID=123;
    GO
    ```
    
    ```console
    (1 rows affected)
    ```
1. <span data-ttu-id="a67f0-175">이 `SELECT` T-SQL 문을 실행하여 `Drivers` 테이블이 비어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-175">Run this `SELECT` T-SQL statement to verify the `Drivers` table is empty.</span></span>
    ```sql
    SELECT COUNT(*) FROM Drivers;
    GO
    ```
    <span data-ttu-id="a67f0-176">테이블에 행이 없는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-176">You see that the table contains no rows.</span></span>
    ```console
    -----------
              0
    
    (1 rows affected)
    ```

## <a name="summary"></a><span data-ttu-id="a67f0-177">요약</span><span class="sxs-lookup"><span data-stu-id="a67f0-177">Summary</span></span>

<span data-ttu-id="a67f0-178">Cloud Shell에서 Azure SQL Database에 대한 작업 방법을 살펴보았으므로 즐겨 사용하는 SQL 관리 도구(SQL Server Management Studio, Visual Studio 또는 기타)에 대한 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-178">Now that you have the hang of working with Azure SQL Database from Cloud Shell, you can get the connection string for your favorite SQL management tool &ndash; whether that's from SQL Server Management Studio, Visual Studio, or something else.</span></span>

<span data-ttu-id="a67f0-179">Cloud Shell을 사용하면 Azure 리소스에 쉽게 액세스하고 관련 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-179">Cloud Shell makes it easy to access and work with your Azure resources.</span></span> <span data-ttu-id="a67f0-180">Cloud Shell은 브라우저 기반이므로 Windows, macOS 또는 Linux를 비롯하여 웹 브라우저가 있는 모든 시스템에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-180">Because Cloud Shell is browser-based, you can access it from Windows, macOS, or Linux &ndash; essentially any system with a web browser.</span></span>

<span data-ttu-id="a67f0-181">Azure CLI 명령을 실행하여 SQL Azure Database에 대한 정보를 가져오는 방법에 대한 몇 가지 실습 경험을 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-181">You gained some hands-on experience running Azure CLI commands to get information about your SQL Azure Database.</span></span> <span data-ttu-id="a67f0-182">추가로 T-SQL 기술도 연습해보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-182">As a bonus, you practiced your T-SQL skills.</span></span>

<span data-ttu-id="a67f0-183">마지막으로, 데이터베이스를 중단하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a67f0-183">Finally, let's wrap up and see how to tear down your database.</span></span>