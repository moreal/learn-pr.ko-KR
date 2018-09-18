<span data-ttu-id="24d1e-101">Azure DevOps 프로젝트의 즉시 사용 가능한 환경은 선택된 방법에 적합한 빌드 및 릴리스 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-101">The out of the box experience with an Azure DevOps Project creates build and release pipelines that make sense for the technologies picked.</span></span> <span data-ttu-id="24d1e-102">이 모듈에서는 Kubernetes 클러스터에 호스트되는 컨테이너에서 실행되는 node.js 앱에 적합한 빌드 및 릴리스 파이프라인을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-102">For this module, you created a build and release pipeline that makes sense for a node.js app running in a container hosted in a Kubernetes cluster.</span></span> 

<span data-ttu-id="24d1e-103">종종 프로젝트와 관련된 작업을 수행하기 위해 빌드 및 릴리스 파이프라인을 사용자 지정해야 할 때가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-103">Often times we need to customize the build and release pipelines to do specific things for our project.</span></span> <span data-ttu-id="24d1e-104">VSTS의 빌드 및 릴리스 파이프라인은 100% 사용자 지정이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-104">The build and release pipelines in VSTS are 100% customizable.</span></span> <span data-ttu-id="24d1e-105">파이프라인으로 필요한 모든 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-105">You can make the pipelines do whatever you need it to do.</span></span>

<span data-ttu-id="24d1e-106">이 모듈에서는 빌드 및 릴리스 파이프라인을 사용자 지정하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-106">In this unit, learn how to customize your build and release pipelines.</span></span>

## <a name="customize-the-build-pipeline"></a><span data-ttu-id="24d1e-107">빌드 파이프라인 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="24d1e-107">Customize the build pipeline</span></span>

<span data-ttu-id="24d1e-108">VSTS의 빌드 엔진은 작업을 하나씩 차례로 수행하는 작업 실행기입니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-108">The build engine in VSTS is just a task runner, doing one task, after another.</span></span> <span data-ttu-id="24d1e-109">빌드를 사용자 지정하려면 작업을 추가 또는 제거하고 작업의 올바른 매개 변수를 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-109">To customize the build, you just add or remove tasks and fill out the correct parameters for the task.</span></span>

<span data-ttu-id="24d1e-110">기본적으로 VSTS는 사용 가능한 약 100개의 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-110">Out of the box, VSTS comes with about 100 tasks that you can use.</span></span> <span data-ttu-id="24d1e-111">기본 제공되지 않는 다른 작업을 해야 하는 경우 700개가 넘는 빌드 및 릴리스 작업을 다운로드하여 사용할 수 있는 마켓플레이스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="24d1e-111">If you need to do something that doesn't exist out of the box, check the marketplace where there are over 700 build and release tasks ready to be downloaded and used.</span></span> <span data-ttu-id="24d1e-112">사용자 고유의 사용자 지정 작업을 작성하는 기능도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-112">You also have the ability to write your own custom tasks.</span></span>

<span data-ttu-id="24d1e-113">이 모듈에서는 코드의 보안을 검사하는 마켓플레이스 작업 WhiteSource Bolt를 설치하여 빌드 파이프라인을 사용자 지정할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-113">For this unit, you will customize the build pipeline by installing the marketplace tasks WhiteSource Bolt to do security scanning of our code.</span></span>

1. <span data-ttu-id="24d1e-114">Azure Portal에서 Azure DevOps 프로젝트를 찾아 빌드 정의 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-114">Browse to the Azure DevOps Project in the Azure portal and click on the build definition link</span></span>  
![빌드 링크](/media-draft/3-buildlink.png)

