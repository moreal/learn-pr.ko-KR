<span data-ttu-id="18c08-101">여러분은 기술 전문가로서 특정 영역에 대한 전문 지식을 갖고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-101">As a technology professional, you likely have expertise in a specific area.</span></span> <span data-ttu-id="18c08-102">저장소 관리자 또는 가상화 전문가인 분도 있고, 최신 보안 사례에 집중하는 분도 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-102">Perhaps you're a storage admin or virtualization expert, or maybe you focus on the latest security practices.</span></span> <span data-ttu-id="18c08-103">아직 학생인 분들 중에는 적성에 맞는 분야를 찾고 있는 분들도 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-103">If you're a student, you may still be exploring what interests you most.</span></span>

<span data-ttu-id="18c08-104">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-104">::: zone pivot="windows-cloud"</span></span>

<span data-ttu-id="18c08-105">여러분이 어떤 역할을 맡고 있든, 대부분의 사람들은 가상 머신을 만들어서 클라우드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-105">No matter your role, most people get started with the cloud by creating a virtual machine.</span></span> <span data-ttu-id="18c08-106">여기서는 Windows Server 2016을 실행하는 가상 머신을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-106">Here you'll bring up a virtual machine running Windows Server 2016.</span></span>

<span data-ttu-id="18c08-107">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-107">::: zone-end</span></span>

<span data-ttu-id="18c08-108">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-108">::: zone pivot="linux-cloud"</span></span>

<span data-ttu-id="18c08-109">여러분이 어떤 역할을 맡고 있든, 대부분의 사람들은 가상 머신을 만들어서 클라우드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-109">No matter your role, most people get started with the cloud by creating a virtual machine.</span></span> <span data-ttu-id="18c08-110">여기서는 Ubuntu 16.04를 실행하는 가상 머신을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-110">Here you'll bring up a virtual machine running Ubuntu 16.04.</span></span>

<span data-ttu-id="18c08-111">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-111">::: zone-end</span></span>

<span data-ttu-id="18c08-112">Azure에서 가상 머신을 만드는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-112">There are many ways to create a virtual machine on Azure.</span></span> <span data-ttu-id="18c08-113">여기서는 Cloud Shell이라고 하는 대화형 터미널을 사용하여 Windows 또는 Linux 가상 머신을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-113">Here, you'll bring up a Windows or Linux virtual machine using an interactive terminal called Cloud Shell.</span></span> <span data-ttu-id="18c08-114">매일 터미널에서 작업하는 분들은 종종 이 방법으로 작업을 가장 빠르게 수행할 수 있다는 사실을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-114">If you work from the terminal on a daily basis, you know this is often the fastest way to get the job done.</span></span>

<span data-ttu-id="18c08-115">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-115">::: zone pivot="windows-cloud"</span></span>

> [!TIP]
> <span data-ttu-id="18c08-116">Linux를 사용하시겠습니까 아니면 뭔가 새로운 것에 도전하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="18c08-116">Prefer Linux or want to try something new?</span></span> <span data-ttu-id="18c08-117">Linux 가상 머신을 실행하려면 이 페이지 맨 위에서 **Linux**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="18c08-117">Select **Linux** from the top of this page to run a Linux virtual machine.</span></span>

<span data-ttu-id="18c08-118">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-118">::: zone-end</span></span>

<span data-ttu-id="18c08-119">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-119">::: zone pivot="linux-cloud"</span></span>

> [!TIP]
> <span data-ttu-id="18c08-120">Windows를 사용하시겠습니까 아니면 뭔가 새로운 것에 도전하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="18c08-120">Prefer Windows or want to try something new?</span></span> <span data-ttu-id="18c08-121">Windows Server 가상 머신을 실행하려면 이 페이지 맨 위에서 **Windows**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="18c08-121">Select **Windows** from the top of this page to run a Windows Server virtual machine.</span></span>

<span data-ttu-id="18c08-122">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-122">::: zone-end</span></span>

