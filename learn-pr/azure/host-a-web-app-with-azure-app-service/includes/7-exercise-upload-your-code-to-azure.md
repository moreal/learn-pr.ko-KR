이 장치를 Azure App Service에 ASP.NET Core 응용 프로그램을 업로드 합니다.

## <a name="create-a-staging-deployment-slot"></a>준비 배포 슬롯 만들기

1. 이전에 만든 App Service 리소스 (웹 앱)를 엽니다. 해당 리소스 페이지를 닫은 경우 찾을 수 있습니다 다시에서 앱을 검색 하 여 **모든 리소스** 또는 포함 된 리소스 그룹 **리소스 그룹**합니다.

1. 왼쪽 탐색 영역에서 **배포 슬롯** 메뉴 항목을 클릭합니다.

1. 내부를 **배포 슬롯** 페이지를 클릭 합니다 **슬롯 추가** 배포 슬롯 페이지의 위쪽 탐색 모음에서 단추입니다.

1. Azure portal이 열립니다는 **슬롯 추가** 아래와 같이 페이지입니다.

    1. 배포 슬롯에 이름을 지정합니다. 이 예제의 경우 `staging`입니다.

    2. **구성 원본** 선택 시에는 두 가지 옵션 중 하나를 사용할 수 있습니다.

        * App Service 앱 또는 기존 배포 슬롯에서 구성 요소를 복제 하도록 선택할 수 있습니다.
        * 또는 구성 요소를 복제하지 않을 수도 있습니다. **기존 슬롯에서 구성 복제 안 함** 옵션을 선택합니다.

        이 배포 슬롯의 경우 두 번째 옵션인 **기존 슬롯에서 구성 복제 안 함**을 선택합니다. 여기서는 요소를 직접 구성합니다.

    ![새 스테이징 배포 슬롯의 구성을 보여주는 Azure Portal의 스크린샷.](../media/7-new-deployment-slot-blade.png)

1. 클릭 합니다 **확인** 에 새 배포 슬롯 만들기 페이지의 맨 위에 있는 단추입니다.

1. 배포 슬롯을 성공적으로 만들어지면 Azure portal 이동 다시 합니다 **배포 슬롯** 웹 앱의 페이지입니다.

    이제 방금 만든 새 배포 슬롯을 볼 수 있습니다.

    ![만든 새 슬롯을 사용 하 여 배포 슬롯 페이지를 보여주는 Azure portal의 스크린샷.](../media/7-deployment-slot-created.png)

1. 새 배포 슬롯을 선택합니다.

1. Azure Portal에 새로 만든 배포 슬롯의 **개요** 페이지가 열립니다.

    ![스테이징 배포 슬롯](../media/7-deployment-slot-staging.png)

    스테이징 배포 슬롯의 **URL**을 확인합니다. 이 URL은 이전에 확인했던 것과는 다른 슬롯 이름이 추가된 URL입니다.

    배포 슬롯은 Azure 내에서 전체 App Service 앱으로 처리 됩니다. 그러나 원래 앱의 자식 이며 원래 앱과 교환할 수 있는 특별 한 형식입니다.

    클릭할 경우 합니다 **URL**, 만든 Azure 배포 슬롯 "앱"에 대 한 Azure portal에서 만든이 처음으로 동일한 기본 페이지가 표시 됩니다.

이제 스테이징 배포 슬롯이 성공적으로 생성되었으므로 **배포 자격 증명**을 구성해야 합니다.

## <a name="create-deployment-credentials"></a>배포 자격 증명 만들기

실제 배포 프로세스를 시작하려면 먼저 Azure에서 배포 자격 증명을 설정해야 합니다. 이런 이유로 고유한 배포 자격 증명을 만드는 방법을 알아봅니다.

1. 왼쪽 탐색 영역에서 **배포 자격 증명** 메뉴 항목을 클릭합니다.

