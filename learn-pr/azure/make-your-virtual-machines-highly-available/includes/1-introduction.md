<span data-ttu-id="7c465-101">대형 은행의 서버 관리자로 작업한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c465-101">Suppose you work as the server administrator for a large bank.</span></span> <span data-ttu-id="7c465-102">고객이 인터넷이나 모바일 장치에서 계정을 쉽게 확인할 수 있는 새로운 뱅킹 포털을 시작하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7c465-102">You are launching a new banking portal for your customers that will enable them to easily check their account from the Internet or mobile device.</span></span> <span data-ttu-id="7c465-103">이 응용 프로그램은 중요 비즈니스용이며 서버 장애 또는 소프트웨어 업그레이드로 인한 가동 중지 시간을 최소화하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c465-103">The application is business-critical, and you want to minimize the downtime that results from server failure or upgrades to the software.</span></span>

<span data-ttu-id="7c465-104">Azure에서 시작하므로 제공되는 몇 가지 확장성 옵션을 활용하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c465-104">Since you are launching on Azure, you want to take advantage of some of the scalability options it provides.</span></span> <span data-ttu-id="7c465-105">목표는 부하 분산 장치가 이러한 유형의 응용 프로그램에 적합한지, 적합한 경우 시스템을 배포 및 구성하는 방법을 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c465-105">Your goal is to determine if a load balancer is appropriate for this type of application, and if so, how to deploy and configure the system.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="7c465-106">학습 목표:</span><span class="sxs-lookup"><span data-stu-id="7c465-106">Learning objectives:</span></span>

<span data-ttu-id="7c465-107">이 모듈에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c465-107">In this module, you will:</span></span>

- <span data-ttu-id="7c465-108">부하 분산 장치를 사용하는 시기 결정</span><span class="sxs-lookup"><span data-stu-id="7c465-108">Decide when to use a load balancer</span></span>
- <span data-ttu-id="7c465-109">기본 부하 분산 장치와 표준 부하 분산 장치 버전 간의 차이점 식별</span><span class="sxs-lookup"><span data-stu-id="7c465-109">Identify the differences between the basic and standard Load Balancer editions</span></span>
- <span data-ttu-id="7c465-110">새 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="7c465-110">Create a new load balancer</span></span>
- <span data-ttu-id="7c465-111">부하 분산 장치와 연결된 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="7c465-111">Create virtual networks associated with a load balancer</span></span>
- <span data-ttu-id="7c465-112">부하 분산 장치 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="7c465-112">Configure load balancer rules</span></span>
- <span data-ttu-id="7c465-113">부하 분산 장치 상태 프로브 구성</span><span class="sxs-lookup"><span data-stu-id="7c465-113">Configure a load balancer health probe</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c465-114">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7c465-114">Prerequisites</span></span>  

- <span data-ttu-id="7c465-115">Azure CLI 환경</span><span class="sxs-lookup"><span data-stu-id="7c465-115">Experience with the Azure CLI</span></span>
- <span data-ttu-id="7c465-116">Azure Portal을 사용하여 Azure 리소스 관리 경험</span><span class="sxs-lookup"><span data-stu-id="7c465-116">Experience administering Azure resources using the Azure portal</span></span>
- <span data-ttu-id="7c465-117">Azure Virtual Machines 환경</span><span class="sxs-lookup"><span data-stu-id="7c465-117">Experience with Azure Virtual Machines</span></span>
- <span data-ttu-id="7c465-118">가상 머신 네트워킹 및 공용 IP 주소에 대한 약간의 지식</span><span class="sxs-lookup"><span data-stu-id="7c465-118">Some knowledge of virtual-machine networking and public IP addresses</span></span>