<span data-ttu-id="534e8-101">빅 데이터 응용 프로그램은 증가한 트랜잭션 볼륨에 맞게 규모를 확장하여 증가한 처리량을 처리하는 기능이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-101">Big data applications should have the ability to process increased throughput by scaling out to meet increased transaction volumes.</span></span>

<span data-ttu-id="534e8-102">은행의 신용 카드 부서에서 근무한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-102">Suppose you work in the credit card department of a bank.</span></span> <span data-ttu-id="534e8-103">각 트랜잭션을 승인 또는 거부할지 결정하기 위해 사기 테스트를 담당하는 시스템을 관리하는 팀의 팀원입니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-103">You're part of a team that manages the system responsible for fraud testing to determine whether to approve or decline each transaction.</span></span> <span data-ttu-id="534e8-104">시스템은 트랜잭션 스트림을 수신하고 실시간으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-104">Your system receives a stream of transactions and needs to process them in real time.</span></span>

<span data-ttu-id="534e8-105">시스템의 부하는 주말 및 휴일 중에 급증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-105">The load on your system can spike during weekends and holidays.</span></span> <span data-ttu-id="534e8-106">따라서 증가한 처리량을 효율적으로 정확하게 처리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-106">It should be able to handle increased throughput efficiently and accurately.</span></span> <span data-ttu-id="534e8-107">트랜잭션의 민감한 특성을 고려하면 최소한의 오류도 큰 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-107">Given the sensitive nature of the transactions, even the slightest error can have a huge impact.</span></span>

<span data-ttu-id="534e8-108">Azure Event Hubs는 많은 트랜잭션을 수신하고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-108">Azure Event Hubs can receive and process large number of transactions.</span></span> <span data-ttu-id="534e8-109">또한 증가한 처리량을 처리하기 위해 필요할 때 동적으로 크기를 조정하도록 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-109">It can also be configured to scale dynamically, when required, to handle increased throughput.</span></span>
<span data-ttu-id="534e8-110">이 모듈에서는 Event Hubs를 응용 프로그램에 연결하고 대량의 트랜잭션 볼륨을 안정적으로 처리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-110">In this module, you’ll learn how to connect Event Hubs to your application and reliably process huge transaction volumes.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="534e8-111">학습 목표</span><span class="sxs-lookup"><span data-stu-id="534e8-111">Learning objectives</span></span>

<span data-ttu-id="534e8-112">이 모듈에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-112">In this module, you will:</span></span>

- <span data-ttu-id="534e8-113">Azure CLI를 사용하여 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-113">Create an event hub using the Azure CLI.</span></span>
- <span data-ttu-id="534e8-114">이벤트 허브를 통해 메시지를 보내거나 받도록 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-114">Configure applications to send or receive messages through an event hub.</span></span>
- <span data-ttu-id="534e8-115">Azure Portal을 사용하여 이벤트 허브 성능을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="534e8-115">Evaluate event hub performance using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="534e8-116">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="534e8-116">Prerequisites</span></span>

- <span data-ttu-id="534e8-117">Azure Portal을 사용하여 리소스를 만들고 관리한 경험.</span><span class="sxs-lookup"><span data-stu-id="534e8-117">Experience creating and managing resources using the Azure portal.</span></span>
- <span data-ttu-id="534e8-118">Azure CLI를 사용 하 여 Azure에 로그인 하 고 리소스를 만들 수을 경험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="534e8-118">Experience with using Azure CLI to sign into Azure, and to create resources.</span></span>
- <span data-ttu-id="534e8-119">스트리밍 및 이벤트 처리와 같은 기본 빅 데이터 개념에 대한 지식.</span><span class="sxs-lookup"><span data-stu-id="534e8-119">Knowledge of basic big data concepts such as streaming and event processing.</span></span>
