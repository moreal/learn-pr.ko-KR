<span data-ttu-id="2540c-101">이제 앱과 Azure Function이 완료되어 로컬에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-101">The app and Azure Function are now complete and running locally.</span></span> <span data-ttu-id="2540c-102">이 단원에서는 함수를 Azure에 게시하여 클라우드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-102">In this unit, you publish the function to Azure to run in the cloud.</span></span>

> <span data-ttu-id="2540c-103">이 단원에서는 Visual Studio에서 함수를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-103">In this unit, you will publish your function from Visual Studio.</span></span> <span data-ttu-id="2540c-104">이는 개념 증명, 프로토타입 및 학습용으로 시작하는 데 유용한 방법이지만, 프로덕션 품질 앱의 경우 이 방법을 사용하면 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="2540c-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="2540c-105">CI 기반 배포 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="2540c-106">[Azure Functions 배포 문서](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span></span>
>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="2540c-107">Azure에 앱 게시</span><span class="sxs-lookup"><span data-stu-id="2540c-107">Publishing your app to Azure</span></span>

<span data-ttu-id="2540c-108">Visual Studio 내부에서 Azure에 Azure 함수를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-108">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="2540c-109">이전 단원에서 로컬 Azure Functions 런타임이 계속 실행 중인 경우 해당 런타임을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-109">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="2540c-110">솔루션 탐색기에서 `ImHere.Functions` 앱을 마우스 오른쪽 단추로 클릭하고 *게시...* 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-110">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Functions 앱에서 마우스 오른쪽 단추를 클릭하여 게시](../media-drafts/8-right-click-publish.png)

1. <span data-ttu-id="2540c-112">**게시 대상 선택** 대화 상자에서 ‘Azure 함수 앱’을 선택하고 **Azure App Service**에 대해 *새로 만들기*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-112">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="2540c-113">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-113">Click **Publish**.</span></span>

    ![게시할 새 Azure App Service 만들기](../media-drafts/8-pick-publish-target.png)

1. <span data-ttu-id="2540c-115">Azure 계정이 두 개 이상 있고 올바른 계정이 선택되지 않은 경우 오른쪽 위에 있는 드롭다운에서 Azure 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-115">Select your Azure account from the drop-down in the top-right corner; if you have more than one Azure accounts and the right one isn't selected.</span></span>

1. <span data-ttu-id="2540c-116">Functions 앱에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-116">Give your Functions app a name.</span></span> <span data-ttu-id="2540c-117">이 이름은 Azure의 모든 Functions 앱에서 전체적으로 고유해야 하므로 “ImHere-\<YourName\>”과 같은 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-117">This name needs to be globally unique across all the Functions apps in the whole of Azure, so use something like "ImHere-\<YourName\>".</span></span>

1. <span data-ttu-id="2540c-118">이 Functions 앱을 만드는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-118">Select the subscription you want to create this Functions app under.</span></span>

1. <span data-ttu-id="2540c-119">**리소스 그룹** 드롭다운 옆에 있는 **새로 만들기...** 단추를 클릭하고 “ImHere”와 같은 이름을 지정하여 이 Functions 앱에 대한 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-119">Create a new resource group for this Functions app by clicking the **New...** button next to the **Resource Group** drop-down and giving it a name such as "ImHere".</span></span> <span data-ttu-id="2540c-120">리소스 그룹 이름은 Azure 전체에서 고유할 필요는 없지만 구독에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-120">Resource group names need to be unique to your subscription, not globally unique across Azure.</span></span> <span data-ttu-id="2540c-121">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-121">Then, click **OK**.</span></span>

    ![새 리소스 그룹 만들기](../media-drafts/8-create-new-resource-group.png)

   <span data-ttu-id="2540c-123">새 리소스 그룹을 만들면 나중에 쉽게 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-123">Creating a new resource group makes it easier to clean up later.</span></span> <span data-ttu-id="2540c-124">리소스 그룹을 삭제하면 이 Functions 앱에 대해 만든 모든 항목이 동시에 삭제됨을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-124">You can delete the resource group and know that everything you've created for this Functions app will all be deleted at the same time.</span></span>

1. <span data-ttu-id="2540c-125">**호스팅 플랜** 드롭다운 옆에 있는 **새로 만들기...** 단추를 클릭하여 새 호스팅 플랜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-125">Create a new hosting plan by clicking the **New...** button next to the **Hosting Plan** drop-down.</span></span> <span data-ttu-id="2540c-126">App Service 계획 이름은 기본적으로 앱 이름의 끝에 “Plan”을 추가하여 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-126">The App Service plan name will default to your app name with "Plan" on the end.</span></span> <span data-ttu-id="2540c-127">**위치**를 가장 가까운 위치로 설정하고 **크기**가 사용량에 맞게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-127">Set the **Location** to the closest location to you and make sure **Size** is set to consumption.</span></span> <span data-ttu-id="2540c-128">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-128">Then, click **OK**.</span></span>

    ![호스팅 플랜 구성](../media-drafts/8-configure-hosting-plan.png)

1. <span data-ttu-id="2540c-130">**저장소 계정** 드롭다운 옆에 있는 **새로 만들기...** 단추를 클릭하여 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-130">Create a new storage account by clicking the **New...** button next to the **Storage Account** drop-down.</span></span> <span data-ttu-id="2540c-131">기본 이름이 제공되므로 모든 기본값을 유지하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-131">A default name will be provided, so keep all the default values and click **OK**.</span></span>

    ![저장소 계정 만들기](../media-drafts/8-create-storage-account.png)

1. <span data-ttu-id="2540c-133">**만들기**를 클릭하여 Azure에 모든 리소스를 프로비전하고 Azure Functions 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-133">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![App Service 만들기](../media-drafts/8-create-app-service.png)

<span data-ttu-id="2540c-135">프로비저닝을 실행하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-135">Provisioning will take a couple of minutes or so to run.</span></span> <span data-ttu-id="2540c-136">다음 리소스가 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-136">The following resources will be provisioned:</span></span>

- <span data-ttu-id="2540c-137">Azure Functions 앱에 필요한 파일을 저장할 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="2540c-137">A storage account to store the files needed for the Azure Functions app</span></span>
- <span data-ttu-id="2540c-138">Azure Functions 앱에 필요한 계산 리소스를 관리할 App Service 계획</span><span class="sxs-lookup"><span data-stu-id="2540c-138">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
- <span data-ttu-id="2540c-139">Azure 함수를 실행하는 App Service</span><span class="sxs-lookup"><span data-stu-id="2540c-139">The App Service that runs the Azure function</span></span>

<span data-ttu-id="2540c-140">이제 함수가 게시되어 https://<your-app-name>.azurewebsites.net/api/SendLocation에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-140">The function will now be published and available to call at https://<your-app-name>.azurewebsites.net/api/SendLocation.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="2540c-141">앱 구성</span><span class="sxs-lookup"><span data-stu-id="2540c-141">Configuring your app</span></span>

<span data-ttu-id="2540c-142">Azure 함수가 로컬에서 실행되었을 때는 `local.settings.json` 파일에 저장된 Twilio 자격 증명을 사용하고 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-142">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="2540c-143">이름에서 알 수 있듯이, 이 파일은 Azure 설정이 아닌 로컬 설정에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-143">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="2540c-144">Azure 내부에서 Azure 함수를 호출하려면 먼저 `TwilioAccountSid` 및 `TwilioAuthToken` 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-144">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="2540c-145">게시 탭에서 **응용 프로그램 설정 관리** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-145">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![응용 프로그램 설정 관리 옵션](../media-drafts/8-application-settings-option.png)

1. <span data-ttu-id="2540c-147">**추가** 단추를 클릭하여 새 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-147">Click the **Add** button to add a new setting.</span></span> <span data-ttu-id="2540c-148">이름을 “TwilioAccountSid”로 지정하고 값을 Twilio 계정 SID로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-148">Name it "TwilioAccountSid" and set the value to your Twilio account SID.</span></span> <span data-ttu-id="2540c-149">“TwilioAuthToken” 이름을 사용하여 인증 토큰에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-149">Repeat this step for your Auth Token using the name "TwilioAuthToken".</span></span>

    ![응용 프로그램 설정에서 Twilio 자격 증명 설정](../media-drafts/8-set-creds-in-app-settings.png)

1. <span data-ttu-id="2540c-151">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-151">Click **OK**.</span></span>

1. <span data-ttu-id="2540c-152">**게시**를 클릭하여 새 응용 프로그램 설정으로 Azure Functions 앱을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-152">Click **Publish** to republish the Azure Functions app with the new application settings.</span></span>

    ![게시 단추](../media-drafts/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="2540c-154">모바일 앱에서 Azure 가리키기</span><span class="sxs-lookup"><span data-stu-id="2540c-154">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="2540c-155">게시 탭에서 값 옆에 있는 복사 단추를 사용하여 **사이트 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-155">From the Publish tab, copy the **Site URL** using the copy button next to the value.</span></span>

    ![게시 탭에서 사이트 URL 복사](../media-drafts/8-copy-site-url.png)

1. <span data-ttu-id="2540c-157">`ImHere` 프로젝트에서 `MainViewModel`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-157">Open the `MainViewModel` from the `ImHere` project.</span></span>

1. <span data-ttu-id="2540c-158">`baseUrl` 필드의 값을 게시 탭에서 복사한 사이트 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-158">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

1. <span data-ttu-id="2540c-159">이 값의 프로토콜을 `http`에서 `https`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-159">Change the protocol for this value from `http` to `https`.</span></span> <span data-ttu-id="2540c-160">사이트 URL은 항상 HTTP를 사용하여 제공되지만, Azure 함수를 호출하려면 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-160">The site URL is always given using HTTP, but you have to use HTTPS to call an Azure function.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="2540c-161">테스트</span><span class="sxs-lookup"><span data-stu-id="2540c-161">Test it out</span></span>

1. <span data-ttu-id="2540c-162">`ImHere.UWP` 앱을 시작 앱으로 설정하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-162">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

1. <span data-ttu-id="2540c-163">전화 번호를 입력하고 **위치 보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-163">Enter a phone number and click the **Send Location** button.</span></span>

1. <span data-ttu-id="2540c-164">위치가 SMS 메시지로 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-164">You should receive the location as an SMS message.</span></span>

## <a name="summary"></a><span data-ttu-id="2540c-165">요약</span><span class="sxs-lookup"><span data-stu-id="2540c-165">Summary</span></span>

<span data-ttu-id="2540c-166">이 단원에서는 Visual Studio 내부에서 Azure에 Azure Functions 프로젝트를 게시하고 응용 프로그램 설정을 구성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="2540c-166">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>