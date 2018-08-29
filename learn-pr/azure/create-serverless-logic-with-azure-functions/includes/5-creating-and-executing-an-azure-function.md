지금까지 함수 앱을 만들었으므로 이제 Azure 함수를 빌드, 구성 및 실행하는 방법을 알아보겠습니다.

### <a name="triggers"></a>트리거
Azure 함수는 이벤트 기반이며, HTTP 요청 또는 큐에 메시지 추가 등의 이벤트에 응답하여 실행됩니다. 

함수를 시작하는 이벤트 유형을 트리거라고 합니다. Azure 함수를 사용하려면 하나 이상의 트리거를 구성해야 합니다. 이것 외에는 함수를 실행하는 방법이 없습니다.

 Azure는 다음을 포함한 광범위한 트리거를 지원합니다.
* HTTPTrigger
* TimerTrigger
* GitHub 웹후크
* CosmosDBTrigger
* BlobTrigger
* QueueTrigger
* EventHubTrigger
* ServiceBusQueueTrigger
* ServiceBusTopicTrigger

### <a name="bindings"></a>바인딩
Azure 함수 바인딩은 데이터를 함수에 프로그래밍 방식으로 연결하는 선언적인 방법입니다.

바인딩은 데이터 서비스에 대한 연결입니다. 0, 1 또는 그 이상의 바인딩이 있는 Azure 함수를 사용하면 여러 데이터 원본에 액세스할 수 있습니다. 이를 입력 또는 출력 바인딩으로 정의하거나 읽기 또는 쓰기 바인딩으로 생각할 수도 있습니다.

Blob이 큐에 추가될 때 함수를 시작하는 QueueTrigger가 있다고 가정해 보겠습니다. 입력 Blob 바인딩은 Azure Blob Storage에 연결하는 데 사용됩니다. 

출력 바인딩은 데이터를 저장하는 데 사용됩니다. 예를 들어 함수의 반환 값을 Azure Table Storage로 보냅니다.

사용 가능한 바인딩의 전체 목록은 [Azure 설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)에서 확인할 수 있습니다.

### <a name="a-sample-trigger-and-binding-functionjson"></a>샘플 트리거 및 바인딩(function.json)
이는 함수에 대한 트리거 및 바인딩의 샘플 정의입니다. 설명하는 바인딩 유형에 따라 설정해야 하는 속성 값이 달라집니다. 각 바인딩에는 입력 바인딩인지 아니면 출력 바인딩인지를 정의하는 지침도 있습니다. 트리거는 항상 입력 바인딩입니다. 이 샘플은 **myqueue-items**라는 큐에 추가되는 메시지에 의해 트리거되는 함수를 보여줍니다. 그런 다음, 함수의 반환 값을 Azure Table Storage의 **outTable** 테이블로 보냅니다.

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
## <a name="premade-functions-and-templates"></a>기본 제공 함수 및 템플릿
Azure는 일반 Azure 함수 시나리오에 대해 미리 구성된 템플릿을 제공합니다.

### <a name="quickstart-templates"></a>빠른 시작 템플릿
Azure 함수를 추가하려면 함수 앱을 선택해야 합니다. 함수 앱은 꺾쇠괄호 아이콘 내의 번개 모양으로 식별할 수 있습니다.  
![함수 아이콘](../images/5-function-icon.png)

첫 번째 Azure 함수를 추가할 때 빠른 시작 화면이 표시됩니다. 이 화면에서 원하는 트리거 유형 및 프로그래밍 언어를 선택할 수 있습니다. 그런 다음, 선택 사항에 따라 Azure는 함수 코드 및 구성을 생성합니다.  
![함수 빠른 시작](../images/5-quickstart-form.png)

