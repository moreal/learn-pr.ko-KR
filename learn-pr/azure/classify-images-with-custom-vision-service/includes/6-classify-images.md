<span data-ttu-id="76a52-101">이 단원에서는 Artworks 앱을 사용하여 이미지를 분류를 위해 Custom Vision Service로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-101">In this unit, you will use the Artworks app to submit images to the Custom Vision Service for classification.</span></span> <span data-ttu-id="76a52-102">이 앱은 Custom Vision 예측 API의 [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) 메서드에 대한 호출에서 반환된 JSON 정보를 사용하여 이미지를 Picasso, Rembrandt, Pollock 중 누가 그린 것인지 또는 이러한 화가가 그리지 않은 것인지를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-102">The app uses the JSON information returned from calls to the Custom Vision Prediction API's [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) method to tell you whether an image represents a painting by Picasso, Rembrandt, Pollock, or none of the above.</span></span> <span data-ttu-id="76a52-103">또한 이미지에 할당된 분류가 올바를 확률도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-103">It also shows the probability that the classification assigned to the image is correct.</span></span>

1. <span data-ttu-id="76a52-104">Artworks 앱에서 **찾아보기(...)** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-104">Click the **Browse (...)** button in the Artworks app.</span></span>

    ![Artworks 앱에서 로컬 이미지 찾아보기](../media/6-app-click-browse.png)

1. <span data-ttu-id="76a52-106">모듈 리소스에서 "Quick Tests" 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-106">Browse to the "Quick Tests" folder in the module resources.</span></span> <span data-ttu-id="76a52-107">**PicassoTest_02.jpg** 파일을 선택한 다음, **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-107">Select the file named **PicassoTest_02.jpg**, and then click **Open**.</span></span>

1. <span data-ttu-id="76a52-108">**예측** 단추를 클릭하여 Custom Vision Service에 이미지를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-108">Click the **Predict** button to submit the image to the Custom Vision Service.</span></span>

    ![Custom Vision Service에 이미지 제출](../media/6-app-click-predict.png)

1. <span data-ttu-id="76a52-110">앱이 그림을 Picasso로 식별하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-110">Confirm that the app identifies the painting as a Picasso.</span></span>

    ![이미지를 Picasso로 분류](../media/6-app-prediction-01.png)

1. <span data-ttu-id="76a52-112">**RembrandtTest_01.jpg** 및 **PollockTest_01.jpg**에 대해 1-3단계를 반복하고 앱이 그림을 Rembrandt 및 Pollock으로 식별할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-112">Repeat steps 1 through 3 for **RembrandtTest_01.jpg** and **PollockTest_01.jpg**, and confirm that the app can identify paintings by Rembrandt and Pollock.</span></span>

    ![이미지를 Rembrandt로 분류](../media/6-app-prediction-02.png)

1. <span data-ttu-id="76a52-114">**VanGoghTest_01.png** 및 **VanGoghTest_02.png**에 대해 1-3단계를 반복하고 앱이 이러한 Van Gogh 명화를 Picasso, Rembrandt 또는 Pollock으로 식별하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-114">Repeat steps 1 through 3 for **VanGoghTest_01.png** and **VanGoghTest_02.png**, and confirm that the app does not identify these Van Gogh masterworks as paintings by Picasso, Rembrandt, or Pollock.</span></span>

    ![Picasso, Rembrandt 또는 Pollock이 아님](../media/6-app-prediction-03.png)

1. <span data-ttu-id="76a52-116">여기서 알 수 있는 것처럼 앱의 예측 API는 Custom Vision Service 포털만큼 믿을 수 있으며 더 재미있기까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-116">As you can see, using the Prediction API from an app is as reliable as it is through the Custom Vision Service portal — and way more fun!</span></span> <span data-ttu-id="76a52-117">뿐만 아니라 포털의 예측 페이지로 이동하면 앱을 통해 업로드한 각 이미지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-117">What's more, if you go to the Predictions page in the portal, you'll find each of the images uploaded via the app shown there as well.</span></span>

    ![Custom Vision Service에 제출된 이미지](../media/6-portal-all-predictions.png)

<span data-ttu-id="76a52-119">자신의 이미지로 자유롭게 테스트하고, 모델이 화가를 잘 식별하는지와 이미지가 Picasso, Rembrandt 또는 Pollock이 아니라고 판단하는 모델의 기능을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-119">Feel free to test with images of your own and gauge the model's adeptness at identifying artists or determining that an image is not a Picasso, Rembrandt, or Pollock.</span></span> <span data-ttu-id="76a52-120">Van Goghs의 작품도 인식하도록 학습시키려면 Van Gogh 그림을 일부 업로드하고, "Van Gogh" 태그를 지정하고, 모델을 다시 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-120">If you'd like to train it to recognize Van Goghs too, upload some Van Gogh paintings, tag them with "Van Gogh," and retrain the model.</span></span> <span data-ttu-id="76a52-121">학습할 의지만 있다면 인텔리전스를 제한 없이 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-121">There is no limit to the intelligence you can add if you're willing to do the training.</span></span> <span data-ttu-id="76a52-122">또한 일반적으로 더 많은 이미지를 학습할수록 모델은 더 똑똑해집니다.</span><span class="sxs-lookup"><span data-stu-id="76a52-122">And remember that in general, the more images you train with, the smarter the model will be.</span></span>