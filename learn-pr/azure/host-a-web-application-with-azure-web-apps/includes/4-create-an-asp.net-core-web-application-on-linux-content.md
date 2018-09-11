<span data-ttu-id="ebded-101">웹 응용 프로그램을 빌드하기 위해 오픈 소스 기술을 사용하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-101">You've decided to use an open-source technology for building your web application.</span></span> <span data-ttu-id="ebded-102">ASP.NET Core는 플랫폼 간 및 오픈 소스 프레임워크임을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-102">You know that ASP.NET Core is a cross-platform and open-source framework.</span></span> <span data-ttu-id="ebded-103">ASP.NET Core를 사용하여 Linux 환경에서 웹앱을 개발하기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-103">You decide to develop your web app in a Linux environment using ASP.NET Core!</span></span>

<span data-ttu-id="ebded-104">Azure의 Web Apps를 사용하면 원하는 웹 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-104">Web Apps in Azure allows you to use your favorite web technology.</span></span> <span data-ttu-id="ebded-105">Node.js, PHP 또는 .NET Core 중 어떤 기술에 가장 편안하든 관계없이 Web Apps가 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-105">Whether you're most comfortable with Node.js, PHP, or .NET Core, Web Apps will work for you.</span></span>

<span data-ttu-id="ebded-106">여기서는 .NET CLI(명령줄 인터페이스)를 사용하여 ASP.NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-106">Here, you will create an ASP.NET Core application using the .NET command-line interface (CLI).</span></span>

## <a name="what-is-aspnet-core"></a><span data-ttu-id="ebded-107">ASP.NET Core란?</span><span class="sxs-lookup"><span data-stu-id="ebded-107">What is ASP.NET Core?</span></span>

<span data-ttu-id="ebded-108">ASP.NET Core는 최신 클라우드 기반, 인터넷 연결 응용 프로그램을 빌드하기 위한 플랫폼 간 오픈 소스 프레임워크인 Microsoft의 인기 있는 ASP.NET 웹 프레임워크의 가장 진화된 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-108">ASP.NET Core is the latest evolution of Microsoft's popular ASP.NET web framework, a cross-platform, open-source framework for building modern, cloud-based, and internet-connected applications.</span></span>

<span data-ttu-id="ebded-109">ASP.NET Core 응용 프로그램은 .NET Core Framework 또는 기존의 전체 .NET Framework를 대상으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-109">ASP.NET Core applications can be written to target the .NET Core Framework or the existing, full .NET Framework.</span></span>

<span data-ttu-id="ebded-110">플랫폼 간 및 오픈 소스 프레임워크가 되면 Windows, macOS 및 Linux를 비롯한 다양한 플랫폼에서 ASP.NET Core 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-110">Being a cross-platform and open-source framework, you can build ASP.NET Core apps on a variety of platforms, including Windows, macOS, and Linux.</span></span> <span data-ttu-id="ebded-111">지금까지 Microsoft는 Windows 및 macOS 환경용 Visual Studio IDE를 둘 다 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-111">Thus far, Microsoft offers the Visual Studio IDE for both Windows and macOS environments.</span></span> <span data-ttu-id="ebded-112">또한 Visual Studio Code 편집기는 플랫폼 간 편집기로 이러한 환경과 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-112">In addition, the Visual Studio Code editor is cross-platform and compatible with them.</span></span>

><span data-ttu-id="ebded-113">다양한 플랫폼에서 ASP.NET Core 응용 프로그램 빌드를 지원하기 위해 Microsoft는 풍부하고 일관적인 플랫폼 간 API 집합을 사용하여 응용 프로그램을 빌드, 테스트 및 게시하는 데 도움이 되는 .NET Core CLI 도구를 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-113">To support building ASP.NET Core applications on different platforms, Microsoft introduced the .NET Core CLI tools to help you build, test, and publish your applications using a rich, consistent, and cross-platform set of APIs.</span></span>

