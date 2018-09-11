<span data-ttu-id="02c5f-101">빌드 중인 응용 프로그램은 Azure 함수와 통신하여 사용자 위치를 공유하는 플랫폼 간 모바일 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-101">The application you're building is a cross-platform mobile app that talks to an Azure function to share your location.</span></span> <span data-ttu-id="02c5f-102">이 단원에서는 Visual Studio를 사용하여 빈 모바일 앱을 만들고 사용자의 위치를 가져오는 데 사용되는 API가 있는 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-102">In this unit, you create the blank mobile app using Visual Studio and install a NuGet package that has an API for getting the user's location.</span></span>

## <a name="create-the-xamarinforms-project"></a><span data-ttu-id="02c5f-103">Xamarin.Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="02c5f-103">Create the Xamarin.Forms project</span></span>

1. <span data-ttu-id="02c5f-104">Visual Studio에서 ‘파일->새로 만들기->프로젝트...’를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-104">From Visual Studio, select *File->New->Project...*.</span></span>

2. <span data-ttu-id="02c5f-105">왼쪽 트리에서 ‘Visual C#->플랫폼 간’을 선택하고 가운데 패널에서 ‘모바일 앱(Xamarin.Forms)’을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-105">From the tree on the left-hand side, select *Visual C#->Cross-Platform* and then select *Mobile App (Xamarin.Forms)* from the panel in the center.</span></span>

3. <span data-ttu-id="02c5f-106">솔루션 이름을 “ImHere”로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-106">Name the solution "ImHere".</span></span>

4. <span data-ttu-id="02c5f-107">솔루션에 적합한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-107">Choose an appropriate location for the solution.</span></span>

    > <span data-ttu-id="02c5f-108">이 모듈을 Windows에서 로컬로 실행 중이며 Android용 빌드를 계획하고 있는 경우 경로를 가능한 한 짧게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-108">If you are running this module locally on Windows and are planning on building for Android, then make sure the path is as short as possible.</span></span> <span data-ttu-id="02c5f-109">Android SDK에는 경로 길이 제한이 있으므로 루트 경로가 가능한 한 짧아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-109">There are path length limitations with the Android SDK, so your root path should be as short as possible.</span></span>

5. <span data-ttu-id="02c5f-110">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-110">Click **OK**.</span></span>

    ![새 솔루션 대화 상자](../media-drafts/2-new-solution-dialog.png)

6. <span data-ttu-id="02c5f-112">**새 플랫폼 간 앱** 대화 상자에서 ‘빈 앱’ 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-112">From the **New Cross Platform App** dialog, select the *Blank App* template.</span></span>

7. <span data-ttu-id="02c5f-113">이 모듈에서는 UWP 앱을 빌드하므로 iOS 및 Android는 선택을 취소하고 UWP는 선택된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-113">For this module you will build a UWP app, so uncheck iOS and Android and leave UWP checked.</span></span>

    > <span data-ttu-id="02c5f-114">이 작업을 로컬에서 실행하는 경우 Android SDK가 Visual Studio 내에서 ‘.NET을 사용한 모바일 개발’ 워크로드의 일부로 설치되므로 Android를 선택한 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-114">If you are running this locally, then you can leave Android checked because the Android SDK is installed as part of the *Mobile Development With .NET* workload inside Visual Studio.</span></span> <span data-ttu-id="02c5f-115">iOS용 앱도 빌드하려면 macOS 빌드 에이전트에 페어링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-115">If you also want to build for iOS, you will need to pair to a macOS build agent.</span></span> <span data-ttu-id="02c5f-116">이에 대한 자세한 내용은 [Xamarin iOS 문서](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02c5f-116">You can read more on this in the [Xamarin iOS docs](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/).</span></span>

8. <span data-ttu-id="02c5f-117">‘코드 공유 전략’은 **.NET Standard**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-117">For the *Code Sharing Strategy*, select **.NET Standard**.</span></span>

9. <span data-ttu-id="02c5f-118">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-118">Click **OK**.</span></span>

    ![새 솔루션 구성 대화 상자](../media-drafts/2-configure-solution-dialog.png)

<span data-ttu-id="02c5f-120">Visual Studio에서는 두 개의 프로젝트, `ImHere.UWP`라는 UWP 앱과 .NET Standard 라이브러리 `ImHere`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-120">Visual Studio will create two projects for you - a UWP app called `ImHere.UWP` and a .NET standard library, `ImHere`.</span></span> <span data-ttu-id="02c5f-121">Xamarin.Forms 앱은 하나 이상의 플랫폼별 앱 프로젝트와 하나 이상의 .NET Standard 라이브러리 두 부분으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-121">Xamarin.Forms apps are made up of two parts - one or more platform-specific app projects and one (or more) .NET standard libraries.</span></span> <span data-ttu-id="02c5f-122">플랫폼별 앱 프로젝트에는 관련 플랫폼에서 앱을 실행하는 데 필요한 플랫폼별 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-122">The platform-specific app projects contain the platform-specific code needed to run an app on the relevant platform.</span></span> <span data-ttu-id="02c5f-123">그러면 이러한 프로젝트에서 플랫폼 간 .NET Standard 라이브러리에 정의된 Xamarin.Forms 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-123">These projects then launch a Xamarin.Forms app that is defined in a cross-platform .NET standard library.</span></span> <span data-ttu-id="02c5f-124">앱은 플랫폼 간 코드로 빌드하고 만들어진 모든 사용자 인터페이스는 런타임 시 관련 플랫폼별 UI 구성 요소로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-124">You build your app in cross-platform code and, at runtime, any user interfaces you create are translated into the relevant platform-specific UI components.</span></span>

## <a name="adding-xamarinessentials"></a><span data-ttu-id="02c5f-125">Xamarin.Essentials 추가</span><span class="sxs-lookup"><span data-stu-id="02c5f-125">Adding Xamarin.Essentials</span></span>

<span data-ttu-id="02c5f-126">UWP, Android 및 iOS 플랫폼은 운영 체제와 하드웨어를 활용하는 여러 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-126">The UWP, Android, and iOS platforms provide numerous similar capabilities that take advantage of the operating system and hardware.</span></span> <span data-ttu-id="02c5f-127">이러한 유사성에도 불구하고 API는 서로 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-127">Despite these similarities, the APIs are very different.</span></span> <span data-ttu-id="02c5f-128">플랫폼 간 코드에서 이러한 API를 사용하려면 .NET Standard 라이브러리에 노출하는 앱 프로젝트에 플랫폼별 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-128">Using these APIs from cross-platform code requires writing platform-specific code in your app projects that you expose to your .NET standard libraries.</span></span> <span data-ttu-id="02c5f-129">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/)는 사용자의 위치를 가져오기 위해 앱에서 사용할 지리적 위치 API를 포함하여 여러 해당 API를 통해 플랫폼 간 추상화를 제공하는 NuGet 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-129">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/) is a NuGet package that provides a cross-platform abstraction over a number of these APIs, including the geolocation APIs that you will use in your app to get the user's location.</span></span>

