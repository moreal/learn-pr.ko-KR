<span data-ttu-id="532de-101">온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-101">Lets' assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="532de-102">표준 PostgreSQL 서버 수준 방화벽 규칙을 사용하여 모든 보안 측면을 관리하고 서버에 대한 모든 액세스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="532de-102">You're managing all security aspects and locked down all access to your servers using the standard PostgreSQL server level firewall rules.</span></span> <span data-ttu-id="532de-103">이제 Azure에서 동일한 서버 수준 방화벽 규칙을 구성할 수 있는지 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-103">You now want to make sure that you can configure the same server level firewall rules in Azure.</span></span>

## <a name="server-security-considerations-and-connection-methods"></a><span data-ttu-id="532de-104">서버 보안 고려 사항 및 연결 방법</span><span class="sxs-lookup"><span data-stu-id="532de-104">Server Security Considerations and Connection Methods</span></span>

<span data-ttu-id="532de-105">Azure Database for PostgreSQL 서버 및 데이터베이스에 대한 액세스를 제한하는 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-105">You have a number of options to restrict access to your Azure Database for PostgreSQL server and databases.</span></span> <span data-ttu-id="532de-106">네트워크 액세스는 네트워크, 서버 또는 데이터베이스 수준에서 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-106">Network access can be restricted at a network, server, or database level.</span></span> <span data-ttu-id="532de-107">다음 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-107">You can use any of the following options:</span></span>

- <span data-ttu-id="532de-108">데이터베이스 액세스를 제한하는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="532de-108">User accounts to restrict database access</span></span>
- <span data-ttu-id="532de-109">네트워크 액세스를 제한하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="532de-109">Virtual networks to restrict network access</span></span>
- <span data-ttu-id="532de-110">서버 액세스를 제한하는 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="532de-110">Firewall rules to restrict server access</span></span>

### <a name="authentication-and-authorization"></a><span data-ttu-id="532de-111">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="532de-111">Authentication and authorization</span></span>

<span data-ttu-id="532de-112">Azure Database for PostgreSQL 서버는 원시 PostgreSQL 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-112">Azure Database for PostgreSQL server supports native PostgreSQL authentication.</span></span> <span data-ttu-id="532de-113">서버의 관리자 로그인을 사용하여 서버에 연결하고 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-113">You can connect and authenticate to server with the server's admin login.</span></span> <span data-ttu-id="532de-114">또한 특정 데이터베이스에 연결하는 사용자를 만들어 액세스를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-114">You'll also create users to connect to specific databases to limit access.</span></span>

### <a name="what-is-a-virtual-network"></a><span data-ttu-id="532de-115">가상 네트워크란?</span><span class="sxs-lookup"><span data-stu-id="532de-115">What is a Virtual Network?</span></span>

<span data-ttu-id="532de-116">가상 네트워크는 Azure 네트워크 내에 만들어진 논리적으로 격리된 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="532de-116">A virtual network is a logically isolated network created within the Azure network.</span></span> <span data-ttu-id="532de-117">가상 네트워크를 사용하여 다른 리소스에 연결할 수 있는 Azure 리소스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-117">You can use a virtual network to control what Azure resources can connect to other resources.</span></span>

<span data-ttu-id="532de-118">데이터베이스에 연결하는 웹 응용 프로그램을 실행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-118">Imagine you're running a web application that connects to a database.</span></span> <span data-ttu-id="532de-119">서브넷을 사용하여 네트워크의 다른 부분을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-119">You'll use subnets to isolate different parts of the network.</span></span> <span data-ttu-id="532de-120">서브넷은 IP 주소 범위를 기반으로 하는 네트워크의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="532de-120">A subnet is a part of a network based upon a range of IP addresses.</span></span>

<span data-ttu-id="532de-121">이러한 서브넷을 구성하려면 가상 네트워크를 만든 다음, 네트워크를 서브넷으로 세분화합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-121">To configure these subnets, you'll create a virtual network and then subdivide the network into subnets.</span></span> <span data-ttu-id="532de-122">웹 응용 프로그램은 한 서브넷과 다른 서브넷의 데이터베이스에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-122">The web application will operate on one subnet and the database on another subnet.</span></span> <span data-ttu-id="532de-123">각 서브넷에는 다른 네트워크와의 통신을 위한 자체의 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-123">Each subnet would have its own rules for communicating to and from the other network.</span></span> <span data-ttu-id="532de-124">이러한 규칙은 데이터베이스에서 웹 응용 프로그램으로의 액세스를 제한하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-124">These rules give you the ability to restrict access from the database to the web application.</span></span>

