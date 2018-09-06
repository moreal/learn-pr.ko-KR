<span data-ttu-id="3ae8c-101">Azure App Service 인증을 사용하면 Azure Functions 앱에서 턴키 인증을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-101">Azure App Service authentication enables turn-key authentication support in an Azure Functions app.</span></span> <span data-ttu-id="3ae8c-102">Facebook, Twitter, Microsoft 계정, Google 및 Azure Active Directory와 원활하게 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-102">It integrates seamlessly with Facebook, Twitter, Microsoft accounts, Google, and Azure Active Directory.</span></span> <span data-ttu-id="3ae8c-103">App Service 인증을 추가하여 웹앱의 백 엔드 API를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-103">You'll add App Service authentication to protect the back-end APIs of your web app.</span></span>

## <a name="enable-app-service-authentication"></a><span data-ttu-id="3ae8c-104">App Service 인증을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3ae8c-104">Enable App Service authentication</span></span>

1. <span data-ttu-id="3ae8c-105">Azure Portal에서 함수 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-105">Open the function app in the Azure portal.</span></span>

1. <span data-ttu-id="3ae8c-106">**플랫폼 기능** 아래에서 **인증/권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-106">Under **Platform features**, select **Authentication/Authorization**.</span></span>

    ![인증 및 권한 부여 선택](../media/6-authorization.jpg)


1. <span data-ttu-id="3ae8c-108">다음 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-108">Select the following values:</span></span>
    
    | <span data-ttu-id="3ae8c-109">설정</span><span class="sxs-lookup"><span data-stu-id="3ae8c-109">Setting</span></span>      |  <span data-ttu-id="3ae8c-110">제안 값</span><span class="sxs-lookup"><span data-stu-id="3ae8c-110">Suggested value</span></span>   | <span data-ttu-id="3ae8c-111">설명</span><span class="sxs-lookup"><span data-stu-id="3ae8c-111">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="3ae8c-112">**App Service 인증**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-112">**App Service Authentication**</span></span> | <span data-ttu-id="3ae8c-113">다른</span><span class="sxs-lookup"><span data-stu-id="3ae8c-113">On</span></span> | <span data-ttu-id="3ae8c-114">인증을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-114">Enable authentication.</span></span> |
    | <span data-ttu-id="3ae8c-115">**요청이 인증되지 않은 경우 작업**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-115">**Action when request is not authenticated**</span></span> | <span data-ttu-id="3ae8c-116">Azure Active Directory로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-116">Sign in with Azure Active Directory.</span></span> | <span data-ttu-id="3ae8c-117">구성된 인증 방법을 선택합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="3ae8c-117">Select a configured authentication method (See below).</span></span> |
    | <span data-ttu-id="3ae8c-118">**인증 공급자**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-118">**Authentication Providers**</span></span> | <span data-ttu-id="3ae8c-119">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-119">See below.</span></span> | <span data-ttu-id="3ae8c-120">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-120">See below.</span></span> |
    | <span data-ttu-id="3ae8c-121">**토큰 저장소**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-121">**Token store**</span></span> | <span data-ttu-id="3ae8c-122">다른</span><span class="sxs-lookup"><span data-stu-id="3ae8c-122">On</span></span> | <span data-ttu-id="3ae8c-123">App Service가 토큰을 저장하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-123">Allow App Service to store and manage tokens.</span></span> |
    | <span data-ttu-id="3ae8c-124">**허용되는 외부 리디렉션 URL**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-124">**Allowed external redirect URLs**</span></span> | <span data-ttu-id="3ae8c-125">응용 프로그램의 URL(예: https://firstserverlessweb.z4.web.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="3ae8c-125">The URL of your application, for example https://firstserverlessweb.z4.web.core.windows.net/.</span></span> | <span data-ttu-id="3ae8c-126">사용자가 인증된 후에 App Service가 리디렉션할 수 있는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-126">URLs that App Service is allowed to redirect to, after a user is authenticated.</span></span> |

