이 강의의 목표 mojify 이미지를 전달된 되며 다음 화면에 표시 하도록 mojified 이미지를 반환 하는 Azure 함수가 HTTP 끝점을 만드는 것입니다.

끝으로 배웁니다.

- 변환 하는 방법에 `JavaScript` Azure 함수 프로젝트를 `TypeScript`입니다.
- 반환 하는 방법을 `raw` 함수 끝점에서 데이터를 이미지입니다.

## <a name="convert-to-typescript"></a>TypeScript 변환

코딩 하는 것 `TypeScript` 있지만 만든 함수 앱을 `JavaScript` 파일인 해야를 통해 변환 `TypeScript`합니다.

1. 이름 바꾸기는 `index.js` 파일 `index.ts`

> **참고**
>
> 실행 하는 경우 `npm run build` 및 관련 된 `tsc -w` 명령을 해당 `index.ts` 파일을 즉시 컴파일됩니다 `index.js` 있어야 하 고는 `index.map` 만든 파일입니다.
>
> 경우는 `index.js` 및 `index.map` 파일은 자동으로 만들어지지 않습니다 후 다시 확인은 `npm run build` 명령이 실행 되 고 출력에 오류가 표시 되지 않습니다.

2. 이 코드를 붙여 넣습니다. `index.ts`

```typescript
export async function index(context, req) {
  context.log("ReplyWithMojifiedImage HTTP trigger");
  context.res.body = "Hello!";
  context.done();
}
```

3. 함수 앱 실행

메서드 중 하나를 사용 하 여 앱이 실행 되는 함수에 소개 된 이전에 사용 하 여 확인 된 `func host start` 명령 또는 디버그 메뉴를 통해 응용 프로그램을 실행 합니다.

다음 방문 하 여 http://localhost:7171/api/MojifyImage 브라우저에서 합니다.

모든 기능이 올바르게 작동 경우 출력은이 `Hello!` 브라우저입니다.

이제 변환한 JavaScript 대신 TypeScript 되도록 함수 트리거 👏합니다.

## <a name="environment-variables-in-azure-functions"></a>Azure Functions에서 환경 변수

보안 유지를; 코드에 하드 코딩 개인 데이터 않으려는 대신 환경 변수 사용해 왔습니다.

특히, 우리가 지금까지 사용한 환경 변수 Face API URL 및 키를 저장 하려면 다음과 같이 합니다.

```bash
export FACE_API_URL=[face-api-url]
export FACE_API_KEY=[face-api-key]
```

Azure Functions 프로젝트를 만들면 해당 파일도 만듭니다 호출 `local.settings.json`합니다. 이 파일은 또한에 `.gitignore` 되므로 파일 _isnot 소스 컨트롤로 체크 인할_합니다.

게시할 원치 않는 중요 한 정보나만 로컬 구성을 저장 하려면 마련입니다.

기본적으로 것 같습니다.

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "node"
  }
}
```

추가 하는 항목을 `Values` 개체 환경 변수로 NodeJS 코드에 제공 됩니다.

Face API 변수의 추가 예 하므로:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "FACE_API_URL": "[face-api-url]",
    "FACE_API_KEY": "[face-api-key]"
  }
}
```

그런 다음 `FACE_API_URL` 및 `FACE_API_KEY` 같이 환경 변수 처럼 변수 노드로 제공 됩니다.

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="copy-existing-code-from-the-mojifyts-script"></a>기존 코드를 복사 하 여 `mojify.ts` 스크립트

작업 만들기 이전 강의에 소요 된 것이 `bin\mojify.ts` 코드 낭비 하지 않아도 됩니다, 해당 코드의 대부분은 이제이 함수에 복사할 수 있습니다.

모든 요소를 복사 **제외 하 고** 는 `main` 함수를 통해를 `index.ts` 파일입니다.

여기서 있지만 중요 하지 않습니다 하려는 모든 imports와 종속 기능 파일의 맨 위에 있는 및 `index` 맨 아래에 함수입니다.

> **중요 한**
>
> 덮어쓰지는 `index` 함수를이 작동 하려면 Azure 함수에 대 한 존재 해야 합니다.

에서는 수정 하지 않습니다는 `getFaces` 함수를 그대로 유지 됩니다 완전히 동일 합니다.

그러나는 `createMojifiedImage` 함수는 필요 하나 변경,이 함수의 원래 버전에 된 이미지를 저장할 코드의 끝에 다음과 같은 줄을 사용 하 여 디스크:

