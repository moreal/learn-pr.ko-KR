Azure Cosmos DB는 서버를 사용하지 않는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스입니다. 이 모듈에서는 Azure Functions를 사용하여 Azure Cosmos DB에서 JSON 문서로 이미지 메타데이터를 저장하고 검색하는 방법을 알아봅니다.

## <a name="create-an-azure-cosmos-db-account-database-and-collection"></a>Azure Cosmos DB 계정, 데이터베이스 및 컬렉션 만들기

Azure Cosmos DB 계정은 Azure Cosmos DB 데이터베이스를 포함하는 Azure 리소스입니다.

1. Cloud Shell에 로그인했는지 확인합니다. 그러지 않은 경우 **포커스 모드로 전환**을 선택하여 Cloud Shell 창을 엽니다. 

1. 이 자습서의 다른 리소스와 동일한 리소스 그룹에서 고유한 이름을 사용하여 Azure Cosmos DB 계정을 만듭니다.

    ```azurecli
    az cosmosdb create -g <rgn>[Sandbox resource group name]</rgn> -n <cosmos db account name>
    ```

1. Azure Cosmos DB 계정을 만든 후에 계정에서 **imagesdb**라는 새 데이터베이스를 만듭니다.

    ```azurecli
    az cosmosdb database create -g <rgn>[Sandbox resource group name]</rgn> -n <cosmos db account name> --db-name imagesdb
    ```

1. 데이터베이스를 만든 후에 데이터베이스에서 400RU(요청 단위)의 처리량을 가진 **images**라는 새 컬렉션을 만듭니다.

    ```azurecli
    az cosmosdb collection create -g <rgn>[Sandbox resource group name]</rgn> -n <cosmos db account name> --db-name imagesdb --collection-name images --throughput 400
    ```


## <a name="save-a-document-to-azure-cosmos-db-when-a-thumbnail-is-created"></a>썸네일을 만들 때 Azure Cosmos DB에 문서를 저장합니다.

Azure Cosmos DB 출력 바인딩을 통해 Azure Functions의 Azure Cosmos DB 컬렉션에서 문서를 만들 수 있습니다. 다음 단계에서는 **ResizeImage** 함수에서 Azure Cosmos DB 출력 바인딩을 구성하고, 저장할 문서(개체)를 반환하도록 함수를 수정합니다.

