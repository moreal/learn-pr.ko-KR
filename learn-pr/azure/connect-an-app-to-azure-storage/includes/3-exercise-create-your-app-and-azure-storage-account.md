<span data-ttu-id="57c6d-101">이 단원에서는 .NET Core 콘솔 응용 프로그램과 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-101">In this unit, you will create a .NET Core console application and an Azure storage account.</span></span>

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="57c6d-102">.NET Core 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="57c6d-102">Create a .NET Core console application</span></span>

<span data-ttu-id="57c6d-103">Visual Studio 2017을 사용하여 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-103">We will be using Visual Studio 2017 to create our app.</span></span>

1. <span data-ttu-id="57c6d-104">Visual Studio 2017에서 **파일** > **새로 만들기** > **프로젝트** 메뉴 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-104">In Visual Studio 2017, select the **File** > **New** > **Project** menu option.</span></span>

1. <span data-ttu-id="57c6d-105">**Visual C# - .NET Core** 범주 내에서 **콘솔 앱(.NET Core)** 을 선택하고 앱 이름을 입력한 다음, **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-105">Within the **Visual C# - .NET Core** category, select **Console App (.NET Core)**, enter a name for your app and select **OK**.</span></span>
  <span data-ttu-id="57c6d-106">![새 앱](..\media-draft\3-new-console-app.png)</span><span class="sxs-lookup"><span data-stu-id="57c6d-106">![New App](..\media-draft\3-new-console-app.png)</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="57c6d-107">Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="57c6d-107">Create an Azure storage account</span></span>

<span data-ttu-id="57c6d-108">Azure Storage 계정에 연결하려면 먼저 연결할 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-108">In order to connect to an Azure storage account, we must first create a storage account to connect to.</span></span>

1. <span data-ttu-id="57c6d-109">Azure Portal의 왼쪽 위에서 '리소스 만들기'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-109">In the top left of the Azure Portal, select 'Create a resource'.</span></span>

1. <span data-ttu-id="57c6d-110">표시되는 선택 창에서 ‘저장소’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-110">In the selection pane that appears, select 'Storage'.</span></span>

1. <span data-ttu-id="57c6d-111">해당 창의 오른쪽에서 ‘저장소 계정 - Blob, File, Table, Queue’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-111">On the right side of that pane, select 'Storage account - blob, file, table, queue'.</span></span>
  <span data-ttu-id="57c6d-112">![포털 선택](..\media-draft\3-portal-storage-select.png)</span><span class="sxs-lookup"><span data-stu-id="57c6d-112">![portal select](..\media-draft\3-portal-storage-select.png)</span></span>

1. <span data-ttu-id="57c6d-113">저장소 계정의 세부 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-113">The details of the storage account need to be entered.</span></span> <span data-ttu-id="57c6d-114">저장소 계정에 사용할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-114">Enter a name for the storage account.</span></span>

1. <span data-ttu-id="57c6d-115">리소스 그룹은 리소스의 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-115">A resource group is a logical container for resources.</span></span> <span data-ttu-id="57c6d-116">선택한 리소스 그룹에 대해 **새로 만들기**를 선택하고 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-116">For the resource group selection, select **Create New** and enter a name for your resource group.</span></span>

1. <span data-ttu-id="57c6d-117">다른 모든 옵션은 기본값으로 남겨 두고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-117">Leave all other options at their default values and click **Create**.</span></span>
  <span data-ttu-id="57c6d-118">![포털 세부 정보](..\media-draft\3-portal-storage-details.png).</span><span class="sxs-lookup"><span data-stu-id="57c6d-118">![Portal details](..\media-draft\3-portal-storage-details.png).</span></span>

<span data-ttu-id="57c6d-119">이제 리소스 그룹이 프로비전되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-119">Your resource group is now being provisioned.</span></span> <span data-ttu-id="57c6d-120">그런 다음, 저장소 계정이 리소스 그룹 내에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-120">After that, your storage account is created within the resource group.</span></span>
<span data-ttu-id="57c6d-121">또한 응용 프로그램을 만들었으며, 해당 응용 프로그램을 구성하고 저장소 계정에 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="57c6d-121">Additionally, you have created your application and are ready to configure and connect it to your storage account.</span></span>
