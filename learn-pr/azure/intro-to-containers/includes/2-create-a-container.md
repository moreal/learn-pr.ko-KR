<span data-ttu-id="43fc2-101">컨테이너를 실행, 나열 및 삭제하는 일반적인 방법 중 일부를 설명하기 전에 Ubuntu VM(가상 머신)에 호스팅되는 Docker 컨테이너에서 실행 중인 기본 Nginx 구성을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-101">Before we cover some of the common ways to run, list, and delete containers, let's see a basic Nginx configuration running on a Docker container that's hosted on an Ubuntu virtual machine (VM).</span></span>

<span data-ttu-id="43fc2-102">여기에서는 다음 방법을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-102">In this part, you'll learn how to:</span></span>

1. <span data-ttu-id="43fc2-103">VM이 처음 부팅될 때 Docker를 설치하도록 구성된 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-103">Create a Linux VM that's configured to install Docker when the VM first boots.</span></span>
1. <span data-ttu-id="43fc2-104">VM에 연결하고 Nginx를 실행하는 Docker 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-104">Connect to your VM and start a Docker container running Nginx.</span></span>
1. <span data-ttu-id="43fc2-105">포트 바인딩을 사용하여 웹 서버가 VM 외부에서 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-105">Use port binding to make your web server accessible from outside the VM.</span></span>

## <a name="what-are-containers"></a><span data-ttu-id="43fc2-106">컨테이너란?</span><span class="sxs-lookup"><span data-stu-id="43fc2-106">What are containers?</span></span>

<span data-ttu-id="43fc2-107">컨테이너는 가상화 환경이지만, 가상 머신과는 달리 항상 전체 운영 체제를 포함하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-107">A container is a virtualization environment but, unlike a virtual machine, it does not always include a full operating system.</span></span> <span data-ttu-id="43fc2-108">대신, 해당 컨테이너를 실행하는 호스팅 환경의 운영 체제를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-108">Instead, it references the operating system of the host environment that runs that container.</span></span> <span data-ttu-id="43fc2-109">예를 들어 특정 Linux 커널이 있는 서버에서 컨테이너 5개를 실행하는 경우 컨테이너 5개가 모두 동일한 커널에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-109">For example, if you run five containers on a server with a specific Linux kernel, all five containers are running on that same kernel.</span></span>

<span data-ttu-id="43fc2-110">컨테이너를 사용하면 응용 프로그램 및 _컨테이너 이미지_로 알려진 것에서 실행하는 데 필요한 모든 것을 패키징할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-110">Containers enable you to package your application and everything that it needs to run into what's known as a _container image_.</span></span> <span data-ttu-id="43fc2-111">컨테이너는 격리되어 있습니다. 이는 동일한 시스템에서 실행 중인 다른 모든 컨테이너를 방해하지 않는다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-111">Containers are isolated, which means they don't interfere with any other container running on the same system.</span></span> <span data-ttu-id="43fc2-112">컨테이너 이미지는 이식 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-112">Container images are also portable.</span></span> <span data-ttu-id="43fc2-113">Docker Hub 또는 Azure Container Registry와 같은 컨테이너 레지스트리에 이미지를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-113">You can upload your images to a container registry, such as Docker Hub or Azure Container Registry.</span></span> <span data-ttu-id="43fc2-114">그런 다음, 클라우드에서 컨테이너를 실행하고 개발 환경에서와 마찬가지로 정확히 동일한 방식으로 컨테이너가 동작하기를 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-114">You can then run your containers in the cloud and expect them to behave the exact same way as they do in your development environment.</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

<span data-ttu-id="43fc2-115">컨테이너는 신속한 반복을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-115">Containers enable rapid iteration.</span></span> <span data-ttu-id="43fc2-116">컨테이너는 운영 체제를 포함할 필요가 없으므로 일반적으로 전체 VM보다 크기가 훨씬 작습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-116">Because containers don't need to include an operating system, they're typically much smaller than full VMs.</span></span> <span data-ttu-id="43fc2-117">이 컨테이너를 사용하면 몇 초 안에 신속하게 컨테이너를 시작 및 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-117">This enables you to start and stop containers quickly, often in seconds.</span></span>

