<span data-ttu-id="c291e-101">우리 법률 사무소에서는 담당 건수를 확대하고 있으며, 귀하는 의뢰인, 다른 법률 사무소, 법 집행 기관 등 다양한 출처의 중요한 문서를 저장할 새로운 Linux 웹 서버를 설치하는 일을 맡았습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-101">Our law firm is expanding it's case load and you have been tasked with putting up a new Linux web server to store critical documents from a variety of sources - clients, other law firms, and law enforcement offices.</span></span> <span data-ttu-id="c291e-102">우리 서버는 업로드를 허용할 수 있으며, 업로드를 디스크에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-102">Our server can accept uploads and needs to store them on disk.</span></span>

> [!TIP]
> <span data-ttu-id="c291e-103">이 연습에서는 Linux를 예시로 사용하지만 VM을 만들고 디스크를 추가하는 기본적인 프로세스는 Windows도 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-103">This exercise uses Linux as the example, but the basic process of creating VMs and adding disks is the same for Windows.</span></span> <span data-ttu-id="c291e-104">주요 차이점은 디스크 분할 및 포맷을 원격 데스크톱 세션에서 기본 제공 디스크 관리 도구를 사용하여 수행한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-104">The primary difference would be in partitioning and formatting the disk - that would be done in a Remote Desktop session using the built-in Disk Management tools.</span></span>

<span data-ttu-id="c291e-105">연습의 목표는 Linux VM(가상 머신)을 만들고 "uploadDataDisk1"이라는 새 VHD(가상 하드 디스크)를 연결하여 "uploads" 디렉터리를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-105">The goal of the exercise is to create a Linux virtual machine (VM) and attach a new virtual hard disk (VHD) named "uploadDataDisk1" to store the "uploads" directory.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm"></a><span data-ttu-id="c291e-106">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c291e-106">Create a Linux VM</span></span>

<span data-ttu-id="c291e-107">Azure CLI를 사용하여 웹 서버를 호스트하는 Linux VM을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-107">Let's create a Linux VM to host our web server using the Azure CLI.</span></span>

