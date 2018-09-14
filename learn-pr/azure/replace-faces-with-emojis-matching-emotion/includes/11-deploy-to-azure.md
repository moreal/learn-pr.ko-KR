<span data-ttu-id="49a4c-101">지금이 모듈에서는 했습니다 관리는 Slack을 가져오려고 _슬래시_ 명령 ngrok를 사용 하 여이 컴퓨터에 터널링 하 여 localhost에 실행 하는 동안에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-101">So far in this module, we've managed to get a Slack _slash_ command working but only while running on localhost and by tunnelling onto our computer using ngrok.</span></span> <span data-ttu-id="49a4c-102">이 경우 개발 했지만 릴리스 코드를 클라우드에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-102">This is fine for development but to release we want our code to be running in the cloud.</span></span>

<span data-ttu-id="49a4c-103">이 강의 하겠습니다 Azure 함수를 클라우드에 배포 하 여 코드의 새 프로덕션 버전을 사용 하 여 slack 구성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-103">In this lecture, we are going to deploy our Azure Function to the cloud and update the slack configuration to use the new production version of our code.</span></span>

<span data-ttu-id="49a4c-104">이 강의의 끝에서 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-104">By the end of this lecture you will learn:</span></span>

- <span data-ttu-id="49a4c-105">Azure에서 Azure 함수 앱을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="49a4c-105">How to create an Azure Function App on Azure</span></span>
- <span data-ttu-id="49a4c-106">Visual Studio Code를 사용 하 여 Azure에 배포 하는 방법</span><span class="sxs-lookup"><span data-stu-id="49a4c-106">How to deploy to Azure using Visual Studio Code</span></span>
- <span data-ttu-id="49a4c-107">적용 방법 프로덕션 환경으로 로컬 설정</span><span class="sxs-lookup"><span data-stu-id="49a4c-107">How to propogate your local settings to production</span></span>

## <a name="create-an-azure-function-app-on-azure"></a><span data-ttu-id="49a4c-108">Azure에서 Azure 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="49a4c-108">Create an Azure Function App on Azure</span></span>

<span data-ttu-id="49a4c-109">VS Code 및 Azure 함수 확장을 사용 하 여 azure 함수를 만들 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-109">We are going to be creating the azure function using VS Code and the Azure Function Extension.</span></span>

1. <span data-ttu-id="49a4c-110">사용 하 여 명령 팔레트 <kbd>Ctrl</kbd>+<kbd>P</kbd> 선택한 `Azure Function: Deploy to Function App`합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-110">Open the command palette with <kbd>Ctrl</kbd>+<kbd>P</kbd> and select `Azure Function: Deploy to Function App`.</span></span>

   ![함수 앱에 배포](/media-drafts/10.deploy-to-function-app.png)

2. <span data-ttu-id="49a4c-112">현재 프로젝트를 업로드 하 고 계속 해 서 선택 하려는 것인지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-112">It asks you to confirm you want to upload the current project, go ahead and select that.</span></span>

   ![배포 폴더를 선택 합니다.](/media-drafts/10.select-folder-to-deploy.png)

3. <span data-ttu-id="49a4c-114">앱과 연결할 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-114">Choose the subscription you want to associate with the app.</span></span>

   <span data-ttu-id="49a4c-115">Azure를 처음 접하는 경우에 구독이 두 개, 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-115">If you are new to Azure you should have one subscription, pick that.</span></span>

4. <span data-ttu-id="49a4c-116">선택한 새 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="49a4c-116">Choose create new function app</span></span>

   ![새 함수 앱 만들기](/media-drafts/10.create-new-function-app.png)

5. <span data-ttu-id="49a4c-118">앱에 대 한 이름을 선택합니다</span><span class="sxs-lookup"><span data-stu-id="49a4c-118">Pick a name for your app</span></span>

   <span data-ttu-id="49a4c-119">이름을 선택 하 여 원하는 호출을 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-119">It asks you to choose a name, call it whatever you want.</span></span> <span data-ttu-id="49a4c-120">마이닝 호출 하려는 `mojifier-slack-function-app`합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-120">I'm calling mine `mojifier-slack-function-app`.</span></span>

   ![앱 이름 선택](/media-drafts/10.choose-app-name.png)

6. <span data-ttu-id="49a4c-122">새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="49a4c-122">Create a new resource group</span></span>

   <span data-ttu-id="49a4c-123">리소스 그룹은 Azure에서 여러 서비스를 하나의 그룹화 하는 방법 _앱_합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-123">Resource groups are how we group multiple services in Azure into one _app_.</span></span> <span data-ttu-id="49a4c-124">새 또는 사용 하 여 이미 만든 기존 것을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-124">You can create a new one or use an existing one you've already created.</span></span>

   <span data-ttu-id="49a4c-125">하나의 고 자동으로 채웁니다 이름을 새를 만들 경우 선택 하거나 다른 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-125">If you create a new one, then It auto-populates a name for you, you can either select that or type another.</span></span>

