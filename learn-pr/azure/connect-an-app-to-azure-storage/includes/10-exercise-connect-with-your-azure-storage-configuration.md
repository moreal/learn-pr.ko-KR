<span data-ttu-id="046fc-101">::: zone pivot="csharp" 구성에서 연결 문자열을 검색하고 해당 연결 문자열을 사용하여 Azure 저장소 계정에 연결하는 코드를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-101">::: zone pivot="csharp" Let's add code to retrieve the connection string from configuration and use it to connect to the Azure storage account.</span></span>

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="046fc-102">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="046fc-102">Retrieve the connection string</span></span>

1. <span data-ttu-id="046fc-103">**Program.cs**를 선택하여 코드 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-103">Select **Program.cs** to open it in the code editor.</span></span>

1. <span data-ttu-id="046fc-104">`Microsoft.WindowsAzure.Storage` 네임스페이스를 참조하도록 파일 맨 위에 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-104">Add a `using` statement at the top of the file to reference the `Microsoft.WindowsAzure.Storage` namespace:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. <span data-ttu-id="046fc-105">`Main` 메서드의 맨 끝에 다음 줄을 추가하여 구성 파일에서 Azure 저장소 계정 연결 문자열을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-105">At the end of the `Main` method, add the following line to retrieve the Azure storage account connection string from the configuration file.</span></span> <span data-ttu-id="046fc-106">전달된 _키_가 **appsettings.json** 파일에 사용된 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-106">The passed _key_ must match the name used in your **appsettings.json** file.</span></span>

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a><span data-ttu-id="046fc-107">BLOB 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="046fc-107">Create a blob client</span></span>

1. <span data-ttu-id="046fc-108">정적 `CloudStorageAccount.TryParse` 메서드를 사용하여 `CloudStorageAccount` 개체를 만듭니다. 이 메서드는 연결 문자열과 `out` 매개 변수를 사용하여 생성된 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-108">Use the static `CloudStorageAccount.TryParse` method to create a `CloudStorageAccount` object - it takes the connection string and an `out` parameter to return the created object.</span></span> <span data-ttu-id="046fc-109">이 메서드는 문자열을 성공적으로 구문 분석했는지 여부를 나타내는 `bool` 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-109">It returns a `bool` value indicating whether it successfully parsed the string.</span></span>
    - <span data-ttu-id="046fc-110">실패하면 콘솔에 메시지를 출력하고 메서드에서 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-110">If it fails, output a message to the console and return from the method.</span></span>

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString, 
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. <span data-ttu-id="046fc-111">반환된 `CloudStorageAccount` 개체를 사용하여 BLOB 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-111">Use the returned `CloudStorageAccount` object to create a blob client.</span></span>

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="046fc-112">다음으로, BLOB 클라이언트를 사용하여 "photoblobs" 컨테이너의 참조를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-112">Next, use the blob client to retrieve a reference to a container named "photoblobs".</span></span> <span data-ttu-id="046fc-113">계정 이름과 비슷하게, Blob 컨테이너 이름은 소문자여야 하고 문자와 숫자로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-113">Much like the account names, the Blob container names must be lowercase and composed of letters and numbers.</span></span>

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. <span data-ttu-id="046fc-114">`CreateIfNotExistsAsync` 메서드를 사용하여 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-114">Use the `CreateIfNotExistsAsync` method to create the container.</span></span> <span data-ttu-id="046fc-115">그러면 컨테이너 생성 여부를 나타내는 `bool`이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-115">This returns a `bool` indicating whether the container was created.</span></span> <span data-ttu-id="046fc-116">이 값을 `created` 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-116">Store this in a variable named `created`.</span></span>
    - <span data-ttu-id="046fc-117">이 메서드는 실제 네트워크 호출을 수행하는 **비동기** 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-117">Notice that this is an **async** method - that means it will perform an actual network call.</span></span>
    - <span data-ttu-id="046fc-118">`await` 키워드를 사용하여 `bool` 결과를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-118">You will need to use the `await` keywords to get the `bool` result.</span></span>

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. <span data-ttu-id="046fc-119">여기서는 `await` 키워드를 사용할 것이므로 `Main` 메서드가 `async`이도록 서명을 변경하고 `Task`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-119">Because we are using the `await` keyword, go ahead and change the signature for the `Main` method to be `async` and return a `Task`.</span></span>

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