<span data-ttu-id="18c08-123">몇 가지 기본 용어를 검토하고 첫 번째 가상 머신을 작동하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-123">Let's review some basic terms and get your first virtual machine up and running.</span></span>

## <a name="what-is-a-virtual-machine"></a><span data-ttu-id="18c08-124">가상 머신이란?</span><span class="sxs-lookup"><span data-stu-id="18c08-124">What is a virtual machine?</span></span>

<span data-ttu-id="18c08-125">VM(가상 머신)은 물리적 컴퓨터의 소프트웨어 에뮬레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-125">A virtual machine, or VM, is a software emulation of a physical computer.</span></span> <span data-ttu-id="18c08-126">VM은 소프트웨어로 존재하기 때문에 수십, 수백, 심지어 수천 대의 Azure VM을 몇 분 안에 생성할 수 있으며, 더 이상 필요 없을 때 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-126">Because VMs exist as software, dozens, hundreds, or even thousands of Azure VMs can be generated in minutes, then deleted when you don't need them anymore.</span></span> <span data-ttu-id="18c08-127">저렴한 분당 요금이 청구되며, 사용하는 동안 계산 리소스 사용량에 대해서만 요금을 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-127">With low-cost, per-minute billing, you pay only for the compute resources you use, for as long as you are using them.</span></span> <span data-ttu-id="18c08-128">또한 여러 가지 방법으로 필요에 맞게 VM을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-128">Plus, there are many ways to configure the VMs to fit your needs.</span></span>

<span data-ttu-id="18c08-129">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-129">::: zone pivot="windows-cloud"</span></span>

<span data-ttu-id="18c08-130">실행 중인 VM의 스냅숏을 _이미지_라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-130">A snapshot of a running VM is called an _image_.</span></span> <span data-ttu-id="18c08-131">Azure는 Windows 및 여러 Linux 버전을 위한 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-131">Azure provides images for Windows and several flavors of Linux.</span></span> <span data-ttu-id="18c08-132">또한 미리 구성된 고유의 이미지를 만들어서 배포를 신속하게 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-132">You can also create your own preconfigured images to make deployments go faster.</span></span> <span data-ttu-id="18c08-133">여기서는 Microsoft에서 제공하는 Windows Server 2016 VM을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-133">Here you'll bring up a Windows Server 2016 VM, provided by Microsoft.</span></span>

<span data-ttu-id="18c08-134">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-134">::: zone-end</span></span>

<span data-ttu-id="18c08-135">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-135">::: zone pivot="linux-cloud"</span></span>

<span data-ttu-id="18c08-136">실행 중인 VM의 스냅숏을 _이미지_라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-136">A snapshot of a running VM is called an _image_.</span></span> <span data-ttu-id="18c08-137">Azure는 Windows 및 여러 Linux 버전을 위한 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-137">Azure provides images for Windows and several flavors of Linux.</span></span> <span data-ttu-id="18c08-138">또한 미리 구성된 고유의 이미지를 만들어서 배포를 신속하게 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-138">You can also create your own preconfigured images to make deployments go faster.</span></span> <span data-ttu-id="18c08-139">여기서는 Canonical에서 제공하는 Ubuntu 16.04 VM을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-139">Here you'll bring up an Ubuntu 16.04 VM, provided by Canonical.</span></span>

<span data-ttu-id="18c08-140">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-140">::: zone-end</span></span>

## <a name="what-defines-a-virtual-machine-on-azure"></a><span data-ttu-id="18c08-141">Azure에서 가상 머신을 정의하는 것은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="18c08-141">What defines a virtual machine on Azure?</span></span>

