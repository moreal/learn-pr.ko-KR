<span data-ttu-id="86e18-101">Microsoft Cognitive Services는 앱을 보강하는 데 사용할 수 있는 지능형 서비스 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-101">Microsoft Cognitive Services is a rich suite of intelligent services that we can use to enrich our apps.</span></span> <span data-ttu-id="86e18-102">앞에서 텍스트 분석 API 서비스의 일부분을 살펴보면서 텍스트에 대한 대략적인 정보를 찾아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-102">We explored a small part of the Text Analytics API service to find out higher-level information about text.</span></span> <span data-ttu-id="86e18-103">서비스를 사용하여 고객의 텍스트 피드백에서 감정을 분석했습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-103">We used the service to analyze text feedback from customers for sentiment.</span></span> <span data-ttu-id="86e18-104">Azure Functions에 호스트되고 이러한 텍스트 메시지를 여러 버킷 또는 큐로 분류하여 추가 처리하는 솔루션을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-104">We created a solution hosted in Azure Functions to sort these text messages into different buckets, or queues, for further processing.</span></span>

<span data-ttu-id="86e18-105">REST API 호출 방법을 알면 이러한 지능형 서비스를 솔루션에 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-105">Once you know how to call a REST API, then you can easily integrate these intelligent services into your solutions.</span></span> <span data-ttu-id="86e18-106">모든 솔루션은 다음과 같은 비슷한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-106">They all follow a similar pattern:</span></span>

- <span data-ttu-id="86e18-107">액세스 키를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-107">Sign up for an access key</span></span>
- <span data-ttu-id="86e18-108">API 테스트 콘솔에서 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-108">Explore in the API testing console</span></span>
- <span data-ttu-id="86e18-109">액세스 키 및 올바른 지역을 사용하여 요청을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-109">Formulate requests using the access key and the correct region.</span></span>
- <span data-ttu-id="86e18-110">솔루션의 요청을 게시하고 응답을 구문 분석하여 인사이트를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-110">POST requests from your solution and parse the responses for insights.</span></span>

<span data-ttu-id="86e18-111">Azure Functions에서 만든 서버리스 논리에 이 인텔리전스를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-111">We added this intelligence to serverless logic created in Azure Functions.</span></span> <span data-ttu-id="86e18-112">다른 유형의 앱에서 이러한 서비스를 간편하게 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-112">You can easily call these services from other types of apps.</span></span> <span data-ttu-id="86e18-113">시작을 도와주는 여러 클라이언트 라이브러리, 자습서 및 빠른 시작이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-113">There are many client libraries, tutorials and,  quickstarts to get you started.</span></span>

## <a name="suggestions-for-further-enhancement-of-our-solution"></a><span data-ttu-id="86e18-114">솔루션의 추가 향상을 위한 제안</span><span class="sxs-lookup"><span data-stu-id="86e18-114">Suggestions for further enhancement of our solution</span></span>

<span data-ttu-id="86e18-115">솔루션을 더욱 개선하기 위해 고려해 볼 수 있는 몇 가지 아이디어가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-115">Here are some ideas for you to consider if you want to take what we did further.</span></span> 

- <span data-ttu-id="86e18-116">더 많은 텍스트 예제를 사용하여 솔루션을 테스트하고 감정 점수를 긍정적, 중립, 부정적으로 분류하도록 설정한 임계값이 적절한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-116">Test the solution with more text examples and decide whether the thresholds we set to categorize sentiment scores into positive, negative, and neutral are appropriate.</span></span> 
- <span data-ttu-id="86e18-117">[!INCLUDE [negative-q](./q-name-negative.md)] 큐의 메시지를 읽고 텍스트 분석 API를 호출하여 텍스트의 핵심 문구를 찾는 또 다른 함수를 함수 앱에 추가하는 방안을 생각해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-117">Consider adding another function into your function app that reads messages from the [!INCLUDE [negative-q](./q-name-negative.md)] queue and calls the Text Analytics API to find key phrases in the text.</span></span>
- <span data-ttu-id="86e18-118">입력 큐에는 원시 텍스트 피드백이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-118">Our input queue contains raw text feedback.</span></span> <span data-ttu-id="86e18-119">실제 세계에서는 피드백을 이메일 주소, 거래처 번호 같은 형태의 사용자 ID와 연결하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-119">In the real-world, we would associate feedback with some form of user ID such as email address, account number, and so on.</span></span> <span data-ttu-id="86e18-120">따라서 ID 필드 및 텍스트를 포함하는 JSON 문서가 되도록 입력 큐 항목을 개선해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-120">So, enhance the input queue items to be JSON documents containing and ID field and the text.</span></span> <span data-ttu-id="86e18-121">그 후 텍스트 메시지를 작업할 때 해당 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-121">Then use that ID when working with the text message.</span></span>
 - <span data-ttu-id="86e18-122">현재 우리 솔루션은 영어로 "하드 코딩"됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-122">Currently our solution is "hard coded" to English.</span></span> <span data-ttu-id="86e18-123">텍스트 분석 API에서 지원되는 모든 언어로 텍스트를 처리할 수 있게 하려면 어떻게 변경해야 하는지 고민해 보세요.</span><span class="sxs-lookup"><span data-stu-id="86e18-123">Think about what changes you would do to make it capable or handling text in all languages supported by the Text Analytics API.</span></span>  

<span data-ttu-id="86e18-124">Cognitive Services API 중 하나를 호출하는 방법을 배웠으니, 몇 가지 다른 서비스를 살펴보고 솔루션에 사용하는 방법을 생각해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="86e18-124">Now that you know how to call one of these Cognitive Services APIs, take a look at some of the other services and think about how you might use them in your solutions.</span></span> 

