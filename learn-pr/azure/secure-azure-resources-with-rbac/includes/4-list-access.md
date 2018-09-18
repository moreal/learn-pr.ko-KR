<span data-ttu-id="e3a5a-101">귀하는 First Up Consultants에서 마케팅 팀의 Azure 구독 액세스 권한을 부여받았습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-101">At First Up Consultants, you've been granted access to the Azure subscription for the marketing team.</span></span> <span data-ttu-id="e3a5a-102">귀하는 Azure Portal 사용법을 숙지하고 현재 할당된 역할을 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-102">You want to familiarize yourself with the Azure portal and see what roles are currently assigned.</span></span>

## <a name="list-role-assignments-for-yourself"></a><span data-ttu-id="e3a5a-103">사용자에 대한 역할 할당 목록</span><span class="sxs-lookup"><span data-stu-id="e3a5a-103">List role assignments for yourself</span></span>

<span data-ttu-id="e3a5a-104">현재 사용자에게 할당된 역할을 확인하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-104">Follow these steps to see what roles are currently assigned to you.</span></span>

1. <span data-ttu-id="e3a5a-105">[Azure Portal](https://portal.azure.com/?azure-portal=true)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-105">Navigate to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="e3a5a-106">탐색 목록에서 **Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-106">In the navigation list, click **Azure Active Directory**.</span></span>

1. <span data-ttu-id="e3a5a-107">**사용자**를 클릭하여 **모든 사용자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-107">Click **Users** to open **All users**.</span></span>

    ![Azure Active Directory 사용자](../media-draft/4-aad-all-users.png)

1. <span data-ttu-id="e3a5a-109">**LabAdmin-_XXXXXXX_** 사용자 이름을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-109">Find and click the **LabAdmin-_XXXXXXX_** user name.</span></span>

    ![Azure Active Directory 랩 사용자](../media-draft/4-aad-all-users-lab.png)

1. <span data-ttu-id="e3a5a-111">**관리** 섹션에서 **Azure 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-111">In the **Manage** section, click **Azure resources**.</span></span>

    ![Azure 리소스](../media-draft/4-aad-user-azure-resources.png)

    <span data-ttu-id="e3a5a-113">Azure 리소스 블레이드에서 액세스 가능한 리소스와 역할을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-113">On the Azure resources blade, you can see the resources and roles you have access to.</span></span> <span data-ttu-id="e3a5a-114">목록은 사용자별로 다르게 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-114">Your list will look different.</span></span>

## <a name="list-role-assignments-for-a-resource-group"></a><span data-ttu-id="e3a5a-115">리소스 그룹에 대한 역할 할당 목록</span><span class="sxs-lookup"><span data-stu-id="e3a5a-115">List role assignments for a resource group</span></span>

<span data-ttu-id="e3a5a-116">리소스 그룹 범위에서 할당된 역할을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-116">Follow these steps to see what roles are assigned at the resource group scope.</span></span>

1. <span data-ttu-id="e3a5a-117">탐색 목록에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-117">In the navigation list, click **Resource groups**.</span></span>

   ![리소스 그룹](../media-draft/4-resource-groups.png)

1. <span data-ttu-id="e3a5a-119">**FirstUpConsultantsRG1-_XXXXXXX_** 라는 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-119">Click the resource group named **FirstUpConsultantsRG1-_XXXXXXX_**.</span></span>

1. <span data-ttu-id="e3a5a-120">**액세스 제어(IAM)** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-120">Click **Access control (IAM)**.</span></span>

   <span data-ttu-id="e3a5a-121">액세스 제어(IAM) 블레이드에서 이 리소스 그룹에 대한 액세스 권한이 있는 사용자를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-121">On the Access control (IAM) blade, you can see who has access to this resource group.</span></span> <span data-ttu-id="e3a5a-122">일부 역할의 범위는 **이 리소스**이지만 나머지는 부모 범위에서 **(상속)** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-122">Notice that some roles are scoped to **This resource** while others are **(Inherited)** from a parent scope.</span></span>

   ![리소스 그룹의 액세스 제어(IAM)](../media-draft/4-resource-group-access-control.png)

## <a name="list-roles"></a><span data-ttu-id="e3a5a-124">역할 나열</span><span class="sxs-lookup"><span data-stu-id="e3a5a-124">List roles</span></span>

<span data-ttu-id="e3a5a-125">이전 단원에서 살펴본 것처럼 역할은 권한 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-125">As you learned in the previous unit, a role is a collection of permissions.</span></span> <span data-ttu-id="e3a5a-126">Azure에는 역할 할당에 사용할 수 있는 기본 제공 역할이 70개 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-126">Azure has over 70 built-in roles that you can use in your role assignments.</span></span> <span data-ttu-id="e3a5a-127">역할을 나열하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-127">Follow these steps to list the roles.</span></span>

- <span data-ttu-id="e3a5a-128">액세스 제어(IAM) 블레이드 맨 위에 있는 **역할**을 클릭하여 모든 기본 제공 역할 및 사용자 지정 역할의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-128">At the top of the Access control (IAM) blade, click **Roles** to see a list of all the built-in and custom roles.</span></span>

   ![역할 옵션](../media-draft/4-roles-option.png)

   <span data-ttu-id="e3a5a-130">각 역할에 할당된 사용자 및 그룹 수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-130">You can see the number of users and groups that are assigned to each role.</span></span>

   ![역할 목록](../media-draft/4-roles-list.png)

## <a name="summary"></a><span data-ttu-id="e3a5a-132">요약</span><span class="sxs-lookup"><span data-stu-id="e3a5a-132">Summary</span></span>

<span data-ttu-id="e3a5a-133">이 단원에서는 Azure Portal에서 직접 역할 할당을 나열하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-133">In this unit, you learned how to list the role assignments for yourself in the Azure portal.</span></span> <span data-ttu-id="e3a5a-134">또한 서로 다른 범위에서 역할 할당을 나열하는 방법도 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-134">You also learned how to list the role assignments at different scopes.</span></span> <span data-ttu-id="e3a5a-135">다음 단원에서는 다음 단계로 가서 RBAC를 사용하여 사용자에게 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a5a-135">In the next unit, you take the next step and use RBAC to grant access to a user.</span></span>
