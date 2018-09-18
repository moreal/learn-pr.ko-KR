<span data-ttu-id="3d545-101">응용 프로그램 흐름의 이 시점에서 알고 있는 것은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-101">At this point in the flow of the application we know:</span></span>

1.  <span data-ttu-id="3d545-102">이미지의 얼굴 목록(있는 경우)</span><span class="sxs-lookup"><span data-stu-id="3d545-102">The list of faces in the image (if any).</span></span>
2.  <span data-ttu-id="3d545-103">각 얼굴에 사용할 이모지</span><span class="sxs-lookup"><span data-stu-id="3d545-103">The emoji to use for each face.</span></span>
3.  <span data-ttu-id="3d545-104">이미지의 각 얼굴에 대한 경계 사각형</span><span class="sxs-lookup"><span data-stu-id="3d545-104">The bounding rectangle of each face in the image.</span></span>

<span data-ttu-id="3d545-105">이에 따라 이미지에서 검색된 각 얼굴에 대해 해당 얼굴 위에 이모지를 겹쳐서 얼굴에 맞게 이모지의 크기를 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-105">So for each face discovered in the image, we need to layer an emoji over the face, resizing the emoji to fit the face.</span></span>

<span data-ttu-id="3d545-106">이 기능을 구현하기 위해 오픈 소스 이미지 조작 라이브러리인 [Jimp](https://www.npmjs.com/package/jimp)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-106">To implement this functionality, we will use the open source image manipulation library [Jimp](https://www.npmjs.com/package/jimp).</span></span>

<span data-ttu-id="3d545-107">이 강의의 목표는 `Jimp` 라이브러리를 사용하여 이미지를 조작하는 방법, 특히 얼굴 위에 이모지를 겹쳐 놓고 해당 이미지를 디스크에 다시 저장하는 방법을 알아보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-107">The goal of this lecture is to learn how to use the `Jimp` library to manipulate images and specifically to learn how to layer an emoji over a face and save that image back out to disk.</span></span>

<span data-ttu-id="3d545-108">`createMojifiedImage` 함수를 구체화하여 이전 강의에서 시작한 `bin/mojify.ts` 스크립트를 확장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-108">We are going to expand on the `bin/mojify.ts` script we started in the previous lecture by fleshing out the `createMojifiedImage` function.</span></span>

> <span data-ttu-id="3d545-109">참고: 나중의 강의에서 Slack 명령과 Azure Function을 만들 때 이 스크립트의 모든 코드를 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-109">NOTE We will be re-using all the code from this script when we create the Slack command and Azure Function in later lectures.</span></span> <span data-ttu-id="3d545-110">헛수고하는 것이 아닙니다!</span><span class="sxs-lookup"><span data-stu-id="3d545-110">It's not wasted effort!</span></span>

## <a name="steps"></a><span data-ttu-id="3d545-111">단계</span><span class="sxs-lookup"><span data-stu-id="3d545-111">Steps</span></span>

### <a name="required-imports"></a><span data-ttu-id="3d545-112">필요한 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="3d545-112">Required Imports</span></span>

<span data-ttu-id="3d545-113">Jimp를 사용하고 파일 시스템의 파일을 조작하려면 몇 가지 패키지를 파일의 위쪽에 가져와야 합니다</span><span class="sxs-lookup"><span data-stu-id="3d545-113">To play around with Jimp and manipulate files on our filesystem we need to import a few packages at the top</span></span>

```typescript
import * as Jimp from "jimp";
import * as path from "path";
```

> <span data-ttu-id="3d545-114">참고: 디스크에서 파일을 로드하므로 `path`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-114">NOTE `path` is needed because we want to load files from disk</span></span>

### <a name="basic-use-case"></a><span data-ttu-id="3d545-115">기본 사용 사례</span><span class="sxs-lookup"><span data-stu-id="3d545-115">Basic Use Case</span></span>

<span data-ttu-id="3d545-116">많은 복잡성을 제거하고 필요한 항목을 요청해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-116">Let's strip away a lot of the complexity and ask what it would take to:</span></span>

1. <span data-ttu-id="3d545-117">이미지 로드</span><span class="sxs-lookup"><span data-stu-id="3d545-117">Load up an image</span></span>
2. <span data-ttu-id="3d545-118">😕 이모지를 오른쪽 위 모서리에 배치합니다(50x50 픽셀 크기로 조정).</span><span class="sxs-lookup"><span data-stu-id="3d545-118">Place the 😕 emoji in the top right corner (resized to 50x50px)</span></span>
3. <span data-ttu-id="3d545-119">이미지 저장</span><span class="sxs-lookup"><span data-stu-id="3d545-119">Save the image</span></span>

<span data-ttu-id="3d545-120">다음과 같이 위의 모든 기능을 6줄의 코드로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-120">We can implement all the functionality above in 6 lines of code, like so:</span></span>

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

<span data-ttu-id="3d545-121">이제 단계별로 분석해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-121">We'll break it down step by step.</span></span>

<span data-ttu-id="3d545-122">`Jimp`를 사용하여 이미지를 로드하려면 다음과 같이 `Jimp.read` 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-122">To load an image using `Jimp` we use the `Jimp.read` function, like so:</span></span>

```typescript
let sourceImage = await Jimp.read(imageUrl);
```

<span data-ttu-id="3d545-123">`shared/emojis`에는 각 이모지의 png 파일에 대한 디렉터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-123">We have a directory of png files for each emoji in `shared/emojis`.</span></span> <span data-ttu-id="3d545-124">각 이모지 png은 <emoji>.png 형식의 이름으로 지정되므로 `😕.png`는 😕 이모지의 png가 포함된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-124">Each emoji png is named as <emoji>.png, so `😕.png` is a file that contains a png of the 😕 emoji.</span></span>

<span data-ttu-id="3d545-125">다음과 같이 `😕.png`를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-125">We load up `😕.png` like so:</span></span>

```typescript
let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
let emojiImage = await Jimp.read(mojiPath);
```

<span data-ttu-id="3d545-126">다음으로, emojiImage의 크기를 50픽셀 너비 x 50픽셀 높이로 조정해야 합니다. 이 작업은 다음과 같이 resize 함수를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-126">Next up we need to resize the emojiImage to 50 pixels width x 50 pixels height, we can do that by using the resize function like so:</span></span>

```typescript
emojiImage.resize(50, 50);
```

<span data-ttu-id="3d545-127">`emojiImage`는 50x50 픽셀 공간에 맞게 크기가 조정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-127">The `emojiImage` has now been resized to fit in a 50x50 px space.</span></span>

<span data-ttu-id="3d545-128">이제 다음과 같이 emojiImage를 왼쪽 위 모서리에 있는 sourceImage 위에 _배치_해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-128">We now need to _place_ the emojiImage over the sourceImage in the top left corner, like so:</span></span>

```typescript
sourceImage = sourceImage.composite(emojiImage, 0, 0);
```

<span data-ttu-id="3d545-129">`composite` 함수를 사용합니다. 이 함수는 위쪽과 아래쪽이 0 픽셀인 `sourceImage` 0 픽셀 위에 `emojiImage`를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-129">We use the `composite` function, which places `emojiImage` ontop of `sourceImage` 0 pixels from the top and 0 pixels down.</span></span> <span data-ttu-id="3d545-130">`composite` 함수는 `sourceImage`를 변경하지 않는 대신, 위에 배치된 `emojiImage`와 함께 `sourceImage`의 복사본을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-130">The `composite` fucntion doesn't alter `sourceImage` in place, instead it returns a copy of `sourceImage` with the `emojiImage` placed on top.</span></span>

<span data-ttu-id="3d545-131">마지막으로, 다음과 같이 출력 이미지를 디스크에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-131">Finally we save the output image to disk like so:</span></span>

```typescript
sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

### <a name="full-use-case"></a><span data-ttu-id="3d545-132">전체 사용 사례</span><span class="sxs-lookup"><span data-stu-id="3d545-132">Full Use Case</span></span>

<span data-ttu-id="3d545-133">다행스럽게도 지금쯤이면 `Jimp`의 작동 방식과 이를 사용하여 이미지를 합성하는 방법을 잘 이해하고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-133">Hopefully by now you have a good understanding of how `Jimp` works and how we can use it to composite images.</span></span> <span data-ttu-id="3d545-134">이제 `createMojifiedImage` 함수의 전체 코드를 살펴보면 더 많이 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-134">So now when we go through the full code for the `createMojifiedImage` function it should make a lot more sense.</span></span>

<span data-ttu-id="3d545-135">아래 코드를 복사하여 `bin/mojify.ts`의 `createMojifiedImage` 함수에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-135">Copy and paste the bellow code into your `createMojifiedImage` function in `bin/mojify.ts`.</span></span>

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

<span data-ttu-id="3d545-136">위의 코드는 이모지와 위치를 하드 코드하는 대신, 오히려 방금 살펴본 기본 사례와 매우 비슷합니다. 그러나 여기서는 합성할 이모지와 전달된 얼굴의 배열에 따라 배치할 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-136">The above code is very similar to the base case we just went through, rather than hardcoding an emoji and poisition however we are deciding which emoji to composite and where to place it based on the array of faces passed in.</span></span>

<span data-ttu-id="3d545-137">얼굴의 배열은 마지막 강의에서 구체화한 `getFaces` 함수에서 나온 것이며, 다음과 같이 main 함수에서 모두 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-137">The array of faces comes from the `getFaces` function we fleshed out in the last lecture, it's all connected up together in the main function, like so:</span></span>

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

<span data-ttu-id="3d545-138">`imageUrl`에 전달된 `getFaces`를 호출하여 `Face` 인스턴스의 배열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-138">We call `getFaces` with the passed in `imageUrl` to get the array of `Face` instances.</span></span>
<span data-ttu-id="3d545-139">원래 이미지와 함께 이 배열을 `createMojifiedImage` 함수에 전달합니다. 이 함수는 사람의 얼굴에 이모지를 합성하고 결과 파일을 `mojified.jpg`로 프로젝트 루트 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-139">We pass this array to the `createMojifiedImage` function along with the original image, this function composites emojis on peoples faces and saves the resulting file to the project root folder as `mojified.jpg`</span></span>

### <a name="try-it-out"></a><span data-ttu-id="3d545-140">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="3d545-140">Try it out</span></span>

<span data-ttu-id="3d545-141">다음과 같이 이 코드를 직접 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3d545-141">Try this code out yourself, like so:</span></span>

```bash
node bin/mojify.js <url>
```

<span data-ttu-id="3d545-142">이 작업이 성공하면 원본 파일의 이모지화된 버전인 `mojified.jpg`가 프로젝트 루트에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d545-142">If this worked then a mojified version of the source fil should be stored in the project root called `mojified.jpg`.</span></span>

<span data-ttu-id="3d545-143">다른 이미지를 사용해 보세요!</span><span class="sxs-lookup"><span data-stu-id="3d545-143">Try it out with different images!</span></span>
