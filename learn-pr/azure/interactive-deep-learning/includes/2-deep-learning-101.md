## <a name="intro-to-deep-learning"></a><span data-ttu-id="4b539-101">심층 학습 소개</span><span class="sxs-lookup"><span data-stu-id="4b539-101">Intro to deep learning</span></span>

<span data-ttu-id="4b539-102">ML(기계 학습)의 목표는 그림, 시계열, 오디오 등의 입력 데이터를 캡션, 가격 값, 전사 등의 지정된 출력으로 변환하는 모델을 학습시키는 기능을 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-102">The goal of Machine Learning ML is to find features to train a model that transforms input data (such as pictures, time series, or audio) to a given output (for example captions, price values, transcriptions).</span></span> <span data-ttu-id="4b539-103">기존 데이터 과학에서는 기능을 수동으로 선택하는 경우가 많았습니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-103">In traditional data science, features are often hand-picked.</span></span>

![피드 전달 심층 신경망의 정식 예제.](../media/2-image1.PNG)

<span data-ttu-id="4b539-105">DL(심층 학습)에서는 입력을 벡터로 표시한 다음 일련의 지능적 선형 대수 연산을 수행하여 지정된 출력으로 변환하는 과정을 통해 기능 추출 프로세스를 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-105">In Deep Learning (DL), the process of feature extraction is learned through representing inputs as vectors and transforming them, with a series of clever linear algebra operations, into a given output.</span></span>  

<span data-ttu-id="4b539-106">그런 후에 손실 함수라는 수식을 사용하여 모델 출력을 필요한 출력과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-106">The model output is then compared against the expected output using an equation called a loss function.</span></span> <span data-ttu-id="4b539-107">각 학습 입력의 손실 함수에서 반환하는 값을 사용하여 모델에 기능 추출 방법을 안내합니다. 따라서 다음 단계에서는 손실 값이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-107">The value returned by the loss function of each training input is used to guide the model to extract features that will result in a lower loss value on the next pass.</span></span>  
 
<span data-ttu-id="4b539-108">선형 대수 구성 요소의 일부분으로 처리되는 일련의 행렬 연산은 대개 계산을 많이 수행하며 매우 상세하게 병렬화할 수 있는 경우가 많으므로 계산을 효율적으로 수행하려면 GPU(그래픽 처리 장치)와 같은 특수 계산 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-108">The series of matrix operations that we computer as part of the linear algebra component tend to be computationally expensive and are often heavily parallelizable, requiring specialized compute such as Graphics Processing Units GPUs to compute efficiently.</span></span>

## <a name="data-science-virtual-machine"></a><span data-ttu-id="4b539-109">Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="4b539-109">Data Science Virtual Machine</span></span>

![DSVM 옵션](../media/2-image2.PNG)

<span data-ttu-id="4b539-111">DSVM은 미리 설치 및 구성되어 있는 Azure Virtual Machine 이미지로, 데이터 분석/기계 학습/심층 학습 교육에 일반적으로 사용되는 몇 가지 인기 도구를 사용하여 테스트를 거쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-111">DSVMs are Azure Virtual Machine images, pre-installed, configured, and tested with several popular tools that are commonly used for data analytics, machine learning, and deep learning training.</span></span>

<span data-ttu-id="4b539-112">DSVM에서 제공하는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-112">They provide:</span></span>

- <span data-ttu-id="4b539-113">팀 전체에서 일관된 설정 사용 가능/더욱 원활한 공유 및 공동 작업 가능/Azure 크기 조정 및 관리 기능/설정 작업이 거의 필요하지 않음/데이터 과학용으로 제공되는 완전한 클라우드 기반 데스크톱.</span><span class="sxs-lookup"><span data-stu-id="4b539-113">Consistent setup across team, promote sharing and collaboration, Azure scale and management, Near-Zero Setup, full cloud-based desktop for data science.</span></span>
- <span data-ttu-id="4b539-114">주문형 탄력적 용량/수직 및 수평 크기 조정을 통해 모든 Azure 하드웨어 구성에서 분석을 실행하는 기능.</span><span class="sxs-lookup"><span data-stu-id="4b539-114">On-demand elastic capacity Ability to run analytics on all Azure hardware configurations with vertical and horizontal scaling.</span></span> <span data-ttu-id="4b539-115">기능 사용 시 사용한 만큼만 요금 지불.</span><span class="sxs-lookup"><span data-stu-id="4b539-115">Pay only for what you use, when you use it.</span></span>
- <span data-ttu-id="4b539-116">GPU를 사용하는 심층 학습/심층 학습 도구가 이미 미리 구성되어 있는 즉시 사용 가능한 GPU 클러스터.</span><span class="sxs-lookup"><span data-stu-id="4b539-116">Deep Learning with GPUs Readily available GPU clusters with Deep Learning tools already pre-configured.</span></span> 

<span data-ttu-id="4b539-117">DSVM에는 인기 심층 학습 프레임워크 및 도구(예: Microsoft R Server Developer Edition, Anaconda Python, Python/R용 Jupyter Notebook, Python/R용 IDE, SQL 데이터베이스 및 기타 여러 데이터 과학/ML 도구)의 GPU 버전을 비롯하여 다양한 AI용 도구가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-117">The DSVM contains several tools for AI including popular GPU editions of deep learning frameworks and tools such as Microsoft R Server Developer Edition, Anaconda Python, Jupyter notebooks for Python and R, IDEs for Python and R, SQL database and many other data science and ML tools.</span></span>

<span data-ttu-id="4b539-118">DSVM은 Azure GPU NC 시리즈 VM 인스턴스에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-118">The DSVM can run on Azure GPU NC-series VM instances.</span></span> <span data-ttu-id="4b539-119">이러한 GPU는 불연속 장치 할당 방식을 사용하므로 운영 체제 미설치 컴퓨터에 가까운 성능이 제공되며, 심층 학습 문제를 해결하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4b539-119">These GPUs use discrete device assignment, resulting in performance close to bare-metal, and are well-suited to deep learning problems.</span></span>

<!--### Quiz? 

What is the goal of machine learning? 
How is traditional machine learning different from deep learning? 
Why are GPU's often used for deep learning? 
What does the DSVM provide? -->