### <a name="function-templates"></a>함수 템플릿
사용할 수 있는 템플릿은 빠른 시작에서 제공하는 것으로 제한되지 않습니다. 30개가 넘는 템플릿 중에서 선택할 수도 있습니다. 후속 함수를 만들거나 빠른 시작 화면에서 **사용자 지정 함수** 옵션을 선택하여 템플릿 목록 화면에 액세스할 수 있습니다.  
![함수 템플릿](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>함수 및 파일 탐색
템플릿에서 함수를 만들면 여러 파일이 생성됩니다. JavaScript와 함께 Webhook + API 빠른 시작을 사용하기로 선택했다고 가정해 보겠습니다. 이 경우 구성 파일, **function.json** 및 소스 코드 파일인 **index.js**가 생성됩니다. 함수 앱에 액세스하면, 앱에서 만들어진 함수를 보여주는 메뉴 트리가 표시됩니다. 메뉴 트리는 함수 앱에 함수를 추가할 수 있는 이 **함수** 메뉴 항목에도 표시됩니다(메뉴 항목 위로 마우스를 이동하면 더하기(+) 아이콘이 나타남).  
![함수 추가 단추](../images/5-function-add-button.png) 

위에서 언급한 이 빠른 시작의 경우 트리 뷰에서 **함수**를 확장하면 기본 이름인 **HttpTriggerJS1**과 함께 하나의 함수가 표시됩니다(함수 f 아이콘으로도 표시됨). 이 함수를 선택하면 코드 창이 열리고 **index.js** 소스 파일이 표시됩니다. 코드 창의 오른쪽에는 **파일 보기**에 대한 탭이 포함된 플라이아웃 메뉴가 있습니다. 이 탭을 선택하면 함수를 구성하는 파일 구조(저장소에서 모방됨)가 표시됩니다.  
![함수 템플릿](../images/5-file-navigation.png)

## <a name="execution-options-for-testing-your-azure-function"></a>Azure 함수 테스트를 위한 실행 옵션입니다.
Azure 함수가 생성되면 테스트 방법을 알아야 합니다. 수동 실행, Azure Portal 내에서 테스트 등 몇 가지 방법이 있습니다.

### <a name="manual-execution-of-a-function"></a>함수의 수동 실행
구성된 트리거를 수동으로 트리거하여 함수 실행을 시작할 수 있습니다. 예를 들어 HttpTrigger를 사용하는 경우 Postman이나 cURL과 같은 도구를 사용하여 함수 엔드포인트 URL에 대한 HTTP 요청을 시작할 수 있습니다.  
![함수의 Postman 실행](../images/5-postman-execution.png) 왼쪽 탐색 창에서 HTTP 트리거를 선택한 후에 **함수 URL 가져오기** 단추를 선택하여 엔드포인트 URL을 가져올 수 있습니다.  
![함수 URL 가져오기](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Azure Portal에서 함수 테스트
Azure Portal에서도 함수를 테스트하는 편리한 방법을 제공합니다. 코드 창의 오른쪽에는 플라이아웃 탭 방식의 탐색 메뉴가 있습니다. 이 메뉴에 **테스트** 항목이 있습니다. 메뉴를 확장하고 이 탭을 선택하면 함수를 실행하고 결과를 볼 수 있습니다. HttpTrigger 시나리오를 사용하여 HTTP 메서드를 설정하고 querystring 매개 변수 및 HTTP 헤더를 요청에 추가할 수 있습니다. 또한 추가 시나리오를 테스트하도록 요청 본문을 변경할 수도 있습니다. 출력 창에 함수의 결과가 표시됩니다.  
![함수의 Portal 실행](../images/5-portal-execution.png)

## <a name="monitoring-an-azure-function"></a>Azure 함수 모니터링
Azure 함수 개발 중 메시지를 기록하고 예외 시나리오를 확인하는 기능은 프로덕션 환경에서 사용하도록 함수를 준비하는 과정에서 매우 중요합니다. 이는 소스 결함을 추적하는 프로덕션 시나리오에서와 마찬가지로 중요합니다. Azure Portal의 사용자 인터페이스는 모니터링 대시보드뿐만 아니라 Azure 함수에서 가져온 실행 로그 및 예외를 검토하는 방법도 제공합니다.

### <a name="monitoring-dashboard"></a>모니터링 대시보드
함수 앱 탐색 메뉴에서 함수 노드를 확장하면 **모니터** 메뉴 항목이 표시됩니다. 모니터 대시보드는 함수 실행의 기록을 보기 위한 빠른 방법을 제공합니다. 이 보기에는 성공적인 완료 여부는 물론 타임스탬프, 결과 코드, 지속 기간 및 작업 ID도 표시됩니다. Azure Application Insights를 통해 데이터가 채워집니다.  
![함수 모니터](../images/5-monitor-function.png)

### <a name="log-window"></a>로그 창
또한 함수에 로그 문을 추가할 수 있습니다. 이 문은 함수의 로그 창에 표시됩니다. 로그 창은 코드 창의 맨 아래에 있는 탭 방식의 플라이아웃 메뉴에 있습니다. JavaScript 기반 함수를 사용하는 경우 다음 구문을 사용하여 로그 문을 추가합니다.
```javascript
  context.log('Enter your logging statement here');
```  
![로그 창](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>오류 및 경고 창
로그 창과 동일한 플라이아웃 메뉴에서 오류 및 경고 창 탭을 찾을 수 있습니다. 이 창에는 코드 내의 컴파일 오류 및 경고가 표시됩니다. JavaScript는 동적이며 해석되는 언어이므로 다음 이미지는 C# 함수의 컴파일 오류를 표시합니다.  
![오류 및 경고 창](../images/5-errors-window.png)
