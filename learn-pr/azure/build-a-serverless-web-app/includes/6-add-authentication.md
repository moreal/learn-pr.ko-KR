<span data-ttu-id="33df1-101">Azure App Service 인증을 사용하면 Azure Functions 앱에서 턴키 인증을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-101">Azure App Service authentication enables turn-key authentication support in an Azure Functions app.</span></span> <span data-ttu-id="33df1-102">Facebook, Twitter, Microsoft 계정, Google 및 Azure Active Directory와 원활하게 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-102">It integrates seamlessly with Facebook, Twitter, Microsoft accounts, Google, and Azure Active Directory.</span></span> <span data-ttu-id="33df1-103">App Service 인증을 추가하여 웹앱의 백 엔드 API를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-103">You'll add App Service authentication to protect the back-end APIs of your web app.</span></span>

## <a name="enable-app-service-authentication"></a><span data-ttu-id="33df1-104">App Service 인증을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="33df1-104">Enable App Service authentication</span></span>

1. <span data-ttu-id="33df1-105">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-105">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="33df1-106">함수 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-106">Open the function app.</span></span>

1. <span data-ttu-id="33df1-107">**플랫폼 기능** 아래에서 **인증/권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-107">Under **Platform features**, select **Authentication/Authorization**.</span></span>

    ![인증 및 권한 부여 선택](../media/6-authorization.jpg)

