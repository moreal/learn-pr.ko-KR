<span data-ttu-id="539ed-101">컨테이너 이미지는 Azure Container Instances, Azure Kubernetes 레지스트리, Windows 또는 Mac용 Docker 등 여러 컨테이너 관리 플랫폼의 Azure Container Registry에서 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-101">Container images can be pulled from Azure Container Registry from many container management platforms, such as Azure Container Instances, Azure Kubernetes Registry, and Docker for Windows or Mac.</span></span> <span data-ttu-id="539ed-102">Azure Container Registry에서 컨테이너 이미지를 실행하는 경우 인증 자격 증명이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-102">When running container images from Azure Container Registry, authentication credentials may be needed.</span></span> <span data-ttu-id="539ed-103">Container Registry에서의 인증에는 Azure 서비스 주체를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-103">It is recommended to use an Azure service principal for authentication with Container Registry.</span></span> <span data-ttu-id="539ed-104">또한 Azure Key Vault에서 Azure 서비스 주체 자격 증명을 보호하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-104">Furthermore, it is also recommended to secure the Azure service principal credentials in Azure Key Vault.</span></span>

<span data-ttu-id="539ed-105">이 단원에서는 Azure Container Registry용 서비스 주체를 만들고 Azure Key Vault에 저장한 후 서비스 주체의 자격 증명을 사용하여 Azure Container Instances에 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-105">In this unit, you will create a service principal for your Azure container registry, store it in Azure Key Vault, and then deploy the container to Azure Container Instances using the service principal's credentials.</span></span>

## <a name="configure-registry-authentication"></a><span data-ttu-id="539ed-106">레지스트리 인증 구성</span><span class="sxs-lookup"><span data-stu-id="539ed-106">Configure registry authentication</span></span>

<span data-ttu-id="539ed-107">모든 프로덕션 시나리오에서는 서비스 주체를 사용하여 Azure Container Registry에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-107">All production scenarios should use service principals to access an Azure container registry.</span></span> <span data-ttu-id="539ed-108">서비스 주체를 통해 컨테이너 이미지에 대해 RBAC(역할 기반 액세스 제어)를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-108">Service principals allow you to provide role-based access control (RBAC) to your container images.</span></span> <span data-ttu-id="539ed-109">예를 들어, 레지스트리에 대해 끌어오기 전용 액세스 권한을 가지는 서비스 주체를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-109">For example, you can configure a service principal with pull-only access to a registry.</span></span>

<span data-ttu-id="539ed-110">Azure Key Vault에 자격 증명 모음이 아직 없는 경우 Azure CLI에서 다음 명령을 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-110">If you don't already have a vault in Azure Key Vault, create one with the Azure CLI using the following commands.</span></span>

<span data-ttu-id="539ed-111">먼저 컨테이너 레지스트리 이름으로 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-111">First, create a variable with the name of your container registry.</span></span> <span data-ttu-id="539ed-112">이 변수는 이 단원 전체에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-112">This variable is used throughout this unit.</span></span>

```azurecli
ACR_NAME=<acrName>
```

<span data-ttu-id="539ed-113">`az keyvault create` 명령을 사용하여 Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-113">Create an Azure key vault with the `az keyvault create` command.</span></span>

```azurecli
az keyvault create --resource-group myResourceGroup --name $ACR_NAME-keyvault
```

<span data-ttu-id="539ed-114">이제 서비스 주체를 만들고 해당 자격 증명을 주요 자격 증명 모음에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-114">Now, you need to create a service principal and store its credentials in your key vault.</span></span>

<span data-ttu-id="539ed-115">`az ad sp create-for-rbac` 명령을 사용하여 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-115">Use the `az ad sp create-for-rbac` command to create the service principal.</span></span> <span data-ttu-id="539ed-116">`--role` 인수는 *읽기 권한자* 역할을 사용하여 서비스 주체를 구성하고, 레지스트리에 대해 끌어오기 전용 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-116">The `--role` argument configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span></span> <span data-ttu-id="539ed-117">밀어넣기 및 끌어오기 액세스 권한을 부여하려면 `--role` 인수를 *contributor*로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-117">To grant both push and pull access, change the `--role` argument to *contributor*.</span></span>

```azurecli
az ad sp create-for-rbac --scopes $(az acr show --name $ACR_NAME --query id --output tsv) --role reader
```

