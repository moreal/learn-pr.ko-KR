<span data-ttu-id="11dd2-101">마지막 장에서 `shared/mojis.ts` 파일에 이모지와 해당 감정 지점의 목록이 있음을 알았습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-101">In the last chapter we learnt that `shared/mojis.ts` file has a list of emojis and their emotional points.</span></span>

<span data-ttu-id="11dd2-102">이 장에서는 얼굴을 이모지에 매핑하는 데 사용할 나머지 코드에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-102">In this chapter we will learn about the rest of the code that we will use to map a face to an emoji.</span></span>

<span data-ttu-id="11dd2-103">다음을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-103">You will learn how to:</span></span>

1. <span data-ttu-id="11dd2-104">얼굴 이미지에 대한 URL을 전달하는 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-104">Create a script where you pass in a URL of an image of a face.</span></span>
2. <span data-ttu-id="11dd2-105">이미지의 모든 얼굴에 대한 감정 지점을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-105">Calculate the emotional point of any faces in the image.</span></span>
3. <span data-ttu-id="11dd2-106">이미지의 얼굴을 가장 가까운 이모지에 매핑</span><span class="sxs-lookup"><span data-stu-id="11dd2-106">Map the faces in the image to the closest emojis</span></span>

<span data-ttu-id="11dd2-107">결국에는 이 작업을 Slack 명령으로 기능적으로 구현하겠지만, 지금은 다음과 같이 명령줄에서 실행할 수 있는 간단한 Node 스크립트로 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-107">Eventually we will be implementing this functionally as a Slack command, but for now we are going to start with a simple node script that you can run on the comand line, like so:</span></span>

```bash
node bin/mojify.js <url-of-image-with-face>
```

## <a name="debugging-typescript"></a><span data-ttu-id="11dd2-108">TypeScript 디버깅</span><span class="sxs-lookup"><span data-stu-id="11dd2-108">Debugging TypeScript</span></span>

<span data-ttu-id="11dd2-109">TypeScript에서 작성하지만 JavaScript를 실행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-109">We are writing in TypeScript but executing JavaScript.</span></span> <span data-ttu-id="11dd2-110">이렇게 하면 읽기 어려울 수 있는 변환된 JavaScript 파일에서 중단점을 설정하고 디버그해야 하므로 디버깅이 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-110">This makes debugging hard as we would have to set breakpoints and debug in the transpiled JavaScript files which can be hard to read.</span></span>

<span data-ttu-id="11dd2-111">TypeScript에서 작성 _및_ 디버그하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-111">What we ideally want is to write _and_ debug in TypeScript.</span></span>

<span data-ttu-id="11dd2-112">다행스럽게도 약간의 구성만으로 VS Code를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-112">The good news is that it's possible with vs code with just a little bit of configuration.</span></span>

<span data-ttu-id="11dd2-113">`Ctrl+P > Debug: Open launch.json` 명령 팔레트를 사용하여 `launch.json` 파일 열기</span><span class="sxs-lookup"><span data-stu-id="11dd2-113">Open up the `launch.json` file by using the command paletee `Ctrl+P > Debug: Open launch.json`</span></span>

> <span data-ttu-id="11dd2-114">TODO: 이미지</span><span class="sxs-lookup"><span data-stu-id="11dd2-114">TODO: Image</span></span>

<span data-ttu-id="11dd2-115">다음과 같이 구성 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-115">Add in a configuration option like so:</span></span>

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

<span data-ttu-id="11dd2-116">이제 [디버그] 메뉴에서 `Mojify`이라는 옵션이 표시됩니다. 이 옵션은 URL을 인수로 전달하는 이미지화(mojify) 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-116">Now in the debug menu you will see an option called `Mojify` this will run the mojify script passing in a URL as the argument.</span></span> <span data-ttu-id="11dd2-117">TypeScript 파일에 중단점을 설정하고, 여기서 변수를 직접 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-117">You will be able to set breakpoints in the TypeScript file and inspect variables directly from there.</span></span>

## <a name="open-up-binmojists"></a><span data-ttu-id="11dd2-118">`bin/mojis.ts` 열기</span><span class="sxs-lookup"><span data-stu-id="11dd2-118">Open up `bin/mojis.ts`</span></span>

<span data-ttu-id="11dd2-119">파일은 다음과 같이 이미 필요한 모든 가져오기를 사용하여 스캐폴드되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-119">The file is already scaffolded with all the required imports, like so:</span></span>

```typescript
require("dotenv").config();
import fetch from "node-fetch";
import { EmotivePoint, Face, Rect } from "../shared/models";
```

<span data-ttu-id="11dd2-120">`dotenv`는 개발에 유용한 환경 변수로서 프로젝트의 루트에 있는 .env 파일의 내용을 로드하는 도우미 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-120">`dotenv` is a helper package which loads up the contents of a .env file in the root of your project as environment variables, useful for development.</span></span>

<span data-ttu-id="11dd2-121">`node-fetch`는 Azure Face API에 HTTP를 요청하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-121">`node-fetch` we use to make http requests to the Azure Face API.</span></span>

<span data-ttu-id="11dd2-122">`EmotivePoint`는 _감정 공간_에 있는 지점을 설명하는 도우미 클래스이며, 아래에서 더 자세히 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-122">`EmotivePoint` is a helper class that describes a point in _emotional space_ - we will be discussing this in more details below.</span></span>

<span data-ttu-id="11dd2-123">`Rect`는 사각형 셰이프를 설명하는 도우미 클래스이며, 이미지의 얼굴 위치를 설명하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-123">`Rect` is a helper class to describe a rectangle shape, we use this to describe the position of a face in an image.</span></span>

