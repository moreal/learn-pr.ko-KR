<span data-ttu-id="f7ff4-101">이제 VM이 실행 중이므로 VM을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-101">Now that your VM is up and running, let's do something with it.</span></span> <span data-ttu-id="f7ff4-102">여기서는 웹 서버를 설치하고 VM의 호스트 이름을 표시하는 기본 웹 페이지를 운영하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-102">Here you'll install a web server and serve up a basic web page that displays the VM's hostname.</span></span>

<span data-ttu-id="f7ff4-103">VM을 구성하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-103">To configure a VM, you have several choices.</span></span> <span data-ttu-id="f7ff4-104">직접 연결하고 대화형으로 시스템을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-104">You can connect directly and interactively configure your system.</span></span> <span data-ttu-id="f7ff4-105">예를 들어 Windows 시스템에서 원격 데스크톱 세션을 만들어서 마치 Windows 머신에 앉아 있는 것처럼 원격 Windows 머신의 UI에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-105">For example, on Windows systems you can create a Remote Desktop session to connect to the UI of your remote Windows computer as if you were seated at it.</span></span> <span data-ttu-id="f7ff4-106">Linux 시스템에서, SSH 연결을 만들어서 터미널에서 원격 Linux 시스템을 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-106">On Linux systems, you can create an SSH connection to securely work with your remote Linux system from the terminal.</span></span>

<span data-ttu-id="f7ff4-107">수동 구성은 처음에는 좋지만, 이후에 시스템을 추가하면서 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-107">Manual configuration is a good start, but as you add systems, you can automate your deployments.</span></span> <span data-ttu-id="f7ff4-108">힘든 작업을 알아서 처리하는 프로그램 및 스크립트처럼 반복 가능한 프로세스의 실행도 자동화의 범위에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-108">Automation involves running repeatable processes such as programs and scripts that take care of the heavy lifting for you.</span></span>

<span data-ttu-id="f7ff4-109">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="f7ff4-109">::: zone pivot="windows-cloud"</span></span>

<span data-ttu-id="f7ff4-110">여기서는 사용자 지정 스크립트 확장이라고 하는 Windows 기반 Azure 가상 머신의 기능을 사용하여 Cloud Shell 세션에서 원격으로 IIS를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-110">Here, you'll configure IIS remotely from your Cloud Shell session using a feature of Windows-based Azure virtual machines called the Custom Script Extension.</span></span>

<span data-ttu-id="f7ff4-111">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="f7ff4-111">::: zone-end</span></span>

<span data-ttu-id="f7ff4-112">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="f7ff4-112">::: zone pivot="linux-cloud"</span></span>

<span data-ttu-id="f7ff4-113">여기서는 사용자 지정 스크립트 확장이라고 하는 Linux 기반 Azure 가상 머신의 기능을 사용하여 Cloud Shell 세션에서 원격으로 Nginx를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-113">Here, you'll configure Nginx remotely from your Cloud Shell session using a feature of Linux-based Azure virtual machines called the Custom Script Extension.</span></span>

<span data-ttu-id="f7ff4-114">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="f7ff4-114">::: zone-end</span></span>

<span data-ttu-id="f7ff4-115">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="f7ff4-115">::: zone pivot="windows-cloud"</span></span>

## <a name="what-is-iis"></a><span data-ttu-id="f7ff4-116">IIS란?</span><span class="sxs-lookup"><span data-stu-id="f7ff4-116">What is IIS?</span></span>

<span data-ttu-id="f7ff4-117">IIS(인터넷 정보 서비스)는 Windows에서 실행되는 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-117">Internet Information Services, or IIS, is a web server that runs on Windows.</span></span> <span data-ttu-id="f7ff4-118">IIS를 사용하여 표준 웹 콘텐츠(HTML, CSS 및 JavaScript)를 제공하거나 ASP.NET 및 다른 종류의 웹 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-118">You can use IIS to serve standard web content (HTML, CSS, and JavaScript) or run ASP.NET and other kinds of web applications.</span></span> <span data-ttu-id="f7ff4-119">IIS는 Windows Server가 함께 제공되지만 웹 페이지 서비스를 시작하려면 먼저 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-119">IIS comes with Windows Server, but you need to activate it to start serving web pages.</span></span>

## <a name="whats-the-custom-script-extension"></a><span data-ttu-id="f7ff4-120">사용자 지정 스크립트 확장이란?</span><span class="sxs-lookup"><span data-stu-id="f7ff4-120">What's the Custom Script Extension?</span></span>

