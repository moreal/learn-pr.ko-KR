이 단원에서는 이전 연습에서 업로드한 이미지와 태그 지정된 이미지를 사용하여 모델을 학습합니다. 포털에서 단추를 클릭하거나 [Custom Vision 교육 API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3)에서 [TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095bed) 메서드를 호출하여 간단히 학습을 진행할 수 있습니다. 모델을 학습하면 추가 태그 지정 이미지를 업로드하고 재학습하여 모델을 미세 조정할 수 있습니다.

1. 페이지 위쪽의 **학습** 단추를 클릭하여 모델을 학습합니다. 모델을 학습할 때마다 새로운 반복이 생성됩니다. Custom Vision Service는 여러 반복을 유지하므로 시간에 따른 진행 상황을 비교할 수 있습니다.

    ![모델 학습](../media/2-portal-click-train.png)

1. 학습 프로세스가 완료될 때까지 대기합니다. 몇 초면 끝납니다. 그런 다음, 반복 1에 표시된 학습 통계를 검토합니다. **정밀도** 및 **재현율**은 별개이지만 모델의 정확도와 관련된 측정값입니다. 모델에 세 개의 Picasso 작품과 세 개의 Van Gogh 작품이 제공되고, Picasso 작품 중 2개는 “Picasso” 이미지로 올바르게 식별되었지만 Van Gogh 작품 중 2개는 Picasso 작품으로 잘못 식별되었다고 가정해봅니다. 이 경우에 정밀도는 50%(Picasso 작품으로 분류된 4개 이미지 중 2개가 실제로 Picasso 작품임)이지만, 재현율은 67%(3개의 Picasso 이미지 중 2개가 Picasso 작품으로 올바르게 식별됨)입니다.

    ![모델 학습의 결과](../media/2-portal-train-complete.png)

이제 포털의 빠른 테스트 기능을 사용하여 모델을 테스트합니다. 그러면 모델에 이미지를 제출하고 학습 이미지에서 얻은 지식을 사용하여 분류하는 방법을 확인할 수 있습니다.