<span data-ttu-id="9767a-101">이제 Azure에서 앱을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="9767a-102">Azure App Service 앱을 만들고, MSI 및 자격 증명 모음 구성을 사용하여 앱을 설정하고, 코드를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-102">We need to create an Azure App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

## <a name="exercise"></a><span data-ttu-id="9767a-103">연습</span><span class="sxs-lookup"><span data-stu-id="9767a-103">Exercise</span></span>

### <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="9767a-104">App Service 계획 및 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9767a-104">Create the App Service plan and app</span></span>

<span data-ttu-id="9767a-105">App Service 만들기는 ‘계획’을 만든 후 ‘앱’을 만드는 2단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-105">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="9767a-106">‘플랜’ 이름은 구독 내에서만 고유해야 하므로 이전에 사용했던 동일한 이름을 사용할 수 있습니다. **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="9767a-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="9767a-107">앱 이름은 전역적으로 고유해야 하므로 사용자가 자신만의 이름을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="9767a-108">Azure Cloud Shell에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a><span data-ttu-id="9767a-109">앱에 구성 추가</span><span class="sxs-lookup"><span data-stu-id="9767a-109">Add configuration to the app</span></span>

<span data-ttu-id="9767a-110">Azure에 배포하려면 구성 파일 대신 응용 프로그램 설정에 구성을 넣는 App Service 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a><span data-ttu-id="9767a-111">MSI 사용</span><span class="sxs-lookup"><span data-stu-id="9767a-111">Enable MSI</span></span>

<span data-ttu-id="9767a-112">앱에서 MSI를 사용하도록 설정하는 것은 간단한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="9767a-113">결과로 생성되는 JSON 출력에서 **principalId** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="9767a-114">PrincipalId는 Azure Active Directory에서 앱의 새 ID 중 고유 ID이며 다음 단계에서 이 ID를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

### <a name="grant-access-to-the-vault"></a><span data-ttu-id="9767a-115">자격 증명 모음에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="9767a-115">Grant access to the vault</span></span>

<span data-ttu-id="9767a-116">이제 앱 ID 권한을 제공하여 프로덕션 환경 자격 증명 모음의 비밀을 가져오고 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-116">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="9767a-117">이전 단계에서 복사한 **principalId** 값을 아래 명령에서 **object-id**의 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="9767a-118">앱을 배포하고 사용해 보기</span><span class="sxs-lookup"><span data-stu-id="9767a-118">Deploy the app and try it out</span></span>

<span data-ttu-id="9767a-119">모든 구성이 설정되고 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-119">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="9767a-120">아래 명령은 사이트를 `pub` 폴더에 게시하고, `site.zip`으로 압축하고, 해당 Zip 파일을 App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="9767a-121">아직 이동하지 않은 경우에는 `cd`를 실행하여 다시 KeyVaultDemoApp 디렉터리로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="9767a-122">사이트가 배포되었음을 나타내는 결과가 표시되면 브라우저에서 `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="9767a-123">비밀 값 **reindeer_flotilla**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="9767a-124">앱이 완료되어 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9767a-124">Your app is finished and deployed!</span></span>