1. Azure portal로 이동 합니다 **배포 자격 증명** 아래와 같이 페이지입니다.

    선택한 **사용자 이름**과 **암호**를 입력한 후 암호를 다시 한번 확인합니다.

    > [!NOTE]
    > 암호를 잊지 않도록 사용자 이름과 암호를 적어 두세요. 나중에 Azure에 대한 코드 업로드 및 배포를 시작할 때 필요합니다.

    ![필수 필드에 예제에서는 자격 증명을 사용 하 여 스테이징 슬롯의 배포 자격 증명 페이지를 보여주는 Azure portal의 스크린샷.](../media/7-deployment-credentials.png)

1. 클릭 합니다 **저장** 맨 위에 있는 단추를 **배포 자격 증명** 페이지입니다.

이제 배포 자격 증명이 생성되었으므로 다른 배포 옵션을 구성해야 합니다.

## <a name="use-a-local-git-repository-as-your-deployment-option"></a>로컬 Git 리포지토리를 배포 옵션으로 사용

다음으로 만들겠습니다 로컬 Git 리포지토리를 Azure에 코드 업로드를 시작할 수 있도록 합니다.

1. 내 합니다 **준비** 배포 슬롯 "앱"을 클릭 합니다 **배포 옵션** 왼쪽 탐색 모음에 메뉴 항목입니다.

1. Azure portal로 이동 합니다 **배포 옵션** 페이지입니다.

1. **원본 선택**을 클릭하여 필수 설정을 구성합니다.

1. Azure Portal에 구성하고 사용할 수 있는 사용 가능한 옵션이 표시됩니다. 이 경우 **로컬 Git 리포지토리** 옵션을 선택합니다.

1. 에 게 반환할 수는 **배포 옵션** 페이지입니다. 클릭 합니다 **확인** 배포 원본 설정 페이지의 맨 위에 있는 단추입니다.

1. 이제 왼쪽 탐색 영역의 **배포 센터 (미리 보기)** 섹션으로 이동하여 새 배포 세부 정보를 확인합니다.

    ![강조 표시 된 슬롯에 대 한 Git 복제 Uri를 사용 하 여 배포 슬롯의 배포 센터 페이지를 보여 주는 Azure portal의 스크린샷.](../media/7-staging-after-setting-git.png)

    여기서 중요 한 정보를 **Git 복제 Uri**,으로 사용 하는 로컬 Git 리포지토리 URL 인를 **원격** 로컬 응용 프로그램 코드 리포지토리에 대 한 합니다.

이제 스테이징 배포 슬롯에 코드를 업로드할 차례입니다.

## <a name="install-git-on-your-machine"></a>머신에 Git 설치

Git을 아직 설치하지 않았으면 Linux 머신에 Git을 설치합니다.

