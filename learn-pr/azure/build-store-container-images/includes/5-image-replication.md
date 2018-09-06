<span data-ttu-id="ae1af-101">이미지가 실행되는 각 지역에 컨테이너 레지스트리를 배치하면 네트워크와 가까운 곳에서 작업하여 이미지 레이어를 가장 빠르고 안정적으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-101">As a best practice, placing a container registry in each region where images are run allows network-close operations, enabling fast, reliable image layer transfers.</span></span> <span data-ttu-id="ae1af-102">지역 복제를 사용하면 Azure Container Registry가 단일 레지스트리로 기능하여 다중 마스터 지역 레지스트리가 있는 둘 이상의 지역에 서비스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-102">Geo-replication enables an Azure container registry to function as a single registry, serving multiple regions with multi-master regional registries.</span></span>

<span data-ttu-id="ae1af-103">지역에서 복제된 레지스트리는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-103">A geo-replicated registry provides the following benefits:</span></span>

* <span data-ttu-id="ae1af-104">둘 이상의 지역에서 단일 레지스트리/이미지/태그 이름 사용 가능</span><span class="sxs-lookup"><span data-stu-id="ae1af-104">Single registry/image/tag names can be used across multiple regions</span></span>
* <span data-ttu-id="ae1af-105">지역별 배포 환경에서 네트워크와 가까운 곳에 위치한 레지스트리에 액세스 가능</span><span class="sxs-lookup"><span data-stu-id="ae1af-105">Network-close registry access from regional deployments</span></span>
* <span data-ttu-id="ae1af-106">컨테이너 호스트와 동일한 지역에 있는 복제된 로컬 레지스트리에서 이미지를 끌어오므로 추가 송신 요금이 부과되지 않음</span><span class="sxs-lookup"><span data-stu-id="ae1af-106">No additional egress fees because images are pulled from a local, replicated registry in the same region as your container host</span></span>
* <span data-ttu-id="ae1af-107">둘 이상의 지역에서 레지스트리를 단일하게 관리</span><span class="sxs-lookup"><span data-stu-id="ae1af-107">Single management of a registry across multiple regions</span></span>

## <a name="replicate-image-to-multiple-locations"></a><span data-ttu-id="ae1af-108">여러 위치에 이미지 복제</span><span class="sxs-lookup"><span data-stu-id="ae1af-108">Replicate image to multiple locations</span></span>

<span data-ttu-id="ae1af-109">`az acr replication create` 명령을 사용하여 컨테이너 이미지를 다른 지역에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-109">Use the `az acr replication create` command to replicate your container images to another region.</span></span> <span data-ttu-id="ae1af-110">이 예에서는 `japaneast` 지역에 대한 복제가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-110">In this example, a replication is created for the `japaneast` region.</span></span> <span data-ttu-id="ae1af-111">컨테이너 레지스트리 이름으로 `<acrName>`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-111">Update `<acrName>` with the name of your container registry.</span></span>

```azurecli
az acr replication create --registry <acrName> --location japaneast
```

<span data-ttu-id="ae1af-112">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-112">The output should look similar to the following:</span></span>

```console
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myACR0007/replications/japaneast",
  "location": "japaneast",
  "name": "japaneast",
  "provisioningState": "Succeeded",
  "resourceGroup": "myresourcegroup",
  "status": {
    "displayStatus": "Syncing",
    "message": null,
    "timestamp": "2018-08-15T20:22:09.275792+00:00"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries/replications"
}
```

<span data-ttu-id="ae1af-113">모든 컨테이너 이미지 복제본의 목록을 보려면 `az acr replication list` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-113">To see a list of all container image replicas, use the `az acr replication list` command.</span></span> <span data-ttu-id="ae1af-114">컨테이너 레지스트리 이름으로 `<acrName>`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-114">Update `<acrName>` with the name of your container registry.</span></span>

```azurecli
az acr replication list --registry <acrName> --output table
```

<span data-ttu-id="ae1af-115">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-115">The output should look similar to the following:</span></span>

```console
NAME       LOCATION    PROVISIONING STATE    STATUS
---------  ----------  --------------------  --------
japaneast  japaneast   Succeeded             Ready
eastus     eastus      Succeeded             Ready
```

<span data-ttu-id="ae1af-116">이 연습에서는 Azure Portal을 사용하지 않았지만 포털 환경을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-116">While the Azure portal was not used in this exercise, it is neat to see the portal experience.</span></span>

<span data-ttu-id="ae1af-117">Azure Portal 내에서 Azure Container Registry에 대해 `Replications`를 선택하면 현재 복제를 자세히 설명하는 맵이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-117">From within the Azure portal, selecting `Replications` for an Azure container registry displays a map that details current replications.</span></span> <span data-ttu-id="ae1af-118">맵에서 지역을 선택하여 컨테이너 이미지를 추가 지역으로 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-118">Container images can be replicated to additional regions by selecting the regions on the map.</span></span>

![Azure Portal에 표시되는 컨테이너 복제 맵](../media/replication-map.png)

## <a name="clean-up"></a><span data-ttu-id="ae1af-120">정리</span><span class="sxs-lookup"><span data-stu-id="ae1af-120">Clean up</span></span>

<span data-ttu-id="ae1af-121">Azure Container Registry 학습 모듈의 마지막 단원입니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-121">This is the last unit of the Azure Container Registry learning module.</span></span> <span data-ttu-id="ae1af-122">이제 리소스 그룹을 삭제하여 만든 리소스를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-122">At this point, you can clean up the created resources by deleting the resource group.</span></span> <span data-ttu-id="ae1af-123">이렇게 하려면 `az group delete` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-123">To do so, use the `az group delete` command.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a><span data-ttu-id="ae1af-124">요약</span><span class="sxs-lookup"><span data-stu-id="ae1af-124">Summary</span></span>

<span data-ttu-id="ae1af-125">이 모듈에서는 Azure CLI를 사용하여 여러 Azure 지역에 컨테이너 이미지를 복제했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1af-125">In this module, you replicated a container image to multiple Azure regions using the Azure CLI.</span></span>