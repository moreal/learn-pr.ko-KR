새 사이트를 준비하는 첫 번째 단계는 개발 환경 준비입니다. ASP.NET 웹 응용 프로그램을 만들고 배포하려면 로컬 머신에 필요한 도구가 설치되어 있어야 합니다. 여기에서는 필요한 도구와 도구를 설치하는 방법에 대해 설명합니다.

## <a name="prepare-your-development-environment"></a>개발 환경 준비

Visual Studio 2017에는 만들기, 게시 및 Azure에 웹 사이트를 배포 해야 하는 두 가지 워크 로드에 있습니다. 이러한 워크로드는 ASP.NET 사이트에 대한 모든 템플릿을 포함하고 있으며 Azure에 사이트를 연결하고 배포하는 기능을 제공합니다.

다음 워크로드가 설치되어 있는지 확인해야 합니다.

- ASP.NET 및 웹 개발

Visual Studio 2017의 웹 개발 워크 로드는 ASP.NET 및 HTML 및 JavaScript와 같은 표준 기반 기술을 사용 하 여 웹 응용 프로그램 개발의 생산성을 극대화 하도록 설계 되었습니다.

- Azure 개발

Visual Studio 2017의 Azure 개발 워크로드는 최신 .NET용 Azure SDK와 Visual Studio용 도구를 설치합니다. 이러한 항목이 설치되면 클라우드 탐색기에서 리소스를 보고, Azure Resource Manager 도구를 사용하여 리소스를 만들고, Azure 웹 및 Cloud Services용 응용 프로그램을 빌드하고, Azure Data Lake 도구를 사용하여 빅 데이터 작업을 수행할 수 있습니다.

## <a name="how-to-install-the-required-workloads"></a>필수 워크로드를 설치하는 방법

Visual Studio 설치 관리자를 사용하여 Visual Studio의 일부로 설치된 구성 요소를 수정합니다.

- 설치 관리자를 시작하려면 Windows 시작 메뉴에서 **V**까지 아래로 스크롤한 후 **Visual Studio 설치 관리자**를 클릭합니다. 그러지 않고, 시작 메뉴가 열려 있는 동안 그냥 ```Visual Studio Installer```를 입력하여 설치 관리자 링크를 찾을 수도 있습니다. 그런 다음, **Enter** 키를 선택합니다.

- Visual Studio 설치 관리자 창이 나타납니다. **수정** 단추를 클릭합니다. 단추가 표시되지 않는 경우 **더 보기** 드롭다운 메뉴에서 **수정**을 선택할 수 있습니다.

    ![Visual Studio 수정](../media-draft/3-visual-studio-installer-modify.PNG)

- **워크로드** 탭의 **웹 및 클라우드** 섹션에서 **ASP.NET 및 웹 개발**과 **Azure 개발** 워크로드가 선택되어 있는지 확인합니다.   ![워크로드 설치](../media-draft/2-select-workloads.png)

그런 다음, 설치 관리자의 오른쪽 아래에 있는 **수정** 단추를 클릭합니다. Visual Studio 설치 관리자는 필요한 구성 요소를 다운로드하여 설치합니다. 이제 ASP.NET 웹앱을 만들어 Microsoft Azure에 업로드할 준비가 되었습니다.

> [!IMPORTANT]
> Mac용 Visual Studio에는 필요한 워크로드가 사전 설치되어 _있어야_ 합니다. 다시 설치해야 하는 경우 설치 관리자를 실행할 [Mac용 Visual Studio](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio-mac/?sku=communitymac&rel=15_)를 다운로드해야 합니다. 거기에서 추가할 워크로드를 선택할 수 있습니다.

## <a name="summary"></a>요약

**ASP.NET 및 웹 개발**과 **Azure 개발** 워크로드가 있는 Visual Studio 2017에서 ASP.NET 웹 사이트를 만들고 관리하며 게시할 수 있습니다.
