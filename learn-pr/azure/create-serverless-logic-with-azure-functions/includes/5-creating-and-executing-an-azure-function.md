지금까지 함수 앱을 만들었으므로 이제 Azure 함수를 빌드, 구성 및 실행하는 방법을 알아보겠습니다.

### <a name="triggers"></a>트리거

함수는 이벤트로 구동됩니다. 즉, 이벤트에 대한 응답으로 실행됩니다.

함수를 시작하는 이벤트 유형을 ‘트리거’라고 합니다. 정확히 하나의 트리거로 함수를 구성합니다.

 Azure는 다음 서비스에 대한 트리거를 지원합니다.


|서비스  |트리거 설명  |
|---------|---------|
|Blob Storage     |  새 BLOB 또는 업데이트된 BLOB이 검색될 때 함수를 시작합니다.       |
|Cosmos DB     |  삽입 및 업데이트가 검색될 때 함수를 시작합니다.      |
|Event Grid     |   Event Grid에서 이벤트를 수신할 때 함수를 시작합니다.       |
|HTTP     |   HTTP 요청으로 함수를 시작합니다.      |
|Microsoft Graph 이벤트     |  Microsoft Graph에서 들어오는 웹후크에 대한 응답으로 함수를 시작합니다. 이 트리거의 각 인스턴스는 한 가지 Microsoft Graph 리소스 종류에 대응할 수 있습니다.       |
|Queue Storage     |    큐에서 새 항목을 수신할 때 함수를 시작합니다. 큐 메시지는 함수에 입력으로 제공됩니다.      |
|Service Bus     |  Service Bus 큐의 메시지에 대한 응답으로 함수를 시작합니다.       |
|타이머     |  일정에 따라 함수를 시작합니다.       |
|Webhook     |  웹후크 요청으로 함수를 시작합니다.       |

### <a name="bindings"></a>바인딩

Azure Functions 바인딩은 데이터와 서비스를 함수에 연결하는 선언적인 방법입니다. 데이터 원본에 연결하고 연결을 관리하기 위해 함수에서 코드를 작성할 필요는 없습니다. 플랫폼은 복잡성을 관리합니다. 바인딩에는 방향이 있습니다. 코드는 ‘입력’ 바인딩에서 데이터를 읽고 ‘출력’ 바인딩에 데이터를 씁니다. 예제를 살펴보겠습니다.

Blob Storage에서 데이터를 읽으려면 *blob* 유형의 입력 바인딩을 구성합니다. Queue Storage에 메시지를 쓰려면 *queue* 유형의 출력 바인딩을 구성합니다.

지원되는 바인딩 및 트리거에 대한 자세한 내용은 [Azure 설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)를 참조하세요.

### <a name="a-sample-trigger-and-binding-functionjson"></a>샘플 트리거 및 바인딩(function.json)

다음 JSON은 함수에 대한 트리거 및 바인딩의 샘플 정의입니다.