1. <span data-ttu-id="3ae8c-127">**Azure Active Directory**를 선택하여 **Azure Active Directory 설정**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-127">Select **Azure Active Directory** to reveal **Azure Active Directory Settings**.</span></span>

    1. <span data-ttu-id="3ae8c-128">**Express**를 **관리 모드**로 선택하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-128">Select **Express** as the **Management Mode** and fill in the following information.</span></span>
    
        | <span data-ttu-id="3ae8c-129">설정</span><span class="sxs-lookup"><span data-stu-id="3ae8c-129">Setting</span></span>      |  <span data-ttu-id="3ae8c-130">제안 값</span><span class="sxs-lookup"><span data-stu-id="3ae8c-130">Suggested value</span></span>   | <span data-ttu-id="3ae8c-131">설명</span><span class="sxs-lookup"><span data-stu-id="3ae8c-131">Description</span></span>                                        |
        | --- | --- | ---|
        | <span data-ttu-id="3ae8c-132">**관리 모드**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-132">**Management mode**</span></span> | <span data-ttu-id="3ae8c-133">Express, 새 AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3ae8c-133">Express, Create new AD app</span></span> | <span data-ttu-id="3ae8c-134">서비스 주체 및 Azure Active Directory 인증을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-134">Automatically set up a service principal and Azure Active Directory authentication.</span></span> |
        | <span data-ttu-id="3ae8c-135">**앱 만들기**</span><span class="sxs-lookup"><span data-stu-id="3ae8c-135">**Create app**</span></span> | <span data-ttu-id="3ae8c-136">my-serverless-webapp</span><span class="sxs-lookup"><span data-stu-id="3ae8c-136">my-serverless-webapp</span></span> | <span data-ttu-id="3ae8c-137">고유한 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-137">Enter a unique application name.</span></span> |
    
    1. <span data-ttu-id="3ae8c-138">**확인**을 클릭하여 Azure Active Directory 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-138">Click **OK** to save the Azure Active Directory settings.</span></span>

    ![인증/권한 부여 및 Azure Active Directory 설정](../media/6-create-aad.png)


1. <span data-ttu-id="3ae8c-140">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-140">Click **Save**.</span></span>


## <a name="modify-the-web-app-to-enable-authentication"></a><span data-ttu-id="3ae8c-141">인증을 사용하도록 웹앱 수정</span><span class="sxs-lookup"><span data-stu-id="3ae8c-141">Modify the web app to enable authentication</span></span>

1. <span data-ttu-id="3ae8c-142">Cloud Shell에서 현재 디렉터리가 **www/dist** 폴더인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-142">In Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="3ae8c-143">함수 앱에서 인증을 사용하려면 다음 코드 줄을 **settings.js** 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-143">To enable authentication in your function app, append the following line of code to the **settings.js** file:</span></span>

    `window.authEnabled = true`

    <span data-ttu-id="3ae8c-144">다음 명령을 사용하거나 VIM과 같은 명령줄 편집기를 사용하여 결과를 변경하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-144">Make the change and view the result by using the following commands, or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.authEnabled = true" >> settings.js
    ```

    <span data-ttu-id="3ae8c-145">파일의 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-145">Confirm that the change was made to the file.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="3ae8c-146">Blob Storage에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-146">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-application"></a><span data-ttu-id="3ae8c-147">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="3ae8c-147">Test the application</span></span>

1. <span data-ttu-id="3ae8c-148">브라우저에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-148">Open the application in a browser.</span></span> <span data-ttu-id="3ae8c-149">**로그인**을 클릭하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-149">Click **Log in** and log in.</span></span>

1. <span data-ttu-id="3ae8c-150">이미지 파일을 선택하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-150">Select an image file and upload it.</span></span>

    ![로그인 페이지](../media/6-aad-auth.png)
    

## <a name="summary"></a><span data-ttu-id="3ae8c-152">요약</span><span class="sxs-lookup"><span data-stu-id="3ae8c-152">Summary</span></span>

<span data-ttu-id="3ae8c-153">이 단원에서는 Azure App Service 인증을 사용하여 응용 프로그램에 인증을 추가하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae8c-153">In this unit, you learned how to add authentication to the application using Azure App Service authentication.</span></span>