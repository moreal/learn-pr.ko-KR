<span data-ttu-id="cbc09-101">이 시점에서 모바일 앱은 간단한 “Hello World” 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-101">At this point, the mobile app is a simple "Hello World" app.</span></span> <span data-ttu-id="cbc09-102">이 단원에서는 UI 및 일부 기본 응용 프로그램 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-102">In this unit, you add the UI and some basic application logic.</span></span>

<span data-ttu-id="cbc09-103">앱의 UI는 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-103">The UI for the app will consist of:</span></span>

- <span data-ttu-id="cbc09-104">일부 전화 번호를 입력하기 위한 텍스트 입력 컨트롤</span><span class="sxs-lookup"><span data-stu-id="cbc09-104">A text-entry control to enter some phone numbers.</span></span>
- <span data-ttu-id="cbc09-105">Azure 함수를 사용하여 해당 번호로 위치를 보내는 단추</span><span class="sxs-lookup"><span data-stu-id="cbc09-105">A button to send your location to those numbers using an Azure function.</span></span>
- <span data-ttu-id="cbc09-106">위치 전송 중, 위치 전송 성공 등 현재 상태의 사용자에게 메시지를 표시하는 레이블</span><span class="sxs-lookup"><span data-stu-id="cbc09-106">A label that will show a message to the user of the current status, such as the location being sent and location sent successfully.</span></span>

<span data-ttu-id="cbc09-107">Xamarin.Forms는 MVVM(Model-View-ViewModel)이라는 디자인 패턴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-107">Xamarin.Forms supports a design pattern called Model-View-ViewModel (MVVM).</span></span> <span data-ttu-id="cbc09-108">[Xamarin MVVM 문서](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm?azure-portal=true)에서 MVVM에 대해 자세히 알아볼 수 있지만, 핵심은 각 페이지(View)에 속성 및 동작을 노출하는 ViewModel이 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-108">You can read more about MVVM in the [Xamarin MVVM docs](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm?azure-portal=true), but the essence of it is, each page (View) has a ViewModel that exposes properties and behavior.</span></span>

<span data-ttu-id="cbc09-109">ViewModel 속성은 이름으로 UI의 구성 요소에 ‘바인딩’되며, 이 바인딩은 View와 ViewModel 간에 데이터를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-109">ViewModel properties are 'bound' to components on the UI by name, and this binding synchronizes data between the View and ViewModel.</span></span> <span data-ttu-id="cbc09-110">예를 들어 `Name`이라는 ViewModel의 `string` 속성은 UI에 있는 텍스트 입력 컨트롤의 `Text` 속성에 바인딩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-110">For example, a `string` property on a ViewModel called `Name` could be bound to the `Text` property of a text-entry control on the UI.</span></span> <span data-ttu-id="cbc09-111">텍스트 입력 컨트롤은 `Name` 속성의 값을 표시하고, 사용자가 UI의 텍스트를 변경하면 `Name` 속성이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-111">The text-entry control shows the value in the `Name` property and, when the user changes the text in the UI, the `Name` property is updated.</span></span> <span data-ttu-id="cbc09-112">ViewModel에서 `Name` 속성의 값이 변경되면 UI가 업데이트되도록 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-112">If the value of the `Name` property is changed in the ViewModel, an event is raised to tell the UI to update.</span></span>

<span data-ttu-id="cbc09-113">ViewModel 동작은 명령 속성으로 노출되며, 명령을 호출할 때 실행되는 작업을 래핑하는 개체가 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-113">ViewModel behavior is exposed as command properties, a command being an object that wraps an action that is executed when the command is invoked.</span></span> <span data-ttu-id="cbc09-114">이러한 명령은 이름으로 단추 등의 컨트롤에 바인딩되고, 단추를 탭하면 명령이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-114">These commands are bound by name to controls like buttons, and tapping a button will invoke the command.</span></span>

## <a name="create-a-base-viewmodel"></a><span data-ttu-id="cbc09-115">기본 ViewModel 만들기</span><span class="sxs-lookup"><span data-stu-id="cbc09-115">Create a base ViewModel</span></span>

<span data-ttu-id="cbc09-116">ViewModel은 모두 `INotifyPropertyChanged` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-116">ViewModels all implement the `INotifyPropertyChanged` interface.</span></span> <span data-ttu-id="cbc09-117">이 인터페이스에는 UI에 업데이트를 알리는 데 사용되는 단일 이벤트 `PropertyChanged`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-117">This interface has a single event, `PropertyChanged`, which is used to notify the UI of any updates.</span></span> <span data-ttu-id="cbc09-118">이 이벤트에는 변경된 속성의 이름을 포함하는 이벤트 인수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-118">This event has event args that contain the name of the property that has changed.</span></span> <span data-ttu-id="cbc09-119">이 인터페이스를 구현하고 일부 도우미 메서드를 제공하여 기본 ViewModel 클래스를 만드는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-119">It's common practice to create a base ViewModel class implementing this interface and providing some helper methods.</span></span>

