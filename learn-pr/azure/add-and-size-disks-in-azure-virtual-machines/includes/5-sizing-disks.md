<span data-ttu-id="df06b-101">Azure는 VHD 이미지를 Azure Storage 계정의 페이지 Blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-101">Azure stores your VHD images as page blobs in an Azure Storage account.</span></span> <span data-ttu-id="df06b-102">관리 디스크를 사용하는 Azure는 사용자 대신 저장소를 관리합니다. 이는 관리 디스크를 선택하는 가장 좋은 이유 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-102">With managed disks, Azure takes care of managing the storage on your behalf - it's one of the best reasons to choose managed disks.</span></span>

<span data-ttu-id="df06b-103">VM을 만들 때 OS 디스크의 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-103">When you create the VM, it chooses a size for the OS disk.</span></span> <span data-ttu-id="df06b-104">특정 크기는 선택한 이미지를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-104">The specific size is based on the image you select.</span></span> <span data-ttu-id="df06b-105">Linux에서는 대게 약 30GB이고, Windows에서는 약 127GB입니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-105">On Linux, it's often around 30 GB, and on Windows about 127 GB.</span></span>

<span data-ttu-id="df06b-106">추가 저장소 공간을 제공하기 위해 데이터 디스크를 추가할 수 있지만 기존 디스크를 확장할 수도 있습니다. 아마도 레거시 응용 프로그램은 드라이브 간에 데이터를 분할할 수 없거나 실제 PC의 드라이브를 Azure로 마이그레이션하고 더 큰 OS 드라이브가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-106">You can add data disks to provide for additional storage space, but you may also wish to expand an existing disk - perhaps a legacy application cannot split its data across drives, or you are migrating a physical PC's drive to Azure and need a larger OS drive.</span></span>

> [!NOTE]
> <span data-ttu-id="df06b-107">디스크 크기를 _큰_ 크기로만 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-107">You can only resize a disk to a _larger_ size.</span></span> <span data-ttu-id="df06b-108">관리 디스크 축소는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-108">Shrinking managed disks is not supported today.</span></span>

<span data-ttu-id="df06b-109">디스크의 크기를 변경하면 디스크 수준도 변경할 수 있습니다(예: P10에서 P20으로).</span><span class="sxs-lookup"><span data-stu-id="df06b-109">Changing the size of the disk can also change the level of the disk (for example from P10 to P20).</span></span> <span data-ttu-id="df06b-110">이는 성능 업그레이드에 유용할 수 있지만 프리미엄 계층으로 이동할수록 더 많은 비용이 소요됨을 명심하세요.</span><span class="sxs-lookup"><span data-stu-id="df06b-110">Keep this in mind - this can be beneficial for performance upgrades, but will also cost more as you move up the premium tiers.</span></span>

## <a name="vm-size-vs-disk-size"></a><span data-ttu-id="df06b-111">VM 크기 대 디스크 크기</span><span class="sxs-lookup"><span data-stu-id="df06b-111">VM size vs. Disk size</span></span>

<span data-ttu-id="df06b-112">VM을 만들 때 선택하는 VM 크기에 따라 할당할 수 있는 리소스 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-112">The VM size you choose when you create your VM will determine how many resources it can allocate.</span></span> <span data-ttu-id="df06b-113">저장소의 경우 크기는 VM에 추가할 수 있는 디스크 수와 각 디스크의 최대 크기를 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-113">For storage, the size will control the number of disks you can add to the VM and the max size of each disk.</span></span> 

<span data-ttu-id="df06b-114">이전 단원에서 언급했듯이 일부 VM 크기는 표준 저장소 드라이브만 지원하므로 I/O 성능이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-114">As mentioned in the previous unit, some VM sizes only support Standard storage drives - limiting the I/O performance.</span></span>

<span data-ttu-id="df06b-115">VM 크기가 허용하는 것보다 많은 저장소가 필요한 경우 VM 크기를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-115">If you find that you need more storage than what your VM size allows for, you can change the VM size.</span></span> <span data-ttu-id="df06b-116">해당 항목은 **Azure Virtual Machines 소개** 모듈에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-116">We cover that topic in the **Introduction to Azure Virtual Machines** module.</span></span>

## <a name="expanding-a-disk-using-the-azure-cli"></a><span data-ttu-id="df06b-117">Azure CLI를 사용하여 디스크 확장</span><span class="sxs-lookup"><span data-stu-id="df06b-117">Expanding a disk using the Azure CLI</span></span>

> [!WARNING]
> <span data-ttu-id="df06b-118">디스크 크기 조정 작업을 수행하기 전에 항상 데이터를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-118">Always make sure that you back up your data before performing disk resize operations!</span></span>

