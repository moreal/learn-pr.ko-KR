<span data-ttu-id="03110-101">온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-101">Let's assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="03110-102">표준 PostgreSQL 서버 수준 방화벽 규칙을 사용하여 모든 보안 측면을 관리하고 서버에 대한 모든 액세스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="03110-102">You're managing all security aspects and you've locked down all access to your servers using the standard PostgreSQL server-level firewall rules.</span></span> <span data-ttu-id="03110-103">이제 Azure에서 동일한 서버 수준 방화벽 규칙을 구성할 수 있는지 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-103">Now you want to make sure that you can configure the same server-level firewall rules in Azure.</span></span>

## <a name="server-security-considerations-and-connection-methods"></a><span data-ttu-id="03110-104">서버 보안 고려 사항 및 연결 방법</span><span class="sxs-lookup"><span data-stu-id="03110-104">Server security considerations and connection methods</span></span>

<span data-ttu-id="03110-105">Azure Database for PostgreSQL 서버 및 데이터베이스에 대한 액세스를 제한하는 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-105">You have a number of options to restrict access to your Azure Database for PostgreSQL server and databases.</span></span> <span data-ttu-id="03110-106">네트워크 액세스는 네트워크, 서버 또는 데이터베이스 수준에서 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-106">Network access can be restricted at a network, server, or database level.</span></span> <span data-ttu-id="03110-107">다음 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-107">You can use any of the following options:</span></span>

- <span data-ttu-id="03110-108">데이터베이스 액세스를 제한하는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="03110-108">User accounts to restrict database access</span></span>
- <span data-ttu-id="03110-109">네트워크 액세스를 제한하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="03110-109">Virtual networks to restrict network access</span></span>
- <span data-ttu-id="03110-110">서버 액세스를 제한하는 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="03110-110">Firewall rules to restrict server access</span></span>

### <a name="authentication-and-authorization"></a><span data-ttu-id="03110-111">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="03110-111">Authentication and authorization</span></span>

<span data-ttu-id="03110-112">Azure Database for PostgreSQL 서버는 원시 PostgreSQL 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-112">The Azure Database for PostgreSQL server supports native PostgreSQL authentication.</span></span> <span data-ttu-id="03110-113">서버의 관리자 로그인을 사용하여 서버에 연결하고 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-113">You can connect and authenticate to the server with the server's admin login.</span></span> <span data-ttu-id="03110-114">또한 특정 데이터베이스에 연결하는 사용자를 만들어 액세스를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-114">You'll also create users to connect to specific databases to limit access.</span></span>

### <a name="what-is-a-virtual-network"></a><span data-ttu-id="03110-115">가상 네트워크란?</span><span class="sxs-lookup"><span data-stu-id="03110-115">What is a virtual network?</span></span>

<span data-ttu-id="03110-116">가상 네트워크는 Azure 네트워크 내에 만들어진 논리적으로 격리된 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-116">A virtual network is a logically isolated network that's created within the Azure network.</span></span> <span data-ttu-id="03110-117">가상 네트워크를 사용하여 다른 리소스에 연결할 수 있는 Azure 리소스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-117">You can use a virtual network to control what Azure resources can connect to other resources.</span></span>

<span data-ttu-id="03110-118">데이터베이스에 연결하는 웹 응용 프로그램을 실행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-118">Imagine you're running a web application that connects to a database.</span></span> <span data-ttu-id="03110-119">서브넷을 사용하여 네트워크의 다른 부분을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-119">You'll use subnets to isolate different parts of the network.</span></span> <span data-ttu-id="03110-120">서브넷은 IP 주소 범위를 기반으로 하는 네트워크의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-120">A subnet is a part of a network that's based on a range of IP addresses.</span></span>