<span data-ttu-id="ebded-114">ASP.NET Core를 사용하면 웹앱과 서비스, IoT 앱 및 모바일 백 엔드를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-114">With ASP.NET Core, you can build web apps and services, IoT apps, and mobile back ends.</span></span> <span data-ttu-id="ebded-115">ASP.NET Core 응용 프로그램은 클라우드 또는 온-프레미스에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-115">ASP.NET Core applications can be hosted either in the cloud or on-premises.</span></span>

<span data-ttu-id="ebded-116">의도적으로 ASP.NET Core는 응용 프로그램 코드를 실행하는 런타임 환경 및 포함된 웹 서버로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-116">By design, ASP.NET Core consists of an embedded web server and a runtime environment that runs the application code.</span></span> <span data-ttu-id="ebded-117">응용 프로그램 코드는 더 작은 모듈과 패키지를 사용하는 재구성된 ASP.NET MVC 프레임워크를 사용하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-117">The application code is written using a reworked ASP.NET MVC framework that relies on smaller modules and packages.</span></span> <span data-ttu-id="ebded-118">결과로 클라우드 환경을 통해 쉽게 유지 관리 및 호스트할 수 있는 보다 작은 웹 응용 프로그램 청사진이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-118">The result is a smaller web application blueprint that is easy to maintain and host over cloud environments.</span></span>

![ASP.NET Core 아키텍처](../media-draft/4-asp-net-core-architecture.png)

<span data-ttu-id="ebded-120">ASP.NET Core 응용 프로그램은 **dotnet** 드라이버 도구를 통해 호출되는 독립 실행형 **콘솔** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-120">ASP.NET Core applications are standalone **console** applications invoked through the **dotnet** driver tool.</span></span> <span data-ttu-id="ebded-121">ASP.NET Core 응용 프로그램은 IIS 작업자 프로세스에 로드되지 않고, 외부 콘솔 응용 프로그램을 실행하는 **AspNetCoreModule**이라는 네이티브 IIS 모듈을 통해 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-121">ASP.NET Core applications are not loaded into the IIS worker process, but rather, are loaded through a native IIS module called **AspNetCoreModule** that executes the external console application.</span></span>

## <a name="how-to-create-an-aspnet-core-web-project"></a><span data-ttu-id="ebded-122">ASP.NET Core 웹 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ebded-122">How to create an ASP.NET Core web project</span></span>

<span data-ttu-id="ebded-123">새 ASP.NET Core 프로젝트를 만들기 위한 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-123">There are a few options for creating a new ASP.NET Core project:</span></span>

- <span data-ttu-id="ebded-124">Visual Studio(Windows 및 macOS 버전) 템플릿을 사용하여 새 프로젝트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-124">You can use Visual Studio (Windows and macOS versions) templates to generate a new project.</span></span> <span data-ttu-id="ebded-125">Visual Studio에서는 웹 프로젝트를 만드는 데 사용할 수 있는 다양한 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-125">Visual Studio offers a variety of templates that you can use to create web projects.</span></span> <span data-ttu-id="ebded-126">예를 들어 **빈** 템플릿을 사용하면 기본 설정을 사용하여 기본적인 ASP.NET Core 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-126">For instance, you can use the **Empty** template to create a bare-bones ASP.NET Core project with the basic setup.</span></span> <span data-ttu-id="ebded-127">또한 **웹 응용 프로그램(Modal-View-Controller)** 템플릿을 사용하면 응용 프로그램 코딩을 시작하는 데 도움이 될 수 있는 샘플 **컨트롤러** 및 **보기**를 사용하여 모든 기능을 갖춘 ASP.NET Core MVC 응용 프로그램을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-127">In addition, you can use the **Web Application (Modal-View-Controller)** template to generate a full-fledged ASP.NET Core MVC application, with sample **controllers** and **views** that can help you start coding your application.</span></span> <span data-ttu-id="ebded-128">가장 최근 제공된 템플릿은 기존 MVC 프로젝트 구조가 아닌 Razor 페이지를 기반으로 ASP.NET Core 프로젝트를 만드는 데 사용되는 **웹 응용 프로그램** 프로젝트 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-128">The latest arrival is the **Web Application** project template that is used to create an ASP.NET Core project based on Razor pages and not on the traditional MVC project structure.</span></span>