## <a name="understand-the-setup"></a><span data-ttu-id="43fc2-118">설정 이해</span><span class="sxs-lookup"><span data-stu-id="43fc2-118">Understand the setup</span></span>

<span data-ttu-id="43fc2-119">학습 목적에서 작업할 샌드박스 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-119">For learning purposes, we provide a sandbox environment for you to work in.</span></span> <span data-ttu-id="43fc2-120">이 환경에는 Azure 리소스를 관리하고 개발하기 위한 브라우저 기반 명령줄 환경인 Azure Cloud Shell이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-120">This environment includes Azure Cloud Shell, a browser-based command-line experience for managing and developing Azure resources.</span></span>

<span data-ttu-id="43fc2-121">Cloud Shell에서 Docker를 포함하는 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-121">From Cloud Shell, you'll create a Linux VM that includes Docker.</span></span> <span data-ttu-id="43fc2-122">Docker 컨테이너를 대화형으로 만들고 사용할 수 있도록 SSH를 통해 Linux VM에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-122">You'll connect to your Linux VM over SSH so that you can interactively create and use Docker containers.</span></span>

<span data-ttu-id="43fc2-123">컨테이너에 대해 알아보려면 이 Linux VM을 개발 환경 및 공간으로 생각하세요.</span><span class="sxs-lookup"><span data-stu-id="43fc2-123">Think of this Linux VM as your development environment and a space to learn about containers.</span></span> <span data-ttu-id="43fc2-124">실제로 앱 개발에 사용되는 컴퓨터에 Docker를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-124">In practice, you would install Docker on the computer you use to develop your apps.</span></span> <span data-ttu-id="43fc2-125">Docker는 Windows, macOS 및 Linux에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-125">Docker runs on Windows, macOS, and Linux.</span></span>

<span data-ttu-id="43fc2-126">이 모듈의 끝에 로컬 개발 환경에서 Docker를 실행하는 방법을 자세히 알아볼 수 있는 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-126">We'll provide resources where you can learn more about running Docker in your local development environment at the end of this module.</span></span>

## <a name="what-is-nginx"></a><span data-ttu-id="43fc2-127">Nginx란?</span><span class="sxs-lookup"><span data-stu-id="43fc2-127">What is Nginx?</span></span>

<span data-ttu-id="43fc2-128">Nginx("엔진-엑스"로 발음)는 인기 있는 무료 오픈 소스 웹 서버로 Unix, Linux, macOS 및 Windows에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-128">Nginx (pronounced "engine-x") is a popular, free, open-source web server that runs on Unix, Linux, macOS, and Windows.</span></span> <span data-ttu-id="43fc2-129">웹 서버 구성은 동작 중인 컨테이너를 확인하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-129">Configuring a web server is a good way to see containers in action.</span></span> <span data-ttu-id="43fc2-130">여기서는 Nginx를 사용하여 기본 웹 페이지를 작동하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-130">Here you'll use Nginx to serve a basic web page.</span></span>

## <a name="what-is-cloud-init"></a><span data-ttu-id="43fc2-131">cloud-init란?</span><span class="sxs-lookup"><span data-stu-id="43fc2-131">What is cloud-init?</span></span>

<span data-ttu-id="43fc2-132">Cloud-init를 사용하면 처음 부팅 시 Linux VM을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-132">Cloud-init enables you to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="43fc2-133">Cloud-init를 사용하여 패키지를 설치하고 파일을 쓰거나, 사용자 및 보안을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-133">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="43fc2-134">여기에서는 cloud-init 스크립트를 사용하여 VM에 Docker를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-134">Here you'll use a cloud-init script to install Docker on your VM.</span></span>

## <a name="what-is-port-binding"></a><span data-ttu-id="43fc2-135">포트 바인딩이란?</span><span class="sxs-lookup"><span data-stu-id="43fc2-135">What is port binding?</span></span>

<span data-ttu-id="43fc2-136">포트 바인딩을 사용하면 해당 호스트에서 컨테이너로 네트워크 트래픽을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-136">Port binding enables you to forward network traffic to a container from its host.</span></span>

