<span data-ttu-id="38aa9-101">이제 콘텐츠를 준비하고 거의 가동 중지 시간 없이 배포하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-101">Now, let's see how we can stage our content and deploy with little or no downtime.</span></span>

## <a name="what-is-a-deployment-slot"></a><span data-ttu-id="38aa9-102">배포 슬롯이란?</span><span class="sxs-lookup"><span data-stu-id="38aa9-102">What is a deployment slot?</span></span>

<span data-ttu-id="38aa9-103">배포 슬롯은 자체 콘텐츠, 구성 및 고유한 호스트 이름이 있는 **독립** 웹앱입니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-103">A deployment slot is an **independent** Web App with its own content, configuration, and even a unique host name.</span></span> <span data-ttu-id="38aa9-104">따라서 다른 웹앱처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-104">Therefore, it functions like any other Web App.</span></span>

> <span data-ttu-id="38aa9-105">Azure는 배포 슬롯 사용에 추가 요금을 부과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-105">Azure doesn't charge you extra for using deployment slots!</span></span>

<span data-ttu-id="38aa9-106">각 배포 슬롯은 고유한 URL에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-106">Each deployment slot is accessible from its unique URL.</span></span> <span data-ttu-id="38aa9-107">예를 들어 이름이 `BESTBIKE`인 **스테이징** 배포 슬롯을 추가했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-107">For instance, let's say I've added a **staging** deployment slot with the name `BESTBIKE`.</span></span> <span data-ttu-id="38aa9-108">응용 프로그램 및 배포 슬롯의 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-108">The URLs for the application and deployment slot are:</span></span>

- https://BESTBIKE.azurewebsites.net/
- https://BESTBIKE-staging.azurewebsites.net/

## <a name="why-are-deployment-slots-useful"></a><span data-ttu-id="38aa9-109">배포 슬롯이 유용한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="38aa9-109">Why are deployment slots useful?</span></span>

<span data-ttu-id="38aa9-110">FTP, 웹 배포, Git 또는 다른 방법을 통해 웹앱을 배포하는지와 관계없이, 기존 방법으로 웹앱을 배포할 경우 다음과 같은 약점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-110">Deploying your Web App in the traditional way, whether it be via FTP, Web Deploy, Git, or another way, has some weaknesses:</span></span>

- <span data-ttu-id="38aa9-111">배포가 완료된 후 웹앱이 다시 시작되어 응용 프로그램에 대한 **콜드 부팅**이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-111">After the deployment completes, the Web App might restart, causing a **cold start** for the application.</span></span> <span data-ttu-id="38aa9-112">응용 프로그램에 대한 첫 번째 요청이 더 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-112">The first request to the application will be slower.</span></span>

- <span data-ttu-id="38aa9-113">잠재적으로 *잘못*된 버전의 웹앱을 배포하고 있으므로 클라이언트에 릴리스하기 전에 프로덕션에서 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-113">Potentially, you are deploying a *bad* version of your Web App, and you should test it (in production) before releasing it to your client.</span></span>

<span data-ttu-id="38aa9-114">여기서 배포 슬롯이 작동하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-114">This is where deployment slots come into play.</span></span> <span data-ttu-id="38aa9-115">웹앱을 **스테이징** 배포 슬롯으로 변경하고 **프로덕션** 배포 슬롯에 액세스하는 사용자에게 영향을 주지 않고 변경 내용을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-115">You can make changes to your Web App to a **staging** deployment slot and test the changes without impacting users who are accessing the **production** deployment slot.</span></span> <span data-ttu-id="38aa9-116">새 기능을 프로덕션으로 이동할 준비가 되면 **가동 중지 시간 없이** 스테이징 및 프로덕션 슬롯만 **교환**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-116">When you are ready to move the new features into production, you can just **swap** the staging and production slots with **no downtime**.</span></span>

<span data-ttu-id="38aa9-117">배포 슬롯을 사용하는 또 다른 이점은 프로덕션 슬롯으로 교환하기 전에 스테이징 슬롯에서 응용 프로그램을 **준비**할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-117">Another benefit of using deployment slots is that you can **warm up** your application in a staging slot before swapping it into the production slot.</span></span> <span data-ttu-id="38aa9-118">**콜드 부팅** 지연 및 긴 초기화 코드가 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-118">You will avoid the delays of a **cold start** and the lengthy initialization code.</span></span>

<span data-ttu-id="38aa9-119">마지막으로 응용 프로그램의 새 버전이 예상대로 작동하지 않음을 알게 되면 이전 배포 슬롯으로 **다시 교환**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-119">Finally, you can **swap back** to the previous deployment slot if you realize that the new version of your application is not working as you expected.</span></span>

## <a name="what-is-automated-deployment"></a><span data-ttu-id="38aa9-120">자동화된 배포란?</span><span class="sxs-lookup"><span data-stu-id="38aa9-120">What is automated deployment?</span></span>

<span data-ttu-id="38aa9-121">자동화된 배포 또는 연속 통합은 최종 사용자에게 최소한의 영향을 주면서 빠르고 반복적인 패턴으로 새 기능 및 버그 수정을 푸시하는 데 사용되는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-121">Automated deployment, or continuous integration, is a process used to push out new features and bug fixes in a fast and repetitive pattern with minimal impact on end users.</span></span>

<span data-ttu-id="38aa9-122">Azure는 여러 원본에서 직접 자동화된 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-122">Azure supports automated deployment directly from several sources.</span></span> <span data-ttu-id="38aa9-123">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-123">The following options are available:</span></span>

