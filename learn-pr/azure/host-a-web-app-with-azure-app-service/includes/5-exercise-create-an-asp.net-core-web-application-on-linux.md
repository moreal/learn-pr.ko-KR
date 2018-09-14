<span data-ttu-id="a08f3-101">이 단위에 ASP.NET Core 웹 앱을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-101">In this unit, you will create an ASP.NET Core web app.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="a08f3-102">새 웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a08f3-102">Create a new web project</span></span>

<span data-ttu-id="a08f3-103">.NET CLI 도구의 핵심은는 `dotnet` 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-103">The heart of the .NET CLI tools is the `dotnet` command line tool.</span></span> <span data-ttu-id="a08f3-104">이 명령을 사용하여 새 ASP.NET Core 웹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-104">Using this command, you will create a new ASP.NET Core web project.</span></span>

1. <span data-ttu-id="a08f3-105">오른쪽에서 Cloud Shell에서 새 ASP.NET Core MVC 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-105">In the Cloud Shell on the right, create a new ASP.NET Core MVC application.</span></span> <span data-ttu-id="a08f3-106">"BestBikeApp" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-106">Name it "BestBikeApp".</span></span>

```bash
dotnet new mvc -name BestBikeApp
```

1. <span data-ttu-id="a08f3-107">명령은 "BestBikeApp" 라는 새 폴더를 만듭니다. 프로젝트를 보관 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-107">The command will create a new folder named "BestBikeApp" to hold your project.</span></span> <span data-ttu-id="a08f3-108">해당 폴더를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-108">Change into that folder.</span></span>

1. <span data-ttu-id="a08f3-109">빌드 및 완료 되었는지 확인 하려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-109">Build and run the application to verify it is complete.</span></span>

```bash
dotnet run
```

<span data-ttu-id="a08f3-110">같은 결과 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-110">You should get something like:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

<span data-ttu-id="a08f3-111">출력 앱을 시작한 후 상황에 설명 합니다: 응용 프로그램을 실행 하 고 5000 포트에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-111">The output describes the situation after starting your app: the application is running and listening at port 5000.</span></span>

<span data-ttu-id="a08f3-112">브라우저를 열 수 없게 하겠습니다 고유한 컴퓨터에서 앱을 실행 된 경우 http://localhost:5000합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-112">If were running the app on our own machine we'd be able to open a browser to http://localhost:5000.</span></span> <span data-ttu-id="a08f3-113">위치에 앱을 배포 해야 하므로 Azure Cloud Shell에서 우리가 공용 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-113">Since we're on Azure Cloud Shell, we'll need to deploy the app to somewhere with a public endpoint.</span></span> <span data-ttu-id="a08f3-114">앞에서 만든 App Service 인스턴스를 가장 하는 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a08f3-114">The App Service instance we created earlier is perfect for that.</span></span>