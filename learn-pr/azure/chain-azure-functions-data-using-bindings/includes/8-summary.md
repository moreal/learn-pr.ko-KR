<span data-ttu-id="4a04f-101">이 모듈은 모두 데이터와 서비스를 함수에 통합하는 것에 관한 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-101">This module was all about integrating data and services into your functions.</span></span> <span data-ttu-id="4a04f-102">함수에 추가할 때 표시되는 바인딩 형식에 대해 빠르게 둘러보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-102">We started off with a quick tour of the binding types that show up when you add them to a function.</span></span> <span data-ttu-id="4a04f-103">그런 다음, 입력 바인딩을 사용하여 Azure Cosmos DB에서 데이터를 읽는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-103">We then looked at reading data from an Azure Cosmos DB using an input binding.</span></span> <span data-ttu-id="4a04f-104">플랫폼은 연결 문자열 관리를 담당하며, 여기서는 바인딩을 사용하여 코드에서 데이터를 읽는 것이 얼마나 쉬운지를 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-104">The platform takes care of managing connection strings and we saw how easy it is to read data in our code using the binding.</span></span> <span data-ttu-id="4a04f-105">마지막으로, 출력 바인딩을 사용하여 다른 원본을 작성하는 데 집중했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-105">Finally we focused our attention on writing data different sources with the help of output bindings.</span></span> <span data-ttu-id="4a04f-106">이 과정은 다음 표에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-106">This journey is summarized in the following table.</span></span>

[!INCLUDE [summary table](./summary-table.md)]

<span data-ttu-id="4a04f-107">여기서 습득한 방법을 적용하여 함수에서 바인딩을 추가하고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-107">You can apply the approaches you have learned here to add and test bindings in your functions.</span></span> <span data-ttu-id="4a04f-108">바인딩을 사용하여 더 많이 연습하고 여기서 습득한 내용을 토대로 하는 몇 가지 흥미로운 아이디어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-108">Here are a few interesting ideas to get more practice with bindings and to build on what you have learned here.</span></span>

* <span data-ttu-id="4a04f-109">Blob Storage 및 이 모듈에서 사용하지 않은 다른 입력 바인딩에서 읽는 다른 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-109">Create another function to read from Blob Storage and other input bindings that we haven't used in this module.</span></span>

* <span data-ttu-id="4a04f-110">지원되는 다른 출력 바인딩 형식을 사용하여 더 많은 대상에 쓰는 다른 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-110">Create another function to write to more destinations using other supported output binding types.</span></span>

* <span data-ttu-id="4a04f-111">마지막 단원에서 큐를 도입하고, 출력 바인딩을 사용하여 메시지를 큐에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-111">In the last unit, we introduced a queue and posted messages to it with an output binding.</span></span> <span data-ttu-id="4a04f-112">다음 단계로, 큐에 있는 메시지를 읽고 `Console.Log()`를 사용하여 **메시지 텍스트**를 콘솔에 출력하는 다른 함수를 추가하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-112">As a next step, consider adding another function that reads the messages in the queue and prints out the **MESSAGE TEXT** to the console with `Console.Log()`.</span></span>

<span data-ttu-id="4a04f-113">이 모듈에서 보았듯이, Azure Portal에서는 함수를 작성하고 데이터와 다른 서비스에 연결하는 데 사용하기 쉬운 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-113">As we saw in this module, the Azure portal offers easy-to-use features to start building functions and connecting them to data and other services.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="4a04f-114">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="4a04f-114">Clean up resources</span></span>

<span data-ttu-id="4a04f-115">Azure에서 *리소스*는 함수 앱, 함수, 저장소 계정 등을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-115">*Resources* in Azure refers to function apps, functions, storage accounts, and so forth.</span></span> <span data-ttu-id="4a04f-116">리소스는 *리소스 그룹*으로 그룹화되며, 그룹을 삭제하여 그룹의 모든 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-116">They are grouped into *resource groups*, and you can delete everything in a group by deleting the group.</span></span>