1. 함수 앱을 엽니다는 [Azure portal](https://portal.azure.com/?azure-portal=true)합니다.

1. 왼쪽 탐색에서 **ResizeImage** 함수를 확장한 다음, **통합**을 선택합니다.

1. **출력**에서 **새 출력**을 클릭합니다.

1. **Azure Cosmos DB** 항목을 찾아 선택합니다. 그런 다음, **선택**을 클릭합니다.

    ![새 출력 선택](../media/4-new-output.jpg)

1. 다음 값으로 **Azure Cosmos DB 출력** 아래에 있는 필드를 채웁니다.

    | 설정      |  제안 값   | 설명                                        |
    | --- | --- | ---|
    | **문서 매개 변수 이름** | **함수 반환 값 사용**을 선택합니다. | 상자의 값은 자동으로 **$return**으로 설정됩니다. |
    | **데이터베이스 이름** | imagesdb | 사용자가 만든 데이터베이스의 이름을 사용합니다. |
    | **컬렉션 이름** | images | 사용자가 만든 컬렉션의 이름을 사용합니다. |

1. **Azure Cosmos DB 계정 연결** 옆에 있는 **새로 만들기**를 클릭합니다. 이전에 만든 Azure Cosmos DB 계정을 선택합니다.

    ![Azure Cosmos DB 출력 바인딩에 대한 설정 입력](../media/4-cosmos-db-output.png)

1. **저장**을 클릭하여 Azure Cosmos DB 출력 바인딩을 만듭니다.

1. 왼쪽에서 **ResizeImage** 함수 이름을 클릭하여 함수를 엽니다.

::: zone pivot="csharp"
1. (C#) 함수의 반환 형식을 **void**에서 **object**로 변경합니다.

1. (C#) 함수 끝에서 다음 코드 블록을 추가하여 저장할 문서를 반환합니다.

    ```csharp
    return new {
        id = name,
        imgPath = "/images/" + name,
        thumbnailPath = "/thumbnails/" + name
    };
    ```

    ![수정 후 ResizeImages 함수의 run.csx](../media/4-update-function.png)

::: zone-end

::: zone pivot="javascript"
1. (JavaScript) `else` 절에서 `context.done()` 문을 변경하여 Azure Cosmos DB에 저장할 문서를 반환합니다.

    ```javascript
    if (error) {
        context.done(error);
    } else {
        context.bindings.thumbnail = stream;
        context.done(null, {
            id: context.bindingData.name,
            imgPath: "/images/" + context.bindingData.name,
            thumbnailPath: "/thumbnails/" + context.bindingData.name
        });
    }
    ```

::: zone-end

1. 코드 창 아래에서 **로그**를 클릭하여 [로그] 패널을 확장합니다.

1. **저장**을 클릭합니다. [로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.

## <a name="create-a-function-to-list-images-from-azure-cosmos-db"></a>Azure Cosmos DB에서 이미지를 나열하는 함수 만들기

Azure Cosmos DB에서 이미지 메타데이터를 검색하기 위해 웹 응용 프로그램에는 API가 필요합니다. 다음 단계에서는 Azure Cosmos DB 입력 바인딩을 사용하는 HTTP 트리거 함수를 만들어서 데이터베이스 컬렉션을 쿼리합니다.

1. 함수 앱에서 왼쪽에 있는 **함수**를 가리키고 더하기 기호(+)를 클릭하여 새 함수를 만듭니다.

1. **HttpTrigger** 템플릿을 찾아 선택합니다.

1. 이러한 값을 사용하여 이미지 가져오기 URL을 생성하는 함수를 만듭니다.

    | 설정      |  제안 값   | 설명                                        |
    | --- | --- | ---|
    | **함수 이름 지정** | GetImages | 응용 프로그램이 함수를 검색할 수 있도록 표시된 대로 이 이름을 정확히 입력합니다. |
    | **권한 부여 수준** | 익명 | 함수가 공개적으로 액세스될 수 있습니다. |

1. **만들기**를 클릭합니다.

1. 새 함수를 만들면 왼쪽 탐색에 있는 함수의 이름에서 **통합**을 클릭합니다.

1. **새 입력**을 클릭하고 **Azure Cosmos DB**를 선택합니다. 

    ![새 입력 선택](../media/4-new-input.jpg)

1. **선택**을 클릭합니다.

1. 다음 값을 입력합니다.

    | 설정      |  제안 값   | 설명                                        |
    | --- | --- | ---|
    | **문서 매개 변수 이름** | documents | 함수에서 매개 변수 이름과 일치합니다. |
    | **데이터베이스 이름** | imagesdb |  |
    | **컬렉션 이름** | images |  |
    | **SQL 쿼리** | select * from c order by c._ts desc | 먼저 최신 문서를 가져옵니다. |
    | **Azure Cosmos DB 계정 연결** | 기존 연결 문자열을 선택합니다. |  |

1. **저장**을 클릭하여 입력 바인딩을 만듭니다.

::: zone pivot="csharp"

1. 함수 이름을 클릭하여 코드 창을 엽니다. **run.csx** 파일의 모든 내용을 [**/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx) 파일의 콘텐츠로 바꿉니다.

::: zone-end

::: zone pivot="javascript"

1. 함수 이름을 클릭하여 코드 창을 엽니다. **index.js** 파일의 모든 내용을 [**/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js) 파일의 콘텐츠로 바꿉니다.

::: zone-end

1. 코드 창 아래에서 **로그**를 클릭하여 [로그] 패널을 확장합니다.

1. **저장**을 클릭합니다. [로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.

## <a name="test-the-application"></a>응용 프로그램 테스트

1. 브라우저에서 응용 프로그램을 엽니다. 이미지 파일을 선택하고 업로드합니다.

1. 몇 초 후에 새 이미지의 썸네일이 페이지에 표시됩니다.

1. Azure Portal에서 **검색** 상자를 사용하여 이름으로 Azure Cosmos DB 계정을 검색합니다. 이름을 클릭하여 계정을 엽니다.

1. 왼쪽에서 **데이터 탐색기**를 클릭하여 컬렉션 및 문서를 찾아봅니다.

1. **imagesdb** 데이터베이스 아래에서 **images** 컬렉션을 선택합니다.

1. 업로드된 이미지에 대한 문서가 생성되었는지 확인합니다.

    ![업로드된 이미지에 대한 문서를 표시하는 데이터 탐색기](../media/4-data-explorer.png)

## <a name="summary"></a>요약

이 단원에서는 Azure Cosmos DB 계정, 데이터베이스 및 컬렉션을 만드는 방법을 알아보았습니다. Azure Cosmos DB 바인딩을 사용하여 Azure Cosmos DB 컬렉션에서 이미지 메타데이터를 저장하고 검색하는 방법을 알아보았습니다. 다음으로, Microsoft Cognitive Services를 사용 하 여 각 업로드 된 이미지에 대 한 캡션을 자동으로 생성 하는 방법을 배웁니다.