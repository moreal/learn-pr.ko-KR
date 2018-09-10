<span data-ttu-id="daa9b-101">가상 머신, 웹 사이트, 네트워크 및 저장소와 같은 Azure 리소스를 보호하는 것은 클라우드를 사용하는 모든 조직에 중요한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-101">Securing your Azure resources, such as virtual machines, websites, networks, and storage, is a critical function for any organization using the cloud.</span></span> <span data-ttu-id="daa9b-102">데이터와 자산은 보호하되 직원과 파트너에게 작업을 수행하는 데 필요한 액세스 권한을 계속 제공하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-102">You want to ensure that your data and assets are protected, but still grant your employees and partners the access they need to perform their jobs.</span></span> <span data-ttu-id="daa9b-103">RBAC(역할 기반 액세스 제어)는 Azure 리소스에 액세스할 수 있는 사용자, 해당 리소스로 수행할 수 있는 작업 및 액세스 권한이 있는 영역을 관리하는 데 도움이 되는 Azure의 권한 부여 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-103">Role-based access control (RBAC) is an authorization system in Azure that helps you manage who has access to Azure resources, what they can do with those resources, and where they have access.</span></span>

<span data-ttu-id="daa9b-104">예를 들어 회로 및 전기 설계 분야의 전문 엔지니어링 회사인 First Up Consultants에 종사하고 있다고 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="daa9b-104">As an example, suppose you work for First Up Consultants, which is an engineering firm that specializes in circuit and electrical design.</span></span> <span data-ttu-id="daa9b-105">이 회사는 여러 사무실과 다른 회사 간에 공동 작업이 더욱 수월하게 이루어질 수 있도록 워크로드와 자산을 Azure로 옮겼습니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-105">They've moved their workloads and assets to Azure to make collaboration easier across several offices and other companies.</span></span> <span data-ttu-id="daa9b-106">귀하는 First Up Consultants의 IT 부서에서 일하고 있고, 회사의 자산을 안전하게 보호하되 사용자가 필요한 리소스에 액세스할 수 있게 해주는 역할을 담당하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-106">You work in the IT department at First Up Consultants, where you are responsible for keeping the company's assets secure, but still allowing users to access the resources they need.</span></span> <span data-ttu-id="daa9b-107">귀하는 RBAC가 Azure의 리소스를 관리하는 데 도움이 될 수 있다는 이야기를 들었습니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-107">You've heard that RBAC can help you manage resources in Azure.</span></span>

<span data-ttu-id="daa9b-108">이 모듈에서는 RBAC(역할 기반 액세스 제어)를 사용하여 Azure의 리소스에 대한 액세스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-108">In this module, you will learn how to use role-based access control (RBAC) to manage access to resources in Azure.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="daa9b-109">학습 목표</span><span class="sxs-lookup"><span data-stu-id="daa9b-109">Learning objectives</span></span>

<span data-ttu-id="daa9b-110">이 모듈에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="daa9b-110">In this module, you will:</span></span>

- <span data-ttu-id="daa9b-111">자신과 다른 사람의 리소스 액세스 권한 확인</span><span class="sxs-lookup"><span data-stu-id="daa9b-111">Verify access to resources for yourself and others</span></span>
- <span data-ttu-id="daa9b-112">리소스에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="daa9b-112">Grant access to resources</span></span>
- <span data-ttu-id="daa9b-113">RBAC 변경 사항에 대한 활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="daa9b-113">View activity logs of RBAC changes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daa9b-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="daa9b-114">Prerequisites</span></span>

- <span data-ttu-id="daa9b-115">Azure Portal 및 리소스 그룹과 같은 기본 Azure 개념에 대한 지식</span><span class="sxs-lookup"><span data-stu-id="daa9b-115">Knowledge of basic Azure concepts, such as the Azure portal and resource groups</span></span>