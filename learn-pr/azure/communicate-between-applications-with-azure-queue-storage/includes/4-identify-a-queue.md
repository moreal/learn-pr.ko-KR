<span data-ttu-id="652c9-101">이제 저장소 계정이 있으므로 보류되는 큐 작업을 수행하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-101">Now that we have a storage account, let's look at how we work with the queue that it will hold.</span></span>

<span data-ttu-id="652c9-102">큐에 액세스하려면 다음 세 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-102">To access a queue, you need three pieces of information:</span></span>

 1. <span data-ttu-id="652c9-103">Storage 계정 이름</span><span class="sxs-lookup"><span data-stu-id="652c9-103">Storage account name</span></span>
 2. <span data-ttu-id="652c9-104">큐 이름</span><span class="sxs-lookup"><span data-stu-id="652c9-104">Queue name</span></span>
 3. <span data-ttu-id="652c9-105">권한 부여 토큰</span><span class="sxs-lookup"><span data-stu-id="652c9-105">Authorization token</span></span>

<span data-ttu-id="652c9-106">이 정보는 큐와 통신하는 두 응용 프로그램(메시지를 추가하는 웹 프런트 엔드 및 메시지를 처리하는 중간 계층)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-106">This information is used by both applications that talk to the queue (the web front end that adds messages and the mid-tier that processes them).</span></span>

## <a name="queue-identity"></a><span data-ttu-id="652c9-107">큐 ID</span><span class="sxs-lookup"><span data-stu-id="652c9-107">Queue identity</span></span>

<span data-ttu-id="652c9-108">모든 큐에는 사용자가 만들 때 할당하는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-108">Every queue has a name that you assign during creation.</span></span> <span data-ttu-id="652c9-109">이 이름은 저장소 계정 내에서 고유해야 하지만 저장소 계정 이름과 달리 전체적으로 고유해야 할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-109">The name must be unique within your storage account but doesn't need to be globally unique (unlike the storage account name).</span></span>

<span data-ttu-id="652c9-110">저장소 계정 이름과 큐 이름의 조합으로 큐를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-110">The combination of your storage account name and your queue name uniquely identifies a queue.</span></span>

## <a name="access-authorization"></a><span data-ttu-id="652c9-111">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="652c9-111">Access authorization</span></span>

<span data-ttu-id="652c9-112">큐에 대한 모든 요청은 인증되어야 하며, 선택할 수 있는 몇 개의 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-112">Every request to a queue must be authorized and there are several options to choose from.</span></span>

| <span data-ttu-id="652c9-113">권한 부여 유형</span><span class="sxs-lookup"><span data-stu-id="652c9-113">Authorization Type</span></span> | <span data-ttu-id="652c9-114">설명</span><span class="sxs-lookup"><span data-stu-id="652c9-114">Description</span></span> |
|--------------------|-------------|
| <span data-ttu-id="652c9-115">**Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="652c9-115">**Azure Active Directory**</span></span> | <span data-ttu-id="652c9-116">역할 기반 인증을 사용하고 AAD 자격 증명을 기준으로 특정 클라이언트를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-116">you can use role-based authentication and identify specific clients based on AAD credentials.</span></span> |
| <span data-ttu-id="652c9-117">**공유 키**</span><span class="sxs-lookup"><span data-stu-id="652c9-117">**Shared Key**</span></span> | <span data-ttu-id="652c9-118">**계정 키**라고도 하는 이 키는 저장소 계정에 연결된 암호화된 키 서명입니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-118">Sometimes referred to as an **account key**, this is an encrypted key signature associated with the storage account.</span></span> <span data-ttu-id="652c9-119">모든 저장소 계정에는 액세스를 인증하기 위해 각 요청과 함께 전달될 수 있는 이러한 두 가지 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-119">Every storage account has two of these keys that can be passed with each request to authenticate access.</span></span> <span data-ttu-id="652c9-120">이 접근 방식을 사용하는 것은 루트 암호를 사용하는 것과 같습니다. 이 방법은 저장소 계정에 대한 _모든 권한_을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-120">Using this approach is like using a root password - it provides _full access_ to the storage account.</span></span> |
| <span data-ttu-id="652c9-121">**공유 액세스 서명**</span><span class="sxs-lookup"><span data-stu-id="652c9-121">**Shared access signature**</span></span> | <span data-ttu-id="652c9-122">SAS(공유 액세스 서명)는 저장소 계정의 개체에 대한 제한된 액세스 권한을 클라이언트에 부여하는 생성되는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-122">A shared access signature (SAS) is a generated URI that grants limited access to objects in your storage account to clients.</span></span> <span data-ttu-id="652c9-123">특정 리소스, 권한 및 범위에 대한 액세스를 특정 데이터 범위로 제한하여 일정 기간 후에 액세스 권한을 자동으로 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-123">You can restrict access to specific resources, permissions, and scope to a data range to automatically turn off access after a period of time.</span></span>  |

