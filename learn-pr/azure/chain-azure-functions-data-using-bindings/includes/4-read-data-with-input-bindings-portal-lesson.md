데이터 원본을 연결하려면 *입력 바인딩*을 구성해야 합니다. 이 바인딩을 통해 최소한의 코드로 메시지를 만들 수 있습니다. 저장소 연결 열기 같은 작업에 코드를 작성할 필요가 없습니다. Azure Functions 런타임 및 바인딩이 이러한 작업을 대신하게 됩니다.

## <a name="input-binding-types"></a>입력 바인딩 형식

여러 가지 입력 유형이 있으나 모든 유형이 입력과 출력을 모두 지원하는 것은 아닙니다. 해당 유형의 데이터를 수집하려 할 때마다 사용하게 됩니다. 여기에서는 입력 바인딩을 지원하는 형식과 사용 시기에 대해 살펴봅니다.

- **Blob Storage** Blob Storage 바인딩은 Blob에서 읽을 수 있도록 합니다.

- **Cosmos DB** Azure Cosmos DB 입력 바인딩은 SQL API를 사용하여 하나 이상의 Azure Cosmos DB 문서를 검색하고, 함수의 입력 매개 변수에 전달합니다. 문서 ID 또는 쿼리 매개 변수는 함수를 호출하는 트리거를 기반으로 결정할 수 있습니다.

- **Microsoft Graph** Microsoft Graph 입력 바인딩을 사용하면 OneDrive에서 파일을 읽고, Excel에서 데이터를 읽고, Microsoft Graph API와 상호 작용하기 위한 인증 토큰을 가져올 수 있습니다.
- **Mobile Apps** Mobile Apps 입력 바인딩은 모바일 테이블 엔드포인트에서 레코드를 로드하여 함수에 전달합니다.

- **테이블 저장소** Azure Table Storage에서 데이터를 읽고 작업할 수 있습니다.

## <a name="how-to-create-an-input-binding"></a>입력 바인딩을 만드는 방법

입력 바인딩을 정의하려면 `direction`을 `in`으로 정의해야 합니다.
각 바인딩 유형에 대한 매개 변수는 다를 수 있습니다. 이것은 [Microsoft설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings?azure-portal=true)에서 자세히 설명합니다.

## <a name="what-is-a-binding-expression"></a>바인딩 식이란?

바인딩 식은 function.json의 특수화된 텍스트, 함수 매개 변수 또는 코드로, 함수가 값을 내기 위해 호출될 때 평가됩니다. 예를 들어, 바인딩 식을 사용하여 현재 시간을 가져오거나 앱 설정에서 값을 검색할 수 있습니다.

### <a name="types-of-binding-expressions"></a>바인딩 식의 형식

- 앱 설정
- 트리거 파일 이름
- 트리거 메타데이터
- JSON 페이로드
- 새 GUID
- 현재 날짜 및 시간
- 바인딩 식

대부분의 식은 중괄호 안에 넣어 식별됩니다. 그러나 앱 설정 바인딩 식은 다른 바인딩 식과는 다르게 식별됩니다. 중괄호 대신 백분율 기호 안에 넣습니다. 예를 들어 blob 출력 바인딩 경로가 `%Environment%/newblob.txt`이고 Environment 앱 설정 값이 Environment인 경우 blob은 Development 컨테이너에 생성됩니다.

입력 바인딩을 사용하여 함수를 데이터 원본에 연결할 수 있습니다. 여러 유형의 데이터 원본을 연결할 수 있고 각각에 대한 매개 변수는 서로 다릅니다. function.json, 함수 매개 변수 또는 코드에서 바인딩 식을 사용하여 다양한 원본에서 값을 확인할 수 있습니다.