<span data-ttu-id="18c08-142">가상 머신은 크기와 위치를 비롯한 여러 요소로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-142">A virtual machine is defined by a number of factors, including its size and location.</span></span> <span data-ttu-id="18c08-143">VM을 가져오기 전에, 어떤 요소가 있는지 간단하게 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-143">Before you bring up your VM, let's briefly cover what's involved.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="18c08-144">**크기**</span><span class="sxs-lookup"><span data-stu-id="18c08-144">**Size**</span></span>
    :::column-end:::
    <span data-ttu-id="18c08-145">:::column span="3"::: VM의 _크기_는 프로세서 속도, 메모리 양, 초기 저장소 양, 예상 네트워크 대역폭을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-145">:::column span="3"::: A VM's _size_ defines its processor speed, amount of memory, initial amount of storage, and expected network bandwidth.</span></span> <span data-ttu-id="18c08-146">일부 크기에는 그래픽 집약적 렌더링 및 비디오 편집용 GPU 같은 특수 하드웨어까지 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-146">Some sizes even include specialized hardware such as GPUs for heavy graphics rendering and video editing.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="18c08-147">**Azure 지역**</span><span class="sxs-lookup"><span data-stu-id="18c08-147">**Region**</span></span>
    :::column-end:::
    <span data-ttu-id="18c08-148">:::column span="3"::: Azure는 전 세계에 분산된 데이터 센터로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-148">:::column span="3"::: Azure is made up of data centers distributed throughout the world.</span></span> <span data-ttu-id="18c08-149">_Azure 지역_은 명명된 지리적 위치에 있는 Azure 데이터 센터의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-149">A _region_ is a set of Azure data centers in a named geographic location.</span></span> <span data-ttu-id="18c08-150">가상 머신을 비롯한 모든 Azure 리소스에는 Azure 지역이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-150">Every Azure resource, including virtual machines, is assigned a region.</span></span> <span data-ttu-id="18c08-151">Azure 지역의 예로 미국 동부, 북유럽 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-151">East US and North Europe are examples of regions.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="18c08-152">**네트워크**</span><span class="sxs-lookup"><span data-stu-id="18c08-152">**Network**</span></span>
    :::column-end:::
    <span data-ttu-id="18c08-153">:::column span="3"::: _가상 네트워크_란 Azure에서 논리적으로 격리된 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-153">:::column span="3"::: A _virtual network_ is a logically isolated network on Azure.</span></span> <span data-ttu-id="18c08-154">Azure의 각 가상 머신은 가상 네트워크와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-154">Each virtual machine on Azure is associated with a virtual network.</span></span> <span data-ttu-id="18c08-155">Azure는 가상 네트워크에 _네트워크 보안 그룹_이라고 하는 클라우드 수준 방화벽을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-155">Azure provides cloud-level firewalls for your virtual networks called _network security groups_.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="18c08-156">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="18c08-156">**Resource groups**</span></span>
    :::column-end:::
    <span data-ttu-id="18c08-157">:::column span="3"::: 가상 머신 및 기타 클라우드 리소스는 _리소스 그룹_이라고 하는 논리적 컨테이너로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-157">:::column span="3"::: Virtual machines and other cloud resources are grouped into logical containers called _resource groups_.</span></span> <span data-ttu-id="18c08-158">그룹은 일반적으로 응용 프로그램 또는 서비스의 일부로 함께 배포되는 리소스 집합을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-158">Groups are typically used to organize sets of resources that are deployed together as part of an application or service.</span></span> <span data-ttu-id="18c08-159">리소스 그룹은 이름을 사용하여 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-159">You refer to a resource group by its name.</span></span>
    :::column-end:::
:::row-end:::

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="18c08-160">Azure Cloud Shell이란?</span><span class="sxs-lookup"><span data-stu-id="18c08-160">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="18c08-161">Azure Cloud Shell은 Azure 리소스를 관리하고 개발하기 위한 브라우저 기반 명령줄 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-161">Azure Cloud Shell is a browser-based command-line experience for managing and developing Azure resources.</span></span> <span data-ttu-id="18c08-162">Cloud Shell을 클라우드에서 실행되는 대화형 콘솔이라고 생각하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-162">Think of Cloud Shell as an interactive console that you run in the cloud.</span></span>

