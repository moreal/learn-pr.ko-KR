이 시점에서 응용 프로그램의 흐름에서 압니다.

1.  목록 (있는 경우) 이미지에서 얼굴입니다.
2.  각 면에 사용할이 모 지입니다.
3.  이미지에 있는 각 얼굴의 경계 사각형입니다.

이미지에서 발견 된 각 얼굴에 대 한 해야는 모 지 면을 통해 계층 얼굴에 맞게이 모 지를 크기 조정 합니다.

이 기능을 구현 하려면 오픈 소스 이미지 조작 라이브러리를 사용 [Jimp](https://www.npmjs.com/package/jimp)합니다.

사용 하는 방법을 알아보려면이 강의의 목표는는 `Jimp` 라이브러리 이미지 조작 하 고는 모 지 면을 통해 계층 및 해당 이미지를 저장 하는 방법에 맞게 디스크에 다시 작성 합니다.

확장 하려고 합니다 `bin/mojify.ts` 수정 하 여 이전 강의에서 시작 하는 스크립트는 `createMojifiedImage` 함수입니다.

> **참고**
>
> 이후 강의에서 Slack 명령 및 Azure 함수를 만들 때이 스크립트의 모든 코드를 다시 사용 합니다. 노력을 낭비 하지 않아도 했습니다!

## <a name="add-the-required-imports"></a>필요한 가져오기 추가

파일의 맨 위에 있는 몇 가지 패키지를 가져올 해야 Jimp을 사용해 자유롭게 다뤄 조작는 파일 시스템에서 파일을 다음과 같이 합니다.

```typescript
import * as Jimp from "jimp";
import * as path from "path";
```

> **참고**
>
> `path` 디스크에서 파일을 로드 하려고 하기 때문에 필요

## <a name="simplified-use-case"></a>간소화 된 사용 사례

보겠습니다 복잡성을 많이 제거 하 고 방금에 맞게 걸리는 요청:

1. 이미지 로드
2. 위치는 😕 오른쪽 위 모서리 (50x50px 조정)에서 모 지
3. 이미지를 저장 합니다.

6 줄의 코드로, 위의 모든 기능을 구현할 수 것 같이:

```typescript
async function createMojifiedImage(imageUrl) {
  let sourceImage = await Jimp.read(imageUrl);

  let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
  let emojiImage = await Jimp.read(mojiPath);

  emojiImage.resize(50, 50);

  sourceImage = sourceImage.composite(emojiImage, 0, 0);
  sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
}
```

에서는 분석 단계.

사용 하 여 이미지를 로드 `Jimp` 사용을 `Jimp.read` 함수를 다음과 같이:

```typescript
let sourceImage = await Jimp.read(imageUrl);
```

이 모 지 각에 대 한 png 파일의 디렉터리가 있으며 `shared/emojis`합니다. 각이 모 지 png로 라고 <emoji>.png 이므로 `😕.png` 의 png를 포함 하는 파일은는 😕 이 모 지입니다.

로드 `😕.png` 다음과 같이 합니다.

```typescript
let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
let emojiImage = await Jimp.read(mojiPath);
```

다음 최대에서는 크기를 조정 해야 합니다 `emojiImage` 50 픽셀 너비 x 50 픽셀 높이, 우리가 해결할 수 있는 크기 조정 함수를 사용 하 여 다음과 같이 합니다.

```typescript
emojiImage.resize(50, 50);
```

`emojiImage` 크기가 이제 50 x 50 픽셀 공간에 맞게 조정 합니다.

이제 해야 _배치_ 는 `emojiImage` 위에 `sourceImage` 왼쪽된 위 모서리에서 다음과 같이:

```typescript
sourceImage = sourceImage.composite(emojiImage, 0, 0);
```

사용 하 여는 `composite` 배치 하는 함수를 `emojiImage` 맨 위에 `sourceImage`, 위치를 정의 하는 마지막 두 개의 인수를 `emojiImage` 는 배치에서는 배치를 위쪽 및 0 픽셀에서 0 픽셀 아래로.

합니다 `composite` 함수를 변경 하지 않습니다 `sourceImage` 진행; 대신 해당 복사본을 반환 합니다 `sourceImage` 사용 하 여는 `emojiImage` 결과 sourceImage에 다시 할당 하는 이유는이 맨 위에 배치 `sourceImage = ...`

마지막으로 출력 이미지 디스크를 저장 했습니다 다음과 같이합니다.

```typescript
sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

## <a name="try-it-out"></a>체험

이 코드를 직접 시도 다음과 같이 합니다.

```bash
node bin/mojify.js [url-to-image]
```

이 작업은 프로젝트 루트에 파일을 저장 한 다음 호출 하는 경우 `mojified.jpg` 다음과 같은 코드를 확인 합니다.

![단순 이미지](/media-drafts/6.simple-mojified-image.jpg)

## <a name="full-use-case"></a>전체 사용 사례

다행히는 방법 잘 알고 있는 지금 `Jimp` 작동 및 사용 하 여이 복합 이미지입니다. 이제 경우 다루지는 대 한 전체 코드는 `createMojifiedImage` 함수를 훨씬 더 좋은 확인 해야 합니다.

복사 및 붙여넣기는 코드를 아래에 `createMojifiedImage` 함수 `bin/mojify.ts`합니다.

```typescript
async function createMojifiedImage(imageUrl) {
  let sourceImage = await Jimp.read(imageUrl);
  // Create a composite image, we will "append" to this composite an emoji image for each face found
  let compositeImage = sourceImage;

  for (let face of faces) {
    const mojiIcon = face.mojiIcon;
    const faceHeight = face.faceRectangle.height;
    const faceWidth = face.faceRectangle.width;
    const faceTop = face.faceRectangle.top;
    const faceLeft = face.faceRectangle.left;

    // Load the emoji from disk
    let mojiPath = path.resolve(
      __dirname,
      "../shared/emojis/" + mojiIcon + ".png"
    );
    let emojiImage = await Jimp.read(mojiPath);

    // Resize the emoji to fit the face
    emojiImage.resize(faceWidth, faceHeight);

    // Compose the emoji on the image
    compositeImage = compositeImage.composite(emojiImage, faceLeft, faceTop);
  }
  compositeImage.write(path.join(__dirname, "..", "mojified.jpg"));
}
```

그러나 위의 코드에서는 이어지는 간소화 된 경우와 매우 비슷합니다는 모 지를 하드 코딩 하 고 위치 대신 복합은이 모 지를 결정 하는 것 이며 전달 된 위치에 얼굴의 배열을 기반으로 배치할.

얼굴의 배열에서 제공 되는 `getFaces` 마지막 강의에서 로그 아웃 완성에서는 함수,의 같이 main 함수에서 함께 연결 하는 모든:

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

이라고 `getFaces` 전달 된와 `imageUrl` 배열을 가져오려면 `Face` 인스턴스.
이 배열에 전달 된 `createMojifiedImage` 이 함수 복합이 모 지 개인적으로 원래 이미지와 함께 함수에 직면 하 고 결과 파일을 프로젝트 루트 폴더에 저장 `mojified.jpg`

## <a name="try-it-out"></a>체험

이 코드를 직접 시도 다음과 같이 합니다.

```bash
node bin/mojify.js <url>
```

소스 파일의 mojified 버전을 프로젝트 루트에 저장 된 후 작동이 호출 되는 경우 `mojified.jpg`, 다음과 같이 합니다.

![복잡 한 이미지](/media-drafts/6.complex-mojified-image.jpg)

시험해 보세요. 다른 이미지를 사용 하 여
