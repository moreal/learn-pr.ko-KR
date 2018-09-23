<span data-ttu-id="88673-101">이 모듈에서는 HTML 기반 사용자 인터페이스를 표시하는 간단한 웹 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-101">In this module, you will deploy a simple web application that presents an HTML-based user interface.</span></span> <span data-ttu-id="88673-102">서버리스 백 엔드를 사용하면 응용 프로그램에서 이미지를 업로드하고 자동으로 설명이 포함된 캡션을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88673-102">A serverless back end enables the application to upload images and automatically generate descriptive captions.</span></span>

![웹앱 실행](../media/0-app-screenshot-finished.png)

<span data-ttu-id="88673-104">다음 일러스트레이션은 응용 프로그램에서 사용하는 Azure 서비스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="88673-104">The following illustration shows the Azure services that are used by the application.</span></span>

![<span data-ttu-id="88673-105">응용 프로그램에서 Azure Blob Storage, Azure Functions, Cosmos DB, Azure Logic Apps, Azure Active Directory 같은 다양한 Azure 서비스를 사용하는 원리를 보여주는 일러스트레이션.</span><span class="sxs-lookup"><span data-stu-id="88673-105">An illustration showing how different Azure services such as, Azure Blob storage, Azure functions, Cosmos DB, Azure logic apps, and Azure active directory are used by the application.</span></span> ](../media/0-architecture.jpg)

1. <span data-ttu-id="88673-106">Azure Blob Storage는 정적 웹 콘텐츠(HTML, CSS, JS)를 제공하고 이미지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-106">Azure Blob storage serves static web content (HTML, CSS, JS) and stores images.</span></span>
2. <span data-ttu-id="88673-107">Azure Functions는 이미지 업로드, 크기 조정 및 메타데이터 저장을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-107">Azure Functions manages image uploads, resizing, and metadata storage.</span></span>
3. <span data-ttu-id="88673-108">Azure Cosmos DB는 이미지 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-108">Azure Cosmos DB stores image metadata.</span></span>
4. <span data-ttu-id="88673-109">Azure Logic Apps는 Cognitive Services Computer Vision API의 이미지 캡션을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-109">Azure Logic Apps retrieves image captions from the Cognitive Services Computer Vision API.</span></span>
5. <span data-ttu-id="88673-110">Azure Active Directory는 사용자 인증을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-110">Azure Active Directory manages user authentication.</span></span>

<span data-ttu-id="88673-111">Azure Blob Storage는 정적 파일을 호스트하는데 사용할 수 있는 저렴한 비용의 확장성이 매우 뛰어난 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="88673-111">Azure Blob storage is a low-cost and massively scalable service that can be used to host static files.</span></span> <span data-ttu-id="88673-112">이 모듈에서는 Blob Storage를 사용하여 빌드한 웹앱에 대한 정적 콘텐츠(예: HTML, JavaScript 또는 CSS)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-112">In this module, you will use Blob storage to serve static content (for example, HTML, JavaScript, or CSS) for a web app you build.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="88673-113">Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="88673-113">Create an Azure Storage account</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="88673-114">Azure Storage 계정은 테이블, 큐, 파일, Blob(개체) 및 가상 머신 디스크를 저장하도록 허용하는 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="88673-114">An Azure Storage account is an Azure resource that allows you to store tables, queues, files, blobs (objects), and virtual machine disks.</span></span>

1. <span data-ttu-id="88673-115">이 모듈에 대한 정적 콘텐츠(HTML, CSS 및 JavaScript 파일)는 Blob Storage에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="88673-115">The static content (HTML, CSS, and JavaScript files) for this module is hosted in Blob storage.</span></span> <span data-ttu-id="88673-116">Blob Storage를 사용하려면 Storage 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-116">Blob storage requires a Storage account.</span></span> <span data-ttu-id="88673-117">리소스 그룹에서 GPv2(범용 v2) Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="88673-117">Create a general-purpose v2 (GPv2) Storage account in the resource group.</span></span> <span data-ttu-id="88673-118">`<storage account name>`을 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="88673-118">Replace `<storage account name>` with a unique name.</span></span>

    ```azurecli
    az storage account create \
        -n <storage account name> \
        -g <rgn>[Sandbox resource group name]</rgn> \
        --kind StorageV2 \
        --https-only true \
        --sku Standard_LRS
    ```
    
1. <span data-ttu-id="88673-119">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-119">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="88673-120">포털의 맨 위에 있는 검색 창을 사용하여 방금 만든 저장소 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="88673-120">Use the Search bar at the top of the portal to find the storage account that you just created.</span></span> <span data-ttu-id="88673-121">계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="88673-121">Open the account.</span></span>

