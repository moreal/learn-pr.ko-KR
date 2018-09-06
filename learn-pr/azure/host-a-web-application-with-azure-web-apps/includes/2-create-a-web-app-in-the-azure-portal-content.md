여기서는 Azure Portal을 사용하여 Azure 웹앱을 만드는 방법을 알아봅니다.

## <a name="why-use-the-azure-portal"></a>Azure Portal을 사용하는 이유는 무엇인가요?

웹 응용 프로그램을 호스트하는 첫 번째 단계는 Azure 구독 내부에 **웹앱**을 만드는 것입니다.

Azure 웹앱을 만들 수 있는 여러 가지 방법이 있습니다. Azure Portal, Azure CLI, 스크립트 또는 IDE를 사용할 수 있습니다.

여기서는 좋은 학습 도구가 될 수 있는 그래픽 환경인 포털을 사용합니다. 포털을 통해 사용 가능한 기능을 검색하고, 다른 리소스를 추가하고, 기존 리소스를 사용자 지정할 수 있습니다.

## <a name="what-is-web-apps-in-azure"></a>Azure의 Web Apps란?

Web Apps는 Azure 환경 내에서 완전히 관리되는 컴퓨팅 플랫폼으로, 웹앱, REST API 및 모바일 백 엔드를 호스트하는 데 최적화되어 있습니다.

Microsoft Azure에서 제공하는 이 PaaS(Platform as a Service)를 사용하면 Azure가 응용 프로그램을 실행하고 크기를 조정하기 위한 인프라를 관리하는 동안 빌드 측면에 초점을 맞출 수 있습니다.

## <a name="how-to-create-an-azure-web-app"></a>Azure 웹앱을 만드는 방법

자신만의 앱을 호스트해야 하면 Azure Portal을 방문하여 **웹앱** 형식의 새 **리소스**를 만듭니다. Azure Portal에서 이 리소스를 만들면 실제로는 ASP.NET Core, Node.js, PHP 등인지와 관계없이 Azure에서 지원되는 웹 기반 응용 프로그램을 호스트하는 데 사용할 수 있는 청사진 또는 **컨테이너**를 만드는 것입니다. 아래 그림은 앱에서 사용하는 프레임워크/언어를 구성하기가 얼마나 쉬운지를 보여 줍니다.

![웹앱 설정](../media-draft/2-web-app-settings.png)

Azure Portal은 새 웹앱을 만들기 위한 템플릿을 제공합니다. 이 템플릿에는 다음 필드가 필요합니다.

- **앱 이름**: 웹앱의 이름입니다.
- **구독**: 유효한 활성 구독입니다.
- **리소스 그룹**: 유효한 리소스 그룹입니다. 아래 섹션에서는 리소스 그룹의 개념을 자세히 설명합니다.
- **OS**: 운영 체제입니다. 옵션은 Windows, Linux 및 Docker 컨테이너입니다. Windows에서는 다양한 기술을 기반으로 한 모든 유형의 응용 프로그램을 호스트할 수 있습니다. Linux 호스팅의 경우도 마찬가지입니다. 단, Linux를 통해서는 .NET Core 프레임워크를 사용하는 ASP.NET Core 웹앱만 만들 수 있습니다. .NET Framework를 사용하는 다른 ASP.NET 앱의 경우 Windows OS를 통해 호스트해야 합니다. 마지막 옵션은 Docker 컨테이너로, 이 경우 Azure에서 호스트 및 유지 관리되는 컨테이너를 통해 로컬 Docker 컨테이너를 직접 배포할 수 있습니다. 따라서 기본적으로 오픈 소스 기술(PHP, ASP.NET Core 등)을 사용하는 웹앱은 Linux OS에서 호스트될 수 있습니다.
- **App Service 계획/위치**: 유효한 Azure App Service 계획입니다. 아래 섹션에서는 App Service 계획의 개념을 자세히 설명합니다.
- **Applications Insights**: Azure Application Insights 옵션을 켜고, 앱 성능을 모니터링하는 데 도움이 되도록 Azure Portal에서 제공하는 모니터링 및 메트릭 도구를 이용할 수 있습니다.

Azure Portal에서 제공되는 다양한 도구를 사용하여 효과적으로 웹앱을 관리, 모니터링 및 제어할 수 있습니다.

### <a name="deployment-slots"></a>배포 슬롯

Azure Portal을 사용하여 웹앱에 **배포 슬롯**을 쉽게 추가할 수 있습니다. 예를 들어 Azure에서 테스트하기 위해 코드를 푸시할 수 있는 **스테이징** 배포 슬롯을 만들 수 있습니다. 코드에 만족할 경우 스테이징 배포 슬롯을 프로덕션 슬롯과 쉽게 **교환**할 수 있습니다. Azure Portal에서 마우스를 몇 번 클릭하면 이 작업을 모두 수행할 수 있습니다.

