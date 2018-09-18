데이터베이스에 추가한 문서 두 개를 쿼리의 대상으로 사용하여 몇 가지 쿼리 기본 사항을 알아봅니다. Azure Cosmos DB는 SQL Server처럼 SQL 쿼리를 사용하여 쿼리 작업을 수행합니다. 기본적으로 모든 속성은 자동으로 인덱싱되기 때문에 데이터베이스의 모든 데이터는 쿼리에 즉시 사용할 수 있습니다.

## <a name="sql-query-basics"></a>SQL 쿼리 기본 사항
모든 SQL 쿼리는 SELECT 절과 선택적 FROM 및 WHERE 절로 구성됩니다. 또한 ORDER BY 및 JOIN과 같은 다른 절을 추가하여 필요한 정보를 얻을 수 있습니다.

SQL 쿼리의 형식은 다음과 같습니다.

    SELECT <select_list>
    [FROM <optional_from_specification>]
    [WHERE <optional_filter_condition>]
    [ORDER BY <optional_sort_specification>]
    [JOIN <optional_join_specification>]

## <a name="select-clause"></a>SELECT 절

SELECT 절은 쿼리가 실행될 때 생성되는 값의 형식을 결정합니다. `SELECT *` 값은 전체 JSON 문서가 반환되는 것을 나타냅니다.

**쿼리**
```
SELECT *
FROM Products p
WHERE p.id ="1"
```

**반환**
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

또는 SELECT 절에 속성 목록을 포함시켜서 특정 속성만 포함되도록 출력을 제한할 수 있습니다. 다음 쿼리에서는 ID, 제조업체 및 제품 설명만 반환됩니다.

**쿼리**
```
SELECT 
    p.id, 
    p.manufacturer, 
    p.description
FROM Products p
WHERE p.id ="1"
```

**반환**
```
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a>FROM 절

FROM 절은 쿼리가 작동하는 데이터 원본을 지정합니다. 컬렉션 전체를 쿼리의 원본으로 지정하거나 컬렉션의 하위 집합을 대신 지정할 수 있습니다. 쿼리의 뒷부분에서 원본을 필터링/프로젝션하지 않을 경우 FROM 절은 선택 사항입니다.

`SELECT * FROM Products`와 같은 쿼리는 전체 Products 컬렉션이 쿼리를 열거할 원본임을 나타냅니다.

컬렉션을 별칭으로 `SELECT p.id FROM Products AS p` 또는 간단히 `SELECT p.id FROM Products p`로 지정할 수 있으며 여기서 `p`는 `Products`에 해당합니다. `AS`는 식별자를 별칭으로 지정하는 선택적 키워드입니다.

별칭으로 지정한 후에는 원래 원본을 바인딩할 수 없습니다. 예를 들어 `SELECT Products.id FROM Products p`는 "Products" 식별자를 더 이상 확인할 수 없으므로 잘못된 구문입니다.

참조해야 하는 모든 속성을 정규화해야 합니다. 엄격한 스키마 준수가 없을 경우 모호한 바인딩을 방지하기 위해 적용됩니다. 따라서 `SELECT id FROM Products p`는 `id` 속성이 바인딩되지 않았으므로 잘못된 구문입니다.

### <a name="subdocuments-in-a-from-clause"></a>FROM 절의 하위 문서
원본을 더 작은 하위 집합으로 줄일 수도 있습니다. 예를 들어 각 문서에서 하위 트리만을 열거하려는 경우 다음 예제에서처럼 하위 루트가 원본이 될 수 있습니다.

**쿼리**
```
SELECT * 
FROM Products.shipping
```

**결과**  

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

위 예제에서는 배열을 원본으로 사용했지만 다음 예제에 나온 대로 개체를 원본으로 사용할 수도 있습니다. 원본에 있는 유효한 모든 JSON 값(undefined 제외)이 쿼리 결과에 포함되기 위해 고려됩니다. 일부 제품에 `shipping.weight` 값이 없는 경우 쿼리 결과에서 제외됩니다.

**쿼리**

    SELECT * 
    FROM Products.shipping.weight

**결과**

    [
        1,
        2
    ]

## <a name="where-clause"></a>WHERE 절
WHERE 절은 소스에서 제공하는 JSON 문서가 결과의 일부로 포함되기 위해 충족해야 하는 조건을 지정합니다. JSON 문서가 결과에 고려되려면 지정된 조건이 **true**여야 합니다. WHERE 절은 선택 사항입니다.

다음 쿼리는 값이 1인 ID가 포함된 문서를 요청합니다.

**쿼리**

    SELECT p.description
    FROM Products p 
    WHERE p.id = "1"

**결과**

    [
        {
            "description": "Quick dry crew neck t-shirt"
        }
    ]

## <a name="order-by-clause"></a>ORDER BY 절

ORDER BY 절을 사용하면 결과를 오름차순이나 내림차순으로 정렬할 수 있습니다.

다음 ORDER BY 쿼리는 가격이 오름차순으로 정렬된 모든 제품의 가격, 설명 및 제품 ID를 반환합니다.

**쿼리**

    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC

**결과**

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

## <a name="join-clause"></a>JOIN 절

JOIN 절을 사용하면 문서 및 하위 루트와 내부 조인을 수행할 수 있습니다. 예를 들어 제품 데이터베이스에서 운송 데이터로 문서를 조인할 수 있습니다.  

다음 쿼리에서는 운송 방법이 있는 각 제품에 대한 제품 ID가 반환됩니다. 운송 속성이 없는 세 번째 제품을 추가하면 세 번째 항목에 운송 속성이 없어서 제외된다는 점에서 결과가 동일합니다.

**쿼리**

    SELECT p.productId
    FROM Products p
    JOIN p.shipping

**결과**

    [
        {
            "productId": "33218896"
        },
        {
            "productId": "33218897"
        }
    ]

## <a name="geospatial-queries"></a>지리 공간적 쿼리

지리 공간적 쿼리를 사용하면 GeoJSON 지점을 사용하여 공간 쿼리를 수행할 수 있습니다. 데이터베이스의 좌표를 사용하여 두 지점 간의 거리를 계산하여 지점, 다각형 또는 LineString이 또 다른 지점, 다각형 또는 LineString 내에 있는지 판단할 수 있습니다.

제품 카탈로그 데이터에 대해 이렇게 하면 사용자가 자신의 위치 정보를 입력하고 반경 50마일 내에 원하는 제품이 있는 매장이 있는지를 확인할 수 있습니다. 

## <a name="summary"></a>요약

Azure Cosmos DB에 데이터를 추가한 후 모든 데이터를 신속하게 쿼리할 수 있고, 익숙한 SQL 쿼리 기술을 사용하면 귀사와 귀사의 고객이 저장된 데이터를 탐색하고 파악하는 데 도움이 됩니다.