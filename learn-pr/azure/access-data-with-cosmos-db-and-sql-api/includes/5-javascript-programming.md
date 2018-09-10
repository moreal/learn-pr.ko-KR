<span data-ttu-id="c2691-101">데이터베이스의 여러 문서를 동시에 업데이트해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> 

<span data-ttu-id="c2691-102">온라인 소매 응용 프로그램에서 사용자가 주문을 할 때 쿠폰 코드, 크레딧, 배당금 중 하나 또는 세 가지를 모두 동시에 사용하려는 경우 해당 옵션에 대해 사용자 계정을 쿼리하고, 사용자가 해당 옵션을 사용했음을 나타내는 업데이트를 사용자 계정에 적용하고, 주문 총액을 업데이트한 후 주문을 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-102">For your online retail application, when a user places an order and wants to use a coupon code, a credit, or a dividend (or all three at once), you'll need to query their account for those options, make updates to their account indicating they used them, update the order total, and process the order.</span></span>

<span data-ttu-id="c2691-103">이러한 모든 작업이 단일 트랜잭션 내에서 동시에 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-103">All of these actions need to happen at the same time, within a single transaction.</span></span> <span data-ttu-id="c2691-104">사용자가 주문 취소를 선택하는 경우에는 변경 내용을 롤백하여 계정 정보를 수정하지 않아야 합니다. 그래야 사용자가 쿠폰 코드, 크레딧, 배당금을 다음 구매 시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-104">If the user chooses to cancel the order, you'll want to roll back the changes and not modify their account information - so that their coupon codes, credits, and dividends are available for their next purchase.</span></span>

<span data-ttu-id="c2691-105">Azure Cosmos DB에서 이러한 트랜잭션을 수행할 때는 저장 프로시저 및 사용자 정의 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-105">The way to perform these transactions in Azure Cosmos DB is by using stored procedures and user defined functions.</span></span> <span data-ttu-id="c2691-106">ACID(원자성, 일관성, 격리, 영속성) 트랜잭션을 수행하는 방법은 저장 프로시저뿐입니다. 저장 프로시저는 서버에서 실행되는 서버 쪽 프로그래밍 입니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-106">Stored procedures are the only way to ensure ACID (Atomicity, Consistency, Isolation, Durability) transactions, as they are run on the server, and are thus referred to as server-side programming.</span></span> <span data-ttu-id="c2691-107">사용자 정의 함수도 서버에 저장되며 쿼리 중에 쿼리 내의 값이나 문서에 대한 계산 논리를 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-107">User-defined functions are also stored on the server, and are used during queries to perform computational logic on values or documents within the query.</span></span> 

<span data-ttu-id="c2691-108">이 모듈에서는 저장 프로시저와 UDF에 대해 알아보고 포털에서 몇 가지 저장 프로시저 및 UDF를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-108">In this module you'll learn about stored procedures and UDFs and then run some in the portal.</span></span>

## <a name="stored-procedure-basics"></a><span data-ttu-id="c2691-109">저장 프로시저 기본 사항</span><span class="sxs-lookup"><span data-stu-id="c2691-109">Stored procedure basics</span></span>

<span data-ttu-id="c2691-110">저장 프로시저는 문서와 속성에 대해 복잡한 트랜잭션을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-110">Stored procedures perform complex transactions on documents and properties.</span></span> <span data-ttu-id="c2691-111">저장 프로시저는 Javascript로 작성되며 Azure Cosmos DB의 컬렉션에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-111">Stored procedures are written in Javascript and are stored in a collection on Azure Cosmos DB.</span></span> <span data-ttu-id="c2691-112">데이터와 인접한 데이터베이스 엔진에서 저장 프로시저를 수행하면 클라이언트 쪽 프로그래밍에 비해 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-112">By performing the stored procedures on the database engine and close to the data, you can improve performance over client-side programming.</span></span>

<span data-ttu-id="c2691-113">Azure Cosmos DB 내에서 원자성 트랜잭션을 수행하는 방법은 저장 프로시저뿐입니다. 클라이언트 쪽 SDK는 트랜잭션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-113">Stored procedures are the only way to achieve atomic transactions within Azure Cosmos DB; the client side SDKs do not support transactions.</span></span>

