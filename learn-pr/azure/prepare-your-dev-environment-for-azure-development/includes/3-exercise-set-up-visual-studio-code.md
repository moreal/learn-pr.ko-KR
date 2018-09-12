이 단원에서는 Visual Studio Code 및 Azure App Service 확장을 설치하여 Microsoft Azure용으로 개발하고 웹앱을 배포할 준비를 합니다.

## <a name="exercise-steps"></a>연습 단계

먼저, 사용 중인 운영 체제를 식별하고 아래 해당 섹션의 단계에 따라 Visual Studio Code를 설치합니다.

### <a name="windows"></a>Windows

1. Windows용 Visual Studio Code 설치 관리자를 다운로드합니다.

1. 설치 관리자를 실행합니다. 시간이 오래 걸리지 않습니다.

1. 설치 폴더(64비트 머신의 경우 기본 경로는 C:\Program Files\Microsoft VS Code)로 이동하여 VS Code를 엽니다.

### <a name="macos"></a>macOS

1. macOS용 Visual Studio Code를 다운로드합니다.

1. 다운로드한 압축 파일을 두 번 클릭하여 콘텐츠를 확장합니다.

1. Visual Studio Code.app을 응용 프로그램 폴더로 끌어 실행 패드에서 사용할 수 있도록 합니다.

1. 아이콘을 마우스 오른쪽 단추로 클릭하고 [옵션] > [Keep in Dock]\(도크에 유지)를 선택하여 VS Code를 도크에 추가합니다.

### <a name="linux--debian-and-ubuntu"></a>Linux - Debian 및 Ubuntu

1. 그래픽 소프트웨어 센터(사용 가능한 경우) 또는 명령줄(다운로드한 .deb 파일 이름으로 `<file>`을 바꿈)을 통해 [.deb 패키지(64비트)](https://go.microsoft.com/fwlink/?LinkID=760868)를 다운로드하여 설치합니다.

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

### <a name="linux--rhel-fedora-and-centos"></a>Linux - RHEL, Fedora 및 CentOS

1. 다음 스크립트를 사용하여 키 및 리포지토리를 설치합니다.

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. 패키지 캐시를 업데이트하고 dnf(Fedora 22 이상)를 사용하여 패키지를 설치합니다.

    ```bash
    dnf check-update
    sudo dnf install code
    ```

### <a name="linux--opensuse-and-sle"></a>Linux - openSUSE 및 SLE

1. yum 리포지토리는 openSUSE 및 SLE 기반 시스템에 대해서도 작동합니다. 다음 스크립트는 키 및 리포지토리를 설치합니다.

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. 패키지 캐시를 업데이트하고 다음을 사용하여 패키지를 설치합니다.

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> 다양한 Linux 배포에서 VS Code를 설치하거나 업데이트하는 방법에 대한 자세한 내용은 [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux)(Linux에서 VS Code 실행) 설명서를 참조하세요.

## <a name="install-azure-app-service-extension"></a>Azure App Service 확장 설치

VS Code를 설치했으면 VS Code를 엽니다.

1. 확장 탭으로 이동합니다.

1. Azure App Service를 검색합니다.

1. [설치]를 클릭합니다.

    다음 스크린샷은 Visual Studio Code 확장 검색 결과에서 Azure App Service 확장이 선택되어 있는 것을 보여 줍니다.

    ![검색 결과에 Azure App Service 확장이 강조되어 있는 확장 탭을 보여 주는 VS Code 스크린샷입니다.](../media/3-install-azure-extension.png)

확장이 설치됩니다. Azure 구독에 연결하고 웹, 모바일 또는 API 앱용으로 개발하여 Azure App Service에 배포할 준비도 완료됩니다.
