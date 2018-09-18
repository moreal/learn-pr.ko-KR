<span data-ttu-id="e23b0-101">CI/CD 파이프라인을 빠르게 설정하는 것은 항상 어려운 과제였습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-101">Setting up a CI/CD pipeline has always been challenging to do quickly.</span></span> <span data-ttu-id="e23b0-102">이제 전체 종단간 Azure DevOps 프로젝트를 처음부터 수행하여 완료하는 것이 믿을 수 없을 정도로 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-102">Now, it is incredibly easy to go from nothing at all to a full end to end Azure DevOps project.</span></span> <span data-ttu-id="e23b0-103">그리고 Azure DevOps 프로젝트에서 다음을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-103">And in the Azure DevOps project, you get the following:</span></span>

1. <span data-ttu-id="e23b0-104">Azure에서 프로비전되는 인프라</span><span class="sxs-lookup"><span data-stu-id="e23b0-104">Infrastructure provisioned for you in Azure.</span></span>

2. <span data-ttu-id="e23b0-105">VSTS 인스턴스의 팀 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e23b0-105">A Team Project in a VSTS instance.</span></span>

3. <span data-ttu-id="e23b0-106">VSTS 인스턴스의 리포지토리에서 선택한 언어로 된 샘플 앱의 소스 코드</span><span class="sxs-lookup"><span data-stu-id="e23b0-106">Source code for a sample app in the language that you picked in the repo of your VSTS instance.</span></span>

4. <span data-ttu-id="e23b0-107">선택한 기술에 적합한 빌드 및 릴리스 파이프라인</span><span class="sxs-lookup"><span data-stu-id="e23b0-107">A build and release pipeline that makes sense for the technologies picked.</span></span>

<span data-ttu-id="e23b0-108">그리고 완료되면 Azure DevOps 프로젝트에서 샘플 앱을 가져와서 파이프라인을 통해 Azure에서 프로비전하는 인프라로 빌드하고 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-108">And when its's done, the Azure DevOps project takes the sample app, builds and releases it through the pipelines into the infrastructure it provisions for you up in Azure.</span></span> <span data-ttu-id="e23b0-109">그리고 이 모든 것을 몇 번의 클릭만으로 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-109">And you get all of this with just a couple of clicks.</span></span>

## <a name="create-an-azure-devops-project"></a><span data-ttu-id="e23b0-110">Azure DevOps 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e23b0-110">Create an Azure DevOps project</span></span>

<span data-ttu-id="e23b0-111">Azure Portal에서 Azure DevOps 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-111">You create an Azure DevOps project from the Azure portal.</span></span>

