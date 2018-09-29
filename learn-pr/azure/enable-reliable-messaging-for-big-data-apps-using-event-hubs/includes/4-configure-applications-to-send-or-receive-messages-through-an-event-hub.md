<span data-ttu-id="bd384-101">이벤트 허브를 만들고 구성한 후에는 이벤트 데이터 스트림을 보내고 받도록 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-101">After you have created and configured your Event Hub, you'll need to configure applications to send and receive event data streams.</span></span>

<span data-ttu-id="bd384-102">예를 들어 결제 처리 솔루션은 발신자 응용 프로그램 형식을 사용하여 고객의 신용 카드 데이터를 수집하고 수신자 응용 프로그램 형식을 사용하여 신용 카드가 유효한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-102">For example, a payment processing solution will use some form of sender application to collect customer's credit card data and a receiver application to verify that the credit card is valid.</span></span>

<span data-ttu-id="bd384-103">Java 응용 프로그램 구성 방식에는 차이가 있지만, .NET 응용 프로그램과 비교하여 응용 프로그램을 이벤트 허브에 연결하고 메시지를 성공적으로 보내거나 받을 수 있는 일반적인 원칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-103">Although there are differences in how a Java application is configured, compared to a .NET application, there are general principles for enabling applications to connect to an Event Hub, and to successfully send or receive messages.</span></span> <span data-ttu-id="bd384-104">따라서 Java 구성 텍스트 파일을 편집하는 프로세스가 Visual Studio를 사용하여 .NET 응용 프로그램을 준비하는 것과 다르더라도 원칙은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-104">So, although the process of editing Java configuration text files is different to preparing a .NET application using Visual Studio, the principles are the same.</span></span>

## <a name="what-are-the-minimum-event-hub-application-requirements"></a><span data-ttu-id="bd384-105">최소 이벤트 허브 응용 프로그램 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="bd384-105">What are the minimum Event Hub application requirements?</span></span>

<span data-ttu-id="bd384-106">이벤트 허브로 메시지를 보내도록 응용 프로그램을 구성하려면, 응용 프로그램이 연결 자격 증명을 만들 수 있도록 다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-106">To configure an application to send messages to an Event Hub, you must provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="bd384-107">이벤트 허브 네임스페이스 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-107">Event Hub namespace name</span></span>
- <span data-ttu-id="bd384-108">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-108">Event Hub name</span></span>
- <span data-ttu-id="bd384-109">공유 액세스 정책 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-109">Shared access policy name</span></span>
- <span data-ttu-id="bd384-110">기본 공유 선택키</span><span class="sxs-lookup"><span data-stu-id="bd384-110">Primary shared access key</span></span>

<span data-ttu-id="bd384-111">이벤트 허브에서 메시지를 받도록 응용 프로그램을 구성하려면, 응용 프로그램이 연결 자격 증명을 만들 수 있도록 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-111">To configure an application to receive messages from an Event Hub, provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="bd384-112">이벤트 허브 네임스페이스 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-112">Event Hub namespace name</span></span>
- <span data-ttu-id="bd384-113">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-113">Event Hub name</span></span>
- <span data-ttu-id="bd384-114">공유 액세스 정책 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-114">Shared access policy name</span></span>
- <span data-ttu-id="bd384-115">기본 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="bd384-115">Primary shared access key</span></span>
- <span data-ttu-id="bd384-116">Storage 계정 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-116">Storage account name</span></span>
- <span data-ttu-id="bd384-117">저장소 계정 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="bd384-117">Storage account connection string</span></span>
- <span data-ttu-id="bd384-118">저장소 계정 컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="bd384-118">Storage account container name</span></span>

<span data-ttu-id="bd384-119">Azure Blob Storage에 메시지를 저장하는 수신자 응용 프로그램이 있는 경우 먼저 저장소 계정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-119">If you have a receiver application that stores messages in Azure Blob Storage, you'll also need to first configure a storage account.</span></span>

## <a name="azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a><span data-ttu-id="bd384-120">범용 표준 저장소 계정을 만들기 위한 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="bd384-120">Azure CLI commands for creating a general-purpose standard storage account</span></span>

<span data-ttu-id="bd384-121">Azure CLI는 저장소 계정을 만들고 관리하는 데 사용할 수 있는 명령 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-121">The Azure CLI provides a set of commands you can use to create and manage a storage account.</span></span> <span data-ttu-id="bd384-122">이 부분에 대해서는 다음 단원에서 살펴볼 예정이지만 명령의 기본적인 개요를 살펴보면 이렇습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-122">We'll work with them in the next unit, but here's a basic synopsis of the commands.</span></span> 

> [!TIP]
> <span data-ttu-id="bd384-123">저장소 계정을 다루는 MS 학습 모듈은 **Azure Storage 소개** 모듈을 시작으로 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-123">There are several MS Learn modules that cover storage accounts, starting in the module **Introduction to Azure Storage**.</span></span>

