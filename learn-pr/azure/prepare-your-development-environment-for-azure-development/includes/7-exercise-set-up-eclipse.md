이 연습에서는 로컬 머신에 Eclipse를 설치한 후 Azure Toolkit를 설치하여 Azure 통합을 통해 Java 응용 프로그램을 개발할 준비를 합니다. 설치는 빠르고 간단합니다. 이 연습을 마치면 첫 번째 Java 응용 프로그램을 시작하는 데 필요한 모든 것이 설정되어 Azure의 기능과 서비스를 활용할 수 있습니다.

## <a name="install-eclipse-ide"></a>Eclipse IDE 설치

1. http://www.eclipse.org/downloads/packages/installer에서 운영 체제에 맞는 Eclipse 버전을 다운로드합니다.

1. 다운로드한 후 Eclipse 설치 관리자를 시작합니다.

    1. Windows에서 다운로드한 파일을 두 번 클릭합니다.

    1. macOS 및 Linux에서, 다운로드된 파일의 설치 관리자 압축을 풉니다. 압축이 풀리면 설치 관리자를 시작합니다.

        > [!NOTE]
        > Java Development Kit가 누락된 경우 설치 관리자에서 설치하라는 메시지를 표시합니다.

1. 설치할 패키지를 선택합니다. Java 개발자의 경우 Java 또는 Java EE Eclipse IDE 옵션을 선택합니다.

1. 머신에서 설치 대상을 선택합니다.

1. Eclipse를 시작하여 제대로 설치되었는지 유효성을 검사합니다.

## <a name="install-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트 설치

Azure Toolkit는 Windows, macOS 및 Linux에서 동일하게 설치됩니다.

1. Eclipse를 시작합니다.

1. **도움말** > **새 소프트웨어 설치...** 로 이동합니다.

    다음 스크린샷은 **새 소프트웨어 설치...** 항목의 메뉴 위치를 보여 줍니다.

    ![Eclipse 도움말 메뉴에 새 소프트웨어 설치 옵션이 강조되어 있는 스크린샷입니다.](../media/7-eclipse-install-new-software.png)

1. **사용 가능한 소프트웨어** 대화 상자가 열립니다. **작업:** 텍스트 상자에 `http://dl.microsoft.com/eclipse/`를 입력하고 Enter 키를 누릅니다.

1. 결과에서 **Azure Toolkit for Java** 옵션을 선택합니다. **Contact all update sites during install to find required software**(설치 중 모든 업데이트 사이트에 문의하여 필요한 소프트웨어 찾기) 옵션이 선택 취소되어 있지 않은 경우 선택 취소해야 합니다.

    다음 스크린샷은 위에 설명된 **사용 가능한 소프트웨어** 설치 구성을 보여 줍니다.

    ![Azure Toolkit for Java를 찾아 설치하는 데 필요한 구성이 강조되어 있는 상자가 포함된 Eclipse의 사용 가능한 소프트웨어 창 스크린샷입니다.](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. **다음**을 클릭합니다.

1. 메시지가 표시되면 사용권 계약을 검토 및 동의하고 **완료**를 클릭합니다.

1. Eclipse는 Azure Toolkit를 다운로드하여 설치합니다.

1. 필요한 경우 Eclipse를 다시 시작합니다.

1. Eclipse에서 **도구** > **Azure** 메뉴 옵션을 찾을 수 있는지 확인하여 Azure Toolkit 설치 유효성을 검사합니다.

## <a name="summary"></a>요약

이 단원에서는 Java용 Eclipse를 설치하고 Azure 서비스 및 제품과 통합하여 활용할 수 있도록 준비했습니다. 설치가 빠르고 간편한 Eclipse는 클라우드 서비스 통합을 통한 Java 개발 작업에 이상적입니다.