1. <span data-ttu-id="e23b0-112">[Azure Portal](https://portal.azure.com)로 이동하여 `Create a resource`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-112">Head to the [Azure Portal](https://portal.azure.com) and click `Create a resource`</span></span>  
![](/media-draft/1-azureportal.png)

2. <span data-ttu-id="e23b0-113">`DevOps Project`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-113">Click `DevOps Project`</span></span>  
<span data-ttu-id="e23b0-114">![DevOps 프로젝트 선택](/media-draft/1-pickdevopsproject.png)</span><span class="sxs-lookup"><span data-stu-id="e23b0-114">![Pick DevOps Project](/media-draft/1-pickdevopsproject.png)</span></span>

3. <span data-ttu-id="e23b0-115">다음 화면에서는 사용하려는 언어를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-115">The next screen is where you get to pick what language you want to use.</span></span> <span data-ttu-id="e23b0-116">.NET(기본), Java, Node, PHP, Python, Ruby 및 Go를 선택하는 방법에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="e23b0-116">Notice how you can choose .NET (of course), java, node, php, python, ruby, and go.</span></span> <span data-ttu-id="e23b0-117">Git 리포지토리에서 사용자 고유의 코드를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-117">You can even bring your own code in from a git repo.</span></span> <span data-ttu-id="e23b0-118">이 단원에서는 Node.js 앱을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-118">For this unit, let’s go ahead and create a Node.js app.</span></span> <span data-ttu-id="e23b0-119">Node.js를 클릭하고 [다음]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-119">Click Node.js and click Next</span></span>  
![언어에 대해 Node.js 선택](/media-draft/1-picknodejsforlang.png)

4. <span data-ttu-id="e23b0-121">다음으로, 사용하려는 Node.js 프레임워크를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-121">Next it's going to ask you what node.js framework you want to use.</span></span> <span data-ttu-id="e23b0-122">이 단원에서는 간단한 Node.js 앱을 선택하고 [다음]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-122">For this unit, pick Simple Node.js app and click Next</span></span>  
![간단한 Node 선택](/media-draft/1-picksimplenode.png)

5. <span data-ttu-id="e23b0-124">다음으로, 앱을 프로비전하고 실행하려는 인프라를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-124">Next, it's going to ask you what infrastructure do you want to provision and run your app in?</span></span> <span data-ttu-id="e23b0-125">이 단원에서는 Azure Kubernetes Service를 사용하여 Kubernetes 클러스터에 프로비전하고 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-125">For this unit, let’s provision and deploy into a Kubernetes cluster using Azure Kubernetes Service.</span></span> <span data-ttu-id="e23b0-126">Kubernetes Service를 선택하고 [다음]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-126">Select Kubernetes Service and click Next</span></span>  
![Kubernetes 선택](/media-draft/1-pickkubernetes.png)

6. <span data-ttu-id="e23b0-128">이제 완전히 새로운 VSTS 인스턴스를 만들거나 기존 VSTS 인스턴스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-128">And now, you can either create a brand new instance of VSTS or choose an existing one.</span></span> <span data-ttu-id="e23b0-129">또한 Kubernetes 클러스터를 실행하려는 위치와 방법을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-129">You also get to set up where and how you want your kubernetes cluster to run.</span></span> <span data-ttu-id="e23b0-130">이 단원에서는 [새로 선택]을 선택하여 새 VSTS 인스턴스를 만들고, VSTS 인스턴스에 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-130">For this unit, go ahead and create a new VSTS instance by choosing Select new and give your VSTS instance a unique name.</span></span> <span data-ttu-id="e23b0-131">[프로젝트 학습] 이름을 입력하고, Azure 구독을 선택하고, 클러스터 이름을 LearnCluster로 지정하고, 위치를 [미국 동부]로 선택한 다음, [완료]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-131">Enter Learn for the Project name, pick your azure subscription, name the Cluster Name LearnCluster, select East US for the location, and click Done</span></span>  
![최종 확인 화면](/media-draft/1-finalconfirmation.png)

<span data-ttu-id="e23b0-133">그리고 그야말로 있는 그대로입니다!</span><span class="sxs-lookup"><span data-stu-id="e23b0-133">And that is literally it!</span></span> <span data-ttu-id="e23b0-134">시간이 좀 걸리므로 Azure에서 수행하도록 내버려 둔 채 잠시 휴식을 취합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-134">This takes a while so kick back, relax and just let Azure do its thing.</span></span> <span data-ttu-id="e23b0-135">대부분의 시간은 Azure 인프라를 프로비전하고 구성하는 데 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-135">Most of the time will be spent provisioning and configuring your Azure infrastructure.</span></span> <span data-ttu-id="e23b0-136">이 모듈의 경우 Azure Kubernetes Service와 Azure Container Registry가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-136">For this module, this will be your Azure Kubernetes Service and Azure Container Registry.</span></span>

## <a name="a-lap-around-the-finished-azure-devops-project"></a><span data-ttu-id="e23b0-137">완성된 Azure DevOps 프로젝트 주위의 환경</span><span class="sxs-lookup"><span data-stu-id="e23b0-137">A lap around the finished Azure DevOps Project</span></span>

<span data-ttu-id="e23b0-138">Azure가 완료되면 [알림]에서 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-138">When Azure is done, you will be notified in your Alerts</span></span>

1. <span data-ttu-id="e23b0-139">[알림], [리소스로 이동]을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-139">Click on the alert and then Go to resource</span></span>  
![[알림]에서 [리소스로 이동]](/media-draft/1-gotoresourcefromalert.png)

2. <span data-ttu-id="e23b0-141">프로비전된 모든 것을 표시하는 포털 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-141">This takes you to a portal blade that displays everything provisioned.</span></span> <span data-ttu-id="e23b0-142">왼쪽에는 CI/CD 파이프라인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-142">On the left-hand side is your CI/CD pipeline.</span></span> <span data-ttu-id="e23b0-143">코드 리포지토리, 빌드 정의 및 릴리스 정의가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-143">You have your code repository, your build definition, and also your release definition.</span></span> <span data-ttu-id="e23b0-144">모든 링크는 VSTS에서 리소스로 직접 이동하는 딥 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-144">All the links are deep links that take you directly into the resource in VSTS.</span></span> <span data-ttu-id="e23b0-145">오른쪽에는 Azure에서 배포한 모든 인프라가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-145">And on the right-hand side, you see all the infrastructure deployed for you in Azure.</span></span> <span data-ttu-id="e23b0-146">샘플 앱이 이미 배포된 Kubernetes 클러스터와 Application Insight가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-146">You have your Kubernetes cluster with your sample app already deployed and also application insight.</span></span> <span data-ttu-id="e23b0-147">다시금 말하지만, 이러한 모든 링크는 Azure의 리소스에 대한 딥 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-147">Once again, all these links are deep links to the resources in Azure.</span></span>  
![포털 DevOps 프로젝트](/media-draft/1-pickdevopsproject.png)

3. <span data-ttu-id="e23b0-149">소스 코드 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-149">Click on the link for your source code</span></span>  
![원본에 연결](/media-draft/1-linktosource.png)

4. <span data-ttu-id="e23b0-151">VSTS 프로젝트의 Git 리포지토리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-151">This takes you to the git repo in your VSTS project.</span></span> <span data-ttu-id="e23b0-152">이 리포지토리는 Helm 차트가 있는 Node.js 샘플 앱을 보유하고 있는 일반적인 Git 리포지토리일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-152">Notice this is just a normal git repo holding the sample node.js app with helm charts.</span></span>  
![VSTS 리포지토리](/media-draft/1-vstsrepo.png)

5. <span data-ttu-id="e23b0-154">빌드로 이동</span><span class="sxs-lookup"><span data-stu-id="e23b0-154">Go into the builds</span></span>  
![빌드에 연결](/media-draft/1-navtobuild.png)

6. <span data-ttu-id="e23b0-156">빌드를 클릭한 다음, [편집]을 클릭하여 만든 빌드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-156">Edit the created build by clicking on the build and then click Edit</span></span>  
![](/media-draft/1-editbuildlink.png)

7. <span data-ttu-id="e23b0-157">선택한 기술에 적합한 빌드 파이프라인이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-157">You will see a build pipeline that makes sense for the technologies picked.</span></span> <span data-ttu-id="e23b0-158">Kubernetes 클러스터에 Node.js 앱을 선택했으므로 Docker 작업을 사용하여 Node.js 앱을 빌드하고, 이미지 컨테이너 이미지를 만든 다음, Helm 작업을 사용하여 Helm 패키지를 만드는 빌드 파이프라인을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-158">Since we picked a node.js app into a Kubernetes cluster, we get a build pipeline that uses Docker tasks to build the Node.js app, create the image container image and then Helm tasks to create a Helm package.</span></span>  
![빌드 파이프라인](/media-draft/1-buildpipeline.png)

8. <span data-ttu-id="e23b0-160">`Releases`를 클릭하여 릴리스 파이프라인으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-160">Go to the Release pipeline by clicking `Releases`</span></span>  
<span data-ttu-id="e23b0-161">![릴리스로 이동](/media-draft/1-gotoreleases.png)</span><span class="sxs-lookup"><span data-stu-id="e23b0-161">![Go to Releases](/media-draft/1-gotoreleases.png)</span></span>

9. <span data-ttu-id="e23b0-162">만든 릴리스 파이프라인이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-162">You'll see the release pipeline created.</span></span> <span data-ttu-id="e23b0-163">릴리스를 클릭하고 `Edit pipeline`을 선택하여 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-163">Edit it by clicking on the release and selecting `Edit pipeline`</span></span>  
<span data-ttu-id="e23b0-164">![릴리스 편집](/media-draft/1-editrelease.png)</span><span class="sxs-lookup"><span data-stu-id="e23b0-164">![Edit Release](/media-draft/1-editrelease.png)</span></span>

10. <span data-ttu-id="e23b0-165">Azure에서 선택한 기술에 적합한 릴리스 파이프라인을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-165">Azure has created a release pipeline that makes sense for the technologies picked.</span></span> <span data-ttu-id="e23b0-166">Kubernetes 클러스터에서 호스팅되는 컨테이너에서 실행되는 Node 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-166">A node app running in a container hosted in a Kubernetes cluster.</span></span>
<span data-ttu-id="e23b0-167">![릴리스 파이프라인](/media-draft/1-releasepipeline.png)</span><span class="sxs-lookup"><span data-stu-id="e23b0-167">![Release Pipeline](/media-draft/1-releasepipeline.png)</span></span>

11. <span data-ttu-id="e23b0-168">Azure Portal로 돌아가서 Kubernetes 서비스에 대한 외부 엔드포인트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-168">Go back to the Azure portal and click on the external endpoint for the kubernetes service</span></span>  
![](/media-draft/1-clickonendpoint.png)

12. <span data-ttu-id="e23b0-169">AKS 클러스터에 빌드되고 배포된 샘플 앱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-169">You should see the sample app build and deployed into your AKS cluster</span></span>  
![앱 실행](/media-draft/1-apprunning.png)

## <a name="summary"></a><span data-ttu-id="e23b0-171">요약</span><span class="sxs-lookup"><span data-stu-id="e23b0-171">Summary</span></span>

<span data-ttu-id="e23b0-172">이 단원에서는 다음 요소로 구성된 Azure DevOps 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-172">In this unit, you created an Azure DevOps project that consists of:</span></span>

1. <span data-ttu-id="e23b0-173">앱용 인프라 - Azure Kubernetes Service 및 Application Insight</span><span class="sxs-lookup"><span data-stu-id="e23b0-173">Infrastructure for your app - Azure Kubernetes Service and Application Insight</span></span>

2. <span data-ttu-id="e23b0-174">VSTS 인스턴스의 팀 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e23b0-174">A Team Project in a VSTS instance.</span></span>

3. <span data-ttu-id="e23b0-175">VSTS 인스턴스의 리포지토리에 있는 컨테이너에서 실행되는 Node.js 샘플 앱에 대한 소스 코드</span><span class="sxs-lookup"><span data-stu-id="e23b0-175">Source code for a Node.js sample app running in a container in the repo of your VSTS instance.</span></span>

4. <span data-ttu-id="e23b0-176">Azure Kubernetes Service 인스턴스에서 실행되는 Node.js 컨테이너 앱에 대한 빌드 및 릴리스 파이프라인</span><span class="sxs-lookup"><span data-stu-id="e23b0-176">A build and release pipeline for a Node.js container app running in your Azure Kubernetes Service instance.</span></span>

<span data-ttu-id="e23b0-177">다음으로, 샘플 앱을 실제 앱으로 바꾸는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e23b0-177">Next, learn how to replace the sample app with your real app.</span></span>