<span data-ttu-id="532de-125">가상 네트워크를 만드는 것은 이 모듈의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="532de-125">Creating a virtual network is beyond the scope of this module.</span></span> <span data-ttu-id="532de-126">자세한 정보가 필요하면 가상 네트워크와 관련된 다른 학습 모듈을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="532de-126">If you need more information, please explore other learning modules related to virtual networks.</span></span>

### <a name="what-is-a-firewall"></a><span data-ttu-id="532de-127">방화벽이란?</span><span class="sxs-lookup"><span data-stu-id="532de-127">What is a firewall?</span></span>

<span data-ttu-id="532de-128">방화벽은 각 요청의 원래 IP 주소에 따라 서버 액세스 권한을 부여하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="532de-128">A firewall is a service that grants server access based on the originating IP address of each request.</span></span> <span data-ttu-id="532de-129">IP 주소 범위를 지정하는 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="532de-129">You create firewall rules that specify ranges of IP addresses.</span></span> <span data-ttu-id="532de-130">이러한 규칙을 통해 부여된 IP 주소의 클라이언트만 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-130">Only clients from these granted IP addresses, will be allowed to access the server.</span></span> <span data-ttu-id="532de-131">또한 일반적으로 말하는 방화벽 규칙에는 특정 네트워크 프로토콜 및 포트 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="532de-131">Firewall rules generally speaking also includes specific network protocol and port information.</span></span> <span data-ttu-id="532de-132">예를 들어 PostgreSQL 서버는 기본적으로 5432 포트에서 TCP 요청을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-132">For example, a PostgreSQL server by default listens to TCP requests on port 5432.</span></span>

### <a name="azure-database-for-postgresql-server-firewall"></a><span data-ttu-id="532de-133">Azure Database for PostgreSQL 서버 방화벽</span><span class="sxs-lookup"><span data-stu-id="532de-133">Azure Database for PostgreSQL server firewall</span></span>

<span data-ttu-id="532de-134">Azure Database for PostgreSQL 서버 방화벽은 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버에 대한 모든 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-134">The Azure Database for PostgreSQL server firewall prevents all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="532de-135">방화벽 구성을 통해 서버에 연결할 수 있는 IP 주소의 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-135">The firewall configuration allows you to specify a range of IP addresses that are allowed to connect to the server.</span></span> <span data-ttu-id="532de-136">서버는 항상 기본 PostgreSQL 연결 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-136">The server always uses the default PostgreSQL connection information.</span></span>

