<span data-ttu-id="424c4-101">만들 수 있는 쿼리의 종류에 대해 알아보았으므로 이제 Azure Portal의 데이터 탐색기를 사용하여 제품 데이터를 검색하고 필터링해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-101">Now that you've learned about what kinds of queries you can create, let's use the Data Explorer in the Azure portal to retrieve and filter your product data.</span></span>

<span data-ttu-id="424c4-102">데이터 탐색기 창에서는 다음 이미지에 표시된 것처럼 기본적으로 **문서** 탭의 쿼리가 `SELECT * FROM c`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-102">In your Data Explorer window, note that by default, the query on the **Document** tab is set to `SELECT * FROM c` as shown in the following image.</span></span> <span data-ttu-id="424c4-103">이 기본 쿼리는 컬렉션에서 모든 문서를 검색하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-103">This default query retrieves and displays all documents in the collection.</span></span>

![데이터 탐색기에서 기본 쿼리는 SELECT \* FROM c입니다.](../media/5-azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a><span data-ttu-id="424c4-105">새 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="424c4-105">Create a new query</span></span>

1. <span data-ttu-id="424c4-106">데이터 탐색기에서 **새 SQL 쿼리** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-106">In Data Explorer, click **New SQL Query**.</span></span> <span data-ttu-id="424c4-107">새 **쿼리 1** 탭의 기본 쿼리가 다시 `SELECT * from c`으로, 컬렉션의 모든 문서가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-107">Note that the default query on the new  **Query 1** tab is again `SELECT * from c`, which will return all documents in the collection.</span></span> 

1. <span data-ttu-id="424c4-108">**Execute Query**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-108">Click **Execute Query**.</span></span> <span data-ttu-id="424c4-109">이 쿼리는 데이터베이스의 모든 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-109">This query returns all results in the database.</span></span>

    ![ORDER BY c._ts DESC를 추가하고 필터 적용을 클릭하여 기본 쿼리를 변경합니다.](../media/5-azure-cosmosdb-data-explorer-edit-query.png)

2. <span data-ttu-id="424c4-111">이제 이전 단원에서 설명했던 쿼리를 몇 개 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-111">Now, let's run some of the queries discussed in the previous unit.</span></span> <span data-ttu-id="424c4-112">쿼리 탭에서 `SELECT * from c`를 삭제하고 다음 쿼리를 복사하여 붙여넣은 후에 **쿼리 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-112">On the query tab, delete `SELECT * from c`, copy and paste the following query, and then click **Execute Query**:</span></span>

    ```sql
    SELECT * 
    FROM Products p 
    WHERE p.id ="1"
    ```

    <span data-ttu-id="424c4-113">그 결과로 `productId`가 1인 제품이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-113">The results return the product whose `productId` is 1.</span></span>

    ![1의 Id에 대해 쿼리하기](../media/5-azure-cosmosdb-data-explorer-query-by-id.png)

3. <span data-ttu-id="424c4-115">이전 쿼리를 삭제하고 다음 쿼리를 복사하여 붙여넣은 후에, **쿼리 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-115">Delete the previous query, copy and paste the following query, and click **Execute Query**.</span></span> <span data-ttu-id="424c4-116">이 쿼리는 가격의 오름차순으로 정렬된 모든 제품의 가격/설명/제품 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-116">This query returns the price, description, and product ID for all products, ordered by price, in ascending order.</span></span>
 
    ```sql
    SELECT p.price, p.description, p.productId 
    FROM Products p 
    ORDER BY p.price ASC
    ```

## <a name="summary"></a><span data-ttu-id="424c4-117">요약</span><span class="sxs-lookup"><span data-stu-id="424c4-117">Summary</span></span>

<span data-ttu-id="424c4-118">이제 Azure Cosmos DB의 데이터에 대해 몇 가지 기본적인 쿼리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="424c4-118">You have now completed some basic queries on your data in Azure Cosmos DB.</span></span> 