![배포 슬롯](../media-draft/2-deployment-slots.png)

### <a name="continuous-integrationdeployment-support"></a>연속 통합/지속적인 배포 지원

Azure Portal은 Azure에서 완전히 관리하는 Visual Studio Team Services, GitHub, Bitbucket, Dropbox, OneDrive 또는 로컬 Git 리포지토리에 대한 연속 통합 및 지속적인 배포를 기본적으로 제공합니다. 웹앱을 위의 원본과 연결하면 Azure가 코드 및 코드의 이후 변경 내용을 웹앱에 자동 동기화하여 나머지 작업을 수행합니다. 또한 Visual Studio Team Services를 통해 고유한 빌드 및 릴리스 프로세스를 정의하여 원본 코드를 컴파일하고, 테스트를 실행하고, 릴리스를 빌드하고, 마지막으로 코드를 커밋할 때마다 릴리스를 웹앱에 푸시할 수 있습니다. 모든 작업은 개입 없이 암시적으로 수행됩니다.

![연속 통합 구성](../media-draft/2-continuous-integration.PNG)

### <a name="integrated-visual-studio-publishing-and-ftp-publishing"></a>통합 Visual Studio 게시 및 FTP 게시

웹앱에 대한 연속 통합/지속적인 배포를 설정할 수 있을 뿐 아니라 언제든지 Visual Studio와 긴밀하게 통합하여 웹 배포 기술을 통해 웹앱을 Azure에 게시할 수 있습니다. 또한 Azure는 FTP를 지원합니다. 그러나 모든 것을 Azure에 게시하는 것이 아니라 변경되거나 추가된 파일만 선택하는 웹 배포의 일부 기능이 없기 때문에 FTP를 사용하지 않는 것이 좋습니다.

### <a name="built-in-auto-scale-support-automatically-scale-updown-based-on-real-world-load"></a>기본 제공 자동 크기 조정 지원(실제 부하에 따라 자동으로 강화/축소)

강화/축소 또는 규모 확장 기능이 웹앱에 포함됩니다. 웹앱 사용량에 따라 웹앱을 호스트 중인 기본 머신의 리소스를 늘리거나 줄여 앱을 강화/축소할 수 있습니다. 리소스는 사용 가능한 코어 수 또는 RAM 크기일 수 있습니다.

이와 달리 규모 확장은 웹앱을 실행 중인 머신 인스턴스 수를 늘리는 기능입니다.

## <a name="what-is-a-resource-group"></a>리소스 그룹이란?

리소스 그룹은 제공된 응용 프로그램 치 환경에 대한 가상 머신, 웹앱, 데이터베이스 등의 상호 종속적 리소스 및 서비스를 그룹화하는 방법입니다. 리소스 그룹은 앱의 요소를 그룹화하는 위치인 **폴더**로 생각하세요.

리소스 그룹을 사용하여 리소스를 쉽게 관리하고 삭제할 수 있습니다. 또한 응용 프로그램을 실행하는 데 필요하거나 클라이언트에서 사용되는 리소스 컬렉션에 대한 청구를 모니터링, 액세스 제어, 프로비전 및 관리하는 방법을 제공합니다.

## <a name="what-is-an-app-service-plan"></a>App Service 계획의 정의

App Service 계획은 App Service 앱을 배포할 수 있는 실제 리소스 및 용량 집합입니다.

Azure Portal은 새 App Service 계획을 만들기 위한 템플릿을 제공합니다. 이 템플릿에는 다음 기본 정보가 필요합니다.

- 지역(미국 서부, 미국 중부, 북유럽 등)
- 확장 개수(1, 2, 3개 인스턴스 등)
- 인스턴스 크기(소, 중, 대)
- Stock Keeping Unit - SKU(무료, 공유, 기본, 표준, 프리미엄 및 가장 최근 프리미엄 v2)

Azure App Service의 Web Apps, Mobile Apps 및 API Apps 기능과 Azure Functions는 모두 App Service 계획에서 실행됩니다. 개수에 제한 없이 응용 프로그램을 App Service 계획에 배포할 수 있지만, 사용하는 개수는 배포된 응용 프로그램 유형 및 CPU 사용률에 필요한 리소스에 따라 크기 달라집니다.

응용 프로그램을 또 다른 App Service 계획으로 확장하거나 이동해야 하는지 결정하는 데 도움이 되도록 Azure Portal에서 App Service 계획을 사용하여 CPU 및 메모리 사용률을 시각화할 수 있습니다.
