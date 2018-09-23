<span data-ttu-id="e633e-101">Azure Portal을 사용하면 PostgreSQL 데이터베이스 서버를 관리하고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-101">The Azure portal allows you to manage and scale PostgreSQL database servers.</span></span> <span data-ttu-id="e633e-102">주자의 운동 능력 데이터를 저장하기 위해 Azure Database for PostgreSQL 서버를 만들기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-102">You decide to create an Azure Database for PostgreSQL server to store runner performance data.</span></span> <span data-ttu-id="e633e-103">기록이 캡처되는 데이터 볼륨에 따라 서버 저장소 요구 사항을 10GB로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-103">Based on historic captured data volumes, you know your server storage requirements should be set at 10 GB.</span></span> <span data-ttu-id="e633e-104">처리 요구 사항을 지원하려면 1개 vCore를 갖춘 5세대 계산을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-104">To support your processing requirements, you need compute Gen 5 support with 1 vCore.</span></span> <span data-ttu-id="e633e-105">또한 일반적으로 25일 동안 백업을 저장한다는 것도 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-105">You also know that you typically store backups for 25 days.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="e633e-106">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-106">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span> 

<span data-ttu-id="e633e-107">Azure 리소스 만들기 및 관리 메뉴가 왼쪽에 표시되고, 나머지 화면에는 대시보드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-107">You'll see the Azure resource creation and management menu on your left and the dashboard filling the rest of the screen.</span></span>

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="e633e-108">Azure Database for PostgreSQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="e633e-108">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="e633e-109">로그인한 후에 기본 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-109">After you sign in, you'll see the default Dashboard displayed.</span></span> <span data-ttu-id="e633e-110">Azure Database for PostgreSQL 서버를 만드는 데 사용할 수 있는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-110">You have a couple of options available to you to create an Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="e633e-111">대시보드에서 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-111">From the Dashboard, you can either:</span></span>

- <span data-ttu-id="e633e-112">**모든 서비스** 옵션을 선택한 다음, **Azure Database for PostgreSQL 서버**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-112">Select the **All services** option and then search for **Azure Database for PostgreSQL server**.</span></span> <span data-ttu-id="e633e-113">이 화면에는 이미 계정에 구성되어 있는 모든 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-113">This screen will display any configured servers that are already in your account.</span></span> <span data-ttu-id="e633e-114">여기서 **추가**를 선택하면 새 서버 만들기 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-114">From here, you select **Add**, which will take you to the new server creation blade.</span></span>

<span data-ttu-id="e633e-115">**or**</span><span class="sxs-lookup"><span data-stu-id="e633e-115">**or**</span></span>

- <span data-ttu-id="e633e-116">**리소스 만들기** 옵션을 선택하면 Azure Marketplace 리소스 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-116">Select the **Create a resource** option, which will present you with Azure Marketplace resource options.</span></span> <span data-ttu-id="e633e-117">여기서 **데이터베이스** 옵션 및 **Azure Database for PostgreSQL**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-117">From here, you select the **Databases** option and choose **Azure Database for PostgreSQL**.</span></span>

### <a name="configure-the-server"></a><span data-ttu-id="e633e-118">서버 구성</span><span class="sxs-lookup"><span data-stu-id="e633e-118">Configure the server</span></span>

<span data-ttu-id="e633e-119">이제 다음 일러스트레이션과 비슷한 PostgreSQL 서버 만들기 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-119">You'll now see the PostgreSQL server create blade, similar to the following illustration.</span></span>

![새 PostgreSQL 데이터베이스의 생성 블레이드를 보여주는 Azure Portal의 스크린샷](../media/4-create-blade.png)

> [!NOTE]
> <span data-ttu-id="e633e-121">PostgreSQL 서버를 만들 때 몇 가지 세부 정보를 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-121">You'll need to remember some details as you create the PostgreSQL server.</span></span> <span data-ttu-id="e633e-122">예를 들어 서버에 액세스하는 데 필요한 사용자 이름과 암호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-122">For example, the username and password to access the server.</span></span> <span data-ttu-id="e633e-123">나중에 이 정보를 사용하여 서버에 연결하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-123">You'll use this information to connect to your server later.</span></span>

