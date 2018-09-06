Linux용 **Data Science Virtual Machine**은 데이터 과학을 간편하게 시작하도록 하는 가상 머신 이미지입니다. 빠르게 가동하고 실행하기 위해 이미 여러 도구가 빌드, 설치 및 구성되어 있습니다. Jupyter 및 TensorFlow와 마찬가지로 NVIDIA GPU 드라이버, NVIDIA CUDA 및 NVIDIA cuDNN(CUDA Deep Neural Network) 라이브러리도 포함되어 있습니다. 미리 설치된 모든 프레임워크는 GPU를 지원하지만, CPU에서도 작동합니다.

## <a name="what-is-covered-in-this-lab"></a>이 랩에서 다루는 내용은 무엇인가요?

 이 랩에서는 다음을 수행합니다.
* Azure에서 Linux Data Science Virtual Machine 만들기
* 원격 데스크톱을 통해 DSVM에 연결
* TensorFlow 모델을 학습하여 핫도그를 포함하는 이미지와 포함하지 않는 이미지 분류
* Python 앱에서 모델 사용

이 랩을 완료하려면 Azure 구독 및 Xfce 원격 데스크톱 클라이언트가 필요합니다. 자세한 내용은 필수 구성 요소 섹션을 참조하세요. Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F)을 만듭니다.

### <a name="prerequisites-for-the-lab"></a>랩의 필수 구성 요소

 1. **Microsoft Azure 계정**: 이 랩을 진행하려면 유효한 활성 Azure 계정이 필요합니다. 아직 등록하지 않은 경우 [평가판](https://azure.microsoft.com/en-us/free/)에 등록할 수 있습니다.

    * Visual Studio 활성 구독자인 경우 매월 $50-$150의 크레딧을 받을 수 있습니다. 정품 인증을 하고 월별 Azure 크레딧 사용을 시작하는 방법을 포함하는 자세한 내용을 알아보려면 이 [링크](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/)를 참조하세요.

    * Visual Studio 구독자가 아닌 경우 [Visual Studio Dev Essentials](https://www.visualstudio.com/dev-essentials/) 체험 프로그램에 등록하여 **Azure 체험 계정**(1년 체험 서비스와 첫 달 $200 크레딧 포함)을 만들 수 있습니다.

    * 학생인 경우 신용 카드 없이 [학생용 Azure](https://aka.ms/azure4students) 체험 계정에 등록하여 $100의 Azure 크레딧과 1년 체험 서비스를 이용할 수 있습니다. 

1. [X2Go](https://wiki.x2go.org/doku.php/download:start)와 같은 [Xfce](https://xfce.org/) 원격 데스크톱 클라이언트