### <a name="create-an-ubuntu-data-science-vm"></a><span data-ttu-id="cddf3-101">Ubuntu Data Science VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cddf3-101">Create an Ubuntu Data Science VM</span></span>

<span data-ttu-id="cddf3-102">Linux용 Data Science Virtual Machine은 데이터 과학을 간편하게 시작하도록 하는 가상 머신 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-102">The Data Science Virtual Machine for Linux is a virtual-machine image that simplifies getting started with data science.</span></span> <span data-ttu-id="cddf3-103">빠르게 가동하고 실행하기 위해 이미 여러 도구가 빌드되고, 설치되고, 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-103">Multiple tools are already built, installed, and configured in order to get you up and running quickly.</span></span> <span data-ttu-id="cddf3-104">[Jupyter](http://jupyter.org/), 일부 샘플 Jupyter 노트 및 [TensorFlow](https://www.tensorflow.org/)와 마찬가지로 NVIDIA GPU 드라이버, [NVIDIA CUDA](https://developer.nvidia.com/cuda-downloads) 및 [NVIDIA cuDNN](https://developer.nvidia.com/cudnn)(CUDA Deep Neural Network) 라이브러리도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-104">The NVIDIA GPU driver, [NVIDIA CUDA](https://developer.nvidia.com/cuda-downloads) and the [NVIDIA CUDA Deep Neural Network](https://developer.nvidia.com/cudnn) (cuDNN) library are also included, as are [Jupyter](http://jupyter.org/), several sample Jupyter notebooks, and [TensorFlow](https://www.tensorflow.org/).</span></span> <span data-ttu-id="cddf3-105">미리 설치된 모든 프레임워크는 GPU를 지원하지만 CPU에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-105">All pre-installed frameworks are GPU-enabled but work on CPUs as well.</span></span> <span data-ttu-id="cddf3-106">이 단원은 Azure에서 Linux용 DSVM(Data Science Virtual Machine) 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-106">In this unit, you will create an instance of the Data Science Virtual Machine (DSVM) for Linux on Azure.</span></span>

1. <span data-ttu-id="cddf3-107">브라우저에서 [Azure Portal](https://portal.azure.com/?azure-portal=true)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-107">Open the [Azure Portal](https://portal.azure.com/?azure-portal=true) in your browser.</span></span>

1. <span data-ttu-id="cddf3-108">포털 왼쪽에 있는 메뉴에서 **리소스 만들기**를 클릭한 다음, 검색 상자에 "data science"(따옴표 제외)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-108">Click **Create a resource** in the menu on the left side of the portal, and then type "data science" (without quotation marks) into the search box.</span></span> <span data-ttu-id="cddf3-109">결과 목록에서 **Linux용 Data Science Virtual Machine(Ubuntu)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-109">Select **Data Science Virtual Machine for Linux (Ubuntu)** from the results list.</span></span>

    ![Ubuntu Data Science VM 찾기](../media-draft/1-new-data-science-vm.png)

1. <span data-ttu-id="cddf3-111">잠시 VM에 포함된 도구 목록을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="cddf3-111">Take a moment to review the list of tools included in the VM.</span></span> <span data-ttu-id="cddf3-112">그런 다음, 블레이드 아래쪽에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-112">Then, click **Create** at the bottom of the blade.</span></span>

1. <span data-ttu-id="cddf3-113">아래 표시된 것처럼 "기본 사항" 블레이드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-113">Fill in the "Basics" blade as shown below.</span></span> <span data-ttu-id="cddf3-114">대문자, 소문자, 숫자 및 특수 문자를 혼합하여 12자 이상의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-114">Provide a password that's at least 12 characters long containing a mix of uppercase letters, lowercase letters, numbers, and special characters.</span></span> <span data-ttu-id="cddf3-115">*모듈에서 나중에 필요하므로 입력한 사용자 이름과 암호를 기억해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="cddf3-115">*Be sure to remember the user name and password that you enter, because you will need them later in the module.*</span></span>

    ![VM에 대한 기본 정보 입력](../media-draft/1-create-data-science-vm-1.png)

1. <span data-ttu-id="cddf3-117">"크기 선택" 블레이드에서 Data Science VM을 저비용으로 실험해 볼 방법을 제공하는 **DS1_V2 표준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-117">In the "Choose a size" blade, select **DS1_V2 Standard**, which provides a low-cost way to experiment with Data Science VMs.</span></span> <span data-ttu-id="cddf3-118">그런 다음, 블레이드 하단에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-118">Then, click the **Select** button at the bottom of the blade.</span></span>

    ![VM 크기 선택](../media-draft/1-create-data-science-vm-2.png)

1. <span data-ttu-id="cddf3-120">**설정** 블레이드에서 기본값을 그대로 수용하고, **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-120">In the **Settings** blade, accept the defaults, and click the **OK** button.</span></span>

1. <span data-ttu-id="cddf3-121">**만들기** 블레이드에서 잠시 VM에 대해 선택한 옵션을 검토하고 **만들기**를 클릭하여 VM 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-121">In the **Create** blade, take a moment to review the options you selected for the VM, and click **Create** to start the VM creation process.</span></span>

    ![VM 만들기](../media-draft/1-create-data-science-vm-4.png)

1. <span data-ttu-id="cddf3-123">포털 왼쪽에 있는 메뉴에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-123">Click **Resource groups** in the menu on the left side of the portal.</span></span> <span data-ttu-id="cddf3-124">그런 다음, **data-science-rg** 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-124">Then, click the **data-science-rg** resource group.</span></span>

    ![리소스 그룹 열기](../media-draft/1-open-resource-group.png)

  
1. <span data-ttu-id="cddf3-126">"배포 중" 상태가 DSVM 및 지원 Azure 리소스가 생성되었음을 나타내는 "성공"으로 변경될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-126">Wait until "Deploying" changes to "Succeeded", indicating that DSVM and supporting Azure resources have been created.</span></span> <span data-ttu-id="cddf3-127">배포는 일반적으로 5분 이내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-127">Deployment typically takes five minutes or less.</span></span> <span data-ttu-id="cddf3-128">블레이드 위쪽에 있는 **새로 고침**을 주기적으로 클릭하여 배포 상태를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="cddf3-128">Periodically click **Refresh** at the top of the blade to refresh the deployment status.</span></span>

    ![배포 상태 모니터링](../media-draft/1-deployment-succeeded.png)
