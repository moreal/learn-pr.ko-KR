<span data-ttu-id="a82cf-101">온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-101">Let's assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="a82cf-102">현재 회사에서 서버를 Azure로 이동하여 장치 지원, 가용성, 데이터 추적 및 처리 기능을 확장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-102">Your company is now looking at expanding device support, availability, data tracking, and processing features by moving your server into Azure.</span></span> <span data-ttu-id="a82cf-103">여러분은 Azure Database for PostgreSQL 생성을 자동화하려면 얼마나 많은 노력이 필요한지 조사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-103">You'll investigate how much effort it takes to automate the creation of an Azure Database for PostgreSQL.</span></span>

<span data-ttu-id="a82cf-104">Azure Portal을 사용하여 단일 Azure Database for PostgreSQL를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-104">Creating a single Azure Database for PostgreSQL server using the Azure portal is easy.</span></span> <span data-ttu-id="a82cf-105">포털만 사용하여 데이터베이스를 두 개 이상 만들고 유지 관리를 지속적으로 실행하는 것은 지루한 일이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-105">Creating more than one database and running ongoing maintenance using only the portal may become tedious.</span></span> <span data-ttu-id="a82cf-106">여러분은 관리 작업을 자동화할 때 Azure CLI를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-106">You'll use the Azure CLI to create scripts when you want to automate management tasks.</span></span>

<span data-ttu-id="a82cf-107">Azure CLI를 사용하여 Microsoft Azure 내에서 거의 모든 리소스 생성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-107">Creating almost any resource within Microsoft Azure can be automated using the Azure CLI.</span></span> <span data-ttu-id="a82cf-108">이 모듈에서는 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버 관리를 자동화하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-108">In this unit, you'll learn how to automate management of your Azure Database for PostgreSQL servers using the Azure CLI.</span></span>

## <a name="what-is-azure-cli"></a><span data-ttu-id="a82cf-109">Azure CLI란?</span><span class="sxs-lookup"><span data-stu-id="a82cf-109">What is Azure CLI?</span></span>

