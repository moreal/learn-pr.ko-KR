<span data-ttu-id="aa05c-101">귀하는 Azure Portal에서 **IAM(액세스 제어)** 블레이드를 문제 없이 사용해 왔지만 매일 여러 건의 권한 요청을 받고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-101">Using the **Access control (IAM)** blade in the Azure portal has been working fine, but you are getting several permission requests each day.</span></span> <span data-ttu-id="aa05c-102">액세스 관리 작업을 처리하기 위해 PowerShell을 사용하여 일부 단계를 자동화하기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-102">To keep up with the access management tasks, you decide to use PowerShell to help automate some of the steps.</span></span>

## <a name="open-cloud-shell-powershell"></a><span data-ttu-id="aa05c-103">Cloud Shell PowerShell 열기</span><span class="sxs-lookup"><span data-stu-id="aa05c-103">Open Cloud Shell PowerShell</span></span>

1. <span data-ttu-id="aa05c-104">Azure Portal에 여전히 **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**으로 로그인되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-104">Make sure you are still signed in to the Azure portal as **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**.</span></span> <span data-ttu-id="aa05c-105">이 창의 상단에 있는 **리소스** 탭에서 사용자 이름과 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-105">You can find the username and password on the **Resources** tab at the top of this window.</span></span>

1. <span data-ttu-id="aa05c-106">포털 상단에서 **Cloud Shell**을 클릭하여 Cloud Shell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-106">At the top of the portal, click **Cloud Shell** to open the Cloud Shell pane.</span></span>

    ![Cloud Shell 단추](../media-draft/6-cloud-shell-button.png)

1. <span data-ttu-id="aa05c-108">Cloud Shell 창 왼쪽 상단에서 **PowerShell**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-108">In the upper left of the Cloud Shell pane, make sure it is set to **PowerShell**.</span></span> <span data-ttu-id="aa05c-109">**Bash**로 설정된 경우 **PowerShell**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-109">If it is set to **Bash**, change it to **PowerShell**.</span></span>

    <span data-ttu-id="aa05c-110">로드하는 데 잠시 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-110">It might take a few moments to load.</span></span> <span data-ttu-id="aa05c-111">완료되면 다음과 비슷한 모습이 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-111">When finished, it will look similar to the following:</span></span>

    ![Cloud Shell PowerShell](../media-draft/6-cloud-shell-powershell.png)

## <a name="grant-access"></a><span data-ttu-id="aa05c-113">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="aa05c-113">Grant access</span></span>

