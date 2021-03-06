마지막 연습에서는 Azure Cosmos DB 데이터베이스에서 책갈피를 조회하는 시나리오를 구현했습니다. 책갈피 컬렉션에서 데이터를 읽도록 입력 바인딩을 구성했습니다. 그러나 더 많은 것을 수행할 수 있습니다. 이제 쓰기를 포함하도록 시나리오를 확장해 보겠습니다. 다음 순서도를 사용하는 것이 좋습니다.

![Cosmos DB 백 엔드에서 책갈피를 찾는 프로세스를 보여 주는 흐름 다이어그램입니다. Azure 함수는 책갈피 ID가 있는 요청을 받을 때 오류 응답이 생성되지 않으면 먼저 요청이 유효한지 확인합니다. 유효한 요청의 경우 함수는 책갈피 ID가 Cosmos DB에 있는지 확인하고, 없으면 오류 응답이 생성됩니다. 책갈피 ID가 있으면 성공 응답이 생성됩니다.](../media/7-add-bookmark-flow-small.png)

이 시나리오에서는 책갈피를 컬렉션에 추가하라는 요청을 받게 됩니다. 요청은 책갈피 URL과 함께 원하는 키 또는 ID를 전달합니다. 순서도에서 볼 수 있듯이 키가 이미 백 엔드에 있는 경우 오류로 응답합니다.

전달된 키가 *없으면* 새 책갈피를 데이터베이스에 추가합니다. 여기서 중지할 수 있지만 조금 더 수행해 보겠습니다.

순서도에서 또 다른 단계가 눈에 띄나요? 지금까지 처리 측면에서 받는 데이터를 별로 다루지 않았습니다. 받는 데이터를 데이터베이스로 이동합니다. 그러나 실제 솔루션에서는 특정 방식으로 데이터를 처리할 수도 있습니다. 동일한 함수에서 모두 처리하도록 결정할 수 있지만, 이 랩에서는 추가 처리를 다른 구성 요소 또는 비즈니스 논리 부분으로 오프로드하는 패턴을 보여 줍니다.

책갈피 시나리오에서 이러한 작업 오프로딩의 좋은 예는 무엇일까요? 그렇다면, 새 책갈피를 QR 코드 생성 서비스로 보내면 어떨까요? 이 경우 해당 서비스에서 URL에 대한 QR 코드를 생성하고, 이미지를 Blob 저장소에 저장하고, QR 이미지의 주소를 책갈피 컬렉션의 항목에 다시 추가합니다. QR 이미지를 생성하는 서비스를 호출하는 경우 시간이 많이 걸리므로 결과를 기다리는 대신 해당 결과를 함수에 전달하여 비동기적으로 처리하도록 합니다.

Azure Functions에서 다양한 통합 원본에 대한 입력 바인딩을 지원하는 것처럼 데이터 원본에 데이터를 쉽게 쓸 수 있도록 하는 일단의 출력 바인딩 템플릿도 있습니다. 출력 바인딩은 *function.json* 파일에도 구성됩니다.  이 연습에서 살펴보겠지만 함수는 다중 데이터 원본 및 서비스를 사용하도록 구성할 수 있습니다.

> [!IMPORTANT]
> 이 연습은 이전 연습을 기반으로 합니다. 동일한 Azure Cosmos DB 데이터베이스 및 입력 바인딩을 사용합니다. 해당 단원을 수행하지 않은 경우 이 단원을 진행하기 전에 수행하는 것이 좋습니다.

## <a name="create-an-http-triggered-function"></a>HTTP-triggered 함수 만들기

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

2. Azure Portal의 해당 모듈에서 만든 함수 앱으로 이동합니다.

3. 함수 앱을 확장한 다음, 함수 컬렉션 위에 마우스를 놓고, **함수** 옆에 있는 추가(**+**) 단추를 선택합니다. 이 작업은 함수 만들기 프로세스를 시작합니다. 다음 애니메이션에서는 이 작업을 보여 줍니다.

    ![사용자가 함수 메뉴 항목을 마우스로 가리키면 표시되는 더하기 기호의 애니메이션](../media/3-func-app-plus-hover-small.gif)

