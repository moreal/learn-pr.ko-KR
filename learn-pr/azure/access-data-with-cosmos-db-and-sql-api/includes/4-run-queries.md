만들 수 있는 쿼리의 종류에 대해 알아보았으면 이제 Azure Portal의 데이터 탐색기를 사용하여 제품 데이터를 검색하고 필터링해 보겠습니다.

데이터 탐색기 창에서는 기본적으로 문서 탭의 쿼리는 `SELECT * FROM c`로 설정됩니다. 이 기본 쿼리는 컬렉션의 모든 문서를 검색하고 표시합니다.

![데이터 탐색기에서 기본 쿼리는 `SELECT * FROM c`입니다.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a>새 쿼리 만들기

1. 데이터 탐색기에서 **새 SQL 쿼리** 탭을 클릭합니다. 새 **쿼리 1** 탭의 기본 쿼리가 `SELECT * from c`인지 확인한 다음, **쿼리 실행**을 클릭합니다. 이 쿼리는 데이터베이스의 모든 결과를 반환합니다.

    ![ORDER BY c._ts DESC를 추가하고 필터 적용을 클릭하여 기본 쿼리를 변경합니다.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-edit-query.png)

2. 이제 이전 단원에서 설명했던 몇 가지 쿼리를 실행해 보겠습니다. 쿼리 탭에서 `SELECT * from c`를 삭제하고 다음 쿼리를 복사하여 붙여넣은 후에, **쿼리 실행**을 클릭합니다.

    ```
    SELECT *
    FROM Products p
    WHERE p.id ="1"
    ```

    결과로 `productId`가 1인 제품이 반환됩니다.

    ![ORDER BY c._ts DESC를 추가하고 필터 적용을 클릭하여 기본 쿼리를 변경합니다.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-query-by-id.png)

3. 이전 쿼리를 삭제하고 다음 쿼리를 복사하여 붙여넣은 후에, **쿼리 실행**을 클릭합니다. 이 쿼리는 모든 제품의 가격, 설명 및 제품 ID를 가격의 오름차순으로 반환합니다.
 
    ```
    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC
    ```

## <a name="summary"></a>요약

이제 Azure Cosmos DB의 데이터에 대한 몇 가지 기본 쿼리를 완료했습니다. 