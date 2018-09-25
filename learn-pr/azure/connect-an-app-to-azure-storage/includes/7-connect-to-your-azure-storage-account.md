<span data-ttu-id="82e86-101">필요한 클라이언트 라이브러리를 응용 프로그램에 추가했고 Azure 저장소 계정에 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-101">You have added the required client libraries to your application and are ready to connect to your Azure storage account.</span></span>

<span data-ttu-id="82e86-102">저장소 계정의 데이터를 사용하려면 앱에 두 개의 데이터 조각이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-102">To work with data in a storage account, your app will need two pieces of data:</span></span>

1. <span data-ttu-id="82e86-103">액세스 키</span><span class="sxs-lookup"><span data-stu-id="82e86-103">An access key</span></span>
1. <span data-ttu-id="82e86-104">REST API 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="82e86-104">The REST API endpoint</span></span>

## <a name="security-access-keys"></a><span data-ttu-id="82e86-105">보안 액세스 키</span><span class="sxs-lookup"><span data-stu-id="82e86-105">Security access keys</span></span>

<span data-ttu-id="82e86-106">각 저장소 계정에는 저장소 계정을 보호하는 데 사용되는 두 개의 고유한 _액세스 키_가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-106">Each storage account has two unique _access keys_ that are used to secure the storage account.</span></span> <span data-ttu-id="82e86-107">앱이 여러 저장소 계정에 연결해야 하는 경우 앱은 저장소 계정마다 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-107">If your app needs to connect to multiple storage accounts, then your app will require an access key for each storage account.</span></span>

![클라우드에서 두 개의 저장소 계정에 연결된 응용 프로그램을 보여주는 일러스트레이션.](..\media\6-multiple-accounts.png)

## <a name="rest-api-endpoint"></a><span data-ttu-id="82e86-110">REST API 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="82e86-110">REST API endpoint</span></span>

<span data-ttu-id="82e86-111">저장소 계정에 인증하기 위한 액세스 키 외에도, REST 요청을 발급하기 위한 저장소 서비스 엔드포인트를 앱에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-111">In addition to access keys for authentication to storage accounts, your app will need to know the storage service endpoints to issue the REST requests.</span></span> 

<span data-ttu-id="82e86-112">REST 엔드포인트는 저장소 계정 _이름_, 데이터 형식, 알려진 도메인의 조합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-112">The REST endpoint is a combination of your storage account _name_, the data type, and a known domain.</span></span> <span data-ttu-id="82e86-113">예:</span><span class="sxs-lookup"><span data-stu-id="82e86-113">For example:</span></span>

| <span data-ttu-id="82e86-114">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="82e86-114">Data type</span></span> | <span data-ttu-id="82e86-115">예제 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="82e86-115">Example endpoint</span></span> |
|-----------|------------------|
| <span data-ttu-id="82e86-116">Blob</span><span class="sxs-lookup"><span data-stu-id="82e86-116">Blobs</span></span>     | `https://[name].blob.core.windows.net/` |
| <span data-ttu-id="82e86-117">큐</span><span class="sxs-lookup"><span data-stu-id="82e86-117">Queues</span></span>    | `https://[name].queue.core.windows.net/` |
| <span data-ttu-id="82e86-118">테이블</span><span class="sxs-lookup"><span data-stu-id="82e86-118">Table</span></span>     | `https://[name].table.core.windows.net/` |
| <span data-ttu-id="82e86-119">파일</span><span class="sxs-lookup"><span data-stu-id="82e86-119">Files</span></span>     | `https://[name].file.core.windows.net/` |

<span data-ttu-id="82e86-120">Azure에 연결된 사용자 지정 도메인이 있는 경우 엔드포인트에 대한 사용자 지정 도메인 URL을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-120">If you have a custom domain tied to Azure, then you can also create a custom domain URL for the endpoint.</span></span>

## <a name="connection-strings"></a><span data-ttu-id="82e86-121">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="82e86-121">Connection strings</span></span>

