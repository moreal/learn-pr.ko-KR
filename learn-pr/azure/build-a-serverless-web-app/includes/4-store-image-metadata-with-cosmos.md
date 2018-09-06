<span data-ttu-id="59d64-101">Azure Cosmos DB는 서버를 사용하지 않는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-101">Azure Cosmos DB is Microsoft's serverless, globally distributed, multi-model database.</span></span> <span data-ttu-id="59d64-102">이 모듈에서는 Azure Functions를 사용하여 Azure Cosmos DB에서 JSON 문서로 이미지 메타데이터를 저장하고 검색하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-102">In this module, you learn how to use Azure Functions to store and retrieve image metadata as JSON documents in Azure Cosmos DB.</span></span>

## <a name="create-an-azure-cosmos-db-account-database-and-collection"></a><span data-ttu-id="59d64-103">Azure Cosmos DB 계정, 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="59d64-103">Create an Azure Cosmos DB account, database, and collection</span></span>

<span data-ttu-id="59d64-104">Azure Cosmos DB 계정은 Azure Cosmos DB 데이터베이스를 포함하는 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-104">An Azure Cosmos DB account is an Azure resource that contains Azure Cosmos DB databases.</span></span>

1. <span data-ttu-id="59d64-105">Cloud Shell에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-105">Ensure you're still signed into Cloud Shell.</span></span> <span data-ttu-id="59d64-106">그러지 않은 경우 **포커스 모드로 전환**을 선택하여 Cloud Shell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-106">If you aren't, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="59d64-107">이 자습서의 다른 리소스와 동일한 리소스 그룹에서 고유한 이름을 사용하여 Azure Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-107">Create an Azure Cosmos DB account with a unique name in the same resource group as the other resources in this tutorial.</span></span>

    ```azurecli
    az cosmosdb create -g first-serverless-app -n <cosmos db account name>
    ```

1. <span data-ttu-id="59d64-108">Azure Cosmos DB 계정을 만든 후에 계정에서 **imagesdb**라는 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-108">After the Azure Cosmos DB account is created, create a new database named **imagesdb** in the account.</span></span>

    ```azurecli
    az cosmosdb database create -g first-serverless-app -n <cosmos db account name> --db-name imagesdb
    ```

1. <span data-ttu-id="59d64-109">데이터베이스를 만든 후에 데이터베이스에서 400RU(요청 단위)의 처리량을 가진 **images**라는 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-109">After the database is created, create a new collection named **images** in the database with a throughput of 400 request units (RUs).</span></span>

    ```azurecli
    az cosmosdb collection create -g first-serverless-app -n <cosmos db account name> --db-name imagesdb --collection-name images --throughput 400
    ```


## <a name="save-a-document-to-azure-cosmos-db-when-a-thumbnail-is-created"></a><span data-ttu-id="59d64-110">썸네일을 만들 때 Azure Cosmos DB에 문서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-110">Save a document to Azure Cosmos DB when a thumbnail is created</span></span>

<span data-ttu-id="59d64-111">Azure Cosmos DB 출력 바인딩을 통해 Azure Functions의 Azure Cosmos DB 컬렉션에서 문서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-111">The Azure Cosmos DB output binding lets you create documents in an Azure Cosmos DB collection from Azure Functions.</span></span> <span data-ttu-id="59d64-112">다음 단계에서는 **ResizeImage** 함수에서 Azure Cosmos DB 출력 바인딩을 구성하고, 저장할 문서(개체)를 반환하도록 함수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-112">In the following steps, you configure an Azure Cosmos DB output binding in the **ResizeImage** function and modify the function to return a document (object) to be saved.</span></span>

1. <span data-ttu-id="59d64-113">Azure Portal에서 함수 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-113">Open the function app in the Azure portal.</span></span>

1. <span data-ttu-id="59d64-114">왼쪽 탐색에서 **ResizeImage** 함수를 확장한 다음, **통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-114">In the left navigation, expand the **ResizeImage** function, and then select **Integrate**.</span></span>

1. <span data-ttu-id="59d64-115">**출력**에서 **새 출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-115">Under **Outputs**, click **New Output**.</span></span>

1. <span data-ttu-id="59d64-116">**Azure Cosmos DB** 항목을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-116">Find the **Azure Cosmos DB** item and select it.</span></span> <span data-ttu-id="59d64-117">그런 다음, **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-117">Then click **Select**.</span></span>

    ![새 출력 선택](../media/4-new-output.jpg)

