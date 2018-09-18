<span data-ttu-id="df53d-101">웹 서버가 등록되고 실행되지만 사용자에게 적합한 환경을 만들려면 더 많은 컴퓨팅 기능이 필요함을 인식하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-101">Your web server is up and running, but you realize you need more computing power to make the experience great for your users.</span></span> <span data-ttu-id="df53d-102">어떻게 VM을 더 빠르게 실행하게 할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="df53d-102">How can you make your VM run faster?</span></span>

<span data-ttu-id="df53d-103">데이터 센터에서 성능 문제를 해결하려면 웹 서버를 더 강력한 하드웨어로 이동시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-103">In your data center, you might move your web server to more powerful hardware to solve performance problems.</span></span> <span data-ttu-id="df53d-104">문제는 새 시스템을 구입하고 보관하고 전원을 제공해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-104">The problem is you need to buy, rack, and power your new system.</span></span> <span data-ttu-id="df53d-105">Azure를 사용하면 답변이 훨씬 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-105">With Azure, the answer is much simpler.</span></span>

<span data-ttu-id="df53d-106">이제 VM을 더 강력한 크기로 확장하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-106">Now you'll scale up your VM to a more powerful size.</span></span> <span data-ttu-id="df53d-107">VM의 크기를 변경하기 전에 종료하거나 할당을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-107">Before you change your VM's size, you must shut it down, or deallocate it.</span></span>

<span data-ttu-id="df53d-108">먼저 크기 조정이 어떤 의미인지, VM 할당을 취소하는 경우 무슨 일이 발생하는지를 정의해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-108">First, let's define what scale means and what happens when you deallocate your VM.</span></span>

## <a name="what-is-scale"></a><span data-ttu-id="df53d-109">크기 조정이란?</span><span class="sxs-lookup"><span data-stu-id="df53d-109">What is scale?</span></span>

<span data-ttu-id="df53d-110">_크기 조정_은 네트워크 대역폭, 메모리, 저장소 또는 계산 능력을 추가하여 성능을 개선하는 것을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-110">_Scale_ refers to adding network bandwidth, memory, storage, or compute power to achieve better performance.</span></span>  

<span data-ttu-id="df53d-111">_확장_ 및 _스케일 아웃_이란 용어를 들어보았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-111">You may have heard the terms _scale up_ and _scale out_.</span></span>

<span data-ttu-id="df53d-112">수직적 크기 조정 즉, 확장은 기존 가상 머신의 메모리, 저장소 또는 계산 능력을 향상시키는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-112">Scaling up, or vertical scaling, means to increase the memory, storage, or compute power on an existing virtual machine.</span></span> <span data-ttu-id="df53d-113">예를 들어 웹 또는 데이터베이스 서버에 추가 메모리를 추가하여 더 빨리 실행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-113">For example, you can add additional memory to a web or database server to make it run faster.</span></span>

> [!TIP]
> <span data-ttu-id="df53d-114">일시적으로 확장해야 하는 경우 시스템을 _축소_할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-114">You can also _scale down_ your system if you needed to scale up only temporarily.</span></span>

<span data-ttu-id="df53d-115">수평적 크기 조정 즉, 스케일 아웃은 응용 프로그램에 전원을 제공하기 위해 가상 머신을 추가하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-115">Scaling out, or horizontal scaling, means to additional virtual machines to power your application.</span></span> <span data-ttu-id="df53d-116">예를 들어, 정확히 동일한 방식으로 구성된 여러 가상 머신을 만들고 부하 분산 장치를 사용하여 가상 머신에 작업을 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-116">For example, you might create many virtual machines configured in exactly the same way and use a load balancer to distribute work across them.</span></span>

## <a name="what-is-deallocation"></a><span data-ttu-id="df53d-117">할당 취소란?</span><span class="sxs-lookup"><span data-stu-id="df53d-117">What is deallocation?</span></span>

<span data-ttu-id="df53d-118">할당 취소는 VM을 종료하고 해당 계산 리소스를 릴리스하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-118">Deallocation is the process that shuts down your VM and releases its compute resources.</span></span>

