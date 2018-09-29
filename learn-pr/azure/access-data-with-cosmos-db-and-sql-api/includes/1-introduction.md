<span data-ttu-id="e3b97-101">데이터베이스에 데이터를 추가하고 데이터를 쿼리하는 작업은 간단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b97-101">Adding data and querying data in your database should be straightforward.</span></span> 

<span data-ttu-id="e3b97-102">온라인 의류 판매점에서 일하면서 Azure Cosmos DB의 전자상거래 데이터베이스에 재고 목록 데이터를 추가해야 한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e3b97-102">Imagine you work for an online clothing retailer and you need to add inventory data to your e-commerce database in Azure Cosmos DB.</span></span> <span data-ttu-id="e3b97-103">데이터가 데이터베이스에 있게 되면, SQL Server에서 사용하는 SQL 쿼리와 동일한 익숙한 SQL 쿼리를 사용하여 쿼리를 실행하고, 저장된 프로시저와 UDF(사용자 정의 함수)를 사용하여 복잡한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3b97-103">Once the data is in the database, you can query it by using familiar SQL queries (yes, just like the ones you use in SQL Server) and perform complex operations by using stored procedures and user-defined functions (UDFs).</span></span>

<span data-ttu-id="e3b97-104">Azure Cosmos DB에는 Azure Portal에서 데이터 추가, 데이터 수정, 저장 프로시저 만들기 및 실행 등과 같은 모든 작업을 수행하는 데 사용할 수 있는 데이터 탐색기가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3b97-104">Azure Cosmos DB provides a Data Explorer in the Azure portal that you can use to perform all these operations: adding data, modifying data, and creating and running stored procedures.</span></span> <span data-ttu-id="e3b97-105">데이터 탐색기는 Azure Portal에서 사용하거나 데이터 작업을 수행할 수 있는 추가 공간을 제공하도록 잠금을 해제하여 독립 실행형 웹 브라우저에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3b97-105">The Data Explorer can be used in the Azure portal or it can be undocked and used in a standalone web browser, providing additional space to work with your data.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="e3b97-106">학습 목표</span><span class="sxs-lookup"><span data-stu-id="e3b97-106">Learning objectives</span></span>

<span data-ttu-id="e3b97-107">이 모듈에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b97-107">In this module, you will:</span></span>

- <span data-ttu-id="e3b97-108">데이터 탐색기에서 제품 카탈로그 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="e3b97-108">Create product catalog documents in the Data Explorer</span></span>
- <span data-ttu-id="e3b97-109">Azure Cosmos DB 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="e3b97-109">Perform Azure Cosmos DB queries</span></span>
- <span data-ttu-id="e3b97-110">저장 프로시저를 사용하여 문서에 대한 작업 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="e3b97-110">Create and run operations on your documents by using stored procedures</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3b97-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e3b97-111">Prerequisites</span></span>

- <span data-ttu-id="e3b97-112">데이터베이스 및 쿼리에 대한 이해</span><span class="sxs-lookup"><span data-stu-id="e3b97-112">Have an understanding of databases and queries</span></span>