| <span data-ttu-id="bd384-124">명령</span><span class="sxs-lookup"><span data-stu-id="bd384-124">Command</span></span> | <span data-ttu-id="bd384-125">설명</span><span class="sxs-lookup"><span data-stu-id="bd384-125">Description</span></span> |
|---------|-------------|
| `storage account create` | <span data-ttu-id="bd384-126">범용 v2 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-126">Create a general-purpose V2 Storage account.</span></span> |
| `storage account key list` | <span data-ttu-id="bd384-127">저장소 계정 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-127">Retrieve the storage account key.</span></span> |
| `storage account show-connection-string` | <span data-ttu-id="bd384-128">Azure Storage 계정의 연결 문자열을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-128">Retrieve the connection string for an Azure Storage account.</span></span> |
| `storage container create` | <span data-ttu-id="bd384-129">저장소 계정으로 새 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-129">Creates a new container in a storage account.</span></span> |

## <a name="shell-command-for-cloning-an-application-github-repository"></a><span data-ttu-id="bd384-130">응용 프로그램 GitHub 리포지토리를 복제하기 위한 셸 명령</span><span class="sxs-lookup"><span data-stu-id="bd384-130">Shell command for cloning an application GitHub repository</span></span>

<span data-ttu-id="bd384-131">Git은 배포 버전 제어 모델을 사용하는 공동 작업 도구이며 소프트웨어 및 문서 프로젝트에 대한 공동 작업을 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-131">Git is a collaboration tool that uses a distributed version control model, and is designed for collaborative working on software and documentation projects.</span></span> <span data-ttu-id="bd384-132">Git 클라이언트는 Windows를 비롯한 여러 플랫폼에서 사용할 수 있으며 Git 명령줄은 Azure Bash Cloud Shell에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-132">Git clients are available for multiple platforms, including Windows, and the Git command line is included in the Azure Bash cloud shell.</span></span> <span data-ttu-id="bd384-133">GitHub는 Git 리포지토리에 대한 웹 기반 호스팅 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-133">GitHub is a web-based hosting service for Git repositories.</span></span> 

<span data-ttu-id="bd384-134">GitHub에서 프로젝트로 호스트되는 응용 프로그램이 있는 경우 **git clone** 명령을 사용하여 리포지토리를 복제하면 프로젝트의 로컬 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-134">If you have an application that is hosted as a project in GitHub, you can make a local copy of the project, by cloning its repository using the **git clone** command.</span></span> <span data-ttu-id="bd384-135">이 작업은 다음 단원에서 수행할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-135">We'll do this in the next unit.</span></span>

## <a name="editing-files-in-the-cloud-shell"></a><span data-ttu-id="bd384-136">Cloud Shell에서 파일 편집</span><span class="sxs-lookup"><span data-stu-id="bd384-136">Editing files in the Cloud SHell</span></span>

<span data-ttu-id="bd384-137">Cloud Shell에 기본 제공되는 편집기 중 하나를 사용하여 응용 프로그램을 구성하는 모든 파일을 수정하고, 이벤트 허브 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-137">You can use one of the built-in editors in the Cloud Shell to modify all the files that make up the application and add your Event Hub namespace, Event Hub name, shared access policy name, and primary key.</span></span> 

<span data-ttu-id="bd384-138">Cloud Shell은 **nano**, **vim**, **emacs** 및 Visual Studio Code와 유사한 **code**라는 편집기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-138">The Cloud Shell supports **nano**, **vim** and **emacs** as well as a Visual Studio Code-like editor named **code**.</span></span> <span data-ttu-id="bd384-139">원하는 편집기의 이름을 입력하기만 하면 사용자 환경에서 편집기가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-139">Just type the name of the editor you want and it will launch in the environment.</span></span> <span data-ttu-id="bd384-140">다음 단원에서는 **code** 편집기를 사용할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-140">We'll use the **code** editor in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="bd384-141">요약</span><span class="sxs-lookup"><span data-stu-id="bd384-141">Summary</span></span>

<span data-ttu-id="bd384-142">발신자 및 수신자 응용 프로그램은 이벤트 허브 환경에 대한 특정 정보로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-142">Sender and receiver applications must be configured with specific information about the Event Hub environment.</span></span> <span data-ttu-id="bd384-143">수신자 응용 프로그램이 메시지를 Blob Storage에 저장하는 경우 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-143">You create a storage account if your receiver application stores messages in Blob Storage.</span></span> <span data-ttu-id="bd384-144">응용 프로그램이 GitHub에서 호스트되는 경우 응용 프로그램을 로컬 디렉터리에 복제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-144">If your application is hosted on GitHub, you have to clone it to your local directory.</span></span> <span data-ttu-id="bd384-145">**nano**와 같은 텍스트 편집기는 네임스페이스를 응용 프로그램에 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd384-145">Text editors, such as **nano** are used to add your namespace to the application.</span></span>