<span data-ttu-id="c5d6d-101">업로드의 크기가 얼마나 커질 수 있는지 과소평가했으며, 업로드 디스크 공간이 부족합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-101">We underestimated how big some of the uploads would be and our upload disk is running out of space.</span></span> <span data-ttu-id="c5d6d-102">여러분은 공간을 두 배로 늘리고 64GB에서 128GB로 업그레이드 하기로 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-102">You decide to double the space and upgrade it from 64 GB to 128 GB.</span></span>

## <a name="resize-the-data-disk"></a><span data-ttu-id="c5d6d-103">데이터 디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c5d6d-103">Resize the data disk</span></span>

<span data-ttu-id="c5d6d-104">디스크 크기를 조정하려면 디스크 ID 또는 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-104">To resize a disk, we need the ID or name of the disk.</span></span> <span data-ttu-id="c5d6d-105">이 예에서는 이름(uploadDataDisk1)을 이미 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-105">In this case we already know the name (uploadDataDisk1).</span></span> <span data-ttu-id="c5d6d-106">그러나 이름이 기억 나지 않거나 다른 사용자가 이름을 만든 경우 `az disk list` 명령을 사용하여 디스크 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-106">But in case we didn't remember that, or it was created by someone else we can get a list of disks using the `az disk list` command.</span></span>

1. <span data-ttu-id="c5d6d-107">먼저 리소스 그룹의 관리 디스크 목록을 가져옵니다. 단일 리소스 그룹에서 여러 VM이 있는 경우 다른 디스크가 여기에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-107">Start by getting a list of the managed disks in the resource group; this might include other disks if you have multiple VMs in a single resource group.</span></span> <span data-ttu-id="c5d6d-108">이 예에서는 우리가 만든 웹 서버만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-108">For our example, there should just be our web server.</span></span>

    ```azurecli
    az disk list \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

1. <span data-ttu-id="c5d6d-109">다음으로, `az vm deallocate` 명령을 사용하여 VM을 중지 및 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-109">Next, stop and deallocate the VM using `az vm deallocate`.</span></span> 

    ```azurecli
    az vm deallocate --name support-web-vm01
    ```
1. <span data-ttu-id="c5d6d-110">이제 `az disk update` 명령을 사용하여 디스크 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-110">Now we can resize the disk with the `az disk update` command.</span></span>

    ```azurecli
    az disk update --name uploadDataDisk1 --size-gb 128
    ```
    
1. <span data-ttu-id="c5d6d-111">크기 조정 작업이 완료되면 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-111">Once the resize operation has completed, restart the VM.</span></span>

    ```azurecli
    az vm start --name support-web-vm01
    ```

## <a name="expand-the-disk-partition"></a><span data-ttu-id="c5d6d-112">디스크 파티션 확장</span><span class="sxs-lookup"><span data-stu-id="c5d6d-112">Expand the disk partition</span></span>

<span data-ttu-id="c5d6d-113">마지막 단계는 사용 가능한 공간에 대해 OS에 알려주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-113">The final step is to tell the OS about the available space.</span></span> <span data-ttu-id="c5d6d-114">앞서 수행한 분할 및 형식 단계와 마찬가지로, 이 프로세스는 온-프레미스 디스크 확장과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-114">Just like the partitioning and format steps we did earlier, this process is identical for on-premise disk expansions.</span></span> 

1. <span data-ttu-id="c5d6d-115">먼저 VM의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-115">First, get the public IP address of your VM.</span></span> <span data-ttu-id="c5d6d-116">VM이 다시 부팅되었기 때문에 IP 주소도 변경되었을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-116">Since it was rebooted, it has likely changed.</span></span> <span data-ttu-id="c5d6d-117">이번에는 다른 방법을 시도하고 필터에 `az vm show` 명령을 사용하여 공용 IP 주소를 반환하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-117">Let's try a different approach this time and use `az vm show` with a filter to return the public IP address.</span></span>

    > [!TIP]
    > <span data-ttu-id="c5d6d-118">IP 주소는 기본적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-118">IP addresses are dynamic by default.</span></span> <span data-ttu-id="c5d6d-119">Azure DNS가 IP 변경 내용을 자동으로 보정하지만, 고정 IP 주소를 사용하여 동작을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-119">Azure DNS will automatically compensate for the IP change, or you can alter the behavior by using static IP addresses.</span></span>

    ```azurecli
    az vm show --name support-web-vm01 -d --query [publicIps] --o tsv
    ```
    
1. <span data-ttu-id="c5d6d-120">Linux 머신에 SSH로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-120">SSH into the Linux machine.</span></span> <span data-ttu-id="c5d6d-121">올바른 IP 주소를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-121">You will need to supply your correct IP address.</span></span>

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. <span data-ttu-id="c5d6d-122">디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-122">Unmount the disk.</span></span> <span data-ttu-id="c5d6d-123">디스크는 `/dev/sdc1`였습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-123">Recall that it was `/dev/sdc1`.</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

1. <span data-ttu-id="c5d6d-124">관리자 권한 shell에서 `parted` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-124">Launch `parted` in an elevated shell</span></span>

    ```bash
    sudo parted /dev/sdc
    ```
    
1. <span data-ttu-id="c5d6d-125">`resizepart` 명령을 사용하여 파티션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-125">Expand the partition with the `resizepart` command.</span></span> <span data-ttu-id="c5d6d-126">파티션 1 및 새 크기(128GB)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-126">Enter partition 1 and the new size (128GB).</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [64GB]? 128GB
    ```

    > [!WARNING]
    > <span data-ttu-id="c5d6d-127">크기에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-127">Be careful about the size.</span></span> <span data-ttu-id="c5d6d-128">파티션 크기를 조정하여 파티션을 축소할 수 있으며, 이 경우 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-128">Resizing the partition allows you to shrink a partition too, and that will likely result in data loss.</span></span>
    
1. <span data-ttu-id="c5d6d-129">`quit` 명령을 입력하여 도구를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-129">Exit the tool by typing `quit`.</span></span>

1. <span data-ttu-id="c5d6d-130">파티션 도구가 자동으로 드라이브를 _다시 탑재_합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-130">The partition tool will automatically _remount_ the drive.</span></span> <span data-ttu-id="c5d6d-131">포맷할 수 있도록 드라이브를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-131">So unmount it again so we can format it.</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```
    
1. <span data-ttu-id="c5d6d-132">`e2fsck` 명령을 사용하여 파티션 일관성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-132">Verify the partition consistency with `e2fsck`.</span></span> <span data-ttu-id="c5d6d-133">이 단계는 반드시 필요하지만, 언제든지 디스크 볼륨의 크기를 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-133">This step is absolutely necessary but is a good idea any time you are changing sizes on a disk volume.</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

1. <span data-ttu-id="c5d6d-134">`resize2fs` 명령을 사용하여 파일 시스템 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-134">Resize the filesystem with `resize2fs`.</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

1. <span data-ttu-id="c5d6d-135">마지막으로, 드라이브를 탑재 지점에 다시 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-135">Finally, mount the drive back to the mount point.</span></span>

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```

<span data-ttu-id="c5d6d-136">OS 디스크 크기를 조정했는지 확인하려면 `df -h`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-136">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="c5d6d-137">이제 드라이브가 128GB로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d6d-137">It should now show that the drive is 128 GB.</span></span>
