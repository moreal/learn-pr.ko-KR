만들었습니다 합니다 `MojifyImage` Azure Function mojified 이미지를 반환 하는;는 slack 사용자가 실행 될 때마다 호출 되는 두 번째 끝점이 필요 합니다 `\mojify` 명령입니다.

이 두 번째 끝점 URL을 반환 해야 하는 경우는 `MojifyImage` Azure 함수입니다.

Slack 명령을 실행할 때 `\mojify [some-image-url]` 를 구성 했 고 전달 된 끝점에 POST 요청 `[some-image-url]` 으로 `text` 쿼리 매개 변수는 메시지의 본문에 포함 합니다.

이 강의의 목표를 조정 하 고 slack; 명령에 응답 하는이 함수를 만들 때 이 두 번째 Azure Function 호출 `RespondToSlackCommand`합니다.

이 강의의 끝에서 배웁니다.

- 명령 Slack에 응답 하는 HTTP 끝점을 만드는 방법에 요청 및 이미지를 사용 하 여 응답 하는 방법에 대해 필요로 하는 Slack 형식 이해할 수 있습니다.

## <a name="create-the-function-trigger-and-convert-to-typescript"></a>함수 트리거를 만들고 TypeScript 변환

다른 HTTP 트리거 Azure 함수를 생성 해야 합니다. 이러한 지침은 이전 강의;와 동일 이 함수를 호출 하는 점만 `RespondToSlackCommand` 대신 `MojifyImage`합니다.

1. 형식 <kbd>Ctrl</kbd>+<kbd>P</kbd> 여 명령 팔레트를 열고 다음에 대 한 검색 및 선택 `Azure Functions: Create Function...`

   ![새 함수 만들기](/media-drafts/7.create-function.png)

2. 함수 프로젝트를 이전에 만든 위치 폴더를 선택 (첫 번째 옵션은 현재 폴더 라고 하는 데 사용)

   ![폴더 선택](/media-drafts/7.select-current-project.png)

3. 에 만들기는 _HTTP 트리거_, 이므로 해당 옵션을 선택 합니다.

   ![폴더 선택](/media-drafts/7.select-trigger.png)

4. 입력 `RespondToSlackCommand` 만들려는 함수의 이름으로

   ![이름 선택](/media-drafts/7.choose-function-name.png)

5. 인증 수준으로 익명 수준 인증을 선택 합니다.

   ![이름 선택](/media-drafts/7.choose-auth-level.png)

성공적으로 완료 한 후 라는 폴더를 경우 `RespondToSlackCommand` 루트 디렉터리에 있어야 합니다.

마지막으로 동일한 강의 보겠습니다 현재 변환에서이 `JavaScript` 에 `TypeScript`입니다.

6. 라는 파일을 만듭니다 `index.ts` 에 `RespondToSlackCommand` 폴더입니다.

   있는지 확인 합니다 `TypeScript` 빌드 프로세스가 계속 실행 되 고 사용자가 자동으로 컴파일 수 `index.js` 및 `index.map` 파일입니다.

7. 이 코드를 붙여 넣습니다. `index.ts`

```typescript
export async function index(context, req) {
  context.log("RespondToSlackCommand HTTP trigger");
  context.res.body = "Hello!";
  context.done();
}
```

## <a name="try-it-out"></a>체험

모든 방문 하 여 작동 하는지 확인 http://localhost:7171/api/RespondToSlackCommand 브라우저에서 인쇄 해야이 `Hello!`합니다.

## <a name="flesh-out-the-index-function"></a>구체화 된 `index` 함수

이 `index` 함수는 이전 함수 보다 쓸 훨씬 빨라졌습니다.

먼저 설치 하겠습니다 우리의 `context.res` 개체

```typescript
context.res = {
  headers: {
    "Content-Type": "application/json"
  },
  body: null
};
```

이전에 설정 하지 않은 것 보다 더 간단 합니다 `isRaw` 속성을 기본값으로 하므로 `false`를 할 콘텐츠 형식 설정 수행 하지만 `application/json`합니다.

키를 사용 하 여 쿼리 문자열로 처리 하고자 하는 Slack 이미지 URL이 전송 되어 이전에 설명한 대로 `text`, 보안상의 이유로 데 필요한 정보를 가져오려면 약간 더 많은 작업을 해야 하므로 요청 본문에 포함이 있지만 를 너무 어렵지 있지만!

쉽게 생활에서 노드를 가져와 보겠습니다 `querystring` 패키지에이의 일부로 제공 됩니다 NodeJS을 별도로 설치할 필요가 없습니다.

```typescript
import * as querystring from "querystring";
```

그런 다음 우리의 `index` 함수를 변환 하는 `req.body` 를 추출 하는 개체로 `text` 속성을 다음과 같이:

```typescript
const { text } = querystring.parse(req.body);
```

사용자 제대로 명령을 입력 한 다음 텍스트를 포함 해야 이미지의 URL을 몇 가지 기본적인 유효성 검사에 추가할 수 있습니다 하는 경우 다음과 같이 합니다.

```typescript
let message = "Your mojified image my liege...";
if (!text) {
  message = "You must provide an image to mojify";
}
```

Slack 명령을 호출 하는 것을 기억 https://somedomain.com/api/RespondToSlackCommand, 대부분을 MojifyImage URL로 응답 해야 하 고 동일한 도메인에 있을 수 있습니다 https://somedomain.com/api/MojifyImage

대신 하드 코딩 파일에서 도메인을 대신 사용해 보겠습니다 동일한 도메인 te 도메인으로 요청으로 `MojifyImage` url을 다음과 같이 합니다.

```typescript
const mojifyUrl = req.url.substr(0, req.url.lastIndexOf("/")) + "/MojifyImage";
```

마지막으로 설정 해보겠습니다 slack 명령 응답의 본문에서는 특정 형식의 응답에 다음과 같이 합니다.

```typescript
context.res.body = {
  response_type: "in_channel",
  text: message,
  attachments: [
    {
      image_url: `${mojifyUrl}?imageUrl=${text}`
    }
  ]
};

context.done();
```

위에 중요 한 점은 `image_url` 에 `attachments` 속성이 반환 값에 설정를 `mojifyUrl` 으로 명령에 제공 된 사용자를 URL에 전달를 `imageUrl` 매개 변수를 쿼리 합니다.

## <a name="try-it-out"></a>체험

모든 방문 하 여 작동 하는지 확인 http://localhost:7171/api/RespondToSlackCommand 브라우저에서 일부 인쇄 이제 해야 `json` 같은 아래:

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "http://localhost:7071/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```
