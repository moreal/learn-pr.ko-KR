<span data-ttu-id="660a7-101">Azure Cosmos DB 데이터베이스에 데이터를 추가하는 작업은 간단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-101">Adding data to your Azure Cosmos DB database should be simple.</span></span> <span data-ttu-id="660a7-102">Azure Portal을 열어서 데이터베이스로 이동하고 **데이터 탐색기**를 사용하여 JSON 문서를 데이터베이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-102">You open the Azure portal, navigate to your database, and use the **Data Explorer** to add json documents to the database.</span></span> <span data-ttu-id="660a7-103">데이터를 추가하는 더 좋은 방법이 있지만, 데이터 탐색기는 Azure Cosmos DB에 제공되는 내부 작동 및 기능을 익히는 데 유용한 도구이므로 여기에서 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-103">There are more advanced ways to add data, but we'll start here as the Data Explorer is a great tool to get you aquainted with the inner workings and functionality provided by Azure Cosmos DB.</span></span>

## <a name="what-is-the-data-explorer"></a><span data-ttu-id="660a7-104">데이터 탐색기란?</span><span class="sxs-lookup"><span data-stu-id="660a7-104">What is the Data Explorer?</span></span>
<span data-ttu-id="660a7-105">Azure Cosmos DB 데이터 탐색기는 Azure Portal에 포함된 도구이며 Azure Cosmos DB에 저장된 데이터를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-105">The Azure Cosmos DB Data Explorer is a tool built included in the Azure Portal that is used to manage data stored in an Azure Cosmos DB.</span></span> <span data-ttu-id="660a7-106">데이터 컬렉션을 보고 탐색하는 것은 물론 DB 내에서 문서를 편집할 수 있는 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-106">It provides UI to view and navigate data collections as well as edit documents within the db.</span></span>

## <a name="add-data-using-the-data-explorer"></a><span data-ttu-id="660a7-107">데이터 탐색기를 사용하여 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="660a7-107">Add data using the Data Explorer</span></span>

1. <span data-ttu-id="660a7-108">이전 모듈에 이어서 진행하는 경우 Azure Portal 창에서 **데이터 탐색기**를 클릭한 다음, **전체 화면 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-108">If you're continuing from the previous module, click **Data Explorer** in the Azure portal window, and then click **Open Full Screen**.</span></span>

    <span data-ttu-id="660a7-109">그렇지 않으면 [Azure Portal](https://portal.azure.com/)에 로그인하고 **모든 서비스** > **데이터베이스** > **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-109">Otherwise, sign in to the [Azure portal](https://portal.azure.com/), click **All services** > **Databases** > **Azure Cosmos DB**.</span></span> <span data-ttu-id="660a7-110">그런 다음, 계정을 선택하고 **데이터 탐색기**를 클릭한 다음, **전체 화면 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-110">Then select your account, click **Data Explorer**, and then click **Open Full Screen**</span></span>
 
   ![Azure Portal의 데이터 탐색기에서 새 문서 만들기](../media-draft/2-add-data/azure-cosmosdb-data-explorer-full-screen.png)

2. <span data-ttu-id="660a7-112">**전체 화면 열기** 상자에서 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-112">In the **Open Full Screen** box, click **Open**.</span></span>

    <span data-ttu-id="660a7-113">웹 브라우저에 새로운 전체 화면 데이터 탐색기가 표시됩니다. 이를 통해 데이터베이스 작업 전용 환경과 공간이 확보됩니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-113">The web browser displays the new full screen Data Explorer, which gives you more space and a dedicated environment for working with your database.</span></span>

3. <span data-ttu-id="660a7-114">새 JSON 문서를 만들려면 **새 문서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-114">To create a new json document, click **New Document**.</span></span>

   ![Azure Portal의 데이터 탐색기에서 새 문서 만들기](../media-draft/2-add-data/azure-cosmosdb-data-explorer-new-document.png)

4. <span data-ttu-id="660a7-116">이제 다음 구조로 컬렉션에 문서를 추가하고 다음 코드를 복사하여 **문서** 탭에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-116">Now add a document to the collection with the following structure, just copy and paste the following code into the **Documents** tab.</span></span>

     ```
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
     ```

5. <span data-ttu-id="660a7-117">**문서** 탭에 JSON을 추가했으면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-117">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Azure Portal의 데이터 탐색기에서 JSON 데이터를 복사하고 저장을 클릭합니다.](../media-draft/2-add-data/azure-cosmosdb-data-explorer-save-document.png)

6. <span data-ttu-id="660a7-119">다음 JSON 개체를 데이터 탐색기에 복사하고 **저장**을 클릭하여 문서 하나를 더 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-119">Create and save one more document by copying the following json object into Data Explorer and clicking **Save**.</span></span>

     ```
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
           }
        }
    }
     ```

7. <span data-ttu-id="660a7-120">왼쪽 메뉴에서 **문서**를 클릭하여 문서가 저장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-120">Confirm the documents have been saved by clicking **Documents** on the left-hand menu.</span></span> 

    <span data-ttu-id="660a7-121">데이터 탐색기의 **문서** 탭에 문서 두 개가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-121">Data Explorer displays the two documents in the **Documents** tab.</span></span>

## <a name="summary"></a><span data-ttu-id="660a7-122">요약</span><span class="sxs-lookup"><span data-stu-id="660a7-122">Summary</span></span>

<span data-ttu-id="660a7-123">이 모듈에서는 데이터 탐색기를 사용하여 제품 카탈로그의 제품을 나타내는 문서 두 개를 데이터베이스에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-123">In this module you added two documents, each representing a product in your product catalog, to your database by using the Data Explorer.</span></span> <span data-ttu-id="660a7-124">데이터 탐색기는 문서를 만들고 문서를 수정하고 Azure Cosmos DB를 시작하기에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="660a7-124">The Data Explorer is a good way to create documents, modify documents, and get started with Azure Cosmos DB.</span></span>  