1. <span data-ttu-id="e633e-124">서버에 대한 고유한 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-124">Choose a unique name for the server.</span></span> <span data-ttu-id="e633e-125">이름은 모두 소문자여야 하며, 숫자와 하이픈을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-125">Recall that then name must be all lowercase and can have numbers and hyphens.</span></span>

1. <span data-ttu-id="e633e-126">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-126">Select a subscription.</span></span> <span data-ttu-id="e633e-127">이 필드가 사용할 구독으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-127">Check to be sure this field is set to the subscription that you want to use.</span></span>

1. <span data-ttu-id="e633e-128">이제 새 리소스를 만들거나 기존 리소스 그룹을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-128">You now have the option to create or reuse an existing resource group.</span></span> <span data-ttu-id="e633e-129">**기존 항목 사용**을 선택하고 드롭다운에서 "<rgn>샌드박스 리소스 그룹 이름</rgn>"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-129">Select **Use existing** and choose "<rgn>[Sandbox resource group name]</rgn>" from the dropdown.</span></span> <span data-ttu-id="e633e-130">이 모듈의 나머지 부분에서 이 그룹을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-130">You'll use this group for the rest of this module.</span></span>

1. <span data-ttu-id="e633e-131">새 서버에 대한 원본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-131">Select the source of your new server.</span></span> <span data-ttu-id="e633e-132">이 랩에서는 옵션을 _비어 있음_으로 그대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-132">For this lab, you'll leave the option set to _Blank_.</span></span> <span data-ttu-id="e633e-133">기존 서버 백업을 복원하려면 옵션을 _백업_으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-133">Recall that you can change the option to _Back up_ if you want to restore an existing server backup.</span></span>

1. <span data-ttu-id="e633e-134">새 서버에 대한 관리자 로그인으로 사용할 로그인 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-134">Choose a login name to use as an administrator login for the new server.</span></span> <span data-ttu-id="e633e-135">관리자 로그인 이름은 azure_superuser, azure_pg_admin, admin, administrator, root, guest 또는 public이 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-135">Recall that the admin login name can't be azure_superuser, azure_pg_admin, admin, administrator, root, guest, or public.</span></span> <span data-ttu-id="e633e-136">pg_로 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-136">It can't start with pg_.</span></span> <span data-ttu-id="e633e-137">나중에 사용하기 위해 이름을 기억하거나 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="e633e-137">Remember or write down the name for future use.</span></span>