1. <span data-ttu-id="59d64-119">다음 값으로 **Azure Cosmos DB 출력** 아래에 있는 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-119">Fill out the fields under **Azure Cosmos DB output** with the following values.</span></span>

    | <span data-ttu-id="59d64-120">설정</span><span class="sxs-lookup"><span data-stu-id="59d64-120">Setting</span></span>      |  <span data-ttu-id="59d64-121">제안 값</span><span class="sxs-lookup"><span data-stu-id="59d64-121">Suggested value</span></span>   | <span data-ttu-id="59d64-122">설명</span><span class="sxs-lookup"><span data-stu-id="59d64-122">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="59d64-123">**문서 매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="59d64-123">**Document parameter name**</span></span> | <span data-ttu-id="59d64-124">**함수 반환 값 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-124">Select **Use function return value**.</span></span> | <span data-ttu-id="59d64-125">상자의 값은 자동으로 **$return**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-125">The value in the box is automatically set to **$return**.</span></span> |
    | <span data-ttu-id="59d64-126">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="59d64-126">**Database name**</span></span> | <span data-ttu-id="59d64-127">imagesdb</span><span class="sxs-lookup"><span data-stu-id="59d64-127">imagesdb</span></span> | <span data-ttu-id="59d64-128">사용자가 만든 데이터베이스의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-128">Use the name of the database that you created.</span></span> |
    | <span data-ttu-id="59d64-129">**컬렉션 이름**</span><span class="sxs-lookup"><span data-stu-id="59d64-129">**Collection name**</span></span> | <span data-ttu-id="59d64-130">images</span><span class="sxs-lookup"><span data-stu-id="59d64-130">images</span></span> | <span data-ttu-id="59d64-131">사용자가 만든 컬렉션의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-131">Use the name of the collection that you created.</span></span> |

1. <span data-ttu-id="59d64-132">**Azure Cosmos DB 계정 연결** 옆에 있는 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-132">Next to **Azure Cosmos DB account connection**, click **new**.</span></span> <span data-ttu-id="59d64-133">이전에 만든 Azure Cosmos DB 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-133">Select the Azure Cosmos DB account that you previously created.</span></span>

    ![Azure Cosmos DB 출력 바인딩에 대한 설정 입력](../media/4-cosmos-db-output.png)

1. <span data-ttu-id="59d64-135">**저장**을 클릭하여 Azure Cosmos DB 출력 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-135">Click **Save** to create the Azure Cosmos DB output binding.</span></span>

1. <span data-ttu-id="59d64-136">왼쪽에서 **ResizeImage** 함수 이름을 클릭하여 함수를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-136">Click on the **ResizeImage** function name on the left to open the function.</span></span>