<span data-ttu-id="82e86-122">응용 프로그램 내에서 액세스 키 및 엔드포인트 URL을 처리하는 가장 간단한 방법은 **저장소 계정 연결 문자열**을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-122">The simplest way to handle access keys and endpoint URLs within applications is to use **storage account connection strings**.</span></span> <span data-ttu-id="82e86-123">연결 문자열은 단일 텍스트 문자열에 필요한 모든 연결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-123">A connection string provides all needed connectivity information in a single text string.</span></span>

<span data-ttu-id="82e86-124">Azure Storage 연결 문자열은 아래 예제와 비슷하지만 특정 저장소 계정의 액세스 키 및 계정 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-124">Azure Storage connection strings look similar to the example below but with the access key and account name of your specific storage account:</span></span>

```
DefaultEndpointsProtocol=https;AccountName={your-storage};
   AccountKey={your-access-key};
   EndpointSuffix=core.windows.net
```

## <a name="security"></a><span data-ttu-id="82e86-125">보안</span><span class="sxs-lookup"><span data-stu-id="82e86-125">Security</span></span>

<span data-ttu-id="82e86-126">액세스 키는 저장소 계정에 대한 액세스를 제공하는 데 중요하므로 사용자 저장소 계정에 액세스하지 않게 하려는 시스템 또는 개인에게 제공해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-126">Access keys are critical to providing access to your storage account and as a result, should not be given to any system or person that you do not wish to have access to your storage account.</span></span> <span data-ttu-id="82e86-127">액세스 키는 사용자의 컴퓨터에 액세스하기 위한 사용자 이름 및 암호와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-127">Access keys are the equivalent of a username and password to access your computer.</span></span>

<span data-ttu-id="82e86-128">일반적으로 저장소 계정 연결 정보는 환경 변수, 데이터베이스 또는 구성 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-128">Typically, storage account connectivity information is stored within an environment variable, database, or configuration file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82e86-129">소스 제어에 해당 파일을 포함하고 공용 리포지토리에 저장하는 경우 이 정보를 구성 파일에 저장하는 것이 위험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-129">It is important to note that storing this information in a configuration file can be dangerous if you include that file in source control and store it in a public repository.</span></span> <span data-ttu-id="82e86-130">이는 일반적인 실수이며 사용자가 공용 리포지토리에서 소스 코드를 찾아보고 저장소 계정 연결 정보를 볼 수 있다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-130">This is a common mistake and means that anyone can browse your source code in the public repository and see your storage account connection information.</span></span>

<span data-ttu-id="82e86-131">각 저장소 계정에는 두 개의 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-131">Each storage account has two access keys.</span></span> <span data-ttu-id="82e86-132">두 개인 이유는 저장소 계정의 보안을 유지하기 위한 보안 모범 사례의 일환으로 주기적으로 키를 순환(다시 생성)하도록 허용하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-132">The reason for this is to allow keys to be rotated (regenerated) periodically as part of security best practice in keeping your storage account secure.</span></span> <span data-ttu-id="82e86-133">이 프로세스는 Azure Portal 또는 Azure CLI/PowerShell 명령줄 도구에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-133">This process can be done from the Azure portal or the Azure CLI / PowerShell command line tool.</span></span>

<span data-ttu-id="82e86-134">키를 순환하면 원래 키 값이 즉시 무효화되며 부적절하게 키를 얻은 모든 사용자의 액세스 권한이 철회됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-134">Rotating a key will invalidate the original key value immediately and will revoke access to anyone who obtained the key inappropriately.</span></span> <span data-ttu-id="82e86-135">두 개의 키가 지원되므로 이러한 키를 사용하는 응용 프로그램에 가동 중지 시간을 일으키지 않고 키를 회전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-135">With support for two keys, you can rotate keys without causing downtime in your applications that use them.</span></span> <span data-ttu-id="82e86-136">앱이 대체 액세스 키를 사용하도록 전환할 수 있으며 다른 키 하나는 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-136">Your app can switch to using the alternate access key while the other key is regenerated.</span></span> <span data-ttu-id="82e86-137">이 저장소 계정을 사용하는 앱이 여러 개인 경우 이 기술을 지원하려면 해당 앱 모두 동일한 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-137">If you have multiple apps using this storage account, they should all use the same key to support this technique.</span></span> <span data-ttu-id="82e86-138">기본적인 개념은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-138">Here's the basic idea:</span></span>