1. <span data-ttu-id="046fc-120">마지막으로, Blob 컨테이너 생성 여부를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-120">Finally, output whether we created the Blob container.</span></span>

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. <span data-ttu-id="046fc-121">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-121">Save the file.</span></span>

<span data-ttu-id="046fc-122">작업을 확인하고 싶은 경우 최종 파일은 이렇게 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-122">The final file should look like this if you'd like to check your work.</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using System.Threading.Tasks;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;

namespace PhotoSharingApp
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
            var connectionString = configuration["StorageAccountConnectionString"];

            if (!CloudStorageAccount.TryParse(connectionString, out CloudStorageAccount storageAccount))
            {
                Console.WriteLine("Unable to parse connection string");
                return;
            }

            var blobClient = storageAccount.CreateCloudBlobClient();
            var blobContainer = blobClient.GetContainerReference("photoblobs");
            bool created = await blobContainer.CreateIfNotExistsAsync();

            Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
        }
    }
}
```

## <a name="use-c-71-to-build-our-app"></a><span data-ttu-id="046fc-123">C# 7.1을 사용하여 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="046fc-123">Use C# 7.1 to build our app</span></span>

<span data-ttu-id="046fc-124">`Main` 메서드의 `async` 및 `await`에 대한 지원이 C# 7.1에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-124">Support for `async` and `await` on `Main` methods was added to C# 7.1.</span></span> <span data-ttu-id="046fc-125">이 버전은 여러분이 사용 중인 컴파일러의 기본 버전이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-125">This might not be the default version of the compiler you are using.</span></span> <span data-ttu-id="046fc-126">이 컴파일러 버전을 사용하도록 구성 파일에서 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-126">Let's make sure we use that version of the compiler by setting it in our configuration file.</span></span>

1. <span data-ttu-id="046fc-127">`PhotoSharingApp.csproj` 파일을 열고 `TargetFramework`를 지정하는 `PropertyGroup`에 `<LangVersion>7.1</LangVersion>`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-127">Open the `PhotoSharingApp.csproj` and add `<LangVersion>7.1</LangVersion>` to the `PropertyGroup` that specifies the `TargetFramework`.</span></span> <span data-ttu-id="046fc-128">완료되면 파일이 다음과 비슷한 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-128">It should look like this when you're finished:</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <LangVersion>7.1</LangVersion> 
        <TargetFramework>netcoreapp2.0</TargetFramework>
      </PropertyGroup>
      ...
    </Project>
    ```

1. <span data-ttu-id="046fc-129">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-129">Save the file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="046fc-130">앱 실행</span><span class="sxs-lookup"><span data-stu-id="046fc-130">Run the app</span></span>

1. <span data-ttu-id="046fc-131">응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-131">Build and run the application.</span></span> <span data-ttu-id="046fc-132">**참고:** 올바른 작업 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-132">**Note:** make sure you're in the correct working directory.</span></span>

    ```bash
    dotnet run
    ```

<span data-ttu-id="046fc-133">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="046fc-133">::: zone-end</span></span>

<span data-ttu-id="046fc-134">::: zone-pivot="javascript" 저장된 연결 문자열을 사용하여 Azure 저장소 계정에 연결하는 코드를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-134">::: zone-pivot="javascript" Let's add code to connect to the Azure storage account using our stored connection string.</span></span> <span data-ttu-id="046fc-135">Azure 클라이언트 라이브러리는 자동으로 **AZURE_STORAGE_CONNECTION_STRING** 환경 변수를 사용하여 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-135">The Azure client library will automatically use the **AZURE_STORAGE_CONNECTION_STRING** environment variable to get the connection string.</span></span>

## <a name="create-a-blob-client"></a><span data-ttu-id="046fc-136">BLOB 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="046fc-136">Create a blob client</span></span>

1. <span data-ttu-id="046fc-137">코드 편집기에서 **index.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-137">Open **index.js** in the code editor.</span></span>