1. <span data-ttu-id="59d64-137">**C#**</span><span class="sxs-lookup"><span data-stu-id="59d64-137">**C#**</span></span>

    1. <span data-ttu-id="59d64-138">(C#) 함수의 반환 형식을 **void**에서 **object**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-138">(C#) Change the return type of the function from **void** to **object**.</span></span>

    1. <span data-ttu-id="59d64-139">(C#) 함수 끝에서 다음 코드 블록을 추가하여 저장할 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-139">(C#) At the end of the function, add the following code block to return the document to be saved:</span></span>
    
        ```csharp
        return new {
            id = name,
            imgPath = "/images/" + name,
            thumbnailPath = "/thumbnails/" + name
        };
        ```
    
        ![수정 후 ResizeImages 함수의 run.csx](../media/4-update-function.png)

1. <span data-ttu-id="59d64-141">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="59d64-141">**JavaScript**</span></span>

    <span data-ttu-id="59d64-142">(JavaScript) `else` 절에서 `context.done()` 문을 변경하여 Azure Cosmos DB에 저장할 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-142">(JavaScript) Change the `context.done()` statement in the `else` clause to return the document to be saved to Azure Cosmos DB.</span></span>

    ```javascript
    if (error) {
        context.done(error);
    } else {
        context.bindings.thumbnail = stream;
        context.done(null, {
            id: context.bindingData.name,
            imgPath: "/images/" + context.bindingData.name,
            thumbnailPath: "/thumbnails/" + context.bindingData.name
        });
    }
    ```

1. <span data-ttu-id="59d64-143">코드 창 아래에서 **로그**를 클릭하여 [로그] 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-143">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="59d64-144">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-144">Click **Save**.</span></span> <span data-ttu-id="59d64-145">[로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-145">Check the logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="create-a-function-to-list-images-from-azure-cosmos-db"></a><span data-ttu-id="59d64-146">Azure Cosmos DB에서 이미지를 나열하는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="59d64-146">Create a function to list images from Azure Cosmos DB</span></span>

<span data-ttu-id="59d64-147">Azure Cosmos DB에서 이미지 메타데이터를 검색하기 위해 웹 응용 프로그램에는 API가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-147">The web application requires an API to retrieve image metadata from Azure Cosmos DB.</span></span> <span data-ttu-id="59d64-148">다음 단계에서는 Azure Cosmos DB 입력 바인딩을 사용하는 HTTP 트리거 함수를 만들어서 데이터베이스 컬렉션을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-148">In the following steps, you create an HTTP-triggered function that uses an Azure Cosmos DB input binding to query the database collection.</span></span>

1. <span data-ttu-id="59d64-149">함수 앱에서 왼쪽에 있는 **함수**를 가리키고 더하기 기호(+)를 클릭하여 새 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-149">In your function app, point to **Functions** on the left and click the plus sign (+) to create a new function.</span></span>

1. <span data-ttu-id="59d64-150">**HttpTrigger** 템플릿을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-150">Find the **HttpTrigger** template and select it.</span></span>

1. <span data-ttu-id="59d64-151">이러한 값을 사용하여 이미지 가져오기 URL을 생성하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-151">Use these values to create a function that generates a get images URL:</span></span>

    | <span data-ttu-id="59d64-152">설정</span><span class="sxs-lookup"><span data-stu-id="59d64-152">Setting</span></span>      |  <span data-ttu-id="59d64-153">제안 값</span><span class="sxs-lookup"><span data-stu-id="59d64-153">Suggested value</span></span>   | <span data-ttu-id="59d64-154">설명</span><span class="sxs-lookup"><span data-stu-id="59d64-154">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="59d64-155">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="59d64-155">**Name your function**</span></span> | <span data-ttu-id="59d64-156">GetImages</span><span class="sxs-lookup"><span data-stu-id="59d64-156">GetImages</span></span> | <span data-ttu-id="59d64-157">응용 프로그램이 함수를 검색할 수 있도록 표시된 대로 이 이름을 정확히 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-157">Enter this name exactly as shown, so the application can discover the function.</span></span> |
    | <span data-ttu-id="59d64-158">**권한 부여 수준**</span><span class="sxs-lookup"><span data-stu-id="59d64-158">**Authorization level**</span></span> | <span data-ttu-id="59d64-159">익명</span><span class="sxs-lookup"><span data-stu-id="59d64-159">Anonymous</span></span> | <span data-ttu-id="59d64-160">함수가 공개적으로 액세스될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-160">Allow the function to be accessed publicly.</span></span> |

1. <span data-ttu-id="59d64-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-161">Click **Create**.</span></span>

1. <span data-ttu-id="59d64-162">새 함수를 만들면 왼쪽 탐색에 있는 함수의 이름에서 **통합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-162">When the new function is created, click **Integrate** under the function name on the left navigation.</span></span>

1. <span data-ttu-id="59d64-163">**새 입력**을 클릭하고 **Azure Cosmos DB**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-163">Click **New Input** and select **Azure Cosmos DB**.</span></span> 

    ![새 입력 선택](../media/4-new-input.jpg)

1. <span data-ttu-id="59d64-165">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-165">Click **Select**.</span></span>

1. <span data-ttu-id="59d64-166">다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-166">Fill out the following values:</span></span>

    | <span data-ttu-id="59d64-167">설정</span><span class="sxs-lookup"><span data-stu-id="59d64-167">Setting</span></span>      |  <span data-ttu-id="59d64-168">제안 값</span><span class="sxs-lookup"><span data-stu-id="59d64-168">Suggested value</span></span>   | <span data-ttu-id="59d64-169">설명</span><span class="sxs-lookup"><span data-stu-id="59d64-169">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="59d64-170">**문서 매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="59d64-170">**Document parameter name**</span></span> | <span data-ttu-id="59d64-171">documents</span><span class="sxs-lookup"><span data-stu-id="59d64-171">documents</span></span> | <span data-ttu-id="59d64-172">함수에서 매개 변수 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-172">Matches the parameter name in the function.</span></span> |
    | <span data-ttu-id="59d64-173">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="59d64-173">**Database name**</span></span> | <span data-ttu-id="59d64-174">imagesdb</span><span class="sxs-lookup"><span data-stu-id="59d64-174">imagesdb</span></span> |  |
    | <span data-ttu-id="59d64-175">**컬렉션 이름**</span><span class="sxs-lookup"><span data-stu-id="59d64-175">**Collection name**</span></span> | <span data-ttu-id="59d64-176">images</span><span class="sxs-lookup"><span data-stu-id="59d64-176">images</span></span> |  |
    | <span data-ttu-id="59d64-177">**SQL 쿼리**</span><span class="sxs-lookup"><span data-stu-id="59d64-177">**SQL query**</span></span> | <span data-ttu-id="59d64-178">select \* from c order by c._ts desc</span><span class="sxs-lookup"><span data-stu-id="59d64-178">select \* from c order by c._ts desc</span></span> | <span data-ttu-id="59d64-179">먼저 최신 문서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-179">Get documents, latest documents first.</span></span> |
    | <span data-ttu-id="59d64-180">**Azure Cosmos DB 계정 연결**</span><span class="sxs-lookup"><span data-stu-id="59d64-180">**Azure Cosmos DB account connection**</span></span> | <span data-ttu-id="59d64-181">기존 연결 문자열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-181">Select existing the connection string.</span></span> |  |

1. <span data-ttu-id="59d64-182">**저장**을 클릭하여 입력 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-182">Click **Save** to create the input binding.</span></span>

1. <span data-ttu-id="59d64-183">**C#**</span><span class="sxs-lookup"><span data-stu-id="59d64-183">**C#**</span></span>

    <span data-ttu-id="59d64-184">함수 이름을 클릭하여 코드 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-184">Click the function name to open the code window.</span></span> <span data-ttu-id="59d64-185">**run.csx** 파일의 모든 내용을 [**/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx) 파일의 콘텐츠로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-185">Replace all of the **run.csx** file with the content in the [**/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx) file.</span></span>

1. <span data-ttu-id="59d64-186">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="59d64-186">**JavaScript**</span></span>

    <span data-ttu-id="59d64-187">함수 이름을 클릭하여 코드 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-187">Click the function name to open the code window.</span></span> <span data-ttu-id="59d64-188">**index.js** 파일의 모든 내용을 [**/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js) 파일의 콘텐츠로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-188">Replace all of the **index.js** file with the content in the [**/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js) file.</span></span>

1. <span data-ttu-id="59d64-189">코드 창 아래에서 **로그**를 클릭하여 [로그] 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-189">Click **Logs** below the code window to expand the Logs panel.</span></span>

1. <span data-ttu-id="59d64-190">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-190">Click **Save**.</span></span> <span data-ttu-id="59d64-191">[로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-191">Check the Logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-application"></a><span data-ttu-id="59d64-192">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="59d64-192">Test the application</span></span>

1. <span data-ttu-id="59d64-193">브라우저에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-193">Open the application in a browser.</span></span> <span data-ttu-id="59d64-194">이미지 파일을 선택하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-194">Select an image file and upload it.</span></span>

1. <span data-ttu-id="59d64-195">몇 초 후에 새 이미지의 썸네일이 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-195">After a few seconds, the thumbnail of the new image appears on the page.</span></span>

1. <span data-ttu-id="59d64-196">Azure Portal에서 **검색** 상자를 사용하여 이름으로 Azure Cosmos DB 계정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-196">In the Azure portal, use the **Search** box to search for your Azure Cosmos DB account by name.</span></span> <span data-ttu-id="59d64-197">이름을 클릭하여 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-197">Click on the name to open the account.</span></span>

1. <span data-ttu-id="59d64-198">왼쪽에서 **데이터 탐색기**를 클릭하여 컬렉션 및 문서를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-198">Click **Data Explorer** on the left to browse collections and documents.</span></span>

1. <span data-ttu-id="59d64-199">**imagesdb** 데이터베이스 아래에서 **images** 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-199">Under the **imagesdb** database, select the **images** collection.</span></span>

1. <span data-ttu-id="59d64-200">업로드된 이미지에 대한 문서가 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-200">Confirm that a document was created for the uploaded image.</span></span>

    ![업로드된 이미지에 대한 문서를 표시하는 데이터 탐색기](../media/4-data-explorer.png)



## <a name="summary"></a><span data-ttu-id="59d64-202">요약</span><span class="sxs-lookup"><span data-stu-id="59d64-202">Summary</span></span>

<span data-ttu-id="59d64-203">이 단원에서는 Azure Cosmos DB 계정, 데이터베이스 및 컬렉션을 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-203">In this unit, you learned how to create an Azure Cosmos DB account, database, and collection.</span></span> <span data-ttu-id="59d64-204">Azure Cosmos DB 바인딩을 사용하여 Azure Cosmos DB 컬렉션에서 이미지 메타데이터를 저장하고 검색하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-204">You also learned how to use the Azure Cosmos DB bindings to save and retrieve image metadata in the Azure Cosmos DB collection.</span></span> <span data-ttu-id="59d64-205">다음으로, Microsoft Cognitive Services를 사용하여 각 업로드된 이미지에 대한 캡션을 자동으로 생성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59d64-205">Next, you learn how to automatically generate a caption for each uploaded image using Microsoft Cognitive Services.</span></span>