<span data-ttu-id="f7ff4-121">사용자 지정 스크립트 확장은 Azure VM에서 간편하게 스크립트를 다운로드하고 실행할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-121">The Custom Script Extension is an easy way to download and run scripts on your Azure VMs.</span></span> <span data-ttu-id="f7ff4-122">VM이 실행 중이면 시스템을 구성할 수 있는 여러 방법 중 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-122">It's just one of the many ways you can configure the system once your VM is up and running.</span></span>

<span data-ttu-id="f7ff4-123">Azure 저장소 또는 GitHub와 같은 공용 위치에 스크립트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-123">You can store your scripts in Azure storage or in a public location such as GitHub.</span></span> <span data-ttu-id="f7ff4-124">스크립트를 수동으로 실행할 수도 있고 자동화된 배포의 일부로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-124">You can run scripts manually or as part of a more automated deployment.</span></span> <span data-ttu-id="f7ff4-125">여기서는 GitHub에서 PowerShell 스크립트를 다운로드하여 VM에서 실행하는 Azure CLI 명령을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-125">Here, you'll run an Azure CLI command to download a PowerShell script from GitHub and execute it on your VM.</span></span> <span data-ttu-id="f7ff4-126">이 스크립트는 IIS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-126">The script configures IIS.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="f7ff4-127">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="f7ff4-127">Configure IIS</span></span>

<!-- TODO: https://github.com/MicrosoftDocs/learn-pr/issues/1864 -->

<span data-ttu-id="f7ff4-128">여기서는 사용자 지정 스크립트 확장을 사용하여 Cloud Shell을 통해 원격으로 VM에서 IIS를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-128">Here you'll use the Custom Script Extension to configure IIS remotely on your VM from Cloud Shell.</span></span> <span data-ttu-id="f7ff4-129">또한 포트 80(HTTP)에 대한 인바운드 네트워크 액세스를 허용하도록 방화벽을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-129">You'll also configure the firewall to allow inbound network access on port 80 (HTTP).</span></span>

1. <span data-ttu-id="f7ff4-130">Cloud Shell에서 이 `az vm extension set` 명령을 실행하여 IIS를 설치하고 기본 홈페이지를 구성하는 PowerShell 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-130">From Cloud Shell, run this `az vm extension set` command to download and execute a PowerShell script that installs IIS and configures a basic home page.</span></span>

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myVM \
      --name CustomScriptExtension \
      --publisher Microsoft.Compute \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1"]}' \
      --protected-settings '{"commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"}'
    ```

    <span data-ttu-id="f7ff4-131">Nginx를 구성하고, 홈페이지의 내용을 설정하고, 서비스를 시작하는 프로세스를 완료하려면 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-131">The process to configure Nginx, set the contents of the homepage, and start the service takes a couple minutes to complete.</span></span>

    <span data-ttu-id="f7ff4-132">그 사이에 원한다면 별도의 브라우저 탭에서 [PowerShell 스크립트를 검사](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1?azure-portal=true)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-132">In the meantime, you can [examine the PowerShell script](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1?azure-portal=true) from a separate browser tab if you'd like.</span></span> <span data-ttu-id="f7ff4-133">이 스크립트는 IIS를 설치하고, VM의 컴퓨터 이름인 "myVM"과 함께 시작 메시지를 표시하도록 홈페이지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-133">The script installs IIS and configures the home page to display a welcome message along with the VM's computer name, "myVM".</span></span>

1. <span data-ttu-id="f7ff4-134">이 `az vm open-port` 명령을 실행하여 방화벽을 통해 포트 80(HTTP)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-134">Run this `az vm open-port` command to open port 80 (HTTP) through the firewall.</span></span>

    ```azurecli
    az vm open-port \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a><span data-ttu-id="f7ff4-135">구성 확인</span><span class="sxs-lookup"><span data-stu-id="f7ff4-135">Verify the configuration</span></span>

<span data-ttu-id="f7ff4-136">IIS를 설정했으니, 실행 중인지 확인하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-136">Now that IIS is set up, let's verify that it's running.</span></span>

