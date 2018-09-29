<span data-ttu-id="04acb-101">큐를 사용할 클라이언트 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-101">Let's create a client application to work with a queue.</span></span> <span data-ttu-id="04acb-102">그런 다음, 코드에 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-102">Then we'll add our connection string to the code.</span></span>

> [!NOTE]
> <span data-ttu-id="04acb-103">.NET Core를 설치한 경우 로컬 컴퓨터에 또는 Cloud Shell 환경에서 직접 클라이언트 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-103">You can create the client application on your local computer if you have .NET Core installed, or directly in the Cloud Shell environment.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="04acb-104">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="04acb-104">Create the application</span></span>

<span data-ttu-id="04acb-105">Linux, macOS 또는 Windows에서 실행할 수 있는 .NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-105">We'll create a .NET Core application that you can run on Linux, macOS, or Windows.</span></span> <span data-ttu-id="04acb-106">이름을 **QueueApp**으로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-106">Let's name it **QueueApp**.</span></span> <span data-ttu-id="04acb-107">간단히 하기 위해 큐를 통해 메시지를 보내고 받을 수 있는 단일 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-107">For simplicity, we'll use a single app that will both send and receive messages through our queue.</span></span>

1. <span data-ttu-id="04acb-108">`dotnet new` 명령을 사용하여 이름이 **QueueApp**인 새 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-108">Use the `dotnet new` command to create a new console app with the name **QueueApp**.</span></span> <span data-ttu-id="04acb-109">오른쪽의 Cloud Shell에 명령을 입력하거나, 로컬로 작업하는 경우 터미널/콘솔 창에 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-109">You can type commands into the Cloud Shell on the right, or if you are working locally, in a terminal/console window.</span></span> <span data-ttu-id="04acb-110">이 명령은 단일 원본 파일(`Program.cs`)이 있는 간단한 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-110">This command creates a simple app with a single source file: `Program.cs`.</span></span>

    ```azurecli
    dotnet new console -n QueueApp
    ```

1. <span data-ttu-id="04acb-111">새로 생성된 `QueueApp` 폴더로 전환하고 앱을 빌드하여 문제가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-111">Switch to the newly created `QueueApp` folder and build the app to verify that all is well.</span></span>

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a><span data-ttu-id="04acb-112">연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="04acb-112">Get your connection string</span></span>

<span data-ttu-id="04acb-113">앞서 말한 것처럼 연결 문자열은 Azure Portal에 있는 저장소 계정의 **설정 > 액세스 키** 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-113">Recall that your connection string is available in the Azure portal **Settings > Access keys** section of your storage account.</span></span>

<span data-ttu-id="04acb-114">Azure CLI 또는 PowerShell 도구를 통해 연결 문자열을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-114">You can also retrieve it through the Azure CLI or PowerShell tools.</span></span> <span data-ttu-id="04acb-115">Azure CLI 명령을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-115">Let's use the Azure CLI command.</span></span> <span data-ttu-id="04acb-116">`<name>`을 만든 저장소 계정의 특정 이름으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-116">Remember to replace the `<name>` with the specific name of the storage account you created.</span></span> <span data-ttu-id="04acb-117">미리 알림이 필요한 경우 `az storage account list`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-117">You can use `az storage account list` if you need a reminder.</span></span>

```azurecli
az storage account show-connection-string --name <name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="04acb-118">이 명령은 연결 문자열이 포함된 JSON 블록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-118">This command will return a JSON block with your connection string.</span></span> <span data-ttu-id="04acb-119">여기에는 저장소 계정 이름과 계정 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-119">It will include the storage account name and the account key:</span></span>

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a><span data-ttu-id="04acb-120">응용 프로그램에 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="04acb-120">Add the connection string to the application</span></span>

<span data-ttu-id="04acb-121">마지막으로 앱에서 저장소 계정에 액세스할 수 있도록 연결 문자열을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-121">Finally, let's add the connection string into our app so it can access the storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="04acb-122">간단히 하기 위해 **Program.cs** 파일에 연결 문자열을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-122">For simplicity, you will place the connection string in the **Program.cs** file.</span></span> <span data-ttu-id="04acb-123">프로덕션 응용 프로그램에서는 이 연결 문자열을 안전한 위치에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-123">In a production application, you should store it in a secure location.</span></span> <span data-ttu-id="04acb-124">서버 쪽에서는 Azure Key Vault를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-124">For server side use, we recommend using Azure Key Vault.</span></span>

1. <span data-ttu-id="04acb-125">터미널에서 `code .`을 입력하여 온라인 코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-125">Type `code .` in the terminal to open the online code editor.</span></span> <span data-ttu-id="04acb-126">또는 사용자 고유의 작업을 수행 중인 경우에는 원하는 IDE를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-126">Alternatively, if you are working on your own you can use the IDE of your choice.</span></span> <span data-ttu-id="04acb-127">뛰어난 플랫폼 간 IDE인 Visual Studio Code를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-127">We recommend Visual Studio Code, which is an excellent cross-platform IDE.</span></span>

1. <span data-ttu-id="04acb-128">프로젝트에서 `Program.cs` 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-128">Open the `Program.cs` source file in the project.</span></span>

1. <span data-ttu-id="04acb-129">`Program` 클래스에서 연결 문자열을 보유할 `const string` 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-129">In the `Program` class, add a `const string` value to hold the connection string.</span></span> <span data-ttu-id="04acb-130">이 값(텍스트 **DefaultEndpointsProtocol**로 시작)만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-130">You only need the value (it starts with the text **DefaultEndpointsProtocol**).</span></span>

1. <span data-ttu-id="04acb-131">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-131">Save the file.</span></span> <span data-ttu-id="04acb-132">클라우드 편집기의 오른쪽 모서리에서 줄임표("...")를 클릭하거나 액셀러레이터 키(Windows 및 Linux에서 <kbd>Ctrl+S</kbd>, macOS에서 <kbd>Cmd+S</kbd>)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-132">You can click the ellipse "..." in the right corner of the cloud editor, or use the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

<span data-ttu-id="04acb-133">코드는 다음과 유사해야 합니다(문자열 값이 사용자 계정에 고유함).</span><span class="sxs-lookup"><span data-stu-id="04acb-133">Your code should look something like this (the string value will be unique to your account).</span></span>

```csharp
...
namespace QueueApp
{
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https; ...";
        
        ...
    }
}
```

<span data-ttu-id="04acb-134">이제 이 시작 프로젝트 설정이 완료되었으므로 코드에서 큐로 작업을 수행하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-134">Now that we have this starter project setup, let's look at how to work with a queue in code.</span></span> <span data-ttu-id="04acb-135">모두가 _messages_로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="04acb-135">It all starts with _messages_.</span></span>