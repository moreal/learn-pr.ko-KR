## <a name="creating-key-vaults-for-your-applications"></a><span data-ttu-id="fb41d-101">응용 프로그램에 대한 Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="fb41d-101">Creating Key Vaults for your applications</span></span>

<span data-ttu-id="fb41d-102">개발, 테스트, 프로덕션과 같이 각 응용 프로그램의 각 배포 환경을 위한 별도의 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-102">Good practice is to create a separate vault for each deployment environment of each of your applications, such as development, test, and production.</span></span> <span data-ttu-id="fb41d-103">자격 증명 모음을 사용하여 여러 앱 간에 비밀을 공유할 수 있지만, 공격자가 자격 증명 모음에 대한 읽기 권한을 얻으면 자격 증명 모음의 비밀 수가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-103">It's possible to use vaults to share secrets across multiple apps, but the impact of an attacker gaining read access to a vault increases with the number of secrets in the vault.</span></span>

> [!TIP]
> <span data-ttu-id="fb41d-104">응용 프로그램에 대한 서로 다른 환경에서 비밀에 동일한 이름을 사용하는 경우 앱의 환경 관련 구성에서는 자격 증명 모음 URL만 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-104">If you use the same names for secrets across different environments for an application, the only environment-specific configuration that has to change in your app is the vault URL.</span></span>

<span data-ttu-id="fb41d-105">자격 증명 모음을 만드는 데 초기 구성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-105">Creating a vault requires no initial configuration.</span></span> <span data-ttu-id="fb41d-106">사용자 ID에 전체 비밀 관리 권한 집합이 자동으로 부여되므로 즉시 비밀 추가를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-106">Your user identity is automatically granted the full set of secret management permissions and you can start adding secrets immediately.</span></span> <span data-ttu-id="fb41d-107">자격 증명 모음이 있으면 Azure Portal, Azure CLI 및 Azure PowerShell 등 모든 Azure 관리 인터페이스에서 비밀을 추가하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-107">Once you have a vault, adding and managing secrets can be done from any Azure administrative interface, including the Azure portal, the Azure CLI, and Azure PowerShell.</span></span> <span data-ttu-id="fb41d-108">자격 증명 모음을 사용하도록 응용 프로그램을 설정할 경우 응용 프로그램에 올바른 권한을 할당해야 합니다. 다음 단원에서 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-108">When you set up your application to use the vault, you'll need to assign the correct permissions to it; we'll see that in the next unit.</span></span>

## <a name="vault-authentication-and-permissions"></a><span data-ttu-id="fb41d-109">자격 증명 모음 인증 및 권한</span><span class="sxs-lookup"><span data-stu-id="fb41d-109">Vault authentication and permissions</span></span>

<span data-ttu-id="fb41d-110">Azure Key Vault의 API는 Azure Active Directory를 사용하여 사용자와 응용 프로그램을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-110">Azure Key Vault's API uses Azure Active Directory to authenticate users and applications.</span></span> <span data-ttu-id="fb41d-111">자격 증명 모음 액세스 정책은 ‘작업’을 기반으로 하고 전체 자격 증명 모음에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-111">Vault access policies are based on *actions*, and are applied across an entire vault.</span></span> <span data-ttu-id="fb41d-112">예를 들어 자격 증명 모음에 대한 **Get**(비밀 값 읽기), **List**(모든 비밀의 이름 나열) 및 **Set**(비밀 값 만들기 또는 업데이트) 권한을 가진 응용 프로그램은 비밀을 만들고, 모든 비밀 이름을 나열하고, 해당 자격 증명 모음의 모든 비밀 값을 가져오고 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-112">For example, an application with **Get** (read secret values), **List** (list names of all secrets), and **Set** (create or update secret values) permissions to a vault is able to create secrets, list all secret names, and get and set all secret values in that vault.</span></span>

<span data-ttu-id="fb41d-113">자격 증명 모음에서 수행되는 ‘모든’ 작업에는 인증과 권한 부여가 필요합니다. 어떤 종류든 익명 액세스 권한을 부여할 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-113">*All* actions performed on a vault require authentication and authorization &mdash; there is no way to grant any kind of anonymous access.</span></span>

> [!TIP]
> <span data-ttu-id="fb41d-114">개발자 및 앱에 대한 자격 증명 모음 액세스 권한을 부여할 경우 필요한 최소 권한 집합만 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-114">When granting vault access to developers and apps, grant only the minimum set of permissions needed.</span></span> <span data-ttu-id="fb41d-115">권한 제한 사항을 적용하면 코드 버그로 인해 발생하는 사고를 방지하고 앱에 삽입되는 도난 당한 자격 증명 또는 악의적인 코드의 영향을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-115">Permissions restrictions help avoid accidents caused by code bugs and reduce the impact of stolen credentials or malicious code injected into your app.</span></span>

