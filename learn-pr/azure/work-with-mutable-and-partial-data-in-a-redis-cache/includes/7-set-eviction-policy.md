<span data-ttu-id="67029-101">여기서는 Azure Redis Cache에 제거 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67029-101">Here you'll add an eviction policy to our Azure Redis Cache.</span></span>

## <a name="set-an-eviction-policy"></a><span data-ttu-id="67029-102">제거 정책 설정</span><span class="sxs-lookup"><span data-stu-id="67029-102">Set an eviction policy</span></span>

<span data-ttu-id="67029-103">Azure에서 제거 정책을 설정하려면 포털에서 간단히 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67029-103">To set an eviction policy in Azure, we simply use a drop-down menu in the portal.</span></span>

1. <span data-ttu-id="67029-104">Azure Portal에서 Redis Cache를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="67029-104">Open your Redis Cache in the Azure portal.</span></span>

1. <span data-ttu-id="67029-105">**고급 설정** 블레이드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67029-105">Select the **Advanced settings** blade.</span></span>

1. <span data-ttu-id="67029-106">**maxmemory-policy** 드롭다운 메뉴를 사용하여 **allkeys-random**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67029-106">Use the **maxmemory-policy** drop-down menu and select **allkeys-random**.</span></span>

1. <span data-ttu-id="67029-107">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67029-107">Click **Save**.</span></span> 

<span data-ttu-id="67029-108">이 시점에서 메모리가 부족하게 되면 Redis가 새 데이터를 위한 공간을 확보하기 위해 임의의 키를 선택하여 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="67029-108">At this point, if you run out of memory, Redis will select a random key to delete to make room for your new data.</span></span>