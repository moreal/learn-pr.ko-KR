<span data-ttu-id="85335-101">빌드 중인 응용 프로그램은 Azure 함수와 통신하여 사용자 위치를 공유하는 플랫폼 간 모바일 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="85335-101">The application you're building is a cross-platform mobile app that talks to an Azure function to share your location.</span></span> <span data-ttu-id="85335-102">이 단원에서는 Visual Studio를 사용하여 빈 모바일 앱을 만들고 사용자의 위치를 가져오는 데 사용되는 API가 있는 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-102">In this unit, you create the blank mobile app using Visual Studio and install a NuGet package that has an API for getting the user's location.</span></span>

## <a name="create-the-xamarinforms-project"></a><span data-ttu-id="85335-103">Xamarin.Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="85335-103">Create the Xamarin.Forms project</span></span>

1. <span data-ttu-id="85335-104">Visual Studio에서 ‘파일->새로 만들기->프로젝트...’를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-104">From Visual Studio, select *File->New->Project...*.</span></span>

1. <span data-ttu-id="85335-105">왼쪽 트리에서 ‘Visual C#->플랫폼 간’을 선택하고 가운데 패널에서 ‘모바일 앱(Xamarin.Forms)’을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-105">From the tree on the left-hand side, select *Visual C#->Cross-Platform* and then select *Mobile App (Xamarin.Forms)* from the panel in the center.</span></span>

1. <span data-ttu-id="85335-106">솔루션 이름을 “ImHere”로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-106">Name the solution "ImHere".</span></span>

1. <span data-ttu-id="85335-107">솔루션에 적합한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-107">Choose an appropriate location for the solution.</span></span>

1. <span data-ttu-id="85335-108">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-108">Click **OK**.</span></span>

    ![새 솔루션 대화 상자](../media/2-new-solution-dialog.png)

1. <span data-ttu-id="85335-110">**새 플랫폼 간 앱** 대화 상자에서 ‘빈 앱’ 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-110">From the **New Cross Platform App** dialog, select the *Blank App* template.</span></span>

1. <span data-ttu-id="85335-111">이 모듈에서는 UWP 앱을 빌드하므로 iOS 및 Android는 선택을 취소하고 UWP는 선택된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="85335-111">For this module you will build a UWP app, so uncheck iOS and Android and leave UWP checked.</span></span>

1. <span data-ttu-id="85335-112">*코드 공유 전략*에 **.NET Standard**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-112">For the *Code Sharing Strategy*, select **.NET Standard**.</span></span>

1. <span data-ttu-id="85335-113">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-113">Click **OK**.</span></span>

    ![새 솔루션 구성 대화 상자](../media/2-configure-solution-dialog.png)

<span data-ttu-id="85335-115">Visual Studio에서는 두 개의 프로젝트, `ImHere.UWP`라는 UWP 앱과 .NET Standard 라이브러리 `ImHere`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85335-115">Visual Studio will create two projects for you - a UWP app called `ImHere.UWP` and a .NET Standard library, `ImHere`.</span></span> <span data-ttu-id="85335-116">Xamarin.Forms 앱은 하나 이상의 플랫폼별 앱 프로젝트와 하나 이상의 .NET Standard 라이브러리 두 부분으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85335-116">Xamarin.Forms apps are made up of two parts - one or more platform-specific app projects and one (or more) .NET Standard libraries.</span></span> <span data-ttu-id="85335-117">플랫폼별 앱 프로젝트에는 관련 플랫폼에서 앱을 실행하는 데 필요한 플랫폼별 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85335-117">The platform-specific app projects contain the platform-specific code needed to run an app on the relevant platform.</span></span> <span data-ttu-id="85335-118">그러면 이러한 프로젝트에서 플랫폼 간 .NET Standard 라이브러리에 정의된 Xamarin.Forms 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-118">These projects then launch a Xamarin.Forms app that is defined in a cross-platform .NET Standard library.</span></span> <span data-ttu-id="85335-119">앱은 플랫폼 간 코드로 빌드하고 만들어진 모든 사용자 인터페이스는 런타임 시 관련 플랫폼별 UI 구성 요소로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="85335-119">You build your app in cross-platform code and, at runtime, any user interfaces you create are translated into the relevant platform-specific UI components.</span></span>

## <a name="adding-xamarinessentials"></a><span data-ttu-id="85335-120">Xamarin.Essentials 추가</span><span class="sxs-lookup"><span data-stu-id="85335-120">Adding Xamarin.Essentials</span></span>

