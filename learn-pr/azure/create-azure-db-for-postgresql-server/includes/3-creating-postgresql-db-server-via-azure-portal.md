<span data-ttu-id="afa6d-101">현재 유연한 데이터 형식 및 지형 공간 지원을 사용하여 온-프레미스 PostgreSQL 관계형 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-101">Let's assume that you're currently using an on-premise PostgreSQL relational database using flexible data types and geospatial support.</span></span> <span data-ttu-id="afa6d-102">회사에서 확장을 고려하고 있으며, 데이터베이스를 확장할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-102">Your company is looking at expanding, requiring the database to scale.</span></span> <span data-ttu-id="afa6d-103">추가 하드웨어에 투자하는 대신, 최적의 클라우드 호스팅 데이터베이스 제품을 찾아야 하며, Azure Database for PostgreSQL 서버를 사용하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-103">As an alternative to investing in additional hardware, you are tasked with finding an optimal cloud-hosted database offering and you have decided to use an Azure Database for PostgreSQL server.</span></span>

## <a name="what-is-an-azure-database-for-postgresql-server"></a><span data-ttu-id="afa6d-104">Azure Database for PostgreSQL 서버란?</span><span class="sxs-lookup"><span data-stu-id="afa6d-104">What is an Azure Database for PostgreSQL server?</span></span>

<span data-ttu-id="afa6d-105">PostgreSQL 서버는 하나 이상의 데이터베이스에 대한 중앙 관리 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-105">The PostgreSQL server is a central administration point for one or more databases.</span></span> <span data-ttu-id="afa6d-106">Azure에서 PostgreSQL 서비스는 성능을 보장하고 서버 수준의 액세스와 기능을 제공하는 관리되는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-106">The PostgreSQL service in Azure is a managed resource that provides performance guarantees, and provides access and features at the server level.</span></span>

<span data-ttu-id="afa6d-107">**Azure Database for PostgreSQL** 서버는 데이터베이스에 대한 부모 _리소스_입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-107">An **Azure Database for PostgreSQL** server is the parent _resource_ for a database.</span></span> <span data-ttu-id="afa6d-108">_리소스_는 Azure를 통해 사용할 수 있는 관리 가능한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-108">A _resource_ is a manageable item that is available through Azure.</span></span> <span data-ttu-id="afa6d-109">이 리소스를 만들면 서버 인스턴스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-109">Creating this resource allows you to configure your server instance.</span></span>

### <a name="what-is-an-azure-database-for-postgresql-server-resource"></a><span data-ttu-id="afa6d-110">Azure Database for PostgreSQL 서버 리소스란?</span><span class="sxs-lookup"><span data-stu-id="afa6d-110">What is an Azure Database for PostgreSQL server resource?</span></span>

<span data-ttu-id="afa6d-111">Azure Database for PostgreSQL 서버 리소스는 서버와 데이터베이스의 수명에 강력한 영향을 주는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-111">An Azure Database for PostgreSQL server resource is a container with strong lifetime implications for your server and databases.</span></span> <span data-ttu-id="afa6d-112">서버 리소스가 삭제되면 모든 데이터베이스도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-112">If the server resource is deleted, all databases are also deleted.</span></span> <span data-ttu-id="afa6d-113">부모 리소스에 속한 모든 리소스는 동일한 지역에서 호스팅된다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="afa6d-113">Keep in mind that all resources belonging to the parent are hosted in the same region.</span></span>

<span data-ttu-id="afa6d-114">서버 리소스 이름은 서버 엔드포인트 이름을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-114">The server resource name is used to define the server endpoint name.</span></span> <span data-ttu-id="afa6d-115">예를 들어 리소스 이름이 **mypgsqlserver**이면 서버 이름은 **mypgsqlserver.postgres.database.azure.com**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-115">For example, if the resource name is **mypgsqlserver** then the server name becomes **mypgsqlserver.postgres.database.azure.com**</span></span>

<span data-ttu-id="afa6d-116">또한 서버 리소스는 해당 데이터베이스에 적용되는 관리 정책에 대한 __연결 범위__를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-116">The server resource also provides the __connection scope__ for management policies that apply to its database.</span></span> <span data-ttu-id="afa6d-117">예를 들어 로그인, 방화벽, 사용자, 역할 및 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-117">For example, login, firewall, users, roles, and configuration.</span></span>

<span data-ttu-id="afa6d-118">PostgreSQL의 오픈 소스 버전과 마찬가지로, 서버는 여러 버전에서 사용할 수 있으며 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-118">Just like the open-source version of PostgreSQL, the server is available in several versions and allows for the installation of extensions.</span></span> <span data-ttu-id="afa6d-119">설치할 서버 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-119">You'll choose which server version to install.</span></span>