7. <span data-ttu-id="49a4c-126">선택할 _새 저장소 계정을 만드는_합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-126">Choose _create new storage account_.</span></span>

   <span data-ttu-id="49a4c-127">함수 앱을 저장소 계정, 데이터 저장 및 파일에 더 영구적인 위치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-127">A function app needs a storage account, a more permanent place to store data and files.</span></span> <span data-ttu-id="49a4c-128">새 또는 사용 하 여 이미 만든 기존 것을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-128">You can create a new one or use an existing one you've already created.</span></span>

   <span data-ttu-id="49a4c-129">자동-채웁니다 이름을; 선택 하거나 다른 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-129">It auto-populates a name for you; you can either select that or type another.</span></span>

8. <span data-ttu-id="49a4c-130">지역 선택</span><span class="sxs-lookup"><span data-stu-id="49a4c-130">Pick a region</span></span>

   <span data-ttu-id="49a4c-131">함수 앱 라이브 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-131">Your function app has to live somewhere.</span></span> <span data-ttu-id="49a4c-132">귀하 또는 사용자에 게 가장 가까운 위치를 선택는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-132">I recommend choosing a location that is closest to you or your users.</span></span> <span data-ttu-id="49a4c-133">I 선택 `West Europe`</span><span class="sxs-lookup"><span data-stu-id="49a4c-133">I'm picking `West Europe`</span></span>

   ![앱 이름 선택](/media-drafts/10.select-region.png)

9. <span data-ttu-id="49a4c-135">업로드가 완료 [출력] 창을 URL을 보여 줍니다. 완료 되 면 같은 따라서 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-135">Wait for the upload to complete, once complete the output window shows a URL like so:</span></span>

```output
Deployment to "mojifier-slack-function-app" completed.
HTTP Trigger Urls:
  MojifyImage: https://mojifier-slack-function-app.azurewebsites.net/api/MojifyImage
```

## <a name="try-it-out"></a><span data-ttu-id="49a4c-136">체험</span><span class="sxs-lookup"><span data-stu-id="49a4c-136">Try it out</span></span>

<span data-ttu-id="49a4c-137">이 시점에서 적어도 리라는 `RespondToSlackCommand` 다른 종속성에 의존 하지 이후 작동 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-137">At this point, we should at least expect the `RespondToSlackCommand` function to be working since it doesn't rely on any other dependencies.</span></span>

<span data-ttu-id="49a4c-138">방문 `[deployed-app-name].azurefunctions.com/api/RespondToSlashCommand?text=[image-url]`</span><span class="sxs-lookup"><span data-stu-id="49a4c-138">Visit `[deployed-app-name].azurefunctions.com/api/RespondToSlashCommand?text=[image-url]`</span></span>

<span data-ttu-id="49a4c-139">모두 작동 하는 경우 다음도 하는 브라우저 창에서 반환 된 일부 JSON 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-139">If all is working well then you should some JSON returned in the browser window like so:</span></span>

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "https://mojifier-slack.azurewebsites.net/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```

## <a name="upload-settings"></a><span data-ttu-id="49a4c-140">업로드 설정</span><span class="sxs-lookup"><span data-stu-id="49a4c-140">Upload Settings</span></span>

<span data-ttu-id="49a4c-141">일부 설정에 있다고 기억 `local.settings.json` cognitive services에 대 한 키와 URL을 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-141">Remember we have some settings we put in `local.settings.json` these were the keys and URL for cognitive services.</span></span>

<span data-ttu-id="49a4c-142">`local.settings.json` 로컬이 복사 되지 통해 프로덕션에 배포 하는 경우 정확 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-142">`local.settings.json` is exactly that, local, it's never copied over to production when you deploy.</span></span>

<span data-ttu-id="49a4c-143">포털로 이동 하 고 아마도 UI 또는 사용을 통해 설정에 수동으로 추가을 해야 일반적으로 `func` CLI를 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-143">Usually, you would need to head over to the portal and perhaps manually add in the settings via the UI or use the `func` CLI to do the same.</span></span>

<span data-ttu-id="49a4c-144">그러나 VS Code를 사용 하기 때문에 로컬 설정을 업로드할 Azure Func 확장 하 고 명령 팔레트 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-144">However, since we are using VS Code, we can use the Azure Func extension and the command palette to upload the local settings for us.</span></span>

1.  <span data-ttu-id="49a4c-145">사용 하 여 명령 팔레트 <kbd>Ctrl</kbd>+<kbd>P</kbd> 선택한 `Azure Functions: Upload Local Settings`합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-145">Open the command palette with <kbd>Ctrl</kbd>+<kbd>P</kbd> and select `Azure Functions: Upload Local Settings`.</span></span>

    ![로컬 설정 업로드](/media-drafts/10.upload-local-settings.png)

