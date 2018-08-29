## <a name="motivation"></a><span data-ttu-id="0cba7-101">사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="0cba7-101">Motivation</span></span>
<span data-ttu-id="0cba7-102">Azure CLI를 사용하면 명령을 작성하고 즉시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-102">The Azure CLI lets you write commands and execute them immediately.</span></span> <span data-ttu-id="0cba7-103">소프트웨어 개발 예제의 전반적인 목표는 테스트할 새로운 웹앱 빌드를 배포하는 것임을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0cba7-103">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="0cba7-104">첫 번째 단계는 리소스 그룹을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-104">The first step is to create a resource group.</span></span> <span data-ttu-id="0cba7-105">여기서 목표는 Azure CLI의 로컬 설치를 사용하여 이러한 리소스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-105">Remember that the goal here is to create these resources using a local installation of the Azure CLI.</span></span> 

<span data-ttu-id="0cba7-106">이 단원에서는 Azure CLI를 사용하여 Azure 구독에 로그인하고 새 리소스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-106">This unit shows you how to use the Azure CLI to sign in to your Azure subscription and create a new resource.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="0cba7-107">Azure CLI를 사용하여 관리할 수 있는 Azure 리소스는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0cba7-107">What Azure resources can be managed using the Azure CLI?</span></span>
<span data-ttu-id="0cba7-108">Azure CLI를 사용하면 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-108">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="0cba7-109">리소스 그룹, 저장소, 가상 머신, Azure AD(Azure Active Directory), 컨테이너, 기계 학습 등을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-109">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="0cba7-110">CLI의 명령은 그룹 및 하위 그룹으로 구조화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-110">Commands in the CLI are structured in groups and subgroups.</span></span> <span data-ttu-id="0cba7-111">각 그룹은 Azure에서 제공되는 서비스를 나타내며, 하위 그룹은 이러한 서비스에 대한 명령을 논리적 그룹으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-111">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="0cba7-112">예를 들어 **저장소** 그룹에는 **계정**, **blob**, **저장소**, **큐** 등의 하위 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-112">For example, the **storage** group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="0cba7-113">그러면 필요한 특정 명령을 찾는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0cba7-113">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="0cba7-114">한 가지 방법은 **az find**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-114">One way is to use **az find**.</span></span> <span data-ttu-id="0cba7-115">예를 들어 저장소 **blob**을 관리하는 데 도움이 되는 명령을 찾으려면 다음 find 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-115">For example, if you want to find commands that might help you manage a storage **blob**, you'd use the following find command:</span></span>

```bash
az find -q blob
```

<span data-ttu-id="0cba7-116">원하는 명령의 이름을 이미 알고 있는 경우 해당 명령에 대한 **--help** 인수가 더 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-116">If you already know the name of the command you want, the **--help** argument for that command may be more useful.</span></span> <span data-ttu-id="0cba7-117">명령에 대한 자세한 정보와 명령 그룹의 사용 가능한 하위 명령 목록을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-117">You get detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="0cba7-118">이 저장소 예제에서 Blob Storage 관리를 위한 하위 그룹 및 명령 목록을 가져올 수 있는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-118">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="0cba7-119">Azure 리소스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="0cba7-119">How to create an Azure resource</span></span>
<span data-ttu-id="0cba7-120">새 Azure 리소스를 만드는 3단계는 일반적으로 Azure 구독에 연결하고, 리소스를 만들고, 리소스가 제대로 만들어졌는지 확인하는 것입니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="0cba7-120">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful (see below).</span></span>

![Azure CLI를 사용하여 리소스를 만드는 단계](../media-drafts/4-create-resources-overview.png)

<span data-ttu-id="0cba7-122">각 단계는 다른 Azure CLI 명령에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-122">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="0cba7-123">연결</span><span class="sxs-lookup"><span data-stu-id="0cba7-123">Connect</span></span>
<span data-ttu-id="0cba7-124">로컬에 설치한 Azure CLI를 사용하므로 Azure CLI **login** 명령을 사용하여 Azure 명령을 실행하기 전에 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-124">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span> 

```bash
az login
```

<span data-ttu-id="0cba7-125">Azure CLI에서는 일반적으로 기본 브라우저가 시작되어 Azure 로그인 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-125">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="0cba7-126">그러지 않는 경우 명령줄 지침에 따라 [https://aka.ms/devicelogin](https://aka.ms/devicelogin)에 인증 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-126">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="0cba7-127">로그인이 성공하면 Azure 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-127">After a successful sign in, you'll be connected to your Azure subscription.</span></span> 

### <a name="create"></a><span data-ttu-id="0cba7-128">생성</span><span class="sxs-lookup"><span data-stu-id="0cba7-128">Create</span></span>
<span data-ttu-id="0cba7-129">새 Azure 서비스를 만들려면 먼저 새 리소스 그룹을 만들어야 하므로 CLI에서 Azure 리소스를 만드는 방법을 보여 주는 예로 리소스 그룹을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-129">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="0cba7-130">Azure CLI **group create** 명령은 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-130">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="0cba7-131">이름 및 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-131">You must specify a name and location.</span></span> <span data-ttu-id="0cba7-132">이름은 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-132">The name must be unique within your subscription.</span></span> <span data-ttu-id="0cba7-133">위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-133">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="0cba7-134">“미국 서부”, “북유럽” 또는 “인도 서부” 같은 문자열을 사용하여 위치를 지정합니다. westus, northeurope 또는 westindia 같이 동일한 의미의 단일 단어를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-134">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="0cba7-135">핵심 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-135">The core syntax is:</span></span>

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="0cba7-136">Verify</span><span class="sxs-lookup"><span data-stu-id="0cba7-136">Verify</span></span>
<span data-ttu-id="0cba7-137">Azure CLI는 여러 Azure 리소스에 대해 리소스 세부 정보를 표시하는 **list** 하위 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-137">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="0cba7-138">예를 들어 Azure CLI **group list** 명령은 Azure 리소스 그룹을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-138">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="0cba7-139">여기서는 리소스 그룹 만들기가 성공했는지 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-139">This is useful here to verify whether creation of the resource group was successful:</span></span>

```bash
az group list
```

<span data-ttu-id="0cba7-140">뷰를 더 간결하게 하려면 출력을 간단한 테이블로 형식 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cba7-140">To get a more concise view, you can format the output as a simple table:</span></span>

```bash
az group list --output table
```