1. <span data-ttu-id="cbc09-120">프로젝트를 마우스 오른쪽 단추로 클릭하고 *추가->클래스...* 를 선택하여 `ImHere` .NET Standard 프로젝트에 `BaseViewModel`이라는 새 클래스를 만듭니다. 새 클래스의 이름을 “BaseViewModel”로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-120">Create a new class in the `ImHere` .NET Standard project called `BaseViewModel` by right-clicking on the project, and then selecting *Add->Class...*. Name the new class "BaseViewModel" and click **Add**.</span></span>

1. <span data-ttu-id="cbc09-121">클래스를 `public`으로 설정하고 `INotifyPropertyChanged`에서 파생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-121">Make the class `public` and derive from `INotifyPropertyChanged`.</span></span> <span data-ttu-id="cbc09-122">`System.ComponentModel`에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-122">You'll need to add a using directive for `System.ComponentModel`.</span></span>

1. <span data-ttu-id="cbc09-123">`PropertyChanged` 이벤트를 추가하여 `INotifyPropertyChanged` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-123">Implement the `INotifyPropertyChanged` interface by adding the `PropertyChanged` event:</span></span>

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

1. <span data-ttu-id="cbc09-124">ViewModel 속성의 일반적인 패턴은 전용 지원 필드가 있는 공용 속성을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-124">The common pattern for ViewModel properties is to have a public property with a private backing field.</span></span> <span data-ttu-id="cbc09-125">속성 setter에서 지원 필드가 새 값과 비교해서 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-125">In the property setter, the backing field is checked against the new value.</span></span> <span data-ttu-id="cbc09-126">새 값이 지원 필드와 다르면 지원 필드가 업데이트되고 `PropertyChanged` 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-126">If the new value is different to the backing field, the backing field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="cbc09-127">이 논리는 메서드로 쉽게 추출되므로 `Set` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-127">This logic is easy to factor out into a method, so add the `Set` method.</span></span> <span data-ttu-id="cbc09-128">`System.Runtime.CompilerServices` 네임스페이스에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-128">You'll need to add a using directive for the `System.Runtime.CompilerServices` namespace.</span></span>

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    <span data-ttu-id="cbc09-129">이 메서드는 지원 필드, 새 값 및 속성 이름에 대한 참조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-129">This method takes a reference to the backing field, the new value, and the property name.</span></span> <span data-ttu-id="cbc09-130">필드가 변경되지 않은 경우 메서드가 반환되고, 변경된 경우에는 필드가 업데이트되고 `PropertyChanged` 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-130">If the field hasn't changed, the method returns, otherwise, the field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="cbc09-131">`Set` 메서드의 `propertyName` 매개 변수는 기본 매개 변수이며 `CallerMemberName` 특성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-131">The `propertyName` parameter on the `Set` method is a default parameter and is marked with the `CallerMemberName` attribute.</span></span> <span data-ttu-id="cbc09-132">이 메서드가 속성 setter에서 호출될 때 이 매개 변수는 일반적으로 기본값으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-132">When this method is called from a property setter, this parameter is normally left as the default value.</span></span> <span data-ttu-id="cbc09-133">그런 다음, 컴파일러가 자동으로 매개 변수 값을 호출 속성의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-133">The compiler will then automatically set the parameter value to be the name of the calling property.</span></span>

<span data-ttu-id="cbc09-134">이 클래스의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-134">The full code for this class is below.</span></span>

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

## <a name="create-a-viewmodel-for-the-page"></a><span data-ttu-id="cbc09-135">페이지에 대한 ViewModel 만들기</span><span class="sxs-lookup"><span data-stu-id="cbc09-135">Create a ViewModel for the page</span></span>

<span data-ttu-id="cbc09-136">`MainPage`에는 전화 번호의 문자 입력 컨트롤과 메시지를 표시할 레이블이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-136">The `MainPage` will have a text-entry control for phone numbers and a label to display a message.</span></span> <span data-ttu-id="cbc09-137">이러한 컨트롤은 ViewModel의 속성에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-137">These controls will be bound to properties on a ViewModel.</span></span>

1. <span data-ttu-id="cbc09-138">`ImHere` .NET Standard 프로젝트에 `MainViewModel`이라는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-138">Create a class called `MainViewModel` in the `ImHere` .NET Standard project.</span></span>

