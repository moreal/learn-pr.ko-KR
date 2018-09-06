이 연습에서는 Azure에 ASP.NET Core 응용 프로그램을 업로드합니다.

## <a name="create-a-staging-deployment-slot"></a>준비 배포 슬롯 만들기

1. 왼쪽 탐색에서 **배포 슬롯** 메뉴 항목을 찾아 클릭합니다.

1. Azure가 아래와 같이 **배포 슬롯** 블레이드를 엽니다.

    ![배포 슬롯](../media-draft/7-deployment-slot-blade.png)

1. 배포 슬롯 블레이드의 위쪽 탐색 모음에서 **+ 슬롯 추가** 단추를 찾아 클릭합니다.

1. Azure Portal이 아래와 같이 **슬롯 추가** 블레이드를 엽니다.

    ![슬롯 추가](../media-draft/7-new-deployment-slot-blade.png)

    배포 슬롯에 이름을 지정합니다. 이 경우 **스테이징**을 사용합니다.

    **구성 원본**을 선택하려면 두 가지 옵션이 있습니다.

    1. Azure에 생성된 다른 슬롯 또는 웹앱에서 구성 요소를 복제하려면 선택합니다.

    1. 구성 요소를 복제하지 않도록 선택할 수 있습니다. 이 경우 **기존 슬롯에서 구성 복제 안 함** 옵션을 선택합니다.

    두 번째 옵션인 **기존 슬롯에서 구성을 복제**을 선택합니다.

1. 블레이드 맨 아래에서 **확인** 단추를 찾아 클릭합니다.

1. 배포 슬롯이 성공적으로 만들어지면 Azure Portal은 다시 웹앱의 **배포 슬롯** 블레이드로 이동합니다.

    이제 방금 만든 새 배포 슬롯을 볼 수 있습니다.

    ![생성된 배포 슬롯](../media-draft/7-deployment-slot-created.png)

1. 새 배포 슬롯을 찾아 클릭합니다.

1. Azure Portal은 새로 만든 배포 슬롯의 **개요** 페이지로 이동합니다.

    ![스테이징 배포 슬롯](../media-draft/7-deployment-slot-staging.png)

    스테이징 배포 슬롯의 **URL**을 확인합니다. 이 URL은 이 단원의 첫 부분에서 이전에 본 것과 동일한 URL입니다.

    배포 슬롯은 Azure 내의 웹앱으로 처리됩니다. 그러나 이는 원래 웹앱의 자식인 특수한 유형이며 원래 웹앱으로 교환될 수 있습니다.

    **URL**을 클릭하면 Azure Portal에서 처음 만들 때 Azure가 웹앱용으로 만든 것과 동일한 기본 페이지가 표시됩니다.

이제 스테이징 배포 슬롯이 성공적으로 생성되었으므로 **배포 자격 증명**을 구성해야 합니다.

## <a name="create-deployment-credentials"></a>배포 자격 증명 만들기

실제 배포 프로세스를 시작하려면 먼저 Azure에서 배포 자격 증명을 설정해야 합니다. 이런 이유로 고유한 배포 자격 증명을 만드는 방법을 알아봅니다.

1. 왼쪽 탐색에서 **배포 자격 증명** 메뉴 항목을 찾아 클릭합니다.

1. Azure Portal은 아래와 같이 **배포 자격 증명** 블레이드로 이동합니다.

    ![배포 자격 증명](../media-draft/7-deployment-credentials.png)

    선택한 **사용자 이름**과 **암호**를 입력한 후 암호를 다시 한번 확인합니다.

    > 암호를 잊지 않도록 사용자 이름과 암호를 적어 두세요. 나중에 Azure에 대한 코드 업로드 및 배포를 시작할 때 필요합니다.

    사용자 이름과 암호를 결정한 후 **배포 자격 증명** 블레이드 맨 위에 있는 **저장** 단추를 찾아 클릭합니다.

이제 배포 자격 증명 정보가 성공적으로 생성되었으므로 **배포 옵션**을 구성해야 합니다.

## <a name="use-a-local-git-repository-as-your-deployment-option"></a>로컬 Git 리포지토리를 배포 옵션으로 사용

이제 코드를 업로드하는 프로세스를 시작할 수 있도록 Azure에서 로컬 Git 리포지토리를 만들어 보겠습니다.

1. 왼쪽 탐색에서 **배포 옵션** 메뉴 항목을 찾아 클릭합니다.

1. Azure Portal은 아래와 같이 **배포 옵션** 블레이드로 이동합니다.

    ![배포 옵션](../media-draft/7-deployment-options.png)

1. **원본 선택/필수 설정 구성**을 클릭합니다.

    ![배포 자격 증명](../media-draft/7-deployment-sources.png)

