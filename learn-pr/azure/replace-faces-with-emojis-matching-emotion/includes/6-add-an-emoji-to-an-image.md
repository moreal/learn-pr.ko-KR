응용 프로그램 흐름의 이 시점에서 알고 있는 것은 다음과 같습니다.

1.  이미지의 얼굴 목록(있는 경우)
2.  각 얼굴에 사용할 이모지
3.  이미지의 각 얼굴에 대한 경계 사각형

이에 따라 이미지에서 검색된 각 얼굴에 대해 해당 얼굴 위에 이모지를 겹쳐서 얼굴에 맞게 이모지의 크기를 조정해야 합니다.

이 기능을 구현하기 위해 오픈 소스 이미지 조작 라이브러리인 [Jimp](https://www.npmjs.com/package/jimp)를 사용합니다.

이 강의의 목표는 `Jimp` 라이브러리를 사용하여 이미지를 조작하는 방법, 특히 얼굴 위에 이모지를 겹쳐 놓고 해당 이미지를 디스크에 다시 저장하는 방법을 알아보는 것입니다.

`createMojifiedImage` 함수를 구체화하여 이전 강의에서 시작한 `bin/mojify.ts` 스크립트를 확장하려고 합니다.

> 참고: 나중의 강의에서 Slack 명령과 Azure Function을 만들 때 이 스크립트의 모든 코드를 다시 사용합니다. 헛수고하는 것이 아닙니다!

## <a name="steps"></a>단계

### <a name="required-imports"></a>필요한 패키지 가져오기

Jimp를 사용하고 파일 시스템의 파일을 조작하려면 몇 가지 패키지를 파일의 위쪽에 가져와야 합니다

```typescript
import * as Jimp from "jimp";
import * as path from "path";
```

> 참고: 디스크에서 파일을 로드하므로 `path`가 필요합니다.

### <a name="basic-use-case"></a>기본 사용 사례

많은 복잡성을 제거하고 필요한 항목을 요청해 보겠습니다.

1. 이미지 로드
2. 😕 이모지를 오른쪽 위 모서리에 배치합니다(50x50 픽셀 크기로 조정).
3. 이미지 저장

다음과 같이 위의 모든 기능을 6줄의 코드로 구현할 수 있습니다.

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

이제 단계별로 분석해 보겠습니다.

`Jimp`를 사용하여 이미지를 로드하려면 다음과 같이 `Jimp.read` 함수를 사용합니다.

```typescript
let sourceImage = await Jimp.read(imageUrl);
```

`shared/emojis`에는 각 이모지의 png 파일에 대한 디렉터리가 있습니다. 각 이모지 png은 <emoji>.png 형식의 이름으로 지정되므로 `😕.png`는 😕 이모지의 png가 포함된 파일입니다.

다음과 같이 `😕.png`를 로드합니다.

```typescript
let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
let emojiImage = await Jimp.read(mojiPath);
```

다음으로, emojiImage의 크기를 50픽셀 너비 x 50픽셀 높이로 조정해야 합니다. 이 작업은 다음과 같이 resize 함수를 사용하여 수행할 수 있습니다.

```typescript
emojiImage.resize(50, 50);
```

`emojiImage`는 50x50 픽셀 공간에 맞게 크기가 조정되었습니다.

이제 다음과 같이 emojiImage를 왼쪽 위 모서리에 있는 sourceImage 위에 _배치_해야 합니다.

```typescript
sourceImage = sourceImage.composite(emojiImage, 0, 0);
```

`composite` 함수를 사용합니다. 이 함수는 위쪽과 아래쪽이 0 픽셀인 `sourceImage` 0 픽셀 위에 `emojiImage`를 배치합니다. `composite` 함수는 `sourceImage`를 변경하지 않는 대신, 위에 배치된 `emojiImage`와 함께 `sourceImage`의 복사본을 반환합니다.

마지막으로, 다음과 같이 출력 이미지를 디스크에 저장합니다.

```typescript
sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

### <a name="full-use-case"></a>전체 사용 사례

다행스럽게도 지금쯤이면 `Jimp`의 작동 방식과 이를 사용하여 이미지를 합성하는 방법을 잘 이해하고 있을 것입니다. 이제 `createMojifiedImage` 함수의 전체 코드를 살펴보면 더 많이 이해할 수 있습니다.

아래 코드를 복사하여 `bin/mojify.ts`의 `createMojifiedImage` 함수에 붙여넣습니다.

```typescript
async function createMojifiedImage(imageUrl) {
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

위의 코드는 이모지와 위치를 하드 코드하는 대신, 오히려 방금 살펴본 기본 사례와 매우 비슷합니다. 그러나 여기서는 합성할 이모지와 전달된 얼굴의 배열에 따라 배치할 위치를 결정합니다.

얼굴의 배열은 마지막 강의에서 구체화한 `getFaces` 함수에서 나온 것이며, 다음과 같이 main 함수에서 모두 연결됩니다.

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

`imageUrl`에 전달된 `getFaces`를 호출하여 `Face` 인스턴스의 배열을 가져옵니다.
원래 이미지와 함께 이 배열을 `createMojifiedImage` 함수에 전달합니다. 이 함수는 사람의 얼굴에 이모지를 합성하고 결과 파일을 `mojified.jpg`로 프로젝트 루트 폴더에 저장합니다.

### <a name="try-it-out"></a>사용해 보기

다음과 같이 이 코드를 직접 사용해 보세요.

```bash
node bin/mojify.js <url>
```

이 작업이 성공하면 원본 파일의 이모지화된 버전인 `mojified.jpg`가 프로젝트 루트에 저장됩니다.

다른 이미지를 사용해 보세요!