1. <span data-ttu-id="e633e-138">위의 관리자 로그인 이름과 함께 사용할 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-138">Choose a password to use with the above administrator login name.</span></span> <span data-ttu-id="e633e-139">암호는 다음 세 범주의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-139">Recall,= that our password must include characters from three of the following categories:</span></span>
   - <span data-ttu-id="e633e-140">영어 대문자</span><span class="sxs-lookup"><span data-stu-id="e633e-140">English uppercase letters</span></span>
   - <span data-ttu-id="e633e-141">영어 소문자</span><span class="sxs-lookup"><span data-stu-id="e633e-141">English lowercase letters</span></span>
   - <span data-ttu-id="e633e-142">숫자(0~9)</span><span class="sxs-lookup"><span data-stu-id="e633e-142">Numbers (0 through 9)</span></span>
   - <span data-ttu-id="e633e-143">영숫자가 아닌 문자(!, $, #, % 등)</span><span class="sxs-lookup"><span data-stu-id="e633e-143">Non-alphanumeric characters (!, $, #, %, and so on)</span></span>

1. <span data-ttu-id="e633e-144">암호를 확인하기 위해 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-144">Retype the password to confirm your password.</span></span>

1. <span data-ttu-id="e633e-145">서버에 대한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-145">Choose a location for your server.</span></span> <span data-ttu-id="e633e-146">다음 목록에서 사용자에게 가장 가까운 위치를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-146">You'll want to choose a location closest to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]


1. <span data-ttu-id="e633e-147">이제 서버의 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-147">You'll now select the version of your server.</span></span> <span data-ttu-id="e633e-148">최신 버전의 PostgreSQL을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-148">Select the latest version of PostgreSQL.</span></span>

1. <span data-ttu-id="e633e-149">마지막 단계에서 두 번째로 **가격 책정 계층** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-149">As the second to last step, select the **Pricing tier** option.</span></span>

    <span data-ttu-id="e633e-150">특정 저장소 및 계산 옵션을 사용하여 서버를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-150">Recall that you need to configure your server with specific storage and compute options:</span></span>

    - <span data-ttu-id="e633e-151">디스크 저장소 10GB</span><span class="sxs-lookup"><span data-stu-id="e633e-151">10 GB of disk storage</span></span>
    - <span data-ttu-id="e633e-152">계산 5세대 지원</span><span class="sxs-lookup"><span data-stu-id="e633e-152">Compute Generation 5 support</span></span>
    - <span data-ttu-id="e633e-153">보존 기간 25일</span><span class="sxs-lookup"><span data-stu-id="e633e-153">Retention period of 25 days</span></span>

    <span data-ttu-id="e633e-154">**가격 책정 계층**을 클릭하여 가격 책정 계층 블레이드에 액세스하고, 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-154">Click **Pricing tier** to access the pricing tier blade and make the following changes:</span></span>

    - <span data-ttu-id="e633e-155">**기본** 옵션 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-155">Choose the **Basic** option tab.</span></span>
    - <span data-ttu-id="e633e-156">**5세대 계산 생성** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-156">Choose the **Gen 5 Computation Generation** option.</span></span>
    - <span data-ttu-id="e633e-157">**vCore** 슬라이더에서 [vCore 1개]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-157">Choose 1 vCore from the **vCore** slider.</span></span> <span data-ttu-id="e633e-158">변경된 슬라이더가 **가격 요약**에 미치는 영향을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-158">Notice how the changes in the slider affect the **Price Summary**.</span></span>
    - <span data-ttu-id="e633e-159">**저장소** 슬라이더에서 10GB를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-159">Choose 10 GB from the **Storage** slider.</span></span> <span data-ttu-id="e633e-160">10GB에 정확하게 슬라이딩하는 데 어려움이 있는 경우 키보드의 왼쪽 및 오른쪽 커서 키를 사용하여 정확한 값에 맞출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-160">If you're having trouble sliding to exactly 10 GB, you can use the left and right cursor keys on your keyboard to get a precise value.</span></span>
    - <span data-ttu-id="e633e-161">**백업 보존 기간** 슬라이더에서 25일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-161">Choose 25 Days from the **Backup Retention Period** slider.</span></span>
    - <span data-ttu-id="e633e-162">백업 중복 옵션을 **로컬 중복**으로 그대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-162">Leave the Backup Redudancy Options set to **Locally Redundant**.</span></span>

    ![새 PostgreSQL 데이터베이스의 데이터베이스 가격 책정 계층을 보여주는 Azure Portal의 스크린샷](../media/4-azure-db-pricing-tier.png)

1. <span data-ttu-id="e633e-164">오른쪽에 있는 가격 요약을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-164">Check out the price summary on the right side.</span></span> <span data-ttu-id="e633e-165">월별 예상 비용과 함께 서버에 대한 비용 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-165">It provides a cost-breakdown for the server along with an estimated monthly cost.</span></span>

1. <span data-ttu-id="e633e-166">선택 항목에 만족하면 **확인**을 클릭하여 해당 선택 항목을 확정하고 가격 책정 계층 옵션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-166">Click **OK** after you're satisfied with your selection to commit your selections and close the pricing tier options.</span></span>

1. <span data-ttu-id="e633e-167">이제 입력한 값을 검토하고, **만들기**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-167">All that's left now is to review the values you entered and click **Create**.</span></span> <span data-ttu-id="e633e-168">만드는 데는 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-168">Creation can take several minutes.</span></span> <span data-ttu-id="e633e-169">Azure Portal 화면의 위쪽에 있는 [알림] 아이콘(벨)을 선택하여 진행 상황을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-169">You can select the Notifications icon (a bell) at the top of the Azure portal screen to monitor progress.</span></span>

<span data-ttu-id="e633e-170">이제 PostgreSQL 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-170">You now have a PostgreSQL server available.</span></span> <span data-ttu-id="e633e-171">다음 단원에서는 Azure CLI를 사용하여 동일한 서버를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e633e-171">In the next unit, you'll see how to create the same server using the Azure CLI.</span></span>