<span data-ttu-id="a82cf-110">[Azure CLI](https://docs.microsoft.com/cli/azure/)는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-110">[Azure CLI](https://docs.microsoft.com/cli/azure/) is Microsoft’s cross-platform command-line environment for managing Azure resources.</span></span> <span data-ttu-id="a82cf-111">브라우저에서 Azure Cloud Shell을 통해 Azure CLI를 사용할 수도 있고 Mac OS X, Linux 또는 Windows에 로컬로 Azure CLI를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-111">You can use the Azure CLI from your browser with Azure Cloud Shell, or you can install Azure CLI locally on Mac OS X, Linux, or Windows.</span></span> <span data-ttu-id="a82cf-112">Azure CLI는 bash 또는 Powershell을 사용하여 로컬 명령줄에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-112">The Azure CLI is run from a local command line using bash or Powershell.</span></span> <span data-ttu-id="a82cf-113">하지만 Azure CLI를 로컬로 실행하려면 추가 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-113">Running Azure CLI locally however requires additional setup.</span></span> <span data-ttu-id="a82cf-114">여기서는 Azure Cloud Shell을 사용하여 Azure CLI 명령을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-114">We'll use the Azure Cloud Shell for executing Azure CLI commands.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="a82cf-115">Azure Cloud Shell이란?</span><span class="sxs-lookup"><span data-stu-id="a82cf-115">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="a82cf-116">Azure Cloud Shell은 클라우드에 호스트되는 브라우저 기반 셸 환경으로, 인증된 세션을 사용하여 Azure에 연결할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-116">Azure Cloud Shell is a browser-based shell experience that is hosted in the cloud and allows you to connect to Azure using an authenticated session.</span></span> <span data-ttu-id="a82cf-117">Azure CLI 명령을 실행하여 Azure Database for PostgreSQL 관리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-117">You can execute Azure CLI commands to automate the management of an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a82cf-118">계정에서 사용할 수 있도록 공용 Azure CLI 도구가 Cloud Shell에 사전 설치 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-118">Common Azure CLI tools are pre-installed and configured in Cloud Shell for you to use with your account.</span></span>

> [!NOTE]
> <span data-ttu-id="a82cf-119">Cloud Shell에서 작업하는 동안 만든 파일을 유지하려면 Azure 저장소 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-119">Cloud Shell requires an Azure storage resource to persist any files you create while working in the Cloud Shell.</span></span> <span data-ttu-id="a82cf-120">Cloud Shell를 처음으로 실행하면 리소스 그룹, 저장소 계정 및 Azure Files 공유를 만들라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-120">On first launch Cloud Shell prompts to create a resource group, storage account, and Azure Files share on your behalf.</span></span> <span data-ttu-id="a82cf-121">이 단계는 한 번만 실행하면 다음부터 모든 세션에서 자동으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-121">This is a one-time step and will be automatically attached for all future Cloud Shell sessions.</span></span>

## <a name="create-an-azure-database-for-postgresql-server-using-azure-cli"></a><span data-ttu-id="a82cf-122">Azure CLI를 사용하여 Azure Database for PostgreSQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="a82cf-122">Create an Azure Database for PostgreSQL server using Azure CLI</span></span>

<span data-ttu-id="a82cf-123">Azure Cloud Shell을 사용하여 Azure CLI를 통해 Azure Database for PostgreSQL를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-123">You'll use Azure Cloud Shell to create an Azure Database for PostgreSQL server using Azure CLI.</span></span> <span data-ttu-id="a82cf-124">수행할 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-124">Let's look at the steps you'll take.</span></span>

<span data-ttu-id="a82cf-125">먼저 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-125">First, sign into the Azure portal.</span></span>

<span data-ttu-id="a82cf-126">Azure Portal에서 Cloud Shell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-126">Open the Cloud Shell from the Azure portal.</span></span> <span data-ttu-id="a82cf-127">브라우저를 열고 [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하여 [Cloud Shell 열기] 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-127">Open your browser and go to [Azure portal](https://portal.azure.com?azure-portal=true) and click the Open Cloud Shell button:</span></span>

![Cloud Shell 단추](../media-draft/cloud-shell-button.png)

<span data-ttu-id="a82cf-129">Cloud Shell을 사용하여 `bash` 또는 `PowerShell`에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-129">Cloud Shell allows you to run your commands either in `bash` or `PowerShell`.</span></span> <span data-ttu-id="a82cf-130">우리는 모든 예제에 `bash` 명령줄 옵션을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-130">We'll use the `bash` command-line option for all examples.</span></span>

<span data-ttu-id="a82cf-131">구독이 여러 개 있는 경우 다음 명령을 사용하여 해당 구독을 활성화하여 0을 사용자의 구독 식별자로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-131">If you have several subscriptions, make sure you activate the appropriate subscription with the following command, replacing the zeros with your subscription identifier.</span></span>

   ```bash
   az account set --subscription 00000000-0000-0000-0000-000000000000
   ```

<span data-ttu-id="a82cf-132">다음 명령을 실행하여 모든 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-132">You'll run the following command to list all your subscriptions.</span></span>

   ```bash
   az account list --output table
   ```

<span data-ttu-id="a82cf-133">그 다음 단계는 서버를 관리하고 리소스 그룹을 배치할 리소스 그룹을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-133">The next step is to create a resource group to manage the server and where the resource group will be located.</span></span> <span data-ttu-id="a82cf-134">리소스 그룹을 사용하여 서버와 관련된 모든 리소스를 관리할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-134">Recall, you'll use a resource group to manage all the resources related to your server.</span></span> <span data-ttu-id="a82cf-135">위치 옵션을 사용하면 서버가 물리적으로 만들어지는 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-135">The location option allows you to specify where the server is created physically.</span></span> <span data-ttu-id="a82cf-136">다음 명령을 실행하고 `<resource_group_name>` 및 `<location>`을 각각 적절한 값으로 바꿀 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-136">You'll run the next command and replace the `<resource_group_name>` and `<location>` respectively with appropriate values.</span></span>

   ```bash
   az group create --name <resourcegroup> --location <location>
   ```

<span data-ttu-id="a82cf-137">마지막 단계는 Azure Database for PostgreSQL 서버를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-137">The last step is to create the Azure Database for PostgreSQL server.</span></span>

   <span data-ttu-id="a82cf-138">사용 가능한 모든 매개 변수를 보여주는 Azure CLI 서버 만들기 명령 사용 도움말은 다음 예제처럼 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-138">The Azure CLI server creation command usage help showing all available parameters looks like the following example:</span></span>

   ```bash
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

   <span data-ttu-id="a82cf-139">다음 명령줄은 Azure Database for PostgreSQL 서버를 만드는 데 필요한 매개 변수 집합을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-139">The following command line shows the required set of parameters to create an Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="a82cf-140">일부 선택적 매개 변수는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-140">You'll notice some are optional parameters and aren't listed.</span></span>

   ```bash
   az postgres server create --resource-group <resource_group_name> --name <new_server_name> --admin-user <admin_user_name> --admin-password <server_admin_password> --sku-name <sku> --version <version_number>  --location <region_name> --storage-size <size> --backup-retention <days>
   ```

### <a name="parameter-descriptions"></a><span data-ttu-id="a82cf-141">매개 변수 설명</span><span class="sxs-lookup"><span data-stu-id="a82cf-141">Parameter descriptions</span></span>

<span data-ttu-id="a82cf-142">`--resource-group <resource_group_name>` 매개 변수는 서버를 만들 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-142">The `--resource-group <resource_group_name>` parameter specifies the resource group within which to create the server.</span></span>

<span data-ttu-id="a82cf-143">여러분이 지정하는 서버 `admin-user` 및 `admin-password`는 서버와 데이터베이스에 로그인하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-143">The server `admin-user` and `admin-password` that you specify is required to sign in to the server and its databases.</span></span> <span data-ttu-id="a82cf-144">나중에 새 서버와 상호 작용할 때 사용할 수 있도록 이 정보를 기억하거나 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="a82cf-144">Remember or record this information for later when interacting with the new server.</span></span>

<span data-ttu-id="a82cf-145">`--sku-name` 매개 변수는 가격 책정 계층의 일부(이 예에서는 계산 리소스)를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-145">You use the `--sku-name` parameter is used to specify part of the pricing tier, in this case compute resource.</span></span> <span data-ttu-id="a82cf-146">값은 `{pricing tier}_{compute generation}_{vCores}` 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-146">The value follows the convention `{pricing tier}_{compute generation}_{vCores}`.</span></span>

<span data-ttu-id="a82cf-147">예제:</span><span class="sxs-lookup"><span data-stu-id="a82cf-147">Examples:</span></span>

- <span data-ttu-id="a82cf-148">`--sku-name B_Gen4_4`는 기본, 4세대 및 vCore 4개에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-148">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span></span>
- <span data-ttu-id="a82cf-149">`--sku-name GP_Gen5_32`는 범용, 5세대 및 vCore 32개에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-149">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span></span>
- <span data-ttu-id="a82cf-150">`--sku-name MO_Gen5_2`는 메모리 최적화, 5세대 및 vCore 2개에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-150">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span></span>

<span data-ttu-id="a82cf-151">포털을 사용하여 서버를 만드는 모듈에서 세 가지 가격 책정 계층에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-151">Recall, we discussed the three pricing tiers in the unit where we create the server using the portal.</span></span>

<span data-ttu-id="a82cf-152">기본, 5세대, 1 vCore 계산 리소스를 사용한다고 가정하고, 매개 변수를 `--sku-name B_Gen5_1`으로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-152">Let's assume you want to use a Basic, Gen 5, and 1 vCore compute resource, you'll then specify the parameter as `--sku-name B_Gen5_1`.</span></span>

<span data-ttu-id="a82cf-153">또한 `--storage-size` 매개 변수를 사용하여 가격 책정 계층의 일부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-153">You use the `--storage-size` parameter is also used the specify part of the pricing tier.</span></span> <span data-ttu-id="a82cf-154">값을 지정하지 않으면 기본값 5,120MB가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-154">If the value isn't specified, then it defaults to 5,120 MB.</span></span> <span data-ttu-id="a82cf-155">유효한 저장소 크기 범위는 5,120MB부터 1,048,576MB까지이며 1,024MB 단위로 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-155">Valid storage sizes range from 5,120 MB and increases in additional increments of 1,024 MB up to 1,048,576 MB.</span></span>

<span data-ttu-id="a82cf-156">`--backup-retention` 매개 변수는 백업 보존 기간을 일 단위로 지정해야 할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-156">The `--backup-retention` parameter is used when you need to specify the retention period for backups specified in days.</span></span> <span data-ttu-id="a82cf-157">값을 지정하지 않으면 기본값 7일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-157">If the value isn't specified, then it defaults to seven days.</span></span>

<span data-ttu-id="a82cf-158">`--version` 매개 변수는 사용하려는 PostgreSQL의 주 버전을 지정하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-158">You use the `--version` parameter is used to specify the major version of PostgreSQL you would like to use.</span></span>

<span data-ttu-id="a82cf-159">Azure CLI를 사용하여 Azure Database for PostgreSQL을 만드는 단계를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-159">You've now seen the steps to create an Azure Database for PostgreSQL using Azure CLI.</span></span> <span data-ttu-id="a82cf-160">그 다음 모듈에서는 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a82cf-160">In the next unit, you'll create an Azure Database for PostgreSQL server using Azure CLI.</span></span>