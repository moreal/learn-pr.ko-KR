<span data-ttu-id="e8546-101">Jim은 다양한 플랫폼에서 운영되는 여러 웹 사이트 및 데이터베이스 서버가 포함된 회사 웹 인프라에서 실행 중인 Azure Virtual Machines 집합을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-101">Jim manages a set of Azure virtual machines running on our corporate web infrastructure, which includes several websites and database servers running on various platforms.</span></span> 

<span data-ttu-id="e8546-102">Azure Portal은 쉽게 사용할 수 있지만, Jim은 여러 블레이드를 탐색하는 경우 일부 태스크에 시간이 더 걸린다는 것을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-102">While the Azure portal is easy to use, Jim has found that navigating through the various blades adds time to some of the tasks.</span></span> 

<span data-ttu-id="e8546-103">대안을 모색하는 동안 Jim은 Azure CLI 도구를 발견합니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-103">While exploring alternatives, he discovers the Azure CLI tool.</span></span>

<span data-ttu-id="e8546-104">Azure CLI로 작업하면서 Jim은 서버의 상태를 확인하고 새 구성을 배포하고 포트를 열거나 가상 머신에 연결하여 설정을 변경하기 위한 스크립트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-104">Working with the Azure CLI, Jim can write scripts to check the status of his servers, deploy a new configuration, open a port, or connect to a virtual machine to change a setting.</span></span>

<span data-ttu-id="e8546-105">Jim과 마찬가지로 여러분도 클라우드 환경에서 태스크를 자동화하는 데 도움이 되는 도구를 찾고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-105">Perhaps you are like Jim and are looking for a tool to help automate tasks in your cloud environment.</span></span> <span data-ttu-id="e8546-106">Azure CLI를 사용하여 Azure에 호스팅되는 가상 머신을 만들고 관리하는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-106">We're going to show you how to use the Azure CLI to create and manage virtual machines hosted in Azure.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="e8546-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e8546-107">Azure CLI</span></span>

<span data-ttu-id="e8546-108">Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-108">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="e8546-109">macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-109">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8546-110">Azure CLI 도구는 현재 Azure CLI 1.0 및 Azure CLI 2.0의 두 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-110">There are two versions of the Azure CLI tool available today: Azure CLI 1.0 and Azure CLI 2.0.</span></span> <span data-ttu-id="e8546-111">1.0용으로 작성된 레거시 스크립트를 실행하는 경우가 아니라면 최신 버전인 Azure CLI 2.0을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-111">We'll be using Azure CLI 2.0, which is the latest version and is recommended unless you're running legacy scripts written for 1.0.</span></span> <span data-ttu-id="e8546-112">Azure CLI 1.0은 `azure` 명령으로 시작되고 Azure CLI 2.0은 `az` 명령으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-112">Azure CLI 1.0 is started with the `azure` command, and Azure CLI 2.0 is started with the `az` command.</span></span> 

<span data-ttu-id="e8546-113">Azure CLI를 사용하면 명령줄이나 스크립트를 통해 가상 머신 및 디스크와 같은 Azure 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-113">The Azure CLI can help you manage Azure resources such as virtual machines and disks from the command line or in scripts.</span></span> <span data-ttu-id="e8546-114">이제 시작하여 무엇을 할 수 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8546-114">Let's get started and see what it can do.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="e8546-115">학습 목표</span><span class="sxs-lookup"><span data-stu-id="e8546-115">Learning Objectives</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e8546-116">CLI로 Azure 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="e8546-116">Create an Azure Virtual Machine with the CLI</span></span>
> * <span data-ttu-id="e8546-117">CLI로 VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e8546-117">Resize VMs with the CLI</span></span>
> * <span data-ttu-id="e8546-118">명령줄에서 VM 관리 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="e8546-118">Manage and query a VM from the command line</span></span>
> * <span data-ttu-id="e8546-119">VM에 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="e8546-119">Install software into a VM</span></span>