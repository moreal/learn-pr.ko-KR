Visual Studio Code는 Azure용 응용 프로그램을 개발하는 데 널리 사용됩니다. 일부 IDE가 수 기가바이트를 사용하는 데 비해, 이 IDE(통합 개발 환경)는 경량이므로 몇 메가바이트 정도의 저장소 공간만 사용합니다. VS Code는 플랫폼 간; Windows, Linux 및 macOS에서 작동합니다.

## <a name="visual-studio-code"></a>Visual Studio Code

Visual Studio Code 또는 VS 코드만 간편 하면서도 강력한 편집기입니다. 대부분의 프로그래밍 언어, 실제로는 수백 개의 언어를 지원하며, 클라우드 서비스에 연결되도록 디자인되었습니다.

플랫폼 간 지원(Windows, Linux 및 macOS에서 실행)과 이식 가능한 민첩한 환경을 제공하는 데 초점을 맞춘 VS Code의 기본 설치에는 점점 더 증가하는 프로그래밍 언어 구문 강조 표시 적용 범위를 인식하는 편집기가 포함되어 있습니다. 그러나 컴파일러는 없습니다. 확장을 통해 또는 클라우드에서 수행 컴파일 것입니다.

Git SCM(소스 제어 관리자)을 사용하여 소스 제어에 대한 유용한 기본 제공 지원을 활용할 수 있습니다. 따라서 Git 프레임워크를 먼저 설치해야 합니다.

## <a name="extension-model"></a>확장 모델

VS Code의 가장 강력한 기능 중 하나는 확장 모델입니다. 타사 기능을를 VS 코드 IDE의 통합된 부분으로 실행 거의 모든 방법으로 상상할 수 있는 IDE의 기능을 확장할 수 있습니다.

확장은 JavaScript 또는 TypeScript로 작성 됩니다. Yeoman을 사용하여 확장을 스캐폴드할 수 있습니다. 이러한 모든 기능은 IntelliSense, 코드 탐색 및 전체 디버깅 환경을 지원합니다.

VS Code의 일반적인 세 가지 확장 범주는 확장, 언어 서버 및 디버거입니다. 후자의 두 경우 특수 한 기능을 제공 하도록 허용 하는 추가 프로토콜

Extension Marketplace에서 사용할 수 있는 확장에는 Python, Go, C++ 및 기타 언어에 대한 지원이 포함됩니다. 또한 확장에는 linter와 같은 코드 서식 도구, Azure와 같은 클라우드 연결용 도구, 새로운 테마, 코드 포맷터 및 코드 조각 라이브러리도 포함되어 있습니다. 이러한 모든 확장은 [VS Code Marketplace](https://marketplace.visualstudio.com/)에서 사용할 수 있습니다.

## <a name="azure-extensions"></a>Azure 확장

많은 확장이 Azure 기능과 제품을 대상으로 하며, 더 많은 확장이 계속 추가되고 있습니다. 이러한 확장은 Docker 지원, 구독 관리, Azure CLI용 도구, 데이터베이스 액세스, Azure Storage API 통합, 일반 Azure 확장과 같은 분야를 대상으로 합니다.

각 Azure 확장은 Azure 통합 지점을 통한 개발을 보다 쉽고 효율적으로 만들어주는 VS Code 기능 집합을 추가로 제공합니다.

## <a name="getting-vs-code-and-preparing-for-azure-development"></a>VS Code 가져오기 및 Azure 개발 준비

VS Code가 지원되는 세 가지 플랫폼은 Windows, macOS 및 Linux입니다. 이러한 세 플랫폼 모두 다운로드 가능한 파일에서 설치되지만 설치 시 다르게 동작합니다.

Windows를 실행 하는 VS Code를 가져오려면 Windows (32 비트 또는 64 비트) 버전에 대 한 파일을 다운로드 하 고 다른 Windows 응용 프로그램과 마찬가지로 설치.

macOS의 경우에도 파일을 다운로드하여 콘텐츠를 확장합니다. VS Code를 실행 패드 및 도크에 추가하는 것이 좋습니다.

Linux 조금 더 복잡 하 고 설치 지침을 사용 하는 분포에 따라 달라 집니다. Debian 및 Ubuntu를 다운로드 하 여 VS Code를 직접 설치 해야 합니다. RHEL, Fedora, CentOS, openSUSE 및 SLE에 대 한 Microsoft Yum 리포지토리를 제공 합니다. 다른 배포판의 경우에도 지원되는 커뮤니티 버전이 적을 수 있습니다.

모든 플랫폼에서 Azure 개발을 위해 VS Code를 준비하려면 Extension Marketplace를 사용하여 필요한 Azure 확장을 설치합니다. App Service를 사용하는 경우 App Service 확장을 사용합니다. Node.js를 사용하는 경우 Azure용 Node 팩이 필요합니다.

## <a name="summary"></a>요약

VS Code는 Azure용 응용 프로그램을 개발하고 만들기 위한 완벽한 파트너입니다. 앱의 효율성과 견고성을 향상하기 위한 포괄적인 확장과 연결된 경량의 플랫폼 간 IDE를 통해 VS Code는 Azure 개발에 이상적인 제품이 되었습니다.
