<span data-ttu-id="b9f82-101">온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-101">Let's assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="b9f82-102">현재 회사에서 서버를 Azure로 이동하여 장치 지원, 가용성, 데이터 추적 및 처리 기능을 확장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-102">Your company is now looking at expanding device support, availability, data tracking, and processing features by moving your server into Azure.</span></span> <span data-ttu-id="b9f82-103">Azure Database for PostgreSQL 서버의 생성을 자동화하려면 얼마나 많은 노력이 필요한지 조사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-103">You'll investigate how much effort it takes to automate the creation of an Azure Database for PostgreSQL server.</span></span>

<span data-ttu-id="b9f82-104">Azure Portal을 사용하여 단일 Azure Database for PostgreSQL 서버를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-104">Creating a single Azure Database for PostgreSQL server using the Azure portal is easy.</span></span> <span data-ttu-id="b9f82-105">포털만 사용하여 데이터베이스를 두 개 이상 만들고 유지 관리를 지속적으로 실행하는 것은 지루한 일이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-105">Creating more than one database and running on-going maintenance using only the portal may become tedious.</span></span> <span data-ttu-id="b9f82-106">관리 작업을 자동화하려는 경우 Azure CLI를 사용하여 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-106">You'll use the Azure CLI to create scripts when you want to automate management tasks.</span></span>

<span data-ttu-id="b9f82-107">Azure CLI를 사용하여 Microsoft Azure 내에서 거의 모든 리소스 생성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-107">Creating almost any resource within Microsoft Azure can be automated using the Azure CLI.</span></span> <span data-ttu-id="b9f82-108">이 단원에서는 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버 관리를 자동화하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-108">In this unit, you'll learn how to automate management of your Azure Database for PostgreSQL servers using the Azure CLI.</span></span>

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="b9f82-109">Azure CLI란?</span><span class="sxs-lookup"><span data-stu-id="b9f82-109">What is the Azure CLI?</span></span>