<span data-ttu-id="03110-121">이러한 서브넷을 구성하려면 가상 네트워크를 만든 다음, 네트워크를 서브넷으로 세분화합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-121">To configure these subnets, you'll create a virtual network and then subdivide the network into subnets.</span></span> <span data-ttu-id="03110-122">웹 응용 프로그램은 한 서브넷과 다른 서브넷의 데이터베이스에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-122">The web application will operate on one subnet and the database on another subnet.</span></span> <span data-ttu-id="03110-123">각 서브넷에는 다른 네트워크와의 통신을 위한 자체의 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-123">Each subnet will have its own rules for communicating to and from the other network.</span></span> <span data-ttu-id="03110-124">이러한 규칙은 데이터베이스에서 웹 응용 프로그램으로의 액세스를 제한하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-124">These rules give you the ability to restrict access from the database to the web application.</span></span>

### <a name="what-is-a-firewall"></a><span data-ttu-id="03110-125">방화벽이란?</span><span class="sxs-lookup"><span data-stu-id="03110-125">What is a firewall?</span></span>

<span data-ttu-id="03110-126">방화벽은 각 요청의 원래 IP 주소에 따라 서버 액세스 권한을 부여하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-126">A firewall is a service that grants server access based on the originating IP address of each request.</span></span> <span data-ttu-id="03110-127">IP 주소 범위를 지정하는 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03110-127">You create firewall rules that specify ranges of IP addresses.</span></span> <span data-ttu-id="03110-128">이러한 권한이 부여된 IP 주소의 클라이언트만 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-128">Only clients from these granted IP addresses will be allowed to access the server.</span></span> <span data-ttu-id="03110-129">일반적으로 방화벽 규칙에는 특정 네트워크 프로토콜 및 포트 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="03110-129">Firewall rules, generally speaking, also include specific network protocol and port information.</span></span> <span data-ttu-id="03110-130">예를 들어 PostgreSQL 서버는 기본적으로 5432 포트에서 TCP 요청을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-130">For example, a PostgreSQL server by default listens to TCP requests on port 5432.</span></span>

### <a name="azure-database-for-postgresql-server-firewall"></a><span data-ttu-id="03110-131">Azure Database for PostgreSQL 서버 방화벽</span><span class="sxs-lookup"><span data-stu-id="03110-131">Azure Database for PostgreSQL server firewall</span></span>

<span data-ttu-id="03110-132">Azure Database for PostgreSQL 서버 방화벽은 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버에 대한 모든 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-132">The Azure Database for PostgreSQL server firewall prevents all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="03110-133">방화벽 구성을 통해 서버에 연결할 수 있는 IP 주소의 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-133">The firewall configuration allows you to specify a range of IP addresses that are allowed to connect to the server.</span></span> <span data-ttu-id="03110-134">서버는 항상 기본 PostgreSQL 연결 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-134">The server always uses the default PostgreSQL connection information.</span></span>

