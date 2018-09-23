<span data-ttu-id="8c277-101">지금까지 사용 가능한 Azure Compute Services를 소개했으며, 이제 각 서비스를 자세히 살펴보고 언제 어떤 서비스를 사용해야 하는지를 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-101">Now that you've been introduced to the Azure compute services available, let's look at each more closely to help you decide when to use each service.</span></span>

## <a name="azure-virtual-machines"></a><span data-ttu-id="8c277-102">Azure 가상 머신</span><span class="sxs-lookup"><span data-stu-id="8c277-102">Azure virtual machines</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="8c277-103">![Azure 가상 머신을 나타내는 이미지](../media/3-azure-vms.png)</span><span class="sxs-lookup"><span data-stu-id="8c277-103">![Image representing Azure virtual machines](../media/3-azure-vms.png)</span></span>
  :::column-end:::
  <span data-ttu-id="8c277-104">:::column span="3"::: 운영 체제 및 환경을 완벽하게 제어해야 하는 경우 가상 머신을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-104">:::column span="3"::: When you need total control over the operating system and environment, virtual machines are an ideal choice.</span></span> <span data-ttu-id="8c277-105">물리적 컴퓨터처럼 VM에서 실행되는 모든 소프트웨어를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-105">You're able to customize all of the software running on the VM, just like a physical computer.</span></span> <span data-ttu-id="8c277-106">VM은 특히 사용자 지정 소프트웨어 또는 사용자 지정 호스팅 구성을 실행하는 경우에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-106">This is especially ideal when running custom software or custom hosting configurations.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="8c277-107">VM은 물리적 서버에서 클라우드로 이동하는 경우에도 좋은 선택이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-107">VMs are also an excellent choice when moving from a physical server to the cloud.</span></span> <span data-ttu-id="8c277-108">대개, 물리적 서버의 이미지를 만들고 가상 머신 내에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-108">You can often create an image of the physical server and host it within a virtual machine.</span></span> <span data-ttu-id="8c277-109">이렇게 하면 운영 체제와 응용 프로그램 실행 환경을 자유롭게 선택할 수 있으므로 선택한 도구를 사용하는 거의 모든 언어로 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-109">This gives you complete freedom to choose operating systems and application execution environments, meaning you can develop in almost any language that uses the tools of your choice.</span></span>

<span data-ttu-id="8c277-110">그러나 가상 머신을 유지 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-110">However, you'll be required to maintain the virtual machine.</span></span> <span data-ttu-id="8c277-111">이는 운영 체제와 운영 체제에서 실행하는 소프트웨어를 업데이트해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-111">This means updating the operating system and the software it runs.</span></span> 

<span data-ttu-id="8c277-112">또한 크기를 조정할 때 추가로 고려할 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-112">It also requires more consideration when scaling.</span></span> <span data-ttu-id="8c277-113">가상 머신을 확장할 수 있으므로 계산 및 메모리 리소스를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-113">You can scale up the virtual machine, meaning you can add more compute and memory resources.</span></span> <span data-ttu-id="8c277-114">그러나 여러 인스턴스를 병렬로 실행하거나 확장해야 하는 경우 부하 분산 장치와 같은 기타 서비스를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-114">But if you need to run multiple instances in parallel, or scale out, you may need to add additional services, such as load balancers.</span></span>

<span data-ttu-id="8c277-115">따라서 과학자가 처리되어야 하는 천문학 이미지를 업로드할 수 있도록 하는 웹 사이트를 실행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-115">So, imagine you're running a web site that enables scientists to upload astronomy images that need to be processed.</span></span> <span data-ttu-id="8c277-116">VM을 복제한 경우 웹 사이트 VM의 여러 인스턴스 간에 요청을 라우팅하는 추가 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-116">If you duplicated the VM, you'd need an additional service to route requests between multiple instances of the web site VM.</span></span>

<span data-ttu-id="8c277-117">Azure에서 사용할 수 있는 고급 가상 머신 서비스도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-117">There are also advanced virtual machine services available in Azure:</span></span>