1. <span data-ttu-id="cbc09-139">이 클래스를 public으로 설정하고 `BaseViewModel`에서 파생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-139">Make this class public and derive from `BaseViewModel`.</span></span>

1. <span data-ttu-id="cbc09-140">각각 지원 필드가 있는 두 개의 `string` 속성, `PhoneNumbers` 및 `Message`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-140">Add two `string` properties, `PhoneNumbers` and `Message`, each with a backing field.</span></span> <span data-ttu-id="cbc09-141">속성 setter에서 기본 클래스 `Set` 메서드를 사용하여 값을 업데이트하고 `PropertyChanged` 이벤트를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-141">In the property setter, use the base class `Set` method to update the value and raise the `PropertyChanged` event.</span></span>

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

1. <span data-ttu-id="cbc09-142">`SendLocationCommand`라는 읽기 전용 명령 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-142">Add a read-only command property called `SendLocationCommand`.</span></span> <span data-ttu-id="cbc09-143">이 명령은 `System.Windows.Input` 네임스페이스의 `ICommand` 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-143">This command will have a type of `ICommand` from the `System.Windows.Input` namespace.</span></span>

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

1. <span data-ttu-id="cbc09-144">클래스에 생성자를 추가하고, 이 생성자에서 `SendLocationCommand`를 새 Xamarin.Forms `Command`로 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-144">Add a constructor to the class, and in this constructor, initialize the `SendLocationCommand` as a new Xamarin.Forms `Command`.</span></span> <span data-ttu-id="cbc09-145">`Xamarin.Forms` 네임스페이스에 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-145">You will need to add a using directive for the `Xamarin.Forms` namespace.</span></span> <span data-ttu-id="cbc09-146">이 명령의 생성자는 명령이 호출될 때 실행할 `Action`을 사용하므로 `async`이라는 `SendLocation` 메서드를 만들고 이 호출을 `await`하는 람다 함수를 생성자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-146">The constructor for this command takes an `Action` to run when the command is invoked, so create an `async` method called `SendLocation` and pass a lambda function that `await`s this call to the constructor.</span></span> <span data-ttu-id="cbc09-147">`SendLocation` 메서드의 본문은 이 모듈의 이후 단원에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-147">The body of the `SendLocation` method will be implemented in later units in this module.</span></span> <span data-ttu-id="cbc09-148">`Task`를 반환하려면 `System.Threading.Tasks` 네임스페이스에 대해 using 지시문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-148">You'll need to add a using directive for the `System.Threading.Tasks` namespace to be able to return a `Task`.</span></span>

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

<span data-ttu-id="cbc09-149">이 클래스의 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-149">The code for this class is shown below.</span></span>

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

## <a name="create-the-user-interface"></a><span data-ttu-id="cbc09-150">사용자 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="cbc09-150">Create the user interface</span></span>

<span data-ttu-id="cbc09-151">XAML을 사용하여 Xamarin.Forms UI를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-151">Xamarin.Forms UIs can be built using XAML.</span></span>

1. <span data-ttu-id="cbc09-152">`ImHere` 프로젝트에서 `MainPage.xaml` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-152">Open the `MainPage.xaml` file from the `ImHere` project.</span></span> <span data-ttu-id="cbc09-153">해당 페이지가 XAML 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-153">The page will open in the XAML editor.</span></span>

    > [!NOTE]
    >  <span data-ttu-id="cbc09-154">`ImHere.UWP` 프로젝트에도 `MainPage.xaml` 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-154">The `ImHere.UWP` project also contains a file called `MainPage.xaml`.</span></span> <span data-ttu-id="cbc09-155">.NET Standard 라이브러리의 파일을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-155">Make sure you're editing the one in the .NET Standard library.</span></span>

1. <span data-ttu-id="cbc09-156">ViewModel의 속성에 컨트롤을 바인딩하려면 먼저 ViewModel 인스턴스를 페이지의 바인딩 컨텍스트로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-156">Before you can bind controls to properties on a ViewModel, you have to set an instance of the ViewModel as the binding context of the page.</span></span> <span data-ttu-id="cbc09-157">최상위 `ContentPage` 안에 다음 XAML을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-157">Add the following XAML inside the top-level `ContentPage`.</span></span>

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