<span data-ttu-id="11dd2-124">`Face`는 이미지의 얼굴에 대한 직사각형과 감정 지점 정보를 결합하는 도우미 유틸리티 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-124">`Face` is a helper utility class which combines the rectangle and emotive point informatoin about a face in an image.</span></span>

<span data-ttu-id="11dd2-125">다음과 같이 파일의 중간에 몇 가지 스텁 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-125">In the middle of the file you should see some stub functions, like so:</span></span>

```typescript
async function getFaces(imageUrl) {
  //TODO
}

async function createMojifiedImage(imageUrl, faces) {
  //TODO
}
```

<span data-ttu-id="11dd2-126">이러한 함수는 이 강의 및 다음 강의에서 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-126">These are the functions you will be fleshing out in this lecture and the next</span></span>

<span data-ttu-id="11dd2-127">파일의 끝에는 이 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-127">At the end of the file you should see this code</span></span>

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

## <a name="add-the-environment-variables"></a><span data-ttu-id="11dd2-128">환경 변수 추가</span><span class="sxs-lookup"><span data-stu-id="11dd2-128">Add the environment variables</span></span>

<span data-ttu-id="11dd2-129">Face API를 호출하여 이전에 생성한 비밀 키와 URL을 사용해야 하므로 파일 위쪽의 imports 아래에 이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-129">We are going to call the Face API so we need to use those secret keys and urls we generated before, add this to the top of the file under the imports:</span></span>

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="call-the-face-api-with-the-provided-image-and-get-a-response"></a><span data-ttu-id="11dd2-130">제공된 이미지를 사용하여 Face API 호출 및 응답 가져오기</span><span class="sxs-lookup"><span data-stu-id="11dd2-130">Call the Face API with the provided image and get a response</span></span>

<span data-ttu-id="11dd2-131">Face API에 요청하려면 이 코드를 `getFaces` 함수의 맨 위에 추가합니다</span><span class="sxs-lookup"><span data-stu-id="11dd2-131">To make a reques to the Face API we add this code to the top of the `getFaces` function</span></span>

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

<span data-ttu-id="11dd2-132">위의 코드는 `fetch` 명령을 사용하여 Face API에 `POST` 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-132">The code above uses the `fetch` command to send a `POST` request to the Face API.</span></span>

<span data-ttu-id="11dd2-133">`API_KEY`를 헤더에 전달하므로 Face API에서 사용자가 제공한 요청임을 인식합니다. 그렇지 않으면 해당 요청이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-133">We pass the `API_KEY` in the header so the Face API knows the request comes from us, otherwise the request is rejected.</span></span>

<span data-ttu-id="11dd2-134">Face API에서 분석되도록 할 `imageUrl` 태그를 본문에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-134">We pass the `imageUrl` we want the Face API to analyse in the body.</span></span>

<span data-ttu-id="11dd2-135">그런 다음, API 요청의 응답을 가져오고 이를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-135">We then get the responce from the API request and print it out.</span></span>

<span data-ttu-id="11dd2-136">이제 스크립트를 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="11dd2-136">If you now run the script with</span></span>

```bash
node bin/mojify.js <path-to-image>
```

<span data-ttu-id="11dd2-137">해당 이미지를 Face API로 전달할 때 반환된 json 응답을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-137">It should print out the json responce returned from passing that image to the face API.</span></span>

## <a name="parse-the-responce"></a><span data-ttu-id="11dd2-138">응답 구문 분석</span><span class="sxs-lookup"><span data-stu-id="11dd2-138">Parse the responce</span></span>

<span data-ttu-id="11dd2-139">이모지를 계산하려면 API의 응답에서 반환된 각 얼굴을 `Face` 클래스의 인스턴스로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-139">To calculate the emojis ee need to convert each face returned in the responce from the API to an instance of a `Face` class.</span></span>

<span data-ttu-id="11dd2-140">`getFaces` 함수에서 API를 호출하는 코드 바로 뒤에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-140">We add this code just after the code to call the API in the `getFaces` fucntion:</span></span>

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

- <span data-ttu-id="11dd2-141">응답에서 반환되는 각 얼굴에 대해 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-141">We loop through each face returned in the responce.</span></span>
- <span data-ttu-id="11dd2-142">반환된 json에서 `EmotivePoint`, `Rect` 및 `Face`을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-142">We generate an `EmotivePoint`, a `Rect` and a `Face` from the returned json.</span></span>
- <span data-ttu-id="11dd2-143">얼굴과 이모지를 일치시키는 `Face` 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="11dd2-143">Creating the `Face` instance matches the face to an emoji</span></span>
- <span data-ttu-id="11dd2-144">일치된 이모지를 확인하기 위해 `mojiicon`을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-144">To see which emoji was matched we print out the `mojiicon`.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="11dd2-145">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="11dd2-145">Try it out</span></span>

<span data-ttu-id="11dd2-146">이제 스크립트를 실행하는 경우 수행되는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-146">Now if you run the script it should:</span></span>

- <span data-ttu-id="11dd2-147">제공된 이미지를 Face API를 통해 전달하고 감정을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-147">Pass the provided image through the Face API and calculate the emotion.</span></span>
- <span data-ttu-id="11dd2-148">감정을 이모지와 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-148">Match emotions to emojis.</span></span>
- <span data-ttu-id="11dd2-149">이모지를 터미널에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-149">Print the emojis to the terminal.</span></span>

<span data-ttu-id="11dd2-150">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11dd2-150">Like so:</span></span>

```bash
node bin/mojify.js <path-to-image>
<path-to-image>
😕
```
