### <a name="exercise-1-create-a-custom-vision-service-project"></a><span data-ttu-id="5a607-101">연습 1: Custom Vision Service 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5a607-101">Exercise 1: Create a Custom Vision Service project</span></span>

<span data-ttu-id="5a607-102">Custom Vision Service로 이미지 분류 모델을 빌드하는 첫 번째 단계는 프로젝트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-102">The first step in building an image-classification model with the Custom Vision Service is to create a project.</span></span> <span data-ttu-id="5a607-103">이 연습에서는 Custom Vision Service 포털을 사용하여 Custom Vision Service 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-103">In this exercise, you will use the Custom Vision Service portal to create a Custom Vision Service project.</span></span>

1. <span data-ttu-id="5a607-104">브라우저에서 [Custom Vision Service 포털](https://www.customvision.ai/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-104">Open the [Custom Vision Service portal](https://www.customvision.ai/) in your browser.</span></span> <span data-ttu-id="5a607-105">그런 다음, **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-105">Then click **Sign In**.</span></span> 
 
    ![Custom Vision Service 포털에 로그인](../images/portal-sign-in.png)

    <span data-ttu-id="5a607-107">_Custom Vision Service 포털에 로그인_</span><span class="sxs-lookup"><span data-stu-id="5a607-107">_Signing in to the Custom Vision Service portal_</span></span>

1. <span data-ttu-id="5a607-108">로그인하라는 메시지가 표시되면 Microsoft 계정의 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-108">If you are asked to sign in, do so using the credentials for your Microsoft account.</span></span> <span data-ttu-id="5a607-109">이 앱에서 사용자 정보에 액세스하도록 허용할지 묻는 메시지가 표시되면 **예**를 클릭하고, 서비스 약관에 동의할지 묻는 메시지가 표시되면 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-109">If you are asked to let this app access your info, click **Yes**, and if prompted, agree to the terms of service.</span></span>

1. <span data-ttu-id="5a607-110">**새 프로젝트**를 클릭하여 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-110">Click **New Project** to create a new project.</span></span>
  
    ![Custom Vision Service 프로젝트 만들기](../images/portal-click-new-project.png)

    <span data-ttu-id="5a607-112">_Custom Vision Service 프로젝트 만들기_</span><span class="sxs-lookup"><span data-stu-id="5a607-112">_Creating a Custom Vision Service project_</span></span>

1. <span data-ttu-id="5a607-113">“새 프로젝트” 대화 상자에서 프로젝트 이름을 “Artworks”로 지정하고 도메인으로 **일반**이 선택되었는지 확인한 다음, **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-113">In the "New project" dialog, name the project "Artworks," ensure that **General** is selected as the domain, and click **Create project**.</span></span>

    > <span data-ttu-id="5a607-114">도메인은 특정 유형의 이미지에 맞게 모델을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-114">A domain optimizes a model for specific types of images.</span></span> <span data-ttu-id="5a607-115">예를 들어, 사용자의 목표가 음식 이미지를 포함된 음식 유형 또는 음식의 전통을 기준으로 분류하는 것이면 Food 도메인을 선택하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-115">For example, if your goal is to classify food images by the types of food they contain or the ethnicity of the dishes, then it might be helpful to select the Food domain.</span></span> <span data-ttu-id="5a607-116">제공된 어떤 도메인과도 일치하지 않거나 어떤 도메인을 선택할지 잘 모르는 경우 일반 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-116">For scenarios that don't match any of the offered domains, or if you are unsure of which domain to choose, select the General domain.</span></span>

    ![Custom Vision Service 프로젝트 만들기](../images/portal-create-project.png)

    <span data-ttu-id="5a607-118">_Custom Vision Service 프로젝트 만들기_</span><span class="sxs-lookup"><span data-stu-id="5a607-118">_Creating a Custom Vision Service project_</span></span>

<span data-ttu-id="5a607-119">다음 단계는 프로젝트에 이미지를 업로드하고 해당 이미지에 태그를 할당하는 분류하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a607-119">The next step is to upload images to the project and assign tags to those images to classify them.</span></span>