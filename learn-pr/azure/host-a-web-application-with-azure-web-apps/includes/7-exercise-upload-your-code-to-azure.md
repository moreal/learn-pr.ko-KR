<span data-ttu-id="07863-101">이 연습에서는 Azure에 ASP.NET Core 응용 프로그램을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-101">In this exercise, you'll upload your ASP.NET Core application to Azure.</span></span>

## <a name="create-a-staging-deployment-slot"></a><span data-ttu-id="07863-102">준비 배포 슬롯 만들기</span><span class="sxs-lookup"><span data-stu-id="07863-102">Create a staging deployment slot</span></span>

1. <span data-ttu-id="07863-103">왼쪽 탐색에서 **배포 슬롯** 메뉴 항목을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-103">Locate and click the **Deployment slots** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="07863-104">Azure가 아래와 같이 **배포 슬롯** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07863-104">Azure opens the **Deployment slots** blade as shown below.</span></span>

    ![배포 슬롯](../media-draft/7-deployment-slot-blade.png)

1. <span data-ttu-id="07863-106">배포 슬롯 블레이드의 위쪽 탐색 모음에서 **+ 슬롯 추가** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-106">Locate and click the **+ Add Slot** button on the top navigation bar of the deployment slots blade.</span></span>

1. <span data-ttu-id="07863-107">Azure Portal이 아래와 같이 **슬롯 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07863-107">The Azure portal opens the **Add a slot** blade as shown below.</span></span>

    ![슬롯 추가](../media-draft/7-new-deployment-slot-blade.png)

    <span data-ttu-id="07863-109">배포 슬롯에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-109">Give your deployment slot a name.</span></span> <span data-ttu-id="07863-110">이 경우 **스테이징**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-110">In this case, use **Staging**.</span></span>

    <span data-ttu-id="07863-111">**구성 원본**을 선택하려면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-111">To choose a **Configuration Source**, you have 2 options.</span></span>

    1. <span data-ttu-id="07863-112">Azure에 생성된 다른 슬롯 또는 웹앱에서 구성 요소를 복제하려면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-112">Select to clone the configuration elements from any other slot or web app created on Azure.</span></span>

    1. <span data-ttu-id="07863-113">구성 요소를 복제하지 않도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-113">You can choose not to clone any configuration elements.</span></span> <span data-ttu-id="07863-114">이 경우 **기존 슬롯에서 구성 복제 안 함** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-114">In this case, you select the option **Don't clone configuration from an existing slot**.</span></span>

    <span data-ttu-id="07863-115">두 번째 옵션인 **기존 슬롯에서 구성을 복제**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-115">Choose the second option, **Don't clone configuration from an existing slot**.</span></span>

1. <span data-ttu-id="07863-116">블레이드 맨 아래에서 **확인** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-116">Locate and click the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="07863-117">배포 슬롯이 성공적으로 만들어지면 Azure Portal은 다시 웹앱의 **배포 슬롯** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-117">Once the deployment slot is successfully created, the Azure portal navigates you back to the **Deployment slots** blade of your web app.</span></span>

    <span data-ttu-id="07863-118">이제 방금 만든 새 배포 슬롯을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-118">Now, you can see the new deployment slot that you have just created.</span></span>

    ![생성된 배포 슬롯](../media-draft/7-deployment-slot-created.png)

1. <span data-ttu-id="07863-120">새 배포 슬롯을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-120">Locate and click the new deployment slot.</span></span>

1. <span data-ttu-id="07863-121">Azure Portal은 새로 만든 배포 슬롯의 **개요** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-121">The Azure portal navigates to the **Overview** page of the newly created deployment slot.</span></span>

    ![스테이징 배포 슬롯](../media-draft/7-deployment-slot-staging.png)

    <span data-ttu-id="07863-123">스테이징 배포 슬롯의 **URL**을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-123">Notice the **URL** of the staging deployment slot.</span></span> <span data-ttu-id="07863-124">이 URL은 이 단원의 첫 부분에서 이전에 본 것과 동일한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-124">It is the exact same URL you saw previously at the beginning of this unit.</span></span>

    <span data-ttu-id="07863-125">배포 슬롯은 Azure 내의 웹앱으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-125">A deployment slot is treated as a web app inside Azure.</span></span> <span data-ttu-id="07863-126">그러나 이는 원래 웹앱의 자식인 특수한 유형이며 원래 웹앱으로 교환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-126">However, it is a special type that is a child of the original web app and can be swapped with the original web app.</span></span>

    <span data-ttu-id="07863-127">**URL**을 클릭하면 Azure Portal에서 처음 만들 때 Azure가 웹앱용으로 만든 것과 동일한 기본 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-127">If you click the **URL**, you will see the same default page that Azure created for the web app the first time we created it in the Azure portal.</span></span>