1. <span data-ttu-id="f7ff4-137">VM의 공용 IP 주소를 나열하는 이 `az vm list-ip-addresses` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-137">Run this `az vm list-ip-addresses` command to list your VM's public IP addresses.</span></span>

    ```azurecli
    az vm list-ip-addresses \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > <span data-ttu-id="f7ff4-138">이 `--query` 인수를 사용하면 이 명령이 조금 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-138">This `--query` argument makes this command a bit complex.</span></span> <span data-ttu-id="f7ff4-139">하지만 여러분은 Azure를 열심히 공부하고 있으니 이 명령의 전문가가 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-139">But you'll be a pro at this as you dig in and explore Azure.</span></span>

    <span data-ttu-id="f7ff4-140">VM의 공용 IP 주소가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-140">You see your VM's public IP address.</span></span> <span data-ttu-id="f7ff4-141">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-141">Here's an example.</span></span>

    ```output
    104.211.9.245
    ```

1. <span data-ttu-id="f7ff4-142">새 브라우저 탭에서 VM의 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-142">In a new browser tab, navigate to your VM's IP address.</span></span> <span data-ttu-id="f7ff4-143">시작 메시지와 VM 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-143">You see your welcome message and your VM's name.</span></span>

    ![](../media/4-iis-browser.png)

<span data-ttu-id="f7ff4-144">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="f7ff4-144">::: zone-end</span></span>

<span data-ttu-id="f7ff4-145">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="f7ff4-145">::: zone pivot="linux-cloud"</span></span>

## <a name="what-is-nginx"></a><span data-ttu-id="f7ff4-146">Nginx란?</span><span class="sxs-lookup"><span data-stu-id="f7ff4-146">What is Nginx?</span></span>

<span data-ttu-id="f7ff4-147">Nginx(발음은 "엔진-엑스")는 인기 있는 무료 오픈 소스 웹 서버로 Unix, Linux, macOS 및 Windows에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-147">Nginx (pronounced "engine-x") is a popular, free, open-source web server that runs on Unix, Linux, macOS, and Windows.</span></span> <span data-ttu-id="f7ff4-148">여기서는 Nginx를 사용하여 기본 웹 페이지를 작동하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-148">Here you'll use Nginx to serve a basic web page.</span></span>

## <a name="whats-the-custom-script-extension"></a><span data-ttu-id="f7ff4-149">사용자 지정 스크립트 확장이란?</span><span class="sxs-lookup"><span data-stu-id="f7ff4-149">What's the Custom Script Extension?</span></span>

<span data-ttu-id="f7ff4-150">사용자 지정 스크립트 확장은 Azure VM에서 간편하게 스크립트를 다운로드하고 실행할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-150">The Custom Script Extension is an easy way to download and run scripts on your Azure VMs.</span></span> <span data-ttu-id="f7ff4-151">VM이 실행 중이면 시스템을 구성할 수 있는 여러 방법 중 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-151">It's just one of the many ways you can configure the system once your VM is up and running.</span></span>

<span data-ttu-id="f7ff4-152">Azure 저장소 또는 GitHub와 같은 공용 위치에 스크립트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-152">You can store your scripts in Azure storage or in a public location such as GitHub.</span></span> <span data-ttu-id="f7ff4-153">스크립트를 수동으로 실행할 수도 있고 자동화된 배포의 일부로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-153">You can run scripts manually or as part of a more automated deployment.</span></span> <span data-ttu-id="f7ff4-154">여기서는 GitHub에서 Bash 스크립트를 다운로드하여 VM에서 실행하는 Azure CLI 명령을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-154">Here, you'll run an Azure CLI command to download a Bash script from GitHub and execute it on your VM.</span></span> <span data-ttu-id="f7ff4-155">이 스크립트는 Nginx를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-155">The script configures Nginx.</span></span>

## <a name="configure-nginx"></a><span data-ttu-id="f7ff4-156">Nginx 구성</span><span class="sxs-lookup"><span data-stu-id="f7ff4-156">Configure Nginx</span></span>

<!-- TODO: https://github.com/MicrosoftDocs/learn-pr/issues/1864 -->

<span data-ttu-id="f7ff4-157">여기서는 사용자 지정 스크립트 확장을 사용하여 Cloud Shell을 통해 원격으로 VM에서 Nginx를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-157">Here you'll use the Custom Script Extension to configure Nginx remotely on your VM from Cloud Shell.</span></span> <span data-ttu-id="f7ff4-158">또한 포트 80(HTTP)에 대한 인바운드 네트워크 액세스를 허용하도록 방화벽을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-158">You'll also configure the firewall to allow inbound network access on port 80 (HTTP).</span></span>

1. <span data-ttu-id="f7ff4-159">Cloud Shell에서 이 `az vm extension set` 명령을 실행하여 Nginx를 설치하고 기본 홈페이지를 구성하는 Bash 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-159">From Cloud Shell, run this `az vm extension set` command to download and execute a Bash script that installs Nginx and configures a basic home page.</span></span>

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myVM \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-nginx.sh"]}' \
      --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
    ```

    <span data-ttu-id="f7ff4-160">IIS를 구성하고, 홈페이지의 내용을 설정하고, 서비스를 시작하는 프로세스를 완료하려면 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-160">The process to configure IIS, set the contents of the homepage, and start the service takes a couple minutes to complete.</span></span>

    <span data-ttu-id="f7ff4-161">그 사이에 원한다면 별도의 브라우저 탭에서 [Bash 스크립트를 검사](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-nginx.sh?azure-portal=true)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-161">In the meantime, you can [examine the Bash script](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-nginx.sh?azure-portal=true) from a separate browser tab if you'd like.</span></span> <span data-ttu-id="f7ff4-162">이 스크립트는 Nginx를 설치하고, VM의 컴퓨터 이름인 "myVM"과 함께 시작 메시지를 표시하도록 홈페이지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-162">The script installs Nginx and configures the home page to display a welcome message along with the VM's computer name, "myVM".</span></span>