- <span data-ttu-id="8c277-118">유사하게 구성된 VM에서 동일한 앱 또는 앱 집합의 인스턴스를 일관성 있게 사용할 수 있도록 실행하는 경우 **Virtual Machine Scale Sets** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-118">Use the **Virtual Machine Scale Sets** option when you need to run consistently available instances of the same app, or sets of apps, on similarly configured VMs.</span></span> <span data-ttu-id="8c277-119">이 옵션은 응용 프로그램과 함께 로드되는 수천 개의 동일한 VM을 수분 이내에 자동으로 생성하므로 사용자가 대기할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-119">It automatically generates thousands of identical VMs loaded with your application in minutes, so your users never have to wait.</span></span> <span data-ttu-id="8c277-120">또한 가상 머신을 미리 프로비전할 필요가 없으므로 언제든지 응용 프로그램에 필요한 계산 리소스만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-120">And, since you don't have to pre-provision virtual machines, you use only the compute resources your application needs at any time.</span></span>

- <span data-ttu-id="8c277-121">수십, 수백 또는 수천 개의 VM으로 확장하는 기능과 함께 클라우드 규모의 작업 예약 및 계산 관리가 필요한 경우 **배치** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-121">Use the **Batch** option when you need cloud-scale job scheduling and compute management with the ability to scale to tens, hundreds, or thousands of VMs.</span></span> <span data-ttu-id="8c277-122">원시 컴퓨팅 기능이나 슈퍼 컴퓨터 수준의 계산 기능이 필요한 경우도 있습니다. &mdash; Azure에서는 이러한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-122">There may be situations in which you need raw computing power or supercomputer level compute power &mdash; Azure provides these capabilities.</span></span>

## <a name="azure-containers"></a><span data-ttu-id="8c277-123">Azure 컨테이너</span><span class="sxs-lookup"><span data-stu-id="8c277-123">Azure containers</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="8c277-124">![Azure 컨테이너를 나타내는 이미지](../media/3-azure-containers.png)</span><span class="sxs-lookup"><span data-stu-id="8c277-124">![Image representing Azure containers](../media/3-azure-containers.png)</span></span>
  :::column-end:::
  <span data-ttu-id="8c277-125">:::column span="3"::: 단일 가상 머신에서 응용 프로그램의 여러 인스턴스를 실행하려는 경우에 컨테이너를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-125">:::column span="3"::: If you wish to run multiple instances of an application on a single virtual machine, containers are an excellent choice.</span></span> <span data-ttu-id="8c277-126">컨테이너 오케스트레이터는 필요에 따라 응용 프로그램 인스턴스를 시작하고, 중지하고, 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-126">The container orchestrator can start, stop, and scale out application instances as needed.</span></span>
  :::column-end:::
:::row-end:::

#### <a name="what-are-containers"></a><span data-ttu-id="8c277-127">컨테이너란?</span><span class="sxs-lookup"><span data-stu-id="8c277-127">What are containers?</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

#### <a name="vms-versus-containers"></a><span data-ttu-id="8c277-128">VM 및 컨테이너</span><span class="sxs-lookup"><span data-stu-id="8c277-128">VMs versus containers</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuaq]

<span data-ttu-id="8c277-129">그러나 컨테이너는 일반적으로 마이크로 서비스 아키텍처를 사용하여 솔루션을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-129">However, containers are commonly used to create solutions using a microservice architecture.</span></span> <span data-ttu-id="8c277-130">컨테이너는 솔루션을 소규모 조각으로 분리하는 데 사용되며, 마이크로 서비스 아키텍처를 사용하여 솔루션을 만드는 데도 사용되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-130">Containers are often used to create solutions using a microservice architecture, as they are often used to break solutions into smaller pieces.</span></span> <span data-ttu-id="8c277-131">예를 들어 웹 사이트를 프런트 엔드를 호스트하는 컨테이너, 백 엔드를 호스트하는 컨테이너 및 저장소용 컨테이너로 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-131">For example, you may split a web site into a container hosting your front end, another hosting your back end, and a third for storage.</span></span> <span data-ttu-id="8c277-132">이렇게 하면 앱의 일부를 논리적 섹션으로 구분하여 독립적으로 유지 관리하거나, 확장하거나, 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-132">This allows you to separate portions of your app into logical sections that can be maintained, scaled, or updated independently.</span></span>

#### <a name="what-is-a-microservice"></a><span data-ttu-id="8c277-133">마이크로 서비스란?</span><span class="sxs-lookup"><span data-stu-id="8c277-133">What is a microservice?</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yual]

