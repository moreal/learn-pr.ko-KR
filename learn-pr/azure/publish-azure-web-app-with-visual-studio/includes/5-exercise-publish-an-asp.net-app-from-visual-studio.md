<span data-ttu-id="6012c-101">이제 로컬에서 ASP.NET Core 웹 응용 프로그램이 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-101">You now have a local running ASP.NET Core web application.</span></span> <span data-ttu-id="6012c-102">이 단원에서는 Azure App Service에 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-102">In this unit, you'll publish your application to Azure App Service.</span></span>

### <a name="visual-studio-for-windows"></a><span data-ttu-id="6012c-103">Windows용 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6012c-103">Visual Studio for Windows</span></span>

1. <span data-ttu-id="6012c-104">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-104">In Solution Explorer, right-click your project and select **Publish**.</span></span>

1. <span data-ttu-id="6012c-105">나타나는 대화 상자에서 왼쪽에 있는 **App Service**를 게시 대상으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-105">In the dialog box that appears, on the left, choose **App Service** as your publish target.</span></span>  <span data-ttu-id="6012c-106">오른쪽에서 **새로 만들기**를 선택하여 새 App Service를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-106">On the right, select **Create New** to create a new app service.</span></span>

1. <span data-ttu-id="6012c-107">**게시** 단추를 클릭하여 새 App Service를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-107">Click the **Publish** button to create your new app service.</span></span>

> [!NOTE]
> <span data-ttu-id="6012c-108">앱을 배포할 때 새 App Service 계획을 만들 수도 있고 기존 계획에 앱을 계속 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-108">When you deploy your apps, you can create a new App Service plan or you can continue to add apps to an existing plan.</span></span> <span data-ttu-id="6012c-109">이 연습에서는 새 **Azure App Service**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-109">For this exercise, you will create a new **Azure app service**.</span></span>

### <a name="visual-studio-mac"></a><span data-ttu-id="6012c-110">Visual Studio Mac</span><span class="sxs-lookup"><span data-stu-id="6012c-110">Visual Studio Mac</span></span>

1. <span data-ttu-id="6012c-111">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-111">In Solution Explorer, right-click your project.</span></span>

1. <span data-ttu-id="6012c-112">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-112">Select **Publish**.</span></span>

1. <span data-ttu-id="6012c-113">**Azure에 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-113">Click **Publish to Azure**.</span></span> <span data-ttu-id="6012c-114">이렇게 하면 Azure 계정에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-114">This will connect to your Azure account.</span></span> <span data-ttu-id="6012c-115">현재 서비스를 연결하고 나열하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-115">It may take a few minutes to connect and list your current services.</span></span>

1. <span data-ttu-id="6012c-116">**새로 만들기**를 클릭하여 새 App Service를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-116">Click **New** to create a new app service.</span></span>

## <a name="configure-your-new-azure-app-service"></a><span data-ttu-id="6012c-117">새 Azure App Service 구성</span><span class="sxs-lookup"><span data-stu-id="6012c-117">Configure your new Azure App Service</span></span>

1. <span data-ttu-id="6012c-118">**App Service 만들기** 대화 상자에서 **계정 추가**를 클릭하고, Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-118">In the **Create App Service dialog** box, click **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="6012c-119">이미 로그인한 경우 드롭다운 메뉴에서 원하는 구독이 포함된 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-119">If you're already signed in, select the account containing the desired subscription from the drop-down menu.</span></span>

