<span data-ttu-id="07eda-101">이전 단원에서는 서버리스 함수가 웹 응용 프로그램에서 Blob Storage로 이미지의 안전한 업로드를 용이하게 할 수 있는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-101">In the previous unit, you saw how a serverless function can facilitate the secure uploading of images to Blob storage from a web application.</span></span> <span data-ttu-id="07eda-102">이 모듈에서는 서버를 사용하지 않는 다른 함수를 만들어서 업로드된 이미지를 감시하고 썸네일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-102">In this module, you create another serverless function to watch for uploaded images and create thumbnails from them.</span></span>

## <a name="create-a-blob-storage-container-for-thumbnails"></a><span data-ttu-id="07eda-103">썸네일에 대한 Blob Storage 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="07eda-103">Create a Blob storage container for thumbnails</span></span>

<span data-ttu-id="07eda-104">전체 크기 이미지는 **images**라는 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-104">The full-size images are stored in a container named **images**.</span></span> <span data-ttu-id="07eda-105">해당 이미지의 썸네일을 저장할 다른 컨테이너가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-105">You need another container to store thumbnails of those images.</span></span>

<span data-ttu-id="07eda-106">모든 Blob에 대한 공용 액세스 권한이 있는 저장소 계정에서 **thumbnails**라는 새 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-106">Create a new container named **thumbnails** in your Storage account with public access to all blobs.</span></span>

```azurecli
az storage container create -n thumbnails --account-name <storage account name> --public-access blob
```

## <a name="create-a-blob-triggered-serverless-function"></a><span data-ttu-id="07eda-107">Blob 트리거 서버를 사용하지 않는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="07eda-107">Create a blob-triggered serverless function</span></span>

<span data-ttu-id="07eda-108">트리거는 함수가 호출되는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-108">A trigger defines how a function is invoked.</span></span> <span data-ttu-id="07eda-109">다음에 만든 함수는 Blob 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-109">The function you create next uses a blob trigger.</span></span> <span data-ttu-id="07eda-110">Blob(이미지 파일)을 **images** 컨테이너에 업로드하면 함수가 자동으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-110">The function is automatically invoked when a blob (image file) is uploaded to the **images** container.</span></span> <span data-ttu-id="07eda-111">함수에는 하나의 트리거만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-111">A function must have one trigger.</span></span> <span data-ttu-id="07eda-112">트리거는 관련 데이터가 있으며, 이 데이터는 일반적으로 함수를 트리거한 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-112">Triggers have associated data, which are usually the payload that triggered the function.</span></span>

<span data-ttu-id="07eda-113">바인딩은 함수가 Azure 또는 타사 서비스에서 데이터를 읽고 기록하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-113">Bindings define how a function reads or writes data in Azure or third-party services.</span></span> <span data-ttu-id="07eda-114">이 함수는 함수를 트리거하는 이미지의 썸네일 버전을 만들고 *thumbnails* 컨테이너에서 썸네일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-114">This function creates a thumbnail version of the image that triggers it and saves the thumbnail in a *thumbnails* container.</span></span>

1. <span data-ttu-id="07eda-115">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-115">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="07eda-116">Function 앱을 열고 포털의 맨 위에 있는 **검색** 상자를 사용하여 이름으로 앱을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-116">Open your Function app, you can use the **Search** box at the top of the portal to find it by name.</span></span>

1. <span data-ttu-id="07eda-117">Functions 앱 창의 왼쪽 탐색에서 **함수**를 가리키고 더하기 기호(+)를 클릭하여 새 서버리스 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-117">In the Functions app window's left navigation, point to **Functions** and click the plus sign (+) to create a new serverless function.</span></span> <span data-ttu-id="07eda-118">빠른 시작 페이지가 표시되면 **사용자 지정 함수**를 클릭하여 함수 템플릿 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-118">If a quickstart page appears, click **Custom function** to see a list of function templates.</span></span>

1. <span data-ttu-id="07eda-119">**BlobTrigger** 템플릿을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-119">Find the **BlobTrigger** template and select it.</span></span>

