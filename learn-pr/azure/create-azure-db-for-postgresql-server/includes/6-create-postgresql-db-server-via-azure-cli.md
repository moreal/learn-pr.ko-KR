<span data-ttu-id="e62a0-101">Azure Database for PostgreSQL을 만들어 주자의 체력 장치에서 캡처된 경로를 저장하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-101">You decide to create an Azure Database for PostgreSQL to store routes captured from runners' fitness devices.</span></span> <span data-ttu-id="e62a0-102">기록이 캡처되는 데이터 볼륨에 따라 서버 저장소 요구 사항을 20GB로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-102">Based on historic captured data volumes, you know your server storage requirements should be set at 20 GB.</span></span> <span data-ttu-id="e62a0-103">처리 요구 사항을 지원하려면 1개 vCore를 갖춘 5세대 계산을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-103">To support your processing requirements, you need compute Gen 5 support with 1 vCore.</span></span> <span data-ttu-id="e62a0-104">또한 데이터 백업에는 15일의 보존 기간이 필요하다는 것도 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-104">You also know that you require a retention period of 15 days for data backups.</span></span>

> [!TIP]
> <span data-ttu-id="e62a0-105">Microsoft Learn에서 수행하는 모든 연습에는 추가 비용이 들지 않지만, 직접 탐색을 시작하면 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-105">All of the exercises you do in Microsoft Learn are free, but once you start exploring on your own, you will need an Azure subscription.</span></span> <span data-ttu-id="e62a0-106">아직 구독이 없는 경우 몇 분 정도 시간을 내어 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-106">If you don't have one yet, take a couple of minutes and create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="e62a0-107">시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-107">Let's begin.</span></span>

<span data-ttu-id="e62a0-108">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-108">Sign in to [the Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

<span data-ttu-id="e62a0-109">Azure Cloud Shell 세션을 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-109">Recall that you'll need to start an Azure Cloud Shell session.</span></span> <span data-ttu-id="e62a0-110">화면 위쪽에 있는 Cloud Shell 아이콘을 선택하여 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-110">Select the Cloud Shell icon at the top of the screen to start the session.</span></span>

![Cloud Shell 단추](../media-draft/cloud-shell-button.png)

<span data-ttu-id="e62a0-112">Cloud Shell에서 사용할 저장소 계정이 아직 없으면 첫 번째 액세스 권한으로 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-112">If you don't already have a storage account to use with Cloud Shell, you'll need to create one with first access.</span></span> <span data-ttu-id="e62a0-113">포털 인터페이스에서 저장소 계정을 만드는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-113">The portal interface will step you through the process of creating a storage account.</span></span>

<span data-ttu-id="e62a0-114">이 랩에서는 `bash`를 명령줄 환경으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-114">This lab uses `bash` as the command-line environment.</span></span>

1. <span data-ttu-id="e62a0-115">서버를 만드는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-115">Select the subscription you'll use to create the server.</span></span>

    <span data-ttu-id="e62a0-116">구독이 여러 개 있는 경우 다음 명령을 사용하여 해당 구독을 활성화하여 0을 사용자의 구독 식별자로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-116">If you have several subscriptions, make sure you activate the appropriate subscription with the following command, replacing the zeros with your subscription identifier.</span></span>

    ``` bash
    az account set --subscription "00000000-0000-0000-0000-000000000000"
    ```

    <span data-ttu-id="e62a0-117">`az account list --output table` 명령을 사용하여 모든 구독을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-117">Recall, you can list all your subscriptions using the `az account list --output table` command.</span></span> <span data-ttu-id="e62a0-118">이 목록에서 사용하려는 구독 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-118">Pick the subscription identifier from this list that you'd like to use.</span></span>

1. <span data-ttu-id="e62a0-119">이전 단원에서 리소스 그룹을 아직 만들지 않았으면 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-119">If you haven't already done so in a previous unit, create a resource group.</span></span> <span data-ttu-id="e62a0-120">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-120">You'll run the following command.</span></span>

    ```bash
    az group create --name <resource_group_name> --location <location>
    ```

    > [!Note]
    > <span data-ttu-id="e62a0-121">`az account list-locations` 명령을 사용하여 모든 위치에 대한 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-121">You can retrieve a list of all locations using this command `az account list-locations`.</span></span> <span data-ttu-id="e62a0-122">`displayName` 또는 `name` 값을 선택하고, `<location>` 매개 변수에 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-122">Select the `displayName` or `name` value and use it for the `<location>` parameter.</span></span>

1. <span data-ttu-id="e62a0-123">이제 `az postgres server create` 명령을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-123">You're now ready to run the `az postgres server create` command.</span></span>

    <span data-ttu-id="e62a0-124">서버 저장소 크기를 20GB로 설정하고, 1개의 vCore 및 15일의 데이터 백업 보존 기간을 갖춘 계산 5세대를 지원하려고 한다는 것을 명심하세요.</span><span class="sxs-lookup"><span data-stu-id="e62a0-124">Keep in mind you want to set your server storage size at 20 GB, compute Gen 5 support with 1 vCore and a retention period of 15 days for data backups.</span></span>

    <span data-ttu-id="e62a0-125">지정할 몇 가지 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-125">There are several parameters that you'll specify:</span></span>

    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`

    <span data-ttu-id="e62a0-126">아래의 솔루션을 살펴보지 않고도 명령을 작성하고 매개 변수를 완성할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-126">See if you can write the command and complete the parameters without looking at the solution below.</span></span> <span data-ttu-id="e62a0-127">`<>`의 값을 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-127">Replace the values in `<>` with your own values.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e62a0-128">`az account list-locations` 명령을 사용하여 모든 위치에 대한 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-128">You can retrieve a list of all locations using this command `az account list-locations`.</span></span> <span data-ttu-id="e62a0-129">`displayName` 또는 `name` 값을 선택하고, `<location>` 매개 변수에 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-129">Select the `displayName` or `name` value and use it for the `<location>` parameter.</span></span>

    ```bash
    az postgres server create --resource-group <resource_group_name> --name <unique_server_name>  --location "UK West" --admin-user <server_admin_login_id> --admin-password <server_admin_password> --sku-name B_Gen5_1 --storage-size 20480 --backup-retention 15 --version 10
    ```

<span data-ttu-id="e62a0-130">실행되면 시스템에서 정보를 처리하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-130">You'll see the system take a few moments to process the information when executed.</span></span> <span data-ttu-id="e62a0-131">서버가 만들어진 경우 해당 서버를 설명하는 JSON(Java Script Object Notation) 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-131">A Java Script Object Notation (JSON) string that describes the server is returned if the server was created.</span></span> <span data-ttu-id="e62a0-132">서버가 만들어지지 않은 경우 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-132">An error message is displayed if the server isn't created.</span></span> <span data-ttu-id="e62a0-133">이 오류 정보를 사용하여 명령 매개 변수를 검토하고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-133">You'll use this error information to review and fix your command parameters.</span></span>

<span data-ttu-id="e62a0-134">Azure CLI를 사용하여 PostgreSQL 서버를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-134">You've successfully created a PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="e62a0-135">다음 단원에서는 서버의 보안 설정을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e62a0-135">In the next unit, you'll see how to configure your server's security settings.</span></span>