1. <span data-ttu-id="c291e-108">먼저 이 세션의 몇 가지 기본값을 설정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-108">Start by setting some defaults for this session.</span></span> <span data-ttu-id="c291e-109">가장 먼저 결정해야 할 것은 VM을 배치할 _위치_입니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-109">The first thing you need to decide is the _location_ to place the VM.</span></span> <span data-ttu-id="c291e-110">이상적으로 클라이언트와 가까운 위치가 좋겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-110">Ideally this would be close to your clients.</span></span> <span data-ttu-id="c291e-111">이 경우 사용 가능한 위치 중 Azure 샌드박스와 가장 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-111">In this case, select the closest region from the locations available to the Azure Sandbox.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="c291e-112">`az configure` 명령을 사용하여 사용할 기본 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-112">Use the `az configure` command to set the default location you want to use.</span></span> <span data-ttu-id="c291e-113">"eastus"를 해당 위치로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-113">Replace "eastus" with the location.</span></span>

    ```azurecli
    az configure --defaults location=eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="c291e-114">Azure 샌드박스: **<rgn>[샌드박스 리소스 그룹]</rgn>** 에 생성된, 사전 구성된 리소스 그룹에 기본 리소스 그룹 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-114">Set the default resource group value to the pre-configured resource group created for the Azure Sandbox: **<rgn>[Sandbox resource group]</rgn>**</span></span>

    ```azurecli
    az configure --defaults group="<rgn>[Sandbox Resource Group]</rgn>"
    ```

1. <span data-ttu-id="c291e-115">다음으로, `vm create` 명령을 사용하여 새로운 Ubuntu Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-115">Next, use the `vm create` command to create a new Ubuntu Linux VM.</span></span>
    - <span data-ttu-id="c291e-116">이름을 "support-web-vm01"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-116">Name it "support-web-vm01".</span></span>
    - <span data-ttu-id="c291e-117">**size**를 _Standard_DS2_v2_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-117">Set the **size** to _Standard_DS2_v2_.</span></span>
    - <span data-ttu-id="c291e-118">**admin-username**을 "azureuser"(또는 원하는 다른 이름)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-118">Set the **admin-username** to "azureuser" (or whatever you prefer).</span></span>
    - <span data-ttu-id="c291e-119">`--generate-ssh-keys` 매개 변수를 사용하여 SSH 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-119">Generate SSH keys with the `--generate-ssh-keys` parameter.</span></span>

    ```azurecli
    az vm create --name support-web-vm01 \
        --image UbuntuLTS \
        --size Standard_DS2_v2 \
        --admin-username azureuser \
        --generate-ssh-keys
    ```
    
    > [!TIP]
    > <span data-ttu-id="c291e-120">VM을 만들고 Azure에 배포하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-120">Creating your VM and deploying it in Azure can take a few minutes.</span></span> <span data-ttu-id="c291e-121">Cloud Shell에서 진행 상황을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-121">You can watch the progress in the Cloud Shell.</span></span>
    
1. <span data-ttu-id="c291e-122">이렇게 하면 생성된 VM에 대한 세부 정보가 포함된 JSON 블록이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-122">This will result in a JSON block with the details about the created VM.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/xxx/resourceGroups/<rgn>[Sandbox resource group]</rgn>/providers/Microsoft.Compute/virtualMachines/support-web-vm01",
        "location": "eastus",
        "macAddress": "00-0D-3A-18-DE-B4",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "40.76.193.249",
        "resourceGroup": "<rgn>[Sandbox resource group]</rgn>",
        "zones": ""
    }
    ```
    <span data-ttu-id="c291e-123">출력의 **publicIpAddress**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-123">Note of the **publicIpAddress** in your output.</span></span> <span data-ttu-id="c291e-124">이를 통해 VM에 원격으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-124">This is how we can access the VM remotely.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c291e-125">이 VM은 디스크 관리 방법을 알아보는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-125">We are using this VM to learn how to manage disks.</span></span> <span data-ttu-id="c291e-126">웹 서버로 사용할 예정이었다면 `az vm open-port` 명령을 사용하여 추가 포트를 열고 웹 서버 소프트웨어를 설치했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-126">If we were truly going to use it as a web server, we'd want to open up additional ports with the `az vm open-port` command, and install web server software.</span></span> <span data-ttu-id="c291e-127">이러한 작업은 이 모듈의 범위를 벗어나지만 **Azure CLI로 가상 머신 관리** 모듈을 통해 이러한 단계를 수행하는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-127">These tasks are outside the scope of this module, but you can go through the **Manage virtual machines with the Azure CLI** module to learn how to do these steps.</span></span> 

## <a name="add-an-empty-data-disk-to-our-vm"></a><span data-ttu-id="c291e-128">VM에 빈 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="c291e-128">Add an empty data disk to our VM</span></span>

<span data-ttu-id="c291e-129">웹 서버의 "uploads" 디렉터리를 저장하는 디스크의 이름을 "uploadDataDisk1"로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-129">We're going to name the disk that stores the "uploads" directory for your web server "uploadDataDisk1".</span></span> 

> [!TIP]
> <span data-ttu-id="c291e-130">VM 생성 시 `vm create` 명령에 `--data-disk-sizes-gb` 매개 변수를 사용하여 데이터 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-130">You can add data disks when the VM is created using the `--data-disk-sizes-gb` parameter on the `vm create` command.</span></span>

1. <span data-ttu-id="c291e-131">`vm disk attach` 명령을 사용하여 서버에 새로운 빈 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-131">Add a new empty disk to the server with the `vm disk attach` command.</span></span>
    - <span data-ttu-id="c291e-132">이름을 "uploadDataDisk1"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-132">Name it "uploadDataDisk1"</span></span>
    - <span data-ttu-id="c291e-133">64GB로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-133">Set it to be 64 GB.</span></span>
    - <span data-ttu-id="c291e-134">로컬 중복을 지원하는 프리미엄 저장소를 사용하기 위해 **sku**를 "_Premium_LRS_"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-134">Set the **sku** to "_Premium_LRS_" so we use premium storage with local redundancy.</span></span>

    ```azurecli
    az vm disk attach \
        --vm-name support-web-vm01 \
        --disk uploadDataDisk1 \
        --size-gb 64 \
        --sku Premium_LRS \
        --new
    ```
    
