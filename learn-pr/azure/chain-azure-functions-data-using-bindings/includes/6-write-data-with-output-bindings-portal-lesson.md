입력 바인딩과 마찬가지로 출력 바인딩에도 여러 형식이 있습니다.

여러 가지 출력 바인딩 형식이 있으나 모든 형식이 입력과 출력을 모두 지원하는 것은 아닙니다. 데이터를 보내거나 저장하고자 할 때마다 사용하게 됩니다. 여기에서는 출력 바인딩을 지원하는 형식과 사용 시기에 대해 살펴봅니다.

## <a name="output-binding-types"></a>출력 바인딩 형식

- **Blob Storage** Blob 출력 바인딩을 사용하여 Blob를 작성하는 데 사용할 수 있습니다.

- **Cosmos DB** Azure Cosmos DB 출력 바인딩을 사용하면 Azure Cosmos DB 데이터베이스에 SQL API를 사용하여 새 문서를 작성할 수 있습니다.

- **Event Hubs** Event Hubs 출력 바인딩을 사용하여 이벤트 스트림에 이벤트를 씁니다. 이벤트를 쓰려면 이벤트 허브에 대한 보내기 사용 권한이 있어야 합니다.

- **HTTP** HTTP 요청 발신기(sender)에 응답하려면 HTTP 출력 바인딩을 사용합니다. 이 바인딩에는 HTTP 트리거가 필요하며 트리거 요청과 관련된 응답을 사용자 지정할 수 있습니다.

- **Microsoft Graph** Microsoft Graph 출력 바인딩을 통해 OneDrive에 파일을 쓰고, Excel 데이터를 수정하며, Outlook을 통해 이메일을 보낼 수 있습니다.

- **Mobile Apps** Mobile Apps 출력 바인딩을 사용하여 Mobile Apps 테이블에 새 레코드를 작성합니다.

- **Notification Hubs** Notification Hubs 출력 바인딩을 사용하여 푸시 알림을 보낼 수 있습니다.

- **Queue Storage** Azure Queue Storage 출력 바인딩을 사용하여 메시지를 큐에 씁니다.

- **Send Grid** SendGrid 바인딩을 사용하여 이메일을 보냅니다.

- **Service Bus** Azure Service Bus 출력 바인딩을 사용하여 큐 또는 토픽 메시지를 보냅니다.

- **Table storage** Azure Table Storage 출력 바인딩을 사용하여 Azure Storage 계정에서 테이블에 쓸 수 있습니다.

- **Twilio** Twilio를 사용하여 문자 메시지를 보냅니다.

- **Webhooks** HTTP 요청 발신기(sender)에 응답하려면 HTTP 출력 바인딩을 사용합니다. 이 바인딩에는 HTTP 트리거가 필요하며 트리거 요청과 관련된 응답을 사용자 지정할 수 있습니다.


## <a name="how-to-create-an-output-binding"></a>출력 바인딩을 만드는 방법
입력 바인딩을 정의하려면 `direction`을 `out`으로 정의해야 합니다.
각 바인딩 유형에 대한 매개 변수는 다를 수 있습니다. 이것은 [Microsoft설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)에서 자세히 설명합니다.

## <a name="combining-input-and-output-bindings"></a>입력 및 출력 바인딩 결합 
단일 함수에 여러 바인딩을 적용할 수 있습니다. 이렇게 하면 입력과 출력 바인딩을 모두 정의할 수 있습니다.

입력과 출력이 같은 바인딩 형식을 가질 수도 있습니다.