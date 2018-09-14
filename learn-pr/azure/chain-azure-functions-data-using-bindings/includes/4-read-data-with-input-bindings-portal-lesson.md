구성 해야 하는 데이터 원본에 연결 하기 위해 프로그램 *입력 바인딩*합니다. 이 바인딩 수 있도록 하는 메시지를 만들려면 최소한의 코드를 작성 합니다. 저장소 연결을 여는 등의 작업에 대 한 코드를 작성할 필요가 없습니다. Azure Functions 런타임 및 바인딩 주의 이러한 작업의 수입니다.

## <a name="input-binding-types"></a>입력 바인딩 형식

하지만 가지 여러 유형의 입력을 지원 일부 형식 모두 입력 및 출력 합니다. 해당 형식의 데이터를 수집 하려면 언제 든 지 사용할 수 있습니다. 여기에서 입력된 바인딩 및 사용 시기를 지 원하는 형식을 살펴보겠습니다.

- **Blob Storage** blob storage 바인딩은 blob에서 읽을 수 있도록 합니다.

- **Cosmos DB** 하나를 검색할 SQL API를 사용 하는 Azure Cosmos DB 입력된 바인딩 또는 더 많은 Azure Cosmos DB 문서를 함수의 입력된 매개 변수에 전달 합니다. 문서 ID 또는 쿼리 매개 변수는 함수를 호출하는 트리거를 기반으로 결정할 수 있습니다.

- **Microsoft Graph** Microsoft Graph 입력된 바인딩은 OneDrive에서 파일 읽기, Excel에서 데이터 읽기 및 모든 Microsoft Graph API를 사용 하 여 상호 작용할 수 있도록 인증 토큰을 가져올 수 있습니다.
- **Mobile Apps** 의 Mobile Apps 입력된 바인딩은 모바일 테이블 끝점에서 레코드를 로드 하 고 함수로 전달 합니다.

- **테이블 저장소** 데이터를 읽고 Azure Table storage와 함께 사용할 수 있습니다.

## <a name="how-to-create-an-input-binding"></a>입력된 바인딩을 만드는 방법

바인딩을 정의 하기 위해를 정의 해야를 입력 합니다 `direction` 으로 `in`입니다.
바인딩의 각 형식에 대 한 매개 변수를 다를 수에 문서화 되어 해당 [Microsoft의 설명서](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings?azure-portal=true)

## <a name="what-is-a-binding-expression"></a>바인딩 식 란?

바인딩 식은 function.json, 함수 매개 변수 또는 함수 값을 생성 하기 위해 호출 될 때 계산 되는 코드에서 특수화 된 텍스트입니다. 예를 들어, 현재 시간을 가져오거나 앱 설정에서 값을 검색 하는 바인딩 식을 사용할 수 있습니다.

### <a name="types-of-binding-expressions"></a>바인딩 식의 형식

- 앱 설정
- 트리거 파일 이름
- 트리거 메타데이터
- JSON 페이로드
- 새 GUID
- 현재 날짜 및 시간
- 바인딩 식

대부분의 식은 중괄호로 래핑하여 식별됩니다. 그러나 앱 설정 바인딩 식은 다른 바인딩 식에서과 다르게 식별 됩니다: 중괄호 대신 백분율 기호로 래핑됩니다. 예를 들어 blob 출력 바인딩 경로가 `%Environment%/newblob.txt` 환경 앱 설정 값은 개발을 개발 컨테이너에 blob을 만들어집니다.

입력된 바인딩은 함수는 데이터 원본에 연결할 수 있습니다. 여러 유형의 데이터 원본에 연결할 수 및 각 기능 마다 나름대로 매개 변수가 있습니다. 다양 한 원본의 값을 확인 하려면 function.json, 함수 매개 변수 또는 코드에서 바인딩 식을 사용할 수 있습니다.