<span data-ttu-id="18c08-163">Cloud Shell은 Bash와 PowerShell의 두 가지 환경 중에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-163">Cloud Shell provides two experiences to choose from: Bash and PowerShell.</span></span> <span data-ttu-id="18c08-164">두 환경 모두 Azure의 명령줄 인터페이스인 Azure CLI에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-164">Both include access to the Azure CLI, the command-line interface for Azure.</span></span>

<span data-ttu-id="18c08-165">Azure Portal, Azure CLI, Azure PowerShell을 비롯한 모든 Azure 관리 인터페이스를 사용하여 모든 종류의 VM을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-165">You can use any Azure management interface, including the Azure portal, Azure CLI, and Azure PowerShell, to manage any kind of VM.</span></span> <span data-ttu-id="18c08-166">여기서는 학습이 목적이기 때문에 Azure CLI를 사용하여 Windows 또는 Linux VM을 만들고 관리하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-166">For learning purposes, here you'll use the Azure CLI to create and manage either a Windows or Linux VM.</span></span>

<span data-ttu-id="18c08-167">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-167">::: zone pivot="windows-cloud"</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="18c08-168">Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="18c08-168">Create a Windows VM</span></span>

<span data-ttu-id="18c08-169">Windows VM을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-169">Let's get your Windows VM up and running.</span></span>

1. <span data-ttu-id="18c08-170">이 페이지 오른쪽의 Cloud Shell에서 `az group create` 명령을 실행하여 미국 동부 지역에 **myResourceGroup**이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-170">From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.</span></span>

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```

1. <span data-ttu-id="18c08-171">`az vm create` 명령을 실행하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-171">Run the `az vm create` command to create your VM.</span></span> <span data-ttu-id="18c08-172">아래의 암호를 나중에 기억하기 쉬운 암호로 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-172">We recommend you change the password shown below to one you'll remember later.</span></span>

      > [!NOTE]
    > <span data-ttu-id="18c08-173">대문자와 소문자, 숫자 및 기호의 조합으로 이루어진 8자 이상의 암호를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-173">Choose a password that contains at least 8 characters with a combination of upper and lowercase letters, numbers, and symbols.</span></span>

    ```azurecli
    az vm create \
      --name myWindowsVM \
      --resource-group myResourceGroup \
      --image Win2016Datacenter \
      --size Standard_DS2_v2 \
      --location eastus \
      --admin-username azureuser \
      --admin-password "Password1234&"
    ```

    > [!TIP]
    > <span data-ttu-id="18c08-174">**복사** 단추를 사용하여 각 명령을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-174">You can use the **Copy** button to copy each command.</span></span> <span data-ttu-id="18c08-175">붙여넣으려면 Cloud Shell 창에서 새 줄을 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-175">To paste it, right click on the new line in the Cloud Shell window and select **Paste**.</span></span>

    <span data-ttu-id="18c08-176">VM이 나타날 때까지 4~5분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-176">Your VM will take four to five minutes to come up.</span></span> <span data-ttu-id="18c08-177">랙 시스템을 구입하여 데이터 센터에서 구성하는 데 걸리는 시간과 비교해 보세요.</span><span class="sxs-lookup"><span data-stu-id="18c08-177">Compare that to the time it takes to purchase, rack, and configure a system in your data center.</span></span> <span data-ttu-id="18c08-178">하늘과 땅 차이죠!</span><span class="sxs-lookup"><span data-stu-id="18c08-178">Quite a difference!</span></span>

<span data-ttu-id="18c08-179">기다리는 동안 방금 실행한 명령을 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-179">While you're waiting, let's review the command you just ran.</span></span>

* <span data-ttu-id="18c08-180">VM 이름은 **myWindowsVM**입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-180">The VM is named **myWindowsVM**.</span></span> <span data-ttu-id="18c08-181">이 이름은 Azure에서 VM을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-181">This name identifies the VM in Azure.</span></span> <span data-ttu-id="18c08-182">또한 VM의 내부 호스트 이름 또는 머신 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-182">It also becomes the VM's internal hostname, or computer name.</span></span>
* <span data-ttu-id="18c08-183">리소스 그룹 또는 VM의 논리적 컨테이너는 **myResourceGroup**입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-183">The resource group, or the VM's logical container, is named **myResourceGroup**.</span></span>
* <span data-ttu-id="18c08-184">**Win2016Datacenter**는 Windows Server 2016 VM 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-184">**Win2016Datacenter** specifies the Windows Server 2016 VM image.</span></span>
* <span data-ttu-id="18c08-185">**Standard_DS2_v2**는 VM 크기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-185">**Standard_DS2_v2** refers to the size of the VM.</span></span> <span data-ttu-id="18c08-186">현재 이 크기는 가상 CPU 2대와 7GB 메모리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-186">This size has two virtual CPUs and 7 GB of memory.</span></span>
* <span data-ttu-id="18c08-187">VM은 **미국 동부** 위치 또는 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-187">The VM exists in the **East US** location, or region.</span></span>
* <span data-ttu-id="18c08-188">사용자 이름 및 암호를 사용하여 나중에 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-188">The username and password enable you to connect to your VM later.</span></span> <span data-ttu-id="18c08-189">예를 들어 원격 데스크톱 또는 WinRM을 통해 연결하여 시스템을 사용하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-189">For example, you can connect over Remote Desktop or WinRM to work with and configure the system.</span></span>

<span data-ttu-id="18c08-190">기본적으로 Azure는 VM에 공용 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-190">By default, Azure assigns a public IP address to your VM.</span></span> <span data-ttu-id="18c08-191">인터넷에서 또는 오직 내부 네트워크에서만 액세스할 수 있도록 VM을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-191">You can configure a VM to be accessible from the Internet or only from the internal network.</span></span>

<span data-ttu-id="18c08-192">VM을 만들고 관리하는 데 사용되는 옵션을 설명하는 이 짧은 비디오도 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="18c08-192">You can also check out this short video about some of the options you have to create and manage VMs.</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

<span data-ttu-id="18c08-193">VM이 준비되면 VM 관련 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-193">When the VM is ready, you see information about it.</span></span> <span data-ttu-id="18c08-194">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-194">Here's an example.</span></span>

```console
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myWindowsVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1E-1B-3B",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "104.211.9.245",
  "resourceGroup": "myResourceGroup",
  "zones": ""
}
```

<span data-ttu-id="18c08-195">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-195">::: zone-end</span></span>

<span data-ttu-id="18c08-196">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="18c08-196">::: zone pivot="linux-cloud"</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="18c08-197">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="18c08-197">Create a Linux VM</span></span>

<span data-ttu-id="18c08-198">Linux VM을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-198">Let's get your Linux VM up and running.</span></span>

1. <span data-ttu-id="18c08-199">이 페이지 오른쪽의 Cloud Shell에서 `az group create` 명령을 실행하여 미국 동부 지역에 **myResourceGroup**이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-199">From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.</span></span>

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```