1. <span data-ttu-id="07eda-120">이러한 값을 사용하여 이미지를 업로드하는 경우 썸네일을 생성하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-120">Use these values to create a function that creates thumbnails as images are uploaded:</span></span>

    | <span data-ttu-id="07eda-121">설정</span><span class="sxs-lookup"><span data-stu-id="07eda-121">Setting</span></span>      |  <span data-ttu-id="07eda-122">제안 값</span><span class="sxs-lookup"><span data-stu-id="07eda-122">Suggested value</span></span>   | <span data-ttu-id="07eda-123">설명</span><span class="sxs-lookup"><span data-stu-id="07eda-123">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="07eda-124">**언어**</span><span class="sxs-lookup"><span data-stu-id="07eda-124">**Language**</span></span> | <span data-ttu-id="07eda-125">C# 또는 JavaScript</span><span class="sxs-lookup"><span data-stu-id="07eda-125">C# or JavaScript</span></span> | <span data-ttu-id="07eda-126">기본 설정 언어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-126">Choose your preferred language.</span></span> |
    | <span data-ttu-id="07eda-127">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="07eda-127">**Name your function**</span></span> | <span data-ttu-id="07eda-128">ResizeImage</span><span class="sxs-lookup"><span data-stu-id="07eda-128">ResizeImage</span></span> | <span data-ttu-id="07eda-129">응용 프로그램이 함수를 검색할 수 있도록 표시된 대로 이 이름을 정확히 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-129">Enter this name exactly as shown, so the application can discover the function.</span></span> |
    | <span data-ttu-id="07eda-130">**Path**</span><span class="sxs-lookup"><span data-stu-id="07eda-130">**Path**</span></span> | <span data-ttu-id="07eda-131">images/{name}</span><span class="sxs-lookup"><span data-stu-id="07eda-131">images/{name}</span></span> | <span data-ttu-id="07eda-132">파일이 **images** 컨테이너에 표시되면 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-132">Execute the function when a file appears in the **images** container.</span></span> |
    | <span data-ttu-id="07eda-133">**저장소 계정 정보**</span><span class="sxs-lookup"><span data-stu-id="07eda-133">**Storage account information**</span></span> | <span data-ttu-id="07eda-134">AZURE_STORAGE_CONNECTION_STRING</span><span class="sxs-lookup"><span data-stu-id="07eda-134">AZURE_STORAGE_CONNECTION_STRING</span></span> | <span data-ttu-id="07eda-135">연결 문자열을 사용하여 이전에 만든 환경 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-135">Use the environment variable previously created with the connection string.</span></span> |

    ![새로운 함수에 대한 설정을 입력합니다.](../media/3-new-function.png)

1. <span data-ttu-id="07eda-137">**만들기**를 클릭하여 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-137">Click **Create** to create the function.</span></span>

1. <span data-ttu-id="07eda-138">함수를 만들면 **통합**을 클릭하여 해당 트리거, 입력 및 출력 바인딩을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-138">When the function is created, click **Integrate** to view its trigger, input, and output bindings.</span></span>

1. <span data-ttu-id="07eda-139">**새 출력**을 클릭하여 새 출력 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-139">Click **New output** to create a new output binding.</span></span>

    ![통합 탭에서 새 출력 선택](../media/3-new-output.jpg)

1. <span data-ttu-id="07eda-141">**Azure Blob Storage**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-141">Select **Azure Blob Storage** and click **Select**.</span></span> <span data-ttu-id="07eda-142">**선택** 단추를 보려면 아래로 스크롤해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-142">You may have to scroll down to see the **Select** button.</span></span>

    ![Azure Blob Storage 선택](../media/3-storage-output.jpg)

1. <span data-ttu-id="07eda-144">다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-144">Enter the following values:</span></span>

    | <span data-ttu-id="07eda-145">설정</span><span class="sxs-lookup"><span data-stu-id="07eda-145">Setting</span></span>      |  <span data-ttu-id="07eda-146">제안 값</span><span class="sxs-lookup"><span data-stu-id="07eda-146">Suggested value</span></span>   | <span data-ttu-id="07eda-147">설명</span><span class="sxs-lookup"><span data-stu-id="07eda-147">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="07eda-148">**Blob 매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="07eda-148">**Blob parameter name**</span></span> | <span data-ttu-id="07eda-149">썸네일</span><span class="sxs-lookup"><span data-stu-id="07eda-149">thumbnail</span></span> | <span data-ttu-id="07eda-150">함수는 이 이름을 가진 매개 변수를 사용하여 썸네일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-150">The function uses the parameter with this name to write the thumbnail.</span></span> |
    | <span data-ttu-id="07eda-151">**함수 반환 값 사용**</span><span class="sxs-lookup"><span data-stu-id="07eda-151">**Use function return value**</span></span> | <span data-ttu-id="07eda-152">아니요</span><span class="sxs-lookup"><span data-stu-id="07eda-152">No</span></span> |  |
    | <span data-ttu-id="07eda-153">**Path**</span><span class="sxs-lookup"><span data-stu-id="07eda-153">**Path**</span></span> | <span data-ttu-id="07eda-154">thumbnails/{name}</span><span class="sxs-lookup"><span data-stu-id="07eda-154">thumbnails/{name}</span></span> | <span data-ttu-id="07eda-155">썸네일은 **thumbnails**라는 컨테이너에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-155">The thumbnails are written to a container named **thumbnails**.</span></span> |
    | <span data-ttu-id="07eda-156">**저장소 계정 연결**</span><span class="sxs-lookup"><span data-stu-id="07eda-156">**Storage account connection**</span></span> | <span data-ttu-id="07eda-157">AZURE_STORAGE_CONNECTION_STRING</span><span class="sxs-lookup"><span data-stu-id="07eda-157">AZURE_STORAGE_CONNECTION_STRING</span></span> | <span data-ttu-id="07eda-158">연결 문자열을 사용하여 이전에 만든 환경 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-158">Use the environment variable previously created with the connection string.</span></span> |

    ![Blob 출력 바인딩에 대한 설정 입력](../media/3-blob-output.png)