1. <span data-ttu-id="046fc-138">**azure-storage** 모듈을 포함하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-138">Start by including the **azure-storage** module.</span></span> <span data-ttu-id="046fc-139">**storage**라는 변수에 모듈을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-139">Store the module in a variable named **storage**.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const storage = require('azure-storage');
    ```

1. <span data-ttu-id="046fc-140">다음으로, 바로 뒤에 **저장소** 개체를 사용하여 `BlobService` 개체를 만들고 글로벌 **blobService**에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-140">Next, right after that, use the **storage** object to create the `BlobService` object and store it in a global named **blobService**.</span></span> <span data-ttu-id="046fc-141">저장소 계정에 대한 액세스를 나타내는 경량 개체라는 사실을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="046fc-141">Remember, these are light-weight objects representing access to the storage account.</span></span>

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. <span data-ttu-id="046fc-142">만들려는 컨테이너를 나타내는 상수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-142">Add a constant to represent the container we want to create.</span></span> <span data-ttu-id="046fc-143">컨테이너 이름을 "photoblobs"로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-143">We'll name the container "photoblobs".</span></span>

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a><span data-ttu-id="046fc-144">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="046fc-144">Create a container</span></span>

<span data-ttu-id="046fc-145">`BlobService` 개체를 사용하여 Azure 저장소에서 BLOB API를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-145">We can use the `BlobService` object to work with blob APIs in Azure storage.</span></span> <span data-ttu-id="046fc-146">앞서 언급했듯이, 네트워크 호출을 만드는 모든 API는 비동기적으로 앱 응답성을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-146">As mentioned before, all the APIs that make network calls are asynchronous to keep the app responsive.</span></span> <span data-ttu-id="046fc-147">`createContainerIfNotExists` 메서드도 이러한 메서드 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-147">The `createContainerIfNotExists` method is one such method.</span></span> <span data-ttu-id="046fc-148">우리는 _promises_를 사용하여 응답을 포함하는 콜백을 처리하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-148">We'll use _promises_ to handle the callback which contains the response.</span></span>

1. <span data-ttu-id="046fc-149">`util.promisify`를 사용하여 `createContainerIfNotExists`의 콜백 버전을 가져와서 promise-returning 메서드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-149">Use `util.promisify` to take the callback version of `createContainerIfNotExists` and turn it into a promise-returning method.</span></span>
    - <span data-ttu-id="046fc-150">콜백 메서드는 개체에 있으므로 끝부분에 해당 컨텍스트에 연결하는 `bind` 호출을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-150">Since the callback method is on an object, make sure to add a `bind` call at the end to connect it to that context.</span></span>
    - <span data-ttu-id="046fc-151">아래와 같이 `createContainerAsync` 파일의 맨 위에 있는 상수에 반환 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-151">Assign the return value to a constant at the top of the file named `createContainerAsync` as shown below.</span></span>

```javascript
const storage = require('azure-storage');
const blobService = storage.createBlobService();

const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';
```

1. <span data-ttu-id="046fc-152">"Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="046fc-152">Remove the "Hello, World!"</span></span> <span data-ttu-id="046fc-153">출력을 `main()`에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-153">output from `main()`.</span></span>

1. <span data-ttu-id="046fc-154">새 `createContainerAsync` promise를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-154">Call your new `createContainerAsync` promise.</span></span>
    - <span data-ttu-id="046fc-155">**containerName** 상수에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-155">Pass it the **containerName** constant.</span></span>
    - <span data-ttu-id="046fc-156">호출에 `await` 키워드를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-156">Apply the `await` keyword to the call.</span></span>
    - <span data-ttu-id="046fc-157">호출을 `try` / `catch` 구문에 래핑하고 아무 오류를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-157">Wrap the call in a `try` / `catch` construct and output any error.</span></span>

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```
    
