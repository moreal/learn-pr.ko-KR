<span data-ttu-id="89d7c-101">온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-101">Let's assume that you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="89d7c-102">표준 PostgreSQL 서버 수준 방화벽 규칙을 사용하여 모든 보안 측면을 관리하고 서버에 대한 모든 액세스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-102">You're managing all security aspects and you've locked down all access to your servers using the standard PostgreSQL server-level firewall rules.</span></span> <span data-ttu-id="89d7c-103">이제는 Azure에서 동일한 서버 수준 방화벽 규칙을 구성하는 방법에 대해 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-103">You now have a good understanding of how to configure the same server-level firewall rules in Azure.</span></span>

<span data-ttu-id="89d7c-104">만든 Azure Database for PostgreSQL 서버 중 하나에 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-104">Let's connect to one of the Azure Database for PostgreSQL servers that you created.</span></span>

## <a name="allow-azure-service-access"></a><span data-ttu-id="89d7c-105">Azure 서비스 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="89d7c-105">Allow Azure service access</span></span>

<span data-ttu-id="89d7c-106">시작하기 전에 PowerShell과 `psql`을 사용하여 서버에 연결하려면 Azure 서비스에 대한 액세스를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-106">Before we begin, you'll have to allow access to Azure services if you want to use PowerShell and `psql` to connect to your server.</span></span> <span data-ttu-id="89d7c-107">액세스는 두 가지 방법으로 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-107">Recall that you can allow access in two ways.</span></span>

<span data-ttu-id="89d7c-108">첫 번째 옵션은 **Azure 서비스 방문 허용**을 사용하도록 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-108">Your first option is to enable **Allow access to Azure services**.</span></span> <span data-ttu-id="89d7c-109">사용자가 만든 사용자 지정 규칙 목록에 규칙이 입력되지 않은 경우에도 액세스를 허용하면 방화벽 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-109">Allowing access will create a firewall rule even though the rule isn't entered in the list of custom rules you create.</span></span>

<span data-ttu-id="89d7c-110">두 번째 옵션은 모든 IP 주소에 대한 액세스를 허용하는 방화벽 규칙을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-110">Your second option is to create a firewall rule that allows access to all IP addresses.</span></span> <span data-ttu-id="89d7c-111">규칙에는 `psql`을 실행하는 데 사용하는 PowerShell이 실행되는 클라이언트에 대한 IP 주소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-111">The rule will include the IP address for the client running PowerShell that you'll use to execute `psql` from.</span></span>

<span data-ttu-id="89d7c-112">또한 **SSL 연결 적용** 옵션은 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-112">You also need to disable the **Enforce SSL connection** option.</span></span>

### <a name="create-a-firewall-rule"></a><span data-ttu-id="89d7c-113">방화벽 규칙을 만들기</span><span class="sxs-lookup"><span data-stu-id="89d7c-113">Create a firewall rule</span></span>

1. <span data-ttu-id="89d7c-114">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-114">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span> 

1. <span data-ttu-id="89d7c-115">방화벽 규칙을 만들려는 서버 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-115">Navigate to the server resource for which you would like to create a firewall rule.</span></span>

1. <span data-ttu-id="89d7c-116">**연결 보안** 옵션을 선택하여 오른쪽에 [연결 보안] 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-116">Select the **Connection Security** option to open the connection security blade to the right.</span></span>

    ![PostgreSQL 데이터베이스 리소스 블레이드의 연결 보안 섹션을 보여 주는 Azure Portal의 스크린샷](../media/7-db-security-settings.png)

<span data-ttu-id="89d7c-118">`psql`을 실행하는 PowerShell 클라이언트에 대한 액세스를 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-118">Recall that you want to allow access to PowerShell clients running `psql`.</span></span>

<span data-ttu-id="89d7c-119">다음 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-119">You can choose to either:</span></span>

- <span data-ttu-id="89d7c-120">**Azure 서비스 방문 허용**을 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-120">Set **Allow access to Azure services** to **ON**</span></span>
- <span data-ttu-id="89d7c-121">**SSL 연결 적용**을 **사용 안 함**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-121">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="89d7c-122">**저장** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-122">Click the **Save** button to save your changes</span></span>