> [!NOTE]
> <span data-ttu-id="afa6d-120">확장을 사용하면 여러 SQL 개체를 모두 단일 패키지에 번들로 묶을 수 있으며, 이에 따라 단일 명령으로 로드하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-120">Extensions allow for bundling multiple SQL objects together in a single package that can be loaded or removed with a single command.</span></span> <span data-ttu-id="afa6d-121">확장의 예로 ```chkpass```가 있으며, 이는 자동으로 암호화된 암호에 대한 데이터 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-121">An example of >an extension is ```chkpass```, which provides a data type for auto-encrypted passwords.</span></span>

## <a name="pricing-tiers"></a><span data-ttu-id="afa6d-122">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="afa6d-122">Pricing tiers</span></span>

<span data-ttu-id="afa6d-123">Azure Database for PostgreSQL은 계산 성능 및 저장소와 같은 매개 변수를 기반으로 하는 세 가지 가격 책정 계층 중에서 선택할 수 있는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-123">The Azure Database for PostgreSQL provides you with the option to choose from three pricing tiers based on parameters such as compute power and storage.</span></span>

### <a name="basic"></a><span data-ttu-id="afa6d-124">기본</span><span class="sxs-lookup"><span data-stu-id="afa6d-124">Basic</span></span>

<span data-ttu-id="afa6d-125">**기본** 계층은 간단한 계산 및 I/O 성능이 필요한 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-125">The **Basic** tier is ideal for workloads that requires light compute and I/O performance.</span></span> <span data-ttu-id="afa6d-126">이 계층에서 액세스 할 수 있는 하드웨어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-126">In this tier, you have access to the following hardware:</span></span>