<span data-ttu-id="07863-128">이제 스테이징 배포 슬롯이 성공적으로 생성되었으므로 **배포 자격 증명**을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-128">Now that the staging deployment slot is created successfully, you need to configure **deployment credentials**.</span></span>

## <a name="create-deployment-credentials"></a><span data-ttu-id="07863-129">배포 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="07863-129">Create deployment credentials</span></span>

<span data-ttu-id="07863-130">실제 배포 프로세스를 시작하려면 먼저 Azure에서 배포 자격 증명을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-130">Azure requires deployment credentials to be set up before you can start the actual deployment process.</span></span> <span data-ttu-id="07863-131">이런 이유로 고유한 배포 자격 증명을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07863-131">For that reason, you will learn how to create your own deployment credentials.</span></span>

1. <span data-ttu-id="07863-132">왼쪽 탐색에서 **배포 자격 증명** 메뉴 항목을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-132">Locate and click the **Deployment credentials** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="07863-133">Azure Portal은 아래와 같이 **배포 자격 증명** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-133">The Azure portal navigates to the **Deployment credentials** blade as shown below.</span></span>

    ![배포 자격 증명](../media-draft/7-deployment-credentials.png)

    <span data-ttu-id="07863-135">선택한 **사용자 이름**과 **암호**를 입력한 후 암호를 다시 한번 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-135">Enter a **username** and **password** of your choice, and then confirm your password once again.</span></span>

    > <span data-ttu-id="07863-136">암호를 잊지 않도록 사용자 이름과 암호를 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="07863-136">Make sure you write down your username and password so that you don't forget them!</span></span> <span data-ttu-id="07863-137">나중에 Azure에 대한 코드 업로드 및 배포를 시작할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-137">You will need them later when we start uploading and deploying our code to Azure.</span></span>

    <span data-ttu-id="07863-138">사용자 이름과 암호를 결정한 후 **배포 자격 증명** 블레이드 맨 위에 있는 **저장** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-138">Once you decide on the username and password, locate and click the **Save** button at the top of the **Deployment credentials** blade.</span></span>

<span data-ttu-id="07863-139">이제 배포 자격 증명 정보가 성공적으로 생성되었으므로 **배포 옵션**을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-139">Now that the deployment credentials are created successfully, you need to configure **deployment options**.</span></span>

## <a name="use-a-local-git-repository-as-your-deployment-option"></a><span data-ttu-id="07863-140">로컬 Git 리포지토리를 배포 옵션으로 사용</span><span class="sxs-lookup"><span data-stu-id="07863-140">Use a local Git repository as your deployment option</span></span>

<span data-ttu-id="07863-141">이제 코드를 업로드하는 프로세스를 시작할 수 있도록 Azure에서 로컬 Git 리포지토리를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-141">Now, it is time to create a local Git repository in Azure so that you can start the process of uploading your code.</span></span>

1. <span data-ttu-id="07863-142">왼쪽 탐색에서 **배포 옵션** 메뉴 항목을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-142">Locate and click the **Deployment options** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="07863-143">Azure Portal은 아래와 같이 **배포 옵션** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-143">The Azure portal navigates to the **Deployment options** blade as shown below.</span></span>

    ![배포 옵션](../media-draft/7-deployment-options.png)

1. <span data-ttu-id="07863-145">**원본 선택/필수 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-145">Click on **Choose source / Configure required settings**.</span></span>

    ![배포 자격 증명](../media-draft/7-deployment-sources.png)

1. <span data-ttu-id="07863-147">Azure Portal에 구성하고 사용할 수 있는 사용 가능한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-147">The Azure portal displays the available options that you can configure and use.</span></span> <span data-ttu-id="07863-148">이 경우 **로컬 Git 리포지토리** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-148">In our case, choose the **Local Git Repository** option.</span></span>

    ![로컬 Git 리포지토리](../media-draft/7-local-git-repo.png)

