마지막 장에서 `shared/mojis.ts` 파일에 이모지와 해당 감정 지점의 목록이 있음을 알았습니다.

이 장에서는 얼굴을 이모지에 매핑하는 데 사용할 나머지 코드에 대해 알아봅니다.

다음을 수행하는 방법을 알아봅니다.

1. 얼굴 이미지에 대한 URL을 전달하는 스크립트를 만듭니다.
2. 이미지의 모든 얼굴에 대한 감정 지점을 계산합니다.
3. 이미지의 얼굴을 가장 가까운 이모지에 매핑

결국에는 이 작업을 Slack 명령으로 기능적으로 구현하겠지만, 지금은 다음과 같이 명령줄에서 실행할 수 있는 간단한 Node 스크립트로 시작하려고 합니다.

```bash
node bin/mojify.js <url-of-image-with-face>
```

## <a name="debugging-typescript"></a>TypeScript 디버깅

TypeScript에서 작성하지만 JavaScript를 실행할 것입니다. 이렇게 하면 읽기 어려울 수 있는 변환된 JavaScript 파일에서 중단점을 설정하고 디버그해야 하므로 디버깅이 어려워집니다.

TypeScript에서 작성 _및_ 디버그하는 것이 가장 좋습니다.

다행스럽게도 약간의 구성만으로 VS Code를 사용할 수 있습니다.

`Ctrl+P > Debug: Open launch.json` 명령 팔레트를 사용하여 `launch.json` 파일 열기

> TODO: 이미지

다음과 같이 구성 옵션을 추가합니다.

```json
{
  "type": "node",
  "request": "launch",
  "name": "Mojify",
  "env": {
    "DEBUG": "*"
  },
  "args": [
    "https://pbs.twmedia-drafts.com/profile_images/833970306339446784/83MO53R9_400x400.jpg"
  ],
  "sourceMaps": true,
  "stopOnEntry": false,
  "console": "integratedTerminal",
  "cwd": "${workspaceRoot}",
  "program": "${workspaceRoot}/bin/mojify.js",
  "outFiles": ["${workspaceRoot}/bin/mojify.js"]
}
```

이제 [디버그] 메뉴에서 `Mojify`이라는 옵션이 표시됩니다. 이 옵션은 URL을 인수로 전달하는 이미지화(mojify) 스크립트를 실행합니다. TypeScript 파일에 중단점을 설정하고, 여기서 변수를 직접 검사할 수 있습니다.

## <a name="open-up-binmojists"></a>`bin/mojis.ts` 열기

파일은 다음과 같이 이미 필요한 모든 가져오기를 사용하여 스캐폴드되어 있습니다.

```typescript
require("dotenv").config();
import fetch from "node-fetch";
import { EmotivePoint, Face, Rect } from "../shared/models";
```

`dotenv`는 개발에 유용한 환경 변수로서 프로젝트의 루트에 있는 .env 파일의 내용을 로드하는 도우미 패키지입니다.

`node-fetch`는 Azure Face API에 HTTP를 요청하는 데 사용합니다.

`EmotivePoint`는 _감정 공간_에 있는 지점을 설명하는 도우미 클래스이며, 아래에서 더 자세히 설명하겠습니다.

`Rect`는 사각형 셰이프를 설명하는 도우미 클래스이며, 이미지의 얼굴 위치를 설명하는 데 사용됩니다.

`Face`는 이미지의 얼굴에 대한 직사각형과 감정 지점 정보를 결합하는 도우미 유틸리티 클래스입니다.

다음과 같이 파일의 중간에 몇 가지 스텁 함수가 있습니다.

```typescript
async function getFaces(imageUrl) {
  //TODO
}

async function createMojifiedImage(imageUrl, faces) {
  //TODO
}
```

이러한 함수는 이 강의 및 다음 강의에서 구체화합니다.

파일의 끝에는 이 코드가 있습니다.

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

## <a name="add-the-environment-variables"></a>환경 변수 추가

Face API를 호출하여 이전에 생성한 비밀 키와 URL을 사용해야 하므로 파일 위쪽의 imports 아래에 이를 추가합니다.

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="call-the-face-api-with-the-provided-image-and-get-a-response"></a>제공된 이미지를 사용하여 Face API 호출 및 응답 가져오기

Face API에 요청하려면 이 코드를 `getFaces` 함수의 맨 위에 추가합니다

```typescript
let response = await fetch(API_URL, {
  headers: {
    "Ocp-Apim-Subscription-Key": API_KEY,
    "Content-Type": "application/json"
  },
  method: "POST",
  body: JSON.stringify({ url: imageUrl })
});
let resp = await response.json();
console.log(resp);
```

위의 코드는 `fetch` 명령을 사용하여 Face API에 `POST` 요청을 보냅니다.

`API_KEY`를 헤더에 전달하므로 Face API에서 사용자가 제공한 요청임을 인식합니다. 그렇지 않으면 해당 요청이 거부됩니다.

Face API에서 분석되도록 할 `imageUrl` 태그를 본문에 전달합니다.

그런 다음, API 요청의 응답을 가져오고 이를 출력합니다.

이제 스크립트를 실행하는 경우

```bash
node bin/mojify.js <path-to-image>
```

해당 이미지를 Face API로 전달할 때 반환된 json 응답을 출력합니다.

## <a name="parse-the-responce"></a>응답 구문 분석

이모지를 계산하려면 API의 응답에서 반환된 각 얼굴을 `Face` 클래스의 인스턴스로 변환해야 합니다.

`getFaces` 함수에서 API를 호출하는 코드 바로 뒤에 이 코드를 추가합니다.

```typescript
let faces = [];
for (let f of resp) {
  let scores = new EmotivePoint(f.faceAttributes.emotion);
  let faceRectangle = new Rect(f.faceRectangle);
  let face = new Face(scores, faceRectangle);
  console.log(face.mojiIcon);
  faces.push(face);
}
return faces;
```

- 응답에서 반환되는 각 얼굴에 대해 반복합니다.
- 반환된 json에서 `EmotivePoint`, `Rect` 및 `Face`을 생성합니다.
- 얼굴과 이모지를 일치시키는 `Face` 인스턴스 만들기
- 일치된 이모지를 확인하기 위해 `mojiicon`을 출력합니다.

## <a name="try-it-out"></a>사용해 보기

이제 스크립트를 실행하는 경우 수행되는 작업은 다음과 같습니다.

- 제공된 이미지를 Face API를 통해 전달하고 감정을 계산합니다.
- 감정을 이모지와 일치시킵니다.
- 이모지를 터미널에 출력합니다.

다음과 같습니다.

```bash
node bin/mojify.js <path-to-image>
<path-to-image>
😕
```