1. <span data-ttu-id="f7ff4-163">이 `az vm open-port` 명령을 실행하여 방화벽을 통해 포트 80(HTTP)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-163">Run this `az vm open-port` command to open port 80 (HTTP) through the firewall.</span></span>

    ```azurecli
    az vm open-port \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a><span data-ttu-id="f7ff4-164">구성 확인</span><span class="sxs-lookup"><span data-stu-id="f7ff4-164">Verify the configuration</span></span>

<span data-ttu-id="f7ff4-165">Nginx를 설정했으니, 실행 중인지 확인하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-165">Now that Nginx is set up, let's verify that it's running.</span></span>

1. <span data-ttu-id="f7ff4-166">VM의 공용 IP 주소를 나열하는 이 `az vm list-ip-addresses` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-166">Run this `az vm list-ip-addresses` command to list your VM's public IP addresses.</span></span>

    ```azurecli
    az vm list-ip-addresses \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > <span data-ttu-id="f7ff4-167">이 `--query` 인수를 사용하면 이 명령이 조금 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-167">This `--query` argument makes this command a bit complex.</span></span> <span data-ttu-id="f7ff4-168">하지만 여러분은 Azure를 열심히 공부하고 있으니 이 명령의 전문가가 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-168">But you'll be a pro at this as you dig in and explore Azure.</span></span>

    <span data-ttu-id="f7ff4-169">VM의 공용 IP 주소가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-169">You see your VM's public IP address.</span></span> <span data-ttu-id="f7ff4-170">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-170">Here's an example.</span></span>

    ```output
    137.135.110.210
    ```

1. <span data-ttu-id="f7ff4-171">새 브라우저 탭에서 VM의 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-171">In a new browser tab, navigate to your VM's IP address.</span></span> <span data-ttu-id="f7ff4-172">시작 메시지와 VM 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-172">You see your welcome message and your VM's name.</span></span>

    ![](../media/4-nginx-browser.png)

<span data-ttu-id="f7ff4-173">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="f7ff4-173">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="f7ff4-174">요약</span><span class="sxs-lookup"><span data-stu-id="f7ff4-174">Summary</span></span>

<span data-ttu-id="f7ff4-175">이제 VM이 실행 중이고 웹 페이지를 제공할 수 있는데, 이것이 여러분에게는 어떤 의미일까요?</span><span class="sxs-lookup"><span data-stu-id="f7ff4-175">Your VM is running and can now serve up web pages, but what does that mean for you?</span></span>

<span data-ttu-id="f7ff4-176">모든 변화는 기본에서 시작하며, 클라우드에서 이루어진 크고 작은 기업의 위대한 혁신은 거의 대부분 여러분과 비슷한 설정에서 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-176">Remember, every journey starts with the basics, and almost any great innovation born in the cloud, from companies big and small, started with a similar setup to yours.</span></span> <span data-ttu-id="f7ff4-177">여러분의 아이디어가 발전할수록 비즈니스와 사용자에게 긍정적인 영향을 미치기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f7ff4-177">As your idea evolves, it begins making a positive impact on your business and your users.</span></span>