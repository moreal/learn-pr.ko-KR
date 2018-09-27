<span data-ttu-id="db534-101">컨테이너 인스턴스에서 환경 변수를 사용하면 컨테이너가 실행하는 응용 프로그램 또는 스크립트의 동적 구성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-101">Environment variables in your container instances allow you to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="db534-102">컨테이너를 만들 때 Azure CLI, PowerShell 또는 Azure Portal을 사용하여 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-102">You can use the Azure CLI, PowerShell, or the Azure portal to set variables when you create the container.</span></span> <span data-ttu-id="db534-103">보안 환경 변수는 중요한 정보가 컨테이너 출력에 표시되지 않도록 방지하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db534-103">Secured environment variables are used to prevent sensitive information from being displayed in container output.</span></span>

<span data-ttu-id="db534-104">여기에서 Azure Cosmos DB 인스턴스를 만들고 환경 변수를 사용하여 연결 정보를 Azure Container Instance에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="db534-104">Here, you will create an Azure Cosmos DB instance and use environment variables to pass the connection information to an Azure container instance.</span></span> <span data-ttu-id="db534-105">컨테이너의 응용 프로그램은 해당 변수를 사용하여 Cosmos DB에서 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="db534-105">An application in the container uses the variables to write and read data from Cosmos DB.</span></span> <span data-ttu-id="db534-106">환경 변수와 보안 환경 변수 모두를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db534-106">You will create both an environment variable and a secured environment variable.</span></span>

## <a name="deploy-azure-cosmos-db"></a><span data-ttu-id="db534-107">Azure Cosmos DB 배포</span><span class="sxs-lookup"><span data-stu-id="db534-107">Deploy Azure Cosmos DB</span></span>

<span data-ttu-id="db534-108">`az cosmosdb create` 명령을 사용하여 Azure Cosmos DB 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db534-108">Create the Azure Cosmos DB instance with the `az cosmosdb create` command.</span></span> <span data-ttu-id="db534-109">또한 이 예제에서는 *COSMOS_DB_ENDPOINT*라는 변수에 Azure Cosmos DB 엔드포인트 주소를 배치하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="db534-109">This example will also place the Azure Cosmos DB endpoint address in a variable named *COSMOS_DB_ENDPOINT*.</span></span> <span data-ttu-id="db534-110">`[cosmos-db-name]`에 고유한 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db534-110">You'll need to supply a unique name for `[cosmos-db-name]`.</span></span>

<span data-ttu-id="db534-111">이 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-111">This command can take a few minutes to complete:</span></span>

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query documentEndpoint --output tsv)
```

<span data-ttu-id="db534-112">그런 다음, `az cosmosdb list-keys` 명령을 사용하여 Azure Cosmos DB 연결 키를 가져온 후 *COSMOS_DB_MASTERKEY*라는 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="db534-112">Next, get the Azure Cosmos DB connection key with the `az cosmosdb list-keys` command and store it in a variable named *COSMOS_DB_MASTERKEY*.</span></span> <span data-ttu-id="db534-113">`[cosmos-db-name]`을 다시 바꾸는 것을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="db534-113">Don't forget to replace `[cosmos-db-name]` again:</span></span>

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query primaryMasterKey --output tsv)
```

## <a name="deploy-a-container-instance"></a><span data-ttu-id="db534-114">컨테이너 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="db534-114">Deploy a container instance</span></span>

<span data-ttu-id="db534-115">`az container create` 명령을 사용하여 Azure 컨테이너 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db534-115">Create an Azure container instance using the `az container create` command.</span></span> <span data-ttu-id="db534-116">두 개의 환경 변수인 `COSMOS_DB_ENDPOINT` 및 `COSMOS_DB_MASTERKEY`가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db534-116">Take note that two environment variables are created, `COSMOS_DB_ENDPOINT` and `COSMOS_DB_MASTERKEY`.</span></span> <span data-ttu-id="db534-117">이러한 변수는 Azure Cosmos DB 인스턴스에 연결하는 데 필요한 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="db534-117">These variables hold the values needed to connect to the Azure Cosmos DB instance:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

