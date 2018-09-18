<span data-ttu-id="c4d55-101">::: zone pivot="csharp" Azure Storage 클라이언트 라이브러리를 .NET Core 콘솔 응용 프로그램에 통합해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-101">::: zone pivot="csharp" Let's integrate the Azure Storage client library into your .NET Core console application.</span></span>

<span data-ttu-id="c4d55-102">.NET용 Azure Storage 클라이언트 라이브러리는 NuGet을 사용하여 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-102">The Azure storage client library for .NET is distributed with NuGet.</span></span> <span data-ttu-id="c4d55-103">**WindowsAzure.Storage** 패키지를 .NET 또는 .NET Core 응용 프로그램에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-103">You will want to add the **WindowsAzure.Storage** package to your .NET or .NET Core applications.</span></span>

## <a name="add-the-azure-storage-nuget-package"></a><span data-ttu-id="c4d55-104">Azure Storage NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="c4d55-104">Add the Azure Storage NuGet package</span></span>

1. <span data-ttu-id="c4d55-105">Cloud Shell을 사용하는 경우 올바른 폴더로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-105">Switch to the correct folder if you are using the Cloud Shell.</span></span>

1. <span data-ttu-id="c4d55-106">**WindowsAzure.Storage** 패키지를 응용 프로그램에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-106">Add the **WindowsAzure.Storage** package to the application.</span></span>

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. <span data-ttu-id="c4d55-107">이렇게 하면 클라이언트 라이브러리 및 필요한 모든 종속성이 다운로드되는 동안 일부 콘솔 활동이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-107">This should result in some console activity while the client library and all the required dependencies are downloaded.</span></span> <span data-ttu-id="c4d55-108">완료되면 앱을 다시 빌드하고 실행하여 모든 준비를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-108">Once it's done, go ahead and build and run the app again to make sure everything is ready to go.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="c4d55-109">이전과 마찬가지로, "Hello, World!"가 출력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-109">As before, it should output "Hello, World!".</span></span>

<span data-ttu-id="c4d55-110">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c4d55-110">::: zone-end</span></span>

<span data-ttu-id="c4d55-111">::: zone-pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="c4d55-111">::: zone-pivot="javascript"</span></span>

<span data-ttu-id="c4d55-112">**Node.js 및 JavaScript용 Microsoft Azure Storage 클라이언트 라이브러리**를 응용 프로그램에 통합해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-112">Let's integrate the **Microsoft Azure Storage Client Library for Node.js and JavaScript** into your application.</span></span>

<span data-ttu-id="c4d55-113">Node.js용 클라이언트 라이브러리는 NPM(노드 패키지 관리자)를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-113">The client library for Node.js is available through the Node Package manager (NPM).</span></span> <span data-ttu-id="c4d55-114">**azure-storage** 패키지를 **packages.json** 파일에 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-114">You will want to add the **azure-storage** package to your **packages.json** file.</span></span>

> [!NOTE]
> <span data-ttu-id="c4d55-115">**Node.js 및 JavaScript용 Microsoft Azure Storage 클라이언트 라이브러리**는 서버 응용 프로그램을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-115">The **Microsoft Azure Storage Client Library for Node.js and JavaScript** is intended for server applications.</span></span> <span data-ttu-id="c4d55-116">클라이언트 쪽 JavaScript를 수행하는 경우 동일한 기능을 제공하지만 브라우저에서 실행되도록 조정된 **JavaScript용 Azure Storage 클라이언트 라이브러리**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-116">If you are doing client-side JavaScript, you will want to use the **Azure Storage Client Library for JavaScript** which provides the same functionality but is tailored to running in a browser.</span></span>

## <a name="add-the-azure-storage-package"></a><span data-ttu-id="c4d55-117">Azure Storage 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="c4d55-117">Add the Azure Storage package</span></span>

1. <span data-ttu-id="c4d55-118">Cloud Shell을 사용하는 경우 올바른 폴더로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-118">Switch to the correct folder if you are using the Cloud Shell.</span></span>

1. <span data-ttu-id="c4d55-119">**azure-storage** 패키지를 응용 프로그램에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-119">Add the **azure-storage** package to the application.</span></span> <span data-ttu-id="c4d55-120">**packages.json**을 유지하도록 `--save` 옵션을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-120">Make sure to supply the `--save` option so it persists to **packages.json**.</span></span>

    ```bash
    npm install azure-storage --save
    ```

1. <span data-ttu-id="c4d55-121">이렇게 하면 클라이언트 라이브러리 및 필요한 모든 종속성이 다운로드되는 동안 일부 콘솔 활동이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-121">This should result in some console activity while the client library and all the required dependencies are downloaded.</span></span> <span data-ttu-id="c4d55-122">완료되면 앱을 다시 빌드하고 실행하여 모든 준비를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-122">Once it's done, go ahead and build and run the app again to make sure everything is ready to go.</span></span>

    ```bash
    node index.js
    ```

1. <span data-ttu-id="c4d55-123">이전과 마찬가지로, "Hello, World!"가 출력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-123">As before, it should output "Hello, World!".</span></span>

<span data-ttu-id="c4d55-124">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c4d55-124">::: zone-end</span></span>

<span data-ttu-id="c4d55-125">필요한 라이브러리를 얻었으니, Azure 저장소를 사용하기 위해 코드에서 수행해야 하는 몇 가지 일반적인 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4d55-125">Now that we have the necessary libraries in place, let's look at the common tasks you'll do in your code to work with Azure storage.</span></span>