<span data-ttu-id="539ed-118">서비스 주체 만들기 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-118">This is what the output of the service principal creation will look like.</span></span> <span data-ttu-id="539ed-119">`appId` 및 `password` 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-119">Take note of the `appId` and the `password` values.</span></span> <span data-ttu-id="539ed-120">이러한 값은 Azure Key Vault에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-120">These will be stored in the Azure key vault.</span></span>

```bash
{
  "appId": "1fa05179-0000-0000-0000-e269a4e97c41",
  "displayName": "azure-cli-2018-08-19-22-35-26",
  "name": "http://azure-cli-2018-08-19-22-35-26",
  "password": "72377509-0000-0000-0000-c8edbcb2d950",
  "tenant": "00000000-0000-0000-0000-000000000000"
}
```

<span data-ttu-id="539ed-121">그런 다음, `az keyvault secret set` 명령을 사용하여 서비스 주체의 *appId*를 자격 증명 모음에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-121">Next, use the `az keyvault secret set` command to store the service principal's *appId* in the vault.</span></span> <span data-ttu-id="539ed-122">`<appId>`를 서비스 주체의 `appId`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-122">Replace `<appId>` with the `appId` of the service principal.</span></span>

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --value <appId>
```

<span data-ttu-id="539ed-123">이제 `az keyvault secret set` 명령을 사용하여 서비스 주체의 *암호*를 자격 증명 모음에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-123">Now, use the `az keyvault secret set` command to store the service principal's *password* in the vault.</span></span> <span data-ttu-id="539ed-124">`<password>`를 서비스 주체의 `password`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-124">Replace `<password>` with the `password` of the service principal.</span></span>

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --value <password>
```

<span data-ttu-id="539ed-125">Azure Key Vault를 만들고 다음 두 비밀을 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-125">You've created an Azure key vault and stored two secrets in it:</span></span>

* <span data-ttu-id="539ed-126">`$ACR_NAME-pull-usr`: 서비스 주체 ID로, 컨테이너 레지스트리 **username**으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-126">`$ACR_NAME-pull-usr`: The service principal ID, for use as the container registry **username**.</span></span>
* <span data-ttu-id="539ed-127">`$ACR_NAME-pull-pwd`: 서비스 주체 암호로, 컨테이너 레지스트리 **password**로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-127">`$ACR_NAME-pull-pwd`: The service principal password, for use as the container registry **password**.</span></span>

<span data-ttu-id="539ed-128">이제 사용자나 응용 프로그램 및 서비스가 레지스트리에서 이미지를 끌어올 때 이러한 비밀을 이름으로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-128">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span></span>

### <a name="deploy-a-container-with-azure-cli"></a><span data-ttu-id="539ed-129">Azure CLI를 사용하여 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="539ed-129">Deploy a container with Azure CLI</span></span>

<span data-ttu-id="539ed-130">서비스 주체 자격 증명은 Azure Key Vault에 저장되므로, 응용 프로그램 및 서비스는 해당 자격 증명을 사용하여 개인 레지스트리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-130">Now that the service principal credentials are stored in Azure Key Vault, your applications and services can use them to access your private registry.</span></span>

<span data-ttu-id="539ed-131">다음 `az container create` 명령을 실행하여 컨테이너 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-131">Execute the following `az container create` command to deploy a container instance.</span></span> <span data-ttu-id="539ed-132">이 명령은 Azure Key Vault에 저장된 서비스 주체의 자격 증명을 사용하여 컨테이너 레지스트리를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-132">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry.</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name acr-build \
    --image $ACR_NAME.azurecr.io/helloacrbuild:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --ip-address Public \
    --registry-username $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --query value -o tsv)
```

<span data-ttu-id="539ed-133">Azure 컨테이너 인스턴스의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-133">Get the IP address of the Azure container instance.</span></span>

```azurecli
az container show --resource-group myResourceGroup --name acr-build --query ipAddress.ip --output table
```

<span data-ttu-id="539ed-134">브라우저를 열고 컨테이너의 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-134">Open up a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="539ed-135">모든 항목이 올바르게 구성되면 다음 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="539ed-135">If everything has been configured correctly, you should see the following results:</span></span>

![Hello World 텍스트가 있는 샘플 웹 응용 프로그램](../media/hello.png)

