<span data-ttu-id="99026-101">컨테이너 인스턴스에서 환경 변수를 설정하면 컨테이너가 실행하는 응용 프로그램 또는 스크립트의 동적 구성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99026-101">Setting environment variables in your container instances allows you to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="99026-102">환경 변수는 컨테이너 생성 시에 Azure CLI, PowerShell 또는 Azure Portal을 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="99026-102">Environment variables are set using the Azure CLI, PowerShell, or the Azure portal at container creation time.</span></span> <span data-ttu-id="99026-103">보안 환경 변수는 민감한 정보가 컨테이너 조작 출력에 표시되지 않도록 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99026-103">Secured environment variables are used to prevent sensitive information from being displayed in container operations output.</span></span>

<span data-ttu-id="99026-104">이 단원에서는 Azure Cosmos DB 인스턴스를 만든 후 환경 변수로 저장된 Azure Cosmos DB 인스턴스의 연결 정보를 사용하여 Azure Container Instance를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-104">In this unit, an Azure Cosmos DB instance is created, and then an Azure container instance runs with the connection information of the Azure Cosmos DB instance stored as environment variables.</span></span> <span data-ttu-id="99026-105">컨테이너의 응용 프로그램은 해당 변수를 사용하여 Azure Cosmos DB에서 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="99026-105">An application in the container uses the variables to write and read data from Azure Cosmos DB.</span></span> <span data-ttu-id="99026-106">이 단원에서는 환경 변수와 보안 환경 변수를 둘 다 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99026-106">In this unit, you will create both an environment variable and a secured environment variable.</span></span>

## <a name="deploy-azure-cosmos-db"></a><span data-ttu-id="99026-107">Azure Cosmos DB 배포</span><span class="sxs-lookup"><span data-stu-id="99026-107">Deploy Azure Cosmos DB</span></span>

<span data-ttu-id="99026-108">`az Azure Cosmos DB create` 명령을 사용하여 Azure Cosmos DB 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99026-108">Create the Azure Cosmos DB instance with the `az Azure Cosmos DB create` command.</span></span> <span data-ttu-id="99026-109">또한 이 예제에서는 *COSMOS_DB_ENDPOINT*라는 변수에 Azure Cosmos DB 엔드포인트 주소를 배치하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-109">This example will also place the Azure Cosmos DB endpoint address in a variable named *COSMOS_DB_ENDPOINT*.</span></span>

<span data-ttu-id="99026-110">이 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99026-110">This command can take a few minutes to complete:</span></span>

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group myResourceGroup --name aci-cosmos --query documentEndpoint -o tsv)
```

<span data-ttu-id="99026-111">그런 다음, `az cosmosdb list-keys` 명령을 사용하여 Azure Cosmos DB 연결 키를 가져온 후 *COSMOS_DB_MASTERKEY*라는 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-111">Next, get the Azure Cosmos DB connection key with the `az cosmosdb list-keys` command and store it in a variable named *COSMOS_DB_MASTERKEY*:</span></span>

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group myResourceGroup --name aci-cosmos --query primaryMasterKey -o tsv)
```

## <a name="deploy-a-container-instance"></a><span data-ttu-id="99026-112">컨테이너 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="99026-112">Deploy a container instance</span></span>

<span data-ttu-id="99026-113">`az container create` 명령을 사용하여 Azure 컨테이너 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99026-113">Create an Azure container instance using the `az container create` command.</span></span> <span data-ttu-id="99026-114">두 개의 환경 변수인 `COSMOS_DB_ENDPOINT` 및 `COSMOS_DB_ENDPOINT`가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="99026-114">Take note that two environment variables are created, `COSMOS_DB_ENDPOINT` and `COSMOS_DB_ENDPOINT`.</span></span> <span data-ttu-id="99026-115">이러한 변수는 Azure Cosmos DB 인스턴스에 연결하는 데 필요한 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-115">These variables hold the values needed to connect to the Azure Cosmos DB instance:</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

