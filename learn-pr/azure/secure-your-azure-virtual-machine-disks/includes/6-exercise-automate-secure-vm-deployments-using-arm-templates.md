<span data-ttu-id="fa8ac-101">매우 중요한 고객 정보를 처리하는 금융 업체에서 VM 디스크 배포를 비롯하여 디스크를 항상 암호화된 상태로 유지하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-101">Your banking company handles highly sensitive customer information and wants you to ensure your disks are encrypted at all times, including VM disk deployment.</span></span> <span data-ttu-id="fa8ac-102">이를 위해 회사 데이터를 보호하기 위한 보안 VM 배포를 자동화하는 작업을 맡게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-102">You've been tasked to automate a secure VM deployment to safeguard your company's data.</span></span>

<span data-ttu-id="fa8ac-103">이 단원에서는 ARM 템플릿을 사용하여 새 Windows VM에 대해 암호화를 자동으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-103">In this unit, you'll use an ARM template to automatically enable encryption for new Windows VMs.</span></span>

## <a name="configure-and-deploy-a-new-vm-using-an-arm-template"></a><span data-ttu-id="fa8ac-104">ARM 템플릿을 사용하여 새 VM 배포 및 구성</span><span class="sxs-lookup"><span data-stu-id="fa8ac-104">Configure and deploy a new VM using an ARM template</span></span>

1. <span data-ttu-id="fa8ac-105">[GitHub의 Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)으로 이동한 다음 **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-105">Go to the [Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image), and then click **Deploy to Azure**.</span></span>
1. <span data-ttu-id="fa8ac-106">Azure Portal의 **Azure 빠른 시작 템플릿** 블레이드 아래 **리소스 그룹**에서 **기존 항목 사용**을 선택한 다음 목록에서 **moneyapprg**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-106">In the Azure portal, on the **Azure quickstart template** blade, under **Resource Group**, select **Use existing**, and in the list, select **moneyapprg**.</span></span>
1. <span data-ttu-id="fa8ac-107">**설정** 섹션에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-107">In the **SETTINGS** section, enter the following information:</span></span>

   - <span data-ttu-id="fa8ac-108">VM 이름: **moneyappsvr02**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-108">Vm Name: **moneyappsvr02**</span></span>
   - <span data-ttu-id="fa8ac-109">**관리자 사용자 이름**: 이전 연습에서 사용한 것과 같은 이름</span><span class="sxs-lookup"><span data-stu-id="fa8ac-109">**Admin Username**: same as you used in the previous exercise</span></span>
   - <span data-ttu-id="fa8ac-110">**관리자 암호**: 이전 연습에서 사용한 것과 같은 암호</span><span class="sxs-lookup"><span data-stu-id="fa8ac-110">**Admin Password**: same as you used in the previous exercise</span></span>
   - <span data-ttu-id="fa8ac-111">**새 저장소 계정 이름**: 고유한 이름 입력</span><span class="sxs-lookup"><span data-stu-id="fa8ac-111">**New Storage Account Name**: enter a unique name</span></span>
   - <span data-ttu-id="fa8ac-112">**VM 크기**: **Standard_B1s**와 같이 이전 연습에서 사용한 것과 같은 크기로 바꾸기(동일 Azure 지역을 사용하므로 현재 지역에서 해당 크기를 사용할 수 있는지 확인해야 함)</span><span class="sxs-lookup"><span data-stu-id="fa8ac-112">**Vm Size**: replace with the same size that you used in the previous exercise, such as **Standard_B1s** (as you are using the same Azure region, ensuring that size is available in your current region)</span></span>
   - <span data-ttu-id="fa8ac-113">**가상 네트워크 이름**: **moneyapprg vnet**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-113">**Virtual Network Name**: **moneyapprg-vnet**</span></span>
   - <span data-ttu-id="fa8ac-114">**서브넷 이름**: **default**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-114">**Subnet Name**: **default**</span></span>
   - <span data-ttu-id="fa8ac-115">**AAD 클라이언트 ID**: 메모장에 붙여넣은 정보에서 복사</span><span class="sxs-lookup"><span data-stu-id="fa8ac-115">**AAD Client Id**: copy from the information you pasted to Notepad</span></span>
   - <span data-ttu-id="fa8ac-116">**AAD 클라이언트 암호**: 메모장에 붙여넣은 정보에서 복사</span><span class="sxs-lookup"><span data-stu-id="fa8ac-116">**AAD Client Secret**: copy from the information you pasted to Notepad</span></span>
   - <span data-ttu-id="fa8ac-117">**Key Vault 이름**: **moneyappkv**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-117">**Key Vault Name**: **moneyappkv**</span></span>
   - <span data-ttu-id="fa8ac-118">**Key Vault 리소스 그룹**: **moneyapprg**</span><span class="sxs-lookup"><span data-stu-id="fa8ac-118">**Key Vault Resource Group**: **moneyapprg**</span></span>
   - <span data-ttu-id="fa8ac-119">**키 암호화 키 URL**: 메모장에 붙여넣은 정보에서 복사</span><span class="sxs-lookup"><span data-stu-id="fa8ac-119">**Key Encryption Key URL**: copy from the information you pasted to Notepad</span></span>
   - <span data-ttu-id="fa8ac-120">**사용 약관에 동의함** 확인란을 선택한 다음 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-120">Select the **I agree to the terms and conditions** check box, and then click **Purchase**.</span></span>
1. <span data-ttu-id="fa8ac-121">배포가 완료되려면 5~10분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-121">The deployment may take 5 - 10 minutes to complete.</span></span>

## <a name="verify-encryption-status-of-new-vm"></a><span data-ttu-id="fa8ac-122">새 VM의 암호화 상태 확인</span><span class="sxs-lookup"><span data-stu-id="fa8ac-122">Verify encryption status of new VM</span></span>

1. <span data-ttu-id="fa8ac-123">Azure Portal의 사이드바에서 **가상 머신**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-123">In the sidebar of the Azure portal, click **Virtual machines**.</span></span>

1. <span data-ttu-id="fa8ac-124">**가상 머신** 블레이드에서 **moneyappsvr02**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-124">On the **Virtual machines** blade, click **moneyappsvr02**.</span></span>

1. <span data-ttu-id="fa8ac-125">**가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-125">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="fa8ac-126">**디스크** 블레이드에서 OS 디스크 암호화 상태가 **사용**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa8ac-126">On the **Disks** blade, notice the OS disk encryption status is **Enabled**.</span></span>