1. <span data-ttu-id="82e86-139">저장소 계정의 보조 액세스 키를 참조하도록 응용 프로그램 코드의 연결 문자열을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-139">Update the connection strings in your application code to reference the secondary access key of the storage account.</span></span>
2. <span data-ttu-id="82e86-140">Azure Portal 또는 명령줄 도구를 사용하여 저장소 계정의 기본 액세스 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-140">Regenerate the primary access key for your storage account using the Azure portal or command line tool.</span></span>
3. <span data-ttu-id="82e86-141">새 기본 액세스 키를 참조하도록 코드의 연결 문자열을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-141">Update the connection strings in your code to reference the new primary access key.</span></span>
4. <span data-ttu-id="82e86-142">같은 방식으로 보조 액세스 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-142">Regenerate the secondary access key in the same manner.</span></span>

> [!TIP]
> <span data-ttu-id="82e86-143">액세스 키의 보안을 유지할 수 있도록 암호를 변경하듯이 액세스 키를 주기적으로 회전할 것을 적극적으로 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-143">It's highly recommended that you periodically rotate your access keys to ensure they remain private, just like changing your passwords.</span></span> <span data-ttu-id="82e86-144">키를 서버 응용 프로그램에 사용하는 경우 **Azure Key Vault**를 사용하여 자동으로 액세스 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-144">If you are using the key in a server application, you can use an **Azure Key Vault** to store the access key for you.</span></span> <span data-ttu-id="82e86-145">Key Vault는 저장소 계정과 직접 동기화하고 키를 주기적으로 자동 회전하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-145">Key Vaults include support to synchronize directly to the Storage Account and automatically rotate the keys periodically.</span></span> <span data-ttu-id="82e86-146">Key Vault를 사용하면 앱이 액세스 키를 직접 작업할 필요가 없는 추가 보안 계층이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-146">Using a Key Vault provides an additional layer of security, so your app never has to work directly with an access key.</span></span>

### <a name="shared-access-signatures-sas"></a><span data-ttu-id="82e86-147">SAS(공유 액세스 서명)</span><span class="sxs-lookup"><span data-stu-id="82e86-147">Shared access signatures (SAS)</span></span>

<span data-ttu-id="82e86-148">액세스키는 저장소 계정에 대한 액세스를 인증하기 위한 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-148">Access keys are the easiest approach to authenticating access to a storage account.</span></span> <span data-ttu-id="82e86-149">그러나 컴퓨터의 루트 암호와 마찬가지로, 저장소 계정의 모든 항목에 대한 전체 접근 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-149">However they provide full access to anything in the storage account, similar to a root password on a computer.</span></span>

<span data-ttu-id="82e86-150">저장소 계정은 제한된 액세스 권한을 부여해야 하는 시나리오에 대한 만료 및 제한된 권한을 지원하는 _공유 액세스 서명_이라는 별도의 인증 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-150">Storage accounts offer a separate authentication mechanism called _shared access signatures_ that support expiration and limited permissions for scenarios where you need to grant limited access.</span></span> <span data-ttu-id="82e86-151">다른 사용자가 데이터를 읽고 저장소 계정에 쓸 수 있게 허용하려면 이 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-151">You should use this approach when you are allowing other users to read and write data to your storage account.</span></span> <span data-ttu-id="82e86-152">이 모듈의 마지막 부분에 이 고급 토픽과 관련된 설명서 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82e86-152">There are links to our documentation on this advanced topic at the end of the module.</span></span>
