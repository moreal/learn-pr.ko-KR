[연습 1](#Exercise1)에서 Azure 웹앱 봇을 만든 경우 Azure 웹앱을 배포하여 해당 봇을 호스트하였습니다. 그러나 아직 봇에는 일부 코드가 필요하며 해당 코드가 Azure 웹앱에 배포되어야 합니다. 다행히 코드는 Azure Bot Service에 의해 생성되었습니다. 이 연습에서는 Visual Studio Code를 사용하여 해당 코드를 로컬 Git 리포지토리에 배치하고, 변경 내용을 로컬 리포지토리에서 봇을 호스팅하는 Azure 웹앱에 연결된 원격 리포지토리로 푸시하여 Azure에 봇을 게시합니다. 이러한 프로세스를 [연속 통합](https://en.wikipedia.org/wiki/Continuous_integration)이라고 합니다.

1. [Git](https://git-scm.com/)이 PC에 설치되어 있지 않으면 https://git-scm.com/downloads로 이동하여 운영 체제에 맞는 Git 클라이언트를 설치하세요. Git은 무료 오픈 소스 분산 버전 제어 시스템으로, Visual Studio Code와 원활하게 통합됩니다. Git이 설치되어 있는지 잘 모르는 경우 명령 프롬프트 또는 터미널 창을 열고 다음 명령을 실행합니다.

    ``` 
    git --version
    ```

    버전 번호가 표시되면 Git 클라이언트가 설치되어 있는 것입니다.

1. Node.js가 PC에 설치되어 있지 않으면 https://nodejs.org/로 이동하여 최신 LTS 버전을 설치합니다. 명령 프롬프트 또는 터미널 창을 열고 다음 명령을 입력하면 Node.js가 설치되어 있는지 확인할 수 있습니다.

    ```
    node --version
    ```

    Node가 설치되어 있으면 버전 번호가 표시됩니다.

1. Visual Studio Code가 PC에 설치되어 있지 않으면 지금 https://code.visualstudio.com/으로 이동하여 설치하세요.

1. 봇의 소스 코드를 보관하려면 하드 디스크에서 선택한 위치에 “Factbot”이라는 폴더를 만듭니다.

1. Azure Portal로 돌아가서 “factbot-rg” 리소스 그룹을 엽니다. 그런 다음, [연습 1](#Exercise1)에서 만든 웹앱 봇을 클릭합니다.

    ![웹앱 봇 열기](../media-draft/4-open-web-app-bot.png)

1. 왼쪽 메뉴에서 **빌드**를 클릭한 후 **zip 파일 다운로드**를 클릭하여 봇의 소스 코드가 포함된 zip 파일을 준비합니다. zip 파일이 준비되면 **zip 파일 다운로드** 단추를 클릭하여 다운로드합니다. 다운로드가 완료되면 zip 파일의 콘텐츠를 4단계에서 만든 “Factbot” 폴더로 복사합니다.

    ![소스 코드 다운로드](../media-draft/4-download-source.png)

1. 계속 “빌드” 블레이드에서 **연속 배포 구성**을 클릭합니다. 뒤이은 블레이드의 맨 위에서 **설정**을 클릭한 다음, **소스 선택**을 클릭합니다. 그런 다음, **로컬 Git 리포지토리**를 배포 원본으로 선택하고 **확인**을 클릭합니다. 

    ![로컬 Git 리포지토리를 배포 원본으로 지정](../media-draft/4-portal-set-local-git.png)

1. “배포” 블레이드를 닫고 왼쪽 메뉴에서 **모든 App Service 설정**을 클릭합니다.

1. **배포 자격 증명**을 클릭한 후 사용자 이름 및 암호를 입력합니다. 사용자 이름은 Azure 내에서 고유해야 하므로 “FactbotAdministrator” 이외의 이름을 입력해야 할 수도 있습니다. 그런 다음, **저장**을 클릭하고 블레이드를 닫습니다.

    ![배포 자격 증명 입력](../media-draft/4-portal-enter-ci-creds.png)

1. Visual Studio Code를 시작하고 **파일** > **폴더 열기...** 명령을 사용하여 6단계에서 봇의 소스 코드를 복사한 “Factbot” 폴더를 엽니다.

1. Visual Studio Code 왼쪽의 작업 막대에서 **소스 제어** 단추를 클릭하고 맨 위에서 **리포지토리 초기화** 아이콘을 클릭합니다. 그런 다음, 뒤 이은 대화 상자에서 **리포지토리 초기화** 단추를 클릭합니다.

    ![로컬 Git 리포지토리 초기화](../media-draft/4-vs-init-git-repo.png)

1. “첫 번째 커밋”을 메시지 상자에 입력한 후 확인 표시를 클릭하여 변경 내용을 커밋합니다.

    ![로컬 리포지토리에 변경 내용 커밋](../media-draft/4-vs-first-git-commit.png)

1. Visual Studio Code의 **보기** 메뉴에서 **통합 터미널**을 선택하여 통합 터미널을 엽니다. 그런 다음, 통합 터미널에서 다음 명령을 실행하여 두 위치의 BOT_NAME을 연습 1, 3단계에서 입력한 봇 이름으로 바꿉니다.

    ```
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. [SOURCE CONTROL] 패널 맨 위의 줄임표(세 개의 점)를 클릭하고 메뉴에서 **분기 게시**를 선택하여 로컬 리포지토리에서 Azure로 봇 코드를 푸시합니다. 자격 증명을 입력하라는 메시지가 표시되면 이 연습의 9단계에서 지정한 사용자 이름과 암호를 입력합니다.

봇이 Azure에 게시되었습니다. 그러나 봇을 테스트하기 전에 로컬에서 봇을 실행하고 Visual Studio Code에서 디버그하는 방법을 배워보겠습니다.