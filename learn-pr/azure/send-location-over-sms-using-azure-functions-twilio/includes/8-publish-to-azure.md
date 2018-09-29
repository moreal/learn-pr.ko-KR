<span data-ttu-id="26b2a-101">이제 앱과 Azure Function이 완료되어 로컬에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-101">The app and Azure Function are now complete and running locally.</span></span> <span data-ttu-id="26b2a-102">이 단원에서는 함수를 Azure에 게시하여 클라우드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-102">In this unit, you publish the function to Azure to run in the cloud.</span></span>

> [!Note]
> <span data-ttu-id="26b2a-103">Visual Studio에서 함수를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-103">You will publish your function from Visual Studio.</span></span> <span data-ttu-id="26b2a-104">이는 개념 증명, 프로토타입 및 학습용으로 시작하는 데 유용한 방법이지만, 프로덕션 품질 앱의 경우 이 방법을 사용하면 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="26b2a-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="26b2a-105">CI 기반 배포 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="26b2a-106">[Azure Functions 배포 문서](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true).</span></span>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="26b2a-107">Azure에 앱 게시</span><span class="sxs-lookup"><span data-stu-id="26b2a-107">Publishing your app to Azure</span></span>

<span data-ttu-id="26b2a-108">Visual Studio 내부에서 Azure에 Azure 함수를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-108">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="26b2a-109">이전 단원에서 로컬 Azure Functions 런타임이 계속 실행 중인 경우 해당 런타임을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-109">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="26b2a-110">솔루션 탐색기에서 `ImHere.Functions` 앱을 마우스 오른쪽 단추로 클릭하고 *게시...* 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-110">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Functions 앱에서 마우스 오른쪽 단추를 클릭하여 게시](../media/8-right-click-publish.png)

1. <span data-ttu-id="26b2a-112">**게시 대상 선택** 대화 상자에서 ‘Azure 함수 앱’을 선택하고 **Azure App Service**에 대해 *새로 만들기*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-112">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="26b2a-113">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-113">Click **Publish**.</span></span>

    ![게시할 새 Azure App Service 만들기](../media/8-pick-publish-target.png)

1. <span data-ttu-id="26b2a-115">이러한 지침의 **리소스** 탭에서 사용자 이름 및 암호를 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-115">Sign in to Azure using the username and password in the **Resources** tab of these instructions.</span></span> <span data-ttu-id="26b2a-116">VM을 사용하는 대신 로컬로 이 앱을 빌드하는 경우 Azure 계정으로 로그인하고, 대화 상자에서 링크를 사용하는 데 필요한 경우 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-116">If you are building this app locally instead of using the VM, log in with your Azure account, creating a new one if necessary using the links on the dialog.</span></span>

1. <span data-ttu-id="26b2a-117">Functions 앱을 실행하는 데 필요한 모든 인프라를 만들므로 모든 값을 기본값으로 내버려 둡니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-117">Leave all the values as the defaults, as this will create all the necessary infrastructure to run your Functions app.</span></span>

1. <span data-ttu-id="26b2a-118">**만들기**를 클릭하여 Azure에 모든 리소스를 프로비전하고 Azure Functions 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-118">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![App Service 만들기](../media/8-create-app-service.png)

1. <span data-ttu-id="26b2a-120">Azure에서 함수 버전을 업데이트하려는지를 묻는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-120">You may be asked if you want to update the functions version on Azure.</span></span> <span data-ttu-id="26b2a-121">이 대화 상자가 나타나면 **예**를 선택하여 함수 앱이 최신 Azure Functions 런타임 버전을 사용하여 게시됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-121">If this dialog appears, select **Yes** to ensure your function app is published with the latest Azure Functions runtime version.</span></span>
    <span data-ttu-id="26b2a-122">![Azure Functions 업데이트 대화 상자](../media/8-update-functions-on-azure.png)</span><span class="sxs-lookup"><span data-stu-id="26b2a-122">![The update Azure Functions dialog](../media/8-update-functions-on-azure.png)</span></span>

<span data-ttu-id="26b2a-123">프로비저닝을 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-123">Provisioning will take a couple of minutes to complete.</span></span> <span data-ttu-id="26b2a-124">다음 리소스가 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-124">The following resources will be provisioned:</span></span>

- <span data-ttu-id="26b2a-125">Azure Functions 앱에 필요한 파일을 저장할 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="26b2a-125">A storage account to store the files needed for the Azure Functions app</span></span>
- <span data-ttu-id="26b2a-126">Azure Functions 앱에 필요한 계산 리소스를 관리할 App Service 계획</span><span class="sxs-lookup"><span data-stu-id="26b2a-126">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
- <span data-ttu-id="26b2a-127">Azure 함수를 실행하는 App Service</span><span class="sxs-lookup"><span data-stu-id="26b2a-127">The App Service that runs the Azure function</span></span>

