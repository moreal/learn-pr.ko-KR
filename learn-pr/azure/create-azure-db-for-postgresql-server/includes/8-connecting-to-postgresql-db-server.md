<span data-ttu-id="177ae-101">온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-101">Lets' assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="177ae-102">표준 PostgreSQL 서버 수준 방화벽 규칙을 사용하여 모든 보안 측면을 관리하고 서버에 대한 모든 액세스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-102">You're managing all security aspects and locked down all access to your servers using the standard PostgreSQL server level firewall rules.</span></span> <span data-ttu-id="177ae-103">이제는 Azure에서 동일한 서버 수준 방화벽 규칙을 구성하는 방법에 대해 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-103">You now have a good understanding of how to configure the same server level firewall rules in Azure.</span></span>

<span data-ttu-id="177ae-104">`psql`을 사용하여 만든 이전의 Azure Databases for PostgreSQL 서버 중 하나에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-104">You now have the chance to connect to one of the previous Azure Databases for PostgreSQL servers you created using `psql`.</span></span>

## <a name="allow-azure-service-access"></a><span data-ttu-id="177ae-105">Azure 서비스 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="177ae-105">Allow Azure service access</span></span>

<span data-ttu-id="177ae-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="177ae-106">Before we begin.</span></span> <span data-ttu-id="177ae-107">PowerShell과 `psql`을 사용하여 서버에 연결하려면 Azure 서비스에 대한 액세스를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-107">You'll have to allow access to Azure services if you want to use PowerShell and `psql` to connect to your server.</span></span> <span data-ttu-id="177ae-108">액세스는 두 가지 방법으로 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-108">Recall, that you can allow access in two ways.</span></span>

<span data-ttu-id="177ae-109">첫 번째 옵션은 **Azure 서비스 방문 허용**을 사용하도록 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-109">Your first option is to enable **Allow access to Azure services**.</span></span> <span data-ttu-id="177ae-110">사용자가 만든 사용자 지정 규칙 목록에 규칙이 입력되지 않은 경우에도 액세스를 허용하면 방화벽 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-110">Allowing access will create a firewall rule even though the rule isn't entered in the list of custom rules you create.</span></span>

<span data-ttu-id="177ae-111">두 번째 옵션은 모든 IP 주소에 대한 액세스를 허용하는 방화벽 규칙을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-111">Your second option is to create a firewall rule that allows access to all IP addresses.</span></span> <span data-ttu-id="177ae-112">규칙에는 `psql`을 실행하는 데 사용하는 PowerShell이 실행되는 클라이언트에 대한 IP 주소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-112">The rule will include the IP address for the client running PowerShell that you'll use to execute `psql` from.</span></span>

<span data-ttu-id="177ae-113">또한 **SSL 연결 적용**은 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-113">You also need to disable the **Enforce SSL connection**.</span></span>

<span data-ttu-id="177ae-114">시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-114">Let's begin.</span></span>

<span data-ttu-id="177ae-115">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-115">Sign in to [the Azure portal](https://portal.azure.com?azure-portal=true).</span></span> <span data-ttu-id="177ae-116">방화벽 규칙을 만들려는 서버 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-116">Navigate to the server resource for which you would like to create a firewall rule.</span></span>

<span data-ttu-id="177ae-117">**연결 보안** 옵션을 선택하여 오른쪽에 [연결 보안] 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-117">Select the **Connection Security** option to open the connection security blade to the right.</span></span>

![PostgreSQL 데이터베이스 보안 설정](../media-draft/7-db-security-settings.png)

<span data-ttu-id="177ae-119">`psql`을 실행하는 PowerShell 클라이언트에 대한 액세스를 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-119">Recall, you want to allow access to PowerShell clients running `psql`.</span></span>

<span data-ttu-id="177ae-120">다음 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-120">You can choose to either:</span></span>

- <span data-ttu-id="177ae-121">**Azure 서비스 방문 허용**을 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-121">Set **Allow access to Azure services** to **ON**</span></span>
- <span data-ttu-id="177ae-122">**SSL 연결 적용**을 **사용 안 함**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-122">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="177ae-123">**저장** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-123">Click the **Save** button to save your changes</span></span>

<span data-ttu-id="177ae-124">또는 모든 IP 주소에 대한 액세스를 허용하는 방화벽 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-124">Or, you can add a firewall rule to allow access to all IP addresses by adding a firewall rule.</span></span> <span data-ttu-id="177ae-125">다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-125">Use the following values:</span></span>

