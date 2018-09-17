<span data-ttu-id="bde17-101">다음으로 Azure CLI를 사용하여 리소스 그룹을 만든 다음, 이 리소스 그룹에 웹앱을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-101">Next, let's use the Azure CLI to create a resource group, and then to deploy a web app into this resource group.</span></span>

<span data-ttu-id="bde17-102">고유한 Azure 구독으로 설치한 Azure CLI를 사용할 수 있지만 Azure CLI가 이미 설치된 Azure Cloud Shell으로 이 연습에 사용할 수 있는 무료 샌드박스 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-102">You can use the Azure CLI you installed with your own Azure subscription, but there is a free sandbox environment available for this exercise with Azure Cloud Shell where the Azure CLI is already installed.</span></span> <span data-ttu-id="bde17-103">다음 지침에서는 무료 샌드박스를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-103">The following instructions assume you will be using the free sandbox.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="bde17-104">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="bde17-104">Create a resource group</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

> [!NOTE]
> <span data-ttu-id="bde17-105">일반적으로 `az group create ...` 명령과 관련된 모든 Azure 리소스에 대한 리소스 그룹을 만들지만 이 실습에서는 하나를 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-105">Normally, you would create a resource group for all your related Azure resources with an `az group create ...` command, but for these exercises one has been created for you.</span></span> <span data-ttu-id="bde17-106">이 리소스 그룹 이름은 이 연습의 뒷부분에 나오는 명령에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-106">This resource group name will be injected into the later commands in this exercise.</span></span>

<!-- TODO: This is original text prior to updates to use the sandbox. These can be worked back in as instructions for people using their own subscriptions. There is one more block like this below. Note that the assignment of RESOURCE_GROUP below would need to be different as well. -->

<!-- 1. Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows. -->

<!-- 1. Start the Azure CLI and run the login command.

    ```azurecli
    az login
    ```
    If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin). -->

<!-- 1. Create a resource group.

    ```azurecli
    az group create --location westeurope --name popupResGroup
    ``` -->

1. <span data-ttu-id="bde17-107">모든 리소스 그룹을 표에 나열하여 리소스 그룹이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```azurecli
    az group list --output table
    ```

    <span data-ttu-id="bde17-108">무료 샌드박스를 사용하는 경우 생성된 `<rgn>[Sandbox resource group name]</rgn>` 리소스 그룹만 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-108">You may only see the `<rgn>[Sandbox resource group name]</rgn>` resource group that was generated for your free sandbox usage.</span></span>

<!-- > [!TIP]
> You can also confirm the resource was created in the Azure portal. Open a web browser, sign in to the portal and navigate to the **Resource Groups** section. The new resource group should be displayed in the list. -->

1. <span data-ttu-id="bde17-109">Azure 개발과 마찬가지로 여러 리소스 그룹이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-109">As you do more Azure development, you can end up with several resource groups.</span></span> <span data-ttu-id="bde17-110">그룹 목록에 여러 항목이 있는 경우 `--query` 옵션을 추가하여 반환 값을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-110">If you have several items in the group list, you can filter the return values by adding a `--query` option.</span></span> <span data-ttu-id="bde17-111">다음 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="bde17-111">Try this command:</span></span>

    ```azurecli
    az group list --query "[?name == '<rgn>[Sandbox resource group name]</rgn>']"
    ```

    <span data-ttu-id="bde17-112">쿼리는 JSON 요청에 대한 표준 쿼리 언어인 **JMESPath**를 사용하여 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-112">The query is formated using **JMESPath** which is a standard query language for JSON requests.</span></span> <span data-ttu-id="bde17-113">이 강력한 필터 언어에 대한 자세한 내용은 <http://jmespath.org/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bde17-113">You can learn more about this powerful filter language at <http://jmespath.org/>.</span></span> <span data-ttu-id="bde17-114">또한 **Azure CLI를 사용하여 VM 관리** 모듈에서 쿼리를 더 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-114">We also cover queries in more depth in the **Manage VMs with the Azure CLI** module.</span></span>

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="bde17-115">서비스 계획을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="bde17-115">Steps to create a service plan</span></span>