1. <span data-ttu-id="07863-150">블레이드 맨 아래에서 **확인** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-150">Locate and click the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="07863-151">왼쪽 탐색에서 **개요** 메뉴 항목을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-151">Locate and click the **Overview** menu item on the left-side navigation.</span></span>

    ![Git이 구성된 배포 슬롯](../media-draft/7-staging-after-setting-git.png)

    <span data-ttu-id="07863-153">다음과 같은 두 가지 중요한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-153">Notice two important pieces of information:</span></span>
    - <span data-ttu-id="07863-154">**Git/배포 사용자 이름**: 나중에 Azure의 로컬 Git 리포지토리에 연결하는 데 사용할 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-154">**Git/Deployment username**: These are the credentials that you will use later on to connect to the local Git repository on Azure.</span></span>

    - <span data-ttu-id="07863-155">**Git Clone URL**: 로컬 웹 응용 프로그램 리포지토리에 **원격**으로 사용할 로컬 Git 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-155">**Git clone url**: This is the local Git repository URL that you will use as a **remote** for your local web application repository.</span></span>

<span data-ttu-id="07863-156">이제 스테이징 배포 슬롯에 코드를 업로드할 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-156">It is time to start uploading your code to the staging deployment slot.</span></span>

## <a name="install-git-on-your-machine"></a><span data-ttu-id="07863-157">머신에 Git 설치</span><span class="sxs-lookup"><span data-stu-id="07863-157">Install Git on your machine</span></span>

<span data-ttu-id="07863-158">내 Ubuntu 18.04 머신에 Git을 설치하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-158">I will be installing Git on my Ubuntu 18.04 machine.</span></span>

1. <span data-ttu-id="07863-159">새 **터미널** 창 열기</span><span class="sxs-lookup"><span data-stu-id="07863-159">Open a new **Terminal** window</span></span>

1. <span data-ttu-id="07863-160">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-160">Type the following command.</span></span> <span data-ttu-id="07863-161">Ubuntu 사용자 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-161">You will be prompted to enter your Ubuntu user password.</span></span>

    ```console
    sudo apt-get update
    ```

1. <span data-ttu-id="07863-162">업데이트가 성공하면 다음 명령을 입력하여 Git을 로컬로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-162">Once the update is successful, type the following command to install Git locally.</span></span> <span data-ttu-id="07863-163">머신에서 Git 설치를 허용할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-163">You will be prompted to accept the installation of Git on your machine.</span></span>

    ```console
    sudo apt-get install git-core
    ```

1. <span data-ttu-id="07863-164">이제 Git이 설치되었는지 확인하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-164">To verify that Git is now installed, type the following command:</span></span>

    ```console
    git --version
    ```

   <span data-ttu-id="07863-165">성공적으로 설치되면 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-165">If the installation is successful, you will see the following output:</span></span>

    ```console
    git version 2.17.1
    ```

1. <span data-ttu-id="07863-166">항상 이름과 메일을 제공하여 Git 설정을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-166">It is always a good practice to configure Git settings by providing your name and email.</span></span> <span data-ttu-id="07863-167">이 경우 중괄호(`{}`) 없이 이름 및 메일의 자리 표시자를 바꾸는 다음 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-167">For that, you need to issue the following commands, replacing the placeholders for name and email, without the curly braces (`{}`):</span></span>

    ```console
    git config --global user.name "{your name}"
    git config --global user.email "{your email}"
    ```

