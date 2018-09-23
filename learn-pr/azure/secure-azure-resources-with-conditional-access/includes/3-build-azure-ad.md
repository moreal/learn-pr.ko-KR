<span data-ttu-id="a95dd-101">Azure AD를 배포하고 어떤 사용자가 Azure Portal에 액세스할 때 Azure에서 Multi-Factor Authentication을 요구하는 조건부 액세스 정책을 사용하도록 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-101">You decide to deploy Azure AD and use conditional access policies that Azure require Multi-Factor Authentication when anyone accesses the Azure portal.</span></span> <span data-ttu-id="a95dd-102">디렉터리를 만들고 임시 라이선스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-102">You need to create a directory and get temporary licenses in place.</span></span>

## <a name="launch-lab-and-sign-in-to-the-azure-portal"></a><span data-ttu-id="a95dd-103">랩을 시작하고 Azure Portal에 로그인</span><span class="sxs-lookup"><span data-stu-id="a95dd-103">Launch lab and sign in to the Azure portal</span></span>

1. <span data-ttu-id="a95dd-104">위의 **VM 모드 시작** 링크를 클릭하여 랩을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-104">Click the **Launch VM mode** link above to launch the lab.</span></span>

1. <span data-ttu-id="a95dd-105">Azure Portal에 LabAdmin(<XXXXXXX>@triplecrownlabsoutlook.onmicrosoft.com)로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-105">Sign in to the Azure portal as LabAdmin-<XXXXXXX>@triplecrownlabsoutlook.onmicrosoft.com.</span></span> <span data-ttu-id="a95dd-106">지침 창의 맨 위에 있는 리소스 탭에서 사용자 이름과 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-106">You can find the username and password on the Resources tab at the top of the instructions window.</span></span>

## <a name="create-a-directory"></a><span data-ttu-id="a95dd-107">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="a95dd-107">Create a directory</span></span>

<span data-ttu-id="a95dd-108">프로덕션 사용자에게 영향을 주지 않고 테스트할 수 있는 First Up Consultants에 대한 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-108">We will create a new directory for First Up Consultants where we can test without fear of impacting production users.</span></span>

1. <span data-ttu-id="a95dd-109">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-109">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="a95dd-110">왼쪽 탐색 창에서 **리소스 만들기** > **ID** > **Azure Active Directory**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-110">In the left navigation pane, click **Create a resource** > **Identity** > **Azure Active Directory**.</span></span>

1. <span data-ttu-id="a95dd-111">**디렉터리 만들기** 블레이드에서 **조직 이름** 및 **초기 도메인 이름**에 대해 다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-111">In the **Create directory** blade, provide the following values for the **Organization name** and **Initial domain name**:</span></span>

   1. <span data-ttu-id="a95dd-112">조직 이름: `First Up Consultants`입니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-112">Organization Name: `First Up Consultants`.</span></span>
   1. <span data-ttu-id="a95dd-113">초기 도메인 이름: `firstupconsultants<XXXXXXX>` 여기서 <XXXXXXX>는 지침 창 위쪽의 **리소스** 탭에 있는 사용자 이름 뒤의 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-113">Initial Domain Name: `firstupconsultants<XXXXXXX>` where <XXXXXXX> is the number after the username on the **Resources** tab at the top of the instructions window.</span></span>

1. <span data-ttu-id="a95dd-114">디렉터리가 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-114">Wait for the directory to be created.</span></span> <span data-ttu-id="a95dd-115">링크를 클릭하여 새 디렉터리로 전환하거나 창 위쪽에서 **디렉터리 및 구독 필터**를 클릭한 다음, 새로 만든 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-115">Click the link to switch to the new directory or click the **Directory and subscription filter** at the top of the window and then choose the newly created directory.</span></span>

## <a name="get-trial-licenses"></a><span data-ttu-id="a95dd-116">평가판 라이선스 가져오기</span><span class="sxs-lookup"><span data-stu-id="a95dd-116">Get trial licenses</span></span>

<span data-ttu-id="a95dd-117">조건부 액세스 및 Multi-Factor Authentication과 같은 기능을 사용하려면 최소한 평가판 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-117">To use features like conditional access and Multi-Factor Authentication, you will need at least a trial license.</span></span> <span data-ttu-id="a95dd-118">다음 단계에서는 평가판 라이선스를 사용하도록 설정하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-118">The following steps walk you through how to enable a trial license:</span></span>

