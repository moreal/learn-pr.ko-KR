데이터베이스의 여러 문서를 동시에 업데이트해야 하는 경우가 많습니다. 

온라인 소매 응용 프로그램에서 사용자가 주문을 할 때 쿠폰 코드, 크레딧, 배당금 중 하나 또는 세 가지를 모두 동시에 사용하려는 경우 사용자 계정에 해당 옵션을 쿼리하고, 사용자가 해당 옵션을 사용했음을 나타내는 업데이트를 사용자 계정에 적용하고, 주문 총액을 업데이트한 후 주문을 처리해야 합니다.

이러한 모든 작업이 단일 트랜잭션 내에서 동시에 수행되어야 합니다. 사용자가 주문 취소를 선택하는 경우에는 변경 내용을 롤백하여 계정 정보를 수정하지 않아야 합니다. 그래야 사용자가 쿠폰 코드, 크레딧, 배당금을 다음 구매 시에 사용할 수 있습니다.

Azure Cosmos DB에서 이러한 트랜잭션을 수행할 때는 저장 프로시저 및 UDF(사용자 정의 함수)를 사용합니다. ACID(원자성, 일관성, 격리, 영속성) 트랜잭션을 수행하는 방법은 저장 프로시저뿐입니다. 저장 프로시저는 서버에서 실행되는 서버 쪽 프로그래밍이기 때문입니다. UDF도 서버에 저장되며 쿼리 중에 쿼리 내의 값이나 문서에 대한 계산 논리를 수행하는 데 사용됩니다. 

이 모듈에서는 저장 프로시저와 UDF에 대해 알아보고 포털에서 몇 가지 저장 프로시저 및 UDF를 실행해 보겠습니다.

## <a name="stored-procedure-basics"></a>저장 프로시저 기본 사항

저장 프로시저는 문서와 속성에 대해 복잡한 트랜잭션을 수행합니다. 저장 프로시저는 JavaScript로 작성되며 Azure Cosmos DB의 컬렉션에 저장됩니다. 데이터와 인접한 위치에서 데이터베이스 엔진에 대해 저장 프로시저를 수행하면 클라이언트 쪽 프로그래밍을 사용할 때에 비해 성능을 개선할 수 있습니다.

Azure Cosmos DB 내에서 원자성 트랜잭션을 수행하는 방법은 저장 프로시저뿐입니다. 클라이언트 쪽 SDK는 트랜잭션을 지원하지 않습니다.

저장 프로시저에서 일괄 처리 작업을 수행하는 방식도 효율적입니다. 이렇게 하면 개별 트랜잭션을 더 적게 만들어도 되기 때문입니다.

<!--TODO: Ideally I'd like to list some cases where a stored procedure is not the best option.-->

## <a name="stored-procedure-example"></a>저장 프로시저 예제

다음 샘플은 현재 컨텍스트를 가져온 다음 “Hello, World”를 표시하는 응답을 보내는 간단한 HelloWorld 저장 프로시저입니다. 저장 프로시저에도 Azure Cosmos DB 문서처럼 ID 값이 있습니다.

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

## <a name="user-defined-function-basics"></a>사용자 정의 함수 기본 사항

UDF는 Azure Cosmos DB SQL 쿼리 언어 문법을 확장하고 사용자 지정 비즈니스 논리(예: 속성과 문서에 대한 계산)를 구현하는 데 사용됩니다. UDF는 쿼리 내에서만 호출할 수 있으며 저장 프로시저와는 달리 컨텍스트 개체에 액세스할 수 없으므로 문서를 읽거나 쓸 수 없습니다.

온라인 상거래 시나리오에서는 UDF를 사용하여 주문 총액에 적용할 판매세 또는 제품이나 주문에 적용할 할인율을 확인할 수 있습니다.

## <a name="user-defined-function-example"></a>사용자 정의 함수 예제

다음 샘플에서는 주문 총액 기준 할인액을 계산하는 UDF를 만든 다음 할인액에 따라 수정된 주문 총액을 반환합니다.

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

## <a name="create-a-stored-procedure-in-the-portal"></a>포털에서 저장 프로시저 만들기

그러면 포털에서 새 저장 프로시저를 만들어 보겠습니다. 포털에서는 컬렉션의 첫 번째 항목을 검색하는 단순한 저장 프로시저가 자동으로 입력되므로, 이 저장 프로시저를 먼저 실행해 보겠습니다.

1. 데이터 탐색기에서 **새 저장 프로시저**를 클릭합니다.

    데이터 탐색기에 샘플 저장 프로시저가 포함된 새 탭이 표시됩니다.

  <!--TODO: Insert animated .gif of creating the stored procedure.-->

2. **저장 프로시저 ID** 상자에 이름을 *sample*로 입력하고 **저장**, **실행**을 차례로 클릭합니다.


3. **입력 매개 변수** 상자에 파티션 키의 이름(*33218896*)을 입력한 다음 **실행**을 클릭합니다. 저장 프로시저는 단일 파티션 내에서 작동합니다.

    ![포털에서 저장 프로시저 실행](../media-draft/6-stored-procedure.gif)

    **결과** 창에 컬렉션의 첫 번째 문서에서 가져온 피드가 표시됩니다.

## <a name="create-a-stored-procedure-that-creates-documents"></a>문서를 만드는 저장 프로시저 만들기

이번에는 문서를 만드는 저장 프로시저를 만들어 보겠습니다.

1. 데이터 탐색기에서 **새 저장 프로시저**를 클릭합니다. 이 저장 프로시저의 이름을 *createDocuments*로 지정하고 **저장**, **실행**을 차례로 클릭합니다.

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

<!--TODO: Need to fix code above.-->

2. 파티션 키 값으로 *3*을 입력하고 **실행**을 클릭합니다.

    새로 만든 문서가 데이터 탐색기에 표시됩니다. 

## <a name="create-a-user-defined-function"></a>사용자 정의 함수 만들기

이제 데이터 탐색기에서 UDF를 만들어 보겠습니다.

데이터 탐색기에서 **새 UDF**를 클릭합니다. 다음 코드를 창에 복사하고 UDF 이름을 *tax*로 지정한 다음 **저장**을 클릭합니다. UDF는 포털에서는 실행할 수 없으며, 이후 모듈에서 사용할 것입니다.

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

