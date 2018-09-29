<span data-ttu-id="f14bb-101">우리는 지금 Azure Storage를 사용하여 사용자 대신 저장하는 사진과 기타 데이터를 관리하는 사진 공유 응용 프로그램을 만들고 있다는 사실을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f14bb-101">Recall that we are working on a photo-sharing application that will use Azure Storage to manage pictures and other bits of data we store on behalf of our users.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="f14bb-102">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="f14bb-102">::: zone pivot="csharp"</span></span>

<span data-ttu-id="f14bb-103">Storage API에 집중할 수 있도록 시나리오를 간소화하기 위해 새 .NET Core 콘솔 응용 프로그램을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-103">To simplify our scenario so that we can focus on the Storage APIs, we will create a new .NET Core Console application.</span></span> <span data-ttu-id="f14bb-104">또한 응용 프로그램이 항상 네트워크에 연결된다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-104">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="f14bb-105">그러나 네트워크 장애 시 사용자 환경에 영향을 미치거나 응용 프로그램 자체가 중단되는 일이 없도록 항상 앱을 보완해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-105">However, you should always harden your app to ensure network failures will not impact the user experience or result in a failure of the application itself.</span></span>

## <a name="create-a-net-core-application"></a><span data-ttu-id="f14bb-106">.NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f14bb-106">Create a .NET Core application</span></span>

<span data-ttu-id="f14bb-107">.NET Core는 macOS, Windows 및 Linux에서 실행되는 .NET의 플랫폼 간 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-107">.NET Core is a cross-platform version of .NET that runs on macOS, Windows, and Linux.</span></span> <span data-ttu-id="f14bb-108">도구를 로컬로 설치하거나 창의 오른쪽에 있는 Cloud Shell을 사용하여 아래 단계를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-108">You can install the tools locally or use the Cloud Shell on the right side of the window to execute the below steps below.</span></span>

1. <span data-ttu-id="f14bb-109">Cloud Shell에 로그인하거나 명령줄 세션을 열고 "PhotoSharingApp"이라는 이름의 새 .NET Core 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-109">Sign into the Cloud Shell or open a command-line session and create a new .NET Core Console application with the name "PhotoSharingApp".</span></span> <span data-ttu-id="f14bb-110">`-o` 또는 `--output` 플래그를 추가하여 특정 폴더에 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-110">You can add the `-o` or `--output` flag to create the app in a specific folder.</span></span>

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. <span data-ttu-id="f14bb-111">앱을 실행하여 올바르게 빌드 및 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-111">Run the app to make sure it builds and executes correctly.</span></span> <span data-ttu-id="f14bb-112">콘솔에 "Hello, World!"가</span><span class="sxs-lookup"><span data-stu-id="f14bb-112">It should display "Hello World!"</span></span> <span data-ttu-id="f14bb-113">표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-113">to the console.</span></span>

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
<span data-ttu-id="f14bb-114">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="f14bb-114">::: zone-end</span></span>

<span data-ttu-id="f14bb-115">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="f14bb-115">::: zone pivot="javascript"</span></span>

<span data-ttu-id="f14bb-116">Storage API에 집중할 수 있도록 시나리오를 간소화하기 위해 콘솔에서 실행할 수 있는 새 Node.js 응용 프로그램을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-116">To simplify our scenario so that we can focus on the Storage APIs, we will create a new Node.js application that can run from the console.</span></span> <span data-ttu-id="f14bb-117">또한 응용 프로그램이 항상 네트워크에 연결된다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-117">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="f14bb-118">그러나 네트워크 장애 시 사용자 환경에 영향을 미치거나 응용 프로그램 자체가 중단되는 일이 없도록 항상 앱을 보완해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-118">However, you should always harden your app to ensure network failures will not impact the user experience, or result in a failure of the application itself.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="f14bb-119">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f14bb-119">Create a Node.js application</span></span>

<span data-ttu-id="f14bb-120">Node.js는 JavaScript 앱을 실행하기 위한 인기 있는 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-120">Node.js is a popular framework for running JavaScript apps.</span></span> <span data-ttu-id="f14bb-121">주로 웹앱에 사용되지만, 명령줄에서 논리를 실행하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-121">It is most commonly used for web apps, but you can use it to run logic from the command line as well.</span></span> <span data-ttu-id="f14bb-122">도구를 로컬로 설치한 경우 명령줄에서 다음 단계를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-122">If you have the tools installed locally, you can run the following steps from a command line.</span></span> <span data-ttu-id="f14bb-123">또는 창 오른쪽에 있는 Cloud Shell을 사용하여 아래 단계를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-123">Alternatively, you can use the Cloud Shell on the right side of the window to execute the below steps.</span></span>

1. <span data-ttu-id="f14bb-124">Cloud Shell에 로그인하거나 명령줄 세션을 열고 "PhotoSharingApp"이라는 이름의 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-124">Sign into the Cloud Shell or open a command-line session and create a new folder named "PhotoSharingApp".</span></span>

    ```bash
    mkdir PhotoSharingApp
    ```

1. <span data-ttu-id="f14bb-125">새 폴더로 변경하고 `npm`을 사용하여 새 Node.js 앱을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-125">Change into the new folder and use `npm` to initialize a new Node.js app.</span></span> <span data-ttu-id="f14bb-126">이렇게 하면 앱을 설명하는 메타데이터가 포함된 **package.json** 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-126">This will create a **package.json** file containing metadata that describes the app.</span></span>

    ```bash
    cd PhotoSharingApp
    npm init -y
    ```

1. <span data-ttu-id="f14bb-127">코드가 이동할 새 소스 파일 **index.js**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-127">Create a new source file **index.js**, which is where our code will go.</span></span>

    ```bash
    touch index.js
    ```

1. <span data-ttu-id="f14bb-128">편집기를 사용하여 **index.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-128">Open the **index.js** file with an editor.</span></span> <span data-ttu-id="f14bb-129">Cloud Shell을 사용하는 경우 `code .`를 입력하여 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-129">If you are using the Cloud Shell, you can type `code .` to open an editor.</span></span>

1. <span data-ttu-id="f14bb-130">다음 프로그램을 **index.js** 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-130">Paste the following program into the **index.js** file.</span></span> <span data-ttu-id="f14bb-131">**Ctrl+V** 바로 가기 키를 사용하거나 마우스 오른쪽 단추를 클릭하여 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-131">You can use the **Ctrl+V** keyboard shortcut or right-click to paste.</span></span>

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. <span data-ttu-id="f14bb-132">&mdash; 파일을 저장하면 Cloud Shell 편집기의 오른쪽 상단 모서리에 있는 "..." 메뉴를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-132">Save the file&mdash;you can use the "..." menu on the top right corner of the Cloud Shell editor.</span></span>

1. <span data-ttu-id="f14bb-133">앱을 실행하여 올바르게 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-133">Run the app to make sure it executes correctly.</span></span> <span data-ttu-id="f14bb-134">콘솔에 "Hello, World!"가</span><span class="sxs-lookup"><span data-stu-id="f14bb-134">It should display "Hello, World!"</span></span> <span data-ttu-id="f14bb-135">표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f14bb-135">to the console.</span></span>

    ```bash
    node index.js
    ```

<span data-ttu-id="f14bb-136">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="f14bb-136">::: zone-end</span></span>