4. 이 페이지에는 지원되는 트리거의 현재 집합을 보여 줍니다. 다음 스크린샷의 첫 번째 항목인 **HTTP 트리거**를 선택합니다.

    ![이미지의 왼쪽 위에 TTP 트리거가 먼저 표시된 트리거 템플릿 선택 UI 일부의 스크린샷.](../media/5-trigger-templates-small.PNG)


5. 다음 값을 사용하여 오른쪽에 표시되는 **새 함수** 창을 채웁니다.

    |필드  |값  |
    |---------|---------|
    |언어     | **JavaScript**        |
    |이름     |   [!INCLUDE [func-name-add](./func-name-add.md)]     |
    | 권한 부여 수준 | **Function** |

6. **만들기**를 선택하여 사용자의 함수를 만듭니다. 이 작업은 코드 편집기에서 **index.js** 파일을 열고 HTTP 트리거 함수의 기본 구현을 표시합니다.

    > [!NOTE]
    > 이 연습에서는 이전 단원의 *코드*와 *구성*을 시작 지점으로 사용하여 작업 속도를 높입니다.

7. **index.js** 파일의 모든 코드를 다음 코드 조각의 코드로 바꾼 다음, **저장**을 선택하여 변경 내용을 저장합니다.

   [!code-javascript[](../code/find-bookmark-single.js)]

   이 코드가 익숙해 보인다면 이는 [!INCLUDE [func-name-find](./func-name-find.md)] 함수를 구현했기 때문입니다. 예상한 대로 함수는 동일한 바인딩을 정의할 때까지 작동하지 않습니다.

1. [!INCLUDE [func-name-add](./func-name-add.md)] 함수에서 **function.json** 파일을 엽니다.

11. 이 파일 내용을 다음 JSON으로 바꿉니다.

    ```json
    {
      "bindings": [
        {
          "authLevel": "function",
          "type": "httpTrigger",
          "direction": "in",
          "name": "req"
        },
        {
          "type": "http",
          "direction": "out",
          "name": "res"
        },
        {
          "type": "documentDB",
          "name": "bookmark",
          "databaseName": "func-io-learn-db",
          "collectionName": "Bookmarks",
          "connection": "unit3test_DOCUMENTDB",
          "direction": "in",
          "id": "{id}"
        }
      ],
      "disabled": false
    }
    ```

12. 모든 변경 내용을 **저장**해야 합니다.

이전 단계에서는 다른 함수에서 바인딩 정의를 복사하여 새 함수에 대한 바인딩을 구성했습니다. 물론 UI를 통해 새 바인딩을 만들 수도 있지만, 이 대안을 사용할 수 있음을 이해하는 것이 좋습니다.

## <a name="try-it-out"></a>사용해 보기

1. 오른쪽 맨 위에서 **함수 URL 가져오기**를 선택하고 **기본값(함수 키)** 을 선택한 다음, **복사**를 선택하여 함수의 URL을 복사합니다.

2. 복사한 URL을 브라우저의 주소 표시줄에 붙여넣습니다. URL의 끝에 `&id=docs` 쿼리 문자열 값을 추가한 다음, Enter 키를 눌러 요청을 실행합니다. 모든 작업이 잘 진행되면 해당 리소스에 대한 URL이 포함된 응답이 표시됩니다.

그러면 지금은 어디에 있을까요? 글쎄요, 지금까지 이전 랩에서 수행했던 것을 그대로 복제했을 뿐입니다. 하지만 괜찮습니다. 이 작업의 시작 지점으로 사용하기 위해 마지막 랩에서 수행한 것을 복사합니다. 다음에 새로운 기능을 다룰 것입니다. 즉, 데이터베이스에 작성할 것입니다. 이를 위해 *출력 바인딩*이 필요합니다.

## <a name="define-azure-cosmos-db-output-binding"></a>Azure Cosmos DB 출력 바인딩 정의

사용자 인터페이스를 통해 새 출력 바인딩을 정의하는 대신, 구성 파일 *function.json*을 직접 업데이트하여 이 바인딩을 만듭니다.