2.  <span data-ttu-id="49a4c-147">선택 `local.settings.json`</span><span class="sxs-lookup"><span data-stu-id="49a4c-147">Choose `local.settings.json`</span></span>

    ![로컬 설정 선택](/media-drafts/10.choose-localsettings.png)

3.  <span data-ttu-id="49a4c-149">함수 앱이 연결 된 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-149">Choose the subscription your function app is associated with.</span></span>

4.  <span data-ttu-id="49a4c-150">함수 앱에 업로드 하려는 선택, 라고 마이닝 `mojifier-slack-function-app`</span><span class="sxs-lookup"><span data-stu-id="49a4c-150">Select the function app you want to upload to, mine is called `mojifier-slack-function-app`</span></span>

5.  <span data-ttu-id="49a4c-151">모든 설정을 덮어쓰려면 요청을 하는 경우 선택 `No To All`</span><span class="sxs-lookup"><span data-stu-id="49a4c-151">If it asks you to overwrite any settings, choose `No To All`</span></span>

    <span data-ttu-id="49a4c-152">이 업로드 새 설정 하는 것, 그렇지 않은 경우 개발에서 설정 사용 하 여 프로덕션 설정을 재정의 하면 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-152">This only uploads new settings which is what we want, otherwise there is a risk you override production settings with settings from development.</span></span>

    ![로컬 설정 선택](/media-drafts/10.choose-no-to-all.png)

## <a name="try-it-out"></a><span data-ttu-id="49a4c-154">체험</span><span class="sxs-lookup"><span data-stu-id="49a4c-154">Try it out</span></span>

<span data-ttu-id="49a4c-155">이제 모든 항목이 예상 대로 작동 하는 경우 다음 이제 MojifyImage 끝점 해야 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-155">Now if everything is working as expected then now the MojifyImage endpoint should be working.</span></span>

<span data-ttu-id="49a4c-156">방문 `[deployed-app-name].azurefunctions.com/api/MojifyImage?imageUrl=[image-url]`</span><span class="sxs-lookup"><span data-stu-id="49a4c-156">Visit `[deployed-app-name].azurefunctions.com/api/MojifyImage?imageUrl=[image-url]`</span></span>

<span data-ttu-id="49a4c-157">모든 사이트가 잘 작동 하는 경우 창의 mojified 이미지를 볼 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-157">If all is working well, then you should see the mojified image in the window.</span></span>

<span data-ttu-id="49a4c-158">작동 하지 않는 경우 여기에 문제 해결 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-158">If it's not working, then try troubleshooting the issues here.</span></span>

## <a name="update-slack"></a><span data-ttu-id="49a4c-159">Slack 업데이트</span><span class="sxs-lookup"><span data-stu-id="49a4c-159">Update Slack</span></span>

<span data-ttu-id="49a4c-160">함수를 클라우드에 배포한 이제 새 가리키도록 Slack의 설정을 업데이트할 수 있습니다 _공용_ URL입니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-160">Now we have deployed our Functions to the cloud we can update the settings in Slack to point to the new _public_ URL.</span></span>

1. <span data-ttu-id="49a4c-161">공용 URL을 사용 하 여 Slack을 업데이트 하면 `RespondToSlackCommand`합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-161">Update Slack, so it uses the public URL of your `RespondToSlackCommand`.</span></span>

![Slack 프로덕션 URL로 업데이트](/media-drafts/10.deploy-update-url.png)

> <span data-ttu-id="49a4c-163">**참고**</span><span class="sxs-lookup"><span data-stu-id="49a4c-163">**NOTE**</span></span>
>
> <span data-ttu-id="49a4c-164">프로덕션을 사용 하는 명령을 업데이트 _공용_의 버전을 `RespondToSlackCommand` 에서 호스트 `*.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="49a4c-164">I'm updating the command to use the production, _public_, version of the `RespondToSlackCommand` hosted on `*.azurewebsites.net`</span></span>

## <a name="try-it-out"></a><span data-ttu-id="49a4c-165">체험</span><span class="sxs-lookup"><span data-stu-id="49a4c-165">Try it out</span></span>

<span data-ttu-id="49a4c-166">Slack 로컬 앱 보다는 배포 된 앱에서 데이터를 요청 및 모든 항목이 올바르게 구성 되어 있는지를 확인 하려면을 해제할 수 있도록 `ngrok` 지금은 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-166">To check that everything is configured correctly and that Slack requests data from the deployed app rather than the local app, let switch off `ngrok` for now.</span></span>

<span data-ttu-id="49a4c-167">다음 창 slack 및 즐겨 slack 슬래시 명령을 입력으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-167">Then head to slack window and type your favourite slack slash command.</span></span>

`/mojify <image>`

<span data-ttu-id="49a4c-168">모든 작업 예상 대로 경우 slack 창에 표시 하는 이미지 표시 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a4c-168">If it's all working as expected then we should see an image appear in the slack window like so:</span></span>

![Win](/media-drafts/10.publish-success.png)