<span data-ttu-id="db534-118">컨테이너가 만들어지면 `az container show` 명령을 사용하여 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db534-118">Once the container has been created, get the IP address with the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --query ipAddress.ip \
    --output tsv
```

<span data-ttu-id="db534-119">브라우저를 열고 컨테이너의 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db534-119">Open a browser and navigate to the IP address of the container.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="db534-120">컨테이너가 완전히 시작되고 연결을 수신할 수 있을 때까지 1~2분 정도 걸리는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-120">Sometimes containers take a minute or two to fully start up and be able to receive connections.</span></span> <span data-ttu-id="db534-121">브라우저에서 IP 주소로 이동할 때 응답이 없는 경우 몇 분 정도 기다렸다가 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="db534-121">If there's no response when you navigate to the IP address in your browser,  wait a few moments and refresh the page.</span></span>

 <span data-ttu-id="db534-122">앱을 사용할 수 있게 되면 다음 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db534-122">Once the app is available, you should see the following application.</span></span> <span data-ttu-id="db534-123">투표를 진행하면 해당 투표 내용이 Azure Cosmos DB 인스턴스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="db534-123">When casting a vote, the vote is stored in the Azure Cosmos DB instance.</span></span>

![두 가지 선택 사항인 고양이와 강아지가 표시되는 Azure 투표 응용 프로그램입니다.](../media/4-azure-vote.png)

## <a name="secured-environment-variables"></a><span data-ttu-id="db534-125">보안 환경 변수</span><span class="sxs-lookup"><span data-stu-id="db534-125">Secured environment variables</span></span>

<span data-ttu-id="db534-126">이전 연습에서는 두 개의 환경 변수에 저장된 Azure Cosmos DB에 대한 연결 정보를 사용하여 컨테이너가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-126">In the previous exercise, a container was created with connection information for Azure Cosmos DB stored in two environment variables.</span></span> <span data-ttu-id="db534-127">기본적으로 환경 변수는 Azure Portal 및 명령줄 도구에 일반 텍스트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db534-127">By default, environment variables are displayed in the Azure portal and command-line tools in plain text.</span></span>

<span data-ttu-id="db534-128">예를 들어 `az container show` 명령을 사용하여 이전 연습에서 만든 컨테이너에 대한 정보를 가져오는 경우 해당 환경 변수에 일반 텍스트로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-128">For example, if you get information about the container created in the previous exercise with the `az container show` command, the environment variables are accessible in plain text:</span></span>

```azurecli
az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name aci-demo --query containers[0].environmentVariables
```

<span data-ttu-id="db534-129">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="db534-129">Example output:</span></span>

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": "https://aci-cosmos.documents.azure.com:443/"
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": "Xm5BwdLlCllBvrR26V00000000S2uOusuglhzwkE7dOPMBQ3oA30n3rKd8PKA13700000000095ynys863Ghgw=="
  }
]
```

보안 환경 변수로 인해 명확한 텍스트 출력이 표시되지 않습니다. <span data-ttu-id="db534-131">보안 환경 변수를 사용하려면 `--environment-variables` 인수를 `--secure-environment-variables` 인수로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db534-131">To use secure environment variables, replace the `--environment-variables` argument with the `--secure-environment-variables` argument.</span></span>

<span data-ttu-id="db534-132">다음 예제를 실행하여 보안 환경 변수를 활용하는 *aci-demo-secure*라는 컨테이너를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="db534-132">Run the following example to create a container named *aci-demo-secure* that utilizes secured environment variables:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

<span data-ttu-id="db534-133">이제 `az container show` 명령을 사용하여 컨테이너가 반환될 때 환경 변수가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db534-133">Now, when the container is returned with the `az container show` command, the environment variables are not displayed:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --query containers[0].environmentVariables
```

<span data-ttu-id="db534-134">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="db534-134">Example output:</span></span>

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": null
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": null
  }
]
```