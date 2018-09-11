<span data-ttu-id="36923-101">이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36923-101">In this unit, you will create an Azure Container Registry using the Azure CLI.</span></span>

## <a name="create-an-azure-container-registry"></a><span data-ttu-id="36923-102">Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="36923-102">Create an Azure Container Registry</span></span>

<span data-ttu-id="36923-103">ACR(Azure Container Registry)을 만들려면 ACR을 배포할 *리소스 그룹*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="36923-103">Before you create your Azure Container Registry (ACR), you need a *resource group* to deploy it to.</span></span> <span data-ttu-id="36923-104">리소스 그룹은 모든 Azure 리소스가 배포 및 관리되는 논리적 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="36923-104">A resource group is a logical collection into which all Azure resources are deployed and managed.</span></span>

<span data-ttu-id="36923-105">`az group create` 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36923-105">Create a resource group with the `az group create` command.</span></span> <span data-ttu-id="36923-106">다음 예제에서는 *eastus* 지역에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36923-106">In the following example, a resource group named *myResourceGroup* is created in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="36923-107">리소스 그룹을 만든 후에는 `az acr create` 명령을 사용하여 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36923-107">Once you've created the resource group, create an Azure container registry with the `az acr create` command.</span></span> <span data-ttu-id="36923-108">컨테이너 레지스트리 이름은 Azure 내에서 고유해야 하며, 5-50자의 영숫자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36923-108">The container registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="36923-109">`<acrName>`를 레지스트리의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="36923-109">Replace `<acrName>` with a unique name for your registry.</span></span>

<span data-ttu-id="36923-110">이 예제에서는 프리미엄 레지스트리 SKU가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="36923-110">For this example, a premium registry SKU is deployed.</span></span> <span data-ttu-id="36923-111">프리미엄 SKU는 지역 복제에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="36923-111">The premium SKU is required for geo-replication.</span></span> <span data-ttu-id="36923-112">Container Registry SKU에 대한 자세한 내용은 [Azure Container Registry SKU](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-skus)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36923-112">For more information on Container Registry SKUs, see, [Azure Container Registry SKUs](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-skus)</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Premium
```

<span data-ttu-id="36923-113">다음은 새 Azure Container Registry의 출력 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="36923-113">Here's example output for a new Azure container registry.</span></span>

```console
{
  "adminUserEnabled": false,
  "creationDate": "2018-08-15T19:19:07.042178+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myACR0007",
  "location": "eastus",
  "loginServer": "myacr.azurecr.io",
  "name": "myACR",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Premium",
    "tier": "Premium"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="36923-114">이 모듈의 나머지 부분에서는 `<acrName>`을 이 단계에서 선택하는 Container Registry 이름의 자리 표시자로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="36923-114">The rest of this module refers to `<acrName>` as a placeholder for the container registry name that you chose in this step.</span></span>

## <a name="summary"></a><span data-ttu-id="36923-115">요약</span><span class="sxs-lookup"><span data-stu-id="36923-115">Summary</span></span>

<span data-ttu-id="36923-116">이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="36923-116">In this unit, an Azure Container Registry was created using the Azure CLI.</span></span> <span data-ttu-id="36923-117">다음 단원에서는 Azure Container Registry를 사용하여 컨테이너 이미지를 만들고 해당 이미지를 Container Registry에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="36923-117">In the next unit, you will use Azure Container Registry to create a container image and store this image in the container registry.</span></span>