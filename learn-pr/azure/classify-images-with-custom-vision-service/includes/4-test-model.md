<span data-ttu-id="21332-101">이제 모델을 학습했으므로 테스트할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="21332-101">Now that we've trained our model, it's time to test it.</span></span> <span data-ttu-id="21332-102">모델에 새 이미지를 제공하고 얼마나 잘 분류하는지 볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21332-102">We'll give the model new images and see how well it classifies it.</span></span>

1. <span data-ttu-id="21332-103">페이지 맨 위에서 **빠른 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-103">Click **Quick Test** at the top of the page.</span></span>

    ![모델 테스트](../media/4-portal-click-quick-test.png)

1. <span data-ttu-id="21332-105">**로컬 파일 찾아보기**를 클릭한 다음, 이전에 다운로드한 모듈 리소스 폴더의 "Quick Tests" 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="21332-105">Click **Browse local files**, and then browse to the "Quick Tests" folder in the module resources folder you download previously.</span></span> <span data-ttu-id="21332-106">**PicassoTest_01.jpg**를 선택하고 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-106">Select **PicassoTest_01.jpg**, and click **Open**.</span></span>

    ![Picasso 테스트 이미지 선택](../media/4-portal-select-test-01.png)

1. <span data-ttu-id="21332-108">"빠른 테스트" 대화 상자에서 테스트 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-108">Examine the results of the test in the "Quick Test" dialog.</span></span> <span data-ttu-id="21332-109">Picasso 그림일 가능성은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="21332-109">What is the probability that the painting is a Picasso?</span></span> <span data-ttu-id="21332-110">Rembrandt 또는 Pollock 그림일 가능성은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="21332-110">What is the probability that it's a Rembrandt or Pollock?</span></span>

    ![Picasso 테스트 이미지 선택](../media/4-quick-test-result.png)

1. <span data-ttu-id="21332-112">“빠른 테스트” 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="21332-112">Close the "Quick Test" dialog.</span></span> <span data-ttu-id="21332-113">그런 다음, 페이지 맨 위에서 **예측**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-113">Then click **Predictions** at the top of the page.</span></span>

    ![수행된 테스트 보기](../media/4-portal-select-predictions.png)

1. <span data-ttu-id="21332-115">업로드한 테스트 이미지를 클릭하여 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-115">Click the test image that you uploaded to show a detail of it.</span></span> <span data-ttu-id="21332-116">그런 다음, 드롭다운 목록에서 **Picasso**를 선택하고 **저장 및 닫기**를 클릭하여 “Picasso”로 이미지 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-116">Then tag the image as a "Picasso" by selecting **Picasso** from the drop-down list and clicking **Save and close**.</span></span>

    > <span data-ttu-id="21332-117">이 방식으로 테스트 이미지 태그를 지정하면 추가 학습 이미지를 업로드하지 않고 모델을 구체화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21332-117">By tagging test images this way, you can refine the model without uploading additional training images.</span></span>

    ![테스트 이미지 태그 지정](../media/4-tag-test-image.png)

1. <span data-ttu-id="21332-119">이번에는 "빠른 테스트" 폴더에 있는 **FlowersTest.jpg** 파일을 사용하여 다른 빠른 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-119">Run another quick test, this time using the file named **FlowersTest.jpg** in the "Quick Test" folder.</span></span> <span data-ttu-id="21332-120">이 이미지가 Picasso, Rembrandt 또는 Pollock일 가능성이 작은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-120">Confirm that this image is assigned a low probability of being a Picasso, a Rembrandt, or a Pollock.</span></span>

<span data-ttu-id="21332-121">모델이 학습되어 사용할 준비가 되면 특정 아티스트별로 그림을 능숙하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="21332-121">The model is trained and ready to go and appears to be skilled at identifying paintings by certain artists.</span></span> <span data-ttu-id="21332-122">HTTP를 통해 예측 엔드포인트를 호출하여 어떤 일이 발생하는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21332-122">Let's call the prediction endpoint over HTTP and see what happens.</span></span>