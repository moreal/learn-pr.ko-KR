이 단원에서는 Artworks 앱을 사용하여 이미지를 분류를 위해 Custom Vision Service로 제출합니다. 이 앱은 Custom Vision 예측 API의 [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) 메서드에 대한 호출에서 반환된 JSON 정보를 사용하여 이미지를 Picasso, Rembrandt, Pollock 중 누가 그린 것인지 또는 이러한 화가가 그리지 않은 것인지를 알려줍니다. 또한 이미지에 할당된 분류가 올바를 확률도 표시합니다.

1. Artworks 앱에서 **찾아보기(...)** 단추를 클릭합니다.

    ![Artworks 앱에서 로컬 이미지 찾아보기](../media/6-app-click-browse.png)

1. 모듈 리소스에서 "Quick Tests" 폴더로 이동합니다. **PicassoTest_02.jpg** 파일을 선택한 다음, **열기**를 클릭합니다.

1. **예측** 단추를 클릭하여 Custom Vision Service에 이미지를 제출합니다.

    ![Custom Vision Service에 이미지 제출](../media/6-app-click-predict.png)

1. 앱이 그림을 Picasso로 식별하는지 확인합니다.

    ![이미지를 Picasso로 분류](../media/6-app-prediction-01.png)

1. **RembrandtTest_01.jpg** 및 **PollockTest_01.jpg**에 대해 1-3단계를 반복하고 앱이 그림을 Rembrandt 및 Pollock으로 식별할 수 있는지 확인합니다.

    ![이미지를 Rembrandt로 분류](../media/6-app-prediction-02.png)

1. **VanGoghTest_01.png** 및 **VanGoghTest_02.png**에 대해 1-3단계를 반복하고 앱이 이러한 Van Gogh 명화를 Picasso, Rembrandt 또는 Pollock으로 식별하지 않는지 확인합니다.

    ![Picasso, Rembrandt 또는 Pollock이 아님](../media/6-app-prediction-03.png)

1. 여기서 알 수 있는 것처럼 앱의 예측 API는 Custom Vision Service 포털만큼 믿을 수 있으며 더 재미있기까지 합니다. 뿐만 아니라 포털의 예측 페이지로 이동하면 앱을 통해 업로드한 각 이미지를 찾을 수 있습니다.

    ![Custom Vision Service에 제출된 이미지](../media/6-portal-all-predictions.png)

자신의 이미지로 자유롭게 테스트하고, 모델이 화가를 잘 식별하는지와 이미지가 Picasso, Rembrandt 또는 Pollock이 아니라고 판단하는 모델의 기능을 측정합니다. Van Goghs의 작품도 인식하도록 학습시키려면 Van Gogh 그림을 일부 업로드하고, "Van Gogh" 태그를 지정하고, 모델을 다시 학습합니다. 학습할 의지만 있다면 인텔리전스를 제한 없이 추가할 수 있습니다. 또한 일반적으로 더 많은 이미지를 학습할수록 모델은 더 똑똑해집니다.