<span data-ttu-id="bde17-116">Azure App Service를 사용하여 Web Apps를 실행하는 경우 앱에서 사용하는 Azure 계산 리소스에 대한 요금이 청구되며, Web Apps와 연결된 App Service 계획에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-116">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="bde17-117">서비스 계획은 앱 데이터 센터에 사용되는 지역, 사용되는 VM 수 및 가격 책정 계층을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-117">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="bde17-118">앱을 실행할 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-118">Create an App Service plan to run your app.</span></span> <span data-ttu-id="bde17-119">다음 명령은 가격 책정 계층 또는 VM 인스턴스 세부 정보를 지정하지 않으므로, 기본적으로 **작은** VM 인스턴스 1개가 포함된 **기본** 플랜이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-119">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    > [!WARNING]
    > <span data-ttu-id="bde17-120">앱 이름과 계획은 _고유_해야 하므로 이름에 접미사를 추가하고 아래 명령에서 `<unique>` 텍스트를 숫자 집합, 이니셜 또는 기타 텍스트 조각으로 바꿔서 모든 Azure에서 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-120">The name of the app and plan must be _unique_, so add a suffix to the name and replace the `<unique>` text in the command below with a set of numbers, your initials, or some other piece of text to make sure it's unique in all of Azure.</span></span>

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group "<rgn>[Sandbox resource group name]</rgn>" --location eastus
    ```

    <span data-ttu-id="bde17-121">이 명령을 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-121">This command can take several minutes to complete.</span></span>

1. <span data-ttu-id="bde17-122">모든 계획을 표에 나열하여 서비스 계획이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-122">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="bde17-123">웹앱을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="bde17-123">Steps to create a web app</span></span>

<span data-ttu-id="bde17-124">이제 서비스 계획에 웹앱을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-124">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="bde17-125">동시에 코드를 배포할 수 있지만, 예제에서는 별도의 단계로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-125">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="bde17-126">웹앱을 만들고 위에서 만든 계획의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-126">Create the web app, supply the name of the plan you created above.</span></span> <span data-ttu-id="bde17-127">**계획과 마찬가지로 앱 이름은 고유해야 하므로 `<unique>` 표식을 일부 텍스트로 바꿔서 이름을 전역적으로 고유하게 설정합니다.**</span><span class="sxs-lookup"><span data-stu-id="bde17-127">**Just like the plan, the app name must be unique, replace the `<unique>` marker with some text to make the name globally unique.**</span></span>
    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group popupResGroup --plan popupappplan-<unique>
    ```

1. <span data-ttu-id="bde17-128">모든 앱을 표에 나열하여 앱이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-128">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```azurecli
    az webapp list --output table
    ```

1. <span data-ttu-id="bde17-129">**DefaultHostName**을 적어 둡니다. 나중에 이 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-129">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="bde17-130">GitHub에서 코드를 배포하는 단계</span><span class="sxs-lookup"><span data-stu-id="bde17-130">Steps to deploy code from GitHub</span></span>

1. <span data-ttu-id="bde17-131">최종 단계는 GitHub 리포지토리에서 웹앱으로 코드를 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-131">The final step is to deploy code from a GitHub repository to the web app.</span></span> <span data-ttu-id="bde17-132">실행 시 “HelloWorld!”를 표시하는 Azure 샘플 Github 리포지토리에서 사용 가능한 간단한 PHP 페이지를</span><span class="sxs-lookup"><span data-stu-id="bde17-132">Let's use a simple PHP page available in the Azure Samples Github repository that displays "HelloWorld!"</span></span> <span data-ttu-id="bde17-133">사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-133">when it executes.</span></span> <span data-ttu-id="bde17-134">직접 만든 웹앱 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-134">Make sure to use the web app name you created.</span></span>

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group "<rgn>[Sandbox resource group name]</rgn>" --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="bde17-135">배포되면 Azure는 `azurewebsites.net` 도메인에서 고유한 앱 이름을 통해 웹 사이트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-135">Once it's deployed, Azure will make your website available through the unique app name in the `azurewebsites.net` domain.</span></span> <span data-ttu-id="bde17-136">예를 들어 앱 이름이 “popupapp-mslearn123”인 경우 웹 사이트 주소는 <http://popupapp-mslearn123.azurewebsites.net>입니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-136">For example, if my app name was "popupapp-mslearn123", then my website address would be: <http://popupapp-mslearn123.azurewebsites.net>.</span></span> <span data-ttu-id="bde17-137">특정 인스턴스에 적중하려면 올바른 URL을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-137">You will need to type in the correct URL to hit your specific instance.</span></span>

1. <span data-ttu-id="bde17-138">페이지에 "Hello World"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-138">The page displays "Hello World!"</span></span>

1. <span data-ttu-id="bde17-139">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-139">Close the browser window.</span></span>

<span data-ttu-id="bde17-140">이 연습에서는 대화형 Azure CLI 세션의 일반적인 패턴을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-140">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="bde17-141">먼저 표준 명령을 사용하여 새 리소스 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-141">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="bde17-142">그런 다음, 명령 집합을 사용하여 이 리소스 그룹에 리소스(이 예제에서는 웹앱)를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-142">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="bde17-143">이 명령 집합을 셸 스크립트에 쉽게 결합하여, 동일한 리소스를 만들어야 할 때마다 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde17-143">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