1. [!INCLUDE [func-name-add](./func-name-add.md)]에 대한 *function.json* 파일이 편집기에서 열려 있는지 확인합니다.

1. 해당 파일에서 이름이 `bookmark`인 바인딩을 복사합니다.

1. 닫는 중괄호(}) 바로 뒤에 커서를 놓고 닫는 대괄호(]) 바로 앞에 커서를 놓습니다. 쉼표(,)를 추가한 다음, 여기에 바인딩의 복사본을 붙여넣습니다. *function.json* 구성 파일은 이제 다음과 같이 표시됩니다.

   [!code-json[](../code/config-new-entry.json?highlight=22-31)]

1. 다음과 같은 변경 내용으로 붙여넣은 바인딩을 편집합니다.

    |속성   |이전 값  |새 값  |
    |---------|---------|---------|
    |name     |   bookmark      |  **newbookmark**       |
    |direction     |   in      |   **out**      |
    |id     |      {id}   |   **이 속성은 삭제합니다. 출력 바인딩에는 존재하지 않기 때문입니다.**      |

1. 이렇게 변경한 후에 파일이 다음 JSON과 같이 표시됩니다.

    [!code-json[](../code/config-q-complete.json?highlight=22-30)]

이는 구성 파일에서 직접 바인딩을 만드는 방법을 보여 주는 데모일 뿐입니다. 이 예제에서는 다른 바인딩의 속성을 다시 사용하기 때문에 의미가 있습니다. 즉, Azure Cosmos DB 입력 바인딩에 대해 이미 구성한 `databaseName`, `collectionName` 및 `connection`을 재사용하고 있습니다.

> [!NOTE]
> 앞의 JSON 파일에서 `connection`의 실제 값은 연결을 만들 때 지정한 연결 이름입니다.

코드를 업데이트하기 전에 큐에 메시지를 게시할 수 있게 하는 바인딩을 하나 더 추가해 보겠습니다.

## <a name="define-azure-queue-storage-output-binding"></a>Azure Queue Storage 출력 바인딩 정의

Azure Queue 저장소는 전 세계 어디서나 액세스할 수 있는 메시지를 저장하는 서비스입니다. 단일 메시지의 크기는 최대 64KB까지 가능하며, 큐에는 정의된 저장소 계정의 총 용량 한도까지 수백만 개의 메시지&mdash;가 포함될 수 있습니다. 다음 다이어그램에서는 이 시나리오에서 큐를 사용하는 방법을 개략적으로 보여 줍니다.

![저장소 큐 및 두 개의 함수 중 하나에 푸시하고 큐에 다른 팝업 메시지를 보여 주는 일러스트레이션](../media/7-q-logical-small.png)

여기에서 새 [!INCLUDE [func-name-add](./func-name-add.md)] 함수에서 메시지를 큐에 추가하는 것을 볼 수 있습니다. 다른 함수, &mdash;예를 들어 *gen-qr-code*라는 가상의 함수&mdash;는 동일한 큐에서 메시지를 팝하고 요청을 처리합니다.  [!INCLUDE [func-name-add](./func-name-add.md)]에서 큐에 메시지를 쓰거나 *푸시*하므로 솔루션에 새 출력 바인딩을 추가합니다. 이번에는 포털 UI를 통해 바인딩을 만들어 보겠습니다.

1. 왼쪽 함수 메뉴에서 **통합**을 선택하여 통합 탭을 엽니다.

2. **출력** 열에서 **새 출력**을 선택합니다.
    가능한 모든 출력 바인딩 형식 목록이 표시됩니다.

3. 목록에서 **Azure Queue Storage**를 선택한 다음, **선택**을 선택합니다.
    그러면 Azure Queue Storage 출력 구성 페이지가 열립니다.

   다음으로, 저장소 계정 연결을 설정합니다. 여기서 큐가 호스팅됩니다.

4. **저장소 계정 연결** 필드의 오른쪽에 있는 **새로 만들기**을 선택합니다.
   **저장소 계정** 선택 창이 열립니다.

5. 이 모듈을 시작하고 함수 앱을 만들었을 때 저장소 계정도 만들어졌습니다. 이 창에 나열되어 있으므로 선택합니다. **저장소 계정 연결** 필드가 연결 이름으로 채워집니다. 연결 문자열 값을 보려면 **값 표시**를 선택합니다.

