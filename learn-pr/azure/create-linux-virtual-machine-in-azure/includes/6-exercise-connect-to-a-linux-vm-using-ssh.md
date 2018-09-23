<span data-ttu-id="74dd8-101">Linux VM을 배포하여 실행하고 있지만 작업을 수행하도록 구성되어 있지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-101">We have our Linux VM deployed and running, but it's not configured to do any work.</span></span> <span data-ttu-id="74dd8-102">VM을 SSH에 연결하고 Apache를 구성해 보겠습니다. 그러면 실행되는 웹 서버가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-102">Let's connect to it with SSH and configure Apache, so we have a running web server.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="74dd8-103">SSH로 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="74dd8-103">Connect to the VM with SSH</span></span>

<span data-ttu-id="74dd8-104">Azure VM을 SSH 클라이언트와 연결하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-104">To connect to an Azure VM with an SSH client, you will need:</span></span>

- <span data-ttu-id="74dd8-105">SSH 클라이언트 소프트웨어(대부분의 최신 운영 체제에 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="74dd8-105">SSH client software (present on most modern operating systems)</span></span>
- <span data-ttu-id="74dd8-106">VM의 공용 IP 주소(VM이 사용자 네트워크에 연결하도록 구성된 경우에는 개인 IP 주소)</span><span class="sxs-lookup"><span data-stu-id="74dd8-106">The public IP address of the VM (or private if the VM is configured to connect to your network)</span></span>

### <a name="get-the-public-ip-address"></a><span data-ttu-id="74dd8-107">공용 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="74dd8-107">Get the public IP address</span></span>

1. <span data-ttu-id="74dd8-108">[Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에서 이전에 만든 가상 머신의 **개요** 패널이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-108">In the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="74dd8-109">해당 패널을 열어야 하는 경우 **모든 리소스** 아래에서 VM을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-109">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="74dd8-110">요약 패널에는 VM과 관련된 많은 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-110">The overview panel has a lot of information about the VM.</span></span>

    - <span data-ttu-id="74dd8-111">VM을 실행 중인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-111">You can see whether the VM is running</span></span>
    - <span data-ttu-id="74dd8-112">중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="74dd8-112">Stop or restart it</span></span>
    - <span data-ttu-id="74dd8-113">VM에 연결하기 위한 공용 IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="74dd8-113">Get the public IP address to connect to the VM</span></span>
    - <span data-ttu-id="74dd8-114">CPU, 디스크 및 네트워크의 활동 확인</span><span class="sxs-lookup"><span data-stu-id="74dd8-114">See the activity of the CPU, disk, and network</span></span>

1. <span data-ttu-id="74dd8-115">창 위쪽에서 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-115">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="74dd8-116">**가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-116">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings.</span></span> <span data-ttu-id="74dd8-117">**SSH** 탭에는 VM에 연결하기 위해 로컬로 실행해야 하는 명령도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-117">On the **SSH** tab, you will also find the command you need to execute locally to connect to the VM.</span></span> <span data-ttu-id="74dd8-118">이것을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-118">Copy this to the clipboard.</span></span>

## <a name="connect-with-ssh"></a><span data-ttu-id="74dd8-119">SSH를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="74dd8-119">Connect with SSH</span></span>

1. <span data-ttu-id="74dd8-120">SSH 탭에서 가져온 명령줄을 Azure Cloud Shell에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-120">Paste the command line you got from the SSH tab into Azure Cloud Shell.</span></span> <span data-ttu-id="74dd8-121">해당 명령줄은 다음과 같습니다. 하지만 실제 IP 주소는 다르며, **jim**을 사용하지 않았다면 사용자 이름도 다를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-121">It should look something like this; however, it will have a different IP address (and perhaps a different username if you didn't use **jim**!):</span></span>

    ```bash
    ssh jim@137.117.101.249
    ```

1. <span data-ttu-id="74dd8-122">이 명령은 Secure Shell 연결을 열고 일반적인 Linux용 셸 명령 프롬프트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-122">This command will open a Secure Shell connection and place you at a traditional shell command prompt for Linux.</span></span>

1. <span data-ttu-id="74dd8-123">몇 가지 Linux 명령을 실행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="74dd8-123">Try executing a few Linux commands</span></span>
    - <span data-ttu-id="74dd8-124">`ls -la /`: 디스크 루트 표시</span><span class="sxs-lookup"><span data-stu-id="74dd8-124">`ls -la /` to show the root of the disk</span></span>
    - <span data-ttu-id="74dd8-125">`ps -l`: 실행 중인 모든 프로세스 표시</span><span class="sxs-lookup"><span data-stu-id="74dd8-125">`ps -l` to show all the running processes</span></span>
    - <span data-ttu-id="74dd8-126">`dmesg`: 모든 커널 메시지 나열</span><span class="sxs-lookup"><span data-stu-id="74dd8-126">`dmesg` to list all the kernel messages</span></span>
    - <span data-ttu-id="74dd8-127">`lsblk`: 모든 블록 장치 나열(여기에 드라이브가 표시됨)</span><span class="sxs-lookup"><span data-stu-id="74dd8-127">`lsblk` to list all the block devices - here you will see your drives</span></span>

<span data-ttu-id="74dd8-128">드라이브 목록에서 더 자세히 살펴보아야 할 사항은 _누락_ 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-128">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="74dd8-129">**데이터** 드라이브(`sdc`)가 있는데 파일 시스템에 탑재되어 있지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-129">Notice that our **Data** drive (`sdc`) is present but not mounted into the file system.</span></span> <span data-ttu-id="74dd8-130">Azure에서 VHD를 추가했지만 초기화하지는 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-130">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="74dd8-131">데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="74dd8-131">Initialize data disks</span></span>

<span data-ttu-id="74dd8-132">처음부터 작성하는 모든 추가 드라이브는 초기화하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-132">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="74dd8-133">이 과정을 수행하는 프로세스는 실제 디스크용 프로세스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-133">The process for doing this is identical to a physical disk:</span></span>

1. <span data-ttu-id="74dd8-134">먼저 디스크를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-134">First, identify the disk.</span></span> <span data-ttu-id="74dd8-135">이 작업은 앞에서 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-135">We did that above.</span></span> <span data-ttu-id="74dd8-136">SCSI 장치용 커널의 모든 메시지를 나열하는 `dmesg | grep SCSI`를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-136">You could also use `dmesg | grep SCSI`, which will list all the messages from the kernel for SCSI devices.</span></span>

1. <span data-ttu-id="74dd8-137">드라이브(`sdc`)가 확인되면 초기화를 수행해야 합니다. `fdisk`를 사용하면 초기화를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-137">Once you know the drive (`sdc`) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="74dd8-138">`sudo`를 포함해 명령을 실행하고 파티션을 지정할 디스크를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-138">You will need to run the command with `sudo` and supply the disk you want to partition.</span></span> <span data-ttu-id="74dd8-139">다음 명령을 사용하여 새로운 주 파티션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-139">We can use the following command to create a new primary partition:</span></span>

    ```bash
    (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
    ```

1. <span data-ttu-id="74dd8-140">이제 `mkfs` 명령을 사용하여 파티션에 파일 시스템을 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-140">Next, we need to write a file system to the partition with the `mkfs` command.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```

1. <span data-ttu-id="74dd8-141">마지막으로, 파일 시스템에 드라이브를 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-141">Finally, we need to mount the drive to the file system.</span></span> <span data-ttu-id="74dd8-142">여기서는 `data` 폴더가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-142">Let's assume we will have a `data` folder.</span></span> <span data-ttu-id="74dd8-143">탑재 지점 폴더를 만들고 드라이브를 탑재하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-143">Let's create the mount point folder and mount the drive.</span></span>

    ```bash
    sudo mkdir /data & sudo mount /dev/sdc1 /data
    ```

    > [!TIP]
    > <span data-ttu-id="74dd8-144">디스크를 초기화하고 탑재했습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-144">We initialized the disk and mounted it.</span></span> <span data-ttu-id="74dd8-145">이 프로세스에 대해 좀 더 자세히 알아보려면 **Azure 가상 머신에서 디스크 추가 및 크기 지정** 모듈을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74dd8-145">If you are interested in more details on this process go through the **Add and size disks in Azure virtual machines** module.</span></span> <span data-ttu-id="74dd8-146">이 작업에 대해 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-146">This task is covered in more detail there.</span></span>

## <a name="install-software-onto-the-vm"></a><span data-ttu-id="74dd8-147">VM에 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="74dd8-147">Install software onto the VM</span></span>

<span data-ttu-id="74dd8-148">보시다시피 SSH를 사용하면 Linux VM을 로컬 컴퓨터처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-148">As you can see, SSH allows you to work with the Linux VM just like a local computer.</span></span> <span data-ttu-id="74dd8-149">이 VM을 다른 Linux 컴퓨터처럼 관리하면서 소프트웨어를 설치하고, 역할을 구성하고, 기능 및 기타 일상적인 작업을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-149">You can administer this VM as you would any other Linux computer: installing software, configuring roles, adjusting features, and other everyday tasks.</span></span> <span data-ttu-id="74dd8-150">잠시 소프트웨어 설치에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-150">Let's focus on installing software for a moment.</span></span>

<span data-ttu-id="74dd8-151">VM에 소프트웨어를 설치하는 옵션은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-151">You have several options to install software onto the VM.</span></span> <span data-ttu-id="74dd8-152">먼저, 앞에서 설명한 것처럼 `scp`를 사용하여 머신의 로컬 파일을 VM에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-152">First, as mentioned, you can use `scp` to copy local files from your machine to the VM.</span></span> <span data-ttu-id="74dd8-153">이렇게 하면 데이터 또는 실행하려는 사용자 지정 응용 프로그램을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-153">This lets you copy over data or custom applications you want to run.</span></span>

<span data-ttu-id="74dd8-154">Secure Shell을 통해 소프트웨어를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-154">You can also install software through Secure Shell.</span></span> <span data-ttu-id="74dd8-155">Azure 머신은 기본적으로 인터넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-155">Azure machines are, by default, internet connected.</span></span> <span data-ttu-id="74dd8-156">표준 명령을 사용하여 표준 리포지토리에서 인기 소프트웨어 패키지를 직접 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-156">You can use standard commands to install popular software packages directly from standard repositories.</span></span> <span data-ttu-id="74dd8-157">이 방식을 사용하여 Apache를 설치해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-157">Let's use this approach to install Apache.</span></span>

### <a name="install-the-apache-web-server"></a><span data-ttu-id="74dd8-158">Apache 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="74dd8-158">Install the Apache web server</span></span>

<span data-ttu-id="74dd8-159">Apache는 Ubuntu의 기본 소프트웨어 리포지토리 내에서 제공되므로 기존 패키지 관리 도구를 사용하여 설치하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-159">Apache is available within Ubuntu's default software repositories, so we will install it using conventional package management tools:</span></span>

1. <span data-ttu-id="74dd8-160">먼저 최신 업스트림 변경 내용을 반영하도록 로컬 패키지 인덱스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-160">Start by updating the local package index to reflect the latest upstream changes:</span></span>

    ```bash
    sudo apt-get update
    ```
    
1. <span data-ttu-id="74dd8-161">그런 다음, Apache를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-161">Next, install Apache:</span></span>

    ```bash
    sudo apt-get install apache2 -y
    ```

1. <span data-ttu-id="74dd8-162">설치는 자동으로 시작됩니다. `systemctl`을 사용하면 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-162">It should start automatically - we can check the status using `systemctl`:</span></span>

    ```bash
    sudo systemctl status apache2 --no-pager
    ```

    <span data-ttu-id="74dd8-163">그러면 다음과 같은 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-163">This should return something like:</span></span>

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
    > [!NOTE]
    > <span data-ttu-id="74dd8-164">이와 같은 명령을 실행하는 것은 간단한 일이지만 이러한 프로세스는 수동으로 수행해야 하므로 많은 소프트웨어를 항상 설치해야 한다면 스크립트를 작성해 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-164">It's trivial to execute commands like this, however it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>
    
1. <span data-ttu-id="74dd8-165">마지막으로 공용 IP 주소를 통해 기본 페이지를 검색해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-165">Finally, we can try retrieving the default page through the public IP address.</span></span> <span data-ttu-id="74dd8-166">그러나 VM에서 웹 서버를 실행하는 경우에도 유효한 연결 또는 응답을 얻을 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-166">However, even though the web server is running on the VM, you won't get a valid connection or response.</span></span> <span data-ttu-id="74dd8-167">이유를 알고 계세요?</span><span class="sxs-lookup"><span data-stu-id="74dd8-167">Do you know why?</span></span>

<span data-ttu-id="74dd8-168">웹 서버와 상호 작용할 수 있도록 하려면 한 단계를 더 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-168">We need to perform one more step to be able to interact with the web server.</span></span> <span data-ttu-id="74dd8-169">가상 네트워크는 인바운드 요청을 차단하고 있으며, 이는 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-169">Our virtual network is blocking the inbound request - this is the default behavior.</span></span> <span data-ttu-id="74dd8-170">이는 구성을 통해 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-170">We can change that through configuration.</span></span> <span data-ttu-id="74dd8-171">이에 대해서는 다음에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="74dd8-171">Let's look at that next.</span></span>