<span data-ttu-id="1ed75-101">::: zone pivot="csharp" .NET Core 응용 프로그램에 지원을 추가하여 구성 파일에서 연결 문자열을 검색해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-101">::: zone pivot="csharp" Let's add support to our .NET core application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="1ed75-102">먼저 필요한 배관을 추가하여 JSON 파일의 구성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-102">We'll start by adding the necessary plumbing to manage configuration in a JSON file.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="1ed75-103">JSON 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1ed75-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="1ed75-104">아직 없는 경우 `cd`를 PhotoSharingApp 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-104">`cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="1ed75-105">명령줄에서 `touch` 도구를 사용하여 **appsettings.json** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-105">Use the `touch` tool on the command line to create a file named **appsettings.json**.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="1ed75-106">편집기에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-106">Open the project in an editor.</span></span> <span data-ttu-id="1ed75-107">로컬로 작업하는 경우 선택한 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-107">If you are working locally, use your editor of choice.</span></span> <span data-ttu-id="1ed75-108">뛰어난 플랫폼 간 IDE인 **Visual Studio Code**를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-108">We recommend **Visual Studio Code**, which is an extensible cross-platform IDE.</span></span> <span data-ttu-id="1ed75-109">Cloud Shell에서 작업하는 경우 Cloud Shell 편집기를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-109">If you are working in the Cloud Shell, we recommend the Cloud Shell editor.</span></span> <span data-ttu-id="1ed75-110">다음 명령은 모두에서 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-110">The following command works for both.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="1ed75-111">편집기에서 **appsettings.json** 파일을 선택하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-111">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="1ed75-112">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-112">Save the file.</span></span> <span data-ttu-id="1ed75-113">Cloud Shell 편집기의 오른쪽 상단 모서리에 일반 파일 작업과 관련된 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-113">In the Cloud Shell editor, there is a menu in the top right corner that has common file operations.</span></span>

    ```json
    {
      "StorageAccountConnectionString": "<value>"
    }
    ```

1. <span data-ttu-id="1ed75-114">이제 저장소 계정 연결 문자열을 가져와서 앱의 구성에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-114">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span> <span data-ttu-id="1ed75-115">Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-115">In Cloud Shell run the following command.</span></span>

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. <span data-ttu-id="1ed75-116">해당 명령에서 반환되는 연결 문자열을 복사하고, **appsettings.json** 파일의 `"<value>"`를 이 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-116">Copy the connection string that is returned from that command, and replace `"<value>"` in the **appsettings.json** file with this connection string.</span></span> <span data-ttu-id="1ed75-117">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-117">Save the file.</span></span>

1. <span data-ttu-id="1ed75-118">다음으로 편집기에서 프로젝트 파일(**PhotoSharingApp.csproj**)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-118">Next, open the project file (**PhotoSharingApp.csproj**) in the editor.</span></span>

1. <span data-ttu-id="1ed75-119">프로젝트에 새 파일을 포함하고 이를 출력 폴더에 복사하려면 다음 구성 블록을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-119">Add the following configuration block to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="1ed75-120">이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-120">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. <span data-ttu-id="1ed75-121">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-121">Save the file.</span></span> <span data-ttu-id="1ed75-122">(반드시 이 작업을 수행해야 합니다. 그렇지 않으면 아래의 패키지를 추가할 때 변경 내용이 손실됩니다!)</span><span class="sxs-lookup"><span data-stu-id="1ed75-122">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="1ed75-123">JSON 구성 파일을 읽도록 지원 추가</span><span class="sxs-lookup"><span data-stu-id="1ed75-123">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="1ed75-124">.NET Core 응용 프로그램을 사용하려면 JSON 구성 파일을 읽을 NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-124">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="1ed75-125">창의 명령 프롬프트 섹션에서 **Microsoft.Extensions.Configuration.Json** NuGet 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-125">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="1ed75-126">구성 파일을 읽는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="1ed75-126">Add code to read the configuration file</span></span>

<span data-ttu-id="1ed75-127">구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 콘솔 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-127">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="1ed75-128">편집기에서 **Program.cs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-128">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="1ed75-129">파일 맨 위에 **using System;** 줄이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-129">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="1ed75-130">해당 줄 아래에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-130">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="1ed75-131">**Main** 메서드의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-131">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="1ed75-132">이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-132">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

<span data-ttu-id="1ed75-133">**Program.cs** 파일은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-133">Your **Program.cs** file should now look like the following:</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace PhotoSharingApp
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

<span data-ttu-id="1ed75-134">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="1ed75-134">::: zone-end</span></span>

<span data-ttu-id="1ed75-135">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="1ed75-135">::: zone pivot="javascript"</span></span>

