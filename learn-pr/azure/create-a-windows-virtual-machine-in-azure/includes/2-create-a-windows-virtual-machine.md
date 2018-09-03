<span data-ttu-id="8ca1b-101">회사는 VM을 사용하여 Azure에서 트래픽 카메라의 비디오 데이터를 관리하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-101">Your company has decided to manage the video data from their traffic cameras in Azure using VMs.</span></span> <span data-ttu-id="8ca1b-102">여러 코덱을 실행하려면 먼저 VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-102">In order to run the multiple codecs, we first need to create the VMs.</span></span> <span data-ttu-id="8ca1b-103">또한 VM을 연결하고 조작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-103">We also need to connect and interact with the VMs.</span></span> <span data-ttu-id="8ca1b-104">이 단원에서는 Azure Portal을 사용하여 VM을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-104">In this unit, you will learn how to create a VM using the Azure portal.</span></span> <span data-ttu-id="8ca1b-105">RDP용 VM을 구성하고, VM 이미지를 선택하고, 적절한 저장소 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-105">You will configure the VM for RDP, select a VM image, and choose the proper storage option.</span></span>

## <a name="introduction-to-windows-virtual-machines-in-azure"></a><span data-ttu-id="8ca1b-106">Azure의 Windows Virtual Machines 소개</span><span class="sxs-lookup"><span data-stu-id="8ca1b-106">Introduction to Windows virtual machines in Azure</span></span>

<span data-ttu-id="8ca1b-107">Azure VM은 요청 시 확장 가능한 클라우드 컴퓨팅 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-107">Azure VMs are an on-demand scalable cloud computing resource.</span></span> <span data-ttu-id="8ca1b-108">Windows Hyper-V에서 호스트되는 가상 머신과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-108">They're similar to virtual machines that are hosted in Windows Hyper-V.</span></span> <span data-ttu-id="8ca1b-109">프로세서, 메모리, 저장소 및 네트워킹 리소스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-109">They include a processor, memory, storage, and networking resources.</span></span> <span data-ttu-id="8ca1b-110">Hyper-V와 마찬가지로 원하는 대로 가상 머신을 시작하고 중지할 수 있으며 포털 또는 Azure CLI를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-110">You can start and stop virtual machines at will just like with Hyper-V and manage them from the portal or with the Azure CLI.</span></span> <span data-ttu-id="8ca1b-111">또한 RDP 클라이언트를 사용하여 Windows 데스크톱 UI(사용자 인터페이스)에 직접 연결하고 로컬 Windows 컴퓨터에 로그인한 것처럼 VM을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-111">You can also use an RDP client to connect directly to the Windows desktop user interface (UI) and use the VM as if you were signed in to a local Windows computer.</span></span>

## <a name="create-resources-for-a-windows-vm"></a><span data-ttu-id="8ca1b-112">Windows VM용 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="8ca1b-112">Create resources for a Windows VM</span></span>

<span data-ttu-id="8ca1b-113">Azure에서 Windows VM을 만드는 경우 VM을 호스트할 리소스도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-113">When creating a Windows VM in Azure, you also create resources to host the VM.</span></span> <span data-ttu-id="8ca1b-114">다른 Azure 서비스와 마찬가지로 **리소스 그룹**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-114">Like other Azure services, you'll need a **Resource Group**.</span></span> <span data-ttu-id="8ca1b-115">일반적으로, 다음을 비롯하여 동일한 리소스 그룹의 VM과 관련된 다른 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-115">It's common practice to include other services that are related to the VM in the same resource group, including:</span></span>

* <span data-ttu-id="8ca1b-116">가상 머신</span><span class="sxs-lookup"><span data-stu-id="8ca1b-116">The virtual machine</span></span>
* <span data-ttu-id="8ca1b-117">Storage</span><span class="sxs-lookup"><span data-stu-id="8ca1b-117">Storage</span></span>
* <span data-ttu-id="8ca1b-118">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="8ca1b-118">Virtual networks</span></span> 
* <span data-ttu-id="8ca1b-119">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="8ca1b-119">Network interfaces</span></span>
* <span data-ttu-id="8ca1b-120">서브넷</span><span class="sxs-lookup"><span data-stu-id="8ca1b-120">Subnet</span></span>
* <span data-ttu-id="8ca1b-121">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="8ca1b-121">Public IP address</span></span>

<span data-ttu-id="8ca1b-122">새 VM을 만드는 경우 기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-122">When you create a new VM, you can either use an existing resource group or create a new one.</span></span>

## <a name="choose-the-vm-image"></a><span data-ttu-id="8ca1b-123">VM 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="8ca1b-123">Choose the VM image</span></span>

