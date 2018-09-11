### <a name="exercise-6-use-the-app-to-classify-images"></a>연습 6: 앱을 사용하여 이미지 분류

이 연습에서는 Artworks 앱을 사용하여 이미지를 분류를 위해 Custom Vision Service로 제출합니다. 이 앱은 Custom Vision 예측 API의 [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) 메서드 호출에서 반환된 JSON 정보를 사용하여 이미지를 Picasso, Rembrandt, Pollock 중 누가 그린 것인지 또는 이러한 화가가 그리지 않은 것인지를 알려줍니다. 또한 이미지에 할당된 분류가 올바를 확률도 표시합니다.

1. Artworks 앱에서 **찾아보기(...)** 단추를 클릭합니다. 

    ![Artworks 앱에서 로컬 이미지 찾아보기](../images/app-click-browse.png)

    _Artworks 앱에서 로컬 이미지 찾아보기_ 

1. 랩 리소스에서 “빠른 테스트” 폴더로 이동합니다. **PicassoTest_02.jpg** 파일을 선택한 다음, **열기**를 클릭합니다.

1. **예측** 단추를 클릭하여 Custom Vision Service에 이미지를 제출합니다.

    ![Custom Vision Service에 이미지 제출](../images/app-click-predict.png)

    _Custom Vision Service에 이미지 제출_ 

1. 앱이 그림을 Picasso로 식별하는지 확인합니다.

    ![이미지를 Picasso로 분류](../images/app-prediction-01.png)

    _이미지를 Picasso로 분류_ 

1. **RembrandtTest_01.jpg** 및 **PollockTest_01.jpg**에 대해 1-3단계를 반복하고 앱이 그림을 Rembrandt 및 Pollock으로 식별할 수 있는지 확인합니다.

    ![이미지를 Rembrandt로 분류](../images/app-prediction-02.png)

    _이미지를 Rembrandt로 분류_ 

1. **VanGoghTest_01.png** 및 **VanGoghTest_02.png**에 대해 1-3단계를 반복하고 앱이 이러한 Van Gogh 명화를 Picasso, Rembrandt 또는 Pollock으로 식별하지 않는지 확인합니다.

    ![Picasso, Rembrandt 또는 Pollock이 아님](../images/app-prediction-03.png)

    _Picasso, Rembrandt 또는 Pollock이 아님_ 

1. 여기서 알 수 있는 것처럼 앱의 예측 API가 Custom Vision Service 포털만큼 믿을 수 있으며 더 재미있기까지 합니다. 그뿐 아니라 포털의 예측 페이지로 이동하면 앱을 통해 업로드한 각 이미지를 찾을 수 있습니다.
 
    ![Custom Vision Service에 제출한 이미지](../images/portal-all-predictions.png)

    _Custom Vision Service에 제출한 이미지_ 

자신의 이미지로 자유롭게 테스트하고, 모델이 화가를 잘 식별하는지와 이미지가 Picasso, Rembrandt 또는 Pollock이 아니라고 판단하는 능력을 측정합니다. Van Goghs의 작품도 인식하도록 학습시키려면 Van Gogh 그림을 일부 업로드하고 “Van Gogh” 태그를 지정한 후 모델을 다시 학습합니다. 학습할 의지만 있다면 인텔리전스를 제한 없이 추가할 수 있습니다. 또한 일반적으로 더 많은 이미지를 학습할수록 모델은 더 똑똑해집니다.