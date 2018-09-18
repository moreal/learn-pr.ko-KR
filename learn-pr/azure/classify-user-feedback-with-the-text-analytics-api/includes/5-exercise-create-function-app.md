솔루션을 빌드하려면 몇 가지 코드를 호스트해야 합니다.  Azure Functions 함수 앱은 논리를 호스트하기에 좋은 위치입니다. 

## <a name="create-a-function-app-to-host-our-function"></a>함수를 호스트할 함수 앱 만들기

[!INCLUDE [resource-group-note](./rg-notice.md)]

1. Azure 계정을 사용하여 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal에 로그인했는지 확인합니다.

1. Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기** 단추를 선택한 다음, **계산** > **함수 앱**을 선택합니다.

1. 다음 표에 지정된 대로 함수 앱 설정을 입력합니다.


    | 설정      | 제안 값  | 설명                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **앱 이름** | 전역적으로 고유한 이름 | 새 함수 앱을 식별하는 이름입니다. 유효한 문자는 `a-z`, `0-9` 및 `-`입니다.  | 
    | **구독** | 본인의 구독 | 새 함수 앱이 만들어질 구독입니다. | 
    | **리소스 그룹**|  [!INCLUDE [resource-group-name](./rg-name.md)] | 함수 앱을 만들 리소스 그룹의 이름입니다.<br/><br/>**기존 항목 사용**을 선택하고 마지막 연습에서 만든 리소스 그룹을 사용해야 합니다. 이렇게 하면 이 모듈에서 만든 모든 리소스가 함께 유지됩니다. | 
    | **OS** | Windows | 함수 앱을 호스트하는 운영 체제입니다.  |
    | **호스팅** |   소비 계획 | 함수 앱에 리소스가 할당되는 방법을 정의하는 호스팅 계획입니다. 기본 **소비 계획**에서 함수의 요구에 따라 리소스가 동적으로 추가됩니다. [서버리스](https://azure.microsoft.com/overview/serverless-computing/) 호스팅에서는 함수가 실행되는 시간만큼만 요금을 지불하면 됩니다.   |
    | **위치** | 미국 서부 | 여러분과 가까운 또는 함수가 액세스하는 다른 서비스와 가까운 [지역](https://azure.microsoft.com/regions/)을 선택합니다.<br/><br/>마지막 연습에서 텍스트 분석 API 계정을 만들 때 사용한 지역과 동일한 지역을 선택합니다. |
    | **저장소 계정** |  전역적으로 고유한 이름 |  함수 앱에서 사용하는 새 저장소 계정의 이름입니다. 저장소 계정 이름은 3~24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다. 이 대화 상자는 여러분이 앱에 지정한 이름에서 파생된 고유한 이름으로 필드를 채웁니다. 하지만 자유롭게 다른 이름을 사용해도 되고, 심지어 기존 계정을 사용해도 됩니다. |

3. **만들기**를 선택하여 함수 앱을 프로비전하고 배포합니다.

4. 포털의 오른쪽 위 모서리에서 [알림] 아이콘을 선택하고 다음 메시지와 비슷한 **배포 진행 중** 메시지가 표시될 때까지 기다립니다.

![함수 앱 배포가 진행 중이라는 알림](../media-draft/func-app-deploy-progress-small.PNG)

5. 배포에 다소 시간이 걸릴 수 있습니다. 따라서 알림 허브에 계속 머물면서 다음 메시지와 비슷한 **배포 성공** 메시지를 기다립니다.

![함수 앱 배포가 완료되었다는 알림](../media-draft/func-app-text-analytics-deploy-success.png)

6. 축하합니다! 함수 앱을 만들고 배포했습니다. **리소스로 이동**을 선택하여 함수 앱을 봅니다.

>[!TIP]
>포털에서 앱 함수를 찾는 데 문제가 있는 경우 [Azure Portal에서 즐겨찾기에 함수 앱을 추가](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite)합니다.

## <a name="create-a-function-to-hold-our-logic"></a>논리를 보관할 함수 만들기

함수 앱이 생겼으니, 이제 함수를 만들 차례입니다. 함수는 트리거를 통해 활성화됩니다. 이 모듈에서는 큐 트리거를 사용하겠습니다. 런타임에서는 큐를 폴링하고 이 함수를 시작하여 새 메시지를 처리합니다.

1. 새 함수 앱을 확장한 다음, 마우스 커서를 **함수** 컬렉션 위로 이동합니다. 추가(**+**) 단추가 나타나면 추가 단추를 선택하여 함수 만들기 프로세스를 시작합니다.

![사용자가 함수 메뉴 항목을 마우스로 가리키면 나타나는 더하기 기호 애니메이션.](../media-draft/func-app-plus-hover-small.gif)

2. 나타나는 **신속하게 시작** 페이지에서 **사용자 지정 함수**를 선택합니다. 그러면 사용 가능한 함수 템플릿 목록이 로드됩니다. 

1. **큐 트리거** 템플릿 목록 항목에서 **JavaScript**를 선택합니다.

![큐 트리거 항목에서 JavaScript를 선택한 Azure Functions 템플릿의 스크린샷.](../media-draft/quickstart-select-queue-trigger.png)

1. 나타나는 **새 함수** 대화 상자에서 다음 값을 입력합니다.


|속성  |값  |
|---------|---------|
|언어     |   **JavaScript**      |
|이름     |   **discover-sentiment-function**      |
|큐 이름     |   **new-feedback-q**      |
|저장소 계정 연결        |  **AzureWebJobsDashboard**       |

![큐 트리거 항목에서 JavaScript를 선택한 Azure Functions 템플릿의 스크린샷.](../media-draft/new-function-dialog.png)

5. **만들기**를 선택하여 함수 만들기 프로세스를 시작합니다.

1. 큐 트리거 함수 템플릿을 사용하여 선택한 언어로 함수가 만들어집니다. 이 모듈에서는 JavaScript로 함수를 구현하지만, [지원되는 모든 언어](https://docs.microsoft.com/azure/azure-functions/supported-languages)로 함수를 만들 수 있습니다.

만들기 프로세스가 완료되면 포털에서 코드 편집기가 열리고 *index.js* 페이지가 로드됩니다. 이 파일은 함수 논리를 작성하는 코드 파일입니다.

## <a name="try-it-out"></a>사용해보기

지금까지 만든 부분을 테스트해 보겠습니다. 아직 코드를 작성하지 않았기 때문에 지금까지 구성한 내용이 실행되는지 확인하는 것이 테스트의 목적입니다.

1. 코드 편집기 맨 위에서 **실행**을 클릭합니다.

2. 화면의 맨 아래에서 열리는 **로그** 탭을 살펴봅니다. 모든 것이 계획대로 작동하면 다음 메시지와 유사한 메시지가 표시됩니다.
![함수 호출이 성공할 때 표시되는 응답 메시지의 스크린샷.](../media-draft/func-default-run.PNG)

**실행** 단추는 함수를 시작하고 기본 텍스트인 *샘플 큐 데이터*를 **테스트** 요청 창에서 함수로 전달했습니다.

잘하셨습니다! 성공적으로 함수 앱에 큐 트리거 함수를 추가하고 예상대로 작동하는지 테스트를 마쳤습니다! 그 다음 연습에서는 함수에 기능을 더 추가하겠습니다.

 함수의 다른 파일인 *function.json* 구성 파일을 간단하게 살펴봅시다. 이 파일의 구성 데이터는 다음 JSON 목록에 표시됩니다.

```json
{
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "new-feedback-q",
      "connection": "AzureWebJobsDashboard"
    }
  ],
  "disabled": false
}
```

보시다시피, 이 함수는 `queueTrigger` 형식의 **myQueueItem**이라는 트리거 바인딩이 있습니다. **new-feedback-q**라고 이름을 붙인 큐에 새 메시지가 도착하면 함수가 호출됩니다. 여기서는 myQueueItem 바인딩 매개 변수를 통해 새 메시지를 참조합니다. 바인딩은 일부 어려운 작업을 자동으로 처리합니다!

그 다음 단계에서는 텍스트 분석 API 서비스를 호출하는 코드를 추가할 것입니다.

>[!TIP]
>Azure Portal의 함수 패널 오른쪽에서 **파일 보기** 메뉴를 확장하여 index.js 및 function.json을 볼 수 있습니다. 

이 연습에서는 Azure Functions 인프라를 준비하는 방법을 다루었습니다. 큐에 새 메시지가 도착하면 실행되는 [!INCLUDE [input-q](./q-name-input.md)] 함수를 만들어서 함수 앱에 호스트했습니다. 진짜 재미있는 부분은 그 다음 연습에서 감정을 분석하는 Microsoft Cognitive 서비스를 호출할 때 시작됩니다.