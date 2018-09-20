<span data-ttu-id="83350-101">다음으로 Azure CLI를 사용하여 리소스 그룹을 만든 다음, 이 리소스 그룹에 웹앱을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-101">Next, let's use the Azure CLI to create a resource group, and then to deploy a web app into this resource group.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="using-a-resource-group"></a><span data-ttu-id="83350-102">리소스 그룹을 사용하기</span><span class="sxs-lookup"><span data-stu-id="83350-102">Using a resource group</span></span>

<span data-ttu-id="83350-103">사용자 고유의 머신 및 Azure 구독에서 작업하는 경우 `az login` 명령을 사용하여 Azure에 처음으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-103">When you are working with your own machine and Azure subscription you will need to first login to Azure using the `az login` command.</span></span> <span data-ttu-id="83350-104">이 로그인은 Cloud Shell 환경에서는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-104">This is unnecessary with the Cloud Shell environment.</span></span>

<span data-ttu-id="83350-105">다음으로 보통 `az group create` 명령과 관련된 모든 Azure 리소스에 대한 리소스 그룹을 만들지만 이러한 연습의 경우 하나의 리소스 그룹을 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-105">Next, you would normally create a resource group for all your related Azure resources with an `az group create` command, but for these exercises one has been created for you.</span></span> <span data-ttu-id="83350-106">리소스 그룹에 대해 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-106">Use **<rgn>[Sandbox resource group name]</rgn>** for your resource group.</span></span>

1. <span data-ttu-id="83350-107">테이블에 모든 리소스 그룹을 나열하도록 Azure CLI에 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-107">You can ask the Azure CLI to list all your resource groups in a table.</span></span> <span data-ttu-id="83350-108">무료 Azure 샌드박스를 사용하는 동안 하나의 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-108">There should just be one while you are in the free Azure Sandbox.</span></span>

    ```azurecli
    az group list --output table
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="83350-109">Azure 개발과 마찬가지로 여러 리소스 그룹이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-109">As you do more Azure development, you can end up with several resource groups.</span></span> <span data-ttu-id="83350-110">그룹 목록에 여러 항목이 있는 경우 `--query` 옵션을 추가하여 반환 값을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-110">If you have several items in the group list, you can filter the return values by adding a `--query` option.</span></span> <span data-ttu-id="83350-111">다음 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="83350-111">Try this command:</span></span>

    ```azurecli
    az group list --query "[?name == '<rgn>[Sandbox resource group name]</rgn>']"
    ```

    <span data-ttu-id="83350-112">쿼리는 JSON 요청에 대한 표준 쿼리 언어인 **JMESPath**를 사용하여 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83350-112">The query is formated using **JMESPath** which is a standard query language for JSON requests.</span></span> <span data-ttu-id="83350-113">이 강력한 필터 언어에 대한 자세한 내용은 <http://jmespath.org/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83350-113">You can learn more about this powerful filter language at <http://jmespath.org/>.</span></span> <span data-ttu-id="83350-114">또한 **Azure CLI를 사용하여 VM 관리** 모듈에서 쿼리를 더 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="83350-114">We also cover queries in more depth in the **Manage VMs with the Azure CLI** module.</span></span>

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="83350-115">서비스 계획을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="83350-115">Steps to create a service plan</span></span>

<span data-ttu-id="83350-116">Azure App Service를 사용하여 Web Apps를 실행하는 경우 앱에서 사용하는 Azure 계산 리소스에 대한 요금이 청구되며, Web Apps와 연결된 App Service 계획에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="83350-116">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="83350-117">서비스 계획은 앱 데이터 센터에 사용되는 지역, 사용되는 VM 수 및 가격 책정 계층을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-117">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="83350-118">앱을 실행할 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83350-118">Create an App Service plan to run your app.</span></span> <span data-ttu-id="83350-119">다음 명령은 가격 책정 계층 또는 VM 인스턴스 세부 정보를 지정하지 않으므로, 기본적으로 **작은** VM 인스턴스 1개가 포함된 **기본** 플랜이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="83350-119">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    > [!WARNING]
    > <span data-ttu-id="83350-120">앱 이름과 계획은 _고유_해야 하므로 이름에 접미사를 추가하고 아래 명령에서 `<unique>` 텍스트를 숫자 집합, 이니셜 또는 기타 텍스트 조각으로 바꾸어 모든 Azure에서 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-120">The name of the app and plan must be _unique_, so add a suffix to the name and replace the `<unique>` text in the command below with a set of numbers, your initials, or some other piece of text to make sure it's unique in all of Azure.</span></span>

    <span data-ttu-id="83350-121">`--location` 매개 변수의 경우 아래 위치 값 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-121">For the `--location` parameter, use one of the below location values.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group <rgn>[Sandbox resource group name]</rgn> --location <location>
    ```

    <span data-ttu-id="83350-122">이 명령을 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-122">This command can take several minutes to complete.</span></span>