1. <span data-ttu-id="02c5f-130">Visual Studio 솔루션 탐색기에서 `ImHere` 솔루션을 마우스 오른쪽 단추로 클릭하고 ‘솔루션에 대한 NuGet 패키지 관리...’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-130">Right-click on the `ImHere` solution in the Visual Studio Solution Explorer and select *Manage NuGet Packages for Solution...*.</span></span>

2. <span data-ttu-id="02c5f-131">**찾아보기** 탭을 선택하고 “Xamarin.Essentials”를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-131">Select the **Browse** tab and search for "Xamarin.Essentials".</span></span> <span data-ttu-id="02c5f-132">이 패키지는 현재 시험판 NuGet 패키지로 사용할 수 있으므로 ‘시험판 포함’ 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-132">This package is currently available as a prerelease NuGet package, so check the *include prelease* box.</span></span>

3. <span data-ttu-id="02c5f-133">**Xamarin.Essentials** NuGet 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-133">Select the **Xamarin.Essentials** NuGet package.</span></span>

4. <span data-ttu-id="02c5f-134">오른쪽 프로젝트 목록에서 모든 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-134">Check all your projects in the project list on the right-hand side.</span></span>

5. <span data-ttu-id="02c5f-135">**설치** 단추를 클릭하여 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-135">Click the **Install** button to install the NuGet package.</span></span> <span data-ttu-id="02c5f-136">계속하려면 라이선스에 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-136">You'll need to accept the license to continue.</span></span>

    ![솔루션의 모든 프로젝트에 Xamarin.Essentials NuGet 패키지 추가](../media-drafts/2-add-essentials-nuget.png)

    > <span data-ttu-id="02c5f-138">이 모듈을 로컬로 실행하고 있으며 Android를 대상으로 지정하려면 몇 가지 추가 설정을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-138">If you are running this module locally and want to target Android, you'll need to do some additional setup.</span></span> <span data-ttu-id="02c5f-139">자세한 내용은 [Xamarin.Essentials 시작 문서](https://docs.microsoft.com/xamarin/essentials/get-started?context=xamarin%2Fios&tabs=windows%2Candroid)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02c5f-139">For more information, see the [Xamarin.Essentials Getting Started docs](https://docs.microsoft.com/xamarin/essentials/get-started?context=xamarin%2Fios&tabs=windows%2Candroid).</span></span>

## <a name="building-and-running-the-app"></a><span data-ttu-id="02c5f-140">앱 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="02c5f-140">Building and running the app</span></span>

1. <span data-ttu-id="02c5f-141">솔루션 탐색기에서 `ImHere.UWP` 프로젝트를 마우스 오른쪽 단추로 클릭하고 ‘시작 프로젝트로 설정’을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-141">Right-click on the `ImHere.UWP` project in Solution Explorer and select *Set as StartUp project*.</span></span>

2. <span data-ttu-id="02c5f-142">빌드 구성은 **디버그**로, 플랫폼은 **x86**으로 설정하고 장치는 **로컬 머신**에서 실행되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-142">Set the build configuration to **Debug**, the platform to **x86**, and the device to run on to **Local Machine**.</span></span>

    ![디버그 x86 구성이 로컬 장치에서 실행되도록 설정](../media-drafts/2-debug-configuration.png)

3. <span data-ttu-id="02c5f-144">앱 디버그를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-144">Start debugging the app.</span></span>

    ![실행 중인 앱](../media-drafts/2-debuging-app.png)

## <a name="summary"></a><span data-ttu-id="02c5f-146">요약</span><span class="sxs-lookup"><span data-stu-id="02c5f-146">Summary</span></span>

<span data-ttu-id="02c5f-147">이 단원에서는 새 Xamarin.Forms 플랫폼 간 모바일 앱을 만들고 Xamarin.Essentials NuGet 패키지를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-147">In this unit, you created a new Xamarin.Forms cross-platform mobile app and added the Xamarin.Essentials NuGet package.</span></span> <span data-ttu-id="02c5f-148">다음에는 모바일 앱 UI 및 논리를 빌드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="02c5f-148">Next, you learn how to build up the mobile app UI and logic.</span></span>