- <span data-ttu-id="38aa9-124">**VSTS(Visual Studio Team Services)**: 코드를 VSTS에 푸시하고, 클라우드에서 코드를 빌드하고, 테스트를 실행하고, 코드에서 릴리스를 생성하고, 마지막으로 코드를 Azure 웹앱에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-124">**Visual Studio Team Services (VSTS)**: You can push your code to VSTS, build your code in the cloud, run the tests, generate a release from the code, and finally, push your code to an Azure Web App.</span></span>

- <span data-ttu-id="38aa9-125">**GitHub**: Azure는 GitHub에서 직접 자동화된 배포를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-125">**GitHub**: Azure supports automated deployment directly from GitHub.</span></span> <span data-ttu-id="38aa9-126">자동화된 배포를 위해 GitHub 리포지토리를 Azure에 연결하면 GitHub의 프로덕션 분기에 푸시하는 모든 변경 내용이 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-126">When you connect your GitHub repository to Azure for automated deployment, any changes you push to your production branch on GitHub will be automatically deployed for you.</span></span>

- <span data-ttu-id="38aa9-127">**Bitbucket**: GitHub와 유사하므로 Bitbucket을 사용하여 자동화된 배포를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-127">**Bitbucket**: With its similarities to GitHub, you can configure an automated deployment with Bitbucket.</span></span>

- <span data-ttu-id="38aa9-128">**OneDrive**: OneDrive 계정의 파일을 변경할 때 Azure에서 변경을 자동으로 감지하고 웹앱 파일의 모든 변경 내용을 다시 풀하도록 OneDrive 계정을 Web Apps와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-128">**OneDrive**: You can connect your OneDrive account with Web Apps so that when you change any file on your OneDrive account, Azure will automatically detect it and pull back any changes on the web app files.</span></span> <span data-ttu-id="38aa9-129">이 옵션은 정적 웹 사이트에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-129">This is a great option for static websites.</span></span> <span data-ttu-id="38aa9-130">이 작업은 Azure에 모든 변경 내용을 반영하는 로컬 파일 시스템을 원활하게 즉시 처리하고 있다는 느낌을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-130">It will give you the feeling that you are dealing with a local file system that reflects any changes on Azure, smoothly and instantly.</span></span>

- <span data-ttu-id="38aa9-131">**Dropbox**: OneDrive와 유사하게 웹앱 파일을 Dropbox 계정에서 호스팅하고 Azure 웹앱을 통해 자동으로 푸시하고 배포되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-131">**Dropbox**: Similar to OneDrive, you can host your web app files in a Dropbox account and have them automatically push and be deployed over an Azure Web App.</span></span>

- <span data-ttu-id="38aa9-132">**외부 리포지토리**: 외부 Git 리포지토리를 사용하여 자동화된 배포를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-132">**External repository**: You can configure automated deployment with any external Git repository.</span></span>

### <a name="non-automated-deployment-to-azure"></a><span data-ttu-id="38aa9-133">Azure에 자동화되지 않은 배포</span><span class="sxs-lookup"><span data-stu-id="38aa9-133">Non-automated deployment to Azure</span></span>

<span data-ttu-id="38aa9-134">코드를 Azure에 수동으로 푸시하는 데 사용할 수 있는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-134">There are a few options that you can use to manually push your code to Azure:</span></span>

- <span data-ttu-id="38aa9-135">**FTP/S**: FTP 또는 FTPS는 코드를 호스팅 환경에 푸시하는 기존 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-135">**FTP/S**: FTP or FTPS is a traditional way of pushing your code to any hosting environment.</span></span> <span data-ttu-id="38aa9-136">더 이상 권장되지 않지만 여전히 사용할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-136">Despite the fact that it is not recommended anymore, you can still make use of it.</span></span>

- <span data-ttu-id="38aa9-137">**웹 배포/IDE**: Visual Studio IDE를 사용하여 웹앱을 Azure에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-137">**Web Deploy/IDE**: You can use the Visual Studio IDE to publish your web app to Azure.</span></span> <span data-ttu-id="38aa9-138">Visual Studio 게시 메커니즘은 웹 배포 기술을 사용하여 코드를 Azure에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-138">The Visual Studio publishing mechanism can make use of Web Deploy technology to push your code to Azure.</span></span>

- <span data-ttu-id="38aa9-139">**Git**: Azure는 응용 프로그램에 대한 **로컬 Git 리포지토리**를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-139">**Git**: Azure maintains a **local Git repository** for your application.</span></span> <span data-ttu-id="38aa9-140">코드를 Git에 직접 **커밋**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-140">You can **commit** your code directly to it.</span></span>

> <span data-ttu-id="38aa9-141">이 모듈에서는 Git을 사용하여 자동화되지 않은 배포를 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-141">In this module, we are going to perform a non-automated deployment using Git.</span></span>

## <a name="summary"></a><span data-ttu-id="38aa9-142">요약</span><span class="sxs-lookup"><span data-stu-id="38aa9-142">Summary</span></span>

<span data-ttu-id="38aa9-143">Azure는 현재 워크플로에 더 잘 맞을 수 있도록 코드를 업로드하는 여러 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-143">Azure provides multiple ways to upload your code to help it better fit in with your current workflow.</span></span> <span data-ttu-id="38aa9-144">배포 슬롯을 사용하여 사용자의 가동 중단 시간을 방지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38aa9-144">You can also use deployment slots to help prevent downtime for your users.</span></span>
