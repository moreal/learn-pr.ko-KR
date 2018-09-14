와 마찬가지로 입력 바인딩 형식은 여러 출력 바인딩의입니다.

하지만 여러 가지 방법으로 출력 바인딩의 일부 형식은 지원 모두 입력 및 출력 합니다. 보내거나 데이터를 저장 하려면 언제 든 지 사용할 수 있습니다. 여기에서 출력 바인딩 및 사용 시기를 지 원하는 형식을 살펴보겠습니다.

## <a name="output-binding-types"></a>출력 바인딩 형식

- **Blob Storage** 바인딩 blob을 쓸 blob 출력을 사용할 수 있습니다.

- **Cosmos DB** Azure Cosmos DB 출력 바인딩 SQL API를 사용 하 여 Azure Cosmos DB 데이터베이스에 새 문서를 작성할 수 있습니다.

- **Event Hubs** 는 Event Hubs 출력 이벤트 스트림에 이벤트를 쓸 바인딩을 사용 합니다. 이벤트를 쓰려면 이벤트 허브에 대한 보내기 사용 권한이 있어야 합니다.

- **HTTP** 을 HTTP 출력 바인딩은 HTTP 요청 보낸 사람에 게 응답을 사용 합니다. 이 바인딩에는 HTTP 트리거가 필요하며 트리거 요청과 관련된 응답을 사용자 지정할 수 있습니다.

- **Microsoft Graph** Microsoft Graph 출력 바인딩은 OneDrive에서 파일에 쓰기, Excel 데이터를 수정 하 고, Outlook 통해 전자 메일을 보낼 수 있습니다.

- **Mobile Apps** 의 Mobile Apps 출력 바인딩 쓰기 Mobile Apps 테이블에 새 레코드입니다.

- **Notification Hubs** Notification Hubs 출력 바인딩을 사용 하 여 푸시 알림을 보낼 수 있습니다.

- **Queue Storage** Azure Queue storage 출력을 큐에 메시지를 쓸 바인딩을 사용 합니다.

- **표를 보낼** SendGrid 바인딩을 사용 하 여 전자 메일을 송신 합니다.

- **Service Bus** 사용 하 여 Azure Service Bus 출력 바인딩 큐 또는 토픽 메시지를 보낼 수 있습니다.

- **테이블 저장소** 사용 하 여 Azure Table 저장소 출력 바인딩을 Azure Storage 계정에서 테이블에 쓸 수 있습니다.

- **Twilio** Twilio 사용 하 여 텍스트 메시지를 보냅니다.

- **웹 후크** 을 HTTP 출력 바인딩은 HTTP 요청 보낸 사람에 게 응답을 사용 합니다. 이 바인딩에는 HTTP 트리거가 필요하며 트리거 요청과 관련된 응답을 사용자 지정할 수 있습니다.

## <a name="how-to-create-an-output-binding"></a>출력 바인딩을 작성 하는 방법
바인딩을 정의 하기 위해를 정의 해야를 입력 합니다 `direction` 으로 `out`입니다.
바인딩의 각 형식에 대 한 매개 변수를 다를 수에 문서화 되어 해당 [Microsoft의 설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)

## <a name="combining-input-and-output-bindings"></a>결합 입력 및 출력 바인딩 
하나의 함수에 여러 바인딩을 적용 하는 것이 가능 합니다. 이 옵션을 사용 하면 입력 및 출력 바인딩을 정의할 수 있습니다.

그리고 입력 및 출력도 수 동일한 바인딩 유형에...