1. <span data-ttu-id="cbc09-158">`StackLayout`을 다음 코드로 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-158">Overwrite the `StackLayout` with the following code:</span></span>

     ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Start"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```
    - <span data-ttu-id="cbc09-159">`Editor` 컨트롤은 전화 번호를 추가하는 데 사용되며, 위의 `Label`은 사용자에게 이 필드의 용도를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-159">The `Editor` control will be used to add phone numbers, and the `Label` above describes the purpose of this field to the user.</span></span> 
    - <span data-ttu-id="cbc09-160">`StackLayout`은 컨트롤이 추가되는 순서대로 자식 컨트롤을 가로 또는 세로로 누적하므로 `Label`을 먼저 추가하면 `Editor` 위에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-160">`StackLayout`'s stack child controls either horizontally or vertically in the order in which the controls are added, so adding the `Label` first will put it above the `Editor`.</span></span>
    - <span data-ttu-id="cbc09-161">`Editor` 컨트롤은 여러 줄 입력 컨트롤이므로 사용자가 행당 하나씩, 여러 개의 전화 번호를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-161">`Editor` controls are multi-line entry controls, allowing the user to enter multiple phone numbers, one per line.</span></span>

   

    <span data-ttu-id="cbc09-162">`Editor`의 `Text` 속성은 `MainViewModel`의 `PhoneNumbers` 속성에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-162">The `Text` property on the `Editor` is bound to the `PhoneNumbers` property on the `MainViewModel`.</span></span> <span data-ttu-id="cbc09-163">바인딩 구문은 속성 값을 `"{Binding <property name>}"`으로 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-163">The syntax for binding is to set the property value to `"{Binding <property name>}"`.</span></span> <span data-ttu-id="cbc09-164">중괄호는 이 값이 특별하며, 단순 `string`과 다르게 처리되어야 함을 XAML 컴파일러에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-164">The curly braces will tell the XAML compiler that this value is special and should be treated differently from a simple `string`.</span></span>

1. <span data-ttu-id="cbc09-165">`Editor` 컨트롤 아래에 `Button`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-165">Add a `Button` below the `Editor` control.</span></span> <span data-ttu-id="cbc09-166">이 단추를 사용하여 사용자의 위치를 보내도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-166">We'll use this button to send the user's location.</span></span>

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    <span data-ttu-id="cbc09-167">`Command` 속성은 ViewModel의 `SendLocationCommand` 명령에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-167">The `Command` property is bound to the `SendLocationCommand` command on the ViewModel.</span></span> <span data-ttu-id="cbc09-168">단추를 탭하면 명령이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-168">When the button is tapped, the command will be executed.</span></span>

1. <span data-ttu-id="cbc09-169">`Button` 컨트롤 아래에 `Label`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-169">Add a `Label` below the `Button` control.</span></span> <span data-ttu-id="cbc09-170">이 레이블에는 상태 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-170">We'll display status messages in this label.</span></span>

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

    <span data-ttu-id="cbc09-171">이 페이지의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-171">The full code for this page is below.</span></span>
    
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
            <Label Text="Phone numbers to send to:" HorizontalOptions="Start"/>
            <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
            <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                    Command="{Binding SendLocationCommand}" />
            <Label Text="{Binding Message}"
                   HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
        </StackLayout>
    </ContentPage>
    ```

1. <span data-ttu-id="cbc09-172">앱을 실행하여 새 UI를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-172">Run the app to see the new UI.</span></span> <span data-ttu-id="cbc09-173">이 시점에서 바인딩의 유효성을 검사하려는 경우 속성 또는 `SendLocation` 메서드에 중단점을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-173">If you want to validate the bindings at this point, you can do so by adding breakpoints to the properties or the `SendLocation` method.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cbc09-174">이 앱을 컴파일할 때 `SendLocation`에 `await` 한정자가 없다는 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-174">When you compile this app, you will see a warning about `SendLocation` lacking `await` modifiers.</span></span> <span data-ttu-id="cbc09-175">이러한 문제는 다음 단원에서 이 메서드에 코드가 한 번 더 추가되면 해결되므로 이 경고는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-175">You can ignore this warning as this will be resolved once more code is added to this method in the next unit.</span></span>
    
    
    ![새로운 앱 UI](../media/3-new-ui.png)

## <a name="summary"></a><span data-ttu-id="cbc09-177">요약</span><span class="sxs-lookup"><span data-stu-id="cbc09-177">Summary</span></span>

<span data-ttu-id="cbc09-178">이 단원에서는 응용 프로그램 논리를 처리하는 ViewModel과 함께 XAML을 사용하여 앱의 UI를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-178">In this unit, you learned how to create the UI for the app using XAML, along with a ViewModel to handle the applications logic.</span></span> <span data-ttu-id="cbc09-179">또한 ViewModel을 UI에 바인딩하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-179">You also learned how to bind the ViewModel to the UI.</span></span> <span data-ttu-id="cbc09-180">다음 단원에서는 ViewModel에 위치 조회를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc09-180">In the next unit, you add location lookup to the ViewModel.</span></span>