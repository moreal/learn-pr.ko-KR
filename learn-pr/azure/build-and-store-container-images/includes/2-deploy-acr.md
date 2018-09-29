<span data-ttu-id="0029e-101">이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-101">In this unit, you will create an Azure container registry using the Azure CLI.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]
 
## <a name="create-an-azure-container-registry"></a><span data-ttu-id="0029e-102">Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="0029e-102">Create an Azure container registry</span></span>

<span data-ttu-id="0029e-103">무료 샌드박스에서 작업할 것이므로 고유한 리소스 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-103">We'll be working in a free sandbox, so there's no need to create your own Resource Group.</span></span> <span data-ttu-id="0029e-104">`az acr create` 명령을 사용하여 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-104">Create an Azure container registry with the `az acr create` command.</span></span> <span data-ttu-id="0029e-105">컨테이너 레지스트리 이름은 Azure 내에서 고유해야 하며, 5~50자 사이의 영숫자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-105">The container registry name must be unique within Azure and contain between 5 and 50 alphanumeric characters.</span></span> <span data-ttu-id="0029e-106">`<acrName>`를 레지스트리의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-106">Replace `<acrName>` with a unique name for your registry.</span></span>

<span data-ttu-id="0029e-107">이 예제에서는 프리미엄 레지스트리 SKU가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-107">In this example, a premium registry SKU is deployed.</span></span> <span data-ttu-id="0029e-108">프리미엄 SKU는 지역 복제에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-108">The premium SKU is required for geo-replication.</span></span> <span data-ttu-id="0029e-109">다음 명령을 Cloud Shell 편집기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-109">Enter the following command into the cloud shell editor.</span></span>

```azurecli
az acr create --resource-group <rgn>[sandbox resource group name]</rgn> --name <acrName> --sku Premium
```

<span data-ttu-id="0029e-110">다음은 새 Azure 컨테이너 레지스트리의 출력 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-110">Here's an example output for a new Azure container registry:</span></span>

```output
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

<span data-ttu-id="0029e-111">이 모듈의 나머지 부분에서는 `<acrName>`을 이 단계에서 선택하는 컨테이너 레지스트리 이름의 자리 표시자로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-111">The rest of this module refers to `<acrName>` as a placeholder for the container registry name that you chose in this step.</span></span>

<span data-ttu-id="0029e-112">이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0029e-112">In this unit, you created an Azure container registry using the Azure CLI.</span></span>