1. <span data-ttu-id="18c08-200">`az vm create` 명령을 실행하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-200">Run the `az vm create` command to create your VM.</span></span>

    ```azurecli
    az vm create \
      --name myLinuxVM \
      --resource-group myResourceGroup \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --location eastus \
      --generate-ssh-keys
    ```

    > [!TIP]
    > <span data-ttu-id="18c08-201">**복사** 단추를 사용하여 각 명령을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-201">You can use the **Copy** button to copy each command.</span></span> <span data-ttu-id="18c08-202">붙여넣으려면 Cloud Shell 창에서 새 줄을 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-202">To paste it, right click on the new line in the Cloud Shell window and select **Paste**.</span></span>

    <span data-ttu-id="18c08-203">VM이 나타날 때까지 약 2분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-203">Your VM will take about two minutes to come up.</span></span> <span data-ttu-id="18c08-204">랙 시스템을 구입하여 데이터 센터에서 구성하는 데 걸리는 시간과 비교해 보세요.</span><span class="sxs-lookup"><span data-stu-id="18c08-204">Compare that to the time it takes to purchase, rack, and configure a system in your data center.</span></span> <span data-ttu-id="18c08-205">하늘과 땅 차이죠!</span><span class="sxs-lookup"><span data-stu-id="18c08-205">Quite a difference!</span></span>