```javascript
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

앞에서 언급했듯이 각 바인딩에는 입력 바인딩인지 아니면 출력 바인딩인지를 정의하는 지침이 있습니다. 트리거는 항상 입력 바인딩입니다. 이전 샘플은 **myqueue-items**라는 큐에 추가되는 메시지에 의해 트리거되는 함수를 보여 줍니다. 그런 다음, 함수의 반환 값을 Azure Table Storage의 **outTable** 테이블로 보냅니다.

## <a name="creating-a-function-in-the-azure-portal"></a>Azure Portal에서 함수 만들기

Azure는 일반 Azure 함수 시나리오에 대해 미리 구성된 템플릿을 제공합니다.

### <a name="quickstart-templates"></a>빠른 시작 템플릿

Azure 함수를 추가하려면 함수 앱을 선택해야 합니다. 함수 앱은 꺾쇠괄호 아이콘 내의 번개 모양으로 식별할 수 있습니다.  
![리소스 그룹에서 선택된 함수 앱을 보여 주는 스크린샷입니다.](../images/5-function-icon.png)

첫 번째 Azure 함수를 추가할 때 빠른 시작 화면이 표시됩니다. 이 화면에서는 트리거 유형 및 프로그래밍 언어를 선택할 수 있습니다. 그런 다음, 선택 사항에 따라 Azure는 함수 코드 및 구성을 생성합니다. 
 
![함수 빠른 시작](../images/5-quickstart-form.png)

### <a name="function-templates"></a>함수 템플릿

선택할 수 있는 템플릿은 빠른 시작에 표시되는 템플릿으로 제한되지 않습니다. 30개가 넘는 템플릿 중에서 선택할 수도 있습니다. 후속 함수를 만들거나 빠른 시작 화면에서 **사용자 지정 함수** 옵션을 선택하여 템플릿 목록 화면에 액세스할 수 있습니다.  
![premade 함수를 빠르게 시작하는 데 도움이 되는 Azure Functions 빠른 시작 사용자 인터페이스의 스크린샷입니다.](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>함수 및 파일 탐색

템플릿에서 함수를 만들면 여러 파일이 생성됩니다. 예를 들어, JavaScript를 사용하는 웹후크+API 빠른 시작을 사용하도록 선택하는 경우 구성 파일, **function.json** 및 소스 코드 파일인 **index.js** 파일이 생성됩니다. 함수 앱에서 생성하는 함수는 함수 앱 포털의 함수 메뉴 항목 아래에 표시됩니다.

함수 앱에서 함수를 선택하면 다음 스크린샷에 설명된 대로 코드 편집기가 열리고 함수에 대한 코드가 표시됩니다.

![함수 개발 속도를 높이기 위해 사용할 수 있는 템플릿 세트를 나열하는 함수 템플릿 선택 인터페이스를 보여 주는 스크린샷입니다.](../images/5-file-navigation.png)

이전 스크린샷에서 볼 수 있듯이 오른쪽에 **파일 보기**에 대한 탭을 포함하는 플라이아웃 메뉴가 있습니다. 이 탭을 선택하면 함수를 구성하는 파일 구조가 표시됩니다.  

## <a name="execution-options-for-testing-your-azure-function"></a>Azure 함수 테스트를 위한 실행 옵션입니다.

함수가 생성되면 이를 테스트하게 됩니다. 수동 실행, Azure Portal 내에서 테스트 등 몇 가지 방법이 있습니다.

### <a name="manual-execution-of-a-function"></a>함수의 수동 실행

구성된 트리거를 수동으로 트리거하여 함수를 시작할 수 있습니다. 예를 들어 HttpTrigger를 사용하는 경우 Postman이나 cURL과 같은 도구를 사용하여 함수 엔드포인트 URL에 대한 HTTP 요청을 시작할 수 있습니다.  

![URL 필드에 함수 URL이 입력되어 있고 요청 본문이 샘플 본문으로 채워진 Postman 응용 프로그램 인터페이스의 부분 스크린샷입니다. ](../images/5-postman-execution.png)

엔드포인트 URL을 가져오려면 왼쪽 탐색에서 HTTP 트리거를 선택한 후 **함수 URL 가져오기**  단추를 선택합니다.  

![함수 앱 포털에서 함수가 선택되어 있고 페이지 맨 위에서 *함수 URL 가져오기* 작업이 선택된 스크린샷입니다.](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Azure Portal에서 함수 테스트

포털은 또한 함수를 테스트하는 편리한 방법을 제공합니다. 코드 창의 오른쪽에는 플라이아웃 탭 방식의 탐색 메뉴가 있습니다. 이 메뉴에 **테스트** 항목이 있습니다. 메뉴를 확장하고 이 탭을 선택하면 함수를 실행하고 결과를 볼 수 있습니다. HttpTrigger 시나리오를 사용하여 HTTP 메서드를 설정하고 쿼리 문자열 매개 변수 및 HTTP 헤더를 요청에 추가할 수 있습니다. 또한 추가 시나리오를 테스트하도록 요청 본문을 변경할 수도 있습니다. 다음 예제에서 테스트는 이름이 *name*이라는 하나의 매개 변수가 포함된 요청 본문이 있는 HTTP POST 요청으로 구성됩니다.
 
![HTTP POST 요청 및 샘플 요청 본문을 표시하는 함수 앱 포털에 있는 테스트 창의 스크린샷입니다. 출력 창에는 “Hello Azure”라는 단어가 있는 함수 호출의 결과가 포함되어 있습니다.](../images/5-portal-execution.png)

이 테스트 창에서 **실행**을 클릭하면 결과가 상태 코드와 함께 출력 창에 표시됩니다. 

## <a name="monitoring-an-azure-function"></a>Azure 함수 모니터링

메시지를 로그하고 함수를 모니터하는 기능은 개발 과정과 프로덕션에서 매우 중요합니다. Azure Portal은 모니터링 대시보드뿐만 아니라 Azure Functions에서 가져온 실행 로그 및 예외를 검토하는 방법도 제공합니다.

### <a name="log-window"></a>로그 창

또한 함수에 로그 문을 추가할 수 있습니다. 이 문은 함수의 로그 창에 표시됩니다. 로그 창은 코드 창의 맨 아래에 있는 탭 방식의 플라이아웃 메뉴에 있습니다. 다음 JavaScript 코드 조각은 `context.log` 메서드를 사용하여 메시지를 로그하는 방법을 보여 줍니다.

```javascript
  context.log('Enter your logging statement here');
```  

![Azure Functions 사용자 인터페이스의 코드 편집기 섹션 스크린샷입니다. context.log() 메서드를 사용하여 로그 창에 메시지를 로그하는 코드 줄도 강조 표시됩니다.](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>오류 및 경고 창

로그 창과 동일한 플라이아웃 메뉴에서 오류 및 경고 창 탭을 찾을 수 있습니다. 이 창에는 코드 내의 컴파일 오류 및 경고가 표시됩니다. JavaScript는 동적이며 해석되는 언어이므로 다음 이미지는 C# 함수의 컴파일 오류를 표시합니다.  

![화면 맨 아래에서 **로그** 창이 강조 표시되어 있는 Azure Functions 사용자 인터페이스의 코드 편집기 섹션 스크린샷입니다.](../images/5-errors-window.png)

### <a name="monitoring-dashboard"></a>모니터링 대시보드

함수 앱 탐색 메뉴에서 함수 노드를 확장하면 **모니터** 메뉴 항목이 표시됩니다. 모니터 대시보드는 함수 실행의 기록을 보기 위한 빠른 방법을 제공합니다. 이 보기에는 성공적인 완료 여부는 물론 타임스탬프, 결과 코드, 지속 기간 및 작업 ID도 표시됩니다. Azure Application Insights를 통해 데이터가 채워집니다.  

![함수에 대한 성공적인 호출 및 실패한 호출의 목록을 보여 주는 **모니터** 함수 메뉴 항목을 통해 실행된 모니터링 대시보드의 스크린샷입니다.](../images/5-monitor-function.png)
