<span data-ttu-id="c3485-101">성공적으로 웹앱을 만들어 Azure에 게시했지만 내용을 변경하려는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="c3485-101">You've successfully created your web app and published it to Azure, but what happens when you want to make changes?</span></span> <span data-ttu-id="c3485-102">Visual Studio는 앱이 게시되는 위치를 기억하므로 앱 업데이트 및 변경을 두 번만 클릭하면 되는 프로세스로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-102">Visual Studio will remember where the app is published, which makes updating and changing your app a two-click process.</span></span>

## <a name="explore-the-project-structure"></a><span data-ttu-id="c3485-103">프로젝트 구조 살펴보기</span><span class="sxs-lookup"><span data-stu-id="c3485-103">Explore the project structure</span></span>

<span data-ttu-id="c3485-104">Visual Studio에서 ASP.NET 웹앱을 만들었으므로 이제 웹 사이트를 편집하고 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-104">We've created an ASP.NET web app in Visual Studio, and now you will need to edit and customize your website.</span></span> <span data-ttu-id="c3485-105">Visual Studio에서 자동으로 만든 프로젝트의 구조를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-105">Let's explore the project structure to see what Visual Studio has created for us.</span></span>

### <a name="dependencies"></a><span data-ttu-id="c3485-106">종속성</span><span class="sxs-lookup"><span data-stu-id="c3485-106">Dependencies</span></span>

<span data-ttu-id="c3485-107">종속성에는 앱이 실행되도록 하는 ASP.NET 내부 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-107">Dependencies include the ASP.NET internals to get your app up and running.</span></span> <span data-ttu-id="c3485-108">특정 타사 패키지를 추가하지 않는 한, 이 폴더에서 많은 시간을 보낼 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-108">Unless you are adding specific third-party packages, you won't need to spend much time in this folder.</span></span>

### <a name="properties"></a><span data-ttu-id="c3485-109">속성</span><span class="sxs-lookup"><span data-stu-id="c3485-109">Properties</span></span>

<span data-ttu-id="c3485-110">속성 폴더에는 웹앱을 호스트하는 위치에 대한 구성 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-110">The properties folder contains configuration data for where you are hosting your web app.</span></span> <span data-ttu-id="c3485-111">지금 **PublishProfiles** 폴더를 확장하면 Alpine Ski Hill 사이트 URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-111">If you expand the **PublishProfiles** folder now, you should see the URL for the Alpine Ski Hill site.</span></span> <span data-ttu-id="c3485-112">각 게시 프로필은 Visual Studio가 파일을 업로드하는 데 사용하는 Azure 주소와 같은 게시 구성 정보가 포함된 .xml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-112">Each publishing profile is an .xml file containing publishing configuration information such as the Azure address that Visual Studio uses to upload your files.</span></span>

### <a name="wwwroot"></a><span data-ttu-id="c3485-113">wwwroot</span><span class="sxs-lookup"><span data-stu-id="c3485-113">wwwroot</span></span>

<span data-ttu-id="c3485-114">wwwroot 파일에는 .css, .js, 이미지 및 .lib 파일과 같은 사이트의 모든 정적 자산이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-114">The wwwroot file contains all of your static assets for your site, such as the .css, .js, images, and .lib files.</span></span> <span data-ttu-id="c3485-115">사이트 스타일을 지정하고 기능을 더 추가할 준비가 되면 여기에서 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-115">When you are ready to style and add more functionality to your site, you will work in here.</span></span>

### <a name="pages"></a><span data-ttu-id="c3485-116">페이지</span><span class="sxs-lookup"><span data-stu-id="c3485-116">Pages</span></span>

<span data-ttu-id="c3485-117">**Pages** 폴더에는 사이트 페이지에 사용할 _**Razor**_ 템플릿이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-117">The **Pages** folder includes _**Razor**_ templates for the pages of your site.</span></span>
<span data-ttu-id="c3485-118">Razor는 HTML을 기반으로 빌드되었으며 사이트에서 데이터를 표시하고 논리를 실행하는 데 사용되는 특별한 규칙이 포함되어 있는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-118">Razor is a syntax that is built up around HTML, which has special conventions for displaying data and executing logic on your site.</span></span>

