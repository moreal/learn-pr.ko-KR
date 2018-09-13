<span data-ttu-id="35b3e-101">Azure SQL 데이터베이스가 작동 중이니 원하는 SQL Server 관리 도구에 연결하여 실제 데이터로 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-101">Now that your Azure SQL database is up and running, you can connect it to your favorite SQL Server management tool to populate it with real data.</span></span>

<span data-ttu-id="35b3e-102">처음에는 데이터베이스를 온-프레미스에서 실행할지 아니면 클라우드에서 실행할지 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-102">You initially considered whether to run your database on-premises or in the cloud.</span></span> <span data-ttu-id="35b3e-103">Azure SQL Database를 사용하면 몇 가지 기본적인 옵션을 구성할 수 있고 앱에 연결할 수 있는 완전한 기능의 SQL 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-103">With Azure SQL Database, you configure a few basic options and you have a fully functional SQL database that you can connect to your apps.</span></span>

<span data-ttu-id="35b3e-104">유지 관리할 인프라 또는 소프트웨어 패치는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-104">There's no infrastructure or software patches to maintain.</span></span> <span data-ttu-id="35b3e-105">이제 자유롭게 운송 물류 앱 프로토타입의 작동 및 실행에 좀 더 집중하고 데이터베이스 관리 부하를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-105">You're now free to focus more on getting your transportation logistics app prototype up and running and less on database administration.</span></span> <span data-ttu-id="35b3e-106">프로토타입은 한 번 쓰고 마는 데모가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-106">Your prototype won't be a throw-away demo, either.</span></span> <span data-ttu-id="35b3e-107">Azure SQL Database는 프로덕션 수준의 보안 및 성능 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-107">Azure SQL Database provides production-level security and performance features.</span></span>

<span data-ttu-id="35b3e-108">각 Azure SQL 논리 서버에는 하나 이상의 데이터베이스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-108">Remember that each Azure SQL logical server contains one or more databases.</span></span> <span data-ttu-id="35b3e-109">Azure SQL Database에는 DTU와 vCore라는 두 가지 가격 책정 모델이 제공되며, 이를 통해 모든 데이터베이스에서 비용 대비 성능의 균형을 맞출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-109">Azure SQL Database provides two pricing models, DTU and vCore, to help you balance cost versus performance across all your databases.</span></span>

<span data-ttu-id="35b3e-110">이제 막 사용하기 시작했거나, 미리 구성된 간단한 구매 옵션을 원하는 경우 DTU를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-110">Choose DTU if you're just getting started or want a simple, preconfigured buying option.</span></span> <span data-ttu-id="35b3e-111">만들고 비용을 지불하는 계산 및 저장소 리소스를 보다 효과적으로 제어하려는 경우 vCore를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-111">Choose vCore when you want greater control over what compute and storage resources you create and pay for.</span></span>

<span data-ttu-id="35b3e-112">Azure Cloud Shell을 사용하면 데이터베이스 작업을 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-112">Azure Cloud Shell makes it easy to start working with your databases.</span></span> <span data-ttu-id="35b3e-113">Cloud Shell에서 Azure CLI에 액세스할 수 있고, 여기에서 Azure 리소스에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-113">From Cloud Shell, you have access to the Azure CLI, which enables you to get information about your Azure resources.</span></span> <span data-ttu-id="35b3e-114">또한 Cloud Shell은 새 데이터베이스로 즉시 작업하는 데 도움이 되는 `sqlcmd`와 같은 여러 다양한 공통 유틸리티도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-114">Cloud Shell also provides many other common utilities, such as `sqlcmd`, to help you start working right away with your new database.</span></span>

## <a name="cleanup"></a><span data-ttu-id="35b3e-115">정리</span><span class="sxs-lookup"><span data-stu-id="35b3e-115">Cleanup</span></span>

<span data-ttu-id="35b3e-116">Azure SQL Database 설치로 자유롭게 실험해보세요.</span><span class="sxs-lookup"><span data-stu-id="35b3e-116">Feel free to experiment more with your Azure SQL Database installation.</span></span> <span data-ttu-id="35b3e-117">완료되면 데이터베이스를 삭제하는 가장 쉬운 방법은 부모 리소스 그룹을 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-117">When you're done, the easiest way to delete your database is to delete its parent resource group.</span></span>

1. <span data-ttu-id="35b3e-118">포털에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-118">From the portal, click **Resource groups**.</span></span>

1. <span data-ttu-id="35b3e-119">**logistics-db-rg**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-119">Select **logistics-db-rg**.</span></span>

1. <span data-ttu-id="35b3e-120">**리소스 그룹 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-120">Click **Delete resource group**.</span></span>

    ![리소스 그룹 삭제](../media-draft/delete-rg.png)

1. <span data-ttu-id="35b3e-122">프롬프트에서 “logistics-db-rg”를 입력하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-122">At the prompt, type "logistics-db-rg" and click **Delete**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35b3e-123">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="35b3e-123">Additional resources</span></span>

<span data-ttu-id="35b3e-124">이 문서에서는 자습서 및 샘플을 포함하는 많은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-124">The documentation provides lots more information, including tutorials and samples.</span></span> <span data-ttu-id="35b3e-125">다음은 여기에서 설명한 내용에 대한 몇 가지 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="35b3e-125">Here are a few links to what we covered here:</span></span>

- [<span data-ttu-id="35b3e-126">Azure SQL Database 설명서</span><span class="sxs-lookup"><span data-stu-id="35b3e-126">Azure SQL Database documentation</span></span>](https://docs.microsoft.com/azure/sql-database/)
- [<span data-ttu-id="35b3e-127">Azure SQL Database 구매 모델 및 리소스</span><span class="sxs-lookup"><span data-stu-id="35b3e-127">Azure SQL Database purchasing models and resources</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)
- [<span data-ttu-id="35b3e-128">Azure SQL Database 논리 서버 및 그에 대한 관리</span><span class="sxs-lookup"><span data-stu-id="35b3e-128">Azure SQL Database logical servers and their management</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-logical-servers)
- [<span data-ttu-id="35b3e-129">Azure SQL Database 및 SQL Data Warehouse 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="35b3e-129">Azure SQL Database and SQL Data Warehouse firewall rules</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)

<span data-ttu-id="35b3e-130">Cloud Shell에 대해 자세히 알아보려면 [Azure Cloud Shell 개요](https://docs.microsoft.com/azure/cloud-shell/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35b3e-130">To learn more about Cloud Shell, see [Overview of Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

<span data-ttu-id="35b3e-131">`sqlcmd` 유틸리티에 대한 자세한 내용은 [sqlcmd 유틸리티](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-2017)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35b3e-131">If you're interested in learning more about the `sqlcmd` utility, see [sqlcmd Utility](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-2017).</span></span>
