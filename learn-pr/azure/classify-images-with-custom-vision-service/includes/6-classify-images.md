### <a name="exercise-6-use-the-app-to-classify-images"></a><span data-ttu-id="3f07e-101">연습 6: 앱을 사용하여 이미지 분류</span><span class="sxs-lookup"><span data-stu-id="3f07e-101">Exercise 6: Use the app to classify images</span></span>

<span data-ttu-id="3f07e-102">이 연습에서는 Artworks 앱을 사용하여 이미지를 분류를 위해 Custom Vision Service로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-102">In this exercise, you will use the Artworks app to submit images to the Custom Vision Service for classification.</span></span> <span data-ttu-id="3f07e-103">이 앱은 Custom Vision 예측 API의 [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) 메서드 호출에서 반환된 JSON 정보를 사용하여 이미지를 Picasso, Rembrandt, Pollock 중 누가 그린 것인지 또는 이러한 화가가 그리지 않은 것인지를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-103">The app uses the JSON information returned from calls to the Custom Vision Prediction API's [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) method to tell you whether an image represents a painting by Picasso, Rembrandt, Pollock, or none of the above.</span></span> <span data-ttu-id="3f07e-104">또한 이미지에 할당된 분류가 올바를 확률도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-104">It also shows the probability that the classification assigned to the image is correct.</span></span>

1. <span data-ttu-id="3f07e-105">Artworks 앱에서 **찾아보기(...)** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-105">Click the **Browse (...)** button in the Artworks app.</span></span> 

    ![Artworks 앱에서 로컬 이미지 찾아보기](../images/app-click-browse.png)

    <span data-ttu-id="3f07e-107">_Artworks 앱에서 로컬 이미지 찾아보기_</span><span class="sxs-lookup"><span data-stu-id="3f07e-107">_Browsing for local images in the Artworks app_</span></span> 

1. <span data-ttu-id="3f07e-108">랩 리소스에서 “빠른 테스트” 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-108">Browse to the "Quick Tests" folder in the lab resources.</span></span> <span data-ttu-id="3f07e-109">**PicassoTest_02.jpg** 파일을 선택한 다음, **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-109">Select the file named **PicassoTest_02.jpg**, and then click **Open**.</span></span>

1. <span data-ttu-id="3f07e-110">**예측** 단추를 클릭하여 Custom Vision Service에 이미지를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-110">Click the **Predict** button to submit the image to the Custom Vision Service.</span></span>

    ![Custom Vision Service에 이미지 제출](../images/app-click-predict.png)

    <span data-ttu-id="3f07e-112">_Custom Vision Service에 이미지 제출_</span><span class="sxs-lookup"><span data-stu-id="3f07e-112">_Submitting the image to the Custom Vision Service_</span></span> 

1. <span data-ttu-id="3f07e-113">앱이 그림을 Picasso로 식별하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-113">Confirm that the app identifies the painting as a Picasso.</span></span>

    ![이미지를 Picasso로 분류](../images/app-prediction-01.png)

    <span data-ttu-id="3f07e-115">_이미지를 Picasso로 분류_</span><span class="sxs-lookup"><span data-stu-id="3f07e-115">_Classifying an image as a Picasso_</span></span> 

1. <span data-ttu-id="3f07e-116">**RembrandtTest_01.jpg** 및 **PollockTest_01.jpg**에 대해 1-3단계를 반복하고 앱이 그림을 Rembrandt 및 Pollock으로 식별할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-116">Repeat steps 1 through 3 for **RembrandtTest_01.jpg** and **PollockTest_01.jpg** and confirm that the app can identify paintings by Rembrandt and Pollock.</span></span>

    ![이미지를 Rembrandt로 분류](../images/app-prediction-02.png)

    <span data-ttu-id="3f07e-118">_이미지를 Rembrandt로 분류_</span><span class="sxs-lookup"><span data-stu-id="3f07e-118">_Classifying an image as a Rembrandt_</span></span> 

1. <span data-ttu-id="3f07e-119">**VanGoghTest_01.png** 및 **VanGoghTest_02.png**에 대해 1-3단계를 반복하고 앱이 이러한 Van Gogh 명화를 Picasso, Rembrandt 또는 Pollock으로 식별하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-119">Repeat steps 1 through 3 for **VanGoghTest_01.png** and **VanGoghTest_02.png** and confirm that the app does not identify these Van Gogh masterworks as paintings by Picasso, Rembrandt, or Pollock.</span></span>

    ![Picasso, Rembrandt 또는 Pollock이 아님](../images/app-prediction-03.png)

    <span data-ttu-id="3f07e-121">_Picasso, Rembrandt 또는 Pollock이 아님_</span><span class="sxs-lookup"><span data-stu-id="3f07e-121">_Not a Picasso, Rembrandt, or Pollock_</span></span> 

1. <span data-ttu-id="3f07e-122">여기서 알 수 있는 것처럼 앱의 예측 API가 Custom Vision Service 포털만큼 믿을 수 있으며 더 재미있기까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-122">As you can see, using the Prediction API from an app is as reliable as through the Custom Vision Service portal — and way more fun!</span></span> <span data-ttu-id="3f07e-123">그뿐 아니라 포털의 예측 페이지로 이동하면 앱을 통해 업로드한 각 이미지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-123">What's more, if you go to the Predictions page in the portal, you'll find each of the images uploaded via the app shown there as well.</span></span>
 
    ![Custom Vision Service에 제출한 이미지](../images/portal-all-predictions.png)

    <span data-ttu-id="3f07e-125">_Custom Vision Service에 제출한 이미지_</span><span class="sxs-lookup"><span data-stu-id="3f07e-125">_image submitted to the Custom Vision Service_</span></span> 

<span data-ttu-id="3f07e-126">자신의 이미지로 자유롭게 테스트하고, 모델이 화가를 잘 식별하는지와 이미지가 Picasso, Rembrandt 또는 Pollock이 아니라고 판단하는 능력을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-126">Feel free to test with images of your own and gauge the model's adeptness at identifying artists or determining that an image is not a Picasso, Rembrandt, or Pollock.</span></span> <span data-ttu-id="3f07e-127">Van Goghs의 작품도 인식하도록 학습시키려면 Van Gogh 그림을 일부 업로드하고 “Van Gogh” 태그를 지정한 후 모델을 다시 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-127">If you'd like to train it to recognize Van Goghs, too, upload some Van Gogh paintings, tag them with "Van Gogh," and retrain the model.</span></span> <span data-ttu-id="3f07e-128">학습할 의지만 있다면 인텔리전스를 제한 없이 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-128">There is no limit to the intelligence you can add if you're willing to do the training.</span></span> <span data-ttu-id="3f07e-129">또한 일반적으로 더 많은 이미지를 학습할수록 모델은 더 똑똑해집니다.</span><span class="sxs-lookup"><span data-stu-id="3f07e-129">And remember that in general, the more images you train with, the smarter the model will be.</span></span>