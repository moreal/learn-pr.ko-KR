<span data-ttu-id="96bc5-101">매우 중요한 고객 정보를 처리하는 금융 업체에서 VM 디스크 배포를 비롯하여 디스크를 항상 암호화된 상태로 유지하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-101">Your banking company handles highly sensitive customer information and wants you to ensure your disks are encrypted at all times, including VM disk deployment.</span></span> <span data-ttu-id="96bc5-102">이를 위해 회사 데이터를 보호하기 위한 보안 VM 배포를 자동화하는 작업을 맡게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-102">You've been tasked to automate a secure VM deployment to safeguard your company's data.</span></span>

<span data-ttu-id="96bc5-103">이 단원에서는 Azure Resource Manager 템플릿을 사용하여 새 Windows VM에 대한 암호화를 자동으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-103">In this unit, you'll use an Azure Resource Manager template to automatically enable encryption for new Windows VMs.</span></span>

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a><span data-ttu-id="96bc5-104">Azure Resource Manager 템플릿을 사용하여 새 VM 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="96bc5-104">Configure and deploy a new VM using an Azure Resource Manager template</span></span>

1. <span data-ttu-id="96bc5-105">[GitHub의 Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)으로 이동한 다음, **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-105">Go to the [Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image), and then click **Deploy to Azure**.</span></span>
1. <span data-ttu-id="96bc5-106">Azure Portal의 **Azure 빠른 시작 템플릿** 블레이드에서 **리소스 그룹** 아래의 **기존 항목 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-106">In the Azure portal, on the **Azure quickstart template** blade, under **Resource Group**, select **Use existing**.</span></span> <span data-ttu-id="96bc5-107">목록에서 **moneyapprg**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-107">In the list, select **moneyapprg**.</span></span>
1. <span data-ttu-id="96bc5-108">**설정** 섹션에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-108">In the **SETTINGS** section, enter the following information:</span></span>

   - <span data-ttu-id="96bc5-109">VM 이름: **moneyappsvr02**</span><span class="sxs-lookup"><span data-stu-id="96bc5-109">Vm Name: **moneyappsvr02**</span></span>
   - <span data-ttu-id="96bc5-110">**관리자 사용자 이름**: 이전 연습에서 사용한 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-110">**Admin Username**: Same as you used in the previous exercise.</span></span>
   - <span data-ttu-id="96bc5-111">**관리자 암호**: 이전 연습에서 사용한 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-111">**Admin Password**: Same as you used in the previous exercise.</span></span>
   - <span data-ttu-id="96bc5-112">**새 저장소 계정 이름**: 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-112">**New Storage Account Name**: Enter a unique name.</span></span>
   - <span data-ttu-id="96bc5-113">**VM 크기**: **Standard_B1s**와 같이 이전 연습에서 사용한 것과 같은 크기로 바꿉니다(동일한 Azure 지역을 사용하므로 현재 지역에서 해당 크기를 사용할 수 있는지 확인해야 함).</span><span class="sxs-lookup"><span data-stu-id="96bc5-113">**Vm Size**: Replace with the same size that you used in the previous exercise, such as **Standard_B1s** (as you are using the same Azure region, ensuring that size is available in your current region).</span></span>
   - <span data-ttu-id="96bc5-114">**가상 네트워크 이름**: **moneyapprg-vnet**</span><span class="sxs-lookup"><span data-stu-id="96bc5-114">**Virtual Network Name**: **moneyapprg-vnet**</span></span>
   - <span data-ttu-id="96bc5-115">**서브넷 이름**: **default**</span><span class="sxs-lookup"><span data-stu-id="96bc5-115">**Subnet Name**: **default**</span></span>
   - <span data-ttu-id="96bc5-116">**AAD 클라이언트 ID**: 메모장에 붙여넣은 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-116">**AAD Client ID**: Copy from the information you pasted to Notepad.</span></span>
   - <span data-ttu-id="96bc5-117">**AAD 클라이언트 비밀**: 메모장에 붙여넣은 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-117">**AAD Client Secret**: Copy from the information you pasted to Notepad.</span></span>
   - <span data-ttu-id="96bc5-118">**Key Vault 이름**: **moneyappkv**</span><span class="sxs-lookup"><span data-stu-id="96bc5-118">**Key Vault Name**: **moneyappkv**</span></span>
   - <span data-ttu-id="96bc5-119">**Key Vault 리소스 그룹**: **moneyapprg**</span><span class="sxs-lookup"><span data-stu-id="96bc5-119">**Key Vault Resource Group**: **moneyapprg**</span></span>
   - <span data-ttu-id="96bc5-120">**키 암호화 키 URL**: 메모장에 붙여넣은 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-120">**Key Encryption Key URL**: Copy from the information you pasted to Notepad.</span></span>
1. <span data-ttu-id="96bc5-121">**사용 약관에 동의함** 확인란을 선택한 다음, **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-121">Select the **I agree to the terms and conditions** check box, and then click **Purchase**.</span></span>

<span data-ttu-id="96bc5-122">배포가 완료되려면 5~10분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-122">The deployment may take 5-10 minutes to complete.</span></span>

## <a name="verify-encryption-status-of-new-vm"></a><span data-ttu-id="96bc5-123">새 VM의 암호화 상태 확인</span><span class="sxs-lookup"><span data-stu-id="96bc5-123">Verify encryption status of new VM</span></span>

1. <span data-ttu-id="96bc5-124">Azure Portal의 사이드바에서 **가상 머신**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-124">In the sidebar of the Azure portal, click **Virtual machines**.</span></span>

1. <span data-ttu-id="96bc5-125">**가상 머신** 블레이드에서 **moneyappsvr02**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-125">On the **Virtual machines** blade, click **moneyappsvr02**.</span></span>

1. <span data-ttu-id="96bc5-126">**가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-126">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="96bc5-127">**디스크** 블레이드에서 OS 디스크 암호화 상태가 **사용**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="96bc5-127">On the **Disks** blade, notice the OS disk encryption status is **Enabled**.</span></span>
