이 시점에서 모바일 앱은 간단한 “Hello World” 앱입니다. 이 단원에서는 UI 및 일부 기본 응용 프로그램 논리를 추가합니다.

앱의 UI는 다음으로 구성됩니다.

- 일부 전화 번호를 입력하기 위한 텍스트 입력 컨트롤
- Azure 함수를 사용하여 해당 번호로 위치를 보내는 단추
- 위치 전송 중, 위치 전송 성공 등 현재 상태의 사용자에게 메시지를 표시하는 레이블

Xamarin.Forms는 MVVM(Model-View-ViewModel)이라는 디자인 패턴을 지원합니다. [Xamarin MVVM 문서](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm)에서 MVVM에 대해 자세히 알아볼 수 있지만, 핵심은 각 페이지(View)에 속성 및 동작을 노출하는 ViewModel이 있다는 것입니다.

ViewModel 속성은 이름으로 UI의 구성 요소에 ‘바인딩’되며, 이 바인딩은 View와 ViewModel 간에 데이터를 동기화합니다. 예를 들어 `Name`이라는 ViewModel의 `string` 속성은 UI에 있는 텍스트 입력 컨트롤의 `Text` 속성에 바인딩될 수 있습니다. 텍스트 입력 컨트롤은 `Name` 속성의 값을 표시하고, 사용자가 UI의 텍스트를 변경하면 `Name` 속성이 업데이트됩니다. ViewModel에서 `Name` 속성의 값이 변경되면 UI가 업데이트되도록 이벤트가 발생합니다.

ViewModel 동작은 명령 속성으로 노출되며, 명령을 호출할 때 실행되는 작업을 래핑하는 개체가 명령입니다. 이러한 명령은 이름으로 단추 등의 컨트롤에 바인딩되고, 단추를 탭하면 명령이 호출됩니다.

## <a name="create-a-base-viewmodel"></a>기본 ViewModel 만들기

ViewModel은 모두 `INotifyPropertyChanged` 인터페이스를 구현합니다. 이 인터페이스에는 UI에 업데이트를 알리는 데 사용되는 단일 이벤트 `PropertyChanged`가 있습니다. 이 이벤트에는 변경된 속성의 이름을 포함하는 이벤트 인수가 있습니다. 이 인터페이스를 구현하고 일부 도우미 메서드를 제공하여 기본 ViewModel 클래스를 만드는 것이 일반적입니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭하고 *추가->클래스...* 를 선택하여 `ImHere` .NET Standard 프로젝트에 `BaseViewModel`이라는 새 클래스를 만듭니다. 새 클래스의 이름을 “BaseViewModel”로 지정하고 **추가**를 클릭합니다.

1. 클래스를 `public`으로 설정하고 `INotifyPropertyChanged`에서 파생합니다. `System.ComponentModel`에 대해 using 지시문을 추가해야 합니다.

1. `PropertyChanged` 이벤트를 추가하여 `INotifyPropertyChanged` 인터페이스를 구현합니다.

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

1. ViewModel 속성의 일반적인 패턴은 전용 지원 필드가 있는 공용 속성을 사용하는 것입니다. 속성 setter에서 지원 필드가 새 값과 비교해서 검사됩니다. 새 값이 지원 필드와 다르면 지원 필드가 업데이트되고 `PropertyChanged` 이벤트가 발생합니다. 이 논리는 메서드로 쉽게 추출되므로 `Set` 메서드를 추가합니다. `System.Runtime.CompilerServices` 네임스페이스에 대해 using 지시문을 추가해야 합니다.

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    이 메서드는 지원 필드, 새 값 및 속성 이름에 대한 참조를 사용합니다. 필드가 변경되지 않은 경우 메서드가 반환되고, 변경된 경우에는 필드가 업데이트되고 `PropertyChanged` 이벤트가 발생합니다. `Set` 메서드의 `propertyName` 매개 변수는 기본 매개 변수이며 `CallerMemberName` 특성으로 표시됩니다. 이 메서드가 속성 setter에서 호출될 때 이 매개 변수는 일반적으로 기본값으로 유지됩니다. 그런 다음, 컴파일러가 자동으로 매개 변수 값을 호출 속성의 이름으로 설정합니다.

이 클래스의 전체 코드는 다음과 같습니다.

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a>페이지에 대한 ViewModel 만들기

`MainPage`에는 전화 번호의 문자 입력 컨트롤과 메시지를 표시할 레이블이 포함됩니다. 이러한 컨트롤은 ViewModel의 속성에 바인딩됩니다.

1. `ImHere` .NET Standard 프로젝트에 `MainViewModel`이라는 클래스를 만듭니다.