<span data-ttu-id="89d7c-123">또는 모든 IP 주소에 대한 액세스를 허용하는 방화벽 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-123">Or, you can add a firewall rule to allow access to all IP addresses by adding a firewall rule.</span></span> <span data-ttu-id="89d7c-124">다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-124">Use the following values:</span></span>

- <span data-ttu-id="89d7c-125">규칙 이름: `AllowAll`</span><span class="sxs-lookup"><span data-stu-id="89d7c-125">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="89d7c-126">시작 IP: `0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="89d7c-126">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="89d7c-127">종료 IP: `255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="89d7c-127">End IP: `255.255.255.255`</span></span>
- <span data-ttu-id="89d7c-128">**SSL 연결 적용**을 **사용 안 함**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-128">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="89d7c-129">**저장** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-129">Click the **Save** button to save your changes</span></span>

> [!Warning]
> <span data-ttu-id="89d7c-130">이 방화벽 규칙을 만들면 인터넷의 모든 IP 주소에서 서버에 연결하려고 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-130">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="89d7c-131">프로덕션 환경에서는 특정 IP 주소에 대한 액세스만 허용하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-131">In production environments, you'll want to restrict access to specific IP addresses.</span></span>

### <a name="connect-to-the-database-with-psql"></a><span data-ttu-id="89d7c-132">PSQL로 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="89d7c-132">Connect to the database with psql</span></span>

1. <span data-ttu-id="89d7c-133">오른쪽의 Azure Cloud Shell에서 다음 명령을 사용하여 PSQL을 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-133">In the Azure Cloud Shell on the right, connect PSQL to your server using the following command.</span></span> <span data-ttu-id="89d7c-134">서버 이름 및 관리자 이름을 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-134">Make sure to replace the server name and admin name.</span></span>

    ```bash
    psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
    ```
    
    <span data-ttu-id="89d7c-135">`server-name` 및 `admin-user`에 대해 선택한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-135">Use the values you chose for the `server-name`, and `admin-user`.</span></span> 

1. <span data-ttu-id="89d7c-136">**postgres**는 각 PostgreSQL 서버를 만들 때마다 포함되는 기본 관리 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-136">**postgres** is the default management database every PostgreSQL server is created with.</span></span> <span data-ttu-id="89d7c-137">서버를 만들 때 제공한 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-137">You'll be prompted for the password you provided when you created the server.</span></span>

1. <span data-ttu-id="89d7c-138">성공적으로 연결되면 모든 데이터베이스를 나열하는 <kbd>\l</kbd> 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-138">Once successfully connected, execute the <kbd>\l</kbd> command to list all databases.</span></span> <span data-ttu-id="89d7c-139">이 명령을 실행하면 둘 이상의 기본 데이터베이스가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-139">This command will result in two or more default databases returned.</span></span>

1. <span data-ttu-id="89d7c-140"><kbd>q</kbd>를 눌러 목록을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-140">Hit <kbd>q</kbd> to exit the list.</span></span>

1. <span data-ttu-id="89d7c-141">다른 PSQL 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-141">You can try other PSQL commands.</span></span>
    - <kbd>\?</kbd> <span data-ttu-id="89d7c-142">도움말 가져오기.</span><span class="sxs-lookup"><span data-stu-id="89d7c-142">to get help.</span></span>
    - <span data-ttu-id="89d7c-143"><kbd>\dt</kbd> 테이블 나열.</span><span class="sxs-lookup"><span data-stu-id="89d7c-143"><kbd>\dt</kbd> to list the tables.</span></span>

1. <span data-ttu-id="89d7c-144">서버에서 PSQL 작업 실행이 완료되면 <kbd>\q</kbd> 명령을 실행하여 PSQL을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="89d7c-144">When you're finished executing PSQL operations on your server, execute the command <kbd>\q</kbd> to quit PSQL.</span></span>