## <a name="further-reading"></a><span data-ttu-id="86e18-125">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="86e18-125">Further reading</span></span>

- [<span data-ttu-id="86e18-126">Text Analytics 개요</span><span class="sxs-lookup"><span data-stu-id="86e18-126">Text Analytics overview</span></span>](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [<span data-ttu-id="86e18-127">Text Analytics에서 감정을 감지하는 방법</span><span class="sxs-lookup"><span data-stu-id="86e18-127">How to detect sentiment in Text Analytics</span></span>](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [<span data-ttu-id="86e18-128">Cognitive Services 설명서</span><span class="sxs-lookup"><span data-stu-id="86e18-128">Cognitive Services Documentation</span></span>](https://docs.microsoft.com/azure/cognitive-services/)

## <a name="clean-up-resources"></a><span data-ttu-id="86e18-129">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="86e18-129">Clean up resources</span></span>

<span data-ttu-id="86e18-130">Azure에서 *리소스*란 앱, 함수, 저장소 계정 등을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-130">*Resources* in Azure refer to function apps, functions, storage accounts, and so forth.</span></span> <span data-ttu-id="86e18-131">리소스는 *리소스 그룹*으로 그룹화되며 그룹을 삭제하면 그룹의 모든 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-131">They are grouped into *resource groups*, and you can delete everything in a group by deleting the group.</span></span>

<span data-ttu-id="86e18-132">이 모듈을 완료하기 위해 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-132">You created resources to complete this module.</span></span> <span data-ttu-id="86e18-133">[계정 상태](https://azure.microsoft.com/account/) 및 [서비스 가격 책정](https://azure.microsoft.com/pricing/)에 따라 리소스에 대해 요금이 청구될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-133">You may be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/).</span></span> <span data-ttu-id="86e18-134">리소스가 더 이상 필요하지 않게 되면 다음과 같이 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-134">If you don't need the resources anymore, here's how to delete them:</span></span>

1. <span data-ttu-id="86e18-135">Azure Portal에서 **리소스 그룹** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-135">In the Azure portal, go to the **Resource group** page.</span></span>

   <span data-ttu-id="86e18-136">함수 앱 페이지에서 해당 페이지로 이동하려면 **개요** 탭을 선택한 후 **리소스 그룹** 아래의 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-136">To get to that page from the function app page, select the **Overview** tab and then select the link under **Resource group**.</span></span>

   <span data-ttu-id="86e18-137">대시보드에서 해당 페이지로 이동하려면 **리소스 그룹**을 선택한 다음, 이 모듈에 사용한 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-137">To get to that page from the dashboard, select **Resource groups**, and then select the resource group that you used for this module.</span></span> 

> [!NOTE]
> <span data-ttu-id="86e18-138">이 모듈에서 제안한 리소스 그룹의 기본 이름은 [!INCLUDE [resource-group-name](./rg-name.md)]이지만, 다른 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-138">The default name of the resource group we suggested for this module was [!INCLUDE [resource-group-name](./rg-name.md)] but it is possible that you used another name.</span></span>

2. <span data-ttu-id="86e18-139">**리소스 그룹** 페이지에서 포함된 리소스 목록을 검토하고 삭제하려는 항목인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-139">In the **Resource group** page, review the list of included resources, and verify that they are the ones you want to delete.</span></span>

3. <span data-ttu-id="86e18-140">**리소스 그룹 삭제**를 선택하고 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-140">Select **Delete resource group**, and follow the instructions.</span></span>

   <span data-ttu-id="86e18-141">삭제는 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-141">Deletion may take a couple of minutes.</span></span> <span data-ttu-id="86e18-142">완료되면 알림이 잠시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-142">When it's done, a notification appears for a few seconds.</span></span> <span data-ttu-id="86e18-143">페이지 위쪽의 종 모양 아이콘을 선택해도 알림을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-143">You can also select the bell icon at the top of the page to view the notification.</span></span>

## <a name="further-reading"></a><span data-ttu-id="86e18-144">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="86e18-144">Further Reading</span></span>

<span data-ttu-id="86e18-145">이 목록은 전체 목록이 아니며, 다음은 이 모듈에서 다루는 흥미로운 토픽과 관련된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="86e18-145">While this is not intended to be an exhaustive list, the following are some resources related to the topics covered in this module that you might find interesting.</span></span>

 * [<span data-ttu-id="86e18-146">Azure Functions 설명서</span><span class="sxs-lookup"><span data-stu-id="86e18-146">Azure Functions documentation</span></span>](https://docs.microsoft.com/azure/azure-functions/)

* [<span data-ttu-id="86e18-147">Azure Functions 과제</span><span class="sxs-lookup"><span data-stu-id="86e18-147">The Azure Functions Challenge</span></span>](https://aka.ms/afc)

* [<span data-ttu-id="86e18-148">Azure 서버리스 컴퓨팅 쿡북</span><span class="sxs-lookup"><span data-stu-id="86e18-148">Azure Serverless Computing Cookbook</span></span>](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)

 * [<span data-ttu-id="86e18-149">Node.js에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="86e18-149">How to use Queue storage from Node.js</span></span>](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)

 * [<span data-ttu-id="86e18-150">Azure Cosmos DB: SQL API 소개</span><span class="sxs-lookup"><span data-stu-id="86e18-150">Introduction to Azure Cosmos DB: SQL API</span></span>](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)

* [<span data-ttu-id="86e18-151">Azure Cosmos DB의 기술 개요</span><span class="sxs-lookup"><span data-stu-id="86e18-151">A technical overview of Azure Cosmos DB</span></span>](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)

* [<span data-ttu-id="86e18-152">Azure Cosmos DB 설명서</span><span class="sxs-lookup"><span data-stu-id="86e18-152">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/azure/cosmos-db/)