1. <span data-ttu-id="07863-168">Git에 의해 정보가 기록되었는지 확인하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-168">To verify that your information has been recorded by Git, type the following command:</span></span>

    ```console
    cat ~/.gitconfig
    ```

   <span data-ttu-id="07863-169">다음과 같이 표시된 이름과 메일과 함께 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-169">You should be seeing the following, with your name and email shown:</span></span>

    ```console
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-web-app"></a><span data-ttu-id="07863-170">웹앱에 대한 로컬 Git 리포지토리 초기화</span><span class="sxs-lookup"><span data-stu-id="07863-170">Initialize a local Git repository for your web app</span></span>

<span data-ttu-id="07863-171">Git 사용을 시작하려면 웹앱에 대한 로컬 Git 리포지토리를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-171">To start using Git, you need to initialize a local Git repository for the web app.</span></span>

1. <span data-ttu-id="07863-172">새 **터미널** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07863-172">Open a new **Terminal** window.</span></span>

1. <span data-ttu-id="07863-173">웹앱의 콘텐츠 루트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-173">Navigate to the content root folder of your web app.</span></span> <span data-ttu-id="07863-174">다음을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-174">You can type the following:</span></span>

    ```console
    cd ~/Documents/BestBikeApp/
    ```

    ![웹앱 콘텐츠 루트 폴더](../media-draft/7-web-app-content-root-folder.png)

1. <span data-ttu-id="07863-176">다음 명령을 실행하여 새 Git 리포지토리를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-176">Initialize a new Git repository by issuing the following command:</span></span>

    ```console
    git init
    ```

    <span data-ttu-id="07863-177">명령이 성공하면 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-177">If the command is successful, you receive a message like the following:</span></span>

    ```console
    Initialized empty Git repository in /home/your-user/Documents/BestBikeApp/.git/
    ```

1. <span data-ttu-id="07863-178">모든 웹앱 파일을 Git에 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-178">Stage all the web app files to Git.</span></span>

   <span data-ttu-id="07863-179">다음 단계는 Git에 웹앱 파일을 알리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-179">The next step is to let Git know about your web app files.</span></span> <span data-ttu-id="07863-180">Git에서 **준비**되도록 작업 디렉터리의 파일을 모두 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-180">Do that by adding all the files of the working directory so that they get **staged** by Git.</span></span> <span data-ttu-id="07863-181">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-181">Type the following command:</span></span>

    ```console
    git add .
    ```

    <span data-ttu-id="07863-182">위의 명령은 “.”로 표시되는 모든 파일을 Git의 스테이징 상태에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-182">The command above adds all files, represented by the ".", to the staging state of Git.</span></span>

1. <span data-ttu-id="07863-183">이제 Git에 변경 내용을 커밋해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-183">Now, you need to commit your changes to Git.</span></span>

   <span data-ttu-id="07863-184">Git을 사용하여 파일을 준비한 후 해당 파일을 로컬 머신의 **Git 커밋 기록**에 커밋해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-184">Once you stage the files with Git, you need to commit your files to the **Git commit history** on your local machine.</span></span> <span data-ttu-id="07863-185">다음 명령을 입력하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-185">You do that by typing the following command:</span></span>

   `git commit -m "Initial create"`

   <span data-ttu-id="07863-186">`commit` 명령은 만들고 있는 커밋에 메시지를 포함하도록 `-m` 인수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-186">The `commit` command accepts  `-m` argument to include a message with the commit you are creating.</span></span> <span data-ttu-id="07863-187">나중에 코드를 Azure에 푸시할 때 이 특정 커밋과 함께 저장된 동일한 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-187">Later on, when you push your code to Azure, you will be able to see the same message stored with this particular commit.</span></span>

## <a name="add-a-remote-for-the-local-git-repository"></a><span data-ttu-id="07863-188">로컬 Git 리포지토리에 대한 원격 추가</span><span class="sxs-lookup"><span data-stu-id="07863-188">Add a remote for the local Git repository</span></span>

<span data-ttu-id="07863-189">현재 새 로컬 Git 리포지토리를 성공적으로 초기화했습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-189">At this point, you have successfully initialized a new local Git repository.</span></span> <span data-ttu-id="07863-190">또한 모든 웹앱 파일을 Git에 커밋했습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-190">In addition, you've committed all of your web app files to Git.</span></span> <span data-ttu-id="07863-191">마지막 단계는 **원격**을 추가하여 Azure에서 호스트되는 원격에 로컬 Git 리포지토리를 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-191">What remains is to add a **remote** to connect your local Git repository to that hosted on Azure.</span></span>

<span data-ttu-id="07863-192">이렇게 하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-192">To do so, you need to:</span></span>

1. <span data-ttu-id="07863-193">위에서 확인한 **Git Clone URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-193">Copy the **Git clone url** that you saw above.</span></span>

1. <span data-ttu-id="07863-194">복사한 후 **터미널** 창으로 돌아가서 다음 Git 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-194">Once copied, you go back to the **Terminal** window and issue the following Git command:</span></span>

    ```console
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    <span data-ttu-id="07863-195">위의 Git 명령은 Azure에서 호스트된 항목에 로컬 Git 리포지토리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-195">The above Git command hooks your local Git repository to the one hosted on Azure.</span></span> <span data-ttu-id="07863-196">이제 로컬 및 원격 Git 리포지토리 간에 푸시 및 풀을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-196">Now, you can start pushing and pulling between the local and remote Git repositories!</span></span>