- <span data-ttu-id="ebded-129">.NET Core CLI 도구를 사용하여 새 ASP.NET Core 프로젝트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-129">You can use the .NET Core CLI tools to generate a new ASP.NET Core project.</span></span> <span data-ttu-id="ebded-130">Microsoft는 Visual Studio 및 CLI 도구에 둘 다 해당하는 거의 공통적인 ASP.NET Core 프로젝트 템플릿 집합을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-130">Microsoft maintains an almost common set of ASP.NET Core project templates for both Visual Studio and the CLI tools.</span></span> <span data-ttu-id="ebded-131">CLI 도구의 유일한 차이점은 새 ASP.NET Core 프로젝트를 만들려면 명령을 입력해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-131">The only difference with the CLI tools is that you need to type commands to create a new ASP.NET Core project.</span></span>
> <span data-ttu-id="ebded-132">.NET CLI 도구는 **템플릿 엔진**을 사용하여 다양한 프로젝트 템플릿을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-132">The .NET CLI tools make use of the **templating engine** to support different project templates.</span></span>  <span data-ttu-id="ebded-133">자세한 내용을 보려면 .NET CLI 도구에서 내부적으로 사용하는 [템플릿 엔진](https://github.com/dotnet/templating)에 대한 GitHub 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ebded-133">To learn more, visit the GitHub repository for the [templating engine](https://github.com/dotnet/templating) used internally by the .NET CLI tools.</span></span>

<span data-ttu-id="ebded-134">위의 템플릿 엔진은 ASP.NET Core 프로젝트를 생성하기 위한 상위 도구로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-134">The above are considered the top tools for generating ASP.NET Core projects.</span></span> <span data-ttu-id="ebded-135">그러나 검색하고 탐색할 수 있는 더 많은 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-135">However, there are more tools out there that you can search for and explore.</span></span>

<span data-ttu-id="ebded-136">서로 다른 도구에서 생성되는 프로젝트는 약간 다를 수 있지만, 모두 유효하고 최적화된 ASP.NET Core 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-136">It's worth mentioning that the projects generated by the different tools can be slightly different, however, they all generate valid and optimized ASP.NET Core projects.</span></span>

## <a name="net-cli-tools"></a><span data-ttu-id="ebded-137">.NET CLI 도구</span><span class="sxs-lookup"><span data-stu-id="ebded-137">.NET CLI tools</span></span>

<span data-ttu-id="ebded-138">.NET Core CLI라고도 하는 .NET CLI 도구는 패키지를 만들고 복원하기 위한 명령과</span><span class="sxs-lookup"><span data-stu-id="ebded-138">The .NET CLI tools, also known as .NET Core CLI, is a cross-platform tool that provides commands for creating and restoring packages, and for building, running.</span></span> <span data-ttu-id="ebded-139">모든 기능을 갖춘 IDE 없이 명령줄에서 .NET 응용 프로그램을 빌드, 실행 및 게시할 수 있는 명령을 제공하는 플랫폼 간 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-139">and publishing .NET applications from the command line without the need for a full-featured IDE.</span></span>

<span data-ttu-id="ebded-140">.NET CLI는 .NET Core SDK의 일부로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-140">The .NET CLI is installed as part of the .NET Core SDK.</span></span> <span data-ttu-id="ebded-141">여러 버전의 CLI가 동일한 머신에 공존하고 나란히 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-141">Multiple versions of the CLI can coexist on the same machine and run side by side.</span></span>

<span data-ttu-id="ebded-142">.NET CLI 사용을 시작하려면 앱을 개발하는 데 사용 중인 환경인 Windows, macOS 또는 Linux를 기준으로 관련된 .NET Core SDK를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-142">To start using the .NET CLI, you need to install the relevant .NET Core SDK with respect to the environment that you are using to develop your app: Windows, macOS, or Linux.</span></span> <span data-ttu-id="ebded-143">[.NET 다운로드](https://www.microsoft.com/net/download?initial-os=linux)로 이동하고 Linux용 .NET Core SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-143">Go to [.NET Downloads](https://www.microsoft.com/net/download?initial-os=linux) and grab the .NET Core SDK for Linux.</span></span> <span data-ttu-id="ebded-144">.NET CLI에서 제공하는 다양한 명령을 설명하기 위해 VMware Workspace Player 14를 사용하여 Windows 10 맨 위에서 실행되는 Ubuntu 18.04 OS를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-144">I am using an Ubuntu 18.04 OS running on top Windows 10 using VMware Workspace Player 14 to demonstrate the different commands offered by .NET CLI.</span></span>

<span data-ttu-id="ebded-145">명령줄을 열고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-145">Open the command line and type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="ebded-146">이 명령은 설치된 .NET CLI 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-146">This command displays the version of the .NET CLI installed.</span></span>

<span data-ttu-id="ebded-147">내 머신에서 위 명령을 실행하면 `2.1.302`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-147">Running the above command on my machine displays this: `2.1.302`.</span></span>

<span data-ttu-id="ebded-148">.NET CLI의 인기 있는 몇 가지 명령을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-148">Let us start exploring some of the popular commands of the .NET CLI.</span></span>

<span data-ttu-id="ebded-149">*dotnet* 명령에는 다음과 같은 일반 구문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-149">The *dotnet* command has the following general syntax:</span></span>

```console
dotnet [verb] [arguments]
```

<span data-ttu-id="ebded-150">동사는 실행할 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-150">The verb represents the action to execute.</span></span> <span data-ttu-id="ebded-151">인수는 실행하기 위해 동사에 필요한 입력 인수 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-151">The arguments represent the list of input arguments that the verb requires in order to execute.</span></span>

<span data-ttu-id="ebded-152">*dotnet* 사용법 및 사용 가능한 모든 *동사* 목록에 대한 도움말을 보려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-152">To get help on the *dotnet* usage and list all of the *verbs* available, and other related information, type the following command:</span></span>

```console
dotnet --help
```

<span data-ttu-id="ebded-153">이 명령은 다음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-153">This command displays the following:</span></span>

```console
.NET Command Line Tools (2.1.302)
Usage: dotnet [runtime-options] [path-to-application]
Usage: dotnet [sdk-options] [command] [arguments] [command-options]

path-to-application:
  The path to an application .dll file to execute.

SDK commands:
  new              Initialize .NET projects.
  restore          Restore dependencies specified in the .NET project.
  run              Compiles and immediately executes a .NET project.
  build            Builds a .NET project.
  publish          Publishes a .NET project for deployment (including the runtime).
  test             Runs unit tests using the test runner specified in the project.

...
```

<span data-ttu-id="ebded-154">**SDK 명령**에서 .NET Core SDK에 실행할 수 있는 전체 명령 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-154">Under the **SDK commands**, you can see the entire list of commands that you can execute against the .NET Core SDK.</span></span>

<span data-ttu-id="ebded-155">항상 가장 유용한 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-155">The most useful commands at all times are the following:</span></span>

- <span data-ttu-id="ebded-156">**dotnet new**: 이 명령은 새 .NET 응용 프로그램을 스캐폴드/생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-156">**dotnet new**: This command is used to scaffold/generate a new .NET application.</span></span>

- <span data-ttu-id="ebded-157">**dotnet restore**: 이 명령은 응용 프로그램에서 참조하는 모든 패키지를 복원/다운로드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-157">**dotnet restore**: This command is used to restore/download all packages that are referenced by the application.</span></span>

- <span data-ttu-id="ebded-158">**dotnet run**: 이 명령은 .NET 응용 프로그램을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-158">**dotnet run**: This command is used to run your .NET application.</span></span>

<span data-ttu-id="ebded-159">이제 특정 명령 사용 방법에 대한 지원을 받으려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-159">Now, to get assistance on how to use a specific command, you can type the following:</span></span>

```console
dotnet run --help
```

<span data-ttu-id="ebded-160">이 명령은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-160">This command results in:</span></span>

```console
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.
  -n, --name          The name for the output being created. If no name is specified, the name of the current directory is used.
  -o, --output        Location to place the generated output.
  -i, --install       Installs a source or a template pack.
  -u, --uninstall     Uninstalls a source or a template pack.
  --nuget-source      Specifies a NuGet source to use during install.
  --type              Filters templates based on available types. Predefined values are "project", "item" or "other".
  --force             Forces content to be generated even if it would change existing files.
  -lang, --language   Filters templates based on language and specifies the language of the template to create.


Templates                                         Short Name         Language          Tags
----------------------------------------------------------------------------------------------------------------------------
Console Application                               console            [C#], F#, VB      Common/Console
Class library                                     classlib           [C#], F#, VB      Common/Library
...

Razor Page                                        page               [C#]              Web/ASP.NET
MVC ViewImports                                   viewimports        [C#]              Web/ASP.NET
MVC ViewStart                                     viewstart          [C#]              Web/ASP.NET
ASP.NET Core Empty                                web                [C#], F#          Web/Empty
ASP.NET Core Web App (Model-View-Controller)      mvc                [C#], F#          Web/MVC
ASP.NET Core Web App                              razor              [C#]              Web/MVC/Razor Pages
ASP.NET Core with Angular                         angular            [C#]              Web/MVC/SPA
...

Solution File                                     sln                                  Solution

Examples:
    dotnet new mvc --auth Individual
    dotnet new webapi
    dotnet new --help
```

<span data-ttu-id="ebded-161">이 명령은 `dotnet new` 명령과 함께 사용할 수 있는 모든 사용 가능한 옵션을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-161">This command lists all the available options that you can use with the `dotnet new` command.</span></span> <span data-ttu-id="ebded-162">또한 다음 .NET 응용 프로그램을 생성하는 데 사용할 수 있는 사용 가능한 모든 프로젝트 템플릿을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-162">Also, it lists all the available project templates that you can use to generate your next .NET application.</span></span> <span data-ttu-id="ebded-163">마지막으로 섹션에는 명령을 사용하여 새 .NET 응용 프로그램을 생성하는 방법에 대한 예제가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-163">Finally, a section shows examples on how to use the command to generate a new .NET application.</span></span>

<span data-ttu-id="ebded-164">.NET CLI에서 사용 가능한 모든 명령에 `--help` 인수를 사용하면 나머지 명령을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-164">You can learn the rest of the commands by using the `--help` argument for any command available in the .NET CLI.</span></span>

## <a name="aspnet-core-installation-on-linux-environment"></a><span data-ttu-id="ebded-165">Linux 환경의 ASP.NET Core 설치</span><span class="sxs-lookup"><span data-stu-id="ebded-165">ASP.NET Core installation on Linux environment</span></span>

<span data-ttu-id="ebded-166">ASP.NET Core의 최신 및 최대 버전은 v2.1입니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-166">The latest and greatest version of ASP.NET Core is v2.1.</span></span> <span data-ttu-id="ebded-167">일반적으로 ASP.NET Core는 .NET Core SDK의 일부로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-167">In general, ASP.NET Core ships as part of the .NET Core SDK.</span></span> <span data-ttu-id="ebded-168">따라서 머신에 .NET Core SDK를 설치하면 ASP.NET Core 웹앱을 포함한 .NET Core 응용 프로그램으로 개발을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-168">Therefore, by installing the .NET Core SDK on your machine, you can start developing with any .NET Core application, including ASP.NET Core web apps.</span></span>

<span data-ttu-id="ebded-169">이 데모에서는 VMware Workstation Player의 지원을 통해 Windows 10에서 실행되는 Ubuntu 18.04 OS를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-169">For this demonstration, I am using an Ubuntu 18.04 OS running on Windows 10, with the help of VMware Workstation Player.</span></span>

<span data-ttu-id="ebded-170">.NET Core SDK를 다운로드하려면 [.NET 다운로드](https://www.microsoft.com/net/download) 홈페이지를 방문해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-170">To download the .NET Core SDK, you need to visit the [.NET Downloads](https://www.microsoft.com/net/download) home page.</span></span> <span data-ttu-id="ebded-171">이 페이지에는 다양한 플랫폼(Windows, Linux 및 macOS)에서 .NET Core SDK를 다운로드하는 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-171">The page contains links to download the .NET Core SDK on different platforms: Windows, Linux, and macOS.</span></span>

<span data-ttu-id="ebded-172">**Linux** 탭을 찾아 클릭합니다. 다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-172">Locate and click on the **Linux** tab. You have two options:</span></span>

- <span data-ttu-id="ebded-173">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="ebded-173">.NET Core SDK</span></span>
- <span data-ttu-id="ebded-174">.NET Core 런타임</span><span class="sxs-lookup"><span data-stu-id="ebded-174">.NET Core Runtime</span></span>

<span data-ttu-id="ebded-175">.NET Core 런타임은 이미 .NET Core SDK에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-175">The .NET Core Runtime is already contained inside the .NET Core SDK.</span></span> <span data-ttu-id="ebded-176">런타임은 응용 프로그램을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-176">The runtime is used to run an application.</span></span> <span data-ttu-id="ebded-177">개발, 테스트, 실행 및 게시하기 위한 모든 도구가 .NET Core SDK에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-177">All the tools to develop, test, run, and publish are inside the .NET Core SDK.</span></span> <span data-ttu-id="ebded-178">따라서 **.NET Core SDK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-178">Therefore, you will click on **.NET Core SDK**.</span></span>

<span data-ttu-id="ebded-179">Microsoft 웹 사이트는 다운로드 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-179">The Microsoft website redirects you to the download page.</span></span> <span data-ttu-id="ebded-180">여기서 **Linux 배포**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-180">There, you need to select the **Linux Distribution**.</span></span> <span data-ttu-id="ebded-181">이 경우에는 **Ubuntu 18.04**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-181">In my case, I will select **Ubuntu 18.04**.</span></span> <span data-ttu-id="ebded-182">선택 시 자동으로 Ubuntu 18.04에서 .NET Core SDK를 설치하는 방법에 대한 지침이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-182">Automatically, upon selection, the instructions on how to install .NET Core SDK on Ubuntu 18.04 is displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="ebded-183">요약</span><span class="sxs-lookup"><span data-stu-id="ebded-183">Summary</span></span>

<span data-ttu-id="ebded-184">웹 응용 프로그램을 빌드하려는 경우 많은 언어와 프레임워크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-184">When deciding to build a web application, you have a choice of many languages and frameworks.</span></span> <span data-ttu-id="ebded-185">Azure에서는 Node.js, PHP 또는 .NET Core와 같은 다양한 유형의 응용 프로그램을 호스트할 수 있어 더 쉽게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-185">Azure tries to make this choice easier by allowing you to host different types of applications, like Node.js, PHP, or .NET Core.</span></span> <span data-ttu-id="ebded-186">이 방법을 사용하여 웹 호스트의 요구 사항을 충족하기 위해 변경하는 대신 가장 편안한 언어와 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebded-186">This allows you to use the languages and frameworks that you're most comfortable with instead of changing to meet the needs of your web host.</span></span>