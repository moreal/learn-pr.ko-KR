<span data-ttu-id="b0f5f-101">이벤트 허브를 만들고 구성한 후에는 이벤트 데이터 스트림을 보내고 받도록 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-101">After you have created and configured your event hub, you'll need to configure applications to send and receive event data streams.</span></span>

<span data-ttu-id="b0f5f-102">예를 들어 결제 처리 솔루션은 발신자 응용 프로그램 형식을 사용하여 고객의 신용 카드 데이터를 수집하고 수신자 응용 프로그램 형식을 사용하여 신용 카드가 유효한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-102">For example, a payment processing solution will use some form of sender application to collect customer's credit card data and a receiver application to verify that the credit card is valid.</span></span>

<span data-ttu-id="b0f5f-103">Java 응용 프로그램 구성 방식에는 차이가 있지만, .NET 응용 프로그램과 비교하여 응용 프로그램을 이벤트 허브에 연결하고 메시지를 성공적으로 보내거나 받을 수 있는 일반적인 원칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-103">Although there are differences in how a Java application is configured, compared to a .NET application, there are general principles for enabling applications to connect to an event hub, and to successfully send or receive messages.</span></span> <span data-ttu-id="b0f5f-104">따라서 Java 구성 텍스트 파일을 편집하는 프로세스가 Visual Studio를 사용하여 .NET 응용 프로그램을 준비하는 것과 다르더라도 원칙은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-104">So, although the process of editing Java configuration text files is different to preparing a .NET application using Visual Studio, the principles are the same.</span></span>

## <a name="what-are-the-minimum-event-hub-application-requirements"></a><span data-ttu-id="b0f5f-105">최소 이벤트 허브 응용 프로그램 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b0f5f-105">What are the minimum Event Hub application requirements?</span></span>

<span data-ttu-id="b0f5f-106">이벤트 허브로 메시지를 보내도록 응용 프로그램을 구성하려면, 응용 프로그램이 연결 자격 증명을 만들 수 있도록 다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-106">To configure an application to send messages to an event hub, you must provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="b0f5f-107">이벤트 허브 네임스페이스 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-107">Event hub namespace name</span></span>
- <span data-ttu-id="b0f5f-108">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-108">Event hub name</span></span>
- <span data-ttu-id="b0f5f-109">공유 액세스 정책 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-109">Shared access policy name</span></span>
- <span data-ttu-id="b0f5f-110">기본 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="b0f5f-110">Primary shared access key</span></span>

<span data-ttu-id="b0f5f-111">이벤트 허브에서 메시지를 받도록 응용 프로그램을 구성하려면, 응용 프로그램이 연결 자격 증명을 만들 수 있도록 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-111">To configure an application to receive messages from an event hub, provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="b0f5f-112">이벤트 허브 네임스페이스 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-112">Event hub namespace name</span></span>
- <span data-ttu-id="b0f5f-113">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-113">Event hub name</span></span>
- <span data-ttu-id="b0f5f-114">공유 액세스 정책 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-114">Shared access policy name</span></span>
- <span data-ttu-id="b0f5f-115">기본 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="b0f5f-115">Primary shared access key</span></span>
- <span data-ttu-id="b0f5f-116">Storage 계정 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-116">Storage account name</span></span>
- <span data-ttu-id="b0f5f-117">저장소 계정 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="b0f5f-117">Storage account connection string</span></span>
- <span data-ttu-id="b0f5f-118">저장소 계정 컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="b0f5f-118">Storage account container name</span></span>

<span data-ttu-id="b0f5f-119">Azure Blob Storage에 메시지를 저장하는 수신자 응용 프로그램이 있는 경우 먼저 저장소 계정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-119">If you have a receiver application that stores messages in Azure Blob Storage, you'll also need to first configure a storage account.</span></span>

## <a name="the-azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a><span data-ttu-id="b0f5f-120">범용 표준 저장소 계정을 만들기 위한 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="b0f5f-120">The Azure CLI commands for creating a general-purpose standard storage account</span></span>