<span data-ttu-id="df06b-119">VM 실행 중에 VHD에 대한 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-119">Operations on VHDs cannot be performed with the VM running.</span></span> <span data-ttu-id="df06b-120">첫 번째 단계는 VM 이름과 리소스 그룹 이름을 제공하는 `az vm deallocate`가 있는 VM을 중지 및 할당 취소하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-120">The first step is to stop and deallocate the VM with `az vm deallocate` supplying the VM name and resource group name.</span></span>

<span data-ttu-id="df06b-121">_중지_와 달리 VM을 할당 취소하면 VM은 관련 컴퓨팅 리소스를 해제하고 Azure가 가상화된 하드웨어의 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-121">Deallocating a VM, unlike just _stopping_ a VM releases the associated computing resources and allows Azure to make configuration changes to the virtualized hardware.</span></span>

```azurecli
az vm deallocate --resource-group <resource-group-name> --name <vm-name>
```

<span data-ttu-id="df06b-122">그런 다음, 디스크 크기를 조정하려면 `az disk update`를 사용하여 디스크 이름, 리소스 그룹 이름 및 새로 요청한 크기를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-122">Next, to resize a disk, you use `az disk update`, passing the disk name, resource group name, and newly requested size.</span></span> <span data-ttu-id="df06b-123">관리 디스크를 확장하면 지정된 크기가 가장 가까운 관리 디스크 크기에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-123">When you expand a managed disk, the specified size is mapped to the nearest managed disk size.</span></span>

```azurecli
az disk update \
    --resource-group <resource-group-name> \
    --name <disk-name> \
    --size-gb 200
```

<span data-ttu-id="df06b-124">마지막으로 `az vm start`를 사용하여 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-124">Finally, you start the VM again with `az vm start`:</span></span>

```azurecli
az vm start --resource-group <resource-group-name> --name <vm-name>
```

## <a name="expanding-a-disk-using-the-azure-portal"></a><span data-ttu-id="df06b-125">Azure Portal을 사용하여 디스크 확장</span><span class="sxs-lookup"><span data-stu-id="df06b-125">Expanding a disk using the Azure portal</span></span>

<span data-ttu-id="df06b-126">Azure Portal을 사용하여 디스크를 확장하는 것이 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-126">Expanding a disk using the Azure portal is even easier.</span></span>

1. <span data-ttu-id="df06b-127">VM의 **개요** 보기에 있는 도구 모음에서 **중지** 단추를 사용하여 VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-127">Stop the VM using the **Stop** button in the toolbar on the **Overview** view of the VM.</span></span>

1. <span data-ttu-id="df06b-128">**설정** 섹션에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-128">Click **Disks** in the **Settings** section.</span></span>

1. <span data-ttu-id="df06b-129">크기를 조정할 데이터 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-129">Select the data disk you want to resize.</span></span>

    ![강조 표시된 항목을 편집하려는 VHD가 있는 VM의 디스크 섹션을 보여 주는 스크린샷](../media/5-portal-disks.png)

1. <span data-ttu-id="df06b-131">디스크 세부 정보에서 현재 크기보다 _큰_ 크기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-131">In the disk details, type a size _larger_ than the current size.</span></span> <span data-ttu-id="df06b-132">여기서 프리미엄에서 표준 (또는 그 반대로)으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-132">You can also change from Premium to Standard (or vice-versa) here.</span></span> <span data-ttu-id="df06b-133">이러한 설정은 예측된 IOPS 섹션에 표시된 대로 성능을 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-133">These settings will adjust your performance as shown in the predicted IOPS section.</span></span>

    ![새 크기 필드가 강조 표시된 VHD 편집 화면을 보여 주는 스크린샷](../media/5-resize-disk.png)

1. <span data-ttu-id="df06b-135">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-135">Click **Save** to save the changes.</span></span>

1. <span data-ttu-id="df06b-136">VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-136">Restart the VM.</span></span>


### <a name="expanding-the-partition"></a><span data-ttu-id="df06b-137">파티션 확장</span><span class="sxs-lookup"><span data-stu-id="df06b-137">Expanding the partition</span></span>

<span data-ttu-id="df06b-138">새 데이터 디스크를 추가하는 것처럼 확장된 디스크는 파티션과 파일 시스템을 확장할 때까지 사용 가능한 공간을 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-138">Just like adding a new data disk, an expanded disk won't add any usable space until you expand the partition and filesystem.</span></span> <span data-ttu-id="df06b-139">이 작업은 VM에서 사용할 수 있는 OS 도구를 통해 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-139">This must be done using the OS tools available to the VM.</span></span> 

<span data-ttu-id="df06b-140">Windows에서는 디스크 관리자 도구 또는 `diskpart` 명령줄 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-140">On Windows, we would use the Disk Manager tool or the `diskpart` command line tool.</span></span>

<span data-ttu-id="df06b-141">Linux에서는 `parted` 및 `resize2fs`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-141">On Linux, you will use `parted` and `resize2fs`.</span></span>

<span data-ttu-id="df06b-142">이러한 명령 중 일부를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df06b-142">Let's try out some of these commands.</span></span>