<span data-ttu-id="c2691-114">저장 프로시저에서 일괄 처리 작업을 수행하는 방식도 효율적입니다. 별도의 트랜잭션을 생성해야 하는 필요성이 줄어들기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-114">Performing batch operations in stored procedures is also recommended because of the reduced need to create separate transactions.</span></span>

<!--TODO: Ideally I'd like to list some cases where a stored proc is not the best option-->

## <a name="stored-procedure-example"></a><span data-ttu-id="c2691-115">저장 프로시저 예제</span><span class="sxs-lookup"><span data-stu-id="c2691-115">Stored procedure example</span></span>

<span data-ttu-id="c2691-116">다음 샘플은 현재 컨텍스트를 가져온 다음, “Hello, World”를 표시하는 응답을 보내는 간단한 HelloWorld 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-116">The following sample is a simple HelloWorld stored procedure that gets the current context, and sends a response that displays "Hello, World".</span></span> <span data-ttu-id="c2691-117">저장 프로시저에도 Azure Cosmos DB 문서처럼 ID 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-117">Note that the stored procedure has an id value, just like Azure Cosmos DB documents.</span></span>

```java
var helloWorldStoredProc = {
    id: "helloWorld",
    serverScript: function () {
        var context = getContext();
        var response = context.getResponse();

        response.setBody("Hello, World");
    }
}
```

## <a name="user-defined-function-basics"></a><span data-ttu-id="c2691-118">사용자 정의 함수 기본 사항</span><span class="sxs-lookup"><span data-stu-id="c2691-118">User defined function basics</span></span>

<span data-ttu-id="c2691-119">UDF(사용자 정의 함수)는 Azure Cosmos DB SQL 쿼리 언어 문법을 확장하고 사용자 지정 비즈니스 논리(예: 속성과 문서에 대한 계산)를 구현하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-119">User-defined functions (UDFs) are used to extend the Azure Cosmos DB SQL query language grammar and implement custom business logic such as calculations on properties and documents.</span></span> <span data-ttu-id="c2691-120">UDF는 쿼리 내에서만 호출할 수 있으며 저장 프로시저와는 달리 컨텍스트 개체에 액세스할 수 없으므로 문서를 읽거나 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-120">UDFs can only be called from inside queries and unlike stored procedures, they do not have access to the context object, so they cannot read or write documents.</span></span>

<span data-ttu-id="c2691-121">온라인 상거래 시나리오에서는 UDF를 사용하여 주문 총액에 적용할 판매세 또는 제품이나 주문에 적용할 할인율을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-121">In an online commerce scenario, a UDF could be used to determine the sales tax to apply to an order total, or a percentage discount to apply to products or orders.</span></span>

## <a name="user-defined-function-example"></a><span data-ttu-id="c2691-122">사용자 정의 함수 예제</span><span class="sxs-lookup"><span data-stu-id="c2691-122">User defined function example</span></span>

<span data-ttu-id="c2691-123">다음 샘플에서는 주문 총액 기준 할인액을 계산하는 UDF를 만든 다음, 할인액에 따라 수정된 주문 총액을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-123">The following sample creates a UDF to calculate discounts based on an order total, and then it returns the modified order total based on the discount.</span></span>

```java
var discountUdf = {
    id: "discount",
    serverScript: function discount(orderTotal) {

        if(orderTotal == undefined) 
            throw 'no input';

        if (orderTotal < 50) 
            return orderTotal * 0.9;
        else if (orderTotal < 100) 
            return orderTotal * 0.8;
        else
            return orderTotal * 0.7;
    }
}
```

## <a name="create-a-stored-procedure-in-the-portal"></a><span data-ttu-id="c2691-124">포털에서 저장 프로시저 만들기</span><span class="sxs-lookup"><span data-stu-id="c2691-124">Create a stored procedure in the portal</span></span>