1. <span data-ttu-id="88673-122">왼쪽 탐색 영역에서 **정적 웹 사이트(미리 보기)** 를 선택하고 정적 웹 사이트 호스팅을 위한 컨테이너를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-122">On the left navigation, select **Static website (preview)** to configure a container for static website hosting.</span></span>
    - <span data-ttu-id="88673-123">**사용**을 선택하여 정적 웹 사이트를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-123">Select **Enabled** to enable a static website.</span></span>
    - <span data-ttu-id="88673-124">**index.html**을 인덱스 문서 이름으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-124">Enter **index.html** as the index document name.</span></span> <span data-ttu-id="88673-125">상자에는 이미 회색 글꼴로 *index.html*이 있지만 예제 텍스트일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="88673-125">The box already has *index.html* in a gray font, but this is only example text.</span></span> <span data-ttu-id="88673-126">상자에 **index.html**을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-126">You still have to enter **index.html** in the box.</span></span>
    - <span data-ttu-id="88673-127">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-127">Click **Save**.</span></span>
    
    ![정적 웹 사이트 설정 입력](../media/1-storage-static-website.png)

1. <span data-ttu-id="88673-129">모듈을 진행하면서 편리하게 복사할 수 있는 위치에 **기본 엔드포인트**를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-129">Save the **Primary Endpoint** in a place where you can conveniently copy it from while working through the module.</span></span> <span data-ttu-id="88673-130">이 엔드포인트는 웹 응용 프로그램의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="88673-130">This endpoint is the URL of your web application.</span></span>

## <a name="upload-the-web-application"></a><span data-ttu-id="88673-131">웹 응용 프로그램 업로드</span><span class="sxs-lookup"><span data-stu-id="88673-131">Upload the web application</span></span>

1. <span data-ttu-id="88673-132">이 모듈에서 빌드한 응용 프로그램에 대한 원본 파일은 [GitHub 리포지토리](https://github.com/Azure-Samples/functions-first-serverless-web-application)에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="88673-132">The source files for the application that you build in this module are located in a [GitHub repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span></span> <span data-ttu-id="88673-133">Cloud Shell의 홈 디렉터리로 이동하여 이 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-133">Go to your home directory in Cloud Shell and clone this repository.</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    <span data-ttu-id="88673-134">리포지토리는 `/home/<username>/functions-first-serverless-web-application`에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="88673-134">The repository is cloned to `/home/<username>/functions-first-serverless-web-application`</span></span>

1. <span data-ttu-id="88673-135">클라이언트 쪽 웹 응용 프로그램은 **www** 폴더에 배치되고 Vue.js JavaScript 프레임워크를 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="88673-135">The client-side web application is located in the **www** folder and is built using the Vue.js JavaScript framework.</span></span> <span data-ttu-id="88673-136">**www** 폴더를 열고, **npm** 명령을 실행하여 응용 프로그램의 종속성을 설치하고 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-136">Open the **www** folder and run **npm** commands to install the application dependencies and build the application.</span></span> <span data-ttu-id="88673-137">이러한 명령 중 마지막을 완료하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88673-137">The last of these commands might take several minutes to complete.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    <span data-ttu-id="88673-138">응용 프로그램은 **dist** 폴더에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="88673-138">The application is generated in the **dist** folder.</span></span>

1. <span data-ttu-id="88673-139">현재 디렉터리를 **dist** 폴더로 변경하고 응용 프로그램을 **$web** Blob 컨테이너로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-139">Change the current directory to the **dist** folder and upload the application to the **$web** blob container.</span></span>

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. <span data-ttu-id="88673-140">응용 프로그램을 보려면 웹 브라우저에서 정적 웹 사이트 기본 엔드포인트 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="88673-140">To view the application, open the static website’s primary endpoint URL in a web browser.</span></span>

    ![첫 번째 서버리스 웹앱 홈페이지](../media/1-app-screenshot-new.png)


## <a name="summary"></a><span data-ttu-id="88673-142">요약</span><span class="sxs-lookup"><span data-stu-id="88673-142">Summary</span></span>

<span data-ttu-id="88673-143">이 모듈에서는 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="88673-143">In this unit, you created a storage account.</span></span> <span data-ttu-id="88673-144">저장소 계정의 **$web**이라는 Blob 컨테이너는 웹 응용 프로그램의 정적 콘텐츠를 저장하고 콘텐츠를 공개적으로 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="88673-144">A blob container named **$web** in the storage account stores the static content for your web application and makes the content publicly available.</span></span> <span data-ttu-id="88673-145">다음으로, 서버리스 함수를 사용하여 이 웹 응용 프로그램에서 Blob Storage에 이미지를 업로드하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="88673-145">Next, you will learn how to use a serverless function to upload images to Blob storage from this web application.</span></span>