<span data-ttu-id="c3485-119">사이트의 각 페이지는 두 개의 코드 파일로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-119">Each page in your site is represented with two code files:</span></span>

- <span data-ttu-id="c3485-120">첫 번째는 Razor 태그 파일인 `.cshtml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-120">The first is a `.cshtml` file, which is the Razor markup file.</span></span> <span data-ttu-id="c3485-121">이 파일에는 표시 HTML과 일부 C# 논리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-121">This file includes your display HTML and some C# logic.</span></span>

- <span data-ttu-id="c3485-122">두 번째 파일은 `.cs` 파일로, `PageModel` 클래스가 포함된 C# 코드 숨김 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-122">The second file is is a `.cs` file, which is the C# code-behind that includes `PageModel` class.</span></span> <span data-ttu-id="c3485-123">이 파일을 사용하면 HTTP 요청을 가로채고 해당 요청에 대한 일부 처리를 수행한 후 Razor 파일로 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-123">This file allows you to intercept HTTP requests and do some processing on that request before passing off any data to the Razor file.</span></span>

### <a name="appsettingjson"></a><span data-ttu-id="c3485-124">appsetting.json</span><span class="sxs-lookup"><span data-stu-id="c3485-124">appsetting.json</span></span>

<span data-ttu-id="c3485-125">ASP.NET용 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-125">This is a configuration file for ASP.NET.</span></span>

### <a name="bundleconfigjson"></a><span data-ttu-id="c3485-126">bundleconfig.json</span><span class="sxs-lookup"><span data-stu-id="c3485-126">bundleconfig.json</span></span>

<span data-ttu-id="c3485-127">bundleconfig.json은 사전 처리 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-127">The bundleconfig.json is preprocessing configuration.</span></span> <span data-ttu-id="c3485-128">이 파일은 .css 및 .js 파일이 게시될 때 크기를 더 작게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-128">This file is making your .css and .js files smaller when they are published.</span></span>

### <a name="programcs-and-startupcs"></a><span data-ttu-id="c3485-129">Program.cs 및 Startup.cs</span><span class="sxs-lookup"><span data-stu-id="c3485-129">Program.cs and Startup.cs</span></span>

<span data-ttu-id="c3485-130">Program.cs 및 Startup.cs는 사이트의 웹 호스트를 구성하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-130">Program.cs and Startup.cs configure and launch your web host for your site.</span></span>

## <a name="updating-your-website-using-razor"></a><span data-ttu-id="c3485-131">Razor를 사용하여 웹 사이트 업데이트</span><span class="sxs-lookup"><span data-stu-id="c3485-131">Updating your website using Razor</span></span>

<span data-ttu-id="c3485-132">웹 사이트에 대해 몇 가지 기본적인 변경을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-132">We will want to make some basic changes to our website.</span></span> <span data-ttu-id="c3485-133">이 작업을 수행하려면 Razor 템플릿을 활용하여 웹앱을 사용자 지정하는 방법에 대한 기본적인 이해가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-133">In order to do this, you will need to have a basic understanding of how to leverage the Razor templates to customize your web app.</span></span>

## <a name="what-is-razor"></a><span data-ttu-id="c3485-134">Razor란?</span><span class="sxs-lookup"><span data-stu-id="c3485-134">What is Razor?</span></span>

<span data-ttu-id="c3485-135">Razor는 C#을 사용하여 동적 웹 페이지를 만드는 데 사용되는 ASP.NET 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-135">Razor is an ASP.NET syntax used to create dynamic web pages with C#.</span></span> <span data-ttu-id="c3485-136">서버가 Razor 페이지를 읽으면 HTML을 렌더링하기 전에 C# 코드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-136">When a server reads a Razor page, the C# code is run before it renders the HTML.</span></span> <span data-ttu-id="c3485-137">이렇게 하면 동적 콘텐츠를 신속하게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-137">This allows you to generate dynamic content quickly.</span></span>

<span data-ttu-id="c3485-138">Razor는 `@` 지시문을 사용하여 페이지를 처리하는 방법을 ASP.NET에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-138">Razor uses `@` directives to tell ASP.NET how to process a page.</span></span>

<span data-ttu-id="c3485-139">예를 들어 `Contact.cshtml` 페이지의 코드를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-139">For example, take a look at the code in the `Contact.cshtml` page.</span></span>

```aspx-csharp
@page
@model ContactModel
@{
    ViewData["Title"] = "Contact";
}
<h2>@ViewData["Title"]</h2>
<h3>@Model.Message</h3>
...
```

<span data-ttu-id="c3485-140">예: `@page` 지시문은 이 파일을 Razor 페이지로 처리하도록 ASP.NET에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-140">For example: The `@page` directive is telling ASP.NET to process this file as a Razor page.</span></span>
<span data-ttu-id="c3485-141">`@model` 지시문은 이 Razor 페이지를 `ContactModel` C# 클래스와 연결하도록 ASP.NET에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-141">The `@model` directive is telling ASP.NET to tie this Razor page with a C# class called `ContactModel`.</span></span>

<span data-ttu-id="c3485-142">또한 Razor는 `@` 기호를 사용하여 코드와 HTML 간에 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-142">Razor also uses the `@` symbol to transition between code and HTML.</span></span>
<span data-ttu-id="c3485-143">예를 들어 위의 코드 조각을 보면 `@{ ... }`를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-143">For example, if you look at the snippet above, you'll notice `@{ ... }`.</span></span> <span data-ttu-id="c3485-144">이것이 **Razor 코드 블록**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-144">This is a **Razor code block**.</span></span> <span data-ttu-id="c3485-145">이 코드는 _실행되지만 렌더링되지 않습니다_.</span><span class="sxs-lookup"><span data-stu-id="c3485-145">It's code which is _executed but not rendered_.</span></span>

<span data-ttu-id="c3485-146">코드 명령문의 출력을 렌더링하려면 C# 식 앞에 `@`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-146">To render the output of a code statement, we use the `@` in front of a C# expression.</span></span> <span data-ttu-id="c3485-147">이에 대한 두 가지 예가 `<h2>` 및 `<h3>` 태그 위의 코드 블록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-147">We have two examples of that in the code block above in the `<h2>` and `<h3>` tags.</span></span>

## <a name="publish-your-updates"></a><span data-ttu-id="c3485-148">업데이트 게시</span><span class="sxs-lookup"><span data-stu-id="c3485-148">Publish your updates</span></span>

<span data-ttu-id="c3485-149">웹 사이트를 변경한 후에는 Azure에 게시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-149">Once you've made the changes to your website, you will want to publish them to Azure.</span></span> <span data-ttu-id="c3485-150">이 프로세스는 처음에 게시한 방법과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-150">This process is similar to how we initially published.</span></span>

1. <span data-ttu-id="c3485-151">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-151">Right-click the project in Solution Explorer.</span></span>
1. <span data-ttu-id="c3485-152">웹 사이트 이름과 웹 배포가 차례로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-152">Now you should see the name of your website followed by Web Deploy.</span></span> <span data-ttu-id="c3485-153">예를 들어 웹 사이트 이름을 AlpineSkiHouse42로 지정한 경우 사용 가능한 옵션에 **AlpineSkiHouse42 - 웹 배포**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-153">For example if you named your website AlpineSkiHouse42, you would see **AlpineSkiHouse42 - Web Deploy** in the available options.</span></span> <span data-ttu-id="c3485-154">해당 옵션을 선택하면 Azure에서 사이트가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-154">Select that and your site will update in Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="c3485-155">요약</span><span class="sxs-lookup"><span data-stu-id="c3485-155">Summary</span></span>

<span data-ttu-id="c3485-156">웹 사이트를 만들고 게시하는 것은 좋은 웹 사이트를 만드는 첫 번째 단계에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-156">Creating and publishing a website are just the first steps in creating a good website.</span></span> <span data-ttu-id="c3485-157">콘텐츠 추가를 시작하면 사이트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-157">Once you start to add content, you'll need to update your site.</span></span> <span data-ttu-id="c3485-158">처음에 사이트를 Azure에 게시한 후에는 언제든 솔루션 탐색기에서 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3485-158">Once you've initially published your site to Azure, you can update at any time from the Solution Explorer.</span></span>