1. Azure Portal에 구성하고 사용할 수 있는 사용 가능한 옵션이 표시됩니다. 이 경우 **로컬 Git 리포지토리** 옵션을 선택합니다.

    ![로컬 Git 리포지토리](../media-draft/7-local-git-repo.png)

1. 블레이드 맨 아래에서 **확인** 단추를 찾아 클릭합니다.

1. 왼쪽 탐색에서 **개요** 메뉴 항목을 찾아 클릭합니다.

    ![Git이 구성된 배포 슬롯](../media-draft/7-staging-after-setting-git.png)

    다음과 같은 두 가지 중요한 정보가 있습니다.
    - **Git/배포 사용자 이름**: 나중에 Azure의 로컬 Git 리포지토리에 연결하는 데 사용할 자격 증명입니다.

    - **Git Clone URL**: 로컬 웹 응용 프로그램 리포지토리에 **원격**으로 사용할 로컬 Git 리포지토리 URL입니다.

이제 스테이징 배포 슬롯에 코드를 업로드할 차례입니다.

## <a name="install-git-on-your-machine"></a>머신에 Git 설치

내 Ubuntu 18.04 머신에 Git을 설치하고 있습니다.

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

1. 항상 이름과 메일을 제공하여 Git 설정을 구성하는 것이 좋습니다. 이 경우 중괄호(`{}`) 없이 이름 및 메일의 자리 표시자를 바꾸는 다음 명령을 실행해야 합니다.

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

## <a name="initialize-a-local-git-repository-for-your-web-app"></a>웹앱에 대한 로컬 Git 리포지토리 초기화

Git 사용을 시작하려면 웹앱에 대한 로컬 Git 리포지토리를 초기화해야 합니다.

1. 새 **터미널** 창을 엽니다.

1. 웹앱의 콘텐츠 루트 폴더로 이동합니다. 다음을 입력할 수 있습니다.

    ```console
    cd ~/Documents/BestBikeApp/
    ```

    ![웹앱 콘텐츠 루트 폴더](../media-draft/7-web-app-content-root-folder.png)

1. 다음 명령을 실행하여 새 Git 리포지토리를 초기화합니다.

    ```console
    git init
    ```

    명령이 성공하면 다음과 같은 메시지가 표시됩니다.

    ```console
    Initialized empty Git repository in /home/your-user/Documents/BestBikeApp/.git/
    ```

1. 모든 웹앱 파일을 Git에 준비합니다.

   다음 단계는 Git에 웹앱 파일을 알리는 것입니다. Git에서 **준비**되도록 작업 디렉터리의 파일을 모두 추가하면 됩니다. 다음 명령을 입력합니다.

    ```console
    git add .
    ```

    위의 명령은 “.”로 표시되는 모든 파일을 Git의 스테이징 상태에 추가합니다.

1. 이제 Git에 변경 내용을 커밋해야 합니다.

   Git을 사용하여 파일을 준비한 후 해당 파일을 로컬 머신의 **Git 커밋 기록**에 커밋해야 합니다. 다음 명령을 입력하여 이를 수행합니다.

   `git commit -m "Initial create"`

   `commit` 명령은 만들고 있는 커밋에 메시지를 포함하도록 `-m` 인수를 허용합니다. 나중에 코드를 Azure에 푸시할 때 이 특정 커밋과 함께 저장된 동일한 메시지를 볼 수 있습니다.

## <a name="add-a-remote-for-the-local-git-repository"></a>로컬 Git 리포지토리에 대한 원격 추가

현재 새 로컬 Git 리포지토리를 성공적으로 초기화했습니다. 또한 모든 웹앱 파일을 Git에 커밋했습니다. 마지막 단계는 **원격**을 추가하여 Azure에서 호스트되는 원격에 로컬 Git 리포지토리를 연결하는 것입니다.

이렇게 하려면 다음을 수행해야 합니다.

1. 위에서 확인한 **Git Clone URL**을 복사합니다.

1. 복사한 후 **터미널** 창으로 돌아가서 다음 Git 명령을 실행합니다.

    ```console
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    위의 Git 명령은 Azure에서 호스트된 항목에 로컬 Git 리포지토리를 연결합니다. 이제 로컬 및 원격 Git 리포지토리 간에 푸시 및 풀을 시작할 수 있습니다.

1. 위의 명령을 확인하려면 다음 Git 명령을 입력합니다.

    ```
    git remote -v
    ```

    위의 명령은 다음 출력을 생성합니다.

    ```console
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a>Azure에 코드 푸시

이제 Azure의 원격 Git 리포지토리에 로컬 Git 리포지토리를 연결했으므로 앱을 개발 및 빌드한 후 웹앱을 Azure에 푸시합니다.

