<span data-ttu-id="33890-101">First Up Consultants의 Alain이라는 동료가 현재 진행 중인 프로젝트를 위한 가상 머신을 만들고 관리할 수 있는 기능을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-101">A co-worker named Alain at First Up Consultants needs the ability to create and manage virtual machines for a project he is working on.</span></span> <span data-ttu-id="33890-102">관리자가 귀하에게 이 요청을 처리해 달라고 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="33890-102">Your manager has asked that you handle this request.</span></span> <span data-ttu-id="33890-103">모범 사례를 사용 하 여 작업을 완료 하려면 최소한의 권한을 사용자에 게 부여를 Alain 리소스 그룹에 대 한 Virtual Machine 참여자 역할을 할당 하려면 하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33890-103">Using the best practice to grant users the least privileges to get their work done, you decide to assign Alain the Virtual Machine Contributor role for a resource group.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="33890-104">Azure Portal에 로그인</span><span class="sxs-lookup"><span data-stu-id="33890-104">Sign in to the Azure portal</span></span>

- <span data-ttu-id="33890-105">Azure Portal에 여전히 **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**으로 로그인되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-105">Make sure you are still signed in to the Azure portal as **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**.</span></span> <span data-ttu-id="33890-106">이 창의 상단에 있는 **리소스** 탭에서 사용자 이름과 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33890-106">You can find the username and password on the **Resources** tab at the top of this window.</span></span>

## <a name="grant-access"></a><span data-ttu-id="33890-107">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="33890-107">Grant access</span></span>

<span data-ttu-id="33890-108">리소스 그룹 범위에서 사용자에게 Virtual Machine 기여자 역할을 할당하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="33890-108">Follow these steps to assign the Virtual Machine Contributor role to a user at the resource group scope.</span></span>

1. <span data-ttu-id="33890-109">탐색 목록에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-109">In the navigation list, click **Resource groups**.</span></span>

1. <span data-ttu-id="33890-110">**FirstUpConsultantsRG1-_XXXXXXX_** 리소스 그룹을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-110">Find and click the **FirstUpConsultantsRG1-_XXXXXXX_** resource group.</span></span>

1. <span data-ttu-id="33890-111">**액세스 제어(IAM)** 를 클릭하면 현재 역할 할당 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33890-111">Click **Access control (IAM)** to see the current list of role assignments.</span></span>

   ![액세스 제어-리소스 그룹에 대 한 역할 할당](../media/5-resource-group-role-assignment.png)

1. <span data-ttu-id="33890-113">상단에서 **추가**를 클릭하여 **권한 추가** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33890-113">At the top, click **Add** to open the **Add permissions** pane.</span></span>

   ![권한 추가 창](../media/5-add-permissions.png)

1. <span data-ttu-id="33890-115">**역할** 드롭다운 목록에서 **Virtual Machine 기여자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-115">In the **Role** drop-down list, select **Virtual Machine Contributor**.</span></span>

1. <span data-ttu-id="33890-116">**선택** 목록에서 **LabUser-_XXXXXXX_** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-116">In the **Select** list, select **LabUser-_XXXXXXX_**.</span></span>

   ![완성된 권한 추가 창](../media/5-add-permissions-save.png)

1. <span data-ttu-id="33890-118">**저장**을 클릭하여 역할 할당을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33890-118">Click **Save** to create the role assignment.</span></span>

   <span data-ttu-id="33890-119">잠시 후 **LabUser-_XXXXXXX_** 사용자에게 **FirstUpConsultantsRG1-_XXXXXXX_** 리소스 그룹 범위의 Virtual Machine 기여자 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="33890-119">After a few moments, the **LabUser-_XXXXXXX_** user is assigned the Virtual Machine Contributor role at the **FirstUpConsultantsRG1-_XXXXXXX_** resource group scope.</span></span> <span data-ttu-id="33890-120">이제 사용자는 이 리소스 그룹 내에서만 가상 머신을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33890-120">The user can now create and manage virtual machines just within this resource group.</span></span>

   ![Virtual Machine 기여자 역할 할당](../media/5-vm-contributor-assignment.png)

## <a name="remove-access"></a><span data-ttu-id="33890-122">액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="33890-122">Remove access</span></span>

<span data-ttu-id="33890-123">RBAC에서 액세스 권한을 제거하려면 역할 할당을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-123">In RBAC, to remove access, you remove a role assignment.</span></span>

1. <span data-ttu-id="33890-124">역할 할당 목록에서 Virtual Machine 기여자 역할이 할당된 **LabUser-_XXXXXXX_** 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-124">In the list of role assignments, select the **LabUser-_XXXXXXX_** user with the Virtual Machine Contributor role.</span></span>

1. <span data-ttu-id="33890-125">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-125">Click **Remove**.</span></span>

   ![역할 할당 제거 메시지](../media/5-remove-role-assignment.png)

1. <span data-ttu-id="33890-127">**표시되는 역할 할당 제거** 메시지에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33890-127">In the **Remove role assignments** message that appears, click **Yes**.</span></span>

## <a name="summary"></a><span data-ttu-id="33890-128">요약</span><span class="sxs-lookup"><span data-stu-id="33890-128">Summary</span></span>

<span data-ttu-id="33890-129">이 단원에서는 Azure Portal을 사용하여 리소스 그룹에 가상 머신을 만들고 관리할 수 있는 액세스 권한을 사용자에게 부여하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="33890-129">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using the Azure portal.</span></span> <span data-ttu-id="33890-130">다음 단원에서는 시간별 RBAC 변경 사항을 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33890-130">In the next unit, you learn how to view the RBAC changes over time.</span></span>