1. <span data-ttu-id="b0f5f-121">리소스 그룹 및 리소스 그룹을 만들 때 사용한 것과 동일한 Azure 데이터 센터 위치에 저장소 계정(범용 V2)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-121">Create the Storage account (general-purpose V2) in your resource group, and the same Azure datacenter location that you used when creating the resource group.</span></span>

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name> --location <location> --sku Standard_RAGRS --encryption blob
    ```

1. <span data-ttu-id="b0f5f-122">이 저장소에 액세스하려면 저장소 계정 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-122">To access this storage, you'll need a storage account access key.</span></span> <span data-ttu-id="b0f5f-123">저장소 계정과 연결된 액세스 키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-123">View the access keys that are associated with the storage account.</span></span>

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

1. <span data-ttu-id="b0f5f-124">**key1**과 연결된 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-124">Save the value associated with **key1**.</span></span>

1. <span data-ttu-id="b0f5f-125">저장소 계정에 대한 연결 정보도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-125">You will also need the connection details for the storage account.</span></span> <span data-ttu-id="b0f5f-126">저장소 계정에 대한 연결 문자열을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-126">View the connection string for the storage account.</span></span>

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

1. <span data-ttu-id="b0f5f-127">**connectionString**과 연결된 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-127">Save the value associated with the **connectionString**.</span></span>

1. <span data-ttu-id="b0f5f-128">메시지는 저장소 계정 내의 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-128">Messages will be stored in a container within your storage account.</span></span> <span data-ttu-id="b0f5f-129">이전 단계의 연결 문자열과 함께 `<connection string>`을 사용하여 저장소 계정에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-129">Create a container in your storage account, using `<connection string>` with the connection string from the previous step.</span></span>

    ```azurecli
    az storage container create -n <container> --connection-string "<connection string>"
    ```

## <a name="shell-command-for-cloning-an-application-github-repository"></a><span data-ttu-id="b0f5f-130">응용 프로그램 GitHub 리포지토리를 복제하기 위한 셸 명령</span><span class="sxs-lookup"><span data-stu-id="b0f5f-130">Shell command for cloning an application GitHub repository</span></span>

<span data-ttu-id="b0f5f-131">Git은 배포 버전 제어 모델을 사용하는 공동 작업 도구이며 소프트웨어 및 문서 프로젝트에 대한 공동 작업을 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-131">Git is a collaboration tool that uses a distributed version control model, and is designed for collaborative working on software and documentation projects.</span></span> <span data-ttu-id="b0f5f-132">Git 클라이언트는 Windows를 비롯한 여러 플랫폼에서 사용할 수 있으며 Git 명령줄은 Azure Bash Cloud Shell에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-132">Git clients are available for multiple platforms, including Windows, and the Git command line is included in the Azure Bash cloud shell.</span></span> <span data-ttu-id="b0f5f-133">GitHub는 Git 리포지토리에 대한 웹 기반 호스팅 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-133">GitHub is a web-based hosting service for Git repositories.</span></span> 

<span data-ttu-id="b0f5f-134">GitHub에서 프로젝트로 호스트되는 응용 프로그램이 있는 경우 **git clone** 명령을 사용하여 리포지토리를 복제하면 프로젝트의 로컬 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-134">If you have an application that is hosted as a project in GitHub, you can make a local copy of the project, by cloning its repository using the **git clone** command.</span></span>

1. <span data-ttu-id="b0f5f-135">리포지토리를 홈 디렉터리에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-135">Clone a repository to your home directory.</span></span>

    ```azurecli
      git clone https://github.com/<project repository>
    ```

## <a name="shell-commands-for-preparing-an-application"></a><span data-ttu-id="b0f5f-136">응용 프로그램을 준비하기 위한 셸 명령</span><span class="sxs-lookup"><span data-stu-id="b0f5f-136">Shell commands for preparing an application</span></span>

1. <span data-ttu-id="b0f5f-137">이제 **nano**와 같은 편집기를 사용하여 응용 프로그램을 편집하고 이벤트 허브 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-137">You can now use an editor, such as **nano** to edit the application and add your event hub namespace, event hub name, shared access policy name, and primary key.</span></span> <span data-ttu-id="b0f5f-138">Nano는 Linux 및 기타 Unix 같은 운영 체제에 사용할 수 있는 간단한 텍스트 편집기이며, Azure Bash Cloud Shell에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-138">Nano is a simple text editor available for Linux and other Unix-like operating systems; it is also available in the Azure Bash cloud shell.</span></span> <span data-ttu-id="b0f5f-139">예를 들어 이 명령을 사용하여 **nano** 편집기에서 Java 응용 프로그램 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-139">For example, use this command to open a Java application file in the **nano** editor.</span></span>

    ```azurecli
    nano <application>.java
    ```

1. <span data-ttu-id="b0f5f-140">응용 프로그램 개발 방법에 따라 이벤트 허브 구성 정보를 추가한 후 응용 프로그램을 컴파일하거나 빌드해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-140">Depending on how your applications are developed, you may need to compile or build the application after you've added the event hub configuration information.</span></span> <span data-ttu-id="b0f5f-141">예를 들어 다음 단원에서 사용되는 Java 응용 프로그램은 Apache **Maven**과 같은 도구를 사용하여 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-141">For example, the Java applications used in the next unit need to be built using a tool such as Apache **Maven**.</span></span> <span data-ttu-id="b0f5f-142">Maven은 .java 파일을 .class 파일로 컴파일하거나 .jar 파일로 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-142">Maven compiles .java files into .class files or packages them into .jar files.</span></span> <span data-ttu-id="b0f5f-143">Maven은 Bash Cloud Shell에서 사용할 수 있으며, Java 응용 프로그램을 빌드하려면 **mvn** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-143">Maven is available from the Bash cloud shell; to build the Java application, you use **mvn** commands.</span></span> <span data-ttu-id="b0f5f-144">이 mvn 명령을 사용하여 Java 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-144">Use this mvn command to build a Java  application.</span></span>

    ```azurecli
    mvn clean package -DskipTests
    ```

## <a name="summary"></a><span data-ttu-id="b0f5f-145">요약</span><span class="sxs-lookup"><span data-stu-id="b0f5f-145">Summary</span></span>

<span data-ttu-id="b0f5f-146">발신자 및 수신자 응용 프로그램은 이벤트 허브 환경에 대한 특정 정보로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-146">Sender and receiver applications must be configured with specific information about the event hub environment.</span></span> <span data-ttu-id="b0f5f-147">수신자 응용 프로그램이 메시지를 Blob Storage에 저장하는 경우 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-147">You create a storage account if your receiver application stores messages in Blob Storage.</span></span> <span data-ttu-id="b0f5f-148">응용 프로그램이 GitHub에서 호스트되는 경우 응용 프로그램을 로컬 디렉터리에 복제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-148">If your application is hosted on GitHub, you have to clone it to your local directory.</span></span> <span data-ttu-id="b0f5f-149">**nano**와 같은 텍스트 편집기는 네임스페이스를 응용 프로그램에 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f5f-149">Text editors, such as **nano** is used to  add your namespace to the application.</span></span>