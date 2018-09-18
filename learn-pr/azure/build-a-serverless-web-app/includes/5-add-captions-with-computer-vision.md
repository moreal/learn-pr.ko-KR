<span data-ttu-id="cb940-101">이 시점에서 응용 프로그램은 이미지를 업로드하고 볼 수 있는 기능 갤러리입니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-101">At this point, the application is a functional gallery that allows you to upload and view images.</span></span> <span data-ttu-id="cb940-102">이 모듈에서는 Microsoft Cognitive Services에서 Computer Vision API를 사용하여 업로드된 이미지에 대한 캡션을 생성하고 Azure Cosmos DB에서 이미지 메타데이터를 포함한 캡션을 저장하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-102">In this module, you learn how to use the Computer Vision API from Microsoft Cognitive Services to generate captions for uploaded images and save the captions with the image metadata in Azure Cosmos DB.</span></span>

## <a name="create-a-computer-vision-account"></a><span data-ttu-id="cb940-103">Computer Vision 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cb940-103">Create a Computer Vision account</span></span>

<span data-ttu-id="cb940-104">Microsoft Cognitive Services는 개발자들이 더욱 지능적인 응용 프로그램을 만들 수 있도록 제공되는 서비스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-104">Microsoft Cognitive Services is a collection of services that are available to developers to make their applications more intelligent.</span></span> <span data-ttu-id="cb940-105">Computer Vision API는 고급 알고리즘을 사용하여 이미지를 처리하고 각 이미지에 대한 정보를 반환하는 서버를 사용하지 않는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-105">The Computer Vision API is a serverless service that processes images using advanced algorithms and returns information about each image.</span></span> <span data-ttu-id="cb940-106">최대 매월 5000개의 API 호출을 제공하는 무료 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-106">It has a free tier that provides up to 5,000 API calls per month.</span></span>

1. <span data-ttu-id="cb940-107">Cloud Shell에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-107">Ensure you're still signed into Cloud Shell.</span></span> <span data-ttu-id="cb940-108">그러지 않은 경우 **포커스 모드로 전환**을 선택하여 Cloud Shell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-108">If you aren't, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="cb940-109">리소스 그룹에서 고유한 이름을 가진 **ComputerVision** 종류의 새 Cognitive Services 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-109">Create a new Cognitive Services account of type **ComputerVision** with a unique name in your resource group.</span></span> <span data-ttu-id="cb940-110">무료 계층에서 **F0**를 SKU로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-110">For the free tier, use **F0** as the SKU.</span></span> <span data-ttu-id="cb940-111">기존 Computer Vision 계정이 있는 경우 표준 계정(S1)을 만들어야 하며, 일부 비용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-111">If you already have an existing Computer Vision account, you may need to create a Standard account (S1), which may incur some costs.</span></span>

    ```azurecli
    az cognitiveservices account create -g first-serverless-app -n <computer vision account name> --kind ComputerVision --sku F0 -l westcentralus
    ```


## <a name="create-function-app-settings-for-computer-vision-url-and-key"></a><span data-ttu-id="cb940-112">Computer Vision URL 및 키에 대한 함수 앱 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="cb940-112">Create function app settings for Computer Vision URL and key</span></span>

<span data-ttu-id="cb940-113">Computer Vision API를 호출하려면 URL 및 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-113">To call the Computer Vision API, a URL and key are required.</span></span>

1. <span data-ttu-id="cb940-114">Computer Vision API 키 및 URL을 가져오고 Bash 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-114">Get the Computer Vision API key and URL and save them in Bash variables.</span></span>

    ```azurecli
    export COMP_VISION_KEY=$(az cognitiveservices account keys list -g first-serverless-app -n <computer vision account name> --query key1 --output tsv)
    ```
    ```azurecli
    export COMP_VISION_URL=$(az cognitiveservices account show -g first-serverless-app -n <computer vision account name> --query endpoint --output tsv)
    ```