- <span data-ttu-id="afa6d-127">계산 4세대 CPU(Intel E5-2673 v3 (Haswell) 2.4GHz 프로세서 기반, 1-2개의 vCore 구성으로 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="afa6d-127">Compute Gen 4 CPUs base on Intel E5-2673 v3 (Haswell) 2.4-GHz processors available as either a 1 or 2 vCore configuration</span></span>
- <span data-ttu-id="afa6d-128">계산 5세대 CPU(Intel E5-2673 v4 (Broadwell) 2.3GHz 프로세서 기반, 1-2개의 vCore 구성으로 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="afa6d-128">Compute Gen 5 CPUs base on Intel E5-2673 v4 (Broadwell) 2.3-GHz processors available as either a 1 or 2 vCore configuration</span></span>
- <span data-ttu-id="afa6d-129">저장소(최대 1TB)</span><span class="sxs-lookup"><span data-stu-id="afa6d-129">Storage up to 1 TB</span></span>
- <span data-ttu-id="afa6d-130">로컬 중복 백업</span><span class="sxs-lookup"><span data-stu-id="afa6d-130">Locally redundant backup</span></span>

<span data-ttu-id="afa6d-131">특정 가격 책정 계층 설정을 사용하여 나중에 예제 서버를 만들 때 특정 시나리오에 대한 지원을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-131">You'll use a specific pricing tier setting to illustrate support of a specific scenario when you create an example server later.</span></span> <span data-ttu-id="afa6d-132">프로덕션 서버의 경우 사용자 환경에 맞게 가격 책정 계층을 선택할 수 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="afa6d-132">Keep in mind that for production servers, you'll choose a pricing tier to match your environment.</span></span>

### <a name="general-purpose"></a><span data-ttu-id="afa6d-133">범용</span><span class="sxs-lookup"><span data-stu-id="afa6d-133">General Purpose</span></span>

<span data-ttu-id="afa6d-134">**범용** 계층은 확장 가능한 I/O 처리량을 갖춘 부하 분산된 계산 및 메모리가 필요한 대부분의 비즈니스 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-134">The **General Purpose** tier is ideal for most business workloads requiring balanced compute and memory with scalable I/O throughput.</span></span> <span data-ttu-id="afa6d-135">이 계층에서 액세스 할 수 있는 하드웨어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-135">In this tier, you have access to the following hardware:</span></span>

- <span data-ttu-id="afa6d-136">계산 4세대 CPU(Intel E5-2673 v3 (Haswell) 2.4GHz 프로세서 기반, 2, 4, 8, 18, 32개의 vCore 구성으로 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="afa6d-136">Compute Gen 4 CPUs base on Intel E5-2673 v3 (Haswell) 2.4-GHz processors available in 2, 4, 8, 18, 32 vCore configurations</span></span>
- <span data-ttu-id="afa6d-137">계산 5세대 CPU(Intel E5-2673 v4 (Broadwell) 2.3GHz 프로세서 기반, 2, 4, 8, 18, 32개의 vCore 구성으로 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="afa6d-137">Compute Gen 5 CPUs base on Intel E5-2673 v4 (Broadwell) 2.3-GHz processors available in 2, 4, 8, 18, 32 vCore configurations</span></span>
- <span data-ttu-id="afa6d-138">저장소(최대 4TB)</span><span class="sxs-lookup"><span data-stu-id="afa6d-138">Storage up to 4 TB</span></span>
- <span data-ttu-id="afa6d-139">로컬 중복 백업</span><span class="sxs-lookup"><span data-stu-id="afa6d-139">Locally redundant backup</span></span>
- <span data-ttu-id="afa6d-140">지역 중복 백업</span><span class="sxs-lookup"><span data-stu-id="afa6d-140">Geographically redundant backup</span></span>

### <a name="memory-optimized"></a><span data-ttu-id="afa6d-141">메모리 최적화</span><span class="sxs-lookup"><span data-stu-id="afa6d-141">Memory Optimized</span></span>

<span data-ttu-id="afa6d-142">**메모리 최적화** 계층은 빠른 트랜잭션 처리와 높은 동시성을 위해 메모리 내 성능이 필요한 고성능 데이터베이스 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-142">The **Memory Optimized** tier is ideal for high-performance database workloads requiring in-memory performance for faster transaction processing and higher concurrency.</span></span> <span data-ttu-id="afa6d-143">이 계층에서 액세스 할 수 있는 하드웨어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-143">In this tier, you have access to the following hardware:</span></span>

- <span data-ttu-id="afa6d-144">계산 5세대 CPU(Intel E5-2673 v4 (Broadwell) 2.3GHz 프로세서 기반, 2, 4, 8, 16개의 vCore 구성으로 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="afa6d-144">Compute Gen 5 CPUs base on Intel E5-2673 v4 (Broadwell) 2.3-GHz processors available in 2, 4, 8, 16 vCore configurations</span></span>
- <span data-ttu-id="afa6d-145">저장소(최대 4TB)</span><span class="sxs-lookup"><span data-stu-id="afa6d-145">Storage up to 4 TB</span></span>
- <span data-ttu-id="afa6d-146">로컬 중복 백업</span><span class="sxs-lookup"><span data-stu-id="afa6d-146">Locally redundant backup</span></span>
- <span data-ttu-id="afa6d-147">지역 중복 백업</span><span class="sxs-lookup"><span data-stu-id="afa6d-147">Geographically redundant backup</span></span>

## <a name="steps-to-create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="afa6d-148">Azure Database for PostgreSQL 서버를 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="afa6d-148">Steps to create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="afa6d-149">일반적으로 Azure Portal을 사용하여 Azure Database for PostgreSQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-149">You'll typically create an Azure Database for PostgreSQL server using the Azure portal.</span></span> <span data-ttu-id="afa6d-150">수행할 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-150">Let's look at the steps you'll take.</span></span>

<span data-ttu-id="afa6d-151">먼저 Azure Portal에 로그인한 다음, **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-151">First you'll sign into the Azure portal, and then you'll click **Create a resource**.</span></span>

<span data-ttu-id="afa6d-152">**데이터베이스**와 **Azure Database for PostgreSQL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-152">You'll select **Databases** and **Azure Database for PostgreSQL**.</span></span> <span data-ttu-id="afa6d-153">[검색] 기능을 사용하여 이 범주를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-153">You can also use the Search functionality to find this category.</span></span>

<span data-ttu-id="afa6d-154">포털에는 선택 작업을 수행할 수 있는 PostgreSQL 서버 구성 화면(블레이드라고도 함)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-154">The portal will display a PostgreSQL server configuration screen, also called a blade, you make your selection.</span></span>

![Azure Portal - PostgreSQL 서버 만들기 사용자 인터페이스 블레이드](../media-draft/4-create-blade.png)

<span data-ttu-id="afa6d-156">블레이드의 모든 항목에 값을 제공해야 하므로 각 항목에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-156">You'll need to give a value to all the items in the blade, so let's have a look at each.</span></span>

### <a name="server-name"></a><span data-ttu-id="afa6d-157">서버 이름</span><span class="sxs-lookup"><span data-stu-id="afa6d-157">Server name</span></span>

<span data-ttu-id="afa6d-158">앞에서 설명한 대로 서버 리소스를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="afa6d-158">Recall, earlier we mentioned that you'll create a server resource.</span></span> <span data-ttu-id="afa6d-159">서버 이름은 이 리소스를 지정하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-159">The server name is the item that specifies this resource.</span></span> <span data-ttu-id="afa6d-160">결과적으로 서버에 대한 고유한 이름을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-160">As a result, you'll have to choose a unique name for the server.</span></span> <span data-ttu-id="afa6d-161">서버 이름은 모두 소문자여야 하며, 숫자와 하이픈을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-161">The server name must be all lowercase and can have numbers and hyphens.</span></span>

<span data-ttu-id="afa6d-162">_Adventure Works 추적_ 서버의 이름을 지정한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-162">Let's say you want to name the server _Adventure Works Tracking_.</span></span> <span data-ttu-id="afa6d-163">그러면 이름을 ```adventure-works-tracking```으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-163">You would then set up the name as ```adventure-works-tracking```.</span></span> <span data-ttu-id="afa6d-164">이미 있는 동일한 이름의 서버를 만들려고 하면 해당 결과에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-164">If you try to create a server with the same name that already exists, you'll get an error to that effect.</span></span>

### <a name="subscription"></a><span data-ttu-id="afa6d-165">구독</span><span class="sxs-lookup"><span data-stu-id="afa6d-165">Subscription</span></span>

<span data-ttu-id="afa6d-166">구독 필드는 요금 청구에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-166">The subscription field is used for billing.</span></span> <span data-ttu-id="afa6d-167">사용할 수 있는 구독이 둘 이상 있는 경우 특정 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-167">You'll pick a specific subscription in case you have more than one subscription available.</span></span>

### <a name="resource-group"></a><span data-ttu-id="afa6d-168">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="afa6d-168">Resource group</span></span>

<span data-ttu-id="afa6d-169">서버와 관련된 모든 리소스를 관리하려면 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-169">You'll use a resource group to manage all the resources related to your server.</span></span> <span data-ttu-id="afa6d-170">새 리소스 그룹을 만들거나 기존 리소스 그룹을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-170">You can create a new resource group or reuse an existing resource group.</span></span>

### <a name="source"></a><span data-ttu-id="afa6d-171">원본</span><span class="sxs-lookup"><span data-stu-id="afa6d-171">Source</span></span>

<span data-ttu-id="afa6d-172">서버는 _비어 있음_ 기본 옵션을 선택하거나 기존 백업에서 처음부터 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-172">You can create a server either from scratch by choosing the _Blank_ default option or from an existing backup.</span></span> <span data-ttu-id="afa6d-173">[백업] 옵션을 사용하면 기존 Azure Database for PostgreSQL 서버의 지역 백업을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-173">The Backup option will give the opportunity restore a geo-backup of an existing Azure Database for PostgreSQL server.</span></span>

### <a name="server-admin-login-name"></a><span data-ttu-id="afa6d-174">서버 관리자 로그인 이름</span><span class="sxs-lookup"><span data-stu-id="afa6d-174">Server admin login name</span></span>

<span data-ttu-id="afa6d-175">서버 관리자 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-175">You create the server admin user.</span></span> <span data-ttu-id="afa6d-176">새 서버에 대한 관리자 로그인으로 사용할 로그인 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-176">Choose a login name to use as an administrator login for the new server.</span></span> <span data-ttu-id="afa6d-177">관리자 로그인 이름은 azure_superuser, azure_pg_admin, admin, administrator, root, guest 또는 public이 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-177">The admin login name can't be azure_superuser, azure_pg_admin, admin, administrator, root, guest, or public.</span></span> <span data-ttu-id="afa6d-178">pg_로 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-178">It can't start with pg_.</span></span> <span data-ttu-id="afa6d-179">나중에 사용하기 위해 이 이름을 기억하거나 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="afa6d-179">Remember or write down this name for future use.</span></span>

### <a name="password"></a><span data-ttu-id="afa6d-180">암호</span><span class="sxs-lookup"><span data-stu-id="afa6d-180">Password</span></span>

<span data-ttu-id="afa6d-181">위의 관리자 로그인 이름과 함께 사용할 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-181">You choose a password to use with the above administrator login name.</span></span> <span data-ttu-id="afa6d-182">암호에는 영어 대문자, 영어 소문자, 숫자(0-9) 및 영숫자가 아닌 문자(!, $, #, % 등)의 세 가지 범주에 속한 문자가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-182">Your password must include characters from three of the following categories: English uppercase letters, English lowercase letters, numbers (0 through 9), and non-alphanumeric characters (!, $, #, %, etc.).</span></span> <span data-ttu-id="afa6d-183">나중에 사용하기 위해 이 암호를 기억하거나 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="afa6d-183">Remember or write down this password for future use.</span></span>

### <a name="confirm-password"></a><span data-ttu-id="afa6d-184">암호 확인</span><span class="sxs-lookup"><span data-stu-id="afa6d-184">Confirm password</span></span>

<span data-ttu-id="afa6d-185">확인을 위해 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-185">Retype the password as confirmation.</span></span>

### <a name="location"></a><span data-ttu-id="afa6d-186">위치</span><span class="sxs-lookup"><span data-stu-id="afa6d-186">Location</span></span>

<span data-ttu-id="afa6d-187">위치 옵션을 사용하면 서버가 물리적으로 만들어지는 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-187">The location option allows you to specify where the server is created physically.</span></span> <span data-ttu-id="afa6d-188">사용자에게 가장 가까운 지리적 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-188">Choose the geographical location closest to you.</span></span> <span data-ttu-id="afa6d-189">실제 시나리오에서 위치는 대다수의 사용자에게 가장 가까운 위치여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-189">In a real-world scenario, the location should be the location closest to the majority of your users.</span></span>

### <a name="version"></a><span data-ttu-id="afa6d-190">버전</span><span class="sxs-lookup"><span data-stu-id="afa6d-190">Version</span></span>

<span data-ttu-id="afa6d-191">사용할 PostgreSQL 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-191">You can specify the version of PostgreSQL to use.</span></span> <span data-ttu-id="afa6d-192">Microsoft는 PostgreSQL의 현재 버전과 두 개의 이전 버전을 지원하는 것을 목표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-192">Microsoft aims to support the current version and two previous versions of PostgreSQL.</span></span> <span data-ttu-id="afa6d-193">그러면 프로덕션 환경에 맞는 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-193">You'll choose a version that matches your production environment.</span></span>

> [!NOTE]
> <span data-ttu-id="afa6d-194">자세한 내용은 다음 자료를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa6d-194">For more information, see the following sources:</span></span>
> - [<span data-ttu-id="afa6d-195">지원되는 PostgreSQL 데이터베이스 버전</span><span class="sxs-lookup"><span data-stu-id="afa6d-195">Supported PostgreSQL Database Versions</span></span>](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions)
> - [<span data-ttu-id="afa6d-196">버전 관리 정책</span><span class="sxs-lookup"><span data-stu-id="afa6d-196">Versioning Policy</span></span>](https://www.postgresql.org/support/versioning/)

### <a name="pricing-tier"></a><span data-ttu-id="afa6d-197">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="afa6d-197">Pricing tier</span></span>

<span data-ttu-id="afa6d-198">서버의 워크로드를 지원하는 가격 책정 계층을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-198">You'll choose a pricing tier that will support your server's workload.</span></span> <span data-ttu-id="afa6d-199">세 가지 계층 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-199">Recall, you have three tiers to choose from.</span></span> <span data-ttu-id="afa6d-200">앞에서 살펴본 대로 이러한 계층 각각에서는 계산 및 저장소 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-200">As we saw earlier, each of these tiers allows you to configure the compute and storage options.</span></span> <span data-ttu-id="afa6d-201">예를 들어 다음은 5세대 계산 및 25일 백업 보존 기간을 갖춘 기본 가격 계층을 선택한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-201">For example, here is an example with the Basic price tier selected, a Gen 5 compute and a 25-day backup retention period.</span></span>

![가격 책정 계층](../media-draft/4-azure-db-pricing-tier.png)

<span data-ttu-id="afa6d-203">이제 입력한 값을 검토하고, 나중에 필요할 수 있는 메모를 작성하고, 만들기 단추를 클릭하여 서버를 만드는 것만 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-203">All that is left now is to review the values you entered, make any notes you may need for later, and click the create button to create the server.</span></span>

<span data-ttu-id="afa6d-204">서버를 배포하는 데는 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-204">Deploying the server takes a couple of minutes.</span></span> <span data-ttu-id="afa6d-205">배포가 완료되면 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-205">You'll receive a notification when the deployment is complete.</span></span> <span data-ttu-id="afa6d-206">알림에서 새로 만든 서버로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-206">From the notification, you can navigate to the newly created server.</span></span>

<span data-ttu-id="afa6d-207">이제까지 Azure Database for PostgreSQL을 만드는 데 필요한 단계를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-207">You've now seen the steps you take to create an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="afa6d-208">다음 단원에서는 사용자 고유의 Azure Database for PostgreSQL 서버를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6d-208">In the next unit, you'll have to opportunity to create your own Azure Database for PostgreSQL server.</span></span>