2. <span data-ttu-id="24d1e-116">빌드 파이프라인 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-116">This takes you to the build pipelines page.</span></span> <span data-ttu-id="24d1e-117">빌드를 클릭하고 `Edit`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-117">Click on the build and select `Edit`</span></span>  
<span data-ttu-id="24d1e-118">![빌드 편집](/media-draft/3-editbuild.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-118">![Edit Build](/media-draft/3-editbuild.png)</span></span>

3. <span data-ttu-id="24d1e-119">빌드 정의로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-119">This takes you to the build definition.</span></span> <span data-ttu-id="24d1e-120">`+`를 클릭하여 에이전트 작업 1에 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-120">Click on the `+` to add a task to Agent Job 1</span></span>  
<span data-ttu-id="24d1e-121">![작업 추가](/media-draft/3-addtask.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-121">![Add Task](/media-draft/3-addtask.png)</span></span>

4. <span data-ttu-id="24d1e-122">텍스트 필드에 `bolt`를 입력하고 `Get it free`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-122">In the text field, type `bolt` and click `Get it free`</span></span>  
<span data-ttu-id="24d1e-123">![무료 다운로드](/media-draft/3-getitfree.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-123">![Get it free](/media-draft/3-getitfree.png)</span></span>

5. <span data-ttu-id="24d1e-124">WhiteSource Bolt 마켓플레이스 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-124">This takes you to the WhiteSource Bolt Marketplace page.</span></span> <span data-ttu-id="24d1e-125">`Get it free`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-125">Click `Get it free`</span></span>  
<span data-ttu-id="24d1e-126">![White Source Bolt 무료 다운로드](/media-draft/3-getwhitesourceboltfree.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-126">![Get White Source Bolt Free](/media-draft/3-getwhitesourceboltfree.png)</span></span>

6. <span data-ttu-id="24d1e-127">VSTS 조직을 선택하고 `Install`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-127">Choose your VSTS organization and then click `Install`</span></span>  
<span data-ttu-id="24d1e-128">![설치](/media-draft/3-install.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-128">![Install](/media-draft/3-install.png)</span></span>

7. <span data-ttu-id="24d1e-129"><https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate>의 지침에 따라 WhiteSource Bolt를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-129">Activate WhiteSource Bolt by following the directions here <https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate></span></span>

8. <span data-ttu-id="24d1e-130">DevOps 프로젝트가 로드되어 있는 Azure Portal로 돌아가서 빌드 파이프라인 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-130">Go back to your Azure portal with the DevOps project loaded and click the build pipeline link</span></span>  
![빌드 파이프라인 링크](/media-draft/3-buildpipelinelink.png)

9. <span data-ttu-id="24d1e-132">빌드를 선택하고 `Edit`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-132">Select your build and click `Edit`</span></span>  
<span data-ttu-id="24d1e-133">![빌드 편집](/media-draft/3-editbuild.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-133">![Edit Build](/media-draft/3-editbuild.png)</span></span>

10. <span data-ttu-id="24d1e-134">`+` 에이전트 작업 1에 작업 추가를 클릭하고, 검색 필드에 `bolt`를 입력하고, `Add`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-134">Click the `+` Add a task to Agent job 1, type in `bolt` in the search field and click `Add`</span></span>  
<span data-ttu-id="24d1e-135">![Bolt 추가](/media-draft/3-addbolt.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-135">![Add Bolt](/media-draft/3-addbolt.png)</span></span>

11. <span data-ttu-id="24d1e-136">작업 목록의 맨 아래에 WhiteSource Bolt 작업이 추가됩니다. 맨 위로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-136">This adds the WhiteSource Bolt task to the bottom of the task list, drag it to the top</span></span>  
![맨 위에 Bolt](/media-draft/3-boltattop.png)

12. <span data-ttu-id="24d1e-138">`Save & queue`를 클릭하고 `Save & queue`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-138">Click `Save & queue` and select `Save & queue`</span></span>  
<span data-ttu-id="24d1e-139">![저장 및 큐에 넣기](/media-draft/3-saveandqueue.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-139">![Save and Queue](/media-draft/3-saveandqueue.png)</span></span>

13. <span data-ttu-id="24d1e-140">`Save & queue`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-140">Click `Save & queue`</span></span>  
<span data-ttu-id="24d1e-141">![저장 및 큐에 넣기 대화 상자](/media-draft/3-saveandqueuedialog.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-141">![Save and Queue Dialog](/media-draft/3-saveandqueuedialog.png)</span></span>

<span data-ttu-id="24d1e-142">수정된 빌드 파이프라인을 저장하고 빌드를 큐에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-142">This saves the modified build pipeline and queues the build.</span></span> <span data-ttu-id="24d1e-143">빌드가 완료된 후 `WhiteSource Bolt Build Report` 빌드를 살펴보면 WhiteSource Bolt가 보안 취약점을 찾기 위해 소스 코드를 검사한 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-143">After the build finishes, looking at the build `WhiteSource Bolt Build Report`, you can see the source code was scanned by WhiteSource Bolt looking for security vulnerabilities.</span></span>

![빌드 보고서](/media-draft/3-buildreport.png)

## <a name="customize-the-release-pipeline"></a><span data-ttu-id="24d1e-145">릴리스 파이프라인 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="24d1e-145">Customize the release pipeline</span></span>

<span data-ttu-id="24d1e-146">빌드와 마찬가지로, 릴리스 파이프라인은 작업 실행 기이며 동일한 방식으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-146">Like the build, the release pipeline is task runner and can be customized the same way.</span></span> <span data-ttu-id="24d1e-147">이 모듈에서는 릴리스 끝부분에 웹 성능 테스트를 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-147">For this unit, you will add a web performance test at the end of the release.</span></span> <span data-ttu-id="24d1e-148">이렇게 하면 앱이 Kubernetes 클러스터에 성공적으로 배포되어 실행되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-148">This will verifying that your app is deployed and running successfully in the Kubernetes cluster.</span></span>

1. <span data-ttu-id="24d1e-149">Azure Portal에서 DevOps 프로젝트를 찾아 릴리스 파이프라인 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-149">Browse to the DevOps project in the Azure Portal and click on the link for the release pipeline</span></span>  
![릴리스 링크](/media-draft/3-releaselink.png)

2. <span data-ttu-id="24d1e-151">릴리스 파이프라인 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-151">This takes you to the release pipeline page.</span></span> <span data-ttu-id="24d1e-152">릴리스 파이프라인을 클릭하고 `Edit`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-152">Click your release pipeline and click on `Edit`</span></span>  
<span data-ttu-id="24d1e-153">![릴리스 파이프라인 편집](/media-draft/3-editreleasepipeline.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-153">![Edit Release Pipeline](/media-draft/3-editreleasepipeline.png)</span></span>

3. <span data-ttu-id="24d1e-154">릴리스 `Dev` 단계에서 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-154">Click on the tasks in your release `Dev` stage</span></span>  
<span data-ttu-id="24d1e-155">![릴리스 단계](/media-draft/3-releasestage.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-155">![Release Stage](/media-draft/3-releasestage.png)</span></span>

4. <span data-ttu-id="24d1e-156">`+` 1단계에 작업 추가를 클릭하고, 검색 필드에 `web test`를 입력하고, 클라우드 기반 웹 성능 테스트 작업에 대한 `Add`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-156">Click on the `+` Add a task to Phase1, type `web test` in the search field and click `Add` for the Cloud-based Web Performance Test task</span></span>  
<span data-ttu-id="24d1e-157">![웹 테스트 추가](/media-draft/3-addwebtest.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-157">![Add Web Test](/media-draft/3-addwebtest.png)</span></span>

5. <span data-ttu-id="24d1e-158">빠른 웹 성능 테스트 작업을 클릭하고, 웹 사이트 URL의 앱 url(url을 찾으려면 Azure Portal DevOps 프로젝트 페이지를 이동한 후 오른쪽에서 샘플 앱 외부 엔드포인트를 마우스 오른쪽 단추로 클릭하고 링크 복사) 및 TestName에 대한 url을 추가하고, `Ping Test`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-158">Edit the Quick Web Performance Test task by clicking on it and adding the url to your app in the Website URL (to find the url, go to the Azure portal DevOps project page and on the right-hand side, right-click your sample app external endpoint and copy link) and then for TestName, enter in `Ping Test`</span></span>  
<span data-ttu-id="24d1e-159">![URL 복사](/media-draft/3-copyurl.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-159">![Copy URL](/media-draft/3-copyurl.png)</span></span>  
<span data-ttu-id="24d1e-160">![웹 테스트 작업 편집](/media-draft/3-editwebtesttask.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-160">![Edit Web Test Task](/media-draft/3-editwebtesttask.png)</span></span>

6. <span data-ttu-id="24d1e-161">`Save`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-161">Click `Save`</span></span>  
<span data-ttu-id="24d1e-162">![릴리스 저장](/media-draft/3-saverelease.png)</span><span class="sxs-lookup"><span data-stu-id="24d1e-162">![Save Release](/media-draft/3-saverelease.png)</span></span>

<span data-ttu-id="24d1e-163">이제 릴리스를 실행하면 새 helm 패키지가 배포된 후 웹 테스트가 실행되고 성공적으로 앱 url에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-163">Now, when you run a release, after deploying the new helm package, a web test is run hitting the app url successfully.</span></span>

![웹 테스트](/media-draft/3-webtest.png)


## <a name="summary"></a><span data-ttu-id="24d1e-165">요약</span><span class="sxs-lookup"><span data-stu-id="24d1e-165">Summary</span></span>

<span data-ttu-id="24d1e-166">이 모듈에서는 빌드 및 릴리스 파이프라인을 사용자 지정하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-166">In this unit, you learned how to customize your build and release pipelines.</span></span> <span data-ttu-id="24d1e-167">마켓플레이스에서 작업을 설치하고 사용하는 방법도 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="24d1e-167">You also learned how to install and use tasks from the Marketplace.</span></span>