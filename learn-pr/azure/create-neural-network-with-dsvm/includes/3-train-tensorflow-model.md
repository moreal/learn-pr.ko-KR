### <a name="train-a-tensorflow-model"></a>TensorFlow 모델 학습

이 단원에서는 핫도그가 포함된 이미지를 인식하는 [TensorFlow](https://www.tensorflow.org/)로 빌드된 이미지 분류 모델에 대해 학습합니다. 모델을 처음부터 만들 경우 엄청난 컴퓨팅 성능과 수만 또는 수십만 개의 이미지가 필요하므로 [전이 학습](https://en.wikipedia.org/wiki/Transfer_learning)으로 알려진 방식인 기존 모델을 사용자 지정합니다. 전이 학습을 사용하면 일반 노트북이나 PC에서 몇 분만 학습해도 수십 개의 이미지만으로 높은 수준의 정확도를 얻을 수 있습니다.

딥 러닝 컨텍스트의 전이 학습에서는 이미지 분류를 수행하도록 미리 학습된 심층 신경망으로 시작하여 문제 도메인 네트워크가 사용자 지정된 계층을 추가합니다. 예를 들어 핫도그가 포함된 이미지 그룹과 포함되지 않은 이미지 그룹 두 개로 이미지를 분류합니다. 20개가 넘는 미리 학습된 TensorFlow 이미지 분류 모델을 <https://github.com/tensorflow/models/tree/master/research/slim#pre-trained-models.>에서 사용할 수 있습니다. [Inception](https://arxiv.org/abs/1512.00567) 및 [ResNet](https://towardsdatascience.com/an-overview-of-resnet-and-its-variants-5281e2f56035) 모델은 정확도가 높으며 그에 따라 리소스 요구 사항이 까다로운 것이 특징입니다. 한편, MobileNet 모델은 정확도가 낮은 대신 간결하고 전력 효율성이 뛰어나며 모바일 장치를 염두에 두고 개발되었습니다. 이러한 모델은 모두 딥 러닝 커뮤니티에 잘 알려져 있으며 여러 경쟁업체 및 실제 응용 프로그램에 사용되었습니다. 정확도와 교육 시간 간에 적절한 균형을 유지하도록 MobileNet 모델 중 하나를 신경망의 기준으로 사용하겠습니다.

모델 학습에서는 기본 모델을 다운로드하고 도메인별 이미지와 레이블을 사용하여 학습되는 계층을 추가하는 Python 스크립트를 실행하기만 하면 됩니다. 필요한 스크립트는 GitHub에 제공되어 있으며 사용할 이미지는 [Kaggle](https://www.kaggle.com)에 제공된 수천 개의 공용 도메인 음식 이미지를 어셈블했습니다.

1. Data Science VM에서 화면 아래쪽에 있는 터미널 아이콘을 클릭하여 터미널 창을 엽니다.

    ![터미널 창 시작](../media-draft/3-launch-terminal.png)

    _터미널 창 시작_

1. 터미널 창에서 다음 명령을 실행하여 “notebooks” 폴더로 이동합니다.

    ```bash
    cd notebooks
    ```
    이 폴더에는 DSVM용으로 큐레이팅된 샘플 Jupyter 노트북이 미리 채워져 있습니다.

1. 이제 다음 명령을 사용하여 GitHub에서 “TensorFlow for Poets” 리포지토리를 복제합니다.

    ```bash
    git clone https://github.com/googlecodelabs/tensorflow-for-poets-2
    ```
    > **팁**: 이 줄을 클립보드에 복사한 후 **Shift+Ins**를 사용하여 터미널 창에 붙여넣을 수 있습니다.

    이 리포지토리에는 전이 학습 모델을 만들고 이미지를 분류하도록 학습된 모델을 호출하는 등의 작업에 사용되는 스크립트가 포함되어 있습니다. 이 리포지토리는 TensorFlow와 다른 Google 도구 및 API에 대해 학습하려는 소프트웨어 개발자를 위한 다양한 리소스와 실습 랩이 포함된 [Google Codelabs](https://codelabs.developers.google.com/)의 일부입니다.

1. 복제가 완료되면 복제된 모델이 있는 폴더로 이동합니다.

    ```bash
    cd tensorflow-for-poets-2
    ```

1. 다음 명령을 사용하여 모델을 학습하는 데 사용할 이미지를 다운로드합니다.

    ```bash
    wget https://topcs.blob.core.windows.net/public/tensorflow-resources.zip -O temp.zip; unzip temp.zip -d tf_files; rm temp.zip
    ```

    이 명령은 수백 개의 음식 이미지가 들어 있는 zip 파일을 다운로드합니다. 해당 이미지의 절반에는 핫도그가 포함되어 있고 다른 절반에는 포함되어 있지 않습니다. 다운로드된 이미지를 이름이 “tf_files”인 하위 디렉터리로 복사합니다.

1. 화면 아래쪽에 있는 파일 관리자 아이콘을 클릭하여 파일 관리자 창을 엽니다.

    ![파일 관리자 시작](../media-draft/3-launch-file-manager.png)

    _파일 관리자 시작_

1. 파일 관리자에서 “notebooks/tensorflow-for-poets-2/tf_files” 폴더로 이동합니다. 폴더에 이름이 “hot_dog” 및 “not_hot_dog”인 하위 디렉터리 쌍이 있는지 확인합니다. 전자에는 핫도그가 포함된 수백 개의 이미지가 있고 후자에는 핫도그가 포함되지 **않은** 동일한 수의 이미지가 있습니다. “hot_dog” 폴더에서 이미지를 찾아 모양을 확인합니다. “not_hot_dog” 폴더에서도 이미지를 확인합니다.

    > 이미지에 핫도그가 포함되어 있는지 판별하는 신경망을 학습하려면 핫도그가 포함된 이미지 및 핫도그가 포함되지 않은 이미지를 사용하여 학습합니다.

    ![“hot_dog” 폴더의 이미지](../media-draft/3-hot-dog-images.png)

    "hot_dog" 폴더의 이미지

    이름이 **retrained_labels_hotdog.txt**인 텍스트 파일이 폴더에 있는지도 확인합니다. 이 파일은 학습 이미지가 포함된 하위 디렉터리를 식별합니다. 모델을 학습하는 Python 스크립트에서 사용합니다. 스크립트는 텍스트 파일(텍스트 파일의 이름은 스크립트에 전달되는 매개 변수임)에 식별된 각 하위 디렉터리의 파일을 열거하고 해당 파일을 사용하여 네트워크를 학습합니다.

1. 두 번째 터미널 창을 열고 첫 번째 터미널 창에 열린 것과 동일한 "notebooks/tensorflow-for-poets-2" 폴더로 이동합니다. 다음 명령을 사용하여 TensorFlow 모델을 시각화하고 전이 학습 프로세스에 대한 인사이트를 얻는 데 사용되는 도구 집합인 [TensorBoard](https://www.tensorflow.org/programmers_guide/summaries_and_tensorboard)를 시작합니다.

     ```bash
     tensorboard --logdir tf_files/training_summaries
     ```

     > TensorBoard 인스턴스가 이미 실행 중인 경우에는 이 명령이 실패합니다. 포트 6006을 이미 사용 중이라는 알림을 받은 경우 ```pkill -f "tensorboard"``` 명령을 사용하여 기존 프로세스를 종료합니다. 그런 다음, ```tensorboard``` 명령을 다시 실행합니다.

1. 원래 터미널 창으로 다시 전환하고 다음 명령을 실행합니다.

    ```bash
    IMAGE_SIZE=224;
    ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}";
    ```

    이러한 명령은 학습 이미지의 해상도 및 신경망을 빌드할 기본 모델을 지정하는 환경 변수를 초기화합니다. IMAGE_SIZE에 유효한 값은 128, 160, 192 및 224입니다. 값이 클수록 학습 시간이 증가하지만 분류자의 정확도도 증가합니다.

1. 이제 다음 명령을 실행하여 전이 학습 프로세스 즉, 다운로드한 이미지를 사용한 모델 학습을 시작합니다.

    ```bash
    python scripts/retrain.py \
    --bottleneck_dir=tf_files/bottlenecks \
    --how_many_training_steps=500 \
    --model_dir=tf_files/models/ \
    --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
    --output_graph=tf_files/retrained_graph_hotdog.pb \
    --output_labels=tf_files/retrained_labels_hotdog.txt \
    --architecture="${ARCHITECTURE}" \
    --image_dir=tf_files \
    --testing_percentage=15 \
    --validation_percentage=15
    ```

    **retrain.py**는 다운로드한 리포지토리에 있는 스크립트 중 하나입니다. 1,000개가 넘는 코드 줄 및 주석으로 구성된 복잡한 스크립트입니다. 이 스크립트는 ```--architecture``` 스위치로 지정된 모델을 다운로드한 후 ```--image_dir``` 스위치로 지정된 디렉터리의 하위 디렉터리에 있는 이미지를 사용하여 학습되는 새 계층을 해당 모델에 추가합니다. 각 이미지는 해당 이미지가 있는 하위 디렉터리의 이름으로 레이블이 지정됩니다. 이 경우에는 “hot_dog” 또는 “not_hot_dog”입니다. 따라서 수정된 신경망에서 이미지 입력을 hot-dog 이미지(“hot_dog”) 또는 not-hot-dog 이미지(“not_hot_dog”)로 분류할 수 있습니다. 학습 세션의 출력은 TensorFlow 모델 파일 **retrained_graph_hotdog.pb**입니다. 이름 및 위치는 ```--output_graph``` 스위치에 지정됩니다.

1. 학습이 완료될 때까지 대기합니다. 학습 시간은 5분 미만입니다. 그런 다음, 출력을 확인하여 모델의 정확도를 판별합니다. 학습 프로세스에 소량의 임의 예상이 포함되어 있으므로 실제 결과가 아래와 약간 다를 수 있습니다.

      ![모델의 정확도 평가](../media-draft/3-running-transfer-learning.png)

1. 바탕 화면 아래쪽에 있는 브라우저 아이콘을 클릭하여 Data Science VM에 설치된 브라우저를 엽니다. 그런 다음, <http://0.0.0.0:6006>으로 이동하여 Tensorboard에 연결합니다.

    ![Firefox 시작](../media-draft/3-launch-firefox.png)

1. "accuracy_1"로 레이블이 지정된 그래프를 검사합니다. 파란색 선은 ```how_many_training_steps``` 스위치를 통해 지정된 500개의 학습 단계가 실행될 때 시간에 따라 성취한 정확도를 보여 줍니다. 이 메트릭은 학습이 진행됨에 따라 모델의 정확도가 어떻게 변화되는지 보여주므로 중요합니다. 발생한 과잉 맞춤의 양을 수량화한 파란색 선과 주황색 선 사이의 거리도 마찬가지로 중요하며 항상 최소화되어야 합니다. [과잉 맞춤](https://en.wikipedia.org/wiki/Overfitting)은 모델이 학습하는 이미지를 분류하는 데는 능숙하지만 제시되는 다른 이미지를 분류하는 데는 능숙하지 않음을 의미합니다. 여기에서는 주황색 선(학습 이미지로 성취한 “학습” 정확도)과 파란색 선(학습 집합 이외의 이미지로 테스트한 경우 성취한 “유효성 검사” 정확도) 사이의 차이가 10% 미만이므로 결과를 허용할 수 있습니다.

    ![TensorBoard 스칼라 표시](../media-draft/3-tensorboard-scalars.png)

1. TensorBoard 메뉴에서 **그래프**를 클릭하고 표시된 그래프를 검사합니다. 이 그래프의 기본 목적은 신경망과 신경망을 구성하는 계층을 보여 주는 것입니다. 이 예제에서 “input_1”은 음식 이미지를 통해 학습되어 신경망에 추가된 계층입니다. “MobilenetV1”은 사용자가 시작한 기본 신경망입니다. 표시되지 않은 많은 계층이 포함되어 있습니다. 심층 신경망을 처음부터 빌드한 경우 모든 계층이 여기에 다이어그램으로 표시됩니다. MobileNet을 구성하는 계층을 보려면 다이어그램에서 “MobilenetV1” 블록을 두 번 클릭합니다. 그래프 표시와 그래프에 표시되는 정보에 대한 자세한 내용은 [TensorBoard: Graph Visualization](https://www.tensorflow.org/programmers_guide/graph_viz)(TensorBoard: 그래프 시각화)을 참조하세요.

    ![TensorBoard 그래프 표시](../media-draft/3-tensorboard-graphs.png)

1. 파일 관리자로 다시 전환하여 "notebooks/tensorflow-for-poets-2/tf_files" 폴더로 이동합니다. 이름이 **retrained_graph_hotdog.pb**인 파일이 포함되어 있는지 확인합니다. 이 파일은 학습 프로세스 중에 만들어졌으며 학습된 TensorFlow 모델을 포함하고 있습니다. 이 파일은 다음 연습에서 NotHotDog 앱의 모델을 호출하는 데 사용됩니다.

10단계에서 실행한 스크립트는 정확도와 학습에 필요한 시간 사이의 균형을 유지하는 500개의 학습 단계를 지정했습니다. 원하는 경우 1000 또는 2000과 같은 더 높은 ```how_many_training_steps``` 값을 사용하여 모델을 다시 학습해 보세요. 일반적으로 단계 개수가 높으면 정확도가 높아지지만 학습 시간도 늘어납니다. 참고로, TensorBoard 스칼라 표시의 주황색 선과 파란색 선 사이 차이를 나타내는 과잉 맞춤에 주의하세요.