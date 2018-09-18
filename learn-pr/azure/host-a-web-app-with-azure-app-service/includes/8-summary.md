<span data-ttu-id="0409a-101">모든 기능을 갖춘 웹 응용 프로그램을 성공적으로 만들고 Azure App Service에 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-101">You've successfully created and deployed a full-featured web application to Azure App Service.</span></span>

<span data-ttu-id="0409a-102">App Service는 기존 호스팅 옵션에 비해 웹앱을 관리하고 제어하는 기능을 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-102">App Service simplifies managing and controlling your web app in comparison to traditional hosting options.</span></span> <span data-ttu-id="0409a-103">App Service는 웹앱 실행 및 관리에 드는 시간과 노력을 줄이는 데 도움이 되고 자동 크기 조정 및 Git 통합과 같은 고급 클라우드 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-103">App Service can help you reduce the time and effort spent running and managing your web app, and provide advanced cloud features such as auto scaling and Git integration.</span></span>

## <a name="clean-up"></a><span data-ttu-id="0409a-104">정리</span><span class="sxs-lookup"><span data-stu-id="0409a-104">Clean up</span></span>
<!---TODO: Update for sandbox?--->

<span data-ttu-id="0409a-105">이 응용 프로그램의 작업이 완료되면 아래 단계에 따라 자습서 중에 만들어진 모든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-105">When you are done working with this application, you can follow the steps below to delete all resources created during the tutorial.</span></span>

<span data-ttu-id="0409a-106">아시다시피 리소스 그룹은 생성되고 웹앱에 관련된 모든 리소스를 연결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-106">As you know, a resource group is useful for associating all the resources that are created and related to your web app.</span></span> <span data-ttu-id="0409a-107">따라서 Azure에서 깨끗이 정리하는 것은 리소스 그룹 삭제의 문제이며, 또한 해당 그룹 아래에 만들어진 모든 리소스가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-107">So, cleaning up after yourself on Azure is a matter of deleting the resource group, and hence, all the resources created under that group disappear.</span></span>

<span data-ttu-id="0409a-108">Azure Portal을 사용하여 리소스 그룹을 삭제하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-108">Let's explore together how you can delete a resource group using the Azure portal:</span></span>

1. <span data-ttu-id="0409a-109">[Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-109">Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="0409a-110">대시보드의 왼쪽에서 **리소스 그룹** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-110">Click the **Resource groups** menu item on the left-side of the Dashboard.</span></span> <span data-ttu-id="0409a-111">**리소스 그룹** 페이지에 Azure Portal에서 만든 모든 리소스 그룹이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-111">The **Resource groups** page lists all the resource groups that you have created in the Azure portal.</span></span>

1. <span data-ttu-id="0409a-112">단원 #2에서 만든 리소스 그룹 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-112">Select the resource group name that you created in Unit #2.</span></span> <span data-ttu-id="0409a-113">포털에서 앱 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-113">The portal navigates you to the app page.</span></span>

1. <span data-ttu-id="0409a-114">Azure Portal에서 **리소스 그룹** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-114">The Azure portal navigates you to the **Resource group** page.</span></span> <span data-ttu-id="0409a-115">여기에서 이 모듈 중에 이 리소스 그룹 아래에서 만든 모든 리소스의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-115">There, you can see a list of all the resources that you've created during this module under this resource group.</span></span>

1. <span data-ttu-id="0409a-116">페이지 위쪽에서 **리소스 그룹 삭제** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-116">Click the **Delete resource group** link at the top of the page.</span></span>

1. <span data-ttu-id="0409a-117">리소스 그룹을 정말로 삭제할지 확인하기 하기 위해서 Azure에 해당 이름을 입력하도록 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-117">Azure verifies that you really want to delete this resource group by asking you to type the name of it.</span></span> <span data-ttu-id="0409a-118">계속하려면 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-118">To proceed, type the name of the resource group.</span></span>

1. <span data-ttu-id="0409a-119">확인 창 아래쪽에서 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-119">Click the **Delete** button at the bottom of the confirmation window.</span></span>

1. <span data-ttu-id="0409a-120">리소스 그룹의 모든 리소스를 삭제하려면 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-120">Azure takes a few seconds to delete all the resources of the resource group.</span></span>
