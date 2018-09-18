<span data-ttu-id="b965a-101">Azure DevOps 프로젝트를 만든 후에 모든 사람들이 가장 먼저 문의한 것은 샘플 앱을 자신의 앱으로 바꾸는 방법이었습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-101">After creating an Azure DevOps project, the first thing everyone ask is how do you replace the sample app with your own app?</span></span> <span data-ttu-id="b965a-102">이 방법은 매우 간단하며 이 단원에서는 두 가지 방법을 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-102">It's quite simple and in this unit, you will learn two ways to do it.</span></span>

1. <span data-ttu-id="b965a-103">VSTS Git 리포지토리의 코드를 실제 코드로 바꾸기</span><span class="sxs-lookup"><span data-stu-id="b965a-103">Replacing the code in the VSTS git repository with your real code</span></span>

2. <span data-ttu-id="b965a-104">빌드 파이프라인에서 실제 코드가 있는 외부 Git 리포지토리 가리키기</span><span class="sxs-lookup"><span data-stu-id="b965a-104">Pointing your build pipeline to an external git repo holding your real code</span></span>

## <a name="replacing-code-in-vsts-git-repository"></a><span data-ttu-id="b965a-105">VSTS Git 리포지토리의 코드 바꾸기</span><span class="sxs-lookup"><span data-stu-id="b965a-105">Replacing code in VSTS git repository</span></span>

<span data-ttu-id="b965a-106">한 가지 간단한 방법은 VSTS에서 Git 리포지토리를 하드 드라이브에 복제하고, 모든 코드를 사용자 고유의 코드로 바꾸고, VSTS로 다시 업로드하는 것입니다. 잘 보세요!</span><span class="sxs-lookup"><span data-stu-id="b965a-106">One simple way is by cloning the git repo in VSTS onto your hard drive, replacing everything with your own code, uploading back to VSTS and voila.</span></span> <span data-ttu-id="b965a-107">이제 코드가 CI/CD 파이프라인을 통해 빌드 및 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-107">Your code will now be built and deployed through the CI/CD pipeline.</span></span>

<span data-ttu-id="b965a-108">이 단원에서는 Node.js 앱에 대한 소스 코드를 다운로드하여 하드 드라이브에 저장하는 것으로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-108">For this unit, you will start by downloading and storing the source code to the node.js app onto your hard drive.</span></span>

1. <span data-ttu-id="b965a-109"><https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip>에서 소스 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="b965a-109">Download the source code from <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip></span></span>