> [!NOTE]
> <span data-ttu-id="652c9-124">여기서는 계정 키 권한 부여가 큐 작업을 시작하는 가장 단순한 방법이므로 이를 사용하겠지만, 프로덕션 앱에서는 SAS(공유 액세스 서명) 또는 AAD(Azure Active Directory)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-124">We will use the account key authorization because it is the simplest way to get started working with queues, however it's recommended that you either use shared access signature (SAS) or Azure Active Directory (AAD) in production apps.</span></span>

### <a name="retrieving-the-account-key"></a><span data-ttu-id="652c9-125">계정 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="652c9-125">Retrieving the account key</span></span>
 
<span data-ttu-id="652c9-126">계정 키는 Azure Portal에서 저장소 계정의 **설정 > 액세스 키** 섹션에서 사용하거나, 다음 명령줄을 통해 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-126">Your account key is available in the **Settings > Access keys** section of your storage account in the Azure portal, or you can retrieve it through the command line:</span></span>

```azurecli
az storage account keys list ...
```

```powershell
Get-AzureRmStorageAccountKey ...
```

## <a name="accessing-queues"></a><span data-ttu-id="652c9-127">큐에 액세스</span><span class="sxs-lookup"><span data-stu-id="652c9-127">Accessing queues</span></span>

<span data-ttu-id="652c9-128">REST API를 사용하여 큐에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-128">You access a queue using a REST API.</span></span> <span data-ttu-id="652c9-129">이를 수행하려면 저장소 계정에 지정한 이름을 도메인 `queue.core.windows.net` 및 작업할 큐 경로와 결합한 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-129">To do this, you'll use a URL that combines the name you gave the storage account with the domain `queue.core.windows.net` and the path to the queue you want to work with.</span></span> <span data-ttu-id="652c9-130">예: `http://<storage account>.queue.core.windows.net/<queue name>`.</span><span class="sxs-lookup"><span data-stu-id="652c9-130">For example: `http://<storage account>.queue.core.windows.net/<queue name>`.</span></span> <span data-ttu-id="652c9-131">`Authorization` 헤더는 모든 요청에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-131">An `Authorization` header must be included with every request.</span></span> <span data-ttu-id="652c9-132">이 값은 세 가지 권한 부여 스타일 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-132">The value can be any of the three authorization styles.</span></span>

### <a name="using-the-azure-storage-client-library-for-net"></a><span data-ttu-id="652c9-133">.NET용 Azure Storage 클라이언트 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="652c9-133">Using the Azure Storage Client Library for .NET</span></span>

<span data-ttu-id="652c9-134">.NET용 Azure Storage 클라이언트 라이브러리는 Microsoft에서 제공하는 라이브러리로, REST 요청을 작성하고 REST 응답을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-134">The Azure Storage Client Library for .NET is a library provided by Microsoft that formulates REST requests and parses REST responses for you.</span></span> <span data-ttu-id="652c9-135">이 라이브러리를 사용하면 작성해야 하는 코드 양이 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-135">This greatly reduces the amount of code you need to write.</span></span> <span data-ttu-id="652c9-136">클라이언트 라이브러리를 사용하여 액세스하려면 동일한 정보(저장소 계정 이름, 큐 이름 및 계정 키)가 필요하지만 이러한 정보가 다르게 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-136">Access using the client library still requires the same pieces of information (storage account name, queue name, and account key); however, they are organized differently.</span></span>

<span data-ttu-id="652c9-137">클라이언트 라이브러리는 **연결 문자열**을 사용하여 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-137">The client library uses a **connection string** to establish your connection.</span></span> <span data-ttu-id="652c9-138">연결 문자열은 Azure Portal에 있는 저장소 계정의 **설정** 섹션 또는 Azure CLI 및 PowerShell을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-138">Your connection string is available in the **Settings** section of your Storage Account in the Azure portal, or through the Azure CLI and PowerShell.</span></span>

<span data-ttu-id="652c9-139">연결 문자열은 저장소 계정 이름과 계정 키를 결합하는 문자열로, 저장소 계정에 액세스하기 위해 응용 프로그램이 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-139">A connection string is a string that combines a storage account name and account key and must be known to the application to access the storage account.</span></span> <span data-ttu-id="652c9-140">형식은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-140">The format looks like this:</span></span>

```csharp
string connectionString = "DefaultEndpointsProtocol=https;AccountName=<your storage account name>;AccountKey=<your key>;EndpointSuffix=core.windows.net"
```

> [!WARNING]
> <span data-ttu-id="652c9-141">이 연결 문자열에 대한 액세스 권한이 있는 사용자가 큐를 조작할 수 있으므로 이 문자열 값은 안전한 위치에 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-141">This string value should be stored in a secure location since anyone who has access to this connection string would be able to manipulate the queue.</span></span>

<span data-ttu-id="652c9-142">연결 문자열에는 큐 이름이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-142">Notice that the connection string doesn't include the queue name.</span></span> <span data-ttu-id="652c9-143">큐에 대한 연결을 설정할 때 큐 이름이 코드에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c9-143">The queue name is supplied in your code when you establish a connection to the queue.</span></span>

<span data-ttu-id="652c9-144">Azure에서 연결 문자열을 가져온 후 새 응용 프로그램에서 사용하도록 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="652c9-144">Let's get our connection string from Azure and set up a new application to use it.</span></span>