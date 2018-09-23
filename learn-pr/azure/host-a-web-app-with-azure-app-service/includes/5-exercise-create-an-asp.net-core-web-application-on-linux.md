<span data-ttu-id="347ab-101">이 단원에서는 ASP.NET Core 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-101">In this unit, you will create an ASP.NET Core web app.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="347ab-102">새 웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="347ab-102">Create a new web project</span></span>

<span data-ttu-id="347ab-103">.NET CLI 도구의 핵심은 `dotnet` 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-103">The heart of the .NET CLI tools is the `dotnet` command line tool.</span></span> <span data-ttu-id="347ab-104">이 명령을 사용하여 새 ASP.NET Core 웹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-104">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="347ab-105">오른쪽의 Cloud Shell에서 새 ASP.NET Core MVC 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-105">In the Cloud Shell on the right, create a new ASP.NET Core MVC application.</span></span> <span data-ttu-id="347ab-106">"BestBikeApp"이라는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-106">Name it "BestBikeApp".</span></span>

```bash
dotnet new mvc --name BestBikeApp
```

<span data-ttu-id="347ab-107">이 명령은 "BestBikeApp"이라는 새 폴더를 만들어서 프로젝트를 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-107">The command will create a new folder named "BestBikeApp" to hold your project.</span></span> <span data-ttu-id="347ab-108">여기서 `cd`는 응용 프로그램을 빌드하고 실행하여 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-108">`cd` there, then build and run the application to verify it is complete.</span></span>

```bash
cd BestBikeApp
dotnet run
```

<span data-ttu-id="347ab-109">다음과 유사한 결과를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-109">You should get something like:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

<span data-ttu-id="347ab-110">출력은 앱을 시작한 후에 발생하는 상황을 설명합니다. 응용 프로그램이 실행 중이고 포트 5000에서 수신 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-110">The output describes the situation after starting your app: the application is running and listening at port 5000.</span></span>

<span data-ttu-id="347ab-111">고유한 머신에서 앱을 실행한 경우 http://localhost:5000에 대해 브라우저를 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-111">If were running the app on our own machine we'd be able to open a browser to http://localhost:5000.</span></span> <span data-ttu-id="347ab-112">Azure Cloud Shell에서 작업하므로 공용 엔드포인트를 포함하는 위치에 앱을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-112">Since we're on Azure Cloud Shell, we'll need to deploy the app to somewhere with a public endpoint.</span></span> <span data-ttu-id="347ab-113">앞에서 만든 App Service 인스턴스가 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="347ab-113">The App Service instance we created earlier is perfect for that.</span></span>