2. <span data-ttu-id="b965a-110">하드 드라이브의 어딘가에 있는 MicrosoftLearnDevOps.zip의 콘텐츠를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-110">Extract the contents of MicrosoftLearnDevOps.zip somewhere on your hard drive.</span></span> <span data-ttu-id="b965a-111">이 예에서는 `C:\users\abel\Downloads\MicrosoftLearnDevOps`가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-111">For this example `C:\users\abel\Downloads\MicrosoftLearnDevOps` was used</span></span>  
<span data-ttu-id="b965a-112">![압축을 푼 디렉터리](/media-draft/2-unzippedfolder.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-112">![Unzipped Directory](/media-draft/2-unzippedfolder.png)</span></span>

<span data-ttu-id="b965a-113">그런 다음, 리포지토리를 하드 드라이브에 복제하고, 샘플 앱을 실제 Node.js 앱으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-113">Next, you need to clone the repo onto your hard drive and replace the sample app with the real node.js app.</span></span> <span data-ttu-id="b965a-114">이 단원에서는 git가 이미 컴퓨터에 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-114">This unit assumes you already have git installed on your computer.</span></span>

1. <span data-ttu-id="b965a-115">Azure Portal에서 Azure DevOps 프로젝트로 이동하여 코드 리포지토리 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-115">From Azure portal browse to your Azure DevOps Project and click on the code repository link.</span></span>  
![](/media-draft/2-browsetorepolink.png)

2. <span data-ttu-id="b965a-116">[복제]를 클릭하고, 오른쪽 위에 있는 Git 리포지토리에 대한 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-116">Click on Clone and copy the url for the git repo in the upper right-hand side.</span></span>  
![복제 URL 복사](/media-draft/2-copycloneurl.png)  
<span data-ttu-id="b965a-118">리포지토리 URL이 클립보드에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-118">This will copy the repo url to your clipboard</span></span>

3. <span data-ttu-id="b965a-119">하드 드라이브에 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="b965a-119">Clone the repo to your hard drive</span></span>  
![Git 복제](/media-draft/2-gitclone.png)  
<span data-ttu-id="b965a-121">이 예에서 리포지토리는 C:\Users\abel\Source\TripleCrown\DevOps에 복제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-121">In this example the repo was cloned to C:\Users\abel\Source\TripleCrown\DevOps</span></span>

4. <span data-ttu-id="b965a-122">로컬 리포지토리에서 `.git` 디렉터리를 제외한 모든 항목 삭제</span><span class="sxs-lookup"><span data-stu-id="b965a-122">Delete everything from your local repo except for the `.git` directory</span></span>  
<span data-ttu-id="b965a-123">![모든 리포지토리 삭제](/media-draft/2-deleterepoofeverything.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-123">![Delete Repo of Everything](/media-draft/2-deleterepoofeverything.png)</span></span>

5. <span data-ttu-id="b965a-124">다운로드한 Node.js 앱에 대한 소스 코드를 리포지토리 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-124">Copy the source code for the downloaded node.js app into the repo folder</span></span>  
![대체된 코드](/media-draft/2-replacedeverything.png)

6. <span data-ttu-id="b965a-126">명령줄에서 `git add *`를 입력하여 모든 변경 내용을 로컬 리포지토리에 추가합니다</span><span class="sxs-lookup"><span data-stu-id="b965a-126">Add all the changes to your local repo by typing `git add *` from the command line</span></span>  
<span data-ttu-id="b965a-127">![Git에 모든 변경 내용 추가](/media-draft/2-gitaddall.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-127">![Git Add All](/media-draft/2-gitaddall.png)</span></span>

7. <span data-ttu-id="b965a-128">`git commit -m "replace sample app with real code"`를 입력하여 변경 내용을 로컬 리포지토리에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-128">Commit changes to your local repo by typing `git commit -m "replace sample app with real code"`</span></span>  
<span data-ttu-id="b965a-129">![Git 커밋](/media-draft/2-gitcommit.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-129">![Git Commit](/media-draft/2-gitcommit.png)</span></span>

8. <span data-ttu-id="b965a-130">`git push`를 사용하여 변경 내용을 VSTS의 Git 리포지토리로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-130">Push changes back to the git repo in VSTS with `git push`</span></span>  
<span data-ttu-id="b965a-131">![Git 푸시](/media-draft/2-gitpush.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-131">![Git Push](/media-draft/2-gitpush.png)</span></span>

9. <span data-ttu-id="b965a-132">변경 내용이 VSTS로 다시 푸시되면 빌드를 통해 실제 앱 코드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-132">After pushing changes back to VSTS, this should send the real app code through the build</span></span>  
<span data-ttu-id="b965a-133">![빌드 시작](/media-draft/2-buildkickedoff.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-133">![Build Kicked Off](/media-draft/2-buildkickedoff.png)</span></span>  
<span data-ttu-id="b965a-134">![실행 중인 빌드](/media-draft/2-buildinaction.png) 및 Azure로의 릴리스 파이프라인</span><span class="sxs-lookup"><span data-stu-id="b965a-134">![Build in Action](/media-draft/2-buildinaction.png) and release pipeline all the way to azure</span></span>  
 <span data-ttu-id="b965a-135">![릴리스 실행](/media-draft/2-releaserunning.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-135">![Release Running](/media-draft/2-releaserunning.png)</span></span>

 <span data-ttu-id="b965a-136">배포가 완료되면 Azure Portal로 돌아가서 실제 앱이 배포되었는지 확인할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b965a-136">After the deployment finishes, you can verify the real app was deployed by going back to the Azure portal</span></span>

 1. <span data-ttu-id="b965a-137">Azure Portal로 이동하고, Azure DevOps 프로젝트를 찾고, 오른쪽에 있는 배포된 앱을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-137">Go to the Azure portal, browse to your Azure DevOps project, and click on your deployed app on the right-hand side</span></span>  
 ![샘플 앱 시작 링크](/media-draft/2-launchapp.png)

 2. <span data-ttu-id="b965a-139">브라우저에서 앱 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-139">This launches the running app in your browser</span></span>  
 ![앱 실행](/media-draft/2-apprunning.png)

## <a name="using-external-git-repo"></a><span data-ttu-id="b965a-141">외부 Git 리포지토리 사용</span><span class="sxs-lookup"><span data-stu-id="b965a-141">Using external git repo</span></span>

<span data-ttu-id="b965a-142">샘플 앱을 실제 앱 코드로 바꾸는 또 다른 방법은 빌드 파이프라인에서 앱 코드가 있는 외부 Git 리포지토리를 가리키는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-142">Another way to swap out the sample app with your real app code is by pointing the build pipeline to an external git repository that holds your app code.</span></span> <span data-ttu-id="b965a-143">이 예의 경우 실제 앱 코드를 GitHub 리포지토리에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-143">For this example, upload the real app code to a github repository.</span></span>

<span data-ttu-id="b965a-144">실제 코드가 GitHub에 업로드되면 다음을 수행하여 빌드 파이프라인에서 이 GitHub 리포지토리를 가리키도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-144">After uploading the real code to github, do the following to point the build pipeline to this github repository</span></span>

1. <span data-ttu-id="b965a-145">Azure Portal에서 Azure DevOps 프로젝트를 찾아 빌드 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-145">From the Azure portal, browse to your Azure DevOps project and click on the build link</span></span>  
![빌드 링크](/media-draft/2-buildlink.png)

2. <span data-ttu-id="b965a-147">빌드 파이프라인으로 이동하고, 빌드 파이프라인, `Edit`을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-147">This takes you to the build pipelines, click your build pipeline and then `Edit`</span></span>  
<span data-ttu-id="b965a-148">![빌드 편집 클릭](/media-draft/2-clickeditbuildlink.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-148">![Click Edit Build](/media-draft/2-clickeditbuildlink.png)</span></span>

3. <span data-ttu-id="b965a-149">빌드 편집기로 이동하고, `Get sources`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-149">This takes you to the build editor, click on `Get sources`</span></span>  
<span data-ttu-id="b965a-150">![원본 가져오기 클릭](/media-draft/2-clickgetsource.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-150">![Click Get Source](/media-draft/2-clickgetsource.png)</span></span>

4. <span data-ttu-id="b965a-151">[원본 선택] 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-151">This takes you to the Select a source page.</span></span> <span data-ttu-id="b965a-152">VSTS Git뿐만 아니라 GitHub, GitHub Enterprise, Subversion, Bitbucket Cloud 및 빌드 파이프라인에 대한 외부 Git 기반 리포지토리도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-152">Notice how you can not only use VSTS Git, but also GitHub, GitHub Enterprise, Subversion, Bitbucket Cloud, and any external Git based repo for the build pipeline.</span></span> <span data-ttu-id="b965a-153">이 연습에서는 GitHub를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-153">For this exercise, select GitHub</span></span>  
![GitHub 선택](/media-draft/2-selectgithub.png)

5. <span data-ttu-id="b965a-155">[GitHub 연결] 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-155">This takes you to the GitHub connection page.</span></span> <span data-ttu-id="b965a-156">OAuth 또는 개인 액세스 토큰을 사용하여 GitHub 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-156">Either use OAuth or a Personal Access Token to connect with your GitHub account</span></span>

6. <span data-ttu-id="b965a-157">실제 앱 코드가 있는 GitHub 리포지토리를 선택하고 `Save & queue`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-157">Select the github repo holding the real app code and click `Save & queue`</span></span>  
<span data-ttu-id="b965a-158">![저장 및 큐에 넣기](/media-draft/2-saveandqueue.png)</span><span class="sxs-lookup"><span data-stu-id="b965a-158">![Save and Queue](/media-draft/2-saveandqueue.png)</span></span>

7. <span data-ttu-id="b965a-159">`Save & queue` 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-159">Click the `Save & queue` button</span></span>  
![](/media-draft/2-saveandqueuedialog.png)

8. <span data-ttu-id="b965a-160">이 작업은 빌드를 저장하고 시작하여 빌드 및 릴리스 파이프라인을 통해 GitHub에서 호스팅되는 실제 앱 코드를 Azure로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-160">This action saves and kicks off the build, sending the real app code hosted in GitHub through our build and release pipelines all the way to Azure</span></span>  
![빌드 실행](/media-draft/2-buildrunning.png)

## <a name="summary"></a><span data-ttu-id="b965a-162">요약</span><span class="sxs-lookup"><span data-stu-id="b965a-162">Summary</span></span>

<span data-ttu-id="b965a-163">이 단원에서는 DevOps 프로젝트의 샘플 코드를 실제 앱 코드로 바꾸는 두 가지 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-163">In this unit, you learned two different ways to replace the sample code in the DevOps project with real app code.</span></span> <span data-ttu-id="b965a-164">이 작업은 VSTS Git 리포지토리의 코드를 바꾸거나 빌드 파이프라인을 앱 코드가 있는 다른 외부 리포지토리와 연결하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-164">This can be done either by replacing the code in the VSTS git repo, or by linking the build pipeline with another external repo which holds your app code.</span></span>

<span data-ttu-id="b965a-165">다음으로, 빌드 및 릴리스 파이프라인을 사용자 지정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b965a-165">Next learn how to customize the build and release pipelines.</span></span>