<span data-ttu-id="df53d-119">직장이나 집의 PC를 종료하는 경우 운영 체제는 프로그램을 닫은 다음, 전원 관리 하드웨어에 전원을 끄도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-119">When you shut down your PC at work or at home, the operating system closes your programs and then notifies the power management hardware to turn off power.</span></span>

<span data-ttu-id="df53d-120">가상 머신 할당 취소는 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-120">Deallocating a virtual machine is similar.</span></span> <span data-ttu-id="df53d-121">VM이 종료된 후 Azure는 VM에 전원을 제공하는 데 사용된 하드웨어를 회수합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-121">After your VM shuts down, Azure reclaims the hardware used to power it.</span></span> <span data-ttu-id="df53d-122">데이터 디스크 및 저장소는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-122">Your data disks and storage remain intact.</span></span> <span data-ttu-id="df53d-123">VM 백업을 시작하면 PC와 마찬가지로 중단했던 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-123">When you start your VM back up, you pick up where you left off, just like with your PC.</span></span>

<span data-ttu-id="df53d-124">할당을 취소하면 가상 머신이 사용하는 계산 및 네트워크 리소스에 대해 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-124">When deallocated, you are not billed for the compute and network resources that your virtual machine uses.</span></span> <span data-ttu-id="df53d-125">저장소에 연결된 모든 디스크에 대해서는 여전히 지불하지만 전체 비용은 VM이 실행 중인 경우보다 훨씬 저렴합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-125">You still pay for any associated disks to sit in storage, but the overall cost is much lower than it would be if the VM were running.</span></span>

<span data-ttu-id="df53d-126">여기에는 크기를 조정할 수 있도록 간단히 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-126">Here, you'll deallocate your VM briefly so that you can resize it.</span></span> <span data-ttu-id="df53d-127">하지만 비용을 절감하려면 오랜 기간 동안 VM의 할당을 취소할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-127">But you can also deallocate your VMs for a longer period to save cost.</span></span> <span data-ttu-id="df53d-128">근무 시간 동안 테스트를 위해 사용하는 VM의 은행이 있다고 가정해봅시다.</span><span class="sxs-lookup"><span data-stu-id="df53d-128">Say you have a bank of VMs that you use for testing during work hours.</span></span> <span data-ttu-id="df53d-129">밤 및 주말에도 자동으로 할당이 취소되도록 VM을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-129">You can schedule your VMs to be automatically deallocated on nights and weekends.</span></span> <span data-ttu-id="df53d-130">밤을 세워야 할 경우 수동으로 VM을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-130">If you need to stay late, you can manually restart them.</span></span>

## <a name="scale-up-your-vm"></a><span data-ttu-id="df53d-131">VM 확장</span><span class="sxs-lookup"><span data-stu-id="df53d-131">Scale up your VM</span></span>

<span data-ttu-id="df53d-132">앞서 언급한 것처럼 VM을 만들 때 **Standard_DS2_v2** 크기를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-132">Recall that you specified the size **Standard_DS2_v2** when you created your VM.</span></span> <span data-ttu-id="df53d-133">현재 VM에는 두 개의 가상 CPU와 7GB 메모리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-133">Your VM currently has two virtual CPUs and 7 GB of memory.</span></span>

<span data-ttu-id="df53d-134">다음 크기 **Standard_DS3_v2**로 늘려보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-134">Let's bump up to the next size, **Standard_DS3_v2**.</span></span> <span data-ttu-id="df53d-135">그러면, VM에는 4개의 가상 CPU 및 14GB 메모리가 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-135">Your VM will then have four virtual CPUs and 14 GB of memory.</span></span>

<span data-ttu-id="df53d-136">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="df53d-136">::: zone pivot="windows-cloud"</span></span>