<span data-ttu-id="85335-121">UWP, Android 및 iOS 플랫폼은 운영 체제와 하드웨어를 활용하는 여러 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-121">The UWP, Android, and iOS platforms provide numerous similar capabilities that take advantage of the operating system and hardware.</span></span> <span data-ttu-id="85335-122">이러한 유사성에도 불구하고 API는 서로 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="85335-122">Despite these similarities, the APIs are very different.</span></span> <span data-ttu-id="85335-123">플랫폼 간 코드에서 이러한 API를 사용하려면 .NET Standard 라이브러리에 노출하는 앱 프로젝트에 플랫폼별 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-123">Using these APIs from cross-platform code requires writing platform-specific code in your app projects that you expose to your .NET Standard libraries.</span></span> <span data-ttu-id="85335-124">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true)는 이러한 API 중 다수에 대한 플랫폼 간 추상화를 지원하는 NuGet 패키지이므로 플랫폼별 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85335-124">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true) is a NuGet package that provides a cross-platform abstraction over a number of these APIs so that you don't need to write platform-specific code.</span></span> <span data-ttu-id="85335-125">여기에는 앱에서 사용자의 위치를 가져오는 데 사용할 지리적 위치 API가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="85335-125">This includes the geolocation APIs that you will use in your app to get the user's location.</span></span>

1. <span data-ttu-id="85335-126">Visual Studio 솔루션 탐색기에서 `ImHere` 솔루션(`ImHere` .NET Standard 프로젝트가 아닌 최상위 수준의 솔루션)을 마우스 오른쪽 단추로 클릭하고 *솔루션에 대한 NuGet 패키지 관리...* 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-126">Right-click on the `ImHere` solution (the top level solution, not the `ImHere` .NET Standard project) in the Visual Studio Solution Explorer and select *Manage NuGet Packages for Solution...*.</span></span>

1. <span data-ttu-id="85335-127">**찾아보기** 탭을 선택하고 “Xamarin.Essentials”를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-127">Select the **Browse** tab and search for "Xamarin.Essentials".</span></span> <span data-ttu-id="85335-128">이 패키지는 현재 시험판 NuGet 패키지로 사용할 수 있으므로 ‘시험판 포함’ 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-128">This package is currently available as a prerelease NuGet package, so check the *include prelease* box.</span></span>

    > [!TIP]
    > <span data-ttu-id="85335-129">Xamarin.Essentials NuGet 패키지가 표시되지 않는 경우 *시험판 포함*이 선택되어 있는지 다시 한 번 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-129">If you do not see the Xamarin.Essentials NuGet package, double check that *include prelease* is checked.</span></span> 

1. <span data-ttu-id="85335-130">**Xamarin.Essentials** NuGet 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-130">Select the **Xamarin.Essentials** NuGet package.</span></span>

1. <span data-ttu-id="85335-131">오른쪽 프로젝트 목록에서 모든 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-131">Check all your projects in the project list on the right-hand side.</span></span>

1. <span data-ttu-id="85335-132">**설치** 단추를 클릭하여 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-132">Click the **Install** button to install the NuGet package.</span></span> <span data-ttu-id="85335-133">계속하려면 라이선스에 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-133">You'll need to accept the license to continue.</span></span>

    ![솔루션의 모든 프로젝트에 Xamarin.Essentials NuGet 패키지 추가](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a><span data-ttu-id="85335-135">앱 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="85335-135">Building and running the app</span></span>

1. <span data-ttu-id="85335-136">솔루션 탐색기에서 `ImHere.UWP` 프로젝트를 마우스 오른쪽 단추로 클릭하고 ‘시작 프로젝트로 설정’을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-136">Right-click on the `ImHere.UWP` project in Solution Explorer and select *Set as StartUp project*.</span></span>

1. <span data-ttu-id="85335-137">빌드 구성은 **디버그**로, 플랫폼은 **x86**으로 설정하고 장치는 **로컬 머신**에서 실행되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-137">Set the build configuration to **Debug**, the platform to **x86**, and the device to run on to **Local Machine**.</span></span>

    ![디버그 x86 구성이 로컬 장치에서 실행되도록 설정](../media/2-debug-configuration.png)

1. <span data-ttu-id="85335-139">앱 디버그를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="85335-139">Start debugging the app.</span></span>

    ![실행 중인 앱](../media/2-debuging-app.png)

## <a name="summary"></a><span data-ttu-id="85335-141">요약</span><span class="sxs-lookup"><span data-stu-id="85335-141">Summary</span></span>

<span data-ttu-id="85335-142">이 단원에서는 새 Xamarin.Forms 플랫폼 간 모바일 앱을 만들고 Xamarin.Essentials NuGet 패키지를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="85335-142">In this unit, you created a new Xamarin.Forms cross-platform mobile app and added the Xamarin.Essentials NuGet package.</span></span> <span data-ttu-id="85335-143">다음에는 모바일 앱 UI 및 논리를 빌드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="85335-143">Next, you learn how to build up the mobile app UI and logic.</span></span>