1. <span data-ttu-id="cb940-115">각각 함수 앱에서 **COMP_VISION_KEY** 및 **COMP_VISION_URL**이라는 앱 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-115">Create app settings named **COMP_VISION_KEY** and **COMP_VISION_URL**, respectively, in the function app.</span></span>

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings COMP_VISION_KEY=$COMP_VISION_KEY COMP_VISION_URL=$COMP_VISION_URL -o table
    ```

## <a name="call-the-computer-vision-api-from-the-resizeimage-function"></a><span data-ttu-id="cb940-116">ResizeImage 함수에서 Computer Vision API 호출</span><span class="sxs-lookup"><span data-stu-id="cb940-116">Call the Computer Vision API from the ResizeImage function</span></span>

<span data-ttu-id="cb940-117">다음 단계에서 각 업로드된 이미지를 설명하고 설명을 Azure Cosmos DB에 저장하도록 Computer Vision API를 호출하는 **ResizeImage** 함수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-117">In the following steps, you modify the **ResizeImage** function to call the Computer Vision API to describe each uploaded image and save the description in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="cb940-118">[Azure Portal](https://portal.azure.com/?azure-portal=true)에서 함수 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-118">Open your function app in the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

<span data-ttu-id="cb940-119">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="cb940-119">::: zone pivot="csharp"</span></span>
1. <span data-ttu-id="cb940-120">(C#) 왼쪽 탐색 영역을 사용하여 **ResizeImage** 함수를 찾고 해당 코드 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-120">(C#) Using the left navigation, locate the **ResizeImage** function and open its code window.</span></span>

1. <span data-ttu-id="cb940-121">(C#) 코드를 [**/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx) 파일의 콘텐츠로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-121">(C#) Replace the code with the contents of the [**/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx) file.</span></span> <span data-ttu-id="cb940-122">이 코드는 `HttpClient`를 사용하여 Computer Vision API를 호출하고 결과를 Azure Cosmos DB에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-122">This code uses `HttpClient` to call the Computer Vision API and save its result in Azure Cosmos DB.</span></span>

<span data-ttu-id="cb940-123">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="cb940-123">::: zone-end</span></span>

<span data-ttu-id="cb940-124">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="cb940-124">::: zone pivot="javascript"</span></span>
1. <span data-ttu-id="cb940-125">(JavaScript) Computer Vision API에 대한 HTTP 호출을 수행하기 위해 이 함수에는 npm의 `axios` 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-125">(JavaScript) This function requires the `axios` package from npm to make an HTTP call to the Computer Vision API.</span></span> <span data-ttu-id="cb940-126">npm 패키지를 설치하려면 왼쪽 탐색 창에서 함수 앱의 이름을 클릭하고, **플랫폼 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-126">To install the npm package, click on the function app name on the left navigation and click **Platform features**.</span></span>

1. <span data-ttu-id="cb940-127">(JavaScript) **콘솔**을 클릭하여 콘솔 창을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-127">(JavaScript) Click **Console** to reveal a console window.</span></span>

1. <span data-ttu-id="cb940-128">(JavaScript) 콘솔에서 `npm install axios` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-128">(JavaScript) Run the command `npm install axios` in the console.</span></span> <span data-ttu-id="cb940-129">작업을 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-129">It may take a few minutes to complete the operation.</span></span>

1. <span data-ttu-id="cb940-130">(JavaScript) 왼쪽 탐색에서 함수 이름(**ResizeImage**)을 클릭하여 함수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-130">(JavaScript) Click on the function name (**ResizeImage**) in the left navigation to reveal the function.</span></span> <span data-ttu-id="cb940-131">모든 **index.js** 파일의 모든 내용을 [**/javascript/ResizeImage/index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js) 파일의 콘텐츠로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-131">Replace all of the **index.js** file with the contents of the [**/javascript/ResizeImage/index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js) file.</span></span>

<span data-ttu-id="cb940-132">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="cb940-132">::: zone-end</span></span>

1. <span data-ttu-id="cb940-133">코드 창 아래에서 **로그**를 클릭하여 [로그] 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-133">Click **Logs** below the code window to expand the Logs panel.</span></span>

1. <span data-ttu-id="cb940-134">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-134">Click **Save**.</span></span> <span data-ttu-id="cb940-135">[로그] 패널을 확인하여 함수가 성공적으로 저장되고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-135">Check the Logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-application"></a><span data-ttu-id="cb940-136">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="cb940-136">Test the application</span></span>

1. <span data-ttu-id="cb940-137">브라우저에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-137">Open the application in a browser.</span></span> 

1. <span data-ttu-id="cb940-138">이미지 파일을 선택하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-138">Select an image file and upload it.</span></span>

1. <span data-ttu-id="cb940-139">몇 초 후에 새 이미지의 썸네일이 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-139">After a few seconds, the thumbnail of the new image should appear on the page.</span></span> <span data-ttu-id="cb940-140">Computer Vision에 의해 생성된 설명을 보려면 이미지를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-140">Point to the image to see the description that's generated by Computer Vision.</span></span>

## <a name="summary"></a><span data-ttu-id="cb940-141">요약</span><span class="sxs-lookup"><span data-stu-id="cb940-141">Summary</span></span>

<span data-ttu-id="cb940-142">이 단원에서는 Microsoft Cognitive Services Computer Vision API를 사용하여 각 업로드된 이미지에 대한 캡션을 자동으로 생성하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-142">In this unit, you learned how to automatically generate captions for each uploaded image using Microsoft Cognitive Services Computer Vision API.</span></span> <span data-ttu-id="cb940-143">다음으로, Azure App Service 인증을 사용하여 응용 프로그램에 인증을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cb940-143">Next, you learn how to add authentication to the application using Azure App Service authentication.</span></span>