6. 다른 모든 필드에 기본값을 그대로 둘 수 있지만 다음 항목을 변경하여 속성에 더 많은 의미를 부여할 수 있습니다.

    |속성  |이전 값  |새 값  | 설명 |
    |---------|---------|---------|---------|
    |큐 이름     |    outqueue     |  **bookmarks-post-process**      | 책갈피를 배치하여 다른 함수에서 추가로 처리할 수 있도록 하는 큐의 이름입니다. |
    | 메시지 매개 변수 이름    |  outputQueueItem       |   **newmessage**      | 코드에서 사용할 바인딩 속성입니다. |

7. **저장**을 선택하여 변경 내용을 저장합니다.

## <a name="update-function-implementation"></a>업데이트 함수 구현

이제 [!INCLUDE [func-name-add](./func-name-add.md)] 함수에 대한 모든 바인딩이 설정되었습니다. 함수에서 이러한 바인딩을 사용할 차례입니다.

1.  [!INCLUDE [func-name-add](./func-name-add.md)] 함수를 선택하여 코드 편집기에서 **index.js** 파일을 엽니다.

2. *index.js* 파일의 모든 코드를 다음 코드 조각의 코드로 바꿉니다.

   [!code-javascript[](../code/add-bookmark.js)]

이 코드의 기능을 분석해 보겠습니다.

* 이 함수는 데이터를 변경하므로 HTTP 요청이 POST이고 책갈피 데이터가 요청 본문에 포함될 것으로 예상합니다.
* Azure Cosmos DB 입력 바인딩은 수신한 `id`를 사용하여 문서 또는 책갈피를 검색하려고 시도합니다. 항목을 찾으면 `bookmark` 개체가 설정됩니다. `if(bookmark)` 조건은 항목이 있는지 여부를 확인합니다.
* 데이터베이스에 추가하는 것은 `context.bindings.newbookmark` 바인딩 매개 변수를 JSON 문자열로 만든 새 책갈피 항목으로 설정하는 것만큼 간단합니다.
* 메시지를 큐에 게시하는 것은 `context.bindings.newmessage parameter`를 설정하는 것만큼 간단합니다.

> [!NOTE]
> 수행한 유일한 작업은 큐 바인딩을 만드는 것이었습니다. 큐는 명시적으로 만들지 않았습니다. 지금 바인딩의 능력을 목격하고 있습니다. 다음 설명선에서 볼 수 있듯이 큐가 없으면 자동으로 만들어집니다.

![큐를 자동으로 만들도록 호출하는 스크린샷.](../media/7-q-auto-create-small.png)

이것으로 끝입니다. 다음 섹션에서 진행 중인 작업을 살펴보겠습니다.

## <a name="try-it-out"></a>사용해 보기

이제 여러 개의 출력 바인딩이 있으므로 테스트가 좀 더 까다로워졌습니다. 이전 랩에서는 HTTP 요청과 쿼리 문자열을 보내 테스트하는 데 만족했지만 이번에는 HTTP 게시를 수행하려고 합니다. 또한 메시지에서 이 게시를 큐에 넣는지 확인해야 합니다.

1. 함수 앱 포털에서 선택한 [!INCLUDE [func-name-add](./func-name-add.md)] 함수를 사용하여 맨 왼쪽에 있는 테스트 메뉴 항목을 선택하여 확장합니다.

2. **테스트** 메뉴 항목을 선택하고, 테스트 창이 열려 있는지 확인합니다. 다음 스크린샷에서는 다음과 같이 표시되는 것을 보여 줍니다.

    ![확장된 함수 테스트 패널을 보여주는 스크린샷.](../media/7-test-panel-open-small.png)

    > [!IMPORTANT]
    > HTTP 메서드 드롭다운 목록에서 **POST**가 선택되어 있는지 확인합니다.

3. 요청 본문의 내용을 다음 JSON 페이로드로 바꿉니다.

    ```json
    {
        "id": "docs",
        "url": "https://docs.microsoft.com/azure"
    }
    ```

