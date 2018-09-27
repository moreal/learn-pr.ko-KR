기어 드라이브 예를 계속 사용하여 온도 서비스의 논리를 추가합니다. 특히 HTTP 요청에서 데이터를 수신하겠습니다.

## <a name="function-requirements"></a>함수 요구 사항

먼저 논리에 대한 몇 가지 요구 사항을 정의해야 합니다.

- 0-25 사이의 온도를 **OK**로 플래그 지정해야 합니다.
- 26-50 사이의 온도를 **CAUTION**으로 플래그를 지정해야 합니다.
- 50을 넘는 온도를 **DANGER**로 플래그 지정해야 합니다.

## <a name="add-a-function-to-our-function-app"></a>함수 앱에 함수 추가

앞에서 설명한 대로 Azure에서는 함수를 빌드하기 시작하는 데 도움이 되는 템플릿을 제공합니다. 이 단원에서는 `HttpTrigger` 템플릿을 사용하여 온도 서비스를 구현합니다.

1. [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. 왼쪽 메뉴에서 **모든 리소스**를 선택한 다음, “**<rgn>[샌드박스 리소스 그룹 이름]</rgn>**”을 선택하여 첫 번째 연습의 리소스 그룹을 선택합니다.

1. 그러면 그룹의 리소스가 표시됩니다. **escalator-functions-xxxxxxx** 항목(번개 아이콘으로도 표시됨)을 선택하여 이전 연습에서 만든 함수 앱의 이름을 클릭합니다.

  ![만든 에스컬레이터 함수 앱뿐만 아니라 강조 표시된 모든 리소스 블레이드를 보여주는 Azure Portal 스크린샷입니다.](../media/5-access-function-app.png)

1. 왼쪽 메뉴에는 함수 앱 이름과 하위 메뉴가 표시되며, 하위 메뉴에는 *함수*, *프록시* 및 *슬롯*이라는 세 항목이 있습니다.  첫 번째 함수를 만들기 시작하려면 **함수**를 선택하고 결과 페이지의 맨 위에 있는 **새 함수** 단추를 클릭합니다.

  ![함수 메뉴 항목 및 새 함수 단추가 강조 표시된 이 함수 앱에 대한 함수 목록을 보여주는 Azure Portal 스크린샷입니다.](../media/5-function-add-button.png)

1. 다음 스크린샷에 나와 있는 것처럼 빠른 시작 화면에서 **직접 만든 함수로 시작** 섹션에 있는 **사용자 지정 함수** 링크를 선택합니다. 빠른 시작 화면이 표시되지 않으면 페이지의 맨 위에 있는 **빠른 시작으로 이동** 링크를 클릭합니다.

  ![사용자 지정 함수 단추가 고유한 섹션의 시작에서 강조 표시된 빠른 시작 블레이드를 보여주는 Azure Portal 스크린샷입니다.](../media/5-custom-function.png)

1. 다음 스크린샷에 나와 있는 것처럼 화면에 표시된 템플릿 목록에서 **HTTP 트리거** 템플릿의 **JavaScript** 구현을 선택합니다.

1. 나타나는 **새 함수** 대화 상자의 이름 필드에 **DriveGearTemperatureService**를 입력합니다. 권한 부여 수준을 "함수"로 유지하고 **만들기** 단추를 눌러 함수를 만듭니다.

  ![언어 필드가 JavaScript로 설정되고 이름이 DriveGearTemperatureService로 설정된 새 HTTP 트리거 함수 옵션을 보여주는 Azure Portal 스크린샷입니다.](../media/5-create-httptrigger-form.png)

1. 함수 만들기가 완료되면 *index.js* 코드 파일의 내용과 함께 코드 편집기가 열립니다. 템플릿이 생성한 기본 코드가 다음 코드 조각에 나열되어 있습니다.

```javascript
module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function processed a request.');

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```

함수는 HTTP 요청 쿼리 문자열을 통해 또는 요청 본문의 일부로 이름이 전달될 것이라고 예상합니다. 이 함수는 **Hello, {name}** 메시지를 반환하고, 요청에서 보낸 이름을 다시 에코하여 응답합니다.

원본 보기의 오른쪽에 두 개의 탭이 표시됩니다. **파일 보기** 탭에는 함수에 대한 코드 및 구성 파일이 나열됩니다.  **function.json**을 선택하여 함수의 구성을 보면 다음과 같습니다.

```javascript
{
    "disabled": false,
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
    }
    ]
}
```

이 구성은 HTTP 요청을 수신할 때 함수가 실행되도록 선언합니다. 출력 바인딩은 응답이 HTTP 응답으로 전송될 것임을 선언합니다.

## <a name="test-the-function"></a>함수 테스트

> [!TIP]
> **cURL**은 파일을 보내거나 받는 데 사용할 수 있는 명령줄 도구입니다. Linux, macOS 및 Windows 10에 포함되어 있으며 대부분의 다른 운영 체제에 다운로드할 수 있습니다. cURL은 HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 등과 같은 많은 프로토콜을 지원합니다. 자세한 내용은 아래 링크를 참조하세요.
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

함수를 테스트하려면 명령줄에서 cURL을 사용하는 함수 URL에 HTTP 요청을 전송할 수 있습니다. 함수의 엔드포인트 URL을 찾으려면 다음 스크린샷에 나와 있는 대로 함수 코드로 돌아가서 **함수 URL 가져오기** 링크를 선택합니다. 이 링크를 일시적으로 저장합니다.

![함수 URL 가저오기 단추가 강조 표시된 함수 편집기를 보여주는 Azure Portal 스크린샷입니다.](../media/5-get-function-url.png)

### <a name="securing-http-triggers"></a>HTTP 트리거 보호

HTTP 트리거를 사용하면 API 키를 사용하여 각 요청에 대한 키가 필요하도록 설정하여 알 수 없는 호출자를 차단할 수 있습니다. 함수를 만들 때 _권한 부여 수준_을 선택합니다. 기본적으로 함수별 API 키가 필요한 "함수"로 설정되지만, "관리자"로 설정하여 글로벌 "마스터" 키를 사용하거나 "익명"으로 설정하여 키가 필요하지 않도록 지정할 수도 있습니다. 생성 후에 함수 속성을 통해 권한 부여 수준을 변경할 수도 있습니다.

이 함수를 만들 때 “함수”를 지정했으므로 HTTP 요청을 보낼 때 키를 제공해야 합니다. `code`라는 쿼리 문자열 매개 변수로 또는 `x-functions-key`라는 HTTP 헤더(기본 설정)로 보낼 수 있습니다.

함수 및 마스터 키는 함수가 확장될 때 **관리** 섹션에 있습니다. 기본적으로 이러한 키는 숨겨져 있으며 사용자가 표시해야 합니다.

1. 함수를 확장하고, **관리** 섹션을 선택하고, 기본 함수 키를 표시하고, 클립보드에 복사합니다.

  ![공개된 함수 키가 강조 표시된 함수 관리 블레이드를 보여주는 Azure Portal의 스크린샷.](../media/5-get-function-key.png)

1. 그런 다음, **cURL** 도구를 설치한 명령줄에서 함수의 URL과 함수 키를 사용하여 cURL 명령을 포맷합니다.

    - `POST` 요청을 사용합니다.
    - `application/json` 형식의 `Content-Type` 헤더 값을 추가합니다.
    - 아래 URL을 자신만의 URL로 바꿉니다.
    - 함수 키를 헤더 값 `x-functions-key`로 전달합니다.

    ```bash
    curl --header "Content-Type: application/json" --header "x-functions-key: <your-function-key>" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
    ```

함수는 다시 텍스트 `"Hello Azure Function"`으로 응답합니다.

> [!NOTE]
> 선택한 함수 옆에 있는 **테스트** 탭을 사용하여 개별 함수의 섹션에서 테스트할 수도 있지만 여기서는 함수 키 시스템이 작동하는지 확인할 수는 없습니다. 테스트 인터페이스에 적절한 헤더 및 매개 변수 값을 추가하고 **실행** 단추를 클릭하여 테스트 출력을 확인합니다.

## <a name="add-business-logic-to-the-function"></a>함수에 비즈니스 논리 추가

그런 다음, 수신하는 온도 값을 확인하고 각각의 상태를 설정하는 함수에 비즈니스 논리를 추가해 보겠습니다.

만든 함수는 다양한 온도 값을 수신할 것으로 예상됩니다. 다음 JSON 코드 조각은 함수에 전송할 요청 본문의 예입니다. 각 `reading` 항목에는 ID, 타임스탬프 및 온도가 있습니다.

```json
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

이번에는 함수의 기본 코드를 비즈니스 논리를 구현하는 다음 코드로 바꿉니다.

1. **index.js** 파일을 열고 다음 코드로 바꿉니다.

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        req.body.readings.forEach(function(reading) {

            if(reading.temperature<=25) {
                reading.status = 'OK';
            } else if (reading.temperature<=50) {
                reading.status = 'CAUTION';
            } else {
                reading.status = 'DANGER'
            }
            context.log('Reading is ' + reading.status);
        });

        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

추가한 논리는 간단합니다. 값의 배열을 반복하고 온도 필드를 확인합니다. 해당 필드의 값에 따라 **OK**, **CAUTION** 또는 **DANGER**의 상태를 설정합니다. 그런 다음, 각 항목에 추가된 상태 필드와 함께 값의 배열을 다시 전송합니다.

`log` 문을 확인합니다. 함수가 실행되면 로그 창에 메시지가 추가됩니다.

## <a name="test-our-business-logic"></a>비즈니스 논리 테스트

이 경우 포털의 **테스트** 창을 사용하여 함수를 테스트해 보겠습니다.

1. 오른쪽 플라이아웃 메뉴에서 **테스트** 창을 엽니다.

1. 샘플 요청을 요청 본문 텍스트 상자에 붙여넣습니다.

    ```json
    {
        "readings": [
            {
                "driveGearId": 1,
                "timestamp": 1534263995,
                "temperature": 23
            },
            {
                "driveGearId": 3,
                "timestamp": 1534264048,
                "temperature": 45
            },
            {
                "driveGearId": 18,
                "timestamp": 1534264050,
                "temperature": 55
            }
        ]
    }
    ```

1. **실행**을 선택하고 출력 창에서 응답을 확인합니다. 로그 메시지를 보려면 페이지의 맨 아래 플라이아웃에서 **로그** 탭을 엽니다. 다음 스크린샷에서는 출력 창의 예제 응답 및 **로그** 창의 메시지를 보여줍니다.

![테스트 및 로그 탭이 표시된 함수 편집기 블레이드를 보여주는 Azure Portal 스크린샷입니다. 함수의 샘플 응답은 출력 창에 표시됩니다.](../media/5-portal-testing.png)

상태 필드가 각 정보에 올바르게 추가되었음을 출력 창에서 확인할 수 있습니다.

**모니터** 대시보드로 이동하면 Application Insights에 요청이 기록되었음을 알 수 있습니다.

![함수 모니터링 대시보드에서 이전 테스트 성공 결과를 보여주는 Azure Portal 스크린샷입니다.](../media/5-app-insights.png)