<span data-ttu-id="43fc2-137">Docker 컨테이너는 컨테이너의 호스트 시스템의 로컬 네트워크에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-137">A Docker container runs on a local network on the container's host system.</span></span> <span data-ttu-id="43fc2-138">이 경우 컨테이너의 네트워크는 Linux VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-138">In this case, the container's network will be on your Linux VM.</span></span>

<span data-ttu-id="43fc2-139">알다시피 웹 요청은 일반적으로 포트 80(HTTP)을 통해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-139">You know that web requests typically run over port 80 (HTTP).</span></span> <span data-ttu-id="43fc2-140">컨테이너는 VM 내의 로컬 네트워크에서 실행되므로 컨테이너는 외부 환경에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-140">Because the container is running on a local network inside your VM, the container is not accessible to the outside world.</span></span>

<span data-ttu-id="43fc2-141">Docker를 사용하면 VM 외부에서 액세스할 수 있게 하는 포트를 게시하거나 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-141">Docker enables you to publish, or expose, a port to make it accessible from outside the VM.</span></span> <span data-ttu-id="43fc2-142">여기에서는 VM의 포트 8080으로 전달되는 네트워크 트래픽을 컨테이너의 포트 80으로 전달할 수 있도록 컨테이너를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-142">Here, you'll configure your container so that network traffic to port 8080 on your VM will be forwarded to port 80 on your container.</span></span>

## <a name="create-a-virtual-machine-to-host-docker"></a><span data-ttu-id="43fc2-143">Docker를 호스트하기 위한 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="43fc2-143">Create a virtual machine to host Docker</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="create-the-cloud-init-script"></a><span data-ttu-id="43fc2-144">cloud-init 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="43fc2-144">Create the cloud-init script</span></span>

1. <span data-ttu-id="43fc2-145">**clouddrive** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-145">Navigate to the **clouddrive** folder.</span></span>

    ```azurecli
    cd clouddrive
    ```

1. <span data-ttu-id="43fc2-146">**vm-config**라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-146">Create a new folder named **vm-config**.</span></span>

    ```azurecli
    mkdir vm-config
    ```

1. <span data-ttu-id="43fc2-147">새 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-147">Navigate to the new folder.</span></span>

    ```azurecli
    cd vm-config
    ```

1. <span data-ttu-id="43fc2-148">Cloud Shell의 통합 편집기를 사용하여 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-148">Create a new file using Cloud Shell's integrated editor.</span></span>

    ```azurecli
    code .
    ```

1. <span data-ttu-id="43fc2-149">이 cloud-init 스크립트를 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-149">Paste this cloud-init script into the editor.</span></span>

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```yaml
    #cloud-config
    package_upgrade: true
    write_files:
      - path: /etc/systemd/system/docker.service.d/docker.conf
        content: |
          [Service]
          ExecStart=
          ExecStart=/usr/bin/dockerd
      - path: /etc/docker/daemon.json
        content: |
          {
            "hosts": ["fd://","tcp://127.0.0.1:2375"]
          }
    runcmd:
      - curl -sSL https://get.docker.com/ | sh
      - usermod -aG docker azureuser
    ```

1. <span data-ttu-id="43fc2-150">파일을 **docker-vm-config.txt**(<kbd>Ctrl+S</kbd> 또는 **저장**을 마우스 오른쪽 단추로 클릭하고 선택)로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-150">Save the file as **docker-vm-config.txt** (<kbd>Ctrl+S</kbd> or right click and select **Save**).</span></span>

1. <span data-ttu-id="43fc2-151">편집기를 닫습니다(<kbd>Ctrl+Q</kbd> 또는 **끝내기**를 마우스 오른쪽 단추로 클릭하고 선택).</span><span class="sxs-lookup"><span data-stu-id="43fc2-151">Close the editor (<kbd>Ctrl+Q</kbd> or right click and select **Quit**).</span></span>

