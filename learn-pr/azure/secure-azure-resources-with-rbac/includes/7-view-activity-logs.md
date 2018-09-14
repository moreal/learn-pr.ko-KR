<span data-ttu-id="5aa33-101">First Up Consultants에서는 감사 및 문제 해결을 위해 RBAC(역할 기반 액세스 제어) 변경 사항을 분기별로 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-101">First Up Consultants reviews role-based access control (RBAC) changes quarterly for auditing and troubleshooting purposes.</span></span> <span data-ttu-id="5aa33-102">아시다시피 변경 사항은 [Azure 활동 로그](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)에 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-102">You know that changes get logged in [Azure Activity Log](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</span></span> <span data-ttu-id="5aa33-103">관리자가 귀하에게 지난달의 역할 할당 및 사용자 지정 역할 변경 사항에 대한 보고서를 생성해 줄 수 있는지 물었습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-103">Your manager has asked if you can generate a report of the role assignment and custom role changes for the last month.</span></span>

## <a name="view-activity-logs"></a><span data-ttu-id="5aa33-104">활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="5aa33-104">View activity logs</span></span>

<span data-ttu-id="5aa33-105">가장 손쉽게 시작할 수 있는 방법은 Azure Portal을 사용하여 활동 로그를 보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-105">The easiest way to get started is to view the activity logs with the Azure portal.</span></span>

1. <span data-ttu-id="5aa33-106">**모든 서비스**를 클릭한 다음, **활동 로그**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-106">Click **All services** and then find **Activity log**.</span></span>

    ![포털을 사용한 활동 로그](../media-draft/7-all-services-activity-log.png)

1. <span data-ttu-id="5aa33-108">**활동 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-108">Click **Activity log**.</span></span>

    ![포털을 사용한 활동 로그](../media-draft/7-activity-log-portal.png)

1. <span data-ttu-id="5aa33-110">**시간 간격** 필터를 **지난달**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-110">Set the **Timespan** filter to **Last month**.</span></span>

1. <span data-ttu-id="5aa33-111">**이벤트 범주** 필터를 **관리**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-111">Set the **Event category** filter to **Administrative**.</span></span>

1. <span data-ttu-id="5aa33-112">**작업** 필터에서 **역할**을 입력하여 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-112">In the **Operation** filter, type **role** to filter the list.</span></span>

1. <span data-ttu-id="5aa33-113">다음 RBAC 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-113">Select the following RBAC operations:</span></span>

    - <span data-ttu-id="5aa33-114">역할 할당 만들기(roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="5aa33-114">Create role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="5aa33-115">역할 할당 삭제(roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="5aa33-115">Delete role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="5aa33-116">사용자 지정 역할 정의 만들기 또는 업데이트(roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="5aa33-116">Create or update custom role definition (roleDefinitions)</span></span>
    - <span data-ttu-id="5aa33-117">사용자 지정 역할 정의 삭제(roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="5aa33-117">Delete custom role definition (roleDefinitions)</span></span>

    ![작업 필터](../media-draft/7-operation-filter.png)

1. <span data-ttu-id="5aa33-119">**적용**을 클릭하여 필터를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-119">Click **Apply** to apply your filters.</span></span>

    <span data-ttu-id="5aa33-120">지난달의 모든 역할 할당 및 역할 정의 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-120">You'll see all the role assignment and role definition operations for the last month.</span></span> <span data-ttu-id="5aa33-121">또한 활동 로그를 CSV 파일로 다운로드하는 링크도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-121">It also includes a link to download the activity log as a CSV file.</span></span>

    ![RBAC 활동 로그](../media-draft/7-activity-log-portal-filter.png)

## <a name="end-lab"></a><span data-ttu-id="5aa33-123">랩 종료</span><span class="sxs-lookup"><span data-stu-id="5aa33-123">End lab</span></span>

1. <span data-ttu-id="5aa33-124">랩을 종료하려면 이 창의 오른쪽 위 모서리에 있는 햄버거 메뉴를 클릭한 다음, **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-124">To end the lab, click the hamburger menu in the upper-right corner of this window and then click **End**.</span></span>

1. <span data-ttu-id="5aa33-125">**예, 랩을 종료합니다**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-125">Click **Yes, end my lab**.</span></span>

## <a name="summary"></a><span data-ttu-id="5aa33-126">요약</span><span class="sxs-lookup"><span data-stu-id="5aa33-126">Summary</span></span>

<span data-ttu-id="5aa33-127">이 단원에서는 Azure 활동 로그를 사용하여 포털의 RBAC 변경 사항을 나열하고 간단한 보고서를 생성하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa33-127">In this unit, you learned how to use Azure Activity Log to list RBAC changes in the portal and generate a simple report.</span></span>