<span data-ttu-id="4a04f-117">이 모듈을 완료하는 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-117">You created resources to complete this module.</span></span> <span data-ttu-id="4a04f-118">[계정 상태](https://azure.microsoft.com/account/) 및 [서비스 가격 책정](https://azure.microsoft.com/pricing/)에 따라 이러한 리소스에 대한 요금이 청구될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-118">You may be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/).</span></span> <span data-ttu-id="4a04f-119">리소스가 더 이상 필요하지 않게 되면 다음과 같이 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-119">If you don't need the resources anymore, here's how to delete them:</span></span>

1. <span data-ttu-id="4a04f-120">Azure Portal에서 **리소스 그룹** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-120">In the Azure portal, go to the **Resource group** page.</span></span>

   <span data-ttu-id="4a04f-121">함수 앱 페이지에서 해당 페이지로 이동하려면 **개요** 탭을 선택한 다음, **리소스 그룹** 아래의 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-121">To get to that page from the function app page, select the **Overview** tab and then select the link under **Resource group**.</span></span>

   <span data-ttu-id="4a04f-122">대시보드에서 해당 페이지로 이동하려면 **리소스 그룹**을 선택한 다음, 이 모듈에 사용한 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-122">To get to that page from the dashboard, select **Resource groups**, and then select the resource group that you used for this module.</span></span> 

> [!NOTE]
> <span data-ttu-id="4a04f-123">이 모듈에 대해 제안한 리소스 그룹의 기본 이름은 [!INCLUDE [resource-group-name](./rg-name.md)]이지만, 다른 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-123">The default name of the resource group we suggested for this module was [!INCLUDE [resource-group-name](./rg-name.md)] but it is possible that you used another name.</span></span>

2. <span data-ttu-id="4a04f-124">**리소스 그룹** 페이지에서 포함된 리소스 목록을 검토하고 삭제하려는 리소스인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-124">In the **Resource group** page, review the list of included resources, and verify that they are the ones you want to delete.</span></span>

3. <span data-ttu-id="4a04f-125">**리소스 그룹 삭제**를 선택하고 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-125">Select **Delete resource group**, and follow the instructions.</span></span>

   <span data-ttu-id="4a04f-126">삭제는 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-126">Deletion may take a couple of minutes.</span></span> <span data-ttu-id="4a04f-127">완료되면 알림이 잠시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-127">When it's done, a notification appears for a few seconds.</span></span> <span data-ttu-id="4a04f-128">또한 페이지 위쪽의 종 모양 아이콘을 선택하여 알림을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-128">You can also select the bell icon at the top of the page to view the notification.</span></span>

## <a name="further-reading"></a><span data-ttu-id="4a04f-129">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="4a04f-129">Further Reading</span></span>

<span data-ttu-id="4a04f-130">이 목록은 완전한 목록이 아니지만, 이 모듈에서 다루는 흥미로운 주제와 관련된 몇 가지 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a04f-130">While this is not intended to be an exhaustive list, the following are some resources related to the topics covered in this module that you might find interesting.</span></span>

 * [<span data-ttu-id="4a04f-131">Azure Functions 설명서</span><span class="sxs-lookup"><span data-stu-id="4a04f-131">Azure Functions documentation</span></span>](https://docs.microsoft.com/azure/azure-functions/)

* [<span data-ttu-id="4a04f-132">Azure Functions 과제</span><span class="sxs-lookup"><span data-stu-id="4a04f-132">The Azure Functions Challenge</span></span>](https://aka.ms/afc)

* [<span data-ttu-id="4a04f-133">Azure 서버리스 컴퓨팅 쿡북</span><span class="sxs-lookup"><span data-stu-id="4a04f-133">Azure Serverless Computing Cookbook</span></span>](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [<span data-ttu-id="4a04f-134">Node.js에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4a04f-134">How to use Queue storage from Node.js</span></span>](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [<span data-ttu-id="4a04f-135">Azure Cosmos DB 소개: SQL API</span><span class="sxs-lookup"><span data-stu-id="4a04f-135">Introduction to Azure Cosmos DB: SQL API</span></span>](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [<span data-ttu-id="4a04f-136">Azure Cosmos DB의 기술적 개요</span><span class="sxs-lookup"><span data-stu-id="4a04f-136">A technical overview of Azure Cosmos DB</span></span>](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [<span data-ttu-id="4a04f-137">Azure Cosmos DB 설명서</span><span class="sxs-lookup"><span data-stu-id="4a04f-137">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/azure/cosmos-db/)
