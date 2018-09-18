<span data-ttu-id="d693b-101">이전 연습에서는 Azure AD에 대한 기본적인 이해를 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-101">In the previous exercises, we gathered a basic understanding of Azure AD.</span></span> <span data-ttu-id="d693b-102">디렉터리를 만들고, 사용자와 그룹을 만든 다음, Azure Portal에 액세스할 때 Azure Multi-Factor Authentication을 요구하는 조건부 액세스 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-102">We created a directory, created a user and group, and then created a conditional access rule that requires Azure Multi-Factor Authentication when accessing the Azure portal.</span></span>

<span data-ttu-id="d693b-103">이제는 리소스에 액세스할 수 있는지 테스트해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-103">Now, we'll test if we can access our resources.</span></span>

## <a name="test-access-to-resources"></a><span data-ttu-id="d693b-104">리소스에 대한 액세스 테스트</span><span class="sxs-lookup"><span data-stu-id="d693b-104">Test access to resources</span></span>

<span data-ttu-id="d693b-105">사용자가 MyApps 포털을 사용하여 로그인하고 모든 SaaS 응용 프로그램에 액세스할 수 있음을 알고 있으므로 이를 테스트해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-105">You know that your users will sign in and access all their SaaS applications using the MyApps portal, so this is what we'll test.</span></span>

1. <span data-ttu-id="d693b-106">InPrivate 브라우저 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-106">Open an InPrivate browser window.</span></span>

1. <span data-ttu-id="d693b-107">https://myapps.microsoft.com으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-107">Browse to https://myapps.microsoft.com.</span></span>

1. <span data-ttu-id="d693b-108">3단원에서 만든 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-108">Sign in as the user that we created in Unit 3.</span></span>

   * <span data-ttu-id="d693b-109">Multi-Factor Authentication을 요구하지 않고 포털에 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-109">Notice that you're signed in to the portal without requiring Multi-Factor Authentication.</span></span>

1. <span data-ttu-id="d693b-110">동일한 브라우저 창에서 https://portal.azure.com으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-110">In the same browser window, browse to https://portal.azure.com.</span></span>

   * <span data-ttu-id="d693b-111">이제 계정을 안전하게 유지하기 위해 더 많은 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-111">Notice that you're now required to provide more information to keep your account secure.</span></span> <span data-ttu-id="d693b-112">이 인터럽트는 만든 조건부 액세스 정책으로 인해 Azure Multi-Factor Authentication이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-112">This interrupt is Azure Multi-Factor Authentication kicking in because of the conditional access policy we created.</span></span> <span data-ttu-id="d693b-113">이 시점에서 중지하고 브라우저 창을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-113">You can stop at this point and close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="d693b-114">요약</span><span class="sxs-lookup"><span data-stu-id="d693b-114">Summary</span></span>

<span data-ttu-id="d693b-115">이 단원에서는 Azure PowerShell을 사용하여 리소스 그룹에 가상 머신을 만들고 관리할 수 있는 액세스 권한을 사용자에게 부여하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-115">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using Azure PowerShell.</span></span> <span data-ttu-id="d693b-116">다음 단원에서는 사용자 지정 역할을 만들고, 사용자 고유의 권한을 정의하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d693b-116">In the next unit, you look at how to create a custom role and define your own permissions.</span></span>