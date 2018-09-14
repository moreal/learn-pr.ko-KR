<span data-ttu-id="5d083-101">회사가 계산 워크로드를 여러 지역에 배포하여 분산된 고객층에게 제공하는 로컬 서비스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-101">Your company has compute workloads deployed to several regions to make sure you have a local presence to serve your distributed customer base.</span></span> 

<span data-ttu-id="5d083-102">이미지를 실행하는 각 지역에 컨테이너 레지스트리를 배치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-102">Your aim is to place a container registry in each region where images are run.</span></span> <span data-ttu-id="5d083-103">네트워크에 가까운 작업에 대해 이 전략을 허용하면 신속하게 신뢰할 수 있는 이미지 계층을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-103">This strategy will allow for network-close operations, enabling fast, reliable image layer transfers.</span></span> 

<span data-ttu-id="5d083-104">지역 복제를 사용하면 Azure Container Registry가 단일 레지스트리로 기능하여 다중 마스터 지역 레지스트리가 있는 여러 지역에 서비스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-104">Geo-replication enables an Azure container registry to function as a single registry, serving several regions with multi-master regional registries.</span></span>

<span data-ttu-id="5d083-105">지역 복제된 레지스트리는 다음과 같은 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-105">A geo-replicated registry provides the following benefits:</span></span>

- <span data-ttu-id="5d083-106">둘 이상의 지역에서 단일 레지스트리/이미지/태그 이름 사용 가능</span><span class="sxs-lookup"><span data-stu-id="5d083-106">Single registry/image/tag names can be used across multiple regions</span></span>
- <span data-ttu-id="5d083-107">지역 배포에서 네트워크와 가까운 곳에 위치한 레지스트리에 액세스 가능</span><span class="sxs-lookup"><span data-stu-id="5d083-107">Network-close registry access from regional deployments</span></span>
- <span data-ttu-id="5d083-108">컨테이너 호스트와 동일한 지역에 있는 복제된 로컬 레지스트리에서 이미지를 가져오므로 추가 송신 요금이 부과되지 않음</span><span class="sxs-lookup"><span data-stu-id="5d083-108">No additional egress fees, as images are pulled from a local, replicated registry in the same region as your container host</span></span>
- <span data-ttu-id="5d083-109">여러 지역에서 레지스트리를 단일 관리</span><span class="sxs-lookup"><span data-stu-id="5d083-109">Single management of a registry across multiple regions</span></span>

## <a name="replicate-an-image-to-multiple-locations"></a><span data-ttu-id="5d083-110">여러 위치에 이미지 복제</span><span class="sxs-lookup"><span data-stu-id="5d083-110">Replicate an image to multiple locations</span></span>

<span data-ttu-id="5d083-111">`az acr replication create` Azure CLI 명령을 사용하여 컨테이너 이미지를 지역 간에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-111">You'll use the `az acr replication create` Azure CLI command to replicate your container images from one region to another.</span></span> <span data-ttu-id="5d083-112">이 예제에서는 `japaneast` 지역에 대한 복제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-112">In this example, you'll create a replication for the `japaneast` region.</span></span> <span data-ttu-id="5d083-113">Container Registry 이름으로 `<acrName>`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-113">Update `<acrName>` with the name of your Container Registry.</span></span>

```azurecli
az acr replication create --registry <acrName> --location japaneast
```

<span data-ttu-id="5d083-114">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-114">The output should look similar to the following:</span></span>

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

<span data-ttu-id="5d083-115">마지막 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-115">As a final step.</span></span> <span data-ttu-id="5d083-116">만든 모든 컨테이너 이미지 복제본을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-116">You are able to retrieve all container image replicas created.</span></span> <span data-ttu-id="5d083-117">`az acr replication list` 명령을 사용하여 이 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-117">You'll use the `az acr replication list` command to retrieve this list.</span></span> <span data-ttu-id="5d083-118">Container Registry 이름으로 `<acrName>`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-118">Update `<acrName>` with the name of your Container Registry.</span></span>

```azurecli
az acr replication list --registry <acrName> --output table
```

<span data-ttu-id="5d083-119">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-119">The output should look similar to the following:</span></span>

```console
NAME       LOCATION    PROVISIONING STATE    STATUS
---------  ----------  --------------------  --------
japaneast  japaneast   Succeeded             Ready
eastus     eastus      Succeeded             Ready
```

<span data-ttu-id="5d083-120">이미지 복제본을 나열하는 Azure CLI로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-120">Keep in mind that you are not limited to the Azure CLI to list your image replicas.</span></span> <span data-ttu-id="5d083-121">Azure Portal 내에서 Azure Container Registry에 대해 `Replications`를 선택하면 현재 복제를 자세히 설명하는 맵이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-121">From within the Azure portal, selecting `Replications` for an Azure Container Registry displays a map that details current replications.</span></span> <span data-ttu-id="5d083-122">맵에서 지역을 선택하여 컨테이너 이미지를 추가 지역으로 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-122">Container images can be replicated to additional regions by selecting the regions on the map.</span></span>

![Azure Portal에 표시되는 컨테이너 복제 맵](../media/replication-map.png)

## <a name="clean-up-your-resources"></a><span data-ttu-id="5d083-124">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="5d083-124">Clean up your resources</span></span>
<!---TODO: Do we need to include cleanup for the free education tier?--->

<span data-ttu-id="5d083-125">이제 리소스 그룹을 삭제하여 만든 리소스를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-125">At this point, you can cleanup the created resources by deleting the resource group.</span></span> <span data-ttu-id="5d083-126">이렇게 하려면 `az group delete` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-126">To do so, use the `az group delete` command.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a><span data-ttu-id="5d083-127">요약</span><span class="sxs-lookup"><span data-stu-id="5d083-127">Summary</span></span>

<span data-ttu-id="5d083-128">이제 Azure CLI를 사용하여 여러 Azure 데이터 센터에 컨테이너 이미지를 성공적으로 복제했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d083-128">You've now successfully replicated a container image to multiple Azure datacenters using the Azure CLI.</span></span> 