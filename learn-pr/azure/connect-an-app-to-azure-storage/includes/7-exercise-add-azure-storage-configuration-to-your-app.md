<span data-ttu-id="a4901-101">이 단원에서는 액세스 키를 검색하여 앱 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-101">In this unit you will retrieve the access key and add it to your app configuration.</span></span> <span data-ttu-id="a4901-102">또한 .NET Core 콘솔 응용 프로그램을 만들었으므로 구성 파일에서 해당 응용 프로그램으로 읽어오기 위한 지원을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-102">In addition, since we created a .NET Core console application, we need to add support for reading from configuration files to the application.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="a4901-103">JSON 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="a4901-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="a4901-104">이전 단원에서 만든 Visual Studio 프로젝트에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가**를 선택한 다음, **새 항목**을 선택하거나 Ctrl+Shift+A를 누르고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-104">In your Visual Studio project that we created in the previous unit, right click the project, select **Add**, and then select **New Item** (or hold down CTRL-SHIFT-A).</span></span>

1. <span data-ttu-id="a4901-105">모달 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-105">A modal dialog is presented.</span></span> <span data-ttu-id="a4901-106">**JavaScript JSON 구성 파일**을 선택하고 **appsettings.json**을 *이름* 텍스트 상자에 입력한 다음, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-106">Select **JavaScript JSON Configuration File** and type **appsettings.json** into the *Name* textbox, and then click **Add**.</span></span>

  ![앱 설정](..\media-draft\7-appsettings.png)

1. <span data-ttu-id="a4901-108">파일이 콘텐츠가 다음과 비슷한 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-108">A file is added to the project with contents similar to the following:</span></span>

    ```json
    {
      "exclude": [
        "**/bin",
        "**/bower_components",
        "**/jspm_packages",
        "**/node_modules",
        "**/obj",
        "**/platforms"
      ]
    }
    ```
1. <span data-ttu-id="a4901-109">**제외** 항목 및 연관된 콘텐츠를 제거하고 빈 문자열 값을 사용하여 단일 항목 **StorageAccountConnectionString**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-109">Remove the **exclude** entry and its associated contents and replace it with the single entry **StorageAccountConnectionString**, with an empty string value.</span></span> <span data-ttu-id="a4901-110">다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-110">It should look similar to the following:</span></span>

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```
1. <span data-ttu-id="a4901-111">**appsettings.json** 파일을 선택하고, 마우스 오른쪽 단추를 클릭한 다음, **속성**을 선택합니다(또는 Alt+Enter나 F4 키를 누름).</span><span class="sxs-lookup"><span data-stu-id="a4901-111">Select the **appsettings.json** file, right click it and select **Properties** (alternatively, press ALT+ENTER or F4).</span></span>

1. <span data-ttu-id="a4901-112">**출력 디렉터리로 복사**를 **변경된 내용만 복사**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-112">Change **Copy to Output Directory** to **Copy if newer**.</span></span>

  ![빌드 작업](..\media-draft\7-build-action.png)

  > <span data-ttu-id="a4901-114">이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-114">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="a4901-115">JSON 구성 파일을 읽도록 지원 추가</span><span class="sxs-lookup"><span data-stu-id="a4901-115">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="a4901-116">.NET Core 콘솔 응용 프로그램이 쉽게 JSON 구성 파일에서 읽을 수 있도록 하려면 특정 라이브러리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-116">A .NET Core console application requires certain libraries to be added to allow it to easily read from a JSON configuration file.</span></span>

1. <span data-ttu-id="a4901-117">프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리 …** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-117">Right click on the project and select **Manage Nuget Packages…**.</span></span>

![NuGet 패키지 관리](..\media-draft\5-manage-nuget-packages.png)

1. <span data-ttu-id="a4901-119">현재 설치된 NuGet 패키지를 보여주는 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-119">A page is displayed, showing currently installed Nuget packages.</span></span> <span data-ttu-id="a4901-120">**찾아보기** 옵션을 클릭하고 검색 필드에 **Microsoft.Extensions.Configuration.Json**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-120">Click on the **Browse** option and type **Microsoft.Extensions.Configuration.Json** in the search field.</span></span> <span data-ttu-id="a4901-121">**Microsoft.Extensions.Configuration.Json** 패키지가 검색 결과에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-121">The **Microsoft.Extensions.Configuration.Json** package is displayed in the search results.</span></span>

1. <span data-ttu-id="a4901-122">**Microsoft.Extensions.Configuration.Json** 패키지를 선택하고 오른쪽 창에서 **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-122">Select the **Microsoft.Extensions.Configuration.Json** package, and in the right pane select **Install**.</span></span>

1. <span data-ttu-id="a4901-123">**변경 내용 미리 보기** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-123">A **Preview Changes** dialog is displayed.</span></span> <span data-ttu-id="a4901-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-124">Click **OK**.</span></span>

1. <span data-ttu-id="a4901-125">라이선스 승인 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-125">A license acceptance dialog is displayed.</span></span> <span data-ttu-id="a4901-126">**동의함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-126">Click **I Accept**.</span></span>


## <a name="read-from-the-configuration-file"></a><span data-ttu-id="a4901-127">구성 파일에서 읽기</span><span class="sxs-lookup"><span data-stu-id="a4901-127">Read from the configuration file</span></span>

<span data-ttu-id="a4901-128">구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 콘솔 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-128">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="a4901-129">프로젝트에서 **Program.cs** 파일을 찾아 Visual Studio에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-129">Locate the **Program.cs** file in your project and open it in Visual Studio.</span></span>

1. <span data-ttu-id="a4901-130">파일 맨 위에 **using System;** 줄이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-130">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="a4901-131">해당 줄 아래에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-131">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="a4901-132">**Main** 메서드의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-132">Replace the contents of the **Main** method with the following code:</span></span>

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

1. <span data-ttu-id="a4901-133">**Program.cs** 파일은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-133">Your **Program.cs** file should now look like the following:</span></span>

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;

    namespace DemoConsoleApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                var builder = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json");

                var configuration = builder.Build();
            }
        }
    }
    ```

> <span data-ttu-id="a4901-134">이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-134">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

## <a name="add-your-connection-string-to-the-configuration-file"></a><span data-ttu-id="a4901-135">구성 파일에 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="a4901-135">Add your connection string to the configuration file</span></span>

<span data-ttu-id="a4901-136">이제 저장소 계정 연결 문자열을 가져와서 앱의 구성에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-136">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span>

1. <span data-ttu-id="a4901-137">저장소 계정이 포함된 구독의 Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-137">Navigate to the Azure portal for your subscription that contains your storage account.</span></span>

1. <span data-ttu-id="a4901-138">저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-138">Navigate to your storage account.</span></span>

1. <span data-ttu-id="a4901-139">포털에서 저장소 계정의 계정 키 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-139">Navigate to the Account Keys blade of the storage account in the portal.</span></span>

1. <span data-ttu-id="a4901-140">**key1** 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-140">Copy the **key1** connection string.</span></span>

1. <span data-ttu-id="a4901-141">포털에서 복사한 액세스 키의 콘텐츠에 **StorageAccountConnectionString**의 값으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-141">Paste in the contents of the access key you copied from the portal as the value for **StorageAccountConnectionString**.</span></span> <span data-ttu-id="a4901-142">이제 구성은 다음과 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4901-142">Your configuration should now look similar to the following:</span></span>

    ```json
    {
      "StorageAccountConnectionString": "your-access-key-connection-string-goes-here"
    }
    ```
