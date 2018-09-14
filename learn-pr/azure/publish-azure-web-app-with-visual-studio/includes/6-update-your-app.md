성공적으로 웹앱을 만들어 Azure에 게시했지만 내용을 변경하려는 경우 어떻게 되나요? Visual Studio는 앱이 게시되는 위치를 기억하므로 앱 업데이트 및 변경을 두 번만 클릭하면 되는 프로세스로 만들 수 있습니다.

## <a name="explore-the-project-structure"></a>프로젝트 구조 살펴보기

Visual Studio에서 ASP.NET 웹앱을 만들었으므로 이제 웹 사이트를 편집하고 사용자 지정해야 합니다. Visual Studio에서 자동으로 만든 프로젝트의 구조를 살펴보겠습니다.

### <a name="dependencies"></a>종속성

종속성에는 앱이 실행되도록 하는 ASP.NET 내부 요소가 포함됩니다. 특정 타사 패키지를 추가하지 않는 한, 이 폴더에서 많은 시간을 보낼 필요는 없습니다.

### <a name="properties"></a>속성

속성 폴더에는 웹앱을 호스트하는 위치에 대한 구성 데이터가 포함되어 있습니다. 지금 **PublishProfiles** 폴더를 확장하면 Alpine Ski Hill 사이트 URL이 표시됩니다. 각 게시 프로필은 Visual Studio가 파일을 업로드하는 데 사용하는 Azure 주소와 같은 게시 구성 정보가 포함된 .xml 파일입니다.

### <a name="wwwroot"></a>wwwroot

wwwroot 파일에는 .css, .js, 이미지 및 .lib 파일과 같은 사이트의 모든 정적 자산이 포함되어 있습니다. 사이트 스타일을 지정하고 기능을 더 추가할 준비가 되면 여기에서 작업을 수행합니다.

### <a name="pages"></a>페이지

**Pages** 폴더에는 사이트 페이지에 사용할 _**Razor**_ 템플릿이 포함되어 있습니다.
Razor는 HTML을 기반으로 빌드되었으며 사이트에서 데이터를 표시하고 논리를 실행하는 데 사용되는 특별한 규칙이 포함되어 있는 구문입니다.

사이트의 각 페이지는 두 개의 코드 파일로 표시됩니다.

- 첫 번째는 Razor 태그 파일인 `.cshtml` 파일입니다. 이 파일에는 표시 HTML과 일부 C# 논리가 포함되어 있습니다.

- 두 번째 파일은는 `.cs` C# 코드 숨김을 포함 하는 파일인 파일 `PageModel` 클래스입니다. 이 파일을 사용하면 HTTP 요청을 가로채고 해당 요청에 대한 일부 처리를 수행한 후 Razor 파일로 데이터를 전달할 수 있습니다.

### <a name="appsettingjson"></a>appsetting.json

ASP.NET용 구성 파일입니다.

### <a name="bundleconfigjson"></a>bundleconfig.json

bundleconfig.json은 사전 처리 구성입니다. 이 파일은 .css 및 .js 파일이 게시될 때 크기를 더 작게 만듭니다.

### <a name="programcs-and-startupcs"></a>Program.cs 및 Startup.cs

Program.cs 및 Startup.cs는 사이트의 웹 호스트를 구성하고 시작합니다.

## <a name="updating-your-website-using-razor"></a>Razor를 사용하여 웹 사이트 업데이트

웹 사이트에 대해 몇 가지 기본적인 변경을 수행하려고 합니다. 이 작업을 수행하려면 Razor 템플릿을 활용하여 웹앱을 사용자 지정하는 방법에 대한 기본적인 이해가 있어야 합니다.

## <a name="what-is-razor"></a>Razor란?

Razor는 C#을 사용하여 동적 웹 페이지를 만드는 데 사용되는 ASP.NET 구문입니다. 서버가 Razor 페이지를 읽으면 HTML을 렌더링하기 전에 C# 코드가 실행됩니다. 이렇게 하면 동적 콘텐츠를 신속하게 생성할 수 있습니다.

Razor는 `@` 지시문을 사용하여 페이지를 처리하는 방법을 ASP.NET에 알려 줍니다.

예를 들어 살펴보겠습니다의 코드는 `Contact.cshtml` 페이지:

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

- `@page` 지시문 ASP.NET Razor 페이지를 사용 하 여이 파일을 처리 하는 데 지정 되어 있습니다.
- `@model` 지시문은 이 Razor 페이지를 `ContactModel` C# 클래스와 연결하도록 ASP.NET에 알려 줍니다.

또한 Razor는 `@` 기호를 사용하여 코드와 HTML 간에 전환합니다. 살펴보면 위의 코드 조각에서 보면 `@{ ... }`합니다. 이것이 **Razor 코드 블록**입니다. 이 코드는 _실행되지만 렌더링되지 않습니다_.

코드 명령문의 출력을 렌더링하려면 C# 식 앞에 `@`를 사용합니다. 이에 대한 두 가지 예가 `<h2>` 및 `<h3>` 태그 위의 코드 블록에 있습니다.

## <a name="publish-your-updates"></a>업데이트 게시

웹 사이트를 변경한 후에는 Azure에 게시하려고 합니다. 이 프로세스는 처음에 게시한 방법과 비슷합니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.

1. 웹 사이트 이름과 웹 배포가 차례로 표시됩니다. 웹 사이트 AlpineSkiHouse42, 명명 된 경우 표시 됩니다 **AlpineSkiHouse42-웹 배포** 사용 가능한 옵션입니다. 해당 옵션을 선택하면 Azure에서 사이트가 업데이트됩니다.

## <a name="summary"></a>요약

웹 사이트를 만들고 게시하는 것은 좋은 웹 사이트를 만드는 첫 번째 단계에 불과합니다. 콘텐츠 추가를 시작하면 사이트를 업데이트해야 합니다. 처음에 사이트를 Azure에 게시한 후에는 언제든 솔루션 탐색기에서 업데이트할 수 있습니다.