> [!NOTE]
> 여기서 제공하는 지침은 Ubuntu 18.04용이므로 사용 중인 배포와 버전에 따라 Git 설치 단계는 달라질 수 있습니다. [Linux Git 설치 지침](https://git-scm.com/download/linux)에서 적절한 단계를 확인하세요.

1. 새 **터미널** 창 열기

1. 다음 명령을 입력합니다. Ubuntu 사용자 암호를 입력하라는 메시지가 표시됩니다.

    ```console
    sudo apt-get update
    ```

1. 업데이트가 성공하면 다음 명령을 입력하여 Git을 로컬로 설치합니다. 머신에서 Git 설치를 허용할지 묻는 메시지가 표시됩니다.

    ```console
    sudo apt-get install git-core
    ```

1. 이제 Git이 설치되었는지 확인하려면 다음 명령을 입력합니다.

    ```console
    git --version
    ```

   성공적으로 설치되면 다음 출력이 표시됩니다.

    ```console
    git version 2.17.1
    ```

1. 항상 이름과 메일을 제공하여 Git 설정을 구성하는 것이 좋습니다. 즉, `{your name}` 및 `{your email}` 자리 표시자를 이름과 이메일로 바꿔 다음 명령을 실행해야 합니다. 이때 중괄호 `{}`는 제거합니다.

    ```console
    git config --global user.name "{your name}"
    git config --global user.email "{your email}"
    ```

1. Git에 의해 정보가 기록되었는지 확인하려면 다음 명령을 입력합니다.

    ```console
    cat ~/.gitconfig
    ```

   다음과 같이 표시된 이름과 메일과 함께 표시되어야 합니다.

    ```console
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-code"></a>코드에 대 한 로컬 Git 리포지토리를 초기화 합니다.

Git를 사용 하 여을 시작 하려면.NET Core 응용 프로그램 코드에 대 한 로컬 Git 리포지토리를 초기화 해야 합니다.

1. 새 **터미널** 창을 엽니다.

1. 이전에 만든.NET Core 앱의 콘텐츠 루트 폴더로 이동 합니다. 다음을 입력하면 됩니다.

    ```console
    cd ~/Documents/BestBikeApp/
    ```

1. 다음 명령을 실행하여 새 Git 리포지토리를 초기화합니다.

    ```console
    git init
    ```

    명령이 성공하면 다음과 같은 메시지가 표시됩니다.

    ```console
    Initialized empty Git repository in /home/{your-user}/Documents/BestBikeApp/.git/
    ```

1. Git으로 모든 응용 프로그램 파일을 준비 합니다.

   다음 단계는 Git 응용 프로그램 파일에 대 한 알 수 있도록 합니다. Git에서 **준비**되도록 작업 디렉터리의 파일을 모두 추가하면 됩니다. 다음 명령을 입력합니다.

    ```console
    git add .
    ```

    위의 명령은 “.”로 표시되는 모든 파일을 Git의 스테이징 상태에 추가합니다.

1. 이제 Git에 변경 내용을 커밋해야 합니다.

   Git을 사용하여 파일을 준비한 후 해당 파일을 로컬 머신의 **Git 커밋 기록**에 커밋해야 합니다. 다음 명령을 입력하여 이를 수행합니다.

    ```console
   git commit -m "Initial create"
    ```

   `commit` 명령은 만들고 있는 커밋에 메시지를 포함하도록 `-m` 인수를 허용합니다. 나중에 코드를 Azure에 푸시할 때 이 특정 커밋과 함께 저장된 동일한 메시지를 볼 수 있습니다.

## <a name="add-a-remote-for-the-local-git-repository"></a>로컬 Git 리포지토리에 대한 원격 추가

현재 새 로컬 Git 리포지토리를 성공적으로 초기화했습니다. 또한 약정 한 응용 프로그램 파일의 모든 Git입니다. 마지막 단계는 **원격**을 추가하여 Azure에서 호스트되는 원격에 로컬 Git 리포지토리를 연결하는 것입니다.

이렇게 하려면 다음을 수행해야 합니다.

1. 위에서 확인한 **Git Clone URL**을 복사합니다.

1. 복사한 후 **터미널** 창으로 돌아가서 다음 Git 명령을 실행합니다.

    ```console
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    위의 Git 명령은 Azure에서 호스트된 항목에 로컬 Git 리포지토리를 연결합니다. 이제 로컬 및 원격 Git 리포지토리 간에 푸시 및 풀을 시작할 수 있습니다.

1. 위의 명령을 확인하려면 다음 Git 명령을 입력합니다.

    ```console
    git remote -v
    ```

    위의 명령은 다음 출력을 생성합니다.

    ```console
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a>Azure에 코드 푸시

했으므로 Azure에서 원격 Git 리포지토리에 후크 로컬 Git 리포지토리를 개발 및 앱을 빌드하고 Azure에 응용 프로그램 코드를 푸시합니다.

1. 다음 Git 명령을 입력하여 Azure의 원격 Git 리포지토리에 **마스터** 분기를 푸시합니다.

    ```console
    git push origin master
    ```

1. 위의 **배포 자격 증명** 섹션에서 구성한 암호를 입력하라는 메시지가 표시됩니다. 암호를 입력하고 Enter 키를 누릅니다. Git이 스테이징 배포 슬롯 아래에 구성된 Azure 원격 Git 리포지토리에 커밋된 파일을 업로드하기 시작합니다.

## <a name="verify-the-code-is-uploaded-to-azure"></a>코드를 Azure에 업로드 되었는지 확인

1. Azure Portal에 로그인합니다.

1. 왼쪽 탐색 영역에서 **모든 리소스** 메뉴 항목을 클릭합니다.

1. Azure Portal은 지금까지 Azure에 생성된 모든 리소스 목록으로 이동합니다.

1. 위에서 생성된 스테이징 슬롯을 클릭합니다. 배포 슬롯을 앱으로 간주 되 고 따라서에서 App Service 리소스로 나타납니다 기억 **모든 리소스**합니다.

1. 스테이징 배포 슬롯 페이지로 열리면 이동할 **배포 옵션**합니다.

    이제 머신에 로컬로 있는 첫 번째 커밋이 Azure Portal에 업로드되었음을 알 수 있습니다.

    App Service에서 원격 Git 리포지토리를 로컬로 코드를 푸시할 때 Azure는이 작업을 기록 합니다.

    코드를 Azure에 푸시할 때마다 머신에서 로컬로 변경 내용을 커밋할 때 입력한 메시지와 함께 새 레코드가 표시됩니다.

    ![Azure portal 개발 옵션 페이지에서 최근 Git 리포지토리 배포를 보여 주는 스크린샷.](../media/7-staging-deployment-slot-after-uploading-files.png)

1. **스테이징 슬롯** URL을 방문하겠습니다. 위에서 언급한 URL이 기억나지 않는 경우에는 항상 스테이징 배포 슬롯의 **개요** 페이지로 이동하여 URL을 선택할 수 있습니다.

1. 브라우저 주소 표시줄에 URL [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/)을 입력합니다.

    ![스테이징 배포 슬롯 웹 사이트의 웹 브라우저 보기를 보여주는 스크린샷.](../media/7-staging-slot-hosted-online.png)

Azure의 스테이징 배포 슬롯에 로컬 응용 프로그램 파일을 업로드 했습니다.

## <a name="swapping-the-staging-and-production-deployment-slots"></a>스테이징 및 프로덕션 배포 슬롯 교환

이제 Azure에서 호스트되는 스테이징 배포 슬롯에서 응용 프로그램이 시작하여 실행 중이므로 이 슬롯을 프로덕션 슬롯과 교환할 차례입니다. 이렇게 하려면 다음 단계를 따르세요.

1. 이전에 만든 원래 앱 페이지로 이동 합니다. 원래 웹 앱을 찾을 수 있습니다 합니다 **모든 리소스** 페이지입니다.

1. 왼쪽 탐색 영역에서 **배포 슬롯** 메뉴 항목을 클릭합니다.

1. 클릭 합니다 **교환** 페이지의 맨 위에 있는 단추입니다.

1. Azure portal을 탐색 하는 **교환** 페이지입니다.

1. **교환** 필드에서 **교환**을 선택합니다.

1. **원본** 필드에서 **스테이징**을 선택합니다.

1. **대상** 필드에서 **프로덕션**을 선택합니다.

    ![배포 슬롯 교환 페이지를 보여 주는 Azure portal의 스크린샷.](../media/7-swap-blade.png)

1. 클릭 합니다 **확인** 페이지의 맨 위에 있는 단추입니다.

1. Azure가 교환 프로세스를 시작합니다. 일반적으로 이 작업은 교환 중인 웹앱의 크기에 따라 몇 초 정도 걸립니다.

1. 작업이 종료되면 웹앱 URL [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/)을 방문합니다.

    ![이제 기본 웹앱으로 호스팅되는 이전 스테이징 배포 슬롯의 웹 브라우저 보기를 보여주는 스크린샷.](../media/7-web-app-page.png)

    교환 작업이 성공했습니다. 이제 스테이징 배포 슬롯에 업로드한 코드도 프로덕션 슬롯에서도 호스트되고 있음을 볼 수 있습니다.

1. 이제 스테이징 슬롯 URL [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/)을 방문합니다.

    ![이제 스테이징 배포 슬롯 웹앱으로 호스팅되는 이전 기본 배포 슬롯의 웹 브라우저 보기를 보여주는 스크린샷.](../media/7-staging-after-swapping.png)

    스테이징 배포 슬롯은 이제 원래 기본 프로덕션 슬롯에서 이전에 제공 된 HTML 파일이 사용 됩니다.

축하합니다. Azure에 응용 프로그램 코드를 업로드 하 고 배포 슬롯을 교환 했습니다.
