이 단원에서는 이전 연습에서 업로드한 이미지와 태그 지정된 이미지를 사용하여 모델을 학습합니다. 모델을 학습하면 추가 태그 지정 이미지를 업로드하고 재학습하여 모델을 미세 조정할 수 있습니다.

1. 페이지 위쪽의 **학습** 단추를 클릭하여 모델을 학습합니다. 모델을 학습할 때마다 새로운 반복이 생성됩니다. Custom Vision Service는 여러 반복을 유지하므로 시간에 따른 진행 상황을 비교할 수 있습니다.

    ![모델 학습](../media/2-portal-click-train.png)

1. 학습 프로세스가 완료될 때까지 대기합니다. 몇 초면 끝납니다. 그런 다음, 반복 1에 표시된 학습 통계를 검토합니다. 

    결과는 모델의 정확도에 대해 **정밀도** 및 **재현율**의 두 가지 측정값을 보여 줍니다. 모델에 세 개의 Picasso 이미지 및 세 개의 Van Gogh 이미지가 제시되었다고 가정합니다. Picasso 샘플 중 두 개를 " Picasso" 이미지로 올바르게 식별했지만, Van Gogh 샘플 중 두 개를 Picasso로 잘못 식별했다고 가정해 보겠습니다. 이 경우에 **정밀도**는 네 개의 이미지 중 두 개를 올바르게 식별했기 때문에 50%가 됩니다. **재현율** 점수 재현율은 세 개의 Picasso 이미지 중 두 개를 올바르게 식별했기 때문에 67%가 될 것입니다.

    ![모델 학습의 결과](../media/2-portal-train-complete.png)

다음 연습에서는 포털의 빠른 테스트 기능을 사용하여 모델을 테스트할 것입니다. 그러면 모델에 이미지를 제출하고 학습 이미지에서 얻은 지식을 사용하여 모델을 분류하는 방법을 확인할 수 있습니다.

> [!TIP]
> Custom Vision 포털 UI를 사용하여 모델을 학습하는 것 외에도 [Custom Vision 교육 API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3)에서 [TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095bed) 메서드를 호출하여 학습할 수도 있습니다.