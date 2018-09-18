<span data-ttu-id="e46d7-101">우리는 지금 Azure Storage를 사용하여 사용자 대신 저장하는 사진과 기타 데이터를 관리하는 사진 공유 응용 프로그램을 만들고 있다는 사실을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e46d7-101">Recall that we are working on a photo-sharing application that will use Azure Storage to manage pictures and other bits of data we store on behalf of our users.</span></span>

<span data-ttu-id="e46d7-102">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="e46d7-102">::: zone pivot="csharp"</span></span>

<span data-ttu-id="e46d7-103">Storage API에 집중할 수 있도록 시나리오를 간소화하기 위해 새 .NET Core 콘솔 응용 프로그램을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-103">To simplify our scenario so that we can focus on the Storage APIs, we will create a new .NET Core Console application.</span></span> <span data-ttu-id="e46d7-104">또한 응용 프로그램이 항상 네트워크에 연결된다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-104">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="e46d7-105">그러나 네트워크 장애 시 사용자 환경에 영향을 미치거나 응용 프로그램 자체가 중단되는 일이 없도록 항상 앱을 보완해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-105">However, you should always harden your app to ensure network failures will not impact the user experience, or result in a failure of the application itself.</span></span>

## <a name="create-a-net-core-application"></a><span data-ttu-id="e46d7-106">.NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e46d7-106">Create a .NET Core application</span></span>

<span data-ttu-id="e46d7-107">.NET Core는 macOS, Windows, 및 Linux에서 실행되는 .NET의 플랫폼 간 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-107">.NET Core is a cross-platform version of .NET that runs on macOS, Windows, and Linux.</span></span> <span data-ttu-id="e46d7-108">이 도구를 로컬로 설치할 수도 있고, 창의 오른쪽에 있는 Cloud Shell을 사용하여 아래 단계를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-108">You can install the tools locally, or use the Cloud Shell on the right side of the window to execute the below steps.</span></span> 

1. <span data-ttu-id="e46d7-109">Cloud Shell에 로그인하거나 명령줄 세션을 열고 "PhotoSharingApp"이라는 이름의 새 .NET Core 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-109">Sign into the Cloud Shell or open a command line session and create a new .NET Core Console application with the name "PhotoSharingApp".</span></span> <span data-ttu-id="e46d7-110">`-o` 또는 `--output` 플래그를 추가하여 특정 폴더에 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-110">You can add the `-o` or `--output` flag to create the app in a specific folder.</span></span>

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. <span data-ttu-id="e46d7-111">앱을 실행하여 올바르게 빌드 및 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-111">Run the app to make sure it builds and executes correctly.</span></span> <span data-ttu-id="e46d7-112">콘솔에 "Hello, World!"가</span><span class="sxs-lookup"><span data-stu-id="e46d7-112">It should display "Hello, World!"</span></span> <span data-ttu-id="e46d7-113">표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-113">to the console.</span></span>

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
<span data-ttu-id="e46d7-114">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="e46d7-114">::: zone-end</span></span>

<span data-ttu-id="e46d7-115">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="e46d7-115">::: zone pivot="javascript"</span></span>

<span data-ttu-id="e46d7-116">Storage API에 집중할 수 있도록 시나리오를 간소화하기 위해 콘솔에서 실행할 수 있는 새 Node.js 응용 프로그램을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-116">To simplify our scenario so that we can focus on the Storage APIs, we will create a new Node.js application that can run from the console.</span></span> <span data-ttu-id="e46d7-117">또한 응용 프로그램이 항상 네트워크에 연결된다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-117">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="e46d7-118">그러나 네트워크 장애 시 사용자 환경에 영향을 미치거나 응용 프로그램 자체가 중단되는 일이 없도록 항상 앱을 보완해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-118">However, you should always harden your app to ensure network failures will not impact the user experience, or result in a failure of the application itself.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="e46d7-119">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e46d7-119">Create a Node.js application</span></span>

<span data-ttu-id="e46d7-120">Node.js는 JavaScript 앱을 실행하기 위한 인기 있는 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-120">Node.js is a popular framework for running JavaScript apps.</span></span> <span data-ttu-id="e46d7-121">주로 웹앱에 사용되지만, 명령줄에서 논리를 실행하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-121">It is most commonly used for web apps, but you can use it to run logic from the command line as well.</span></span> <span data-ttu-id="e46d7-122">도구를 로컬로 설치한 경우 명령줄에서 다음 단계를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-122">If you have the tools installed locally, you can run the following steps from a command line.</span></span> <span data-ttu-id="e46d7-123">또는 창 오른쪽의 Cloud Shell을 사용하여 아래 단계를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-123">Alternatively, you can use the Cloud Shell on the right side of the window to execute the below steps.</span></span>

1. <span data-ttu-id="e46d7-124">Cloud Shell에 로그인하거나 명령줄 세션을 열고 "PhotoSharingApp"이라는 이름의 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-124">Sign into the Cloud Shell or open a command line session and create a new folder named "PhotoSharingApp".</span></span>

    ```bash
    mkdir PhotoSharingApp
    ```

1. <span data-ttu-id="e46d7-125">새 폴더로 변경하고 NPM(노드 패키지 관리자)을 사용하여 새 앱을 설명할 **package.json** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-125">Change into the new folder and create a **package.json** file with the Node Package Manager (NPM) that will describe our new app.</span></span>
    - <span data-ttu-id="e46d7-126">파일 이름을 "PhotoSharingApp"으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-126">Name it "PhotoSharingApp".</span></span>
    - <span data-ttu-id="e46d7-127">그 외의 프롬프트에서는 기본값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-127">You can take defaults for all the other prompts.</span></span>

    ```bash
    cd PhotoSharingApp
    npm init
    ```

1. <span data-ttu-id="e46d7-128">코드가 이동할 새 소스 파일 **index.js**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-128">Create a new source file **index.js** which will be where our code will go.</span></span>

    ```bash
    touch index.js
    ```

1. <span data-ttu-id="e46d7-129">편집기를 사용하여 **index.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-129">Open the **index.js** file with an editor.</span></span> <span data-ttu-id="e46d7-130">Cloud Shell을 사용하는 경우 `code .`를 입력하여 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-130">If you are using the Cloud Shell, you can type `code .` to open an editor.</span></span>

1. <span data-ttu-id="e46d7-131">다음 프로그램을 **index.js** 파일에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-131">Put the following program into the **index.js** file.</span></span>

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. <span data-ttu-id="e46d7-132">파일을 저장합니다. Cloud Shell 편집기의 오른쪽 상단 모서리에서 "..." 메뉴를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-132">Save the file - you can use the "..." menu on the top right corner of the Cloud Shell editor.</span></span>

1. <span data-ttu-id="e46d7-133">앱을 실행하여 올바르게 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-133">Run the app to make sure it executes correctly.</span></span> <span data-ttu-id="e46d7-134">콘솔에 "Hello, World!"가</span><span class="sxs-lookup"><span data-stu-id="e46d7-134">It should display "Hello, World!"</span></span> <span data-ttu-id="e46d7-135">표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e46d7-135">to the console.</span></span>

    ```bash
    node index.js
    ```

<span data-ttu-id="e46d7-136">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="e46d7-136">::: zone-end</span></span>