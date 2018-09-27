Azure 개발을 위해 Visual Studio Code를 사용하려면 Visual Studio Code를 로컬에 설치하고 하나 이상의 Azure 확장을 설치해야 합니다. 이 연습에서는 **Azure App Service** 확장을 추가합니다.

## <a name="install-visual-studio-code"></a>Visual Studio Code 설치

::: zone pivot="windows"

### <a name="windows"></a>Windows

1. [Windows용 Visual Studio Code 설치 관리자를 다운로드](https://code.visualstudio.com/)합니다.

1. 설치 관리자를 실행합니다.

1. Windows 키를 누르거나 작업 표시줄에서 Windows 아이콘을 클릭하고, "Visual Studio Code"를 입력하고, **Visual Studio Code** 결과를 클릭하여 Visual Studio Code를 엽니다.

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a>macOS

1. [macOS용 Visual Studio Code를 다운로드](https://code.visualstudio.com/)합니다.

1. 다운로드한 보관 파일을 두 번 클릭하여 콘텐츠를 확장합니다.

1. Visual Studio Code.app을 응용 프로그램 폴더로 끕니다.

1. 앱 섹션 아이콘을 클릭하거나 Spotlight에서 Visual Studio Code를 검색하여 Visual Studio Code를 엽니다.

::: zone-end

::: zone pivot="linux"

### <a name="linux"></a>Linux 

#### <a name="debian-and-ubuntu"></a>Debian 및 Ubuntu

1. 그래픽 소프트웨어 센터(사용 가능한 경우) 또는 명령줄(`<file>`을 다운로드한 .deb 파일 이름으로 바꿈)을 통해 [.deb 패키지(64비트)](https://go.microsoft.com/fwlink/?LinkID=760868)를 다운로드하여 설치합니다.

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

#### <a name="rhel-fedora-and-centos"></a>RHEL, Fedora 및 CentOS

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

#### <a name="opensuse-and-sle"></a>openSUSE 및 SLE

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
> 다양한 Linux 배포에 Visual Studio Code를 설치하거나 업데이트하는 방법에 대한 자세한 내용은 [Linux에서 Visual Studio Code 실행 설명서](https://code.visualstudio.com/docs/setup/linux)를 참조하세요.

::: zone-end

## <a name="install-azure-app-service-extension"></a>Azure App Service 확장 설치

1. 아직 설치하지 않은 경우 Visual Studio Code를 엽니다.

1. 확장 브라우저를 엽니다. 왼쪽 메뉴를 통해 액세스할 수 있습니다.

1. **Azure App Service**를 검색합니다.

1. **Azure App Service** 결과를 선택하고 **설치**를 클릭합니다.

    다음 스크린샷은 Visual Studio Code 확장 검색 결과에서 Azure App Service 확장이 선택되어 있는 것을 보여 줍니다.

    ![검색 결과에 Azure App Service 확장이 강조 표시된 확장 탭을 보여 주는 Visual Studio Code의 스크린샷입니다.](../media/3-install-azure-extension.png)

이렇게 하면 확장이 설치됩니다. Azure 구독에 연결하고 Azure App Service에 웹, 모바일 또는 API 앱을 배포할 준비가 되었습니다.
