---
zone_pivot_groups: platform
ms.openlocfilehash: 5e0a236b9cf0c3c0b23beb1324f35a34dade2e92
ms.sourcegitcommit: 926510a198d738c5726081f6d7994fe9b6fc6edb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43179831"
---
<span data-ttu-id="86b9c-101">로컬 머신에 Azure CLI를 설치한 후에 간단한 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-101">Let's install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> <span data-ttu-id="86b9c-102">Azure CLI 설치에 사용하는 방법은 컴퓨터의 운영 체제에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-102">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="86b9c-103">운영 체제에 맞는 단계를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="86b9c-103">Please choose the steps for your operating system.</span></span>

<span data-ttu-id="86b9c-104">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="86b9c-104">::: zone pivot="linux"</span></span>

### <a name="linux"></a><span data-ttu-id="86b9c-105">Linux</span><span class="sxs-lookup"><span data-stu-id="86b9c-105">Linux</span></span>
<span data-ttu-id="86b9c-106">여기서는 고급 패키징 도구(**apt**) 및 Bash 명령줄을 사용하여 **Ubuntu Linux**에 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-106">Here you will install the Azure CLI on **Ubuntu Linux** using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!WARNING]
> <span data-ttu-id="86b9c-107">아래에 나열된 명령은 Ubuntu 버전 18.04용입니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="86b9c-108">다른 버전의 Ubuntu를 사용하는 경우 다른 리포지토리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="86b9c-109">자세한 내용은 [apt를 사용하여 Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli-apt)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b9c-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="86b9c-110">Microsoft 리포지토리가 등록되도록 소스 목록을 수정하면 패키지 관리자가 Azure CLI 패키지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. <span data-ttu-id="86b9c-111">Microsoft Ubuntu 리포지토리의 암호화 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="86b9c-112">이렇게 하면 설치한 Azure CLI 패키지가 Microsoft에서 오는 것인지를 패키지 관리자가 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="86b9c-113">Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

<span data-ttu-id="86b9c-114">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="86b9c-114">::: zone-end</span></span>

<span data-ttu-id="86b9c-115">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="86b9c-115">::: zone pivot="macos"</span></span>

### <a name="macos"></a><span data-ttu-id="86b9c-116">macOS</span><span class="sxs-lookup"><span data-stu-id="86b9c-116">macOS</span></span>
<span data-ttu-id="86b9c-117">여기서는 Homebrew 패키지 관리자를 사용하여 macOS에 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-117">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86b9c-118">**brew** 명령을 사용할 수 없는 경우에는 Homebrew 패키지 관리자를 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-118">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="86b9c-119">자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b9c-119">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="86b9c-120">최신 Azure CLI 패키지를 가져올 수 있도록 brew 리포지토리를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-120">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```

1. <span data-ttu-id="86b9c-121">Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-121">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

<span data-ttu-id="86b9c-122">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="86b9c-122">::: zone-end</span></span>

<span data-ttu-id="86b9c-123">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="86b9c-123">::: zone pivot="windows"</span></span>

### <a name="windows"></a><span data-ttu-id="86b9c-124">Windows</span><span class="sxs-lookup"><span data-stu-id="86b9c-124">Windows</span></span>
<span data-ttu-id="86b9c-125">여기서는 MSI 설치 프로그램을 사용하여 Windows에 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-125">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="86b9c-126">[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)로 이동하여 브라우저 보안 대화 상자에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-126">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="86b9c-127">설치 프로그램에서 라이선스 이용 약관에 동의한 후에 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-127">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="86b9c-128">**사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-128">In the **User Account Control** dialog, select **Yes**.</span></span>

<span data-ttu-id="86b9c-129">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="86b9c-129">::: zone-end</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="86b9c-130">Azure CLI 실행</span><span class="sxs-lookup"><span data-stu-id="86b9c-130">Running the Azure CLI</span></span>
<span data-ttu-id="86b9c-131">bash 셸(Linux 및 macOS) 또는 명령 프롬프트나 PowerShell(Windows)을 열어 Azure CLI를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-131">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="86b9c-132">Azure CLI를 시작하고 버전 검사를 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-132">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

<span data-ttu-id="86b9c-133">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="86b9c-133">::: zone pivot="windows"</span></span>

> [!NOTE]
> <span data-ttu-id="86b9c-134">PowerShell에서 Azure CLI를 실행하면 Windows 명령 프롬프트에서 Azure CLI를 실행할 때에 비해 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-134">Running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the Windows command prompt.</span></span> <span data-ttu-id="86b9c-135">PowerShell은 명령 프롬프트에서 사용할 수 있는 탭 완성 기능 외에 일부 탭 완성 기능을 추가로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-135">PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

<span data-ttu-id="86b9c-136">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="86b9c-136">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="86b9c-137">요약</span><span class="sxs-lookup"><span data-stu-id="86b9c-137">Summary</span></span>
<span data-ttu-id="86b9c-138">Azure CLI를 사용하여 Azure 리소스를 관리하도록 로컬 머신을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-138">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="86b9c-139">이제 로컬에서 Azure CLI를 사용하여 명령을 입력하거나 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-139">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="86b9c-140">Azure CLI가 Azure 데이터 센터로 명령을 전달하면 Azure 구독 내에서 명령이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="86b9c-140">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>