4. 테스트 창 아래쪽에서 **실행**을 선택합니다.

5. 다음 다이어그램에 표시된 대로 **출력** 창에 "책갈피가 이미 존재함"이라는 메시지가 표시되는지 확인합니다.

    ![테스트 패널 및 실패한 테스트의 결과를 보여 주는 스크린샷.](../media/7-test-exists-small.png)

6. 요청 본문을 다음 페이로드로 바꿉니다.

    ```json
    {
        "id": "github",
        "url": "https://www.github.com"
    }
    ```
7. 테스트 창 아래쪽에서 **실행**을 선택합니다.

8. 다음 다이어그램에 표시된 대로 *출력* 상자에 "책갈피 추가됨"이라는 메시지가 표시되는지 확인합니다.

    ![테스트 패널 및 성공한 테스트의 결과를 보여 주는 스크린샷](../media/7-test-success-small.png)

축하합니다! [!INCLUDE [func-name-add](./func-name-add.md)]는 설계한 대로 작동하지만 코드에 있던 큐 작업은 어떨까요? 그럼, 큐에 어떤 것이 쓰여 있는지 살펴보겠습니다.

### <a name="verify-that-a-message-is-written-to-the-queue"></a>메시지가 큐에 쓰여 있는지 확인합니다.

Azure Queue Storage 큐는 저장소 계정에서 호스팅됩니다. 이 연습에서는 출력 바인딩을 만들 때 이미 저장소 계정을 선택했습니다.

1. Azure Portal의 기본 검색 상자에서 **저장소 계정**을 입력하고, 결과 목록의 **서비스**에서 **저장소 계정**을 선택합니다.

      ![기본 검색 상자에서 저장소 계정에 대한 검색 결과를 보여 주는 스크린샷.](../media/7-search-for-sa-small.png)

2. 반환된 저장소 계정 목록에서 **newmessage** 출력 바인딩을 만드는 데 사용한 저장소 계정을 선택합니다.
   저장소 계정 설정은 포털의 주 창에 표시됩니다.

3. **서비스** 목록에서 **큐** 항목을 선택합니다.
   이 저장소 계정에서 호스팅하는 큐의 목록이 표시됩니다. 다음 스크린샷과 같이 **bookmarks-post-process** 큐가 있는지 확인합니다.

      ![이 저장소 계정에서 호스팅하는 큐 목록에서 큐를 보여 주는 스크린샷](../media/7-q-in-list-small.png)

4. **bookmarks-post-process**를 선택하여 큐를 엽니다.
   큐에 있는 메시지가 목록에 표시됩니다. 모두 계획에 따라 진행된 경우, 데이터베이스에 책갈피를 추가할 때 게시한 메시지가 큐에 포함됩니다. 다음과 같아야 합니다.

    ![큐의 메시지를 보여 주는 스크린샷](../media/7-message-in-q-small.png)

   이 예제에서는 메시지에 고유한 ID가 지정되어 있고 **메시지 텍스트** 필드에 책갈피가 JSON 문자열 형식으로 표시된다는 것을 알 수 있습니다.

5. 테스트 창에서 요청 본문을 새 ID/URL 집합으로 변경하고 함수를 실행하여 함수를 추가로 테스트할 수 있습니다. 이 큐를 조사하여 더 많은 메시지가 도착하는지 확인합니다. 데이터베이스를 보고 새 항목이 추가되었는지 확인할 수도 있습니다.

이 랩에서는 바인딩 지식을 출력 바인딩으로 확장하고 Azure Cosmos DB에 데이터를 작성했습니다. 더 나아가 Azure 큐에 메시지를 게시하는 또 다른 출력 바인딩을 추가했습니다. 여기서는 들어오는 원본에서 데이터를 만들고 다양한 대상으로 이동하는 데 도움이 되는 바인딩의 진정한 능력을 보여 주었습니다. 데이터베이스 코드를 작성하지 않았거나 연결 문자열을 직접 관리해야 했습니다. 대신 바인딩을 선언적으로 구성하고 플랫폼이 연결 보안, 함수 크기 조정 및 연결 크기 조정을 처리하도록 했습니다.