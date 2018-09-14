앱에는 UI와 ViewModel이 있습니다. 이 단원에서는 Xamarin.Essentials를 사용하여 ViewModel에 위치 조회를 추가합니다.

## <a name="enable-location-permissions"></a>위치 권한 사용

모든 모바일 플랫폼에는 카메라, 사진 라이브러리, 사용자 위치 등 사용자 정보 및 특정 하드웨어와 관련된 보안이 있습니다. 앱이 사용자 위치에 액세스하려면 먼저 사용자가 설치 시 이러한 권한을 암시적으로 부여하거나 런타임에 권한을 부여하도록 선택하여 권한을 부여해야 합니다. 스토어에서 UWP 앱을 볼 때 앱에 필요한 권한이 목록에 표시됩니다. 앱을 설치하면 암시적으로 권한이 부여됩니다. 이러한 권한은 앱 매니페스트 파일에서 구성됩니다.

1. `ImHere.UWP` 앱 프로젝트에서 `Package.appxmanifest` 파일을 엽니다.

1. **기능** 탭으로 이동하여 *위치* 기능을 선택합니다.

    ![UWP 기능 탭](../media/4-uwp-location-capability.png)

> Android 또는 iOS를 지원하려는 경우 권한을 다르게 구성해야 합니다. [Xamarin.Essentials 지리적 위치 문서](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started)에 자세히 설명되어 있습니다.

## <a name="query-for-the-users-location"></a>사용자 위치 쿼리

사용자 위치를 가져오는 두 가지 방법이 있으며 마지막으로 알려진 위치 또는 현재 위치입니다. 현재 위치를 가져오려면 장치에서 GPS 링크를 설정하고 정확한 위치가 감지되기를 기다려야 하기 때문에 몇 시간이 걸릴 수 있습니다. 가장 빠른 방법은 장치에서 감지된 마지막으로 알려진 위치를 가져오는 것입니다. 마지막으로 알려진 위치는 잠재적으로 정확성은 떨어지지만 훨씬 빠른 호출입니다. 위치는 [10진수 도](https://en.wikipedia.org/wiki/Decimal_degrees)로 표시된 위도 및 경도와 해수면 위의 장치 고도(미터)로 제공됩니다.

1. `ImHere` .NET Standard 프로젝트의 `MainViewModel` 클래스를 엽니다.

1. `SendLocation` 메서드에서 `Xamarin.Essentials` 네임스페이스의 `Geolocation` 클래스에 대해 `GetLastKnownLocationAsync` 정적 메서드를 호출합니다.

    ```csharp
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

1. 사용자 위치가 발견되면 `Message` 속성을 해당 위치로 업데이트합니다.

    ```csharp
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

이 메서드의 전체 코드는 다음과 같습니다.

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

앱을 실행하고 **위치 보내기** 단추를 클릭하여 UI에서 위치를 확인합니다.

![사용자 위치를 표시하는 실행 중인 앱](../media/4-running-app-showing-location.png)

> 이 앱은 마지막으로 알려진 위치를 사용합니다. 프로덕션 품질 앱에서는 시간 제한을 지정하여 정확한 현재 위치를 가져오고, 시간 이내에 발견되지 않을 경우 마지막으로 알려진 위치로 대체합니다. [Xamarin.Essentials 지리적 위치 문서](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다. 이 앱에는 오류 처리 기능이 없습니다. 프로덕션 품질 앱에서는 발생하는 예외(예: 위치 사용 불가)를 처리해야 합니다.

## <a name="summary"></a>요약

이 단원에서는 Xamarin.Essentials를 사용하여 사용자 위치를 가져오는 방법을 배웠습니다. 다음 단원에서는 모바일 앱의 백 엔드 역할을 하는 Azure 함수를 만들겠습니다.