1. 다음 Git 명령을 입력하여 Azure의 원격 Git 리포지토리에 **마스터** 분기를 푸시합니다.

    ```console
    git push origin master
    ```

1. 위의 **배포 자격 증명** 섹션에서 구성한 암호를 입력하라는 메시지가 표시됩니다. 암호를 입력하고 Enter 키를 누릅니다. Git이 스테이징 배포 슬롯 아래에 구성된 Azure 원격 Git 리포지토리에 커밋된 파일을 업로드하기 시작합니다.

## <a name="verify-the-web-app-is-uploaded-to-azure"></a>웹앱이 Azure에 업로드되었는지 확인

1. Azure Portal에 로그인합니다.

1. 왼쪽 탐색에서 **모든 리소스** 메뉴 항목을 찾아 클릭합니다.

1. Azure Portal은 지금까지 Azure에 생성된 모든 리소스 목록으로 이동합니다.

1. 위에서 생성된 스테이징 슬롯을 찾아 클릭합니다. 배포 슬롯은 웹앱으로 간주하므로 **모든 리소스** 아래에 웹앱 리소스로 표시됩니다.

1. 스테이징 배포 슬롯 블레이드에 도착하면 **배포 옵션**으로 이동합니다.

    ![웹앱을 업로드한 후 스테이징 배포 슬롯](../media-draft/7-staging-deployment-slot-after-uploading-files.png)

    이제 머신에 로컬로 있는 첫 번째 커밋이 Azure Portal에 업로드되었음을 알 수 있습니다.

    Azure에서 호스트된 원격 Git 리포지토리에 코드를 로컬로 푸시하면 Azure가 이 작업을 기록했습니다.

    코드를 Azure에 푸시할 때마다 머신에서 로컬로 변경 내용을 커밋할 때 입력한 메시지와 함께 새 레코드가 표시됩니다.

1. **스테이징 슬롯** URL을 방문하겠습니다. 위에서 언급한 URL이 기억나지 않는 경우에는 항상 스테이징 배포 슬롯의 **개요** 페이지로 이동하여 URL을 선택할 수 있습니다.

1. 브라우저 주소 표시줄에 URL [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/)을 입력합니다.

    ![온라인으로 호스트된 스테이징 슬롯](../media-draft/7-staging-slot-hosted-online.png)

로컬 웹앱 파일을 Azure의 스테이징 배포 슬롯에 성공적으로 업로드했습니다.

## <a name="swapping-the-staging-and-production-deployment-slots"></a>스테이징 및 프로덕션 배포 슬롯 교환

이제 Azure에서 호스트되는 스테이징 배포 슬롯에서 응용 프로그램이 시작하여 실행 중이므로 이 슬롯을 프로덕션 슬롯과 교환할 차례입니다. 이렇게 하려면 다음 단계를 따르세요.

1. 단원 #2에서 생성된 원래 웹앱 블레이드를 찾아서 이동합니다.

1. 왼쪽 탐색에서 **배포 슬롯** 메뉴 항목을 찾아 클릭합니다.

    ![웹앱 배포 슬롯 블레이드](../media-draft/7-web-app-slots.png)

1. 블레이드 위쪽에서 **교환** 단추를 찾아 클릭합니다.

1. Azure Portal이 **교환** 블레이드로 이동합니다.

    ![교환 블레이드](../media-draft/7-swap-blade.png)

1. **교환** 필드에서 **교환**을 선택합니다.

1. **원본** 필드에서 **스테이징**을 선택합니다.

1. **대상** 필드에서 **프로덕션**을 선택합니다.

1. 블레이드 맨 아래에서 **확인** 단추를 찾아 클릭합니다.

1. Azure가 교환 프로세스를 시작합니다. 일반적으로 이 작업은 교환 중인 웹앱의 크기에 따라 몇 초 정도 걸립니다.

1. 작업이 종료되면 웹앱 URL [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/)을 방문합니다.

    ![웹앱 페이지](../media-draft/7-web-app-page.png)

    교환 작업이 성공했습니다. 이제 스테이징 배포 슬롯에 업로드한 코드도 프로덕션 슬롯에서도 호스트되고 있음을 볼 수 있습니다.

1. 이제 스테이징 슬롯 URL [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/)을 방문합니다.

    ![스테이징 웹앱](../media-draft/7-staging-after-swapping.png)

    이제 스테이징 배포 슬롯에는 프로덕션 슬롯에서 이전에 호스트된 원래 기본 웹 응용 프로그램 파일이 포함됩니다.

축하합니다. Azure에 웹앱을 성공적으로 배포했습니다.
