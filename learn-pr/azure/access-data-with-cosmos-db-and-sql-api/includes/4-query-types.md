<span data-ttu-id="17463-101">데이터베이스에 추가한 문서 두 개를 쿼리의 대상으로 사용하여 몇 가지 쿼리 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="17463-101">Using the two documents you added to the database as the target of our queries, let's walk through some query basics.</span></span> <span data-ttu-id="17463-102">Azure Cosmos DB는 SQL Server처럼 SQL 쿼리를 사용하여 쿼리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-102">Azure Cosmos DB uses SQL queries, just like SQL Server, to perform query operations.</span></span> <span data-ttu-id="17463-103">기본적으로 모든 속성은 자동으로 인덱싱되기 때문에 데이터베이스의 모든 데이터는 쿼리에 즉시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-103">All properties are automatically indexed by default, so all data in the database is instantly available to query.</span></span>

## <a name="sql-query-basics"></a><span data-ttu-id="17463-104">SQL 쿼리 기본 사항</span><span class="sxs-lookup"><span data-stu-id="17463-104">SQL query basics</span></span>
<span data-ttu-id="17463-105">모든 SQL 쿼리는 SELECT 절과 선택적 FROM 및 WHERE 절로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-105">Every SQL query consists of a SELECT clause and optional FROM and WHERE clauses.</span></span> <span data-ttu-id="17463-106">또한 ORDER BY 및 JOIN과 같은 다른 절을 추가하여 필요한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-106">In addition, you can add other clauses like ORDER BY and JOIN to get the information you need.</span></span>

<span data-ttu-id="17463-107">SQL 쿼리의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-107">A SQL query has the following format:</span></span>

    SELECT <select_list>
    [FROM <optional_from_specification>]
    [WHERE <optional_filter_condition>]
    [ORDER BY <optional_sort_specification>]
    [JOIN <optional_join_specification>]

## <a name="select-clause"></a><span data-ttu-id="17463-108">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="17463-108">SELECT clause</span></span>

<span data-ttu-id="17463-109">SELECT 절은 쿼리가 실행될 때 생성되는 값의 형식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-109">The SELECT clause determines the type of values that will be produced when the query is executed.</span></span> <span data-ttu-id="17463-110">`SELECT *` 값은 전체 JSON 문서가 반환되는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17463-110">A value of `SELECT *` indicates that the entire JSON document is returned.</span></span>

<span data-ttu-id="17463-111">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-111">**Query**</span></span>
```
SELECT *
FROM Products p
WHERE p.id ="1"
```

<span data-ttu-id="17463-112">**반환**</span><span class="sxs-lookup"><span data-stu-id="17463-112">**Returns**</span></span>
```
[
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
                "width": 6,
                "height": 8,
                "depth": 1
            }
        },
        "_rid": "iAEeANrzNAAJAAAAAAAAAA==",
        "_self": "dbs/iAEeAA==/colls/iAEeANrzNAA=/docs/iAEeANrzNAAJAAAAAAAAAA==/",
        "_etag": "\"00003a02-0000-0000-0000-5b9208440000\"",
        "_attachments": "attachments/",
        "_ts": 1536297028
    }
]
```

<span data-ttu-id="17463-113">또는 SELECT 절에 속성 목록을 포함시켜서 특정 속성만 포함되도록 출력을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-113">Or, you can limit the output to include only certain properties by including a list of properties in the SELECT clause.</span></span> <span data-ttu-id="17463-114">다음 쿼리에서는 ID, 제조업체 및 제품 설명만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-114">In the following query, only the ID, manufacturer, and product description are returned.</span></span>

<span data-ttu-id="17463-115">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-115">**Query**</span></span>
```
SELECT 
    p.id, 
    p.manufacturer, 
    p.description
FROM Products p
WHERE p.id ="1"
```

