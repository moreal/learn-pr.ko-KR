<span data-ttu-id="30086-101">앱에는 UI와 ViewModel이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="30086-102">이 단원에서는 Xamarin.Essentials를 사용하여 ViewModel에 위치 조회를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="30086-103">위치 권한 사용</span><span class="sxs-lookup"><span data-stu-id="30086-103">Enable location permissions</span></span>

<span data-ttu-id="30086-104">모든 모바일 플랫폼에는 카메라, 사진 라이브러리, 사용자 위치 등 사용자 정보 및 특정 하드웨어와 관련된 보안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="30086-105">앱이 사용자 위치에 액세스하려면 먼저 사용자가 설치 시 이러한 권한을 암시적으로 부여하거나 런타임에 권한을 부여하도록 선택하여 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="30086-106">스토어에서 UWP 앱을 볼 때 앱에 필요한 권한이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30086-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="30086-107">앱을 설치하면 암시적으로 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="30086-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="30086-108">이러한 권한은 앱 매니페스트 파일에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="30086-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="30086-109">`ImHere.UWP` 앱 프로젝트에서 `Package.appxmanifest` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30086-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

2. <span data-ttu-id="30086-110">**기능** 탭으로 이동하여 *위치* 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![UWP 기능 탭](../media-drafts/4-uwp-location-capability.png)

> <span data-ttu-id="30086-112">Android 또는 iOS를 지원하려는 경우 권한을 다르게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-112">If you want to support Android or iOS, the permissions need to be configured differently.</span></span> <span data-ttu-id="30086-113">[Xamarin.Essentials 지리적 위치 문서](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-113">This is detailed in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span></span>

## <a name="query-for-the-users-location"></a><span data-ttu-id="30086-114">사용자 위치 쿼리</span><span class="sxs-lookup"><span data-stu-id="30086-114">Query for the user's location</span></span>

<span data-ttu-id="30086-115">사용자 위치를 가져오는 두 가지 방법이 있으며 마지막으로 알려진 위치 또는 현재 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="30086-115">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="30086-116">현재 위치를 가져오려면 장치에서 GPS 링크를 설정하고 정확한 위치가 감지되기를 기다려야 하기 때문에 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-116">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="30086-117">가장 빠른 방법은 장치에서 감지된 마지막으로 알려진 위치를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30086-117">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="30086-118">마지막으로 알려진 위치는 잠재적으로 정확성은 떨어지지만 훨씬 빠른 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="30086-118">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="30086-119">위치는 [10진수 도](https://en.wikipedia.org/wiki/Decimal_degrees)로 표시된 위도 및 경도와 해수면 위의 장치 고도(미터)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="30086-119">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="30086-120">`ImHere` .NET Standard 프로젝트의 `MainViewModel` 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30086-120">Open the `MainViewModel` class in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="30086-121">`SendLocation` 메서드에서 `Xamarin.Essentials` 네임스페이스의 `Geolocation` 클래스에 대해 `GetLastKnownLocationAsync` 정적 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-121">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span>

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. <span data-ttu-id="30086-122">사용자 위치가 발견되면 `Message` 속성을 해당 위치로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-122">Update the `Message` property with the user's location if one is found.</span></span>

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

<span data-ttu-id="30086-123">이 메서드의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-123">The full code for this method is below.</span></span>

```cs
async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
}
```

<span data-ttu-id="30086-124">앱을 실행하고 **위치 보내기** 단추를 클릭하여 UI에서 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-124">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

![사용자 위치를 표시하는 실행 중인 앱](../media-drafts/4-running-app-showing-location.png)

> <span data-ttu-id="30086-126">이 앱은 마지막으로 알려진 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-126">This app uses the last known location.</span></span> <span data-ttu-id="30086-127">프로덕션 품질 앱에서는 시간 제한을 지정하여 정확한 현재 위치를 가져오고, 시간 이내에 발견되지 않을 경우 마지막으로 알려진 위치로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-127">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="30086-128">[Xamarin.Essentials 지리적 위치 문서](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다. 이 앱에는 오류 처리가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-128">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). This app does not have error handling.</span></span> <span data-ttu-id="30086-129">프로덕션 품질 앱에서는 가령 위치를 사용할 수 없고 예외가 발생할 경우 발생하는 예외를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30086-129">In a production-quality app, you should handle any exceptions that occur, for example, if the location was not available and an exception was thrown.</span></span>

## <a name="summary"></a><span data-ttu-id="30086-130">요약</span><span class="sxs-lookup"><span data-stu-id="30086-130">Summary</span></span>

<span data-ttu-id="30086-131">이 단원에서는 Xamarin.Essentials를 사용하여 사용자 위치를 가져오는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="30086-132">다음 단원에서는 모바일 앱의 백 엔드 역할을 하는 Azure 함수를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="30086-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>