1. <span data-ttu-id="07eda-160">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-160">Click **Save** to save your changes.</span></span>

<span data-ttu-id="07eda-161">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="07eda-161">::: zone pivot="javascript"</span></span>

11. <span data-ttu-id="07eda-162">창의 오른쪽 위 모서리에서 **고급 편집기**를 클릭하여 바인딩을 나타내는 JSON을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-162">Click on **Advanced editor** in the top right corner of the window to reveal the JSON that represents the bindings.</span></span>

1. <span data-ttu-id="07eda-163">`blobTrigger` 바인딩에서 `binary`의 값을 포함한 `dataType`이라는 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-163">In the `blobTrigger` binding, add a property named `dataType` with a value of `binary`.</span></span> <span data-ttu-id="07eda-164">이렇게 하면 Blob 콘텐츠를 이진 데이터로 함수에 전달하도록 바인딩을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-164">This configures the binding to pass the blob contents to the function as binary data.</span></span>

    ```json
    {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "images/{name}",
        "connection": "AZURE_STORAGE_CONNECTION_STRING",
        "dataType": "binary"
    }
    ```

1. <span data-ttu-id="07eda-165">**저장**을 클릭하여 새 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-165">Click **Save** to create the new binding.</span></span>

<span data-ttu-id="07eda-166">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="07eda-166">::: zone-end</span></span>

<span data-ttu-id="07eda-167">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="07eda-167">::: zone pivot="csharp"</span></span>

11. <span data-ttu-id="07eda-168">왼쪽 탐색 창에서 **ResizeImage** 함수 이름을 선택하여 함수의 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-168">Select the **ResizeImage** function name in the left navigation to open the function's source code.</span></span>

1. <span data-ttu-id="07eda-169">썸네일을 생성하려면 함수는 **ImageResizer**라는 NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-169">The function requires a NuGet package called **ImageResizer** to generate the thumbnails.</span></span> <span data-ttu-id="07eda-170">**project.json** 파일을 사용하여 NuGet 패키지를 C# 함수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-170">NuGet packages are added to C# functions using a **project.json** file.</span></span> <span data-ttu-id="07eda-171">파일을 만들려면 오른쪽에서 **파일 보기**를 클릭하여 함수를 구성하는 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-171">To create the file, click **View Files** on the right to reveal the files that make up the function.</span></span>

1. <span data-ttu-id="07eda-172">**추가**를 클릭하여 **project.json**이라는 새 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-172">Click **Add** to add a new file named **project.json**.</span></span> <span data-ttu-id="07eda-173">파일 추가가 완료되면 **Enter 키**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-173">Press **Enter** when done to add the file.</span></span>

1. <span data-ttu-id="07eda-174">[**/csharp/ResizeImage/project.json**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) 파일의 콘텐츠를 새로 만든 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-174">Copy the contents of the [**/csharp/ResizeImage/project.json**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) file into the newly created file.</span></span> <span data-ttu-id="07eda-175">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-175">Save the file.</span></span> <span data-ttu-id="07eda-176">파일이 업데이트될 때 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-176">Packages are automatically restored when the file is updated.</span></span>

    ![ImageResizer를 포함한 project.json 파일](../media/3-project-json.png)

1. <span data-ttu-id="07eda-178">**파일 보기** 아래에서 **run.csx**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-178">Under **View Files**, select **run.csx**.</span></span> <span data-ttu-id="07eda-179">해당 콘텐츠를 [**/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx) 파일의 콘텐츠로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-179">Replace its content with the content in the [**/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx) file.</span></span>

1. <span data-ttu-id="07eda-180">[로그] 패널을 확장하려면 코드 창 아래에서 **로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-180">To expand the logs panel, click **Logs** below the code window.</span></span>

1. <span data-ttu-id="07eda-181">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-181">Click **Save**.</span></span> <span data-ttu-id="07eda-182">[로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-182">Check the Logs panel to ensure the function is successfully saved and there are no errors.</span></span>

<span data-ttu-id="07eda-183">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="07eda-183">::: zone-end</span></span>

<span data-ttu-id="07eda-184">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="07eda-184">::: zone pivot="javascript"</span></span>

