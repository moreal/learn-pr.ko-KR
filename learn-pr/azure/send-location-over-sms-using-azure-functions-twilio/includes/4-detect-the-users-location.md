<span data-ttu-id="e88d9-101">앱에는 UI와 ViewModel이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="e88d9-102">이 단원에서는 Xamarin.Essentials를 사용하여 ViewModel에 위치 조회를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="e88d9-103">위치 권한 사용</span><span class="sxs-lookup"><span data-stu-id="e88d9-103">Enable location permissions</span></span>

<span data-ttu-id="e88d9-104">모든 모바일 플랫폼에는 카메라, 사진 라이브러리, 사용자 위치 등 사용자 정보 및 특정 하드웨어와 관련된 보안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="e88d9-105">앱이 사용자 위치에 액세스하려면 먼저 사용자가 설치 시 이러한 권한을 암시적으로 부여하거나 런타임에 권한을 부여하도록 선택하여 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="e88d9-106">스토어에서 UWP 앱을 볼 때 앱에 필요한 권한이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="e88d9-107">앱을 설치하면 암시적으로 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="e88d9-108">이러한 권한은 앱 매니페스트 파일에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="e88d9-109">`ImHere.UWP` 앱 프로젝트에서 `Package.appxmanifest` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

1. <span data-ttu-id="e88d9-110">**기능** 탭으로 이동하여 *위치* 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![UWP 기능 탭](../media/4-uwp-location-capability.png)

## <a name="query-for-the-users-location"></a><span data-ttu-id="e88d9-112">사용자 위치 쿼리</span><span class="sxs-lookup"><span data-stu-id="e88d9-112">Query for the user's location</span></span>

<span data-ttu-id="e88d9-113">사용자 위치를 가져오는 두 가지 방법이 있으며 마지막으로 알려진 위치 또는 현재 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-113">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="e88d9-114">현재 위치를 가져오려면 장치에서 GPS 링크를 설정하고 정확한 위치가 감지되기를 기다려야 하기 때문에 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-114">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="e88d9-115">가장 빠른 방법은 장치에서 감지된 마지막으로 알려진 위치를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-115">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="e88d9-116">마지막으로 알려진 위치는 잠재적으로 정확성은 떨어지지만 훨씬 빠른 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-116">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="e88d9-117">위치는 [10진수 도](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true)로 표시된 위도 및 경도와 해발 미터로 표시된 장치 고도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-117">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="e88d9-118">`ImHere` .NET Standard 프로젝트에서 `MainViewModel` 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-118">Open the `MainViewModel` class in the `ImHere` .NET Standard project.</span></span>

1. <span data-ttu-id="e88d9-119">`SendLocation` 메서드에서 `Xamarin.Essentials` 네임스페이스의 `Geolocation` 클래스에 대해 `GetLastKnownLocationAsync` 정적 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-119">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span> <span data-ttu-id="e88d9-120">`Xamarin.Essentials` 네임스페이스에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-120">You will need to add a using directive for the `Xamarin.Essentials` namespace.</span></span>

    ```csharp
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

1. <span data-ttu-id="e88d9-121">사용자 위치가 발견되면 해당 위치를 사용하여 `Message` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-121">Update the `Message` property with the user's location if one is found.</span></span>

    ```csharp
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

    <span data-ttu-id="e88d9-122">이 메서드의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-122">The full code for this method is below.</span></span>
    
    ```csharp
    async Task SendLocation()
    {
        Location location = await Geolocation.GetLastKnownLocationAsync();
    
        if (location != null)
        {
            Message = $"Location found: {location.Latitude}, {location.Longitude}.";
        }
    }
    ```

1. <span data-ttu-id="e88d9-123">앱을 실행하고 **위치 보내기** 단추를 클릭하여 UI에서 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-123">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

    ![사용자 위치를 표시하는 실행 중인 앱](../media/4-running-app-showing-location.png)    

> [!NOTE]
> <span data-ttu-id="e88d9-125">이 앱은 마지막으로 알려진 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-125">This app uses the last known location.</span></span> <span data-ttu-id="e88d9-126">프로덕션 품질 앱에서는 시간 제한을 지정하여 정확한 현재 위치를 가져오고, 시간 이내에 발견되지 않을 경우 마지막으로 알려진 위치로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-126">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="e88d9-127">[Xamarin.Essentials 지리적 위치 문서](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-127">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true).</span></span>
> 
> <span data-ttu-id="e88d9-128">이 앱에는 오류 처리 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-128">This app does not have error handling.</span></span> <span data-ttu-id="e88d9-129">프로덕션 품질 앱에서는 발생하는 예외(예: 위치 사용 불가)를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-129">In a production-quality app, you should handle any exceptions that occur, such as if the location was not available.</span></span>

## <a name="summary"></a><span data-ttu-id="e88d9-130">요약</span><span class="sxs-lookup"><span data-stu-id="e88d9-130">Summary</span></span>

<span data-ttu-id="e88d9-131">이 단원에서는 Xamarin.Essentials를 사용하여 사용자 위치를 가져오는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="e88d9-132">다음 단원에서는 모바일 앱의 백 엔드 역할을 하는 Azure 함수를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e88d9-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>