1. <span data-ttu-id="6012c-120">App Service 계획에 대한 필수 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-120">Enter the required information about your App Service plan.</span></span>

    ![App Service 만들기](../media-draft/5-CreateAppService.png)

    <span data-ttu-id="6012c-122">**App Service 만들기** 대화 상자에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-122">In the **Create App Service** dialog box, you will provide the following information:</span></span>

    - <span data-ttu-id="6012c-123">**앱 이름**: 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-123">**App Name**: This is the name of your application.</span></span>  <span data-ttu-id="6012c-124">앱 이름은 게시된 응용 프로그램의 URL을 판별하며, https://_AppName_.azurewebsites.net 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-124">This will determine the URL of the published application, which will be https://_AppName_.azurewebsites.net.</span></span>  <span data-ttu-id="6012c-125">고유한 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-125">It has to be a unique value.</span></span> <span data-ttu-id="6012c-126">따라서 예약되지 않은 이름을 찾으려면 여러 가지 다른 이름을 시도해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-126">Therefore, you will have to try out some different names to find one that is not reserved.</span></span>

    - <span data-ttu-id="6012c-127">**구독**: App Service를 배포하려는 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-127">**Subscription**: The Azure subscription you wish to deploy the app service to.</span></span>

    - <span data-ttu-id="6012c-128">**리소스 그룹**: 리소스 그룹 옆의 **새로 만들기...** 단추를 클릭하고 리소스 그룹의 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-128">**Resource Group:** Click the **New...** button next to the resource group, and enter a unique name for the resource group.</span></span>

        ![새 리소스 그룹](../media-draft/5-NewResourceGroup.png)

    - <span data-ttu-id="6012c-130">**호스팅 계획:** 호스팅 계획은 위치, 크기 및 앱을 호스트하는 웹 서버 팜의 기능을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-130">**Hosting Plan:** The hosting plan specifies the location, size, and features of the web server farm that hosts your app.</span></span> <span data-ttu-id="6012c-131">기존 호스팅 계획을 선택하거나 새 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-131">You can select an existing hosting plan or create a new one.</span></span> <span data-ttu-id="6012c-132">이 연습에서는 새 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-132">For this exercise, you will create a new one.</span></span>

        <span data-ttu-id="6012c-133">호스팅 계획 옆에 있는 **새로 만들기...** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-133">Click the **New...** button next to the hosting plan.</span></span>

        ![새 호스팅 계획](../media-draft/5-NewHostingPlan.png)

        <span data-ttu-id="6012c-135">호스팅 계획에 이름을 지정한 다음 위치와 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-135">Give your hosting plan a name, and then specify the location and the size.</span></span>  
        
        > [!NOTE]
        > <span data-ttu-id="6012c-136">다른 위치 및 크기를 지정하면 서비스 비용에 영향이 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-136">Specifying different locations and sizes will impact the cost of the service.</span></span> <span data-ttu-id="6012c-137">이 연습에서는 **무료** 크기를 지정하여 비용이 부과되지 않도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-137">For the exercise, it is recommended that you specify the **Free** size, which will ensure you won't incur any costs.</span></span>

    - <span data-ttu-id="6012c-138">**Application Insights:** 응용 프로그램에 Application Insights를 사용할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-138">**Application Insights:** Specifies if you want to use Application Insights for your application.</span></span> <span data-ttu-id="6012c-139">이 연습에서는 **없음**을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-139">For this exercise, we recommend that you choose **None.**</span></span>

1. <span data-ttu-id="6012c-140">App Service를 프로비전하려면 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-140">Click the **Create** button to start provisioning your app service.</span></span> <span data-ttu-id="6012c-141">배포 시 진행률이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-141">You will see progress as it deploys:</span></span>

    ![배포 진행률](../media-draft/5-DeployProgress.png)

1. <span data-ttu-id="6012c-143">App Service가 프로비전되면 Visual Studio에서 웹앱을 빌드하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-143">Once the app service is provisioned, Visual Studio will build and deploy your web app.</span></span>  <span data-ttu-id="6012c-144">Visual Studio 빌드 출력에서 배포 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-144">In your Visual Studio build output, you can see the output of the deployment.</span></span>

    ![결과 게시](../media-draft/5-PublishResult.png)

1. <span data-ttu-id="6012c-146">축하합니다. 이제 ASP.NET Core 웹 응용 프로그램이 게시되어 라이브 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-146">Congratulations, your ASP.NET Core web application is now published and live.</span></span> <span data-ttu-id="6012c-147">빌드 출력과 Visual Studio의 게시 페이지에서도 사이트의 최종 URL을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-147">You will be able to see the final URL for your site in the build output and also on the publishing page in Visual Studio.</span></span>

    ![결과 게시](../media-draft/5-PublishPage.png)

1. <span data-ttu-id="6012c-149">웹 사이트를 테스트하려면 표시된 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-149">To test your website, go to the URL indicated.</span></span>

    ![라이브 사이트](../media-draft/5-WebPageLive.png)

## <a name="summary"></a><span data-ttu-id="6012c-151">요약</span><span class="sxs-lookup"><span data-stu-id="6012c-151">Summary</span></span>

<span data-ttu-id="6012c-152">이 연습에서는 Azure App Service를 프로비전하고 ASP.NET Core 웹 응용 프로그램을 배포하는 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-152">This exercise demonstrated the process of provisioning an Azure app service and deploying an ASP.NET Core web application.</span></span> <span data-ttu-id="6012c-153">이제 라이브 웹앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6012c-153">You now have a live web app.</span></span>
