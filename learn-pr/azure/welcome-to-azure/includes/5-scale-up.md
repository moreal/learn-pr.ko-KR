<span data-ttu-id="cc893-101">웹 서버가 등록되고 실행되지만 사용자에게 적합한 환경을 만들려면 더 많은 컴퓨팅 기능이 필요함을 인식하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-101">Your web server is up and running, but you realize you need more computing power to make the experience great for your users.</span></span> <span data-ttu-id="cc893-102">어떻게 VM을 더 빠르게 실행하게 할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cc893-102">How can you make your VM run faster?</span></span>

<span data-ttu-id="cc893-103">데이터 센터에서 성능 문제를 해결하려면 웹 서버를 더 강력한 하드웨어로 이동시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-103">In your data center, you might move your web server to more powerful hardware to solve performance problems.</span></span> <span data-ttu-id="cc893-104">문제는 새 시스템을 구입하고 보관하고 전원을 제공해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-104">The problem is you need to buy, rack, and power your new system.</span></span> <span data-ttu-id="cc893-105">Azure를 사용하면 답변이 훨씬 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-105">With Azure, the answer is much simpler.</span></span>

<span data-ttu-id="cc893-106">더 강력한 크기로 VM을 강화하기 전에 먼저 크기 조정의 의미를 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-106">Before you scale up your VM to a more powerful size, let's first define what scale means.</span></span>

## <a name="what-is-scale"></a><span data-ttu-id="cc893-107">크기 조정이란?</span><span class="sxs-lookup"><span data-stu-id="cc893-107">What is scale?</span></span>

<span data-ttu-id="cc893-108">_크기 조정_은 네트워크 대역폭, 메모리, 저장소 또는 계산 능력을 추가하여 성능을 개선하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-108">_Scale_ refers to adding network bandwidth, memory, storage, or compute power to achieve better performance.</span></span>  

<span data-ttu-id="cc893-109">_강화_ 및 _확장_이란 용어를 들어보았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-109">You may have heard the terms _scaling up_ and _scaling out_.</span></span>

<span data-ttu-id="cc893-110">수직적 크기 조정 즉, 강화는 기존 가상 머신의 메모리, 저장소 또는 계산 능력을 향상시키는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-110">Scaling up, or vertical scaling, means to increase the memory, storage, or compute power on an existing virtual machine.</span></span> <span data-ttu-id="cc893-111">예를 들어 웹 또는 데이터베이스 서버에 추가 메모리를 추가하여 더 빨리 실행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-111">For example, you can add additional memory to a web or database server to make it run faster.</span></span>

<span data-ttu-id="cc893-112">수평적 크기 조정 즉, 확장은 응용 프로그램을 개선하기 위해 가상 머신을 추가하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-112">Scaling out, or horizontal scaling, means to additional virtual machines to power your application.</span></span> <span data-ttu-id="cc893-113">예를 들어, 정확히 동일한 방식으로 구성된 여러 가상 머신을 만들고 부하 분산 장치를 사용하여 가상 머신에 작업을 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-113">For example, you might create many virtual machines configured in exactly the same way and use a load balancer to distribute work across them.</span></span>

> [!TIP]
> <span data-ttu-id="cc893-114">클라우드는 탄력적입니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-114">The cloud is elastic.</span></span> <span data-ttu-id="cc893-115">일시적으로 강화하거나 확장해야 하는 경우 배포를 _축소_하거나 _감축_할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-115">You can _scale down_ or _scale in_ your deployment if you needed to scale up or scale out only temporarily.</span></span> <span data-ttu-id="cc893-116">축소 또는 감축은 비용을 절약하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-116">Scaling down or scaling in can help you save money.</span></span><br><br><span data-ttu-id="cc893-117">**Azure Advisor** 및 **Azure Cost Management**는 클라우드를 최적화할 수 있는 두 개의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-117">**Azure Advisor** and **Azure Cost Management** are two services that help you optimize cloud spend.</span></span> <span data-ttu-id="cc893-118">이러한 서비스를 사용하여 필요한 것보다 더 많이 사용하는 경우를 식별한 다음, 실제로 사용 중인 용량으로 다시 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-118">You can use these services to identify where you're using more than you need, and then scale back to the capacity you're actually using.</span></span>

## <a name="scale-up-your-vm"></a><span data-ttu-id="cc893-119">VM 강화</span><span class="sxs-lookup"><span data-stu-id="cc893-119">Scale up your VM</span></span>

<span data-ttu-id="cc893-120">앞서 언급한 것처럼 VM을 만들 때 **Standard_DS2_v2** 크기를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-120">Recall that you specified the size **Standard_DS2_v2** when you created your VM.</span></span> <span data-ttu-id="cc893-121">현재 VM에는 두 개의 가상 CPU와 7GB 메모리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-121">Your VM currently has two virtual CPUs and 7 GB of memory.</span></span>

<span data-ttu-id="cc893-122">다음 크기 **Standard_DS3_v2**로 늘려보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-122">Let's bump up to the next size, **Standard_DS3_v2**.</span></span> <span data-ttu-id="cc893-123">그러면, VM에는 4개의 가상 CPU 및 14GB 메모리가 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-123">Your VM will then have four virtual CPUs and 14 GB of memory.</span></span>

<span data-ttu-id="cc893-124">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="cc893-124">::: zone pivot="windows-cloud"</span></span>

1. <span data-ttu-id="cc893-125">Cloud Shell에서 `az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-125">From Cloud Shell, run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="cc893-126">업데이트 프로세스에는 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-126">The update process takes about a minute.</span></span> <span data-ttu-id="cc893-127">이 프로세스 동안 VM이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-127">Your VM restarts during the process.</span></span>

1. <span data-ttu-id="cc893-128">`az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-128">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="cc893-129">새 VM 크기 **Standard_DS3_v2**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-129">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```output
    Standard_DS3_v2
    ```

<span data-ttu-id="cc893-130">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="cc893-130">::: zone-end</span></span>

<span data-ttu-id="cc893-131">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="cc893-131">::: zone pivot="linux-cloud"</span></span>

1. <span data-ttu-id="cc893-132">Cloud Shell에서 `az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-132">From Cloud Shell, run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="cc893-133">업데이트 프로세스에는 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-133">The update process takes about a minute.</span></span> <span data-ttu-id="cc893-134">이 프로세스 동안 VM이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-134">Your VM restarts during the process.</span></span>

1. <span data-ttu-id="cc893-135">`az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-135">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="cc893-136">새 VM 크기 **Standard_DS3_v2**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-136">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```output
    Standard_DS3_v2
    ```

<span data-ttu-id="cc893-137">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="cc893-137">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="cc893-138">요약</span><span class="sxs-lookup"><span data-stu-id="cc893-138">Summary</span></span>

<span data-ttu-id="cc893-139">잘했습니다!</span><span class="sxs-lookup"><span data-stu-id="cc893-139">Nice job!</span></span> <span data-ttu-id="cc893-140">단 하나의 명령으로 이제 VM이 두 배 강력해집니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-140">With just one command, your VM is now twice as powerful.</span></span>

<span data-ttu-id="cc893-141">강화 및 확장은 성능을 향상시키기 위한 두 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-141">Scaling up and scaling out are two ways to increase performance.</span></span> <span data-ttu-id="cc893-142">여기서 VM을 강화하여 계산 능력을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cc893-142">Here you scaled up your VM to increase its compute power.</span></span>