1. <span data-ttu-id="33df1-109">다음 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-109">Select the following values:</span></span>

    | <span data-ttu-id="33df1-110">설정</span><span class="sxs-lookup"><span data-stu-id="33df1-110">Setting</span></span>      |  <span data-ttu-id="33df1-111">제안 값</span><span class="sxs-lookup"><span data-stu-id="33df1-111">Suggested value</span></span>   | <span data-ttu-id="33df1-112">설명</span><span class="sxs-lookup"><span data-stu-id="33df1-112">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="33df1-113">**App Service 인증**</span><span class="sxs-lookup"><span data-stu-id="33df1-113">**App Service Authentication**</span></span> | <span data-ttu-id="33df1-114">다른</span><span class="sxs-lookup"><span data-stu-id="33df1-114">On</span></span> | <span data-ttu-id="33df1-115">인증을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-115">Enable authentication.</span></span> |
    | <span data-ttu-id="33df1-116">**요청이 인증되지 않은 경우 작업**</span><span class="sxs-lookup"><span data-stu-id="33df1-116">**Action when request is not authenticated**</span></span> | <span data-ttu-id="33df1-117">Azure Active Directory로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-117">Sign in with Azure Active Directory.</span></span> | <span data-ttu-id="33df1-118">구성된 인증 방법을 선택합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="33df1-118">Select a configured authentication method (See below).</span></span> |
    | <span data-ttu-id="33df1-119">**인증 공급자**</span><span class="sxs-lookup"><span data-stu-id="33df1-119">**Authentication Providers**</span></span> | <span data-ttu-id="33df1-120">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33df1-120">See below.</span></span> | <span data-ttu-id="33df1-121">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33df1-121">See below.</span></span> |
    | <span data-ttu-id="33df1-122">**토큰 저장소**</span><span class="sxs-lookup"><span data-stu-id="33df1-122">**Token store**</span></span> | <span data-ttu-id="33df1-123">다른</span><span class="sxs-lookup"><span data-stu-id="33df1-123">On</span></span> | <span data-ttu-id="33df1-124">App Service가 토큰을 저장하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-124">Allow App Service to store and manage tokens.</span></span> |
    | <span data-ttu-id="33df1-125">**허용되는 외부 리디렉션 URL**</span><span class="sxs-lookup"><span data-stu-id="33df1-125">**Allowed external redirect URLs**</span></span> | <span data-ttu-id="33df1-126">응용 프로그램의 URL(예: https://firstserverlessweb.z4.web.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="33df1-126">The URL of your application, for example https://firstserverlessweb.z4.web.core.windows.net/.</span></span> | <span data-ttu-id="33df1-127">사용자가 인증된 후에 App Service가 리디렉션할 수 있는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-127">URLs that App Service is allowed to redirect to, after a user is authenticated.</span></span> |

1. <span data-ttu-id="33df1-128">**Azure Active Directory**를 선택하여 **Azure Active Directory 설정**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-128">Select **Azure Active Directory** to reveal **Azure Active Directory Settings**.</span></span>

    1. <span data-ttu-id="33df1-129">**Express**를 **관리 모드**로 선택하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-129">Select **Express** as the **Management Mode** and fill in the following information.</span></span>

        | <span data-ttu-id="33df1-130">설정</span><span class="sxs-lookup"><span data-stu-id="33df1-130">Setting</span></span>      |  <span data-ttu-id="33df1-131">제안 값</span><span class="sxs-lookup"><span data-stu-id="33df1-131">Suggested value</span></span>   | <span data-ttu-id="33df1-132">설명</span><span class="sxs-lookup"><span data-stu-id="33df1-132">Description</span></span>                                        |
        | --- | --- | ---|
        | <span data-ttu-id="33df1-133">**관리 모드**</span><span class="sxs-lookup"><span data-stu-id="33df1-133">**Management mode**</span></span> | <span data-ttu-id="33df1-134">Express, 새 AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="33df1-134">Express, Create new AD app</span></span> | <span data-ttu-id="33df1-135">서비스 주체 및 Azure Active Directory 인증을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-135">Automatically set up a service principal and Azure Active Directory authentication.</span></span> |
        | <span data-ttu-id="33df1-136">**앱 만들기**</span><span class="sxs-lookup"><span data-stu-id="33df1-136">**Create app**</span></span> | <span data-ttu-id="33df1-137">my-serverless-webapp</span><span class="sxs-lookup"><span data-stu-id="33df1-137">my-serverless-webapp</span></span> | <span data-ttu-id="33df1-138">고유한 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-138">Enter a unique application name.</span></span> |

    1. <span data-ttu-id="33df1-139">**확인**을 클릭하여 Azure Active Directory 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-139">Click **OK** to save the Azure Active Directory settings.</span></span>

    ![인증/권한 부여 및 Azure Active Directory 설정](../media/6-create-aad.png)

1. <span data-ttu-id="33df1-141">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-141">Click **Save**.</span></span>

## <a name="modify-the-web-app-to-enable-authentication"></a><span data-ttu-id="33df1-142">인증을 사용하도록 웹앱 수정</span><span class="sxs-lookup"><span data-stu-id="33df1-142">Modify the web app to enable authentication</span></span>

1. <span data-ttu-id="33df1-143">Cloud Shell에서 현재 디렉터리가 **www/dist** 폴더인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-143">In Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="33df1-144">**settings.js**를 수정하여 함수 앱의 인증을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-144">You enable authentication in your function app by modifying **settings.js**.</span></span> <span data-ttu-id="33df1-145">Cloud Shell 편집기에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-145">Open the file in Cloud Shell Editor.</span></span>

    ```azurecli
    code settings.js
    ```

1. <span data-ttu-id="33df1-146">다음 줄을 파일에 추가하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-146">Append the following line to the file and save it.</span></span>

    ```azurecli
    window.authEnabled = true
    ```

1. <span data-ttu-id="33df1-147">파일의 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-147">Confirm the change was made to the file.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="33df1-148">Blob Storage에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-148">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload \
        -c \$web \
        --account-name <storage account name> \
        -f settings.js \
        -n settings.js
    ```

## <a name="test-the-application"></a><span data-ttu-id="33df1-149">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="33df1-149">Test the application</span></span>

1. <span data-ttu-id="33df1-150">브라우저에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-150">Open the application in a browser.</span></span> <span data-ttu-id="33df1-151">**로그인**을 클릭하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-151">Click **Log in** and log in.</span></span>

1. <span data-ttu-id="33df1-152">이미지 파일을 선택하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-152">Select an image file and upload it.</span></span>

    ![로그인 페이지](../media/6-aad-auth.png)

## <a name="summary"></a><span data-ttu-id="33df1-154">요약</span><span class="sxs-lookup"><span data-stu-id="33df1-154">Summary</span></span>

<span data-ttu-id="33df1-155">이 단원에서는 Azure App Service 인증을 사용하여 응용 프로그램에 인증을 추가하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="33df1-155">In this unit, you learned how to add authentication to the application using Azure App Service authentication.</span></span>