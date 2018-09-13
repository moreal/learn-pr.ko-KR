<span data-ttu-id="8b699-101">다음으로 Azure CLI를 사용하여 리소스 그룹을 만든 후 이 리소스 그룹에 웹앱을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-101">Next, let's use the Azure CLI to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="8b699-102">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8b699-102">Create a resource group</span></span>

1. <span data-ttu-id="8b699-103">Linux 또는 macOS에서 bash 셸을 열거나, Windows에서 작업하는 경우 명령 프롬프트 창 또는 PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="8b699-104">Azure CLI를 시작하고 로그인 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-104">Start the Azure CLI and run the login command.</span></span>

    ```azurecli
    az login
    ```
    <span data-ttu-id="8b699-105">웹 브라우저에 Azure 로그인 페이지가 표시되지 않는 경우 명령줄 지침을 따르고 [https://aka.ms/devicelogin](https://aka.ms/devicelogin)에 인증 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="8b699-106">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-106">Create a resource group.</span></span>

    ```azurecli
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="8b699-107">모든 리소스 그룹을 표에 나열하여 리소스 그룹이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```azurecli
    az group list --output table
    ```

> [!TIP]
> <span data-ttu-id="8b699-108">Azure Portal에서 리소스가 생성되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-108">You can also confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="8b699-109">웹 브라우저를 열고 포털에 로그인한 다음, **리소스 그룹** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section.</span></span> <span data-ttu-id="8b699-110">새 리소스 그룹이 목록에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-110">The new resource group should be displayed in the list.</span></span>

1. <span data-ttu-id="8b699-111">그룹에 많은 항목이 있는 경우 `--query` 옵션을 추가하여 반환 값을 필터링하고 다음 명령을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-111">If you have a lot of items in the group, you can filter the return values by adding a `--query` option, try this command:</span></span>

    ```azurecli
    az group list --query '[?name == popupResGroup]'
    ```

    <span data-ttu-id="8b699-112">쿼리는 JSON 요청에 대한 표준 쿼리 언어인 **JMESPath**를 사용하여 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-112">The query is formmated using **JMESPath** which is a standard query language for JSON requests.</span></span> <span data-ttu-id="8b699-113">이 강력한 필터 언어에 대한 자세한 내용은 <http://jmespath.org/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b699-113">You can learn more about this powerful filter language at <http://jmespath.org/>.</span></span> <span data-ttu-id="8b699-114">또한 **Azure CLI를 사용하여 VM 관리** 모듈에서 쿼리를 더 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-114">We also cover queries in more depth in the **Manage VMs with the Azure CLI** module.</span></span>

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="8b699-115">서비스 계획을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="8b699-115">Steps to create a service plan</span></span>

<span data-ttu-id="8b699-116">Azure App Service를 사용하여 Web Apps를 실행하는 경우 앱에서 사용하는 Azure 계산 리소스에 대한 요금이 청구되며, Web Apps와 연결된 App Service 계획에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-116">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="8b699-117">서비스 계획은 앱 데이터 센터에 사용되는 지역, 사용되는 VM 수 및 가격 책정 계층을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-117">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="8b699-118">앱을 실행할 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-118">Create an App Service plan to run your app.</span></span> <span data-ttu-id="8b699-119">다음 명령은 가격 책정 계층 또는 VM 인스턴스 세부 정보를 지정하지 않으므로, 기본적으로 **작은** VM 인스턴스 1개가 포함된 **기본** 플랜이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-119">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    > [!WARNING]
    > <span data-ttu-id="8b699-120">앱 이름과 계획은 ‘고유’해야 하므로 이름에 접미사를 추가하고 아래 명령에서 `<unique>` 텍스트를 숫자 집합, 이니셜 또는 기타 텍스트 조각으로 바꿔서 모든 Azure에서 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-120">The name of the app and plan must be _unique_, so add a suffix to the name and replace the `<unique>` text in the command below with a set of numbers, your initials, or some other piece of text to make sure it's unique in all of Azure.</span></span> 

    ```azurecli
    az appservice plan create --name popupapp-<unique> --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="8b699-121">모든 계획을 표에 나열하여 서비스 계획이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-121">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="8b699-122">웹앱을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="8b699-122">Steps to create a web app</span></span>

<span data-ttu-id="8b699-123">이제 서비스 계획에 웹앱을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-123">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="8b699-124">동시에 코드를 배포할 수 있지만, 예제에서는 별도의 단계로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-124">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="8b699-125">웹앱을 만들고 위에서 만든 계획의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-125">Create the web app, supply the name of the plan you created above.</span></span> <span data-ttu-id="8b699-126">**계획과 마찬가지로 앱 이름은 고유해야 하므로 `<unique>` 표식을 일부 텍스트로 바꿔서 이름을 전역적으로 고유하게 설정합니다.**</span><span class="sxs-lookup"><span data-stu-id="8b699-126">**Just like the plan, the app name must be unique, replace the `<unique>` marker with some text to make the name globally unique.**</span></span>
    ```azurecli
    az webapp create --name popupapp-<unique> --resource-group popupResGroup --plan popupapp-<unique>
    ```

1. <span data-ttu-id="8b699-127">모든 앱을 표에 나열하여 앱이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-127">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```azurecli
    az webapp list --output table
    ```

1. <span data-ttu-id="8b699-128">**DefaultHostName**을 적어 둡니다. 나중에 이 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-128">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="8b699-129">GitHub에서 코드를 배포하는 단계</span><span class="sxs-lookup"><span data-stu-id="8b699-129">Steps to deploy code from GitHub</span></span>

1. <span data-ttu-id="8b699-130">최종 단계는 GitHub 리포지토리에서 웹앱으로 코드를 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-130">The final step is to deploy code from a GitHub repository to the web app.</span></span> <span data-ttu-id="8b699-131">실행 시 “HelloWorld!”를 표시하는 Azure 샘플 Github 리포지토리에서 사용 가능한 간단한 PHP 페이지를</span><span class="sxs-lookup"><span data-stu-id="8b699-131">Let's use a simple PHP page available in the Azure Samples Github repository that displays "HelloWorld!"</span></span> <span data-ttu-id="8b699-132">사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-132">when it executes.</span></span> <span data-ttu-id="8b699-133">직접 만든 웹앱 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-133">Make sure to use the web app name you created.</span></span>

    ```azurecli
    az webapp deployment source config --name popupapp-<unique> --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="8b699-134">배포되면 Azure는 `azurewebsites.net` 도메인에서 고유한 앱 이름을 통해 웹 사이트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-134">Once it's deployed, Azure will make your website available through the unique app name in the `azurewebsites.net` domain.</span></span> <span data-ttu-id="8b699-135">예를 들어 앱 이름이 “popupapp-mslearn123”인 경우 웹 사이트 주소는 <http://popupapp-mslearn123.azurewebsites.net>입니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-135">For example, if my app name was "popupapp-mslearn123", then my website address would be: <http://popupapp-mslearn123.azurewebsites.net>.</span></span> <span data-ttu-id="8b699-136">특정 인스턴스에 적중하려면 올바른 URL을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-136">You will need to type in the correct URL to hit your specific instance.</span></span>

1. <span data-ttu-id="8b699-137">페이지에 “HelloWorld”가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-137">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="8b699-138">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-138">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="8b699-139">요약</span><span class="sxs-lookup"><span data-stu-id="8b699-139">Summary</span></span>

<span data-ttu-id="8b699-140">이 연습에서는 대화형 Azure CLI 세션의 일반적인 패턴을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-140">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="8b699-141">먼저 표준 명령을 사용하여 새 리소스 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-141">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="8b699-142">그런 다음, 명령 집합을 사용하여 이 리소스 그룹에 리소스(이 예제에서는 웹앱)를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-142">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="8b699-143">이 명령 집합을 셸 스크립트에 쉽게 결합하여, 동일한 리소스를 만들어야 할 때마다 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b699-143">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