14. <span data-ttu-id="07eda-185">사진 크기를 조정하려면 이 함수는 npm의 `jimp` 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-185">This function requires the `jimp` package from npm to resize the photo.</span></span> <span data-ttu-id="07eda-186">npm 패키지를 설치하려면 왼쪽 탐색 창에서 Functions 앱의 이름을 클릭하고, **플랫폼 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-186">To install the npm package, click on the Functions app name on the left navigation and click **Platform features**.</span></span>

1. <span data-ttu-id="07eda-187">**콘솔**을 클릭하여 콘솔 창을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-187">Click **Console** to reveal a console window.</span></span>

1. <span data-ttu-id="07eda-188">콘솔에서 `npm install jimp` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-188">Run the command `npm install jimp` in the console.</span></span> <span data-ttu-id="07eda-189">작업을 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-189">It may take a few minutes to complete the operation.</span></span>

1. <span data-ttu-id="07eda-190">왼쪽 탐색 창에서 **ResizeImage** 함수 이름을 클릭하여 함수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-190">Click on the **ResizeImage** function name in the left navigation to reveal the function.</span></span> <span data-ttu-id="07eda-191">**index.js** 파일의 모든 콘텐츠를 [**/javascript/ResizeImage/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js) 파일의 콘텐츠로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-191">Replace all the content in the **index.js** file with the content of the [**/javascript/ResizeImage/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js) file.</span></span>

1. <span data-ttu-id="07eda-192">[로그] 패널을 확장하려면 코드 창 아래에서 **로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-192">To expand the logs panel, click **Logs** below the code window.</span></span>

1. <span data-ttu-id="07eda-193">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-193">Click **Save**.</span></span> <span data-ttu-id="07eda-194">[로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-194">Check the Logs panel to ensure the function is successfully saved and there are no errors.</span></span>

<span data-ttu-id="07eda-195">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="07eda-195">::: zone-end</span></span>

## <a name="test-the-serverless-function"></a><span data-ttu-id="07eda-196">서버리스 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="07eda-196">Test the serverless function</span></span>

1. <span data-ttu-id="07eda-197">브라우저에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-197">Open the application in a browser.</span></span> <span data-ttu-id="07eda-198">이미지 파일을 선택하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-198">Select an image file and upload it.</span></span> <span data-ttu-id="07eda-199">업로드가 완료되지만 아직 이미지를 표시하는 기능을 추가하지 않았으므로 앱은 업로드한 사진을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-199">The upload completes, but because we haven't added the ability to display images yet, the app doesn't show the uploaded photo.</span></span>

1. <span data-ttu-id="07eda-200">Cloud Shell에서 이미지를 **images** 컨테이너로 업로드했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-200">In Cloud Shell, confirm the image was uploaded to the **images** container.</span></span>

    ```azurecli
    az storage blob list \
        --account-name <storage account name> \
        -c images \
        -o table
    ```

1. <span data-ttu-id="07eda-201">**thumbnails**라는 컨테이너에서 썸네일이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-201">Confirm the thumbnail was created in a container named **thumbnails**.</span></span>

    ```azurecli
    az storage blob list \
        --account-name <storage account name> \
        -c thumbnails \
        -o table
    ```

1. <span data-ttu-id="07eda-202">썸네일의 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-202">Get the URL for the thumbnail.</span></span>

    ```azurecli
    az storage blob url \
        --account-name <storage account name> \
        -c thumbnails \
        -n <filename> \
        --output tsv
    ```

    <span data-ttu-id="07eda-203">브라우저에서 URL을 열고 썸네일이 제대로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-203">Open the URL in a browser and confirm the thumbnail was properly created.</span></span>

1. <span data-ttu-id="07eda-204">다음 단원을 계속하기 전에 **images** 및 **thumbnails** 컨테이너에서 모든 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-204">Before continuing to the next unit, delete all files in the **images** and **thumbnails** containers.</span></span>

    ```azurecli
    az storage blob delete-batch \
        -s images \
        --account-name <storage account name>
    ```

    ```azurecli
    az storage blob delete-batch \
        -s thumbnails \
        --account-name <storage account name>
    ```

## <a name="summary"></a><span data-ttu-id="07eda-205">요약</span><span class="sxs-lookup"><span data-stu-id="07eda-205">Summary</span></span>

<span data-ttu-id="07eda-206">이 단원에서는 이미지를 Blob Storage 컨테이너에 업로드할 때마다 썸네일을 만드는 서버리스 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-206">In this unit, you created a serverless function to create a thumbnail when an image is uploaded to a Blob storage container.</span></span> <span data-ttu-id="07eda-207">다음으로, Azure Cosmos DB를 사용하여 이미지 메타데이터를 저장하고 나열하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07eda-207">Next, you will learn how to use Azure Cosmos DB to store and list image metadata.</span></span>