<span data-ttu-id="42f02-101">이 모듈에서는 Azure Portal을 사용하여 Windows VM을 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-101">In this module, you learned how to create a Windows VM using the Azure portal.</span></span> <span data-ttu-id="42f02-102">그런 다음, 해당 VM의 공용 IP 주소에 연결하고 RDP를 통해 관리했습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-102">You then connected to the public IP address of the VM and managed it over RDP.</span></span> <span data-ttu-id="42f02-103">어떻게 Azure에서 RDP가 물리적 컴퓨터에 대화형으로 로그온하는 것과 비슷한 환경을 제공하는지 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-103">You discovered how RDP in Azure provides a similar experience to logging on interactively to a physical computer.</span></span>

<span data-ttu-id="42f02-104">RDP를 사용하면 가상 머신의 운영 체제 및 소프트웨어를 조작할 수 있고 포털을 사용하면 가상 하드웨어 및 연결을 구성할 수 있다는 것을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-104">You learned that while RDP allows us to interact with the operating system and software of the virtual machine, the portal allows us to configure the virtual hardware and connectivity.</span></span> <span data-ttu-id="42f02-105">명령줄이나 스크립트 가능 환경을 선호하는 경우 PowerShell 또는 Azure CLI를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-105">We also could have used PowerShell or the Azure CLI, if a command-line or scriptable environment were preferred.</span></span>

## <a name="clean-up-the-resources"></a><span data-ttu-id="42f02-106">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="42f02-106">Clean up the resources</span></span>

<span data-ttu-id="42f02-107">VM이 실행되는 동안 VM 요금이 청구되고, 사용량에 따라 저장소 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-107">You are charged for VMs while they run, and for the storage based on how much you use.</span></span> <span data-ttu-id="42f02-108">VM을 사용하지 않을 때에는 항상 VM을 중지하고 할당을 취소해야 하며, 더 이상 리소스가 필요 없으면 리소스를 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-108">Always stop and deallocate VMs when you aren't using them, and when you no longer need the resources it's a good idea to delete them.</span></span> <span data-ttu-id="42f02-109">생성한 모든 리소스를 제거하려면 하나씩 삭제하거나 리소스 그룹을 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-109">To remove all the resources that you created, you can delete them one-by-one, or just delete the resource group.</span></span>

1. <span data-ttu-id="42f02-110">Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-110">Sign in to the Azure portal.</span></span>

1. <span data-ttu-id="42f02-111">왼쪽 메뉴에서 **모든 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-111">On the left menu, select **All Services**.</span></span>

1. <span data-ttu-id="42f02-112">**리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-112">Select **Resource Groups**.</span></span>

1. <span data-ttu-id="42f02-113">첫 번째 연습에서 만든 리소스 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-113">Find the resource group that you created in the first exercise.</span></span> <span data-ttu-id="42f02-114">목록 보기 오른쪽에 있는 줄임표(...)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-114">Click the ellipsis (...) on the right side of the list view.</span></span>

1. <span data-ttu-id="42f02-115">**리소스 그룹 삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-115">Select **Delete resource group**.</span></span>

1. <span data-ttu-id="42f02-116">다음 화면에서 리소스 그룹 이름을 입력하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-116">On the next screen, enter the resource group name to confirm the deletion.</span></span>

1. <span data-ttu-id="42f02-117">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f02-117">Click **Delete**.</span></span>