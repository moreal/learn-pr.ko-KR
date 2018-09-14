마지막 장에 나와에서는 학습 하는 `shared/mojis.ts` 파일에는 모 지 및 감정적인 지점을 목록이 있습니다.

이 장에서이 모 지 면을 매핑할을 사용 하 여 코드의 나머지 부분에 대 한 알아봅니다.

다음 방법에 대해 알아봅니다.

1. 얼굴 이미지의 URL에 전달 하는 스크립트를 만듭니다.
2. 이미지에서 모든 얼굴 감정적인 시점을 계산 합니다.
3. 이미지에서 얼굴을 가장 가까운이 모 지 매핑합니다

결국 구현이 기능적 Slack 명령으로 하지만 이제 것으로 시작 하려면 명령줄에서 실행할 수 있는 간단한 노드 스크립트를 다음과 같이 합니다.

```bash
node bin/mojify.js <url-of-image-with-face>
```

## <a name="debugging-typescript-in-vs-code"></a>VS Code에서 디버깅 TypeScript

작성 하 고 `TypeScript` 하지만 실행 `JavaScript`; 이렇게이 하면 디버깅 중단점을 설정 하 고 디버그 해야 하는 대로 하드에 트랜스 파일 된 JavaScript 파일는 읽기 어려울 수 있습니다.

작성 하는 것이 가장 좋습니다 원하는 _고_ TypeScript에서 디버그 합니다.

좋은 소식은 구성의 약간 vs code를 사용 하 여 수 있다는 것입니다.

엽니다는 `launch.json` 명령 palete를 사용 하 여 파일 <kbd>Ctrl</kbd>+<kbd>P</kbd> 하 고 해당 입력 `Debug: Open launch.json`

![열기 시작 Json](/media-drafts/5.open-debug-launch.json.png)

열립니다는 `launch.json` 구성 파일입니다. 추가 하 고 디버그 구성을 제거 하려면이 파일을 편집 합니다.

추가 된 디버그 구성 옵션 설정 배열 아래:

```json
{
  "type": "node",
  "request": "launch",
  "name": "Mojify",
  "env": {
    "DEBUG": "*"
  },
  "args": [
    "https://pbs.twimg.com/profile_images/833970306339446784/83MO53R9_400x400.jpg"
  ],
  "sourceMaps": true,
  "stopOnEntry": false,
  "console": "integratedTerminal",
  "cwd": "${workspaceRoot}",
  "program": "${workspaceRoot}/bin/mojify.js",
  "outFiles": ["${workspaceRoot}/bin/mojify.js"]
}
```

디버그 메뉴에서 호출 하는 옵션이 표시 이제 `Mojify` 이 URL을 인수로 전달 mojify 스크립트를 실행 합니다. 중단점을 설정할 수는 `TypeScript` 파일을 여기에서 직접 변수를 검사 합니다.

## <a name="open-up-binmojists"></a>말 좀 해 보세요 `bin/mojis.ts`

파일은 이미 스 캐 폴드 된 필요한 모든 가져오기를 사용 하 여 다음과 같이 합니다.

```typescript
require("dotenv").config();
import fetch from "node-fetch";
import { EmotivePoint, Face, Rect } from "../shared/models";
```

`dotenv` 환경 변수를 개발에 유용한 프로젝트의 루트에.env 파일의 내용을 로드 하는 도우미 패키지가입니다.

`node-fetch` Azure의 Face API에 HTTP 요청을 사용 합니다.

`EmotivePoint` 특정 시점을 설명 하는 도우미 클래스인 _감정적인 공간_ -이 아래에 자세히 설명 합니다.

`Rect` 사각형을 설명 하는 도우미 클래스를 사용 하 여이 이미지에서 얼굴의 위치를 설명 합니다.

`Face` 사각형 및 이미지에서 얼굴에 대 한 emotive 지점 정보를 결합 하는 도우미 유틸리티 클래스가입니다.

파일 중 일부 스텁 함수도 표시 되어야 다음과 같이 합니다.

```typescript
async function getFaces(imageUrl) {
  //TODO
}

async function createMojifiedImage(imageUrl, faces) {
  //TODO
}
```

이들은 있습니다이 강의 하 고 다음에 수정 수는 함수입니다.

파일의 끝이 코드가 표시 됩니다.

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

## <a name="add-the-environment-variables"></a>환경 변수를 추가 합니다.

해당 비밀 키와 Url을 생성 하기 전에 사용 하 여, 가져오기 아래에 있는 파일의 맨 위에 추가 해야 하므로 Face API를 호출 하겠습니다.

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="call-the-face-api-with-the-provided-image-and-get-a-response"></a>제공 된 이미지를 사용 하 여 Face API를 호출 하 고 응답을 가져옵니다

Face API를 요청 하려면의 맨 위에 다음이 코드 추가 `getFaces` 함수

```typescript
const fullUrl =
  API_URL +
  "/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion";

let response = await fetch(fullUrl, {
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

사용 하 여 위의 코드는 `fetch` 보낼 명령을 `POST` Face API에 요청 합니다.

> **참고**
>
> 추가 해야 `/detect` 및 얼굴 감지 및 감정도 반환 되도록 하려면 API_URL에 일부 쿼리 매개 변수입니다.

전달는 `API_KEY` 헤더에서 Face API에서 알 수 있도록에서 요청 하는 미국; 그렇지 않으면 요청이 거부 됩니다.

전달 된 `imageUrl` Face API를 본문에 분석 하려고 합니다.

다음 API 요청에서 응답을 가져올 하 고 코드를 출력 합니다.

이제 스크립트를 실행 하는 경우

```bash
node bin/mojify.js <path-to-image>
```

Face API에 해당 이미지를 전달할에서 반환한 JSON 응답 출력 됩니다.

## <a name="parse-the-response"></a>응답을 구문 분석

인스턴스에 API의 응답에서 반환 된 각 얼굴을 변환 해야 할 ee이 모 지를 계산 하는 `Face` 클래스입니다.

이 코드에서 API를 호출 하는 코드 바로 뒤 추가 `getFaces` 함수:

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

- 응답에서 반환 된 각 얼굴을 반복 합니다.
- 생성 하는 `EmotivePoint`, `Rect` 및 `Face` 에서 반환 된 json입니다.
- 만들기는 `Face` 인스턴스는이 모 지를 얼굴 일치
- 인쇄 우리는 모 지를 일치 하는 참조 하는 `mojiicon`합니다.

## <a name="try-it-out"></a>체험

이제 스크립트를 실행 하는 경우 다음과 같습니다.

1. Face API를 통해 제공 된 이미지를 전달 하 고 emotion을 계산 합니다.
2. 이 모 지를 감정을 일치 합니다.
3. 터미널이 모 지를 인쇄 합니다.

다음과 같습니다.

```bash
node bin/mojify.js <path-to-image>
<path-to-image>
😕
```