<span data-ttu-id="26b2a-128">이제 함수가 게시되어 **https://\<your-app-name\>.azurewebsites.net/api/SendLocation**에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-128">The function will now be published and available to call at **https://\<your-app-name\>.azurewebsites.net/api/SendLocation**.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="26b2a-129">앱 구성</span><span class="sxs-lookup"><span data-stu-id="26b2a-129">Configuring your app</span></span>

<span data-ttu-id="26b2a-130">Azure 함수가 로컬에서 실행되었을 때는 `local.settings.json` 파일에 저장된 Twilio 자격 증명을 사용하고 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-130">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="26b2a-131">이름에서 알 수 있듯이, 이 파일은 Azure 설정이 아닌 로컬 설정에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-131">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="26b2a-132">Azure 내부에서 Azure 함수를 호출하려면 먼저 `TwilioAccountSid` 및 `TwilioAuthToken` 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-132">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="26b2a-133">게시 탭에서 **응용 프로그램 설정 관리** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-133">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![응용 프로그램 설정 관리 옵션](../media/8-application-settings-option.png)

1. <span data-ttu-id="26b2a-135">**응용 프로그램 설정** 대화 상자에는 로컬 및 원격 값 모두를 포함한 응용 프로그램 설정이 표시됩니다. 로컬 값은 `local.settings.json` 파일에서 제공되며 원격 값은 Azure에서 호스팅될 때 사용자 함수가 사용할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-135">The **Application Settings** dialog will show application settings with both a local and remote value - the local coming from your `local.settings.json` file, and the remote value is the one your function will use when it is hosted in Azure.</span></span> <span data-ttu-id="26b2a-136">**TwilioAccountSid** 및 **TwilioAuthToken** 값의 경우 *로컬*에서 *원격* 상자로 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-136">Copy the values from the *Local* to the *Remote* boxes for the **TwilioAccountSid** and **TwilioAuthToken** values.</span></span>

    ![응용 프로그램 설정에서 Twilio 자격 증명 설정](../media/8-set-creds-in-app-settings.png)

1. <span data-ttu-id="26b2a-138">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-138">Click **OK**.</span></span> <span data-ttu-id="26b2a-139">그러면 Azure 함수 앱에 값이 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-139">This will publish the values to the Azure functions app.</span></span>

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="26b2a-140">모바일 앱에서 Azure 가리키기</span><span class="sxs-lookup"><span data-stu-id="26b2a-140">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="26b2a-141">게시 탭에서 값 옆에 있는 **클립보드로 복사** 단추를 사용하여 **사이트 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-141">From the Publish tab, copy the **Site URL** using the **Copy to clipboard** button next to the value.</span></span>

    ![게시 탭에서 사이트 URL 복사](../media/8-copy-site-url.png)

1. <span data-ttu-id="26b2a-143">`ImHere` 프로젝트에서 `MainViewModel`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-143">Open the `MainViewModel` from the `ImHere` project.</span></span>

1. <span data-ttu-id="26b2a-144">`baseUrl` 필드의 값이 게시 탭에서 복사한 사이트 URL이 되도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-144">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="26b2a-145">테스트</span><span class="sxs-lookup"><span data-stu-id="26b2a-145">Test it out</span></span>

1. <span data-ttu-id="26b2a-146">`ImHere.UWP` 앱을 시작 앱으로 설정하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-146">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

1. <span data-ttu-id="26b2a-147">전화 번호를 입력하고 **위치 보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-147">Enter a phone number and click the **Send Location** button.</span></span>

1. <span data-ttu-id="26b2a-148">위치가 SMS 메시지로 수신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-148">You should receive the location as an SMS message.</span></span>

1. <span data-ttu-id="26b2a-149">*사용할 수 없는 서비스* 오류가 다시 발생하면 함수 앱에서 사용 중인 "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet 패키지의 버전을 확인합니다. 해당 버전은 3.0.0이 아니라 3.0.0-rc1이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-149">If you get back a *Service Unavailable* error, check what version of the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package your functions app is using, it should be 3.0.0-rc1, NOT 3.0.0.</span></span>
1. <span data-ttu-id="26b2a-150">*사용할 수 없는 서비스* 오류가 다시 발생하면 함수 앱에서 사용 중인 "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet 패키지의 버전을 확인합니다. 해당 버전은 3.0.0이 **아니라** 3.0.0-rc1이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-150">If you get back a *Service Unavailable* error, check what version of the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package your functions app is using, it should be 3.0.0-rc1, **NOT** 3.0.0.</span></span>

## <a name="summary"></a><span data-ttu-id="26b2a-151">요약</span><span class="sxs-lookup"><span data-stu-id="26b2a-151">Summary</span></span>

<span data-ttu-id="26b2a-152">이 단원에서는 Visual Studio 내부에서 Azure에 Azure Functions 프로젝트를 게시하고 응용 프로그램 설정을 구성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="26b2a-152">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>