<span data-ttu-id="aa05c-114">Azure PowerShell을 사용하여 사용자에게 액세스 권한을 부여하려면 [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-114">To grant access to a user using Azure PowerShell, you use the [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) command.</span></span> <span data-ttu-id="aa05c-115">보안 주체, 역할 정의 및 범위를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-115">You must specify the security principal, role definition, and scope.</span></span>

<span data-ttu-id="aa05c-116">리소스 그룹 범위에서 **LabUser-_XXXXXXX_** 사용자에게 Virtual Machine 기여자 역할을 할당하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aa05c-116">Follow these steps to assign the Virtual Machine Contributor role to the **LabUser-_XXXXXXX_** user at the resource group scope.</span></span>

1. <span data-ttu-id="aa05c-117">이 창의 상단에 있는 **리소스** 탭에서 **PowerShell에 액세스 권한 부여** 명령을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-117">On the **Resources** tab at the top of this window, copy the **Grant access PowerShell** command.</span></span>

1. <span data-ttu-id="aa05c-118">PowerShell 창에 명령을 붙여넣고 Enter 키를 눌러 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-118">Paste the command into the PowerShell pane and press the Enter key to run it.</span></span> <span data-ttu-id="aa05c-119">다음은 명령 예제와 출력을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-119">The following shows an example command and the output:</span></span>

    ```Example
    PS Azure:\> New-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"

    RoleAssignmentId   : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX/providers/Microsoft.Authorization/roleAssignments/33333333-3333-3333-3333-333333333333
    Scope              : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX
    DisplayName        : LabUser-XXXXXXX
    SignInName         : LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com
    RoleDefinitionName : Virtual Machine Contributor
    RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
    ObjectId           : 11111111-1111-1111-1111-111111111111
    ObjectType         : User
    CanDelegate        : False
    ```

    <span data-ttu-id="aa05c-120">이 출력은 Virtual Machine 기여자 역할이 FirstUpConsultantsRG1-_XXXXXXX_ 범위의 LabUser-_XXXXXXX_에게 할당되었음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-120">The output shows that the Virtual Machine Contributor role has been assigned to LabUser-_XXXXXXX_ at the FirstUpConsultantsRG1-_XXXXXXX_ scope.</span></span>

## <a name="list-access"></a><span data-ttu-id="aa05c-121">액세스 권한 나열</span><span class="sxs-lookup"><span data-stu-id="aa05c-121">List access</span></span>

<span data-ttu-id="aa05c-122">리소스 그룹에 대한 액세스 권한을 확인하려면 [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment) 명령을 사용하여 역할 할당을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-122">To verify the access for the resource group, you use the [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment) command to list the role assignments.</span></span>

<span data-ttu-id="aa05c-123">리소스 그룹 범위에서 **LabUser-XXXXXXX** 사용자에게 할당된 모든 역할을 나열하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aa05c-123">Follow these steps to list all the role assignments for the **LabUser-XXXXXXX** user at the resource group scope.</span></span>

1. <span data-ttu-id="aa05c-124">이 창의 상단에 있는 **리소스** 탭에서 **PowerShell 액세스 권한 나열** 명령을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-124">On the **Resources** tab at the top of this window, copy the **List access PowerShell** command.</span></span>

1. <span data-ttu-id="aa05c-125">PowerShell 창에 명령을 붙여넣고 Enter 키를 눌러 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-125">Paste the command into the PowerShell pane and press the Enter key to run it.</span></span> <span data-ttu-id="aa05c-126">다음은 명령 예제와 출력을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-126">The following shows an example command and the output.</span></span>

    ```Example
    PS Azure:\> Get-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"

    RoleAssignmentId   : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX/providers/Microsoft.Authorization/roleAssignments/33333333-3333-3333-3333-333333333333
    Scope              : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX
    DisplayName        : LabUser-XXXXXXX
    SignInName         : LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com 
    RoleDefinitionName : Virtual Machine Contributor
    RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
    ObjectId           : 11111111-1111-1111-1111-111111111111
    ObjectType         : User
    CanDelegate        : False
    ```

    <span data-ttu-id="aa05c-127">이 출력은 Virtual Machine 기여자 역할이 FirstUpConsultantsRG1-_XXXXXXX_ 범위의 LabUser-_XXXXXXX_에게 할당되었음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-127">The output shows that the Virtual Machine Contributor role has been assigned to LabUser-_XXXXXXX_ at the FirstUpConsultantsRG1-_XXXXXXX_ scope.</span></span>

    <span data-ttu-id="aa05c-128">Azure Portal에서 리소스 그룹의 **IAM(액세스 제어)** 블레이드를 새로 고치면 다음과 같이 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-128">If you refresh the **Access control (IAM)** blade for the resource group in the Azure portal, this is how the role assignment looks:</span></span>

    ![리소스 그룹에서 사용자의 역할 할당](../media-draft/6-cloud-shell-access-control.png)

## <a name="remove-access"></a><span data-ttu-id="aa05c-130">액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="aa05c-130">Remove access</span></span>

<span data-ttu-id="aa05c-131">사용자, 그룹 및 응용 프로그램의 액세스 권한을 제거하려면 [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment) 명령을 사용하여 역할 할당을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-131">To remove access for users, groups, and applications, you use [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment) to remove a role assignment.</span></span>

<span data-ttu-id="aa05c-132">리소스 그룹 범위에서 **LabUser-_XXXXXX_** 사용자에게 할당된 Virtual Machine 기여자 역할을 제거하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aa05c-132">Follow these steps to remove the Virtual Machine Contributor role assignment for the **LabUser-_XXXXXX_** user at the resource group scope.</span></span>

1. <span data-ttu-id="aa05c-133">이 창의 상단에 있는 **리소스** 탭에서 **PowerShell 액세스 권한 제거** 명령을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-133">On the **Resources** tab at the top of this window, copy the **Remove access PowerShell** command.</span></span>

1. <span data-ttu-id="aa05c-134">PowerShell 창에 명령을 붙여넣고 Enter 키를 눌러 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-134">Paste the command into the PowerShell pane and press the Enter key to run it.</span></span> <span data-ttu-id="aa05c-135">다음은 예제 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-135">The following shows an example command.</span></span>

    ```Example
    PS Azure:\> Remove-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"
    ```

1. <span data-ttu-id="aa05c-136">PowerShell 창에서 닫기(**X**) 단추를 클릭하여 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-136">In the PowerShell pane, click the close (**X**) button to close the pane.</span></span>

    ![Cloud Shell 닫기 단추](../media-draft/6-cloud-shell-close.png)


## <a name="summary"></a><span data-ttu-id="aa05c-138">요약</span><span class="sxs-lookup"><span data-stu-id="aa05c-138">Summary</span></span>

<span data-ttu-id="aa05c-139">이 단원에서는 Azure PowerShell을 사용하여 리소스 그룹에 가상 머신을 만들고 관리할 수 있는 액세스 권한을 사용자에게 부여하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-139">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using Azure PowerShell.</span></span> <span data-ttu-id="aa05c-140">다음 단원에서는 시간별 RBAC 변경 사항을 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aa05c-140">In the next unit, you learn how to view the RBAC changes over time.</span></span>