<span data-ttu-id="99026-116">컨테이너가 만들어지면 `az container show` 명령을 사용하여 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="99026-116">Once the container has been created, get the IP address with the `az container show` command:</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-demo --query ipAddress.ip --output tsv
```

<span data-ttu-id="99026-117">브라우저를 열고 컨테이너의 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-117">Open up a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="99026-118">다음 응용 프로그램이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-118">You should see the following application.</span></span> <span data-ttu-id="99026-119">투표를 진행하면 해당 투표 내용이 Azure Cosmos DB 인스턴스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="99026-119">When casing a vote, the vote is stored in the Azure Cosmos DB instance.</span></span>

![두 가지 선택 사항인 고양이와 강아지가 표시되는 Azure 투표 응용 프로그램](../media-draft/azure-vote.png)

## <a name="secured-environment-variables"></a><span data-ttu-id="99026-121">보안 환경 변수</span><span class="sxs-lookup"><span data-stu-id="99026-121">Secured environment variables</span></span>

<span data-ttu-id="99026-122">이전 연습에서는 두 개의 환경 변수에 저장된 Azure Cosmos DB에 대한 연결 정보를 사용하여 컨테이너가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="99026-122">In the previous exercise, a container was created with connection information for Azure Cosmos DB stored in two environment variables.</span></span> <span data-ttu-id="99026-123">기본적으로 환경 변수는 Azure Portal 및 명령줄 도구에 일반 텍스트로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="99026-123">By default, environment variables are displayed in the Azure portal and command-line tools in plain text.</span></span>

<span data-ttu-id="99026-124">예를 들어, `az container show` 명령을 사용하여 이전 연습에서 만든 컨테이너에 대한 정보를 가져오는 경우 해당 환경 변수는 일반 텍스트로 액세스 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-124">For example, if you get information about the container created in the previous exercise with the `az container show` command, the environment variables are accessible in plain text:</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-demo --query containers[0].environmentVariables
```

<span data-ttu-id="99026-125">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="99026-125">Example output:</span></span>

```bash
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

보안 환경 변수로 인해 명확한 텍스트 출력이 표시되지 않습니다. <span data-ttu-id="99026-127">보안 환경 변수를 사용하려면 `--environment-variables` 인수를 `--secure-environment-variables` 인수로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="99026-127">To use secure environment variables, replace the `--environment-variables` argument with the `--secure-environment-variables` argument.</span></span>

<span data-ttu-id="99026-128">다음 예제를 실행하여 보안 환경 변수를 활용하는 *aci-demo-secure*라는 컨테이너를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="99026-128">Run the following example to create a container named *aci-demo-secure* that utilizes secured environment variables:</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

<span data-ttu-id="99026-129">이제 `az container show` 명령을 사용하여 컨테이너가 반환될 때 환경 변수가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99026-129">Now, when the container is returned with the `az container show` command, the environment variables are not displayed:</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-demo-secure --query containers[0].environmentVariables
```

<span data-ttu-id="99026-130">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="99026-130">Example output:</span></span>

```bash
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

## <a name="summary"></a><span data-ttu-id="99026-131">요약</span><span class="sxs-lookup"><span data-stu-id="99026-131">Summary</span></span>

<span data-ttu-id="99026-132">이 단원에서는 Azure Cosmos DB 인스턴스와 Azure Container Instance를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="99026-132">In this unit, you created an Azure Cosmos DB instance and an Azure container instance.</span></span> <span data-ttu-id="99026-133">컨테이너 내부에서 실행되는 응용 프로그램이 Azure Cosmos DB 인스턴스에 연결할 수 있도록 환경 변수가 컨테이너 인스턴스에 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99026-133">Environment variables were set in the container instance such that the application running inside of the container was able to connect to the Azure Cosmos DB instance.</span></span>

<span data-ttu-id="99026-134">다음 단원에서는 데이터 지속성을 위해 Azure 컨테이너 인스턴스에 데이터 볼륨을 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="99026-134">In the next unit, you will mount data volumes to an Azure container instance for data persistence.</span></span>