```typescript
compositeImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

코드의 새 Azure Function 버전에서는 디스크에 파일을 저장 하려고 하지 않습니다. 하고자 _반환_ 사용자 이미지 대신 브라우저 창에 표시 합니다.

잠깐 해야 작업을 수행 하는 `buffer`, 문의할 수 있습니다 `Jimp` 의 버퍼를 제공 하지만 이미지를 하려면 코드를 래핑할를 `Promise` 때문에 `Jimp.getBuffer` 함수는 비동기입니다.

위의 대체 `compositeImage.write` 이 줄:

```typescript
return new Promise((resolve, reject) => {
  compositeImage.getBuffer(Jimp.MIME_JPEG, (error, buffer) => {
    // get a buffer of the composed image
    if (error) {
      let message = "There was an error adding the emoji to the image";
      context.log.error(error);
      reject(message);
    } else {
      // put the image into the context body
      resolve(buffer);
    }
  });
});
```

이 이미지는 원시 이진 데이터의 버퍼를 반환합니다.

알 수 있듯이 시점에 대 한 알 수 없는 TypeScript가 불평 하는 `context` 변수입니다.

추가 하는이 문제를 해결 하려면 `context` 첫 번째 인수로 `createMojifiedImage` 함수를 다음과 같이 합니다.

```typescript
async function createMojifiedImage(context, imageUrl, faces) {
  ...
}
```

## <a name="connect-it-all-in-the-index-function"></a>연결 모두를 `index` 함수

이 끝점을 방문한 사람이 해야 합니다.

1. 가져오기는 `imageUrl` 요청 하는
2. Mojify는 `imageUrl` 원시 버퍼를 받고 있습니다.
3. 이미지를 브라우저에 표시 되는 방식으로 HTTP 요청에 응답 합니다.

인덱스 함수 수정 시작 해 보겠습니다.

`context.res` 응답을 설명 하는 속성 브라우저에 반환 되는 항목은 여기에 설정이 함수의 합니다.

구성 `context.res` 다음과 같이 합니다.

```typescript
context.res = {
  status: 200,
  headers: {
    "Content-Type": "image/jpeg"
  },
  isRaw: true
};
```

맨 위에 추가 `index` 함수를이 설정 상태 코드 200을 반환에 대 한 응답 jpeg 되도록 반환 콘텐츠 형식을 설정 하 고 설정 합니다 `isRaw` 이진 반환 수 있도록 하려면 true로 플래그 _이미지_ 데이터.

다음으로 추출 하고자 합니다 `imageUrl` 쿼리 매개 변수에서 어떤 이미지가 알 수 있도록 있어야 mojifying 합니다. 또한 사용자가 제공 하지 않는 경우 몇 가지 유용한 오류 메시지를 반환 하려고 합니다.

```typescript
const { imageUrl } = req.query;
if (!imageUrl) {
  let message = `imageUrl is required`;
  context.log.error(message);
  return context.done(message, { status: 400, body: message });
} else {
  context.log(`Called with imageUrl: "${imageUrl}"`);
}
```

마지막으로, 호출 하고자 합니다 `getFaces` 및 `createMojifiedImage` 파일의 맨 위에 추가한 함수.

```typescript
// Get the response from the faceAPI
try {
  let faces = await getFaces(imageUrl);
  let buffer = await createMojifiedImage(context, imageUrl, faces);
  context.res.body = buffer;
  context.log(`Posted reply with mojified image`);
  context.done();
} catch (err) {
  let message =
    "There was an error processing this image: " + JSON.stringify(err);
  context.log.error(message);
  context.done(null, {
    status: 400,
    body: message
  });
}
```

위의 중요 한 두 줄 다음과 같습니다.

```typescript
context.res.body = buffer;
context.done();
```

원시 이진 데이터는 응답 개체를 본문으로 설정 하 고 호출 후 `context.done()` 에서는 작업이 완료 되 고 응답을 반환 하는 작업을 수행할 수는 함수 앱에서 알 수 있도록 합니다.

같은 index.ts 함수에 대 한 전체 나열 됩니다.

```typescript
export async function index(context, req) {
  context.log("ReplyWithMojifiedImage HTTP trigger");

  context.res = {
    status: 200,
    headers: {
      "Content-Type": "image/jpeg"
    },
    isRaw: true
  };

  const { imageUrl } = req.query;
  if (!imageUrl) {
    let message = `imageUrl is required`;
    context.log.error(message);
    return context.done(message, { status: 400, body: message });
  } else {
    context.log(`Called with imageUrl: "${imageUrl}"`);
  }

  // Get the response from the faceAPI
  try {
    let faces = await getFaces(imageUrl);
    let buffer = await createMojifiedImage(context, imageUrl, faces);
    context.res.body = buffer;
    context.log(`Posted reply with mojified image`);
    context.done();
  } catch (err) {
    let message =
      "There was an error processing this image: " + JSON.stringify(err);
    context.log.error(message);
    context.done(null, {
      status: 400,
      body: message
    });
  }
}
```

## <a name="try-it-out"></a>체험

디버그 메뉴에서 시작 하거나 터미널에서 실행 하 여 함수 앱이 실행 중인지 확인 다음과 같이 합니다.

```bash
func host start
```

함수 앱이 같이 [출력] 창을 표시 해야 올바르게 시작:

```
Http Functions:
        MojifyImage: http://localhost:7071/api/MojifyImage
```

함수 앱을 정상적으로 시작 하는 경우 다음 url을 통해 이미지 URL에 전달 하는 것은 `imageUrl` 쿼리 매개 변수를 다음과 같이:

http://localhost:7171/api/MojifyImage?imageUrl=[url-to-an-image]

이미지의 mojified 버전을 반환 해야 작동 하는 모든 경우 다음과 같이 합니다.

![Mojified 이미지](/media-drafts/7.mojified-image.png)
