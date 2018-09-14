<span data-ttu-id="9ed79-101">Container instances에서 환경 변수를 사용 하면 응용 프로그램 또는 컨테이너에서 실행 되는 스크립트의 동적 구성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-101">Environment variables in your container instances allow you to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="9ed79-102">컨테이너를 만들 때 변수를 설정 하려면 Azure CLI, PowerShell 또는 Azure portal을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-102">You use the Azure CLI, PowerShell, or the Azure portal to set variables when you create the container.</span></span> <span data-ttu-id="9ed79-103">보안 환경 변수는 민감한 정보가 컨테이너 조작 출력에 표시되지 않도록 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-103">Secured environment variables are used to prevent sensitive information from being displayed in container operations output.</span></span>

<span data-ttu-id="9ed79-104">여기에서 Azure Cosmos DB 인스턴스 및 연결 정보를 Azure container instance를 전달할 환경 변수를 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-104">Here, you will create an Azure Cosmos DB instance and use environment variables to pass the connection information to an Azure container instance.</span></span> <span data-ttu-id="9ed79-105">컨테이너에서 응용 프로그램에서는 Cosmos DB에서 데이터를 읽고 쓰는 데 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-105">An application in the container uses the variables to write and read data from Cosmos DB.</span></span> <span data-ttu-id="9ed79-106">환경 변수 및 보안된 환경 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-106">You will create both an environment variable and a secured environment variable.</span></span>

## <a name="deploy-azure-cosmos-db"></a><span data-ttu-id="9ed79-107">Azure Cosmos DB 배포</span><span class="sxs-lookup"><span data-stu-id="9ed79-107">Deploy Azure Cosmos DB</span></span>

<span data-ttu-id="9ed79-108">`az Azure Cosmos DB create` 명령을 사용하여 Azure Cosmos DB 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-108">Create the Azure Cosmos DB instance with the `az Azure Cosmos DB create` command.</span></span> <span data-ttu-id="9ed79-109">또한 이 예제에서는 *COSMOS_DB_ENDPOINT*라는 변수에 Azure Cosmos DB 엔드포인트 주소를 배치하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-109">This example will also place the Azure Cosmos DB endpoint address in a variable named *COSMOS_DB_ENDPOINT*.</span></span>

<span data-ttu-id="9ed79-110">이 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-110">This command can take a few minutes to complete:</span></span>

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group <rgn>[Sandbox resource group name]</rgn> --name aci-cosmos --query documentEndpoint -o tsv)
```

<span data-ttu-id="9ed79-111">그런 다음, `az cosmosdb list-keys` 명령을 사용하여 Azure Cosmos DB 연결 키를 가져와 *COSMOS_DB_MASTERKEY*라는 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-111">Next, get the Azure Cosmos DB connection key with the `az cosmosdb list-keys` command and store it in a variable named *COSMOS_DB_MASTERKEY*:</span></span>

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group <rgn>[Sandbox resource group name]</rgn> --name aci-cosmos --query primaryMasterKey -o tsv)
```

## <a name="deploy-a-container-instance"></a><span data-ttu-id="9ed79-112">컨테이너 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="9ed79-112">Deploy a container instance</span></span>

<span data-ttu-id="9ed79-113">`az container create` 명령을 사용하여 Azure 컨테이너 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-113">Create an Azure container instance using the `az container create` command.</span></span> <span data-ttu-id="9ed79-114">두 개의 환경 변수인 `COSMOS_DB_ENDPOINT` 및 `COSMOS_DB_ENDPOINT`가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-114">Take note that two environment variables are created, `COSMOS_DB_ENDPOINT` and `COSMOS_DB_ENDPOINT`.</span></span> <span data-ttu-id="9ed79-115">이러한 변수는 Azure Cosmos DB 인스턴스에 연결하는 데 필요한 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-115">These variables hold the values needed to connect to the Azure Cosmos DB instance:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

<span data-ttu-id="9ed79-116">컨테이너가 만들어지면 `az container show` 명령을 사용하여 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-116">Once the container has been created, get the IP address with the `az container show` command:</span></span>

```azurecli
az container show --resource-group <rgn>[Sandbox resource group name]</rgn> --name aci-demo --query ipAddress.ip --output tsv
```

<span data-ttu-id="9ed79-117">브라우저를 열고 컨테이너의 IP 주소로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-117">Open a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="9ed79-118">다음 응용 프로그램이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-118">You should see the following application.</span></span> <span data-ttu-id="9ed79-119">응답으로 캐스팅할 때 응답이 Azure Cosmos DB 인스턴스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-119">When casting a vote, the vote is stored in the Azure Cosmos DB instance.</span></span>

![두 가지 선택 사항인 고양이와 강아지가 표시되는 Azure 투표 응용 프로그램.](../media-draft/azure-vote.png)

## <a name="secured-environment-variables"></a><span data-ttu-id="9ed79-121">보안 환경 변수</span><span class="sxs-lookup"><span data-stu-id="9ed79-121">Secured environment variables</span></span>

<span data-ttu-id="9ed79-122">이전 연습에서는 두 개의 환경 변수에 저장된 Azure Cosmos DB에 대한 연결 정보를 사용하여 컨테이너가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-122">In the previous exercise, a container was created with connection information for Azure Cosmos DB stored in two environment variables.</span></span> <span data-ttu-id="9ed79-123">기본적으로 환경 변수는 Azure Portal 및 명령줄 도구에 일반 텍스트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-123">By default, environment variables are displayed in the Azure portal and command-line tools in plain text.</span></span>

<span data-ttu-id="9ed79-124">예를 들어 `az container show` 명령을 사용하여 이전 연습에서 만든 컨테이너에 대한 정보를 가져오는 경우 해당 환경 변수에 일반 텍스트로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-124">For example, if you get information about the container created in the previous exercise with the `az container show` command, the environment variables are accessible in plain text:</span></span>

```azurecli
az container show --resource-group <rgn>[Sandbox resource group name]</rgn> --name aci-demo --query containers[0].environmentVariables
```

<span data-ttu-id="9ed79-125">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="9ed79-125">Example output:</span></span>

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

보안 환경 변수로 인해 명확한 텍스트 출력이 표시되지 않습니다. <span data-ttu-id="9ed79-127">보안 환경 변수를 사용하려면 `--environment-variables` 인수를 `--secure-environment-variables` 인수로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-127">To use secure environment variables, replace the `--environment-variables` argument with the `--secure-environment-variables` argument.</span></span>

<span data-ttu-id="9ed79-128">다음 예제를 실행하여 보안 환경 변수를 활용하는 *aci-demo-secure*라는 컨테이너를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="9ed79-128">Run the following example to create a container named *aci-demo-secure* that utilizes secured environment variables:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

<span data-ttu-id="9ed79-129">이제 `az container show` 명령을 사용하여 컨테이너가 반환될 때 환경 변수가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed79-129">Now, when the container is returned with the `az container show` command, the environment variables are not displayed:</span></span>

```azurecli
az container show --resource-group <rgn>[Sandbox resource group name]</rgn> --name aci-demo-secure --query containers[0].environmentVariables
```

<span data-ttu-id="9ed79-130">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="9ed79-130">Example output:</span></span>

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