<span data-ttu-id="fb41d-116">일반적으로 개발자는 개발 환경 자격 증명 모음에 대한 **Get** 및 **List** 권한만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-116">Developers will usually only need **Get** and **List** permissions to a development-environment vault.</span></span> <span data-ttu-id="fb41d-117">책임 또는 선임 개발자는 필요한 경우 비밀을 변경하고 추가하기 위해 자격 증명 모음에 대한 전체 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-117">A lead or senior developer will need full permissions to the vault to change and add secrets when necessary.</span></span> <span data-ttu-id="fb41d-118">일반적으로 프로덕션 환경 자격 증명 모음에 대한 전체 권한은 선임 작업 직원용으로 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-118">Full permissions to production-environment vaults are typically reserved for senior operations staff.</span></span>

<span data-ttu-id="fb41d-119">앱의 경우 일반적으로 **Get** 권한만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-119">For apps, typically only **Get** permissions are required.</span></span> <span data-ttu-id="fb41d-120">일부 앱의 경우 앱이 구현되는 방식에 따라 **List**가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-120">Some apps may require **List** depending on the way the app is implemented.</span></span> <span data-ttu-id="fb41d-121">이 모듈의 연습에서 구현하는 앱의 경우 앱이 자격 증명 모음에서 비밀을 읽는 데 사용하는 방법 때문에 **List** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-121">The app we'll implement in this module's exercise requires the **List** permission because of the technique it uses to read secrets from the vault.</span></span>

## <a name="exercise"></a><span data-ttu-id="fb41d-122">연습</span><span class="sxs-lookup"><span data-stu-id="fb41d-122">Exercise</span></span>

<span data-ttu-id="fb41d-123">응용 프로그램 비밀과 관련해서 회사에서 발생하는 모든 문제의 경우 관리 부서에서는 다른 개발자에게 올바른 경로를 제시할 수 있는 작은 시작 앱을 만들도록 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-123">Given all the trouble the company's been having with application secrets, management has asked you to create a small starter app to set the other developers on the right path.</span></span> <span data-ttu-id="fb41d-124">앱에서는 가능한 한 간단하고 안전하게 비밀을 관리하는 모범 사례를 제시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-124">The app needs to demonstrate best practices for managing secrets as simply and securely as possible.</span></span>

<span data-ttu-id="fb41d-125">시작하려면 자격 증명 모음을 만들고 하나의 비밀을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-125">To start, you'll create a vault and store one secret.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="fb41d-126">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="fb41d-126">Create a resource group</span></span>

<span data-ttu-id="fb41d-127">이 연습에 있는 모든 리소스에 대한 `keyvault-exercise-group`라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-127">Create a resource group called `keyvault-exercise-group` for all of the resources in this exercise.</span></span> <span data-ttu-id="fb41d-128">이 모듈이 끝날 때 이 리소스 그룹을 삭제하여 모든 항목을 한 번에 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-128">At the end of this module, we'll be deleting this resource group to clean up everything at once.</span></span> <span data-ttu-id="fb41d-129">`eastus`를 이 연습에 있는 모든 항목의 위치로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-129">We'll use `eastus` as the location for everything in this exercise.</span></span>

<span data-ttu-id="fb41d-130">오른쪽에 있는 Azure Cloud Shell 터미널을 사용하여 다음 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-130">Use the Azure Cloud Shell terminal on the right to run the following Azure CLI command.</span></span> <span data-ttu-id="fb41d-131">이렇게 하면 구독에 리소스 그룹이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-131">This will create the resource group in your subscription.</span></span>

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a><span data-ttu-id="fb41d-132">자격 증명 모음을 만들고 그 안에 비밀을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-132">Create the vault and store the secret in it</span></span>

<span data-ttu-id="fb41d-133">그런 다음, 자격 증명 모음을 만들고 그 안에 비밀을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-133">Next, we'll create the vault and store our secret in it.</span></span>

<span data-ttu-id="fb41d-134">**Key Vault 이름은 전역적으로 고유해야 하므로 고유 이름을 선택해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="fb41d-134">**Key Vault names must be globally unique, so you'll need to pick a unique name**.</span></span> <span data-ttu-id="fb41d-135">자격 증명 모음 이름은 3-24자로, 영숫자 및 대시만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-135">Vault names must be 3-24 characters long and contain only alphanumeric characters and dashes.</span></span>

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

<span data-ttu-id="fb41d-136">완료되면 새 자격 증명 모음을 설명하는 JSON 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-136">When it finishes, you'll see JSON output describing the new vault.</span></span>

<span data-ttu-id="fb41d-137">이제 비밀을 추가합니다. 비밀의 이름은 **SecretPassword**로 지정되고 값은 **reindeer_flotilla**입니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-137">Now add the secret: our secret will be named **SecretPassword** with a value of **reindeer_flotilla**.</span></span>

```azurecli
az keyvault secret set --name SecretPassword --value reindeer_flotilla --vault-name <your-unique-vault-name>
```

<span data-ttu-id="fb41d-138">곧 다시 필요하게 되므로 자격 증명 모음 이름을 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="fb41d-138">Make a note of the vault name &mdash; you'll be needing it again soon.</span></span>

<span data-ttu-id="fb41d-139">응용 프로그램에 대한 코드는 금방 작성하지만, 먼저 앱이 자격 증명 모음에 인증되는 방법을 조금 알아봐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb41d-139">We'll write the code for our application shortly, but first we need to learn a little bit about how our app is going to authenticate to a vault.</span></span>