<span data-ttu-id="b9f82-110">[Azure CLI](https://docs.microsoft.com/cli/azure/)는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-110">The [Azure CLI](https://docs.microsoft.com/cli/azure/) is Microsoft’s cross-platform command-line environment for managing Azure resources.</span></span> <span data-ttu-id="b9f82-111">브라우저에서 Azure Cloud Shell을 통해 Azure CLI를 사용할 수도 있고 Mac OS X, Linux 또는 Windows에 로컬로 Azure CLI를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-111">You can use the Azure CLI from your browser with Azure Cloud Shell, or you can install the Azure CLI locally on Mac OS X, Linux, or Windows.</span></span> <span data-ttu-id="b9f82-112">Azure CLI는 bash 또는 PowerShell을 사용하여 로컬 명령줄에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-112">The Azure CLI is run from a local command line using bash or PowerShell.</span></span> <span data-ttu-id="b9f82-113">Azure CLI를 로컬로 실행하려면 추가 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-113">Running the Azure CLI locally requires additional setup.</span></span> <span data-ttu-id="b9f82-114">여기서는 Azure Cloud Shell을 사용하여 Azure CLI 명령을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-114">We'll use Azure Cloud Shell for executing the Azure CLI commands.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="b9f82-115">Azure Cloud Shell이란?</span><span class="sxs-lookup"><span data-stu-id="b9f82-115">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="b9f82-116">Azure Cloud Shell은 클라우드에 호스트되는 브라우저 기반 셸 환경으로, 인증된 세션을 사용하여 Azure에 연결할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-116">Azure Cloud Shell is a browser-based shell experience that's hosted in the cloud and allows you to connect to Azure using an authenticated session.</span></span> <span data-ttu-id="b9f82-117">Azure CLI 명령을 실행하여 Azure Database for PostgreSQL 서버 관리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-117">You can execute the Azure CLI commands to automate the management of an Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="b9f82-118">계정에서 사용할 수 있도록 공용 Azure CLI 도구가 Cloud Shell에 사전 설치 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-118">Common Azure CLI tools are pre-installed and configured in Cloud Shell for you to use with your account.</span></span>

> [!NOTE]
> <span data-ttu-id="b9f82-119">Cloud Shell은 Cloud Shell에서 작업하는 동안 만든 파일을 유지하려면 Azure 저장소 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-119">Cloud Shell requires an Azure storage resource to persist any files you create while working in Cloud Shell.</span></span> <span data-ttu-id="b9f82-120">처음 시작하면 Cloud Shell은 사용자를 대신하여 리소스 그룹, 저장소 계정 및 Azure Files 공유를 만들라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-120">On first launch, Cloud Shell prompts to create a resource group, storage account, and Azure Files share on your behalf.</span></span> <span data-ttu-id="b9f82-121">이는 일회성 단계이며 이후의 모든 Cloud Shell 세션에 대해 자동으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-121">This is a one-time step and will be automatically attached for all future Cloud Shell sessions.</span></span>

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a><span data-ttu-id="b9f82-122">Azure CLI를 사용하여 Azure Database for PostgreSQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b9f82-122">Create an Azure Database for PostgreSQL server using the Azure CLI</span></span>

<span data-ttu-id="b9f82-123">오른쪽에 있는 Azure Cloud Shell 터미널을 사용하여 Azure CLI를 통해 Azure Database for PostgreSQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-123">You'll use the Azure Cloud Shell terminal on the right to create an Azure Database for PostgreSQL server using Azure CLI.</span></span>

<span data-ttu-id="b9f82-124">사용 가능한 모든 매개 변수를 보여 주는 Azure CLI 서버 만들기 명령 사용 도움말은 다음 예제와 같이 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-124">The Azure CLI server creation command usage help showing all available parameters looks like the following example:</span></span>

```azurecli
az postgres server create [-h] [--verbose] [--debug]
                            [--output {json,jsonc,table,tsv}]
                            [--query JMESPATH]
                            --resource-group RESOURCE_GROUP_NAME --name SERVER_NAME
                            --sku-name SKU_NAME [--location LOCATION]
                            --admin-user ADMINISTRATOR_LOGIN
                            [--admin-password ADMINISTRATOR_LOGIN_PASSWORD]
                            [--backup-retention BACKUP_RETENTION]
                            [--geo-redundant-backup GEO_REDUNDANT_BACKUP]
                            [--ssl-enforcement {Enabled,Disabled}]
                            [--storage-size STORAGE_MB]
                            [--tags [TAGS [TAGS ...]]]
                            [--version VERSION]
                            [--subscription _SUBSCRIPTION]

```

<span data-ttu-id="b9f82-125">선택적 매개 변수는 대괄호로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-125">The optional parameters are surrounded in brackets.</span></span> <span data-ttu-id="b9f82-126">몇 가지 일반적인 것들을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-126">Let's examine a few of the common ones.</span></span>

### <a name="parameters"></a><span data-ttu-id="b9f82-127">매개 변수</span><span class="sxs-lookup"><span data-stu-id="b9f82-127">Parameters</span></span>

<span data-ttu-id="b9f82-128">`--resource-group <resource_group_name>` 매개 변수는 서버를 만들 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-128">The `--resource-group <resource_group_name>` parameter specifies the resource group within which to create the server.</span></span>

<span data-ttu-id="b9f82-129">여러분이 지정하는 서버 `admin-user` 및 `admin-password`는 서버와 데이터베이스에 로그인하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-129">The server `admin-user` and `admin-password` that you specify is required to sign in to the server and its databases.</span></span> <span data-ttu-id="b9f82-130">나중에 새 서버와 상호 작용할 때 이 정보를 기억하거나 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="b9f82-130">Remember or record this information for later when interacting with the new server.</span></span>

<span data-ttu-id="b9f82-131">`--sku-name` 매개 변수를 사용하여 가격 책정 계층의 일부(이 경우 계산 리소스)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-131">You use the `--sku-name` parameter to specify part of the pricing tier, in this case, compute resource.</span></span> <span data-ttu-id="b9f82-132">값은 `{pricing tier}_{compute generation}_{vCores}` 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-132">The value follows the convention `{pricing tier}_{compute generation}_{vCores}`.</span></span>

<span data-ttu-id="b9f82-133">예제:</span><span class="sxs-lookup"><span data-stu-id="b9f82-133">Examples:</span></span>

- <span data-ttu-id="b9f82-134">`--sku-name B_Gen4_4`는 기본, 4세대 및 vCore 4개에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-134">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span></span>
- <span data-ttu-id="b9f82-135">`--sku-name GP_Gen5_32`는 범용, 5세대 및 vCore 32개에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-135">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span></span>
- <span data-ttu-id="b9f82-136">`--sku-name MO_Gen5_2`는 메모리 최적화, 5세대 및 2 vCore에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-136">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span></span>

<span data-ttu-id="b9f82-137">포털을 사용하여 서버를 만드는 단원에서 세 가지 가격 책정 계층에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-137">Recall that we discussed the three pricing tiers in the unit where we created the server using the portal.</span></span>

<span data-ttu-id="b9f82-138">기본, 5세대, 1 vCore 계산 리소스를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-138">Let's assume you want to use a Basic, Gen 5, and 1 vCore compute resource.</span></span> <span data-ttu-id="b9f82-139">매개 변수를 `--sku-name B_Gen5_1`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-139">You'll specify the parameter as `--sku-name B_Gen5_1`.</span></span>

<span data-ttu-id="b9f82-140">`--storage-size` 매개 변수를 사용하여 가격 책정 계층의 일부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-140">You use the `--storage-size` parameter to specify part of the pricing tier.</span></span> <span data-ttu-id="b9f82-141">값을 지정하지 않으면 기본값은 5,120MB입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-141">If the value isn't specified, then it defaults to 5,120 MB.</span></span> <span data-ttu-id="b9f82-142">유효한 저장소 크기 범위는 5,120MB부터 1,024MB 단위로 증가하여 1,048,576MB까지 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-142">Valid storage sizes range from 5,120 MB and increases in increments of 1,024 MB up to 1,048,576 MB.</span></span>

<span data-ttu-id="b9f82-143">`--backup-retention` 매개 변수는 일 단위로 지정된 백업 보존 기간을 지정해야 할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-143">The `--backup-retention` parameter is used when you need to specify the retention period for backups, which is specified in days.</span></span> <span data-ttu-id="b9f82-144">값을 지정하지 않으면 기본값은 7일입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-144">If the value isn't specified, then it defaults to seven days.</span></span>

<span data-ttu-id="b9f82-145">`--version` 매개 변수를 통해 사용하려는 PostgreSQL의 주 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-145">You use the `--version` parameter to specify the major version of PostgreSQL that you'd like to use.</span></span>

<span data-ttu-id="b9f82-146">이제 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버를 만드는 단계를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-146">You've now seen the steps to create an Azure Database for PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="b9f82-147">다음 단원에서는 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f82-147">In the next unit, you'll create an Azure Database for PostgreSQL server using the Azure CLI.</span></span>