<span data-ttu-id="7d6ae-101">다음 도구 중 하나를 사용하여 가상 머신 디스크 캐시 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-101">You can configure virtual machine disk cache settings with any of the following tools:</span></span>

- <span data-ttu-id="7d6ae-102">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7d6ae-102">Azure portal</span></span>
- <span data-ttu-id="7d6ae-103">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="7d6ae-103">Resource Manager templates</span></span>
- <span data-ttu-id="7d6ae-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7d6ae-104">Azure CLI</span></span>
- <span data-ttu-id="7d6ae-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d6ae-105">Azure PowerShell</span></span>

<span data-ttu-id="7d6ae-106">다음 연습에서는 포털을 사용하여 VM을 만들고 해당 디스크에 대한 캐싱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-106">In the next exercise, we're going to use the portal to create a VM and configure caching on its disks.</span></span> <span data-ttu-id="7d6ae-107">명심해야 할 몇 가지 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-107">Here's some information to keep in mind.</span></span> 

<span data-ttu-id="7d6ae-108">Azure Portal을 사용하여 새 VM을 프로비전하는 경우 먼저 VM을 배포한 후에 OS 디스크에 대한 기본 캐싱 구성을 읽기/쓰기에서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-108">When you provision a new VM using the Azure portal, you can't change the default caching configuration for the OS disk from Read/write until the VM is deployed.</span></span>

<span data-ttu-id="7d6ae-109">기존 VM에 데이터 디스크를 추가하는 경우에는 캐시 옵션을 구성한 후에 디스크를 VM에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-109">When you add a data disk to an existing VM, you can configure the cache option before the disk is deployed to the VM.</span></span>

<span data-ttu-id="7d6ae-110">Azure 디스크의 캐시 설정이 변경되면 대상 디스크를 분리하고 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-110">Changing the cache setting of an Azure disk detaches and reattaches the target disk.</span></span> <span data-ttu-id="7d6ae-111">운영 체제 디스크인 경우 VM이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-111">If it's the operating system disk, the VM is restarted.</span></span> <span data-ttu-id="7d6ae-112">디스크 캐시 설정을 변경하기 전에 이 중단의 영향을 받을 수 있는 모든 응용 프로그램/서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-112">Stop all applications/services that might be affected by this disruption before changing the disk cache setting.</span></span>

<span data-ttu-id="7d6ae-113">Azure Portal을 사용하여 VM을 만들고 캐시 설정을 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6ae-113">Let's create a VM and change the cache settings using the Azure portal.</span></span>