![들어오는 모든 요청의 IP 주소를 검색하는 Azure Database for PostgreSQL 서버 방화벽을 보여주는 일러스트레이션](../media/7-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a><span data-ttu-id="03110-137">Azure Database for PostgreSQL 서버 SSL 연결</span><span class="sxs-lookup"><span data-stu-id="03110-137">Azure Database for PostgreSQL server SSL connections</span></span>

<span data-ttu-id="03110-138">Azure Database for PostgreSQL은 클라이언트 응용 프로그램에서 SSL(Secure Sockets Layer)을 사용하여 PostgreSQL 서비스에 연결하도록 기본 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-138">Azure Database for PostgreSQL prefers that your client applications connect to the PostgreSQL service using the Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="03110-139">데이터베이스 서버와 클라이언트 응용 프로그램 간에 SSL 연결을 적용하면 서버와 클라이언트 간에 데이터를 암호화하여 "메시지 가로채기(man in the middle)" 공격 및 유사한 공격으로부터 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-139">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" and similar attacks by encrypting the data between the server and client.</span></span> <span data-ttu-id="03110-140">SSL을 사용하려면 클라이언트와 서버 간에 키와 엄격한 인증을 교환하여 연결이 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-140">Enabling SSL requires the exchange of keys and strict authentication between client and server for the connection to work.</span></span> <span data-ttu-id="03110-141">SSL을 사용하는 방법에 대한 자세한 내용은 이 학습 모듈의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="03110-141">Details about using SSL are beyond the scope of this learning module.</span></span>

## <a name="configure-connection-security"></a><span data-ttu-id="03110-142">연결 보안 구성</span><span class="sxs-lookup"><span data-stu-id="03110-142">Configure connection security</span></span>

<span data-ttu-id="03110-143">Azure Database for PostgreSQL 서버 방화벽을 구성하기 위해 수행하는 결정과 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-143">Let's look at the decisions and steps you make to configure an Azure Database for PostgreSQL server firewall.</span></span> <span data-ttu-id="03110-144">또한 이전에 만든 서버에 연결하는 방법도 확인하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-144">You'll also see how to connect to the server that you created earlier.</span></span>

<span data-ttu-id="03110-145">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-145">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span> <span data-ttu-id="03110-146">방화벽 규칙을 만들려는 서버 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-146">Navigate to the server resource for which you'd like to create a firewall rule.</span></span>

<span data-ttu-id="03110-147">그런 다음, **연결 보안** 옵션을 선택하여 오른쪽에 연결 보안 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03110-147">Then, you'll select the **Connection Security** option to open the connection security blade to the right.</span></span>

![PostgreSQL 데이터베이스 리소스 블레이드의 연결 보안 섹션을 보여주는 Azure Portal의 스크린샷](../media/7-db-security-settings.png)

<span data-ttu-id="03110-149">이 화면에는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-149">On this screen, you have several options.</span></span> <span data-ttu-id="03110-150">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-150">You can:</span></span>

- <span data-ttu-id="03110-151">**클라이언트 IP 추가** 단추를 클릭하여 포털에 액세스하는 데 사용하는 IP 주소를 방화벽 항목으로 추가합니다</span><span class="sxs-lookup"><span data-stu-id="03110-151">Add the IP address that you use to access the portal as a firewall entry by clicking on the **Add client IP** button.</span></span>
- <span data-ttu-id="03110-152">Azure 서비스에 대한 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="03110-152">Allow access to Azure services.</span></span> <span data-ttu-id="03110-153">모든 Azure 서비스는 기본적으로 PostgreSQL 서버에 액세스할 수 **없습니다**.</span><span class="sxs-lookup"><span data-stu-id="03110-153">By default, all Azure services **don't** have access to the PostgreSQL server.</span></span>
- <span data-ttu-id="03110-154">IP 주소 범위를 입력하여 방화벽 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="03110-154">Add firewall rules by entering ranges of IP addresses.</span></span>
- <span data-ttu-id="03110-155">SSL 연결 적용</span><span class="sxs-lookup"><span data-stu-id="03110-155">Enforce SSL connections.</span></span> <span data-ttu-id="03110-156">이 옵션은 클라이언트에서 SSL 인증서를 사용하여 서버에 연결하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-156">This option forces your client to connect to the server using an SSL certificate.</span></span>

<span data-ttu-id="03110-157">변경한 후에 업데이트된 구성을 저장하려면 항상 항목 필드 위에 있는 **저장** 아이콘을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-157">Always remember to click on the **Save** icon above the entry fields to save the updated configuration after you've made changes.</span></span>

### <a name="allow-access-to-azure-services"></a><span data-ttu-id="03110-158">Azure 서비스에 대한 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="03110-158">Allow access to Azure services</span></span>

<span data-ttu-id="03110-159">Azure Cloud Shell을 사용하여 서버에 액세스하거나 구성하려면 **Azure 서비스 방문 허용**을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-159">To use Azure Cloud Shell to access or configure your server, make sure to enable **Allow Access to Azure Services**.</span></span> <span data-ttu-id="03110-160">이 단계에서는 Cloud Shell에서 액세스할 수 있도록 허용하는 방화벽 규칙을 서버 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-160">This step is going to add a firewall rule to the server configuration to allow access from Cloud Shell.</span></span> <span data-ttu-id="03110-161">이 규칙은 추가한 사용자 지정 규칙 중 하나로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-161">This rule won't show as one of the custom rules that you add.</span></span>

<span data-ttu-id="03110-162">또한 **SSL 연결 적용**은 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-162">You also need to disable **Enforce SSL connection**.</span></span> <span data-ttu-id="03110-163">클라이언트 연결에 SSL이 필요한 경우 PowerShell에서는 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-163">PowerShell can't connect to the server if SSL is required for client connections.</span></span>

<span data-ttu-id="03110-164">이 두 옵션이 모두 올바르게 구성되지 않으면 명령줄에 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03110-164">Both of these options will result in an error message that's displayed on the command line if not configured correctly.</span></span>

<span data-ttu-id="03110-165">예를 들어 Azure 서비스에 대한 액세스가 허용되지 않고 SSL 연결 적용을 사용하도록 설정되는 경우 방화벽에서 액세스를 차단할 때 다음 오류와 비슷한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03110-165">For example, if access is not allowed to Azure services and enforce SSL connections is enabled, then you'll see something similar to this error when the firewall is blocking access:</span></span>

```output
psql: FATAL: no pg_hba.conf entry for host "123.45.67.89", user "adminuser", database "postgres", SSL on FATAL:  SSL connection is required. Please specify SSL options and retry.
```

### <a name="create-a-firewall-rule-using-the-portal"></a><span data-ttu-id="03110-166">포털을 사용하여 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="03110-166">Create a firewall rule using the portal</span></span>

<span data-ttu-id="03110-167">모든 IP 주소에서 액세스를 제공하는 방화벽 규칙을 만들려고 한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-167">Let's say you want to create a firewall rule that provides access from any IP address.</span></span>

> [!WARNING]
> <span data-ttu-id="03110-168">이 방화벽 규칙을 만들면 인터넷의 모든 IP 주소에서 서버에 연결하려고 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-168">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="03110-169">클라이언트가 사용자 이름과 암호를 사용하여 서버에 액세스할 수 있더라도 이 규칙을 신중하게 사용하도록 설정하고 보안에 미치는 영향을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-169">Even though clients won't be able access the server without the username and password, enable this rule with caution and make sure you understand the security implications.</span></span>

<span data-ttu-id="03110-170">레이블이 지정된 필드에서 다음 데이터를 입력하여 새 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03110-170">You create a new firewall rule by entering the following data in the labeled fields:</span></span>

- <span data-ttu-id="03110-171">규칙 이름: `AllowAll`</span><span class="sxs-lookup"><span data-stu-id="03110-171">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="03110-172">시작 IP: `0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="03110-172">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="03110-173">종료 IP: `255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="03110-173">End IP: `255.255.255.255`</span></span>

<span data-ttu-id="03110-174">방화벽 규칙을 제거하려면 삭제하려는 규칙 끝에 있는 줄임표(...)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-174">To remove a firewall rule, you'll click the ellipsis (...) at the end of the rule that you want to delete.</span></span> <span data-ttu-id="03110-175">**삭제** 단추를 클릭하여 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-175">Click the **Delete** button to delete the rule.</span></span>

<span data-ttu-id="03110-176">항목 필드 위에 있는 **저장** 아이콘을 클릭하여 규칙 삭제를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-176">Click on the **Save** icon above the entry fields to commit the deletion of the rule.</span></span>

### <a name="create-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="03110-177">Azure CLI를 사용하여 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="03110-177">Create a firewall rule using the Azure CLI</span></span>

<span data-ttu-id="03110-178">Azure CLI를 사용하여 `az postgres server firewall-rule create` 명령으로 서버에 방화벽 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-178">You can use the Azure CLI to add firewall rules to your server with the `az postgres server firewall-rule create` command.</span></span> <span data-ttu-id="03110-179">위의 규칙을 만드는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-179">Here's an example that creates the rule from above.</span></span>

```azurecli
az postgres server firewall-rule create \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --server <server-name> \
  --name AllowAll \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 255.255.255.255
```

<span data-ttu-id="03110-180">`az postgres server firewall-rule delete` 명령을 사용하여 서버에서 방화벽 규칙을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-180">You remove firewall rules from your server with the command `az postgres server firewall-rule delete`.</span></span> <span data-ttu-id="03110-181">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-181">Here's an example:</span></span>

```azurecli
az postgres server firewall-rule delete \
  --name AllowAll \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --server-name <server-name>
```

## <a name="connecting-to-your-server"></a><span data-ttu-id="03110-182">서버에 연결</span><span class="sxs-lookup"><span data-stu-id="03110-182">Connecting to your server</span></span>

<span data-ttu-id="03110-183">최신 데이터베이스와 마찬가지로, PostgreSQL도 최상의 성능을 얻기 위해 정기적으로 서버를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-183">Like any modern database, PostgreSQL requires regular server administration to achieve best performance.</span></span> <span data-ttu-id="03110-184">Azure Database for PostgreSQL 서버를 연결하고 관리하는 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-184">You have a number of options to connect and manage your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="03110-185">`psql`을 사용하여 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-185">We'll use `psql` to connect to the server.</span></span>

### <a name="what-is-psql"></a><span data-ttu-id="03110-186">psql이란?</span><span class="sxs-lookup"><span data-stu-id="03110-186">What is psql?</span></span>

<span data-ttu-id="03110-187">`psql`이라는 명령줄 도구는 PostgreSQL 서버 및 데이터베이스 작업을 위한 PostgreSQL 분산 대화형 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-187">The command-line tool called `psql` is the PostgreSQL distributed interactive terminal for working with PostgreSQL servers and databases.</span></span> <span data-ttu-id="03110-188">`psql`은 다른 PostgreSQL 구현과 마찬가지로 Azure Database for PostgreSQL에서 작동하며 Azure Cloud Shell에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-188">`psql` works with Azure Database for PostgreSQL the same as with any other PostgreSQL implementation and is included with Azure Cloud Shell.</span></span> <span data-ttu-id="03110-189">`psql` 도구를 사용하면 데이터베이스를 관리할 수 있을 뿐만 아니라 이러한 데이터베이스에 대한 구조 쿼리도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-189">The `psql` tool allows you to manage databases as well as execute structure queries against these databases.</span></span>

<span data-ttu-id="03110-190">`psql`을 사용하려면 PostgreSQL 서버에 성공적으로 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-190">Using `psql` requires a successful connection to a PostgreSQL server.</span></span> <span data-ttu-id="03110-191">`psql`로 작업할 때 사용할 수 있는 여러 가지 명령줄 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-191">There are a number of command-line parameters available for use when working with `psql`.</span></span>

- <span data-ttu-id="03110-192">`--host` - 연결하려는 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-192">`--host` - The host to which you'd like to connect.</span></span>
- <span data-ttu-id="03110-193">`--username` - 연결할 사용자 이름/ID입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-193">`--username` - The user name/ID with which to connect.</span></span>
- <span data-ttu-id="03110-194">`--dbname` - 연결할 데이타베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="03110-194">`--dbname` - The name of the database to connect to.</span></span>

> [!TIP]
> <span data-ttu-id="03110-195">서버 액세스 및 데이터베이스 구성을 관리하는 경우 일반적으로 `postgres` 관리 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="03110-195">You'll typically connect to the `postgres` management database when managing your server access and database configurations.</span></span>

<span data-ttu-id="03110-196">전체 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-196">Here is the complete command:</span></span>

```bash
psql --host=<server-name>.postgres.database.azure.com
      --username=<admin-user>@<server-name>
      --dbname=<database>
```

<span data-ttu-id="03110-197">사용자가 연결되면 명령 프롬프트가 표시되고 서버와 데이터베이스에 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-197">After you're connected, you'll be presented with a command prompt and can execute commands to your server and databases.</span></span>

<span data-ttu-id="03110-198">이제 Azure Database for PostgreSQL 보안 설정을 구성하는 단계를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-198">You've now seen the steps that you take to configure Azure Database for PostgreSQL security settings.</span></span> <span data-ttu-id="03110-199">다음 단원에서는 Azure Database for PostgreSQL 보안 설정을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-199">In the next unit, you'll configure Azure Database for PostgreSQL security settings.</span></span> <span data-ttu-id="03110-200">또한 Cloud Shell을 사용하여 서버에 연결하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03110-200">You'll also connect to the server using Cloud Shell.</span></span>
