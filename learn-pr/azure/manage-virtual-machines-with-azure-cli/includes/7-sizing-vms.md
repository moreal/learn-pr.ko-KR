<span data-ttu-id="d6de7-101">예상 업무에 맞게 가상 머신의 크기를 적절히 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-101">Virtual machines must be sized appropriately for the expected work.</span></span> <span data-ttu-id="d6de7-102">정확한 메모리 또는 CPU가 없는 VM은 로드되지 않거나, 실행 속도가 너무 느려서 효과적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-102">A VM without the correct amount of memory or CPU will fail under load or run too slowly to be effective.</span></span> 

<span data-ttu-id="d6de7-103">가상 머신을 만들 때, VM에 사용할 계산 리소스의 양을 결정하는 _VM 크기_ 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-103">When you create a virtual machine, you can supply a _VM size_ value that will determine the amount of compute resources that will be devoted to the VM.</span></span> <span data-ttu-id="d6de7-104">여기에는 Azure에서 가상 머신에 사용할 수 있는 CPU, GPU 및 메모리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-104">This includes CPU, GPU, and memory that are made available to the virtual machine from Azure.</span></span>

<span data-ttu-id="d6de7-105">Azure는 예상 사용량을 기반으로 선택할 수 있도록 Linux 및 Windows용 [사전 정의의 VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-105">Azure defines a set of [pre-defined VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) for Linux and Windows to choose from based on the expected usage.</span></span> 

| <span data-ttu-id="d6de7-106">type</span><span class="sxs-lookup"><span data-stu-id="d6de7-106">Type</span></span> | <span data-ttu-id="d6de7-107">크기</span><span class="sxs-lookup"><span data-stu-id="d6de7-107">Sizes</span></span> | <span data-ttu-id="d6de7-108">설명</span><span class="sxs-lookup"><span data-stu-id="d6de7-108">Description</span></span> |
|------|-------|-------------|
| <span data-ttu-id="d6de7-109">범용 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d6de7-109">General purpose</span></span>   | <span data-ttu-id="d6de7-110">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="d6de7-110">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="d6de7-111">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-111">Balanced CPU-to-memory.</span></span> <span data-ttu-id="d6de7-112">개발/테스트와 소규모에서 중간 정도의 응용 프로그램 및 데이터 솔루션에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-112">Ideal for dev/test and small to medium applications and data solutions.</span></span> |
| <span data-ttu-id="d6de7-113">계산 최적화</span><span class="sxs-lookup"><span data-stu-id="d6de7-113">Compute optimized</span></span> | <span data-ttu-id="d6de7-114">Fs, F</span><span class="sxs-lookup"><span data-stu-id="d6de7-114">Fs, F</span></span> | <span data-ttu-id="d6de7-115">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-115">High CPU-to-memory.</span></span> <span data-ttu-id="d6de7-116">트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-116">Good for medium-traffic applications, network appliances, and batch processes.</span></span> |
| <span data-ttu-id="d6de7-117">메모리 최적화</span><span class="sxs-lookup"><span data-stu-id="d6de7-117">Memory optimized</span></span>  | <span data-ttu-id="d6de7-118">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="d6de7-118">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="d6de7-119">메모리 대 코어 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-119">High memory-to-core.</span></span> <span data-ttu-id="d6de7-120">관계형 데이터베이스, 중대형 캐시 및 메모리 내 분석에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-120">Great for relational databases, medium to large caches, and in-memory analytics.</span></span> |
| <span data-ttu-id="d6de7-121">저장소 최적화</span><span class="sxs-lookup"><span data-stu-id="d6de7-121">Storage optimized</span></span> | <span data-ttu-id="d6de7-122">Ls</span><span class="sxs-lookup"><span data-stu-id="d6de7-122">Ls</span></span> | <span data-ttu-id="d6de7-123">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="d6de7-123">High disk throughput and IO.</span></span> <span data-ttu-id="d6de7-124">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-124">Ideal for big data, SQL, and NoSQL databases.</span></span> |
| <span data-ttu-id="d6de7-125">GPU에 최적화</span><span class="sxs-lookup"><span data-stu-id="d6de7-125">GPU optimized</span></span> | <span data-ttu-id="d6de7-126">NV, NC</span><span class="sxs-lookup"><span data-stu-id="d6de7-126">NV, NC</span></span> | <span data-ttu-id="d6de7-127">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-127">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span> |
| <span data-ttu-id="d6de7-128">고성능</span><span class="sxs-lookup"><span data-stu-id="d6de7-128">High performance</span></span> | <span data-ttu-id="d6de7-129">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="d6de7-129">H, A8-11</span></span> | <span data-ttu-id="d6de7-130">당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-130">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> | 

<span data-ttu-id="d6de7-131">사용 가능한 크기는 VM을 만들고 있는 지역에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-131">The available sizes change based on the region you're creating the VM in.</span></span> <span data-ttu-id="d6de7-132">`vm list-sizes` 명령을 사용하여 사용 가능한 크기 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-132">You can get a list of the available sizes using the `vm list-sizes` command.</span></span> <span data-ttu-id="d6de7-133">Azure Cloud Shell에 이 명령을 입력해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d6de7-133">Try typing this into Azure Cloud Shell:</span></span>

```azurecli
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="d6de7-134">다음은 `eastus`에 대한 간략한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-134">Here's an abbreviated response for `eastus`:</span></span>

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

<span data-ttu-id="d6de7-135">VM을 만들 때 크기를 지정하지 않았으므로, Azure에서는 `Standard_DS1_v2`의 기본 범용 크기를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-135">We didn't specify a size when we created our VM - so Azure selected a default general-purpose size for us of `Standard_DS1_v2`.</span></span> <span data-ttu-id="d6de7-136">그러나 `--size` 매개 변수를 사용하여 `vm create` 명령의 일부로 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-136">However, we can specify the size as part of the `vm create` command using the `--size` parameter.</span></span> <span data-ttu-id="d6de7-137">예를 들어, 다음 명령을 사용하여 16코어 가상 머신을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-137">For example, you could use the following command to create a 16-core virtual machine:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

> [!WARNING]
> <span data-ttu-id="d6de7-138">구독 계층은 생성할 수 있는 리소스 수와 해당 리소스의 전체 크기에 대한 [제한을 적용](https://docs.microsoft.com/azure/azure-subscription-service-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-138">Your subscription tier [enforces limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) on how many resources you can create, as well as the total size of those resources.</span></span> <span data-ttu-id="d6de7-139">예를 들어, 종량제 구독에서는 **20개의 가상 CPU**로, 평가판 계층에는 **4개의 vCPU**만으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-139">For example, you are capped to **20 virtual CPUs** with the pay-as-you-go subscription, and only **4 vCPUs** for a free tier.</span></span> <span data-ttu-id="d6de7-140">Azure CLI는 이 한도를 초과할 때 **할당량이 초과됨** 오류로 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-140">The Azure CLI will let you know when you exceed this with a **Quota Exceeded** error.</span></span> <span data-ttu-id="d6de7-141">아키텍처를 만들 때 이 오류가 발생하면 [평가판 온라인 요청](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-quota-errors)을 통해 유료 구독과 관련된 제한(최대 10,000개의 vCPU!)을 올리도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-141">If you hit this error when creating your architecture, you can request to raise the limits associated with your paid subscription (up to 10,000 vCPUs!) through a [free online request](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-quota-errors).</span></span> 

## <a name="resizing-an-existing-vm"></a><span data-ttu-id="d6de7-142">기존 VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d6de7-142">Resizing an existing VM</span></span>
<span data-ttu-id="d6de7-143">워크로드가 변경되거나 생성 시 크기가 잘못 조정된 경우에도 기존 VM의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-143">We can also resize an existing VM if the workload changes, or if it was incorrectly sized at creation.</span></span> <span data-ttu-id="d6de7-144">크기를 조정하기 전에 먼저 VM이 포함된 클러스터에서 원하는 크기를 사용할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-144">Before a resize is requested, we must check to see if the desired size is available in the cluster our VM is part of.</span></span> <span data-ttu-id="d6de7-145">이 경우 `vm list-vm-resize-options` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-145">We can do this with the `vm list-vm-resize-options` command:</span></span>

```azurecli
az vm list-vm-resize-options --resource-group ExerciseResources --name SampleVM --output table
```

<span data-ttu-id="d6de7-146">이 명령은 리소스 그룹에서 사용 가능한 모든 크기 구성의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-146">This will return a list of all the possible size configurations available in the resource group.</span></span> <span data-ttu-id="d6de7-147">클러스터에서는 사용할 수 없지만 지역에서는 사용할 수 _있는_ 크기인 경우 [VM 할당을 취소](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-147">If the size we want isn't available in our cluster, but _is_ available in the region, we can [deallocate the VM](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate).</span></span> <span data-ttu-id="d6de7-148">이 명령은 실행 중인 VM을 중지한 후 리소스의 손실 없이 현재 클러스터에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-148">This command will stop the running VM and remove it from the current cluster without losing any resources.</span></span> <span data-ttu-id="d6de7-149">그런 다음, 크기를 조정할 수 있습니다. 그러면 크기 구성을 사용할 수 있는 새 클러스터에서 VM이 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-149">Then we can resize it, which will re-create the VM in a new cluster where the size configuration is available.</span></span>

<span data-ttu-id="d6de7-150">VM의 크기를 조정하려면 `vm resize` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-150">To resize a VM, we use the `vm resize` command.</span></span> <span data-ttu-id="d6de7-151">예를 들어 현재 VM 리소스를 2G 메모리, 1 CPU 코어 및 4G 디스크 공간이라는 최소 수준으로 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-151">For example, let's reduce our current VM resources to the bare minimum: 2G of memory, 1 CPU core, and 4G of disk space.</span></span> <span data-ttu-id="d6de7-152">다음 명령을 Cloud Shell에 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="d6de7-152">Type this command in Cloud Shell:</span></span>

```azurecli
az vm resize --resource-group ExerciseResources --name SampleVM --size "Standard_B1ms"
```

<span data-ttu-id="d6de7-153">이 명령으로 VM의 리소스를 줄이는 데 몇 분 정도 소요되며, 완료되면 새 JSON 구성이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6de7-153">This command will take a few minutes to reduce the resources of the VM, and once it's done, it will return a new JSON configuration.</span></span>