<span data-ttu-id="c291e-135">이제 "uploadDataDisk1"이라는 디스크가 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-135">We've now defined a disk named "uploadDataDisk1" .</span></span> <span data-ttu-id="c291e-136">이 디스크를 사용하려면 분할하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-136">To use the disk, we'll need to partition and format it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="c291e-137">데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="c291e-137">Initialize data disks</span></span>

<span data-ttu-id="c291e-138">처음부터 작성하는 모든 추가 드라이브는 초기화하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-138">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="c291e-139">이 과정을 수행하는 프로세스는 실제 디스크용 프로세스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-139">The process for doing this is identical to a physical disk:</span></span>

1. <span data-ttu-id="c291e-140">먼저 원래 VM 생성 응답에서 얻은 공용 IP 주소를 사용하여 Linux 서버에 SSH로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-140">First, SSH into the Linux server using the public IP address you got back from the original VM creation response.</span></span> <span data-ttu-id="c291e-141">해당 주소가 없다면 다음 명령을 사용하여 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-141">If you don't have that, you can use the following command to get the IP address:</span></span>

    ```azurecli
    az vm list-ip-addresses -n support-web-vm01
    ```

1. <span data-ttu-id="c291e-142">자신이 만든 공용 IP 및 사용자 이름과 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-142">Use SSH with the public IP and the username you created.</span></span>

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. <span data-ttu-id="c291e-143">다음으로, 모든 블록 장치를 나열하는 `lsblk` 명령을 사용하여 디스크를 식별합니다. 여기에 드라이브가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-143">Next, identify the disk with the `lsblk` command to list all the block devices - here you will see your drives.</span></span>

    ```bash
    lsblk
    ```

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom
    sdc      8:32   0   64G  0 disk
    sda      8:0    0   30G  0 disk
    └─sda1   8:1    0   30G  0 part /
    ```

<span data-ttu-id="c291e-144">우리가 만든 64GB 드라이브를 찾아보세요. 여기에는 **sdc**가 있으며 탑재되지 않은 것을 알 수 있습니다. 초기화되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-144">Look for the 64 GB drive we created - here you can see it's **sdc** and it's not mounted - this is because it's not been initialized.</span></span>

1. <span data-ttu-id="c291e-145">드라이브(**sdc**)가 확인되면 초기화를 수행해야 합니다. `fdisk`를 사용하면 초기화를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-145">Once you know the drive (**sdc**) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="c291e-146">`sudo`를 포함해 명령을 실행하고 파티션을 지정할 디스크를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-146">You will need to run the command with `sudo` and supply the disk you want to partition:</span></span>

    ```bash
    sudo fdisk /dev/sdc
    ```

1. <span data-ttu-id="c291e-147">새 파티션을 추가하려면 <kbd>n</kbd> 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-147">Use the <kbd>n</kbd> command to add a new partition.</span></span> <span data-ttu-id="c291e-148">또한 이 예제에서는 주 파티션에 대해 <kbd>p</kbd>를 선택하고 나머지 기본값을 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-148">In this example, we also choose <kbd>p</kbd> for a primary partition and accept the rest of the default values.</span></span> <span data-ttu-id="c291e-149">출력은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-149">The output will be similar to the following example:</span></span>   

    ```output
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x3b44089f.
    
    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-268435455, default 2048):
    Last sector, +sectors or +size{K,M,G,T,P} ...
    Created a new partition 1 of type 'Linux' and of size 64 GiB.    
    ```

1. <span data-ttu-id="c291e-150"><kbd>p</kbd> 명령을 사용하여 파티션 테이블을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-150">Print the partition table with the <kbd>p</kbd> command.</span></span> <span data-ttu-id="c291e-151">인쇄한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-151">It should look something like this:</span></span>

    ```output
    Disk /dev/sdc: 64 GiB ...
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 4096 bytes
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
    Disklabel type: dos
    Disk identifier: 0x3b44089f
    
    Device     Boot Start ... Size Id Type
    /dev/sdc1        2048 ... 64G 83 Linux
    ```

1. <span data-ttu-id="c291e-152"><kbd>w<kbd> 명령을 사용하여 변경 내용을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-152">Write the changes with the <kbd>w<kbd> command.</span></span> <span data-ttu-id="c291e-153">그러면 도구가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-153">This will exit the tool.</span></span>

1. <span data-ttu-id="c291e-154">이제 `mkfs` 명령을 사용하여 파티션에 파일 시스템을 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-154">Next, we need to write a file system to the partition with the `mkfs` command.</span></span> <span data-ttu-id="c291e-155">이렇게 하려면 `fdisk` 출력에서 가져온 파일 시스템 유형과 장치 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-155">We will need to specify the file system type and device name that we got from the `fdisk` output:</span></span>
    - <span data-ttu-id="c291e-156">`-t ext4`를 전달하여 _ext4_ 파일 시스템을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-156">Pass `-t ext4` to create an _ext4_ filesystem.</span></span>
    - <span data-ttu-id="c291e-157">장치 이름은 `/dev/sdc`입니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-157">The device name is `/dev/sdc`.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    <span data-ttu-id="c291e-158">이 명령을 완료하는 데 1분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-158">This command will take a minute or so to complete.</span></span>

    ```output
    mke2fs 1.42.13 (17-May-2015)
    Discarding device blocks: done
    Creating filesystem with 16777088 4k blocks and 4194304 inodes
    ...
    Allocating group tables: done
    Writing inode tables: done
    Creating journal (32768 blocks): done
    Writing superblocks and filesystem accounting information: done
    ```
    
1. <span data-ttu-id="c291e-159">다음으로, 탑재 지점으로 사용할 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-159">Next, create a directory we will use as our mount point.</span></span> <span data-ttu-id="c291e-160">여기서는 `uploads` 폴더가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-160">Let's assume we will have a `uploads` folder:</span></span>

    ```bash
    sudo mkdir /uploads
    ```
1. <span data-ttu-id="c291e-161">마지막으로 `mount`를 사용하여 탑재 지점에 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-161">Finally, use `mount` to attach the disk to the mount point:</span></span>

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```
    <span data-ttu-id="c291e-162">이제 `lsblk`를 사용하여 탑재된 드라이브를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-162">You should be able to use `lsblk` to see the mounted drive now:</span></span>
    
    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom
    sdc      8:32   0   64G  0 disk
    └─sdc1   8:33   0   64G  0 part /uploads
    sda      8:0    0   30G  0 disk
    └─sda1   8:1    0   30G  0 part /
    ```
    
### <a name="mounting-the-drive-automatically"></a><span data-ttu-id="c291e-163">드라이브 자동 탑재</span><span class="sxs-lookup"><span data-stu-id="c291e-163">Mounting the drive automatically</span></span>

<span data-ttu-id="c291e-164">다시 부팅 후 드라이브가 자동으로 다시 탑재되도록 하려면 `/etc/fstab` 파일에 드라이브를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-164">To ensure that the drive is mounted automatically after a reboot, it must be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="c291e-165">또한 `/etc/fstab`에 UUID(Universally Unique Identifier)를 사용하여 장치 이름만 사용하는 대신 `/dev/sdc1`과 같이 드라이브를 가리키는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-165">It is also highly recommended that the UUID (universally unique identifier) is used in `/etc/fstab` to refer to the drive rather than just the device name (such as `/dev/sdc1`).</span></span> <span data-ttu-id="c291e-166">부팅하는 동안 OS에서 디스크 오류를 검색하는 경우 UUID를 사용하여 지정된 위치에 탑재되어 있는 잘못된 디스크를 회피합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-166">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="c291e-167">나머지 데이터 디스크에는 동일한 장치 ID가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-167">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="c291e-168">새 드라이브의 UUID를 찾으려면 `blkid` 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-168">To find the UUID of the new drive, use the `blkid` utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="c291e-169">그러면 다음과 같은 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-169">It will return something like:</span></span>

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. <span data-ttu-id="c291e-170">`/dev/sdc1` 드라이브의 UUID를 복사하고 텍스트 편집기에서 `/etc/fstab` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-170">Copy the UUID for the `/dev/sdc1` drive and open the `/etc/fstab` file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> <span data-ttu-id="c291e-171">`/etc/fstab` 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-171">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="c291e-172">확실하지 않은 경우 배포판의 설명서에서 이 파일을 올바르게 편집하는 방법에 대한 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c291e-172">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="c291e-173">또한 프로덕션 시스템에서 작업할 때는 편집하기 전에 파일의 백업을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-173">It is also recommended that a backup of the file is created before editing when you are working with production systems.</span></span>

1. <span data-ttu-id="c291e-174"><kbd>G</kbd> 키를 눌러 파일의 마지막 줄로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-174">Press <kbd>G</kbd> to move to the last line in the file.</span></span>

1. <span data-ttu-id="c291e-175"><kbd>I</kbd> 키를 눌러 삽입 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-175">Press <kbd>I</kbd> to enter INSERT mode.</span></span> <span data-ttu-id="c291e-176">화면 아래쪽에 모드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-176">It should indicate the mode at the bottom of the screen.</span></span>

1. <span data-ttu-id="c291e-177"><kbd>End</kbd> 키를 눌러 줄 맨 끝으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-177">Press the <kbd>END</kbd> key to move to the end of the line.</span></span> <span data-ttu-id="c291e-178">화살표 키를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-178">Alternatively, you can use the arrow keys.</span></span> <span data-ttu-id="c291e-179"><kbd>Enter</kbd> 키를 눌러 새 줄로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-179">Press <kbd>ENTER</kbd> to move to a new line.</span></span>

1. <span data-ttu-id="c291e-180">편집기에 다음 줄을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-180">Type the following line into the editor.</span></span> <span data-ttu-id="c291e-181">값은 공백이나 탭으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-181">The values can be space or tab separated.</span></span> <span data-ttu-id="c291e-182">각 열에 대한 자세한 내용은 설명서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c291e-182">Check the documentation for more information on each of the columns:</span></span>

    ```output
    UUID=<uuid-goes-here>    /uploads    ext4    defaults,nofail    1    2
    ```
1. <span data-ttu-id="c291e-183">**ESC** 키를 누른 다음, **:w!** 를 입력하여</span><span class="sxs-lookup"><span data-stu-id="c291e-183">Press **ESC**, then type **:w!**</span></span> <span data-ttu-id="c291e-184">파일을 작성하고 **:q**를 입력하여 편집기를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-184">to write the file and **:q** to quit the editor.</span></span>

1. <span data-ttu-id="c291e-185">마지막으로 OS가 탑재 지점을 새로 고치도록 하여 입력 내용이 정확한지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-185">Finally, let's check to make sure the entry is correct by asking the OS to refresh the mount points:</span></span>

    ```bash
    sudo mount -a
    ```

    <span data-ttu-id="c291e-186">오류가 반환되면 파일을 편집하여 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-186">If it returns an error, edit the file to find the problem.</span></span>

> [!TIP]
> <span data-ttu-id="c291e-187">일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-187">Some Linux kernels support TRIM to discard unused blocks on disks.</span></span> <span data-ttu-id="c291e-188">이 기능은 Azure 디스크에서 사용할 수 있으며 큰 파일을 만든 다음, 삭제하면 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-188">This feature is available on Azure disks and can save you money if you create large files and then delete them.</span></span> <span data-ttu-id="c291e-189">설명서에서 [이 기능을 설정](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure)하는 방법을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c291e-189">Learn how to [turn this feature on](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure) in our documentation.</span></span>

<span data-ttu-id="c291e-190">지금까지 VM에 디스크를 추가하는 것이 얼마나 쉬운지 알아보았으므로 생성 가능한 디스크 유형에 대해 좀 더 살펴보도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-190">Now that you've seen how easy it is to add disks to your VMs, let's explore a bit more about the types of disks you might create.</span></span> <span data-ttu-id="c291e-191">특히 선택 가능한 표준 및 프리미엄 저장소에 대해 알아보도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c291e-191">In particular the choice between Standard and Premium storage.</span></span>