1. <span data-ttu-id="046fc-158">`createContainerAsync` promise는 컨테이너 결과인 기본 `createContainerIfNotExists`의 첫 번째 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-158">The `createContainerAsync` promise returns the first value from the underlying `createContainerIfNotExists` which is the container result.</span></span> <span data-ttu-id="046fc-159">여기에는 컨테이너 생성 여부에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-159">This includes information on whether the container was created or not.</span></span> <span data-ttu-id="046fc-160">결과를 변수에 캡처하고 `result.created` 속성에 따라 컨테이너 생성 여부를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-160">Capture the result in a variable and output whether the container was created based on the `result.created` property.</span></span>

    ```javascript
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. <span data-ttu-id="046fc-161">마지막으로, `async` 키워드로 `main` 함수를 데코레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-161">Finally, decorate the `main` function with the `async` keyword.</span></span>
        
1. <span data-ttu-id="046fc-162">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-162">Save the file.</span></span>

<span data-ttu-id="046fc-163">작업을 확인하고 싶은 경우 최종 파일은 이렇게 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-163">The final file should look like this if you'd like to check your work.</span></span>

```javascript
#!/usr/bin/env node

require('dotenv').load();

const util = require('util');

const storage = require('azure-storage');
const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';

async function run() {
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

run();
```

## <a name="run-the-app"></a><span data-ttu-id="046fc-164">앱 실행</span><span class="sxs-lookup"><span data-stu-id="046fc-164">Run the app</span></span>

1. <span data-ttu-id="046fc-165">응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-165">Build and run the application.</span></span> <span data-ttu-id="046fc-166">**참고:** 올바른 작업 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-166">**Note:** make sure you're in the correct working directory.</span></span>

    ```bash
    node index.js
    ```

<span data-ttu-id="046fc-167">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="046fc-167">::: zone-end</span></span>

<span data-ttu-id="046fc-168">BLOB 컨테이너가 생성되었다고 응용 프로그램이 보고할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-168">It should report that the blob container was created.</span></span> <span data-ttu-id="046fc-169">응용 프로그램을 두 번째로 실행하면 컨테이너가 이미 있다고 보고할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-169">If you run it a second time, it should tell you it already exists.</span></span>

<span data-ttu-id="046fc-170">컨테이너를 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="046fc-170">To verify the container:</span></span>

1. <span data-ttu-id="046fc-171">[Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-171">Sign in to the [Azure Portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="046fc-172">저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-172">Navigate to your storage account.</span></span> <span data-ttu-id="046fc-173">**모든 리소스** 섹션을 사용하여 저장소 계정을 찾거나, 포털 창의 맨 위에 있는 _검색 상자_에서 이름으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-173">You can use the **All Resources** section to find the storage account, or search by name from the _search box_ at the top of the portal window.</span></span> 

1. <span data-ttu-id="046fc-174">**Blob 서비스** 섹션에서 저장소 계정의 **Blob** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-174">Select the **Blobs** entry of the storage account in the **Blob services** section.</span></span>

1. <span data-ttu-id="046fc-175">Blob 패널에 **photoblobs** 컨테이너가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-175">You should see your **photoblobs** container in the Blobs panel.</span></span> <span data-ttu-id="046fc-176">항목의 오른쪽에 있는 "..." 메뉴를 통해 컨테이너를 삭제하고 앱에서 컨테이너를 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-176">You can delete the container through the "..." menu on the right hand side of the entry to try re-creating it with your app.</span></span>

> [!NOTE]
> <span data-ttu-id="046fc-177">포털에서 컨테이너가 매우 빠르게 사라지지만, 실제로 삭제될 때까지 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-177">The container will disappear from the portal very quickly, but it takes a few minutes to actually delete.</span></span> <span data-ttu-id="046fc-178">컨테이너가 삭제되는 동안 컨테이너를 다시 만들려고 시도하면 Azure에서 오류 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-178">You will get an error response from Azure while it is being deleted if you attempt to recreate it.</span></span>

## <a name="delete-the-app"></a><span data-ttu-id="046fc-179">앱 삭제</span><span class="sxs-lookup"><span data-stu-id="046fc-179">Delete the app</span></span>
<span data-ttu-id="046fc-180">응용 프로그램 소스 코드를 Cloud Shell 환경에 유지하지 않기로 결정하는 경우 다음 명령을 사용하여 폴더와 모든 콘텐츠를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046fc-180">If you decide you don't want to keep the application source code in your Cloud Shell environment, you can use the following command to remove the folder and all the contents.</span></span>

```bash
rm -r PhotoSharingApp/
```
