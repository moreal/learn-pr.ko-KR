<span data-ttu-id="72394-101">Azure CLI를 사용하면 명령줄에서 명령을 입력하고 바로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-101">The Azure CLI lets you type commands and execute them immediately from the command line.</span></span> <span data-ttu-id="72394-102">소프트웨어 개발 예제의 전반적인 목표는 테스트할 새로운 웹앱 빌드를 배포하는 것임을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="72394-102">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="72394-103">Azure CLI로 수행할 수 있는 작업 종류에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-103">Let's talk about the sorts of tasks you can do with the Azure CLI.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="72394-104">Azure CLI를 사용하여 관리할 수 있는 Azure 리소스는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="72394-104">What Azure resources can be managed using the Azure CLI?</span></span>

<span data-ttu-id="72394-105">Azure CLI를 사용하면 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-105">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="72394-106">리소스 그룹, 저장소, 가상 머신, Azure AD(Azure Active Directory), 컨테이너, 기계 학습 등을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-106">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="72394-107">CLI의 명령은 _그룹_ 및 _하위 그룹_으로 구조화됩니다.</span><span class="sxs-lookup"><span data-stu-id="72394-107">Commands in the CLI are structured in _groups_ and _subgroups_.</span></span> <span data-ttu-id="72394-108">각 그룹은 Azure에서 제공되는 서비스를 나타내며, 하위 그룹은 이러한 서비스에 대한 명령을 논리적 그룹으로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="72394-108">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="72394-109">예를 들어 `storage` 그룹에는  **계정**, **BLOB**, **저장소** 및 **큐** 등의 하위 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-109">For example, the `storage` group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="72394-110">그러면 필요한 특정 명령을 찾는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="72394-110">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="72394-111">한 가지 방법은 `az find`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72394-111">One way is to use `az find`.</span></span> <span data-ttu-id="72394-112">예를 들어 저장소 BLOB을 관리하는 데 도움이 되는 명령을 찾으려면 다음 find 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-112">For example, if you want to find commands that might help you manage a storage blob, you can use the following find command:</span></span>

```azurecli
az find -q blob
```

<span data-ttu-id="72394-113">원하는 명령의 이름을 이미 알고 있는 경우 해당 명령의 `--help` 인수를 사용하면 명령에 대한 자세한 정보가 표시되고, 명령 그룹에 이 인수를 사용하면 사용 가능한 하위 명령 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72394-113">If you already know the name of the command you want, the `--help` argument for that command will get you more detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="72394-114">이 저장소 예제에서 Blob Storage 관리를 위한 하위 그룹 및 명령 목록을 가져올 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-114">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```azurecli
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="72394-115">Azure 리소스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="72394-115">How to create an Azure resource</span></span>

<span data-ttu-id="72394-116">새 Azure 리소스를 만드는 3단계는 일반적으로 Azure 구독에 연결하고, 리소스를 만들고, 리소스가 제대로 만들어졌는지 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72394-116">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful.</span></span> <span data-ttu-id="72394-117">다음 그림은 프로세스의 상위 수준 개요를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-117">The following illustration shows a high-level overview of the process.</span></span>

![명령줄 인터페이스를 사용하여 Azure 리소스를 만드는 단계를 보여 주는 그림](../media/4-create-resources-overview.png)

<span data-ttu-id="72394-119">각 단계는 다른 Azure CLI 명령에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-119">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="72394-120">연결</span><span class="sxs-lookup"><span data-stu-id="72394-120">Connect</span></span>

<span data-ttu-id="72394-121">로컬에 설치한 Azure CLI를 사용하므로 Azure CLI **login** 명령을 사용하여 Azure 명령을 실행하기 전에 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-121">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span>

```azurecli
az login
```

<span data-ttu-id="72394-122">Azure CLI에서는 일반적으로 기본 브라우저가 시작되어 Azure 로그인 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="72394-122">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="72394-123">그러지 않는 경우 명령줄 지침에 따라 [https://aka.ms/devicelogin](https://aka.ms/devicelogin)에 인증 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-123">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="72394-124">로그인이 성공하면 Azure 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="72394-124">After a successful sign in, you'll be connected to your Azure subscription.</span></span>

### <a name="create"></a><span data-ttu-id="72394-125">생성</span><span class="sxs-lookup"><span data-stu-id="72394-125">Create</span></span>

<span data-ttu-id="72394-126">새 Azure 서비스를 만들려면 먼저 새 리소스 그룹을 만들어야 하므로 CLI에서 Azure 리소스를 만드는 방법을 보여 주는 예로 리소스 그룹을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-126">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="72394-127">Azure CLI **group create** 명령은 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72394-127">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="72394-128">이름 및 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-128">You must specify a name and location.</span></span> <span data-ttu-id="72394-129">이름은 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-129">The name must be unique within your subscription.</span></span> <span data-ttu-id="72394-130">위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-130">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="72394-131">“미국 서부”, “북유럽” 또는 “인도 서부” 같은 문자열을 사용하여 위치를 지정합니다. westus, northeurope 또는 westindia 같이 동일한 의미의 단일 단어를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-131">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="72394-132">핵심 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-132">The core syntax is:</span></span>

```azurecli
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="72394-133">Verify</span><span class="sxs-lookup"><span data-stu-id="72394-133">Verify</span></span>

<span data-ttu-id="72394-134">Azure CLI는 여러 Azure 리소스에 대해 리소스 세부 정보를 표시하는 **list** 하위 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-134">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="72394-135">예를 들어 Azure CLI **group list** 명령은 Azure 리소스 그룹을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-135">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="72394-136">여기서는 리소스 그룹 만들기가 성공했는지 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="72394-136">This is useful here to verify whether creation of the resource group was successful:</span></span>

```azurecli
az group list
```

<span data-ttu-id="72394-137">뷰를 더 간결하게 하려면 출력을 간단한 테이블로 형식 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72394-137">To get a more concise view, you can format the output as a simple table:</span></span>

```azurecli
az group list --output table
```
