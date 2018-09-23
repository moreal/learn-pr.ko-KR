<span data-ttu-id="c3716-101">이전 연습에서는 평가판 라이선스를 사용하도록 설정하고, 디렉터리와 사용자를 만들고, 솔루션을 테스트할 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-101">In the previous exercise, we enabled trial licenses, created a directory, created a user, and created a group to test our solution.</span></span> <span data-ttu-id="c3716-102">이 단원에서는 Azure Portal에 Azure Multi-Factor Authentication을 요구하는 조건부 액세스 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-102">In this unit, we will create our conditional access rule to require Azure Multi-Factor Authentication for the Azure portal.</span></span>

## <a name="enable-conditional-access-based-multi-factor-authentication"></a><span data-ttu-id="c3716-103">조건부 액세스 기반 Multi-Factor Authentication 사용</span><span class="sxs-lookup"><span data-stu-id="c3716-103">Enable conditional access-based Multi-Factor Authentication</span></span>

<span data-ttu-id="c3716-104">조건부 액세스를 사용하면 관리자가 수행할 작업을 원하거나 원하지 않는 경우를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-104">Conditional access allows administrators to configure when they do or do not want something to happen.</span></span> <span data-ttu-id="c3716-105">여러 규칙을 병렬로 사용하여 리소스에 대한 액세스를 허용하거나 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-105">They can use multiple rules in parallel to grant or deny access to resources.</span></span> <span data-ttu-id="c3716-106">만들어야 하는 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-106">Here's the rule that we need to create:</span></span>

<span data-ttu-id="c3716-107">**Azure Portal에 액세스할 때 - 다단계 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="c3716-107">**When accessing the Azure portal - Require multi-factor authentication**</span></span>

<span data-ttu-id="c3716-108">다음 단계에서는 사용자가 Azure Portal에 액세스할 때 다단계 인증을 수행하도록 요구하는 조건부 액세스 규칙을 만드는 프로세스를 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-108">The steps that follow will walk you through the process to create a conditional access rule to require users to perform multi-factor authentication when they access the Azure portal.</span></span>

1. <span data-ttu-id="c3716-109">**Azure Active Directory** > **조건부 액세스**로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-109">Browse to **Azure Active Directory** > **Conditional access**.</span></span>

1. <span data-ttu-id="c3716-110">**새 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-110">Click **New policy**.</span></span>

1. <span data-ttu-id="c3716-111">정책 이름을 **Azure Portal에 MFA 요구**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-111">Name the policy **Require MFA for Azure portal**.</span></span>

1. <span data-ttu-id="c3716-112">**할당** > **사용자 및 그룹** 아래에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-112">Under **Assignments** > **Users and groups**, select **Users and groups**.</span></span> <span data-ttu-id="c3716-113">만든 **CA-MFA-AzurePortal** 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-113">Select the group that we created **CA-MFA-AzurePortal**.</span></span> <span data-ttu-id="c3716-114">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-114">and click **Done**.</span></span>

1. <span data-ttu-id="c3716-115">**클라우드 앱** > **앱 선택** 아래에서 **Microsoft Azure 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-115">Under **Cloud apps** > **Select apps**, select **Microsoft Azure Management**.</span></span>

1. <span data-ttu-id="c3716-116">**액세스 제어** > **허용** 아래에서 **다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-116">Under **Access controls** > **Grant**, select **Require multi-factor authentication**.</span></span>

1. <span data-ttu-id="c3716-117">**정책 사용**을 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-117">Set **Enable policy** to **On**.</span></span>

1. <span data-ttu-id="c3716-118">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-118">Click **Create**.</span></span>

<span data-ttu-id="c3716-119">이 단원에서는 조건부 액세스 규칙을 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-119">In this unit, you learned how to create a conditional access rule.</span></span> <span data-ttu-id="c3716-120">이 규칙은 Azure Portal에 액세스할 때 Multi-Factor Authentication을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="c3716-120">The rule requires Multi-Factor Authentication when accessing the Azure portal.</span></span>