<span data-ttu-id="c2691-125">포털에서 저장 프로시저를 새로 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-125">Let's create a new stored procedure in the portal.</span></span> <span data-ttu-id="c2691-126">포털에서는 컬렉션의 첫 번째 항목을 검색하는 단순한 저장 프로시저가 자동으로 입력되므로, 이 저장 프로시저를 먼저 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-126">The portal automatically populates a simple stored procedure that retrieves the first item in the collection, so we'll run this stored procedure first.</span></span>

1. <span data-ttu-id="c2691-127">데이터 탐색기에서 **새 저장 프로시저**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-127">In the Data Explorer, click **New Stored Procedure**.</span></span>

    <span data-ttu-id="c2691-128">데이터 탐색기에 샘플 저장 프로시저가 포함된 새 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-128">Data Explorer displays a new tab with a sample stored procedure.</span></span>

  <!--TODO: Insert animated gif of creating the stored proc-->

2. <span data-ttu-id="c2691-129">**저장 프로시저 ID** 상자에 이름을 *sample*로 입력하고 **저장**, **실행**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-129">In the **Stored Procedure Id** box, enter the name *sample*, click **Save**, and then click **Execute**.</span></span>


3. <span data-ttu-id="c2691-130">**입력 매개 변수** 상자에 파티션 키의 이름(*33218896*)을 입력한 다음, **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-130">In the **Input parameters** box, type the name of a partition key, *33218896* and then click **Execute**.</span></span> <span data-ttu-id="c2691-131">저장 프로시저는 단일 파티션 내에서 작동하는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="c2691-131">Note that stored procedures work within a single partition.</span></span>

    ![포털에서 저장 프로시저 실행](../media-draft/5-javascript-programming/stored-procedure.gif)

    <span data-ttu-id="c2691-133">결과 창에 컬렉션의 첫 번째 문서에서 가져온 피드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-133">The Result pane displays the feed from the first document in the collection.</span></span>

## <a name="create-a-stored-procedure-that-creates-documents"></a><span data-ttu-id="c2691-134">문서를 만드는 저장 프로시저 만들기</span><span class="sxs-lookup"><span data-stu-id="c2691-134">Create a stored procedure that creates documents</span></span>

<span data-ttu-id="c2691-135">이번에는 문서를 만드는 저장 프로시저를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-135">Now let's create a stored procedure that creates documents.</span></span>

1. <span data-ttu-id="c2691-136">데이터 탐색기에서 **새 저장 프로시저**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-136">In the Data Explorer, click **New Stored Procedure**.</span></span> <span data-ttu-id="c2691-137">이 저장 프로시저의 이름을 *createDocuments*로 지정하고 **저장**, **실행**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-137">Name this stored procedure *createDocuments*, click **Save** and then click **Execute**.</span></span>

    ```java
    var createDocumentStoredProc = {
        id: "createMyDocument",
        productid: "5"
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();
    
            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }
    ```

<!--TODO: Need to fix code above-->

2. <span data-ttu-id="c2691-138">파티션 키 값으로 *3*을 입력하고 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-138">Enter a partition key value of *3*, and then click **Execute**.</span></span>

    <span data-ttu-id="c2691-139">새로 만든 문서가 데이터 탐색기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-139">Data explorer displays the newly created document.</span></span> 

## <a name="create-a-user-defined-functions"></a><span data-ttu-id="c2691-140">사용자 정의 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="c2691-140">Create a User-defined functions</span></span>

<span data-ttu-id="c2691-141">이제 데이터 탐색기에서 사용자 정의 함수를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-141">Now let's create a user defined function in Data Explorer.</span></span>

1. <span data-ttu-id="c2691-142">데이터 탐색기에서 **새 UDF**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-142">In the Data Explorer, click **New UDF**.</span></span> <span data-ttu-id="c2691-143">다음 코드를 창에 복사하고 UDF 이름을 *tax*로 지정한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-143">Copy the following code into the window, name the UDF *tax*, and then click **Save**.</span></span> <span data-ttu-id="c2691-144">UDF는 포털에서는 실행할 수 없지만 나중에 모듈에서 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2691-144">There's no way to run the UDF from the portal, but we'll use it in a later module.</span></span>

```java
function userDefinedFunction(){
    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }
}
```