<span data-ttu-id="1ed75-136">Node.js 응용 프로그램에 지원을 추가하여 구성 파일에서 연결 문자열을 검색해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-136">Let's add support to our Node.js application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="1ed75-137">먼저 필요한 배관을 추가하여 JavaScript 파일의 구성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-137">We'll start by adding the necessary plumbing to manage configuration from our JavaScript file.</span></span>

## <a name="create-a-env-configuration-file"></a><span data-ttu-id="1ed75-138">.env 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1ed75-138">Create a .env configuration file</span></span>

1. <span data-ttu-id="1ed75-139">프로젝트의 올바른 작업 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-139">Make sure you are in the correct working directory for your project.</span></span>

1. <span data-ttu-id="1ed75-140">명령줄에서 `touch` 도구를 사용하여 **.env** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-140">Use the `touch` tool on the command line to create a file named **.env**.</span></span>

    ```bash
    touch .env
    ```

1. <span data-ttu-id="1ed75-141">Cloud Shell 편집기에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-141">Open the project in the Cloud Shell editor.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="1ed75-142">편집기에서 **.env** 파일을 선택하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-142">Select the **.env** file in the editor and add the following text.</span></span> <span data-ttu-id="1ed75-143">새 파일을 확인하려면 코드에서 새로 고침 단추를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-143">You may need to click the refresh button in code to see the new files.</span></span> <span data-ttu-id="1ed75-144">파일 저장 - 온라인 편집기의 오른쪽 상단 모서리에 일반 파일 작업과 관련된 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-144">Save the file - in the online editor, there is a menu in the top right corner which has common file operations.</span></span>

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > <span data-ttu-id="1ed75-145">**AZURE_STORAGE_CONNECTION_STRING** 값은 Storage API가 액세스 키를 조회하는 데 사용되는 하드 코딩된 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-145">The **AZURE_STORAGE_CONNECTION_STRING** value is a hard-coded environment variable used for Storage APIs to look up access keys.</span></span> <span data-ttu-id="1ed75-146">원하는 경우 자신이 원하는 이름을 사용할 수 있지만 Node.js 앱에서 `BlobService` 개체를 만들 때 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-146">You can use your own name if you prefer, but you must supply the name to the when you create the `BlobService` object in your Node.js app.</span></span>

1. <span data-ttu-id="1ed75-147">이제 저장소 계정 연결 문자열을 가져와서 앱의 구성에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-147">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span> <span data-ttu-id="1ed75-148">Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-148">In Cloud Shell run the following command.</span></span>

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. <span data-ttu-id="1ed75-149">해당 명령에서 반환되는 연결 문자열을 복사하고, **.env** 파일의 `<value>`를 이 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-149">Copy the connection string that is returned from that command, minus the quotes, and replace `<value>` in the **.env** file with this connection string.</span></span>

1. <span data-ttu-id="1ed75-150">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-150">Save the file.</span></span>

## <a name="add-support-to-read-an-environment-configuration-file"></a><span data-ttu-id="1ed75-151">환경 구성 파일을 읽도록 지원 추가</span><span class="sxs-lookup"><span data-stu-id="1ed75-151">Add support to read an environment configuration file</span></span>

<span data-ttu-id="1ed75-152">Node.js 앱에는 **dotenv** 패키지를 추가하여 **.env** 파일에서 읽을 수 있는 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-152">Node.js apps can include support to read from the **.env** file by adding the **dotenv** package.</span></span>

1. <span data-ttu-id="1ed75-153">창의 명령 프롬프트 섹션에서 `npm`을 사용하여 *dotenv*\* 패키지에 대한 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-153">In the command prompt section of the window, add a dependency to the  *dotenv*\* package using `npm`.</span></span>

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="1ed75-154">구성 파일을 읽는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="1ed75-154">Add code to read the configuration file</span></span>

<span data-ttu-id="1ed75-155">구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-155">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our application.</span></span>

1. <span data-ttu-id="1ed75-156">편집기에서 \*index.js\*\*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-156">Select *index.js*\* in the editor.</span></span>

1. <span data-ttu-id="1ed75-157">파일 맨 위에 **#!/usr/bin/env node** 줄이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-157">At the top of the file, a **#!/usr/bin/env node** line is present.</span></span> <span data-ttu-id="1ed75-158">이 줄 아래에 **dotenv** 패키지를 로드하도록 `require` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-158">Underneath that line, add a `require` statement to load the **dotenv** package.</span></span> <span data-ttu-id="1ed75-159">이렇게 하면 **.env** 파일에 정의된 환경 변수를 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-159">This will make environment variables defined in our **.env** file available to the program.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
<span data-ttu-id="1ed75-160">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="1ed75-160">::: zone-end</span></span>

<span data-ttu-id="1ed75-161">이제 모든 정보가 정리되었으므로 저장소 계정을 사용하기 위한 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed75-161">Now that we have that all wired up, we can start adding code to use our storage account.</span></span>