1. 이 클래스를 public으로 설정하고 `BaseViewModel`에서 파생합니다.

1. 각각 지원 필드가 있는 두 개의 `string` 속성, `PhoneNumbers` 및 `Message`를 추가합니다. 속성 setter에서 기본 클래스 `Set` 메서드를 사용하여 값을 업데이트하고 `PropertyChanged` 이벤트를 발생시킵니다.

   ```cs
    string message = "";
    public string Message
    {
        get => message;
        set => Set(ref message, value);
    }

    string phoneNumbers = "";
    public string PhoneNumbers
    {
        get => phoneNumbers;
        set => Set(ref phoneNumbers, value);
    }
   ```

1. `SendLocationCommand`라는 읽기 전용 명령 속성을 추가합니다. 이 명령은 `System.Windows.Input` 네임스페이스의 `ICommand` 형식이 지정됩니다.

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

1. 클래스에 생성자를 추가하고, 이 생성자에서 `SendLocationCommand`를 `Xamarin.Forms` 네임스페이스의 새 `Command`로 초기화합니다. 이 명령의 생성자는 명령이 호출될 때 실행할 `Action`을 사용하므로 `async`이라는 `SendLocation` 메서드를 만들고 이 호출을 `await`하는 람다 함수를 생성자에 전달합니다. `SendLocation` 메서드의 본문은 이 모듈의 이후 단원에서 구현됩니다. `Task`를 반환하려면 `System.Threading.Tasks` 네임스페이스에 대해 using 지시문을 추가해야 합니다.

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

이 클래스의 코드는 다음과 같습니다.

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using Xamarin.Forms;

namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a>사용자 인터페이스 만들기

XAML을 사용하여 Xamarin.Forms UI를 빌드할 수 있습니다.

1. `ImHere` 프로젝트에서 `MainPage.xaml` 파일을 엽니다. 해당 페이지가 XAML 편집기에서 열립니다.

    참고 - `ImHere.UWP` 프로젝트에도 `MainPage.xaml` 파일이 포함되어 있습니다. .NET Standard 라이브러리의 파일을 편집해야 합니다.

1. ViewModel의 속성에 컨트롤을 바인딩하려면 먼저 ViewModel 인스턴스를 페이지의 바인딩 컨텍스트로 설정해야 합니다. 최상위 `ContentPage` 안에 다음 XAML을 추가합니다.

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

1. `StackLayout`의 콘텐츠를 삭제하고 안쪽 여백을 추가하여 UI 모양을 개선합니다.

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

1. 사용자가 전화 번호를 추가하는 데 사용할 수 있는 `Editor` 컨트롤을 `StackLayout`에 추가하고, 입력 컨트롤의 용도를 설명하는 `Label`을 위에 배치합니다. `StackLayout`은 컨트롤이 추가되는 순서대로 자식 컨트롤을 가로 또는 세로로 누적하므로 `Label`을 먼저 추가하면 `Editor` 위에 배치됩니다. `Editor` 컨트롤은 여러 줄 입력 컨트롤이므로 사용자가 행당 하나씩, 여러 개의 전화 번호를 입력할 수 있습니다.

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    `Editor`의 `Text` 속성은 `MainViewModel`의 `PhoneNumbers` 속성에 바인딩됩니다. 바인딩 구문은 속성 값을 `"{Binding <property name>}"`으로 설정하는 것입니다. 중괄호는 이 값이 특별하며, 단순 `string`과 다르게 처리되어야 함을 XAML 컴파일러에 알립니다.

1. 사용자 위치를 보내는 `Button`을 `Editor` 아래에 추가합니다.

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    `Command` 속성은 ViewModel의 `SendLocationCommand` 명령에 바인딩됩니다. 단추를 탭하면 명령이 실행됩니다.

1. 상태 메시지를 표시하는 `Label`을 `Button` 아래에 추가합니다.

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

이 페이지의 전체 코드는 다음과 같습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ImHere"
             x:Class="ImHere.MainPage">
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
        <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                Command="{Binding SendLocationCommand}" />
        <Label Text="{Binding Message}"
               HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

앱을 실행하여 새 UI를 확인합니다. 이 시점에서 바인딩의 유효성을 검사하려는 경우 속성 또는 `SendLocation` 메서드에 중단점을 추가하면 됩니다.

![새로운 앱 UI](../media-drafts/3-new-ui.png)

## <a name="summary"></a>요약

이 단원에서는 응용 프로그램 논리를 처리하는 ViewModel과 함께 XAML을 사용하여 앱의 UI를 만드는 방법을 배웠습니다. 또한 ViewModel을 UI에 바인딩하는 방법을 배웠습니다. 다음 단원에서는 ViewModel에 위치 조회를 추가하겠습니다.