<span data-ttu-id="17463-116">**반환**</span><span class="sxs-lookup"><span data-stu-id="17463-116">**Returns**</span></span>
```
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a><span data-ttu-id="17463-117">FROM 절</span><span class="sxs-lookup"><span data-stu-id="17463-117">FROM clause</span></span>

<span data-ttu-id="17463-118">FROM 절은 쿼리가 작동하는 데이터 원본을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-118">The FROM clause specifies the data source upon which the query operates.</span></span> <span data-ttu-id="17463-119">컬렉션 전체를 쿼리의 원본으로 지정하거나 컬렉션의 하위 집합을 대신 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-119">You can make the whole collection the source of the query or you can specify a subset of the collection instead.</span></span> <span data-ttu-id="17463-120">쿼리의 뒷부분에서 원본을 필터링/프로젝션하지 않을 경우 FROM 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="17463-120">The FROM clause is optional unless the source is filtered or projected later in the query.</span></span>

<span data-ttu-id="17463-121">`SELECT * FROM Products`와 같은 쿼리는 전체 Products 컬렉션이 쿼리를 열거할 원본임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17463-121">A query such as `SELECT * FROM Products` indicates that the entire Products collection is the source over which to enumerate the query.</span></span>

<span data-ttu-id="17463-122">컬렉션을 별칭으로 `SELECT p.id FROM Products AS p` 또는 간단히 `SELECT p.id FROM Products p`로 지정할 수 있으며 여기서 `p`는 `Products`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-122">A collection can be aliased, such as `SELECT p.id FROM Products AS p` or simply `SELECT p.id FROM Products p`, where `p` is the equivalent of `Products`.</span></span> <span data-ttu-id="17463-123">`AS`는 식별자를 별칭으로 지정하는 선택적 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="17463-123">`AS` is an optional keyword to alias the identifier.</span></span>

<span data-ttu-id="17463-124">별칭으로 지정한 후에는 원래 원본을 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-124">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="17463-125">예를 들어 `SELECT Products.id FROM Products p`는 "Products" 식별자를 더 이상 확인할 수 없으므로 잘못된 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="17463-125">For example, `SELECT Products.id FROM Products p` is syntactically invalid because the identifier "Products" cannot be resolved anymore.</span></span>

<span data-ttu-id="17463-126">참조해야 하는 모든 속성을 정규화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-126">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="17463-127">엄격한 스키마 준수가 없을 경우 모호한 바인딩을 방지하기 위해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-127">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="17463-128">따라서 `SELECT id FROM Products p`는 `id` 속성이 바인딩되지 않았으므로 잘못된 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="17463-128">Therefore, `SELECT id FROM Products p` is syntactically invalid because the property `id` is not bound.</span></span>

### <a name="subdocuments-in-a-from-clause"></a><span data-ttu-id="17463-129">FROM 절의 하위 문서</span><span class="sxs-lookup"><span data-stu-id="17463-129">Subdocuments in a FROM clause</span></span>
<span data-ttu-id="17463-130">원본을 더 작은 하위 집합으로 줄일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-130">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="17463-131">예를 들어 각 문서에서 하위 트리만을 열거하려는 경우 다음 예제에서처럼 하위 루트가 원본이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-131">For instance, to enumerate only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="17463-132">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-132">**Query**</span></span>
```
SELECT * 
FROM Products.shipping
```

<span data-ttu-id="17463-133">**결과**</span><span class="sxs-lookup"><span data-stu-id="17463-133">**Results**</span></span>  

```
[
    {
        "weight": 1,
        "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
        }
    },
    {
        "weight": 2,
        "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
        }
    }
]
```

<span data-ttu-id="17463-134">위 예제에서는 배열을 원본으로 사용했지만 다음 예제에 나온 대로 개체를 원본으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-134">Although the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example.</span></span> <span data-ttu-id="17463-135">원본에 있는 유효한 모든 JSON 값(undefined 제외)이 쿼리 결과에 포함되기 위해 고려됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-135">Any valid JSON value (that's not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="17463-136">일부 제품에 `shipping.weight` 값이 없는 경우 쿼리 결과에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-136">If some products don’t have a `shipping.weight` value, they are excluded in the query result.</span></span>

<span data-ttu-id="17463-137">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-137">**Query**</span></span>

    SELECT * 
    FROM Products.shipping.weight

<span data-ttu-id="17463-138">**결과**</span><span class="sxs-lookup"><span data-stu-id="17463-138">**Results**</span></span>

    [
        1,
        2
    ]

## <a name="where-clause"></a><span data-ttu-id="17463-139">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="17463-139">WHERE clause</span></span>
<span data-ttu-id="17463-140">WHERE 절은 소스에서 제공하는 JSON 문서가 결과의 일부로 포함되기 위해 충족해야 하는 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-140">The WHERE clause specifies the conditions that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="17463-141">JSON 문서가 결과에 고려되려면 지정된 조건이 **true**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-141">Any JSON document must evaluate the specified conditions to **true** to be considered for the result.</span></span> <span data-ttu-id="17463-142">WHERE 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="17463-142">The WHERE clause is optional.</span></span>

<span data-ttu-id="17463-143">다음 쿼리는 값이 1인 ID가 포함된 문서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-143">The following query requests documents that contain an ID whose value is 1:</span></span>

<span data-ttu-id="17463-144">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-144">**Query**</span></span>

    SELECT p.description
    FROM Products p 
    WHERE p.id = "1"

<span data-ttu-id="17463-145">**결과**</span><span class="sxs-lookup"><span data-stu-id="17463-145">**Results**</span></span>

    [
        {
            "description": "Quick dry crew neck t-shirt"
        }
    ]

## <a name="order-by-clause"></a><span data-ttu-id="17463-146">ORDER BY 절</span><span class="sxs-lookup"><span data-stu-id="17463-146">ORDER BY clause</span></span>

<span data-ttu-id="17463-147">ORDER BY 절을 사용하면 결과를 오름차순이나 내림차순으로 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-147">The ORDER BY clause enables you to order the results in ascending or descending order.</span></span>

<span data-ttu-id="17463-148">다음 ORDER BY 쿼리는 가격이 오름차순으로 정렬된 모든 제품의 가격, 설명 및 제품 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-148">The following ORDER BY query returns the price, description, and product ID for all products, ordered by price, in ascending order:</span></span>

<span data-ttu-id="17463-149">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-149">**Query**</span></span>

    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC

<span data-ttu-id="17463-150">**결과**</span><span class="sxs-lookup"><span data-stu-id="17463-150">**Results**</span></span>

```
[
    {
        "price": "14.99",
        "description": "Quick dry crew neck t-shirt",
        "productId": "33218896"
    },
    {
        "price": "49.99",
        "description": "Black wool pea-coat",
        "productId": "33218897"
    }
]
```

## <a name="join-clause"></a><span data-ttu-id="17463-151">JOIN 절</span><span class="sxs-lookup"><span data-stu-id="17463-151">JOIN clause</span></span>

<span data-ttu-id="17463-152">JOIN 절을 사용하면 문서 및 하위 루트와 내부 조인을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-152">The JOIN clause enables you to perform inner joins with the document and the document subroots.</span></span> <span data-ttu-id="17463-153">예를 들어 제품 데이터베이스에서 운송 데이터로 문서를 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-153">So in the product database, for example, you can join the documents with the shipping data.</span></span>  

<span data-ttu-id="17463-154">다음 쿼리에서는 운송 방법이 있는 각 제품에 대한 제품 ID가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-154">In the following query, the product IDs are returned for each product that has a shipping method.</span></span> <span data-ttu-id="17463-155">운송 속성이 없는 세 번째 제품을 추가하면 세 번째 항목에 운송 속성이 없어서 제외된다는 점에서 결과가 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="17463-155">If you added a third product that didn't have a shipping property, the result would be the same because the third item would be excluded for not having a shipping property.</span></span>

<span data-ttu-id="17463-156">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="17463-156">**Query**</span></span>

    SELECT p.productId
    FROM Products p
    JOIN p.shipping

<span data-ttu-id="17463-157">**결과**</span><span class="sxs-lookup"><span data-stu-id="17463-157">**Results**</span></span>

    [
        {
            "productId": "33218896"
        },
        {
            "productId": "33218897"
        }
    ]

## <a name="geospatial-queries"></a><span data-ttu-id="17463-158">지리 공간적 쿼리</span><span class="sxs-lookup"><span data-stu-id="17463-158">Geospatial queries</span></span>

<span data-ttu-id="17463-159">지리 공간적 쿼리를 사용하면 GeoJSON 지점을 사용하여 공간 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-159">Geospatial queries enable you to perform spatial queries using GeoJSON Points.</span></span> <span data-ttu-id="17463-160">데이터베이스의 좌표를 사용하여 두 지점 간의 거리를 계산하여 지점, 다각형 또는 LineString이 또 다른 지점, 다각형 또는 LineString 내에 있는지 판단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-160">Using the coordinates in the database, you can calculate the distance between two points and determine whether a Point, Polygon, or LineString is within another Point, Polygon, or LineString.</span></span>

<span data-ttu-id="17463-161">제품 카탈로그 데이터에 대해 이렇게 하면 사용자가 자신의 위치 정보를 입력하고 반경 50마일 내에 원하는 제품이 있는 매장이 있는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17463-161">For product catalog data, this would enable your users to enter their location information and determine whether there were any stores within a 50-mile radius that have the item they're looking for.</span></span> 

## <a name="summary"></a><span data-ttu-id="17463-162">요약</span><span class="sxs-lookup"><span data-stu-id="17463-162">Summary</span></span>

<span data-ttu-id="17463-163">Azure Cosmos DB에 데이터를 추가한 후 모든 데이터를 신속하게 쿼리할 수 있고, 익숙한 SQL 쿼리 기술을 사용하면 귀사와 귀사의 고객이 저장된 데이터를 탐색하고 파악하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17463-163">Being able to quickly query all your data after adding it to Azure Cosmos DB and using familiar SQL query techniques can help you and your customers to explore and gain insights into your stored data.</span></span>