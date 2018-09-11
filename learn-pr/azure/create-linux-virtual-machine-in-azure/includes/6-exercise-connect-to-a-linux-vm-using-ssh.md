<span data-ttu-id="52100-101">Linux VM을 배포하여 실행하기는 했지만, 해당 VM은 작업을 수행하도록 구성되지는 않은 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="52100-101">We have our Linux VM deployed and running, but it's not configured to do any work.</span></span> <span data-ttu-id="52100-102">VM을 SSH에 연결하고 Apache를 구성해 보겠습니다. 그러면 실행되는 웹 서버가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-102">Let's connect to it with SSH and configure Apache, so we have a running web server.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="52100-103">SSH를 사용하여 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="52100-103">Connect to the VM with SSH</span></span>

<span data-ttu-id="52100-104">Azure VM을 SSH 클라이언트와 연결하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-104">To connect to an Azure VM with an SSH client, you will need:</span></span>

- <span data-ttu-id="52100-105">SSH 클라이언트 소프트웨어(대다수 최신 운영 체제에 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="52100-105">SSH client software (present on most modern operating systems)</span></span>
- <span data-ttu-id="52100-106">VM의 공용 IP 주소(VM이 사용자 네트워크에 연결하도록 구성된 경우에는 개인 IP 주소)</span><span class="sxs-lookup"><span data-stu-id="52100-106">The public IP address of the VM (or private if the VM is configured to connect to your network)</span></span>

### <a name="get-the-public-ip-address"></a><span data-ttu-id="52100-107">공용 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="52100-107">Get the public IP address</span></span>

1. <span data-ttu-id="52100-108">[Azure Portal](https://portal.azure.com?azure-portal=true)에서 이전에 만든 가상 머신의 **개요** 패널이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-108">In the [Azure portal](https://portal.azure.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="52100-109">해당 패널을 열어야 하는 경우 **모든 리소스** 아래에서 VM을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-109">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="52100-110">요약 패널에는 VM과 관련된 많은 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-110">The overview panel has a lot of information about the VM.</span></span>

    - <span data-ttu-id="52100-111">VM이 실행 중인지도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-111">You can see whether the VM is running</span></span>
    - <span data-ttu-id="52100-112">VM 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="52100-112">Stop or restart it</span></span>
    - <span data-ttu-id="52100-113">VM에 연결하기 위한 공용 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="52100-113">Get the public IP address to connect to the VM</span></span>
    - <span data-ttu-id="52100-114">CPU, 디스크 및 네트워크의 활동 확인</span><span class="sxs-lookup"><span data-stu-id="52100-114">See the activity of the CPU, disk, and network</span></span>

1. <span data-ttu-id="52100-115">창 위쪽에서 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-115">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="52100-116">**가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-116">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings.</span></span> <span data-ttu-id="52100-117">**SSH** 탭에는 VM에 연결하기 위해 로컬로 실행해야 하는 명령도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-117">On the **SSH** tab, you will also find the command you need to execute locally to connect to the VM.</span></span> <span data-ttu-id="52100-118">이 명령을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-118">Copy this to the clipboard.</span></span>

<!-- TODO: this will be necessary if we ever have inline portal integration 

### Open the Azure Cloud Shell

Let's use the Cloud Shell in the Azure Portal. If you generated the SSH key locally, you need to use your local session since the private key won't be in your storage account.

1. Switch back to the **Dashboard** by clicking the Dashboard button in the Azure sidebar.

1. Open the Cloud Shell by clicking the shell button in the top toolbar.

    ![Open the Azure Cloud Shell](../media-drafts/6-cloud-shell.png)

1. Select **Bash** as the shell type. PowerShell is also available if you are a Windows administrator.

    ![Select bash shell in the portal](../media-drafts/6-use-bash-shell.png)

-->

## <a name="connect-with-ssh"></a><span data-ttu-id="52100-119">SSH를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="52100-119">Connect with SSH</span></span>

1. <span data-ttu-id="52100-120">SSH 탭에서 가져온 명령줄을 Cloud Shell에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-120">Paste the command line you got from the SSH tab into the Cloud Shell.</span></span> <span data-ttu-id="52100-121">해당 명령줄은 다음과 같습니다. 하지만 실제 IP 주소는 다르며, **jim**을 사용하지 않았다면 사용자 이름도 다를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="52100-121">It should look something like this; however it will have a different IP address (and perhaps a different username if you didn't use **jim**!)</span></span>

    ```bash
    ssh jim@137.117.101.249
    ```

1. <span data-ttu-id="52100-122">이 명령은 Secure Shell 연결을 열고 일반적인 Linux용 셸 명령 프롬프트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-122">This command will open a secure shell connection and place you at a traditional shell command prompt for Linux.</span></span>

1. <span data-ttu-id="52100-123">몇 가지 Linux 명령을 실행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="52100-123">Try executing a few Linux commands</span></span>
    - <span data-ttu-id="52100-124">`ls -la /`: 디스크 루트 표시</span><span class="sxs-lookup"><span data-stu-id="52100-124">`ls -la /` to show the root of the disk</span></span>
    - <span data-ttu-id="52100-125">`ps -l`: 실행 중인 모든 프로세스 표시</span><span class="sxs-lookup"><span data-stu-id="52100-125">`ps -l` to show all the running processes</span></span>
    - <span data-ttu-id="52100-126">`dmesg`: 모든 커널 메시지 나열</span><span class="sxs-lookup"><span data-stu-id="52100-126">`dmesg` to list all the kernel messages</span></span>
    - <span data-ttu-id="52100-127">`lsblk`: 모든 블록 장치 나열(여기에 드라이브가 표시됨)</span><span class="sxs-lookup"><span data-stu-id="52100-127">`lsblk` to list all the block devices - here you will see your drives</span></span>

<span data-ttu-id="52100-128">드라이브 목록에서 더 자세히 살펴보아야 할 사항은 _누락_ 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="52100-128">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="52100-129">**데이터** 드라이브(`sdc`)가 있는데 파일 시스템에 탑재되어 있지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-129">Notice that our **Data** drive (`sdc`) is present but not mounted into the file system.</span></span> <span data-ttu-id="52100-130">Azure에서 VHD를 추가했지만 초기화하지는 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="52100-130">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="52100-131">데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="52100-131">Initialize data disks</span></span>

<span data-ttu-id="52100-132">처음부터 작성하는 모든 추가 드라이브는 초기화하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-132">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="52100-133">이 과정을 수행하는 프로세스는 실제 디스크용 프로세스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-133">The process for doing this is identical to a physical disk.</span></span>

1. <span data-ttu-id="52100-134">먼저 디스크를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-134">First, identify the disk.</span></span> <span data-ttu-id="52100-135">이 작업은 앞에서 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-135">We did that above.</span></span> <span data-ttu-id="52100-136">SCSI 장치용 커널의 모든 메시지를 나열하는 `dmesg | grep SCSI`를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-136">You could also use `dmesg | grep SCSI` which will list all the messages from the kernel for SCSI devices.</span></span>

1. <span data-ttu-id="52100-137">드라이브(`sdc`)가 확인되면 초기화를 수행해야 합니다. `fdisk`를 사용하면 초기화를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-137">Once you know the drive (`sdc`) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="52100-138">`sudo`를 포함해 명령을 실행하고 파티션을 지정할 디스크를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-138">You will need to run the command with `sudo` and supply the disk you want to partition.</span></span>

    ```bash
    sudo fdisk /dev/sdc
    ```
1. <span data-ttu-id="52100-139">새 파티션을 추가하려면 `n` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-139">Use the `n` command to add a new partition.</span></span>  <span data-ttu-id="52100-140">또한 이 예제에서는 주 파티션에 대해 p를 선택하고 나머지 기본값은 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-140">In this example, we also choose p for a primary partition and accept the rest of the default values.</span></span> <span data-ttu-id="52100-141">출력은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-141">The output will be similar to the following example:</span></span>   

    ```output
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x1f2d0c46.
    
    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-2145386495, default 2048):
    Last sector, +sectors or +size{K,M,G,T,P} (2048-2145386495, default 2145386495):
    
    Created a new partition 1 of type 'Linux' and of size 1023 GiB.
    ```    

1. <span data-ttu-id="52100-142">`p` 명령을 사용하여 파티션 테이블을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-142">Print the partition table with the `p` command.</span></span> <span data-ttu-id="52100-143">인쇄한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-143">It should look something like this:</span></span>

    ```output
    Disk /dev/sdc: 1023 GiB, 1098437885952 bytes, 2145386496 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 4096 bytes
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
    Disklabel type: dos
    Disk identifier: 0x1f2d0c46
    
    Device     Boot Start        End    Sectors  Size Id Type
    /dev/sdc1        2048 2145386495 2145384448 1023G 83 Linux
    ```
    
1. <span data-ttu-id="52100-144">`w` 명령을 사용하여 변경 내용을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="52100-144">Write the changes with the `w` command.</span></span> <span data-ttu-id="52100-145">그러면 도구가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-145">This will exit the tool.</span></span>

1. <span data-ttu-id="52100-146">이제 `mkfs` 명령을 사용하여 파티션에 파일 시스템을 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-146">Next, we need to write a file system to the partition with the `mkfs` command.</span></span> <span data-ttu-id="52100-147">이렇게 하려면 `fdisk` 출력에서 가져온 파일 시스템 유형과 장치 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-147">We will need to specify the file system type and device name which we got from the `fdisk` output.</span></span>
    - <span data-ttu-id="52100-148">`-t ext4`를 전달하여 _ext4_ 파일 시스템을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52100-148">Pass `-t ext4` to create an _ext4_ filesystem.</span></span>
    - <span data-ttu-id="52100-149">장치 이름은 `/dev/sdc`입니다.</span><span class="sxs-lookup"><span data-stu-id="52100-149">The device name is `/dev/sdc`.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    <span data-ttu-id="52100-150">이 명령을 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="52100-150">This command will take a few minutes to complete.</span></span>

    ```output
    mke2fs 1.44.1 (24-Mar-2018)
    Discarding device blocks: done
    Creating filesystem with 268173056 4k blocks and 67043328 inodes
    Filesystem UUID: e311c905-e0d9-43ab-af63-7f4ee4ef108e
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
            102400000, 214990848
    
    Allocating group tables: done
    Writing inode tables: done
    Creating journal (262144 blocks): done
    Writing superblocks and filesystem accounting information: done
    ```

1. <span data-ttu-id="52100-151">다음으로는 탑재 지점으로 사용할 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52100-151">Next, create a directory we will use as out mount point.</span></span> <span data-ttu-id="52100-152">여기서는 `data` 폴더가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-152">Let's assume we will have a `data` folder.</span></span>

    ```bash
    sudo mkdir /data
    ```
1. <span data-ttu-id="52100-153">마지막으로 `mount`를 사용하여 탑재 지점에 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-153">Finally, use `mount` to attach the disk to the mount point.</span></span>

    ```bash
    sudo mount /dev/sdc1 /data
    ```
    <span data-ttu-id="52100-154">이제 `lsblk`를 사용하여 탑재된 드라이브를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-154">You should be able to use `lsblk` to see the mounted drive now.</span></span>
    
    ```output
    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda       8:0    0   30G  0 disk
    ├─sda1    8:1    0 29.9G  0 part /
    ├─sda14   8:14   0    4M  0 part
    └─sda15   8:15   0  106M  0 part /boot/efi
    sdb       8:16   0   16G  0 disk
    └─sdb1    8:17   0   16G  0 part /mnt
    sdc       8:32   0 1023G  0 disk
    └─sdc1    8:33   0 1023G  0 part /data
    sr0      11:0    1  628K  0 rom
    ```

### <a name="mounting-the-drive-automatically"></a><span data-ttu-id="52100-155">드라이브 자동 탑재</span><span class="sxs-lookup"><span data-stu-id="52100-155">Mounting the drive automatically</span></span>

<span data-ttu-id="52100-156">다시 부팅 후 드라이브가 자동으로 다시 탑재되도록 하려면 `/etc/fstab` 파일에 드라이브를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-156">To ensure that the drive is mounted automatically after a reboot, it must be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="52100-157">또한 `/etc/fstab`에 UUID(Universally Unique Identifier)를 사용하여 장치 이름만 사용하는 대신 `/dev/sdc1`과 같이 드라이브를 가리키는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-157">It is also highly recommended that the UUID (Universally Unique Identifier) is used in `/etc/fstab` to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="52100-158">부팅하는 동안 OS에서 디스크 오류를 검색하는 경우 UUID를 사용하여 지정된 위치에 탑재되어 있는 잘못된 디스크를 회피합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-158">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="52100-159">그런 다음 남아 있는 데이터 디스크를 동일한 장치 ID에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-159">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="52100-160">새 드라이브의 UUID를 찾으려면 `blkid` 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-160">To find the UUID of the new drive, use the `blkid` utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="52100-161">그러면 다음과 같은 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-161">It will return something like:</span></span>

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. <span data-ttu-id="52100-162">`/dev/sdc1` 드라이브의 UUID를 복사한 다음 텍스트 편집기에서 `/etc/fstab` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52100-162">Copy the UUID for the `/dev/sdc1` drive and open the `/etc/fstab` file in a text editor.</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> <span data-ttu-id="52100-163">`/etc/fstab` 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-163">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="52100-164">확실하지 않은 경우 배포 설명서에서 이 파일을 제대로 편집하는 방법에 대한 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="52100-164">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="52100-165">또한 프로덕션 시스템에서 작업할 때는 편집하기 전에 파일의 백업을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-165">It is also recommended that a backup of the file is created before editing when you are working with production systems.</span></span>

1. <span data-ttu-id="52100-166">**G** 키를 눌러 파일의 마지막 줄로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-166">Press **G** to move to the last line in the file.</span></span>

1. <span data-ttu-id="52100-167">**I** 키를 눌러 삽입 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-167">Press **I** to enter INSERT mode.</span></span> <span data-ttu-id="52100-168">화면 아래쪽에 모드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-168">It should indicate the mode at the bottom of the screen.</span></span>

1. <span data-ttu-id="52100-169">**End** 키를 눌러 줄 맨 끝으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-169">Press the **END** key to move to the end of the line.</span></span> <span data-ttu-id="52100-170">화살표 키를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-170">Alternatively, you can use the arrow keys.</span></span> <span data-ttu-id="52100-171">**Enter** 키를 눌러 새 줄로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-171">Press **ENTER** to move to a new line.</span></span>

1. <span data-ttu-id="52100-172">편집기에 다음 줄을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-172">Type the following line into the editor.</span></span> <span data-ttu-id="52100-173">값은 공백이나 탭으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-173">The values can be space or tab separated.</span></span> <span data-ttu-id="52100-174">각 열에 대한 자세한 내용은 설명서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="52100-174">Check the documentation for more information on each of the columns.</span></span>

    ```output
    UUID=<uuid-goes-here>    /data    ext4    defaults,nofail    1    2
    ```
1. <span data-ttu-id="52100-175">**Esc** 키를 누르고 **:w!** 를 입력하여</span><span class="sxs-lookup"><span data-stu-id="52100-175">Press **ESC**, then type **:w!**</span></span> <span data-ttu-id="52100-176">파일을 쓴 다음 **:q**를 입력하여 편집기를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-176">to write the file, and **:q** to quit the editor.</span></span>

1. <span data-ttu-id="52100-177">마지막으로 OS가 탑재 지점을 새로 고치도록 하여 입력 내용이 정확한지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-177">Finally, let's check to make sure the entry is correct by asking the OS to refresh the mount points.</span></span>

    ```bash
    sudo mount -a
    ```
    
    <span data-ttu-id="52100-178">오류가 반환되면 파일을 편집하여 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-178">If it returns an error, edit the file to find the problem.</span></span>

> [!TIP]
> <span data-ttu-id="52100-179">일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-179">Some Linux kernels support TRIM to discard unused blocks on disks.</span></span> <span data-ttu-id="52100-180">Azure 디스크에서 제공되는 이 기능을 사용하면 큰 파일을 만들었다가 삭제하는 경우 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-180">This feature is available on Azure disks and can save you money if you create large files and then delete them.</span></span> <span data-ttu-id="52100-181">설명서에서 [이 기능을 설정](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure)하는 방법을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="52100-181">Learn how to [turn this feature on](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure) in our documentation.</span></span>

## <a name="install-software-onto-the-vm"></a><span data-ttu-id="52100-182">VM에 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="52100-182">Install software onto the VM</span></span>

<span data-ttu-id="52100-183">여러 가지 옵션을 통해 VM에 소프트웨어를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-183">You have several options to install software onto the VM.</span></span> <span data-ttu-id="52100-184">먼저, 앞에서 설명한 것처럼 `scp`를 사용하여 컴퓨터의 로컬 파일을 VM에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-184">First, as mentioned, you can use `scp` to copy local files from your machine to the VM.</span></span> <span data-ttu-id="52100-185">이렇게 하면 데이터 또는 실행하려는 사용자 지정 응용 프로그램을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-185">This lets you copy over data, or custom applications you want to run.</span></span>

<span data-ttu-id="52100-186">Secure Shell을 통해 소프트웨어를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-186">You can also install software through the secure shell.</span></span> <span data-ttu-id="52100-187">Azure 컴퓨터는 기본적으로 인터넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-187">Azure machines are by default, Internet-connected.</span></span> <span data-ttu-id="52100-188">표준 명령을 사용하여 표준 리포지토리에서 인기 소프트웨어 패키지를 직접 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-188">You can use standard commands to install popular software packages directly from standard repositories.</span></span> <span data-ttu-id="52100-189">이 방식을 사용하여 Apache를 설치해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-189">Let's use this approach to install Apache.</span></span>

### <a name="install-apache-web-server"></a><span data-ttu-id="52100-190">Apache 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="52100-190">Install Apache web server</span></span>

<span data-ttu-id="52100-191">Apache는 Ubuntu의 기본 소프트웨어 리포지토리 내에서 제공되므로 기존 패키지 관리 도구를 사용하여 설치하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-191">Apache is available within Ubuntu's default software repositories, so we will install it using conventional package management tools.</span></span>

1. <span data-ttu-id="52100-192">먼저 최신 업스트림 변경 내용을 반영하도록 로컬 패키지 인덱스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-192">Start by updating the local package index to reflect the latest upstream changes.</span></span>

    ```bash
    sudo apt-get update
    ```
    
1. <span data-ttu-id="52100-193">그런 다음 Apache를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-193">Next, install Apache.</span></span>

    ```bash
    sudo apt-get install apache2
    ```
    
1. <span data-ttu-id="52100-194">설치는 자동으로 시작됩니다. `systemctl`을 사용하면 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-194">It should start automatically - we can check the status using `systemctl`:</span></span>

    ```bash
    sudo systemctl status apache2
    ```

    <span data-ttu-id="52100-195">그러면 다음과 같은 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="52100-195">This should return something like:</span></span>

    ```output
    apache2.service - The Apache HTTP Server
       Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
      Drop-In: /lib/systemd/system/apache2.service.d
               └─apache2-systemd.conf
       Active: active (running) since Mon 2018-09-03 21:00:03 UTC; 1min 34s ago
     Main PID: 11156 (apache2)
        Tasks: 55 (limit: 4915)
       CGroup: /system.slice/apache2.service
               ├─11156 /usr/sbin/apache2 -k start
               ├─11158 /usr/sbin/apache2 -k start
               └─11159 /usr/sbin/apache2 -k start
    
    test-web-eus-vm1 systemd[1]: Starting The Apache HTTP Server...
    test-web-eus-vm1 apachectl[11129]: AH00558: apache2: Could not reliably determine the server's fully qua
    test-web-eus-vm1 systemd[1]: Started The Apache HTTP Server.
    ```

1. <span data-ttu-id="52100-196">마지막으로 공용 IP 주소를 통해 기본 페이지를 검색해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-196">Finally, we can try retrieving the default page through the public IP address.</span></span> <span data-ttu-id="52100-197">그러면 기본 페이지가 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52100-197">It should return a default page.</span></span>

    ![Apache 기본 웹 페이지](../media-drafts/6-apache-works.png)

<span data-ttu-id="52100-199">보시다시피 SSH를 사용하면 Linux VM을 로컬 컴퓨터처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-199">As you can see, SSH allows you to work with the Linux VM just like a local computer.</span></span> <span data-ttu-id="52100-200">이 VM을 다른 Linux 컴퓨터처럼 관리하면서 소프트웨어를 설치하고, 역할을 구성하고, 기능 및 기타 일상적인 작업을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-200">You can administer this VM as you would any other Linux computer: installing software, configuring roles, adjusting features and other everyday tasks.</span></span> <span data-ttu-id="52100-201">하지만 이러한 프로세스는 수동으로 수행해야 하므로 소프트웨어를 많이 설치해야 한다면 스크립트를 작성해 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52100-201">However, it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>
