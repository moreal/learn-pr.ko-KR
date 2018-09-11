<span data-ttu-id="ae31f-101">큐를 사용할 클라이언트 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-101">Let's create a client application to work with a queue.</span></span> <span data-ttu-id="ae31f-102">그런 다음, 코드에 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-102">Then we'll add our connection string to the code.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="ae31f-103">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ae31f-103">Create the application</span></span>

<span data-ttu-id="ae31f-104">Linux, macOS 또는 Windows에서 실행할 수 있는 .NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-104">We'll create a .NET Core application that you can run on Linux, macOS, or Windows.</span></span> <span data-ttu-id="ae31f-105">이름을 **QueueApp**으로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-105">Let's name it **QueueApp**.</span></span> <span data-ttu-id="ae31f-106">간단히 하기 위해 큐를 통해 메시지를 보내고 받을 수 있는 단일 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-106">For simplicity, we'll use a single app that will both send and receive messages through our queue.</span></span>

1. <span data-ttu-id="ae31f-107">`dotnet new` 명령을 사용하여 이름이 **QueueApp**인 새 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-107">Use the `dotnet new` command to create a new console app with the name **QueueApp**.</span></span> <span data-ttu-id="ae31f-108">오른쪽의 Cloud Shell에 명령을 입력하거나, 로컬로 작업하는 경우 터미널/콘솔 창에 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-108">You can type commands into the Cloud Shell on the right, or if you are working locally, in a terminal/console window.</span></span> <span data-ttu-id="ae31f-109">그러면 단일 소스 파일(`Program.cs`)이 있는 단순 앱이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-109">This creates a simple app with a single source file: `Program.cs`.</span></span>

    ```azurecli
    dotnet new console -n QueueApp
    ```

2. <span data-ttu-id="ae31f-110">새로 생성된 `QueueApp` 폴더로 전환하고 앱을 빌드하여 문제가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-110">Switch to the newly created `QueueApp` folder and build the app to verify that all is well.</span></span>

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a><span data-ttu-id="ae31f-111">연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="ae31f-111">Get your connection string</span></span>

<span data-ttu-id="ae31f-112">앞서 언급한 것처럼 연결 문자열은 Azure Portal에 있는 저장소 계정의 **설정 > 액세스 키** 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-112">Recall that your connection string is available in the Azure portal **Settings > Access keys** section of your storage account.</span></span>

<span data-ttu-id="ae31f-113">Azure CLI 또는 Powershell 도구를 통해 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-113">You can also retrieve it through the Azure CLI or Powershell tools.</span></span> <span data-ttu-id="ae31f-114">Azure CLI 명령을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-114">Let's use the Azure CLI command.</span></span> <span data-ttu-id="ae31f-115">`<name>`을 만든 저장소 계정의 특정 이름으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-115">Remember to replace the `<name>` with the specific name of the storage account you created.</span></span> <span data-ttu-id="ae31f-116">미리 알림이 필요한 경우 `az storage account list`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-116">You can use `az storage account list` if you need a reminder.</span></span>

```azurecli
az storage account show-connection-string --name <name> --resource-group ExerciseResources
```

<span data-ttu-id="ae31f-117">이 명령은 연결 문자열이 포함된 JSON 블록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-117">This command will return a JSON block with your connection string.</span></span> <span data-ttu-id="ae31f-118">여기에는 저장소 계정 이름과 계정 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-118">It will include the storage account name and the account key:</span></span>

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a><span data-ttu-id="ae31f-119">응용 프로그램에 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="ae31f-119">Add the connection string to the application</span></span>

<span data-ttu-id="ae31f-120">마지막으로 앱에서 저장소 계정에 액세스할 수 있도록 연결 문자열을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-120">Finally, let's add the connection string into our app so it can access the storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="ae31f-121">간단히 하기 위해 **Program.cs** 파일에 연결 문자열을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-121">For simplicity, you will place the connection string in the **Program.cs** file.</span></span> <span data-ttu-id="ae31f-122">프로덕션 응용 프로그램에서는 이 연결 문자열을 안전한 위치에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-122">In a production application, you should store it in a secure location.</span></span> <span data-ttu-id="ae31f-123">서버 쪽에서는 Azure Key Vault를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-123">For server side use, we recommend using Azure Key Vault.</span></span>

1. <span data-ttu-id="ae31f-124">터미널에서 `code .`을 입력하여 온라인 코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-124">Type `code .` in the terminal to open the online code editor.</span></span> <span data-ttu-id="ae31f-125">또는 사용자 고유의 작업을 수행 중인 경우에는 원하는 IDE를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-125">Alternatively, if you are working on your own you can use the IDE of your choice.</span></span> <span data-ttu-id="ae31f-126">뛰어난 플랫폼 간 IDE인 Visual Studio Code를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-126">We recommend Visual Studio Code, which is an excellent cross-platform IDE.</span></span>

2. <span data-ttu-id="ae31f-127">프로젝트에서 `Program.cs` 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-127">Open the `Program.cs` source file in the project.</span></span>

3. <span data-ttu-id="ae31f-128">`Program` 클래스에서 연결 문자열을 보유할 `const string` 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-128">In the `Program` class, add a `const string` value to hold the connection string.</span></span> <span data-ttu-id="ae31f-129">이 값(텍스트 **DefaultEndpointsProtocol**로 시작)만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-129">You only need the value (it starts with the text **DefaultEndpointsProtocol**).</span></span>

4. <span data-ttu-id="ae31f-130">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-130">Save the file.</span></span> <span data-ttu-id="ae31f-131">클라우드 편집기의 오른쪽 모서리에 있는 줄임표 “...”를 클릭하면 바로 가기 키도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-131">You can click the ellipse "..." in the right corner of the cloud editor, it will also show you the keyboard shortcut.</span></span>

<span data-ttu-id="ae31f-132">코드는 다음과 유사해야 합니다(문자열 값이 사용자 계정에 고유함).</span><span class="sxs-lookup"><span data-stu-id="ae31f-132">Your code should look something like this (the string value will be unique to your account).</span></span>

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

<span data-ttu-id="ae31f-133">이제 이 시작 프로젝트 설정이 완료되었으므로 코드에서 큐로 작업을 수행하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-133">Now that we have this starter project setup, let's look at how to work with a queue in code.</span></span> <span data-ttu-id="ae31f-134">모두가 _messages_로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae31f-134">It all starts with _messages_.</span></span>