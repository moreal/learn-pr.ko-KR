### <a name="exercise-4-test-the-model"></a><span data-ttu-id="3368a-101">연습 4: 모델 테스트</span><span class="sxs-lookup"><span data-stu-id="3368a-101">Exercise 4: Test the model</span></span>

<span data-ttu-id="3368a-102">[연습 5](../5-build-app.yml)에서는 모델을 사용하여 제시된 그림의 아티스트를 식별하는 Node.js 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-102">In [Exercise 5](../5-build-app.yml), you will create a Node.js app that uses the model to identify the artist of paintings presented to it.</span></span> <span data-ttu-id="3368a-103">그러나 모델을 테스트하기 위해 앱을 작성할 필요는 없습니다. 포털에서 테스트할 수 있으며 테스트하는 이미지를 사용하여 모델을 더 구체화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-103">But you don't have to write an app to test the model; you can do your testing in the portal, and you can further refine the model using the images that you test with.</span></span> <span data-ttu-id="3368a-104">이 연습에서는 제공된 테스트 이미지를 사용하여 그림의 아티스트를 식별하는 모델의 기능을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-104">In this exercise, you will test the model's ability to identify the artist of a painting using test images provided for you.</span></span>

1. <span data-ttu-id="3368a-105">페이지 맨 위에서 **빠른 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-105">Click **Quick Test** at the top of the page.</span></span>
 
    ![모델 테스트](../images/portal-click-quick-test.png)

    <span data-ttu-id="3368a-107">_모델 테스트_</span><span class="sxs-lookup"><span data-stu-id="3368a-107">_Testing the model_</span></span> 

1. <span data-ttu-id="3368a-108">**로컬 파일 찾아보기**를 클릭한 후 랩 리소스의 “Quick Tests” 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-108">Click **Browse local files**, and then browse to the "Quick Tests" folder in the lab resources.</span></span> <span data-ttu-id="3368a-109">**PicassoTest_01.jpg**를 선택하고 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-109">Select **PicassoTest_01.jpg**, and click **Open**.</span></span>

    ![Picasso 테스트 이미지 선택](../images/portal-select-test-01.png)

    <span data-ttu-id="3368a-111">_Picasso 테스트 이미지 선택_</span><span class="sxs-lookup"><span data-stu-id="3368a-111">_Selecting a Picasso test image_</span></span> 

1. <span data-ttu-id="3368a-112">“빠른 테스트” 대화 상자에서 테스트 결과를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-112">Examine the results of the test in the "Quick Test" dialog.</span></span> <span data-ttu-id="3368a-113">Picasso 그림일 가능성은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="3368a-113">What is the probability that the painting is a Picasso?</span></span> <span data-ttu-id="3368a-114">Rembrandt 또는 Pollock 그림일 가능성은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="3368a-114">What is the probability that it is a Rembrandt or Pollock?</span></span>

1. <span data-ttu-id="3368a-115">“빠른 테스트” 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-115">Close the "Quick Test" dialog.</span></span> <span data-ttu-id="3368a-116">그런 다음, 페이지 맨 위에서 **예측**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-116">Then click **Predictions** at the top of the page.</span></span>
 
    ![수행된 테스트 보기](../images/portal-select-predictions.png)

    <span data-ttu-id="3368a-118">_수행된 테스트 보기_</span><span class="sxs-lookup"><span data-stu-id="3368a-118">_Viewing the tests that have been performed_</span></span> 

1. <span data-ttu-id="3368a-119">업로드한 테스트 이미지를 클릭하여 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-119">Click the test image that you uploaded to show a detail of it.</span></span> <span data-ttu-id="3368a-120">그런 다음, 드롭다운 목록에서 **Picasso**를 선택하고 **저장 및 닫기**를 클릭하여 “Picasso”로 이미지 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-120">Then tag the image as a "Picasso" by selecting **Picasso** from the drop-down list and clicking **Save and close**.</span></span>

    > <span data-ttu-id="3368a-121">이 방식으로 테스트 이미지 태그를 지정하면 추가 학습 이미지를 업로드하지 않고 모델을 구체화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-121">By tagging test images this way, you can refine the model without uploading additional training images.</span></span>
 
    ![테스트 이미지 태그 지정](../images/tag-test-image.png)

    <span data-ttu-id="3368a-123">_테스트 이미지 태그 지정_</span><span class="sxs-lookup"><span data-stu-id="3368a-123">_Tagging the test image_</span></span> 

1. <span data-ttu-id="3368a-124">“Quick Test” 폴더에 있는 **FlowersTest.jpg** 파일을 사용하여 또 다른 빠른 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-124">Perform another quick test using the file named **FlowersTest.jpg** in the "Quick Test" folder.</span></span> <span data-ttu-id="3368a-125">이 이미지가 Picasso, Rembrandt 또는 Pollock일 가능성이 작은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-125">Confirm that this image is assigned a low probability of being a Picasso, a Rembrandt, or a Pollock.</span></span>

<span data-ttu-id="3368a-126">모델이 학습되어 사용할 준비가 되면 특정 아티스트별로 그림을 능숙하게 가려냅니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-126">The model is trained and ready to go and appears to be adept at identifying paintings by certain artists.</span></span> <span data-ttu-id="3368a-127">이제 한 단계 더 나아가 모델 인텔리전스를 앱에 통합해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3368a-127">Now let's go a step further and incorporate the model's intelligence into an app.</span></span>