### <a name="create-the-vm"></a><span data-ttu-id="43fc2-152">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="43fc2-152">Create the VM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43fc2-153">일반적으로 `az group create` 명령과 관련된 모든 Azure 리소스에 대한 리소스 그룹을 만들지만 이 실습에서는 하나의 리소스만 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-153">Normally, you would create a resource group for all your related Azure resources with the `az group create` command, but for these exercises one has been created for you.</span></span> <span data-ttu-id="43fc2-154">모든 단계의 리소스 그룹으로 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-154">Use "**<rgn>[sandbox resource group name]</rgn>**" as your resource group in all the steps.</span></span>

1. <span data-ttu-id="43fc2-155">`az vm create` 명령을 실행하여 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-155">Run this `az vm create` command to create your Linux VM.</span></span>

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --image UbuntuLTS \
      --admin-username azureuser \
      --generate-ssh-keys \
      --custom-data docker-vm-config.txt
    ```

<span data-ttu-id="43fc2-156">`--custom-data` 인수는 VM이 처음 부팅될 때 Docker를 설치하는 cloud-init 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-156">The `--custom-data` argument specifies the cloud-init script that installs Docker when the VM first boots.</span></span> <span data-ttu-id="43fc2-157">프로세스를 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-157">The process will take a few minutes to complete.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="43fc2-158">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="43fc2-158">Connect to the VM</span></span>

<span data-ttu-id="43fc2-159">여기에서는 연결을 구성할 수 있도록 VM에 대한 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-159">Here you'll create an SSH connection to your VM so that you can configure it.</span></span>

1. <span data-ttu-id="43fc2-160">이 `az vm show` 명령을 실행하여 VM의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-160">Run this `az vm show` command to get your VM's IP address.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

1. <span data-ttu-id="43fc2-161">VM에 SSH 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-161">SSH into the VM.</span></span> <span data-ttu-id="43fc2-162">**ip-address**를 사용자의 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-162">Replace **ip-address** with yours.</span></span>

    ```bash
    ssh azureuser@ip-address
    ```

1. <span data-ttu-id="43fc2-163">Docker 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-163">Verify the Docker version.</span></span>

    ```bash
    docker version
    ```

    > [!NOTE]
    > <span data-ttu-id="43fc2-164">명령이 실패하거나 Docker 디먼 소켓에 연결하는 방법에 대한 오류 메시지가 표시되는 경우는 cloud-init 스크립트 아직 완료되지 않았다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-164">If the command fails, or you see an error message about connecting to the Docker daemon socket, that means that the cloud-init script hasn't yet completed.</span></span> <span data-ttu-id="43fc2-165">스크립트 완료를 대기하는 몇몇 방법이 있기는 하지만 현재로서는 `exit`를 실행하여 SSH 세션을 종료하고 1~2분 뒤 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-165">Although there are ways to wait for the script to complete, for now run `exit` to leave your SSH session and try reconnecting in a minute or two.</span></span>

## <a name="start-nginx"></a><span data-ttu-id="43fc2-166">Nginx 시작</span><span class="sxs-lookup"><span data-stu-id="43fc2-166">Start Nginx</span></span>

<span data-ttu-id="43fc2-167">여기에서는 Nginx를 실행하는 Docker 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-167">Here you'll start a Docker container that's running Nginx.</span></span>

1. <span data-ttu-id="43fc2-168">이 `docker run` 명령을 실행하여 Nginx를 실행하는 Docker 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-168">Run this `docker run` command to start a Docker container running Nginx.</span></span>

    ```bash
    docker run -d -p 8080:80 --name nginx nginx
    ```

    <span data-ttu-id="43fc2-169">이 명령은 [Docker 허브](https://hub.docker.com/_/nginx?azure-portal=true)에서 Nginx로 미리 구성된 Docker 이미지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-169">The command downloads a Docker image that's preconfigured with Nginx from [Docker Hub](https://hub.docker.com/_/nginx?azure-portal=true).</span></span>

    <span data-ttu-id="43fc2-170">`--name` 인수는 나중에 작업할 수 있도록 Docker 컨테이너에 "nginx"라는 이름을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-170">The `--name` argument assigns the name "nginx" to your Docker container so you can work with it later.</span></span>

    <span data-ttu-id="43fc2-171">`-p` 인수는 VM의 포트 8080으로 전달되는 네트워크 트래픽을 컨테이너의 포트 80으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-171">The `-p` argument forwards network traffic to port 8080 on your VM to port 80 on your container.</span></span>

1. <span data-ttu-id="43fc2-172">`curl`을 실행하여 Nginx가 실행 중이며 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-172">Run `curl` to verify that Nginx is running and accessible.</span></span>

    ```bash
    curl http://localhost:8080
    ```

1. <span data-ttu-id="43fc2-173">SSH 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-173">Exit your SSH session.</span></span>

    ```bash
    exit
    ```

## <a name="access-your-web-server-from-a-web-browser"></a><span data-ttu-id="43fc2-174">웹 브라우저에서 웹 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="43fc2-174">Access your web server from a web browser</span></span>

<span data-ttu-id="43fc2-175">앞서 언급한 것처럼 포트 8080으로 전달되는 네트워크 트래픽이 컨테이너의 포트 80으로 전달될 수 있도록 컨테이너를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-175">Recall that you configured your container so that network traffic on port 8080 is forwarded to port 80 on your container.</span></span>

<span data-ttu-id="43fc2-176">동작 중인 포트 매핑을 확인하려면 여기서는 Azure 방화벽을 통해 VM의 포트 8080을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-176">To see port mapping in action, here you'll open port 8080 to your VM through the Azure firewall.</span></span> <span data-ttu-id="43fc2-177">그러면 브라우저에서 웹 서버에 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-177">Then you'll access your web server from a browser.</span></span>

1. <span data-ttu-id="43fc2-178">이 `az vm open-port` 명령을 실행하여 방화벽을 통해 VM에서 포트 8080을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-178">Run this `az vm open-port` command to open port 8080 on your VM through the firewall.</span></span>

    ```azurecli
    az vm open-port \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --port 8080 \
      --priority 1001
    ```

1. <span data-ttu-id="43fc2-179">웹 브라우저에서 VM의 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-179">From a web browser, navigate to your VM's IP address.</span></span> <span data-ttu-id="43fc2-180">포트 8080, 예를 들어 **http://40.121.106.164:8080**을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-180">Be sure to include port 8080, for example,  **http://40.121.106.164:8080**.</span></span>

    <span data-ttu-id="43fc2-181">기본 홈 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-181">You see the default home page.</span></span>

    ![브라우저에서 실행 중인 웹 사이트](../media/2-nginx-browser.png)

## <a name="stop-the-container"></a><span data-ttu-id="43fc2-183">컨테이너 중지</span><span class="sxs-lookup"><span data-stu-id="43fc2-183">Stop the container</span></span>

<span data-ttu-id="43fc2-184">이제 컨테이너를 중지하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-184">Now let's stop the container.</span></span>

1. <span data-ttu-id="43fc2-185">먼저 VM에 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-185">First, log back in to your VM.</span></span> <span data-ttu-id="43fc2-186">배운 내용을 떠올려 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-186">Here's a refresher.</span></span>

    <span data-ttu-id="43fc2-187">IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-187">Get the IP address.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

    <span data-ttu-id="43fc2-188">VM에 SSH 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-188">SSH into the VM.</span></span> <span data-ttu-id="43fc2-189">**ip-address**를 사용자의 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-189">Replace **ip-address** with yours.</span></span>

    ```bash
    ssh azureuser@ip-address
    ```

1. <span data-ttu-id="43fc2-190">`docker stop nginx`을 실행하여 "nginx"라는 컨테이너를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-190">Run `docker stop nginx` to stop the container named "nginx".</span></span>

    ```bash
    docker stop nginx
    ```

<span data-ttu-id="43fc2-191">다음을 위해 SSH 연결을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-191">Keep your SSH connection open for the next part.</span></span>

<span data-ttu-id="43fc2-192">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="43fc2-192">Congratulations!</span></span> <span data-ttu-id="43fc2-193">성공적으로 가상 머신을 만들어 Nginx 컨테이너화된 웹 서버를 호스팅하는 데 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="43fc2-193">You've successfully created a virtual machine and used it to host an Nginx containerized web server.</span></span>