![Azure 방화벽 기능 다이어그램](../media-draft/7-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a><span data-ttu-id="532de-138">Azure Database for PostgreSQL 서버 SSL 연결</span><span class="sxs-lookup"><span data-stu-id="532de-138">Azure Database for PostgreSQL server SSL connections</span></span>

<span data-ttu-id="532de-139">Azure Database for PostgreSQL은 기본적으로 클라이언트 응용 프로그램에서 SSL(Secure Sockets Layer)을 사용하여 PostgreSQL 서비스에 연결하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-139">Azure Database for PostgreSQL prefers your client applications connects to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="532de-140">데이터베이스 서버와 클라이언트 응용 프로그램 간에 SSL 연결을 적용하면 서버와 응용 프로그램 간의 데이터를 암호화하여 "메시지 가로채기(man in the middle)" 공격 및 이와 유사한 공격으로부터 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-140">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" and similar attacks by encrypting the data between the server and client.</span></span> <span data-ttu-id="532de-141">SSL을 사용하려면 클라이언트와 서버 간에 키와 엄격한 인증을 교환하여 연결이 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-141">Enabling SSL requires the exchange of keys and strict authentication between client and server for the connection to work.</span></span> <span data-ttu-id="532de-142">SSL을 사용하는 방법에 대한 자세한 내용은 이 학습 모듈의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="532de-142">Details about using SSL are beyond the scope of this learning module.</span></span> <span data-ttu-id="532de-143">자세한 정보가 필요하면 SSL과 관련된 다른 학습 모듈을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="532de-143">If you need more information, please explore other learning modules related to SSL.</span></span>

## <a name="configure-connection-security"></a><span data-ttu-id="532de-144">연결 보안 구성</span><span class="sxs-lookup"><span data-stu-id="532de-144">Configure Connection Security</span></span>

<span data-ttu-id="532de-145">Azure Database for PostgreSQL 서버 방화벽을 구성하기 위해 수행하는 결정과 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-145">Let's look at the decisions and steps you make to configure an Azure Database for PostgreSQL server firewall.</span></span> <span data-ttu-id="532de-146">또한 이전에 만든 서버에 연결하는 방법도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-146">You'll also see how to connect to the server you've created earlier.</span></span>

<span data-ttu-id="532de-147">먼저 [Azure Portal](https://portal.azure.com?azure-portal=true)을 열고 방화벽 규칙을 만들려는 서버 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-147">First, you'll open the [Azure portal](https://portal.azure.com?azure-portal=true) and navigate to the server resource for which you would like to create a firewall rule.</span></span>

<span data-ttu-id="532de-148">그런 다음, **연결 보안** 옵션을 선택하여 오른쪽에 [연결 보안] 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="532de-148">Then you'll select the **Connection Security** option to open the connection security blade to the right.</span></span>

![PostgreSQL 데이터베이스 보안 설정](../media-draft/7-db-security-settings.png)

<span data-ttu-id="532de-150">이 화면에는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-150">On this screen, you have several options.</span></span> <span data-ttu-id="532de-151">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-151">You can:</span></span>

- <span data-ttu-id="532de-152">**+ 클라이언트 IP 추가** 단추를 클릭하여 포털에 액세스하는 데 사용하는 IP 주소를 방화벽 항목으로 추가합니다</span><span class="sxs-lookup"><span data-stu-id="532de-152">Add the IP address you use to access the portal as a firewall entry by clicking on the **+ Add client IP** button</span></span>
- <span data-ttu-id="532de-153">Azure 서비스 방문 허용.</span><span class="sxs-lookup"><span data-stu-id="532de-153">Allow access to Azure services.</span></span> <span data-ttu-id="532de-154">모든 Azure 서비스는 기본적으로 PostgreSQL 서버에 **액세스할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="532de-154">By default all Azure services **don't** have access to the PostgreSQL server</span></span>
- <span data-ttu-id="532de-155">IP 주소 범위를 입력하여 방화벽 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="532de-155">Add firewall rules by entering ranges of IP addresses</span></span>
- <span data-ttu-id="532de-156">SSL 연결 적용.</span><span class="sxs-lookup"><span data-stu-id="532de-156">Enforce SSL connections.</span></span> <span data-ttu-id="532de-157">이 옵션은 클라이언트에서 SSL 인증서를 사용하여 서버에 연결하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-157">This option forces you client to connect to the server using an SSL certificate.</span></span>

<span data-ttu-id="532de-158">변경한 후에 업데이트된 구성을 저장하려면 항상 입력 필드 위에 있는 **저장** 아이콘을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-158">Always remember to click on the **Save** icon above the entry fields to save the updated configuration once you've made changes.</span></span>

### <a name="allow-access-to-azure-services"></a><span data-ttu-id="532de-159">Azure 서비스 방문 허용</span><span class="sxs-lookup"><span data-stu-id="532de-159">Allow access to Azure services</span></span>

<span data-ttu-id="532de-160">Azure Cloud Shell을 사용하여 서버에 액세스하거나 구성하려면 **Azure 서비스 방문 허용**을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-160">To use Azure Cloud Shell to access or configure your server, make sure to enable **Allow Access to Azure Services**.</span></span> <span data-ttu-id="532de-161">이 단계에서는 Cloud Shell에서 액세스할 수 있도록 허용하는 방화벽 규칙을 서버 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-161">This step is going to add a firewall rule to the server configuration to allow access from Cloud Shell.</span></span> <span data-ttu-id="532de-162">이 규칙은 추가하는 사용자 지정 규칙 중 하나로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-162">This rule will not show as one of the custom rules you add though.</span></span>

<span data-ttu-id="532de-163">또한 **SSL 연결 적용**은 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-163">You also need to disable **Enforce SSL connection**.</span></span> <span data-ttu-id="532de-164">클라이언트 연결에 SSL이 필요한 경우 PowerShell에서 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-164">PowerShell cann't connect to the server if SSL is required for client connections.</span></span>

<span data-ttu-id="532de-165">이 두 옵션이 모두 올바르게 구성되지 않으면 명령줄에 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="532de-165">Both of these options will result in an error message displayed on the command line if not configured correctly.</span></span>

<span data-ttu-id="532de-166">예를 들어 Azure 서비스에 대한 액세스가 허용되지 않고 SSL 연결 적용을 사용하도록 설정되는 경우 방화벽에서 액세스를 차단할 때 다음 오류와 비슷한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="532de-166">For example, if access is not allowed to Azure services and enforce SSL connections is enabled then you'll see something similar to this error when the firewall is blocking access.</span></span>

> <span data-ttu-id="532de-167">psql: FATAL: "123.45.67.89" 호스트, "adminuser" 사용자, "postgres" 데이터베이스에 대한 pg_hba.conf 항목이 없습니다. SSL on FATAL: SSL 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-167">psql: FATAL: no pg_hba.conf entry for host "123.45.67.89", user "adminuser", database "postgres", SSL on FATAL:  SSL connection is required.</span></span> <span data-ttu-id="532de-168">SSL 옵션을 지정하고 다시 시도하십시오.</span><span class="sxs-lookup"><span data-stu-id="532de-168">Please specify SSL options and retry.</span></span>

### <a name="create-a-firewall-rule-using-the-portal"></a><span data-ttu-id="532de-169">포털을 사용하여 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="532de-169">Create a firewall rule using the portal</span></span>

<span data-ttu-id="532de-170">모든 IP 주소에서 액세스를 제공하는 방화벽 규칙을 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-170">Let's say, you want to create a firewall rule that provides access from any IP address.</span></span>

> [!WARNING]
> <span data-ttu-id="532de-171">이 방화벽 규칙을 만들면 인터넷의 모든 IP 주소에서 서버에 연결하려고 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-171">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="532de-172">클라이언트에서 사용자 이름과 암호를 사용하여 서버에 액세스 할 수 있는 경우에도 이 규칙을 신중하게 사용하도록 설정하고 보안에 미치는 영향을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-172">Eventhough clients will not be able access the server without the username and password, enable this rule with caution and make sure you understand the security implications.</span></span>

<span data-ttu-id="532de-173">레이블이 지정된 필드에서 다음 데이터를 입력하여 새 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="532de-173">You create a new firewall rule by entering the following data in the labeled fields:</span></span>

- <span data-ttu-id="532de-174">규칙 이름: `AllowAll`</span><span class="sxs-lookup"><span data-stu-id="532de-174">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="532de-175">시작 IP: `0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="532de-175">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="532de-176">종료 IP: `255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="532de-176">End IP: `255.255.255.255`</span></span>

<span data-ttu-id="532de-177">방화벽 규칙을 제거하려면 삭제하려는 규칙 끝에 있는 줄임표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-177">To remove a firewall rule, you'll click the ellipsis at the end of the rule you want to delete.</span></span> <span data-ttu-id="532de-178">[삭제] 단추를 클릭하여 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-178">Click the Delete button to delete the rule.</span></span>

<span data-ttu-id="532de-179">입력 필드 위에 있는 **저장** 아이콘을 클릭하여 규칙 삭제를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-179">Click on the **Save** icon above the entry fields to commit the deletion of the rule.</span></span>

### <a name="create-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="532de-180">Azure CLI를 사용하여 방화벽 만들기</span><span class="sxs-lookup"><span data-stu-id="532de-180">Create a firewall rule using the Azure CLI</span></span>

<span data-ttu-id="532de-181">Azure CLI를 사용하여 Azure CloudShell에서 `az postgres server firewall-rule create` 명령으로 서버에 방화벽 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-181">You use the Azure CLI to add firewall rules to your server with the `az postgres server firewall-rule create` command using Azure CloudShell.</span></span>

<span data-ttu-id="532de-182">다음 명령을 사용하여 위와 동일한 규칙을 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-182">Let's say you want to create the same rules as above You'' use the following command:</span></span>

  ```bash
  az postgres server firewall-rule create --resource-group <resource_group_name> --server <server-name> --name AllowAll --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
  ```

<span data-ttu-id="532de-183">`az postgres server firewall-rule delete` 명령을 사용하여 서버에서 방화벽 규칙을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-183">You remove firewall rules from your server with the command `az postgres server firewall-rule delete`.</span></span>

<span data-ttu-id="532de-184">만든 방화벽을 삭제하고 나서 다음 명령을 사용하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-184">Let's say you want to delete the firewall you created then use the following command:</span></span>

  ```bash
  az postgres server firewall-rule delete --name AllowAll --resource-group <resource_group_name> --server-name <server-name>
  ```

## <a name="connecting-to-your-server"></a><span data-ttu-id="532de-185">서버에 연결</span><span class="sxs-lookup"><span data-stu-id="532de-185">Connecting to your server</span></span>

<span data-ttu-id="532de-186">모든 최신 데이터베이스와 마찬가지로, PostgreSQL도 최상의 성능을 얻기 위해 정기적으로 서버를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-186">Like any modern database, PostgreSQL requires regularly server administration to achieve best performance.</span></span> <span data-ttu-id="532de-187">Azure Database for PostgreSQL 서버를 연결하고 관리하는 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-187">You have a number of options to connect and manage your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="532de-188">`psql`을 사용하여 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-188">We'll use `psql` to connect to the server.</span></span>

### <a name="what-is-psql"></a><span data-ttu-id="532de-189">psql이란?</span><span class="sxs-lookup"><span data-stu-id="532de-189">What is psql?</span></span>

<span data-ttu-id="532de-190">`psql`이라는 명령줄 도구는 PostgreSQL 서버 및 데이터베이스 작업을 위한 PostgreSQL 분산 대화형 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="532de-190">The command-line tool called `psql` is the PostgreSQL distributed interactive terminal for working with PostgreSQL server and databases.</span></span> <span data-ttu-id="532de-191">`psql`은 다른 PostgreSQL 구현과 마찬가지로 Azure Database for PostgreSQL에서 작동하며 Azure Cloud Shell에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-191">`psql` works with Azure Database for PostgreSQL the same as with any other PostgreSQL implementation and is included with the Azure Cloud Shell.</span></span> <span data-ttu-id="532de-192">`psql` 도구를 사용하면 데이터베이스를 관리할 수 있을 뿐만 아니라 이러한 데이터베이스에 대한 구조 쿼리도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-192">The `psql` tool allows you to manage databases as well as execute structure queries against these databases.</span></span>

<span data-ttu-id="532de-193">`psql`을 사용하려면 PostgreSQL 서버에 성공적으로 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-193">Using `psql` requires a successful connection to a PostgreSQL server.</span></span> <span data-ttu-id="532de-194">`psql`을 사용할 때 사용할 수 있는 여러 가지 명령줄 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-194">There are a number of command-line parameters available for use when working with `psql`.</span></span>

- <span data-ttu-id="532de-195">`--host` - 연결하려는 호스트</span><span class="sxs-lookup"><span data-stu-id="532de-195">`--host` - the host to which you'd like to connect</span></span>
- <span data-ttu-id="532de-196">`--username` - 연결하는 데 사용할</span><span class="sxs-lookup"><span data-stu-id="532de-196">`--username` - the user name/i.d.</span></span> <span data-ttu-id="532de-197">사용자 이름/ID</span><span class="sxs-lookup"><span data-stu-id="532de-197">with which to connect</span></span>
- <span data-ttu-id="532de-198">`--dbname` - 연결할 데이타베이스의 이름</span><span class="sxs-lookup"><span data-stu-id="532de-198">`--dbname` - the name of the database to connect to.</span></span>

> [!Note]
> <span data-ttu-id="532de-199">서버 액세스 및 데이터베이스 구성을 관리하는 경우 일반적으로 `postgres` 관리 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-199">You'll typically connect to the `postgres` management database when managing your server access and databases configuration.</span></span>

<span data-ttu-id="532de-200">전체 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-200">Here is the complete command:</span></span>

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=<database>
  ```

<span data-ttu-id="532de-201">연결되면 명령 프롬프트가 표시되고 서버와 데이터베이스에 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-201">Once connected, you'll be presented with a command prompt and can execute commands to your server and databases.</span></span>

<span data-ttu-id="532de-202">이제 Azure Database for PostgreSQL 보안 설정을 구성하는 단계를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="532de-202">You've now seen the steps you take to configure an Azure Database for PostgreSQL security settings.</span></span> <span data-ttu-id="532de-203">다음 단원에서는 Azure Database for PostgreSQL 보안 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-203">In the next unit, you'll configure an  Azure Database for PostgreSQL security settings.</span></span> <span data-ttu-id="532de-204">또한 Cloud Shell을 사용하여 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="532de-204">You'll also connect to the server using Cloud Shell.</span></span>