<span data-ttu-id="18c08-206">기다리는 동안 방금 실행한 명령을 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-206">While you're waiting, let's review the command you just ran.</span></span>

* <span data-ttu-id="18c08-207">VM 이름은 **myLinuxVM**입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-207">The VM is named **myLinuxVM**.</span></span> <span data-ttu-id="18c08-208">이 이름은 Azure에서 VM을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-208">This name identifies the VM in Azure.</span></span> <span data-ttu-id="18c08-209">또한 VM의 내부 호스트 이름 또는 머신 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-209">It also becomes the VM's internal hostname, or computer name.</span></span>
* <span data-ttu-id="18c08-210">리소스 그룹 또는 VM의 논리적 컨테이너는 **myResourceGroup**입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-210">The resource group, or the VM's logical container, is named **myResourceGroup**.</span></span>
* <span data-ttu-id="18c08-211">**UbuntuLTS**는 Ubuntu 16.04 LTS VM 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-211">**UbuntuLTS** specifies the Ubuntu 16.04 LTS VM image.</span></span>
* <span data-ttu-id="18c08-212">**Standard_DS2_v2**는 VM 크기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-212">**Standard_DS2_v2** refers to the size of the VM.</span></span> <span data-ttu-id="18c08-213">현재 이 크기는 가상 CPU 2대와 7GB 메모리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-213">This size has two virtual CPUs and 7 GB of memory.</span></span>
* <span data-ttu-id="18c08-214">VM은 **미국 동부** 위치 또는 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-214">The VM exists in the **East US** location, or region.</span></span>
* <span data-ttu-id="18c08-215">`--generate-ssh-keys` 옵션은 VM에 로그인할 수 있도록 SSH 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-215">The `--generate-ssh-keys` option creates an SSH key pair to enable you to log in to the VM.</span></span>

<span data-ttu-id="18c08-216">기본적으로 Azure는 VM에 공용 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-216">By default, Azure assigns a public IP address to your VM.</span></span> <span data-ttu-id="18c08-217">인터넷에서 또는 오직 내부 네트워크에서만 액세스할 수 있도록 VM을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-217">You can configure a VM to be accessible from the Internet or only from the internal network.</span></span>

<span data-ttu-id="18c08-218">VM을 만들고 관리하는 데 사용되는 옵션을 설명하는 이 짧은 비디오도 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="18c08-218">You can also check out this short video about some of the options you have to create and manage VMs.</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

<span data-ttu-id="18c08-219">VM이 준비되면 VM 관련 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-219">When the VM is ready, you see information about it.</span></span> <span data-ttu-id="18c08-220">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-220">Here's an example.</span></span>

```console
{
    "fqdns": "",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myLinuxVM",
    "location": "eastus",
    "macAddress": "00-0D-3A-1D-EB-02",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "137.135.110.210",
    "resourceGroup": "myResourceGroup",
    "zones": ""
}
```

<span data-ttu-id="18c08-221">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="18c08-221">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="18c08-222">요약</span><span class="sxs-lookup"><span data-stu-id="18c08-222">Summary</span></span>

<span data-ttu-id="18c08-223">몇 가지 개념을 살펴보았으니, 이제 몇 분 안에 Azure에서 VM을 실행할 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-223">With just a few concepts under your belt, you're able to spin up a VM on Azure in just a few minutes.</span></span> <span data-ttu-id="18c08-224">여러분은 VM의 크기 및 방화벽 규칙을 포함한 여러 개념에 이미 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-224">Many of these concepts, such as a VM's size and firewall rules, are likely familiar to you already.</span></span>

<span data-ttu-id="18c08-225">다음으로, VM에 웹 서버를 설치하고 기본 웹 사이트 역할을 하도록 웹 서버를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c08-225">Next, you'll install a web server on your VM and configure your web server to serve up a basic web site.</span></span>