1. <span data-ttu-id="07863-197">위의 명령을 확인하려면 다음 Git 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-197">To verify the above command, type the following Git command:</span></span>

    ```
    git remote -v
    ```

    <span data-ttu-id="07863-198">위의 명령은 다음 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-198">The command above generates the following output:</span></span>

    ```console
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a><span data-ttu-id="07863-199">Azure에 코드 푸시</span><span class="sxs-lookup"><span data-stu-id="07863-199">Push your code to Azure</span></span>

<span data-ttu-id="07863-200">이제 Azure의 원격 Git 리포지토리에 로컬 Git 리포지토리를 연결했으므로 앱을 개발 및 빌드한 후 웹앱을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-200">Now that you have your local Git repository hooked to the remote Git repository on Azure, you will develop and build the app, and then push your web app to Azure.</span></span>

1. <span data-ttu-id="07863-201">다음 Git 명령을 입력하여 Azure의 원격 Git 리포지토리에 **마스터** 분기를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-201">Type the following Git command to push your **master** branch to the remote Git repository on Azure:</span></span>

    ```console
    git push origin master
    ```

1. <span data-ttu-id="07863-202">위의 **배포 자격 증명** 섹션에서 구성한 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-202">You will be prompted to enter the password that you have configured in the **Deployment credentials** section above.</span></span> <span data-ttu-id="07863-203">암호를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="07863-203">Enter your password and hit Enter.</span></span> <span data-ttu-id="07863-204">Git이 스테이징 배포 슬롯 아래에 구성된 Azure 원격 Git 리포지토리에 커밋된 파일을 업로드하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-204">Git starts uploading your committed files to the Azure remote Git repository configured under the staging deployment slot.</span></span>

## <a name="verify-the-web-app-is-uploaded-to-azure"></a><span data-ttu-id="07863-205">웹앱이 Azure에 업로드되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="07863-205">Verify the web app is uploaded to Azure</span></span>

1. <span data-ttu-id="07863-206">Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-206">Log in to the Azure portal.</span></span>

1. <span data-ttu-id="07863-207">왼쪽 탐색에서 **모든 리소스** 메뉴 항목을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-207">Locate and click on the **All Resources** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="07863-208">Azure Portal은 지금까지 Azure에 생성된 모든 리소스 목록으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-208">The Azure portal navigates you to the list of all resources created on Azure so far.</span></span>

1. <span data-ttu-id="07863-209">위에서 생성된 스테이징 슬롯을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-209">Locate and click on the staging slot created above.</span></span> <span data-ttu-id="07863-210">배포 슬롯은 웹앱으로 간주하므로 **모든 리소스** 아래에 웹앱 리소스로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-210">Remember, a deployment slot is considered a web app, and hence, it will appear as a web app resource under **All Resources**.</span></span>

1. <span data-ttu-id="07863-211">스테이징 배포 슬롯 블레이드에 도착하면 **배포 옵션**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-211">Once you arrive to the staging deployment slot blade, go to **Deployment options**.</span></span>

    ![웹앱을 업로드한 후 스테이징 배포 슬롯](../media-draft/7-staging-deployment-slot-after-uploading-files.png)

    <span data-ttu-id="07863-213">이제 머신에 로컬로 있는 첫 번째 커밋이 Azure Portal에 업로드되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-213">You will see that your first commit that you have locally on your machine is now uploaded to the Azure portal!</span></span>

    <span data-ttu-id="07863-214">Azure에서 호스트된 원격 Git 리포지토리에 코드를 로컬로 푸시하면 Azure가 이 작업을 기록했습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-214">By pushing your code locally to the remote Git repository hosted on Azure, Azure has recorded this operation.</span></span>

    <span data-ttu-id="07863-215">코드를 Azure에 푸시할 때마다 머신에서 로컬로 변경 내용을 커밋할 때 입력한 메시지와 함께 새 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-215">Every time you push your code to Azure, you will see a new record, together with the message that you type when committing your changes locally on your machine.</span></span>

1. <span data-ttu-id="07863-216">**스테이징 슬롯** URL을 방문하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-216">Let's visit the **staging slot** URL.</span></span> <span data-ttu-id="07863-217">위에서 언급한 URL이 기억나지 않는 경우에는 항상 스테이징 배포 슬롯의 **개요** 페이지로 이동하여 URL을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-217">The URL was mentioned above, however, if your forget that URL, you can always go to the **Overview** page of the staging deployment slot and pick up the URL.</span></span>

1. <span data-ttu-id="07863-218">브라우저 주소 표시줄에 URL [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-218">Type the following URL in your browser address bar: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span></span>

    ![온라인으로 호스트된 스테이징 슬롯](../media-draft/7-staging-slot-hosted-online.png)

<span data-ttu-id="07863-220">로컬 웹앱 파일을 Azure의 스테이징 배포 슬롯에 성공적으로 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-220">You have successfully uploaded your local web app files to the staging deployment slot on Azure.</span></span>

## <a name="swapping-the-staging-and-production-deployment-slots"></a><span data-ttu-id="07863-221">스테이징 및 프로덕션 배포 슬롯 교환</span><span class="sxs-lookup"><span data-stu-id="07863-221">Swapping the staging and production deployment slots</span></span>

<span data-ttu-id="07863-222">이제 Azure에서 호스트되는 스테이징 배포 슬롯에서 응용 프로그램이 시작하여 실행 중이므로 이 슬롯을 프로덕션 슬롯과 교환할 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="07863-222">Now that the application is up and running on the staging deployment slot hosted on Azure, it is time to swap this slot with the production one.</span></span> <span data-ttu-id="07863-223">이렇게 하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="07863-223">To do so, follow these steps:</span></span>

1. <span data-ttu-id="07863-224">단원 #2에서 생성된 원래 웹앱 블레이드를 찾아서 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-224">Locate and navigate to the original web app blade, created in Unit #2.</span></span>

1. <span data-ttu-id="07863-225">왼쪽 탐색에서 **배포 슬롯** 메뉴 항목을 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-225">Locate and click the **Deployment slots** menu item on the left-side navigation.</span></span>

    ![웹앱 배포 슬롯 블레이드](../media-draft/7-web-app-slots.png)

1. <span data-ttu-id="07863-227">블레이드 위쪽에서 **교환** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-227">Locate and click on the **Swap** button at the top of the blade.</span></span>

1. <span data-ttu-id="07863-228">Azure Portal이 **교환** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-228">The Azure portal navigates you to the **Swap** blade.</span></span>

    ![교환 블레이드](../media-draft/7-swap-blade.png)

1. <span data-ttu-id="07863-230">**교환** 필드에서 **교환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-230">For the **Swap** field, select **Swap**.</span></span>

1. <span data-ttu-id="07863-231">**원본** 필드에서 **스테이징**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-231">For the **Source** field, select **Staging**.</span></span>

1. <span data-ttu-id="07863-232">**대상** 필드에서 **프로덕션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-232">For the **Destination** field, select **Production**.</span></span>

1. <span data-ttu-id="07863-233">블레이드 맨 아래에서 **확인** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-233">Locate and click on the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="07863-234">Azure가 교환 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-234">Azure starts the swapping process.</span></span> <span data-ttu-id="07863-235">일반적으로 이 작업은 교환 중인 웹앱의 크기에 따라 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="07863-235">Usually, this operation takes a few seconds, depending on the size of the web app being swapped.</span></span>

1. <span data-ttu-id="07863-236">작업이 종료되면 웹앱 URL [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-236">Once the operation ends, visit the web app URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span></span>

    ![웹앱 페이지](../media-draft/7-web-app-page.png)

    <span data-ttu-id="07863-238">교환 작업이 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-238">The swapping operation has been successful!</span></span> <span data-ttu-id="07863-239">이제 스테이징 배포 슬롯에 업로드한 코드도 프로덕션 슬롯에서도 호스트되고 있음을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-239">You can now see the code that you uploaded to the staging deployment slot also being hosted on the production slot!</span></span>

1. <span data-ttu-id="07863-240">이제 스테이징 슬롯 URL [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-240">Now, visit the URL of the staging slot: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span></span>

    ![스테이징 웹앱](../media-draft/7-staging-after-swapping.png)

    <span data-ttu-id="07863-242">이제 스테이징 배포 슬롯에는 프로덕션 슬롯에서 이전에 호스트된 원래 기본 웹 응용 프로그램 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07863-242">The staging deployment slot now contains the original, default web application files that were previously hosted under the production slot.</span></span>

<span data-ttu-id="07863-243">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="07863-243">Congratulations!</span></span> <span data-ttu-id="07863-244">Azure에 웹앱을 성공적으로 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="07863-244">You have successfully uploaded your web app to Azure!</span></span>
