
<span data-ttu-id="dc561-101">이 연습에서는 로컬 머신의 Azure CLI를 사용하여 리소스 그룹을 만든 다음, 이 리소스 그룹에 웹앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="dc561-102">리소스 그룹을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="dc561-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="dc561-103">Linux 또는 macOS에서 bash 셸을 열거나, Windows에서 작업하는 경우 명령 프롬프트 창 또는 PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="dc561-104">Azure CLI를 시작하고 로그인 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="dc561-105">웹 브라우저에 Azure 로그인 페이지가 표시되지 않는 경우 명령줄 지침을 따르고 [https://aka.ms/devicelogin](https://aka.ms/devicelogin)에 인증 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="dc561-106">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="dc561-107">모든 리소스 그룹을 표에 나열하여 리소스 그룹이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="dc561-108">필요에 따라 Azure Portal에서 리소스가 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-108">Optionally, confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="dc561-109">웹 브라우저를 열고 포털에 로그인한 다음, **리소스 그룹** 섹션으로 이동합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="dc561-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="dc561-110">새 리소스 그룹이 목록에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-110">The new resource group should be displayed in the list.</span></span>

![포털을 사용하여 리소스 그룹 나열](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="dc561-112">서비스 계획을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="dc561-112">Steps to create a service plan</span></span>
<span data-ttu-id="dc561-113">Azure App Service를 사용하여 Web Apps를 실행하는 경우 앱에서 사용하는 Azure 계산 리소스에 대한 요금이 청구되며, Web Apps와 연결된 App Service 계획에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-113">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="dc561-114">서비스 계획은 앱 데이터 센터에 사용되는 지역, 사용되는 VM 수 및 가격 책정 계층을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="dc561-115">앱을 실행할 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="dc561-116">앱 및 플랜의 이름은 고유해야 하므로 문자열 “12345”를 임의 숫자로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="dc561-117">다음 명령은 가격 책정 계층 또는 VM 인스턴스 세부 정보를 지정하지 않으므로, 기본적으로 **작은** VM 인스턴스 1개가 포함된 **기본** 플랜이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="dc561-118">모든 계획을 표에 나열하여 서비스 계획이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-118">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="dc561-119">웹앱을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="dc561-119">Steps to create a web app</span></span>
<span data-ttu-id="dc561-120">이제 서비스 계획에 웹앱을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="dc561-121">동시에 코드를 배포할 수 있지만, 예제에서는 별도의 단계로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-121">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="dc561-122">문자열 “12345”를 이전에 사용한 것과 동일한 임의 번호로 변경하여 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="dc561-123">모든 앱을 표에 나열하여 앱이 성공적으로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-123">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="dc561-124">**DefaultHostName**을 적어 둡니다. 나중에 이 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-124">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="dc561-125">GitHub에서 코드를 배포하는 단계</span><span class="sxs-lookup"><span data-stu-id="dc561-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="dc561-126">최종 단계는 GitHub 리포지토리에서 웹앱으로 코드를 배포하는 것입니다. 이번에도 문자열 “12345”를 이전에 사용한 것과 동일한 임의 번호로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-126">The final step is to deploy code from a GitHub repository to the web app, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="dc561-127">브라우저에 다음 URL을 복사하여 웹앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="dc561-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="dc561-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="dc561-129">페이지에 “HelloWorld”가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-129">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="dc561-130">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="dc561-131">요약</span><span class="sxs-lookup"><span data-stu-id="dc561-131">Summary</span></span>
<span data-ttu-id="dc561-132">이 연습에서는 대화형 Azure CLI 세션의 일반적인 패턴을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="dc561-133">먼저 표준 명령을 사용하여 새 리소스 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="dc561-134">그런 다음, 명령 집합을 사용하여 이 리소스 그룹에 리소스(이 예제에서는 웹앱)를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="dc561-135">이 명령 집합을 셸 스크립트에 쉽게 결합하여, 동일한 리소스를 만들어야 할 때마다 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc561-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
