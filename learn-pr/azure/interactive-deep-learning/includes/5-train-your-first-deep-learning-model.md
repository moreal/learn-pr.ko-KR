## <a name="train-your-first-deep-learning-model-using-pytorch-and-jupyter"></a><span data-ttu-id="ca0f0-101">PyTorch 및 Jupyter를 사용하여 첫 번째 심층 학습 모델 학습시키기</span><span class="sxs-lookup"><span data-stu-id="ca0f0-101">Train your first deep learning model using PyTorch and Jupyter</span></span>

![PyTorch 로고](../media/5-image1.PNG) 

<span data-ttu-id="ca0f0-103">심층 학습 엔지니어는 대개 모든 행렬 대수 연산을 수동으로 하드 코드하지 않으며,</span><span class="sxs-lookup"><span data-stu-id="ca0f0-103">Typically deep learning engineers do not hard code matrix algebra operations all by hand.</span></span> <span data-ttu-id="ca0f0-104">대신 PyTorch나 TensorFlow 등의 프레임워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-104">They instead use frameworks such as PyTorch or TensorFlow.</span></span>  

<span data-ttu-id="ca0f0-105">PyTorch는 유연한 심층 학습 개발 플랫폼으로 사용 가능한 python 기반 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-105">PyTorch is a python-based framework that provides flexibility as a deep learning development platform.</span></span> <span data-ttu-id="ca0f0-106">PyTorch의 워크플로는 python의 공학용 컴퓨팅 라이브러리인 nympy를 기반으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-106">PyTorch's workflow is built on top of python scientific computing library numpy.</span></span> 

<span data-ttu-id="ca0f0-107">그렇다면 PyTorch를 사용하여 심층 학습 모델을 작성하는 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ca0f0-107">Now you might ask, why would we use PyTorch to build deep learning models?</span></span>  

- <span data-ttu-id="ca0f0-108">간편하게 사용 가능한 API - PyTorch는 매우 단순한 python 기반 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-108">Easy to use API – It's as simple as python can be.</span></span>
- <span data-ttu-id="ca0f0-109">python 지원 – PyTorch는 공학용 컴퓨팅 스택과 원활하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-109">Python support – PyTorch smoothly integrates with the scientific computing stack.</span></span>
- <span data-ttu-id="ca0f0-110">동적 계산 그래프 – PyTorch는 특정 기능을 포함하는 미리 정의된 그래프를 제공하는 대신, 런타임에 수정 가능한 계산 그래프를 동적으로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-110">Dynamic computation graphs – Instead of predefined graphs with specific functionalities, PyTorch build computational graphs dynamically that can be modified during runtime.</span></span> <span data-ttu-id="ca0f0-111">동적 계산 그래프는 중첩 일괄 처리를 수행할 때, 그리고 지정된 네트워크를 만드는 데 필요한 메모리의 양을 모를 때 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-111">Dynamic computation graphs are valuable for nested batching and when we do not know how much memory will be needed for creating a given network.</span></span>

## <a name="run-your-first-pytorch-model"></a><span data-ttu-id="ca0f0-112">첫 번째 PyTorch 모델 실행</span><span class="sxs-lookup"><span data-stu-id="ca0f0-112">Run your first PyTorch model</span></span>

<span data-ttu-id="ca0f0-113">마지막 장에서 설정한 Jupyter Notebook으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-113">Navigate to the Jupyter Notebook that you set up in the last chapter.</span></span>

- <span data-ttu-id="ca0f0-114">[[DSVM의 호스트 이름]].westus2.cloudapp.azure.com:8888/?token={토큰}</span><span class="sxs-lookup"><span data-stu-id="ca0f0-114">[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com:8888/?token={sometoken}</span></span>

<span data-ttu-id="ca0f0-115">first_pytorch_classifier.ipynb Notebook을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-115">Select the first_pytorch_classifier.ipynb notebook</span></span>

![first_pytorch_classifier.ipynb 선택](../media/5-image2.PNG)

<span data-ttu-id="ca0f0-117">Notebook의 지침에 따라 첫 번째 PyTorch 분류자를 학습시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ca0f0-117">Follow the instructions in the notebook to train your first PyTorch classifer.</span></span>

![Notebook 스크린샷](../media/5-image3.PNG)