1. <span data-ttu-id="a95dd-119">Azure AD **개요** 창에서 **평가판 시작** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-119">In the Azure AD **Overview** pane, click the **Start a free trial** link.</span></span>

1. <span data-ttu-id="a95dd-120">**Azure AD Premium P2** 항목 아래에서 **평가판**을 클릭한 다음, **활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-120">Under the item **Azure AD Premium P2**, click **Free trial**, and then click **Activate**.</span></span>

## <a name="create-a-test-user"></a><span data-ttu-id="a95dd-121">테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a95dd-121">Create a test user</span></span>

<span data-ttu-id="a95dd-122">여기서는 사용자를 통해 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-122">We're going to need to test this out with a user.</span></span> <span data-ttu-id="a95dd-123">팀의 다른 멤버인 Isabella Simonsen이 자원하여 도움을 주었습니다. 디렉터리에 계정이 필요하므로 계정을 만드는 단계를 거치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-123">Isabella Simonsen (another member of your team) has volunteered to help you out. She will need an account in the directory, so we will go through the steps to create her account.</span></span>

1. <span data-ttu-id="a95dd-124">**Azure Active Directory** > **사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-124">Browse to **Azure Active Directory** > **Users**.</span></span>

1. <span data-ttu-id="a95dd-125">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-125">Click **New user**.</span></span>

1. <span data-ttu-id="a95dd-126">사용자 이름이 **Isabella Simonsen**인 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-126">Create a user named **Isabella Simonsen** with a user name of:</span></span>

   `Isabella@firstupconsultants<XXXXXXX>.onmicrosoft.com`

   <span data-ttu-id="a95dd-127">위의 *디렉터리 만들기* 섹션에서 만든 도메인을 사용하여 @ 뒤에서 도메인을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-127">Match the domain after the @ with the domain you created in the *Create a directory* section above.</span></span>

1. <span data-ttu-id="a95dd-128">사용자에 대한 **암호 표시** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-128">Check the box to **Show Password** for the user.</span></span> <span data-ttu-id="a95dd-129">나중에 테스트할 때 사용할 수 있도록 암호를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-129">Make a note of the password so you can use it later when testing.</span></span>

1. <span data-ttu-id="a95dd-130">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-130">Click **Create**.</span></span>

## <a name="create-a-pilot-group"></a><span data-ttu-id="a95dd-131">파일럿 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a95dd-131">Create a pilot group</span></span>

<span data-ttu-id="a95dd-132">만든 정책을 사용자 그룹에 할당하지만 이 정책에 대한 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-132">We will be assigning the policy that we create to a group of users, but we need to create a group for this policy.</span></span> <span data-ttu-id="a95dd-133">다음 단계는 파일럿 배포에 대한 보안 그룹을 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-133">The following steps help you create a security group for the pilot deployment.</span></span>

1. <span data-ttu-id="a95dd-134">**Azure Active Directory** > **그룹**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-134">Browse to **Azure Active Directory** > **Groups**.</span></span>

1. <span data-ttu-id="a95dd-135">**새 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-135">Click **New group**.</span></span>

1. <span data-ttu-id="a95dd-136">그룹 유형: **보안**</span><span class="sxs-lookup"><span data-stu-id="a95dd-136">Group type **Security**.</span></span>

1. <span data-ttu-id="a95dd-137">그룹 이름: **AzurePortal-CA-MFA**</span><span class="sxs-lookup"><span data-stu-id="a95dd-137">Group name **CA-MFA-AzurePortal**.</span></span>

1. <span data-ttu-id="a95dd-138">멤버 자격 유형: **할당됨**</span><span class="sxs-lookup"><span data-stu-id="a95dd-138">Membership type **Assigned**.</span></span>

1. <span data-ttu-id="a95dd-139">이전 단계에서 만든 사용자를 선택하고 **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-139">Select the user that we created in the previous step and choose **Select**.</span></span>

1. <span data-ttu-id="a95dd-140">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-140">Click **Create**.</span></span>

<span data-ttu-id="a95dd-141">이 단원에서는 Azure Portal에 평가판 사용이 허가된 디렉터리, 테스트 사용자 및 파일럿 그룹을 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-141">In this unit, you learned how to create a trial licensed directory, a test user, and a pilot group in the Azure portal.</span></span>