1. <span data-ttu-id="83350-123">모든 계획을 표에 나열하여 서비스 계획이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-123">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="83350-124">웹앱을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="83350-124">Steps to create a web app</span></span>

<span data-ttu-id="83350-125">이제 서비스 계획에 웹앱을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-125">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="83350-126">동시에 코드를 배포할 수 있지만, 예제에서는 별도의 단계로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-126">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="83350-127">웹앱을 만들고 위에서 만든 계획의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-127">Create the web app, supply the name of the plan you created above.</span></span> <span data-ttu-id="83350-128">**계획과 마찬가지로 앱 이름은 고유해야 하므로** 일부 텍스트로 `<unique>` 표식을 바꾸어 글로벌로 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-128">**Just like the plan, the app name must be unique**, replace the `<unique>` marker with some text to make the name globally unique.</span></span>

    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group <rgn>[Sandbox resource group name]</rgn> --plan popupappplan-<unique>
    ```

1. <span data-ttu-id="83350-129">모든 앱을 표에 나열하여 앱이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-129">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```azurecli
    az webapp list --output table
    ```

1. <span data-ttu-id="83350-130">테이블에 나열된 **DefaultHostName**을 기록합니다. 이는 새 웹 사이트에 연결할 수 있는 웹 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="83350-130">Make a note of the **DefaultHostName** listed in the table; this is the reachable web address for the new website.</span></span> <span data-ttu-id="83350-131">Azure는 `azurewebsites.net` 도메인에서 고유한 앱 이름을 통해 웹 사이트를 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-131">Azure will make your website available through the unique app name in the `azurewebsites.net` domain.</span></span> <span data-ttu-id="83350-132">예를 들어 앱 이름이 “popupapp-mslearn123”인 경우 웹 사이트 URL은 `http://popupwebapp-mslearn123.azurewebsites.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="83350-132">For example, if my app name was "popupwebapp-mslearn123", then my website URL would be: `http://popupwebapp-mslearn123.azurewebsites.net`.</span></span>

1. <span data-ttu-id="83350-133">사이트에는 브라우저에서 또는 CURL을 통해 확인할 수 있는 Azure에서 생성한 "빠른 시작" 페이지가 있으므로 **DefaultHostName**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-133">Your site has a "QuickStart" page created by Azure that you can see either in a browser, or with CURL, just use the **DefaultHostName**:</span></span>

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="83350-134">GitHub에서 코드를 배포하는 단계</span><span class="sxs-lookup"><span data-stu-id="83350-134">Steps to deploy code from GitHub</span></span>

1. <span data-ttu-id="83350-135">최종 단계는 GitHub 리포지토리에서 웹앱으로 코드를 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83350-135">The final step is to deploy code from a GitHub repository to the web app.</span></span> <span data-ttu-id="83350-136">실행 시 “HelloWorld!”를 표시하는 Azure 샘플 Github 리포지토리에서 사용 가능한 간단한 PHP 페이지를</span><span class="sxs-lookup"><span data-stu-id="83350-136">Let's use a simple PHP page available in the Azure Samples Github repository that displays "HelloWorld!"</span></span> <span data-ttu-id="83350-137">사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-137">when it executes.</span></span> <span data-ttu-id="83350-138">직접 만든 웹앱 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-138">Make sure to use the web app name you created.</span></span>

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group <rgn>[Sandbox resource group name]</rgn> --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="83350-139">배포되면 브라우저 또는 CURL을 사용하여 사이트를 다시 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="83350-139">Once it's deployed, hit your site again with a browser or CURL.</span></span>

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
    <span data-ttu-id="83350-140">페이지에 "Hello World!"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83350-140">The page displays "Hello World!"</span></span>

    ```output
    Hello World!
    ```

<span data-ttu-id="83350-141">이 연습에서는 대화형 Azure CLI 세션의 일반적인 패턴을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-141">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="83350-142">먼저 표준 명령을 사용하여 새 리소스 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-142">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="83350-143">그런 다음, 명령 집합을 사용하여 이 리소스 그룹에 리소스(이 예제에서는 웹앱)를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-143">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="83350-144">이 명령 집합을 셸 스크립트에 쉽게 결합하여, 동일한 리소스를 만들어야 할 때마다 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83350-144">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>