- <span data-ttu-id="177ae-126">규칙 이름: `AllowAll`</span><span class="sxs-lookup"><span data-stu-id="177ae-126">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="177ae-127">시작 IP: `0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="177ae-127">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="177ae-128">종료 IP: `255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="177ae-128">End IP: `255.255.255.255`</span></span>
- <span data-ttu-id="177ae-129">**SSL 연결 적용**을 **사용 안 함**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-129">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="177ae-130">**저장** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-130">Click the **Save** button to save your changes</span></span>

> [!Warning]
> <span data-ttu-id="177ae-131">이 방화벽 규칙을 만들면 인터넷의 모든 IP 주소에서 서버에 연결하려고 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-131">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="177ae-132">클라이언트에서 사용자 이름과 암호를 사용하여 서버에 액세스 할 수 있는 경우에도 이 규칙을 신중하게 사용하도록 설정하고 보안에 미치는 영향을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-132">Even though clients will not be able access the server without the username and password, enable this rule with caution and make sure you understand the security implications.</span></span> <span data-ttu-id="177ae-133">프로덕션 환경에서는 특정 클라이언트 IP 주소에 대한 액세스만 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-133">In production environments, you'll only allow access to specific client IP addresses.</span></span>

<span data-ttu-id="177ae-134">다음 단계에서는 Azure Cloud Shell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-134">For the next steps, you'll start an Azure Cloud Shell session.</span></span> <span data-ttu-id="177ae-135">이 랩에서는 `bash`를 명령줄 환경으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-135">This lab uses `bash` as the command-line environment.</span></span>

- <span data-ttu-id="177ae-136">Azure Portal에서 Cloud Shell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-136">Open the Cloud Shell from the Azure portal.</span></span> <span data-ttu-id="177ae-137">[Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하고 [Cloud Shell 열기] 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-137">Go to [Azure portal](https://portal.azure.com?azure-portal=true) and click the Open Cloud Shell button:</span></span>

  ![Cloud Shell 단추](../media-draft/cloud-shell-button.png)

- <span data-ttu-id="177ae-139">구독이 여러 개 있는 경우 요청 시 올바른 구독을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-139">In case you have several subscriptions, check to make sure you're using the correct subscription when asked.</span></span> <span data-ttu-id="177ae-140">다음 명령을 실행하여 활성 구독을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-140">You can also run the following command to set the active subscription.</span></span> <span data-ttu-id="177ae-141">0을 사용자의 구독 식별자로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-141">Remember to replace the zeros with your subscription identifier.</span></span>

   ```bash
   az account set --subscription 00000000-0000-0000-0000-000000000000
   ```

- <span data-ttu-id="177ae-142">다음 명령을 사용하여 psql을 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-142">Connect psql to your server using the following command:</span></span>

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
  ```

   <span data-ttu-id="177ae-143">`server-name` 및 `admin-user`는 서버를 만들 때 관리자 계정에 대해 선택한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-143">Recall, `server-name`, and `admin-user` are the values you chose for the administrator account when you created the server.</span></span> <span data-ttu-id="177ae-144">`postgres`는 각 PostgreSQL 서버를 만들 때마다 포함되는 기본 관리 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-144">`postgres` is the default management database every PostgreSQL server is created with.</span></span> <span data-ttu-id="177ae-145">서버를 만들 때 제공한 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-145">You'll be prompted for the password you provided when you created the server.</span></span>

- <span data-ttu-id="177ae-146">성공적으로 연결되면 모든 데이터베이스를 나열하는 `\l` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-146">Once successfully connected, execute the `\l` command to list all databases.</span></span>

   <span data-ttu-id="177ae-147">이 명령을 실행하면 둘 이상의 기본 데이터베이스가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-147">This command will result in two or more default databases returned from.</span></span>

- <span data-ttu-id="177ae-148">서버에서 psql 작업 실행이 완료되면 `\q` 명령을 실행하여 `psql`을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-148">When you're finished executing psql operations on your server, execute the command `\q` to quit `psql`.</span></span>

- <span data-ttu-id="177ae-149">마지막으로, Cloud Shell을 종료하려면 `exit` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="177ae-149">Finally, to exit Cloud Shell, execute the command `exit`.</span></span>