1. <span data-ttu-id="df53d-137">Cloud Shell에서 `az vm deallocate`를 실행하여 VM의 할당을 취소하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-137">From Cloud Shell, run `az vm deallocate` to deallocate, or stop, your VM.</span></span>

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    <span data-ttu-id="df53d-138">이 프로세스는 완료되는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-138">The process takes a couple of minutes to complete.</span></span>
1. <span data-ttu-id="df53d-139">`az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-139">Run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="df53d-140">업데이트 프로세스는 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-140">The update process takes about a minute.</span></span>
1. <span data-ttu-id="df53d-141">`az vm start`를 실행하여 VM 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-141">Run `az vm start` to restart your VM.</span></span>

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    <span data-ttu-id="df53d-142">이 프로세스는 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-142">The process takes about a minute.</span></span>
1. <span data-ttu-id="df53d-143">`az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-143">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="df53d-144">새 VM 크기 **Standard_DS3_v2**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-144">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```console
    Standard_DS3_v2
    ```

<span data-ttu-id="df53d-145">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="df53d-145">::: zone-end</span></span>

<span data-ttu-id="df53d-146">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="df53d-146">::: zone pivot="linux-cloud"</span></span>

1. <span data-ttu-id="df53d-147">Cloud Shell에서 `az vm deallocate`를 실행하여 VM의 할당을 취소하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-147">From Cloud Shell, run `az vm deallocate` to deallocate, or stop, your VM.</span></span>

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    <span data-ttu-id="df53d-148">이 프로세스는 완료되는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-148">The process takes a couple of minutes to complete.</span></span>
1. <span data-ttu-id="df53d-149">`az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-149">Run `az vm resize` to increase your VM's size to **Standard_DS3_v2**.</span></span>

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --size Standard_DS3_v2
    ```
    <span data-ttu-id="df53d-150">업데이트 프로세스는 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-150">The update process takes about a minute.</span></span>
1. <span data-ttu-id="df53d-151">`az vm start`를 실행하여 VM 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-151">Run `az vm start` to restart your VM.</span></span>

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    <span data-ttu-id="df53d-152">이 프로세스는 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-152">The process takes about a minute.</span></span>
1. <span data-ttu-id="df53d-153">`az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-153">Run `az vm show` to verify that your VM is running the new size.</span></span>

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    <span data-ttu-id="df53d-154">새 VM 크기 **Standard_DS3_v2**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-154">You see your new VM size, **Standard_DS3_v2**.</span></span>
    ```console
    Standard_DS3_v2
    ```

<span data-ttu-id="df53d-155">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="df53d-155">::: zone-end</span></span>

> [!NOTE]
> <span data-ttu-id="df53d-156">기본적으로 VM을 중지하고 다시 시작하는 경우 Azure는 VM에 새 공용 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-156">By default, Azure assigns a new public IP address to your VM when you stop and restart it.</span></span> <span data-ttu-id="df53d-157">이 과정은 학습 목적으로 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-157">This is OK for learning purposes.</span></span> <span data-ttu-id="df53d-158">실제로 VM을 다시 시작하는 경우에도 VM에 포함된 공용 IP 주소를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-158">In practice, you can reserve a public IP address that stays with your VM even when your VM is restarted.</span></span>

## <a name="summary"></a><span data-ttu-id="df53d-159">요약</span><span class="sxs-lookup"><span data-stu-id="df53d-159">Summary</span></span>

<span data-ttu-id="df53d-160">잘 하셨습니다!</span><span class="sxs-lookup"><span data-stu-id="df53d-160">Nice job!</span></span> <span data-ttu-id="df53d-161">단 몇 가지 명령으로 이제 VM이 두 배 강력해집니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-161">With just a few commands, your VM is now twice as powerful.</span></span>

<span data-ttu-id="df53d-162">확장 및 스케일 아웃은 성능을 향상시키기 위한 두 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-162">Scaling up and scaling out are two ways to increase performance.</span></span> <span data-ttu-id="df53d-163">여기서 VM을 확장하여 계산 능력을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-163">Here you scaled up your VM to increase its compute power.</span></span>

<span data-ttu-id="df53d-164">크기를 조정할 수 있기 전에 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-164">You deallocate a VM before you can resize it.</span></span> <span data-ttu-id="df53d-165">VM이 비용 절감을 위해 사용되지 않는 경우에도 VM의 할당을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df53d-165">You can also deallocate your VMs when they're not in use to save costs.</span></span>