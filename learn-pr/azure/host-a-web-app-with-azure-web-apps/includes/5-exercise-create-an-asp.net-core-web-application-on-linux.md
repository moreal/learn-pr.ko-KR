<span data-ttu-id="2fe5e-101">이 단원에서는 Ubuntu 머신에서 .NET CLI를 사용하여 ASP.NET Core 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-101">In this unit, you will create an ASP.NET Core web app using the .NET CLI on an Ubuntu machine.</span></span>

## <a name="aspnet-core-installation-on-linux-environment"></a><span data-ttu-id="2fe5e-102">Linux 환경의 ASP.NET Core 설치</span><span class="sxs-lookup"><span data-stu-id="2fe5e-102">ASP.NET Core installation on Linux environment</span></span>

<span data-ttu-id="2fe5e-103">Microsoft [.NET 다운로드 페이지](https://www.microsoft.com/net/download)를 방문하여 .NET Core SDK 페이지에 언급된 것과 동일한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-103">Visit the Microsoft [.NET Downloads page](https://www.microsoft.com/net/download) and follow the same steps mentioned on the .NET Core SDK page.</span></span> <span data-ttu-id="2fe5e-104">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-104">They are below.</span></span> <span data-ttu-id="2fe5e-105">명령을 실행하려면 새 **터미널** 명령줄 인스턴스를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-105">In order to execute the commands, you need to open a new **Terminal** command-line instance.</span></span>

### <a name="register-microsoft-key-and-feed"></a><span data-ttu-id="2fe5e-106">Microsoft 키 및 피드 등록</span><span class="sxs-lookup"><span data-stu-id="2fe5e-106">Register Microsoft key and feed</span></span>

<span data-ttu-id="2fe5e-107">.NET을 설치하기 전에 Microsoft 키를 등록하고, 제품 리포지토리를 등록하고, 필수 종속성을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-107">Before installing .NET, you'll need to register the Microsoft key, register the product repository, and install the required dependencies.</span></span> <span data-ttu-id="2fe5e-108">머신당 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-108">This only needs to be done once per machine.</span></span>

```console
~$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
~$ sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-sdk"></a><span data-ttu-id="2fe5e-109">.NET SDK 설치</span><span class="sxs-lookup"><span data-stu-id="2fe5e-109">Install the .NET SDK</span></span>

<span data-ttu-id="2fe5e-110">설치할 수 있는 제품을 업데이트한 후 .NET SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-110">Update the products available for installation, then install the .NET SDK.</span></span>

<span data-ttu-id="2fe5e-111">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-111">At your command prompt, run the following commands:</span></span>

```console
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

<span data-ttu-id="2fe5e-112">설치 프로세스 중에 계정 암호를 입력하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-112">During the installation process, you might be asked to enter your account password.</span></span> <span data-ttu-id="2fe5e-113">암호를 입력하고 Enter 키를 눌러 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-113">Provide your password and hit Enter to continue.</span></span>

<span data-ttu-id="2fe5e-114">설치를 확인하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-114">To verify the installation, type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="2fe5e-115">표시되는 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-115">And the output displayed is:</span></span>

```console
2.1.302
```

<span data-ttu-id="2fe5e-116">이제 .NET Core SDK가 설치되었으므로 ASP.NET Core도 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-116">Now that you have the .NET Core SDK installed, you also have the ASP.NET Core installed.</span></span> <span data-ttu-id="2fe5e-117">.NET CLI를 사용하여 방금 알아본 명령을 통해 새 ASP.NET Core 프로젝트를 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-117">Let's see together how you can make use of the .NET CLI to create a new ASP.NET Core project using the commands we just learned.</span></span>

## <a name="open-a-terminal-window"></a><span data-ttu-id="2fe5e-118">터미널 창 열기</span><span class="sxs-lookup"><span data-stu-id="2fe5e-118">Open a Terminal window</span></span>

<span data-ttu-id="2fe5e-119">먼저 터미널 창을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-119">First, you need to open the Terminal window.</span></span> <span data-ttu-id="2fe5e-120">터미널 창에서 명령을 실행할 수 있고 이 창은 Windows 명령 프롬프트 창과 유사한 역할을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-120">The Terminal window allows you to execute commands, and has a similar role to the Windows Command Prompt window.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="2fe5e-121">새 웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2fe5e-121">Create a new web project</span></span>

<span data-ttu-id="2fe5e-122">.NET CLI 도구의 핵심은 *dotnet* 드라이버 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-122">The heart of the .NET CLI tools is the *dotnet* driver tool.</span></span> <span data-ttu-id="2fe5e-123">이 명령을 사용하여 새 ASP.NET Core 웹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-123">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="2fe5e-124">새 ASP.NET Core MVC 응용 프로그램을 만들려면 다음 명령을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-124">To create a new ASP.NET Core MVC application, you only need to type the following commands:</span></span>

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

<span data-ttu-id="2fe5e-125">위 명령은 *Documents* 루트 폴더로 이동한 후 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-125">The above commands navigate to the *Documents* root folder, and then create a new folder.</span></span> <span data-ttu-id="2fe5e-126">그런 다음 해당 폴더 내로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-126">Then, you go inside that folder.</span></span> <span data-ttu-id="2fe5e-127">마지막으로 .NET CLI 명령을 실행하여 모든 패키지가 복원된 새 ASP.NET MVC 응용 프로그램을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-127">Finally, you issue the .NET CLI command to generate a new ASP.NET MVC application with all the packages restored:</span></span>

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

<span data-ttu-id="2fe5e-128">이제 다음 명령을 실행하여 응용 프로그램을 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-128">All you have to do now is run the application by issuing this command:</span></span>

```console
dotnet run
```

<span data-ttu-id="2fe5e-129">‘터미널’에서 *dotnet* 명령은 실행 중인 앱에 대한 몇 가지 유용한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-129">In the *terminal*, the *dotnet* command displays some useful information for the running app:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Development
Content root path: /home/your-user/Documents/BestBikeApp
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="2fe5e-130">출력은 앱을 시작한 후에 발생하는 상황을 설명합니다. 응용 프로그램이 실행 중이고 포트 5001 및 5002에서 수신 대기 중입니다(HTTPS 사용).</span><span class="sxs-lookup"><span data-stu-id="2fe5e-130">The output describes the situation after starting your app: the application is running and listening at port 5001 and 5002 (via HTTPS).</span></span>

<span data-ttu-id="2fe5e-131">개발 모드의 머신에서 HTTPS를 로컬로 실행하려면 **자체 서명된 인증서**를 만들고 신뢰해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-131">In order to run HTTPS locally on the machine in development mode, you need to create and trust a **self-signed certificate**.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="2fe5e-132">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="2fe5e-132">Create a self-signed certificate</span></span>

<span data-ttu-id="2fe5e-133">다음 명령을 실행하여 개발 자체 서명 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-133">Run the command below to generate a development self-signed certificate:</span></span>

```console
dotnet dev-certs https -v
```

<span data-ttu-id="2fe5e-134">명령을 실행하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-134">Running the command returns the following:</span></span>

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a><span data-ttu-id="2fe5e-135">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2fe5e-135">Run the application</span></span>

<span data-ttu-id="2fe5e-136">이 데모에서는 Firefox 브라우저를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-136">For this demonstration, we are using the Firefox browser.</span></span>

<span data-ttu-id="2fe5e-137">브라우저를 열고 주소로 `http://localhost:5001`을 입력하여 응용 프로그램이 정상적으로 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-137">Open the browser and type in the address `http://localhost:5001` to verify the application is running successfully.</span></span>

![ASP.NET Core MVC 템플릿 기본 웹 페이지의 웹 브라우저 보기를 보여 주는 스크린샷.](../media/5-asp-core-mvc-default-template.PNG)

> [!NOTE]
> <span data-ttu-id="2fe5e-139">개발 자체 서명 인증서는 Firefox에서 확인할 수 없으므로 응용 프로그램 URL에 대한 **예외를 추가**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe5e-139">You need to **add an exception** for the application's URL because the development self-signed certificate couldn't be verified by Firefox.</span></span>