<span data-ttu-id="8c277-134">웹 사이트 백 엔드가 용량에 도달했지만 프런트 엔드와 저장소는 부하가 크지 않은 경우를 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8c277-134">Imagine your web site back end has reached capacity but the front end and storage aren't being stressed.</span></span> <span data-ttu-id="8c277-135">성능 향상을 위해 별도로 백 엔드의 크기를 조정하거나 다른 저장소 서비스를 사용하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-135">You could scale the back end separately to improve performance, or you could decide to use a different storage service.</span></span> <span data-ttu-id="8c277-136">또는 응용 프로그램의 나머지 부분에 영향을 주지 않고 저장소 컨테이너를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-136">Or you could even replace the storage container without affecting the rest of the application.</span></span>

<span data-ttu-id="8c277-137">팀이 Kubernetes 컨테이너 오케스트레이션을 사용하는 데 익숙한 경우 **AKS(Azure Kubernetes Service)** 옵션을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8c277-137">If your team is comfortable with using Kubernetes container orchestration, consider the **Azure Kubernetes Service (AKS)** option.</span></span> <span data-ttu-id="8c277-138">이 옵션은 Kubernetes 오케스트레이션의 관리, 배포 및 조작을 단순화하고 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-138">It simplifies and automates the management, deployment, and operations of Kubernetes orchestration.</span></span>

#### <a name="what-is-kubernetes"></a><span data-ttu-id="8c277-139">Kubernetes란?</span><span class="sxs-lookup"><span data-stu-id="8c277-139">What is Kubernetes?</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuX]

## <a name="azure-functions"></a><span data-ttu-id="8c277-140">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8c277-140">Azure Functions</span></span>

:::row:::
  :::column:::
    <span data-ttu-id="8c277-141">![Azure Functions를 나타내는 이미지](../media/3-azure-functions.png)</span><span class="sxs-lookup"><span data-stu-id="8c277-141">![Image representing Azure Functions](../media/3-azure-functions.png)</span></span>
  :::column-end:::
  <span data-ttu-id="8c277-142">:::column span="3"::: 기본 플랫폼이나 인프라가 아닌, 서비스를 실행하는 코드에 대해서만 관심이 있는 경우에 Azure Functions를 사용하는 것이 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-142">:::column span="3"::: When you're concerned only about the code running your service, and not the underlying platform or infrastructure, Azure Functions are ideal.</span></span> <span data-ttu-id="8c277-143">Azure Functions는 REST 요청, 타이머 또는 다른 Azure 서비스로부터 받은 메시지를 통해 이벤트에 대한 응답으로 작업을 수행해야 하는 경우, 그리고 해당 작업을 수초 이내에 빠르게 완료할 수 있는 경우에 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-143">They're commonly used when you need to perform work in response to an event, often via a REST request, timer, or message from another Azure service and when that work can be completed quickly, within seconds or less.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="8c277-144">Azure Functions는 자동으로 크기가 조정되므로 수요가 가변적인 경우에 좋은 선택이며, 함수가 트리거된 경우에만 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-144">Azure Functions scale automatically, so they're a solid choice when demand is variable, and you're charged only when a function is triggered.</span></span> <span data-ttu-id="8c277-145">예를 들어 배달 차량을 모니터하는 데 사용되는 IoT 솔루션으로부터 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-145">For example, you may be receiving messages from an IoT solution used to monitor a fleet of delivery vehicles.</span></span> <span data-ttu-id="8c277-146">이 경우에 업무 시간 중에 더 많은 데이터가 도착할 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-146">You'll likely have more data arriving during business hours.</span></span>

<span data-ttu-id="8c277-147">게다가 Azure Functions는 상태 비저장이므로 이벤트에 응답할 때마다 다시 시작되는 것처럼 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-147">Furthermore, Azure Functions are stateless; they behave as if they're restarted every time they respond to an event.</span></span> <span data-ttu-id="8c277-148">들어오는 데이터를 처리하는 데도 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-148">This is ideal for processing incoming data.</span></span> <span data-ttu-id="8c277-149">또한 상태가 필요한 경우 Azure Storage 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c277-149">And if state is required, they can be connected to an Azure storage service.</span></span>
