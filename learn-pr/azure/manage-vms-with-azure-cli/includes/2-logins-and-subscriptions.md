<span data-ttu-id="59561-101">시작하기 전에 Azure CLI 도구의 구문을 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-101">Before we start, let's review the syntax for the Azure CLI tool.</span></span> <span data-ttu-id="59561-102">**Azure CLI를 사용하여 Azure 서비스 제어** 모듈을 사용해봤다면 Azure CLI 명령이 다음과 같은 형식임을 알 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59561-102">If you've taken the **Control Azure services with the Azure CLI** module, then you know that Azure CLI commands take the form of:</span></span>

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

<span data-ttu-id="59561-103">`[command]`는 제어할 Azure의 특정 영역을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="59561-103">The `[command]` identifies the specific area of Azure you want to control.</span></span> <span data-ttu-id="59561-104">예를 들어 `account` 명령을 사용하여 구독 정보를 관리하거나 `sql` 명령을 사용하여 SQL 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-104">For example, you can manage subscription information with the `account` command, or SQL databases with the `sql` command.</span></span> <span data-ttu-id="59561-105">`[subcommand]` 및 `[--parameters]`는 작업 중인 명령에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="59561-105">The `[subcommand]` and `[--parameters]` are then dependent upon the command you're working with.</span></span> 

<span data-ttu-id="59561-106">부분 명령을 입력하여 명령, 하위 명령 및 매개 변수의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-106">You can view a list of commands, subcommands, and parameters by typing in a partial command.</span></span> <span data-ttu-id="59561-107">예를 들어, 명령줄에 `az`를 입력하면 최상위 레벨 도움말 화면이 표시되고, `az vm`을 입력하면 가상 머신에 대한 모든 하위 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59561-107">For example, typing `az` at the command line will give you the top-level help screen, and typing `az vm` will give you all the subcommands for virtual machines.</span></span> <span data-ttu-id="59561-108">이 접근법은 Azure CLI 도구를 탐색하는 훌륭한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="59561-108">This approach can be a great way to explore the Azure CLI tool.</span></span>

> [!NOTE]
> <span data-ttu-id="59561-109">Azure CLI 작업을 위해 브라우저 기반의 Azure Cloud Shell을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59561-109">We will be using browser-hosted Azure Cloud Shell to work with the Azure CLI.</span></span> <span data-ttu-id="59561-110">로컬 머신에서 작업하는 것이 편한 경우, [Azure CLI를 설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)하면 여기에서 다루는 모든 명령을 명령줄에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-110">If you prefer to work from your local machine, all of the commands we cover can also be executed from the command line by [installing the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="59561-111">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="59561-111">Log in to Azure</span></span>

<span data-ttu-id="59561-112">Azure CLI로 작업할 때 처음 하는 일은 Azure 계정에 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59561-112">The first thing you'll do when working with the Azure CLI is to log in to your Azure account.</span></span> <span data-ttu-id="59561-113">이 작업은 `login` 명령을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="59561-113">This is done with the `login` command.</span></span> <span data-ttu-id="59561-114">Cloud Shell을 사용하는 경우 Azure에 로그인하는 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-114">If you're using Cloud Shell, there will be a button to sign in to Azure.</span></span>

```azurecli
az login
```

<span data-ttu-id="59561-115">이 명령을 실행하면 브라우저 창이 열리며, 여기에서 사용할 Microsoft 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-115">This command will launch a browser window and allow you to select the Microsoft account you want to use.</span></span>

## <a name="working-with-subscriptions"></a><span data-ttu-id="59561-116">구독 작업</span><span class="sxs-lookup"><span data-stu-id="59561-116">Working with subscriptions</span></span>

<span data-ttu-id="59561-117">이 모듈에서는 테스트용으로 만들어진 임시 구독으로 작업하지만, 일반적으로는 본인 계정의 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59561-117">In this module, we will work in a temporary subscription created as a playground, but you will normally use a subscription from your own account.</span></span> <span data-ttu-id="59561-118">둘 이상의 구독이 있는 경우 `az account list --output table` 문을 사용하여 명확하게 서식이 지정된 구독 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-118">If you have more than one subscription, you can get a clearly formatted list of subscriptions using the `az account list --output table` statement.</span></span>

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

<span data-ttu-id="59561-119">이 명령은 또한 모든 명령이 적용되는 _기본_ 구독을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="59561-119">Notice that the command also identifies the _default_ subscription where all your commands will apply.</span></span> <span data-ttu-id="59561-120">다른 구독으로 작업하려면 `az account set --subscription "[name]"` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-120">If you would prefer to work in a different subscription, you can use the `az account set --subscription "[name]"` command.</span></span> <span data-ttu-id="59561-121">예를 들어 다음 명령을 통해 현재 구독을 위 목록에서 `Visual Studio Enterprise`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59561-121">For example, we could set our current subscription to be `Visual Studio Enterprise` from the above list through the following command:</span></span>

```azurecli
az account set --subscription "Visual Studio Enterprise"
```