<span data-ttu-id="8ca1b-124">이미지 선택은 VM을 만들 때 처음 내리는 가장 중요한 결정 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-124">Selecting an image is one of the first and most important decisions you'll make when creating a VM.</span></span> <span data-ttu-id="8ca1b-125">이미지는 VM을 만드는 데 사용되는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-125">An image is a template that's used to create a VM.</span></span> <span data-ttu-id="8ca1b-126">이러한 템플릿에는 OS가 포함되어 있으며, 개발 도구 또는 웹 호스팅 환경과 같은 기타 소프트웨어가 포함된 경우도 많습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-126">These templates include an OS and often other software, such as development tools or web hosting environments.</span></span>

<span data-ttu-id="8ca1b-127">컴퓨터에서 설치할 수 있는 모든 요소가 이미지에 포함될 수 있으므로 아주 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-127">Anything that a computer can have installed can be included in an image and that's powerful.</span></span> <span data-ttu-id="8ca1b-128">ASP.NET Core 앱을 호스트하는 것과 같이 정확히 필요한 태스크로 미리 구성된 이미지에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-128">You can create a VM from an image that's preconfigured to exactly the tasks you need, such as hosting an ASP.Net Core app.</span></span>

<span data-ttu-id="8ca1b-129">선택적으로 고유한 이미지를 만들고 업로드할 수도 있지만 이러한 작업은 이 모듈의 범위에서 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-129">You can optionally create and upload your own images, but that's outside the scope of this module.</span></span>

> [!Note] 
> <span data-ttu-id="8ca1b-130">“가상 머신(클래식)”이라는 기능을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-130">You may notice a feature called "Virtual Machine (classic)."</span></span> <span data-ttu-id="8ca1b-131">이미 인스턴스를 만든 고객에 대해 지원되는 레거시 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-131">This is a legacy feature that's supported for customers who already have created instances.</span></span> <span data-ttu-id="8ca1b-132">새 워크로드의 경우 “Azure 가상 머신” 기능 또는 간단히 “가상 머신”을 사용하려 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-132">For new workloads, you'll want the "Azure Virtual Machine" feature or "Virtual Machines" for short.</span></span>

## <a name="sizing-your-vm"></a><span data-ttu-id="8ca1b-133">VM 크기 지정</span><span class="sxs-lookup"><span data-stu-id="8ca1b-133">Sizing your VM</span></span>

<span data-ttu-id="8ca1b-134">물리적 머신과 마찬가지로 가상 머신에는 일정한 양의 메모리와 CPU 처리 능력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-134">Just as a physical machine has a certain amount of memory and CPU power, so does a virtual machine.</span></span> <span data-ttu-id="8ca1b-135">Azure는 크기와 가격이 다양한 여러 VM을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-135">Azure offers a range of VMs of differing sizes at different price points.</span></span> <span data-ttu-id="8ca1b-136">이러한 VM은 A 시리즈 엔트리 수준 개발로 시작하여 범용 컴퓨팅을 위한 D 시리즈까지 이미지를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-136">These VMs start with A-Series entry-level development and test images through the D-Series for general-purpose computing.</span></span> <span data-ttu-id="8ca1b-137">고성능 계산 요구 사항을 충족할 H 시리즈와 GPU(그래픽 처리 장치) 최적화 역할에 필요한 N 시리즈가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-137">They include the H-Series for high-performance computational needs and the N-series for graphics processor unit (GPU)-optimized roles.</span></span>

<span data-ttu-id="8ca1b-138">모듈 뒷부분에 나와 있는 것처럼 VM을 만든 후 VM 크기를 변경할 수 있지만 이렇게 하면 시스템을 종료해야 하므로 워크로드 가동 중지 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-138">As you'll see later in the module, we can change the size of a VM after it's been created, but that requires shutting it down, which could result in downtime for our workloads.</span></span>

## <a name="choosing-storage-options"></a><span data-ttu-id="8ca1b-139">저장소 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="8ca1b-139">Choosing storage options</span></span>

<span data-ttu-id="8ca1b-140">VM 지정에서 다음에 선택할 사항은 하드 드라이브 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-140">The next choice when specifying a VM is the hard drive technology.</span></span> <span data-ttu-id="8ca1b-141">기존의 플래터 기반 HDD(하드 디스크 드라이브) 또는 최신 SSD(반도체 드라이브)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-141">Options include a traditional platter-based hard disk drive (HDD) or a more modern solid-state drive (SSD).</span></span> <span data-ttu-id="8ca1b-142">SSD 저장소를 사용하면 비용이 더 많은 들지만 성능이 더 뛰어나므로, 특히 높은 수준의 데이터 전송이나 잦은 I/O를 지원하는 환경에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-142">SSD storage costs more to use, but it gives better performance, particularly in environments that support high levels of data transfer or frequent I/O.</span></span>

> [!Note] 
> <span data-ttu-id="8ca1b-143">Azure Virtual Machines의 응용 프로그램은 Azure Cosmos DB, Azure Blob Storage 등 Azure에 있는 다른 형태의 지속성에도 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca1b-143">Applications in Azure Virtual Machines can also connect to other forms of persistence in Azure like Azure Cosmos DB and Azure Blob storage.</span></span>