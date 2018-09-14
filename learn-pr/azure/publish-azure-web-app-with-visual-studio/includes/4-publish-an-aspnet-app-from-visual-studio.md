사이트를 만들었으며 이를 Azure에 배포하려고 합니다. 이제 요구 사항을 가장 잘 지원할 수 있는 Azure 서비스를 고려해야 합니다. App Service는 응용 프로그램에 대해 확장성이 뛰어나고 자체 패치가 가능한 웹 호스팅 서비스를 제공합니다.

여기서는 Visual Studio를 사용하여 ASP.NET Core 웹 응용 프로그램을 Azure App Service 계획에 게시하는 방법을 살펴봅니다.

## <a name="what-is-web-apps"></a>Web Apps란 무엇인가요?

Azure App Service는 웹 응용 프로그램, REST API 및 모바일 백 엔드를 호스트하는 서비스입니다. App Service는 .NET, .NET Core, Java, Ruby, Node.js, PHP 및 Python과 같은 다양한 언어로 작성된 코드를 지원합니다. App Service는 특히 호스팅 인프라에 많은 제어가 필요하지 않은 경우 대부분 웹 사이트에 이상적입니다.

## <a name="what-is-the-app-service-plan"></a>App Service 계획이란 무엇인가요?

App Service 계획은 앱이 이용할 계산 리소스, 이러한 리소스가 있는 위치, 계획에 사용할 수 있는 추가 리소스의 수 및 사용 중인 서비스 계획 유형을 정의합니다. 이러한 계산 리소스는 기존 웹 호스팅의 서버 팜과 유사합니다. 동일한 App Service 계획에서 실행되도록 하나 이상의 앱을 구성할 수 있습니다.

앱을 배포할 때 App Service 계획을 만들거나 기존 계획에 앱을 계속 추가할 수 있습니다.  그러나 동일한 App Service 계획의 앱만이 동일한 계산 리소스를 공유합니다. 새 앱에 필요한 리소스가 있는지 확인하려면 기존 App Service 계획의 용량과 새 앱의 예상 부하를 이해해야 합니다. App Service 계획을 오버로드하면 새 앱과 기존 앱의 가동 중지 시간이 발생할 수 있습니다.

Azure Portal에서 PowerShell 또는 Azure CLI를 사용하여 App Service 계획을 미리 정의할 수도 있고, Visual Studio에서 응용 프로그램을 게시할 때 App Service 계획을 설정할 수도 있습니다.

각 App Service 계획은 다음을 정의합니다.

- 지역(미국 서부, 미국 동부 등)
- VM 인스턴스 수
- VM 인스턴스 크기(소, 중, 대)
- 가격 책정 계층(무료, 공유, 기본, 표준, 프리미엄, Premium V2, 격리, 사용)

## <a name="specify-the-region"></a>지역 지정

App Service 계획을 생성할 때 해당 계획을 호스트할 지역 또는 위치를 정의해야 합니다. 일반적으로 예상 고객과 지리적으로 가까운 지역을 선택하게 됩니다.

## <a name="what-are-the-pricing-and-reliability-levels"></a>가격 및 안정성 수준은 어떤가요?

Azure App Service에 앱을 배포할 때의 핵심 요소는 올바른 서비스 계획을 선택하는 것입니다. 언제든지 App Service 계획을 확장하고 축소할 수 있습니다. 처음에 더 낮은 가격 책정 계층을 선택하고 더 많은 App Service 기능이 필요하면 나중에 확장할 수 있습니다.

가격 책정 계층의 몇 가지 범주가 있습니다.

**공유 계산**: **체험** 및 **공유**라는 두 개의 기본 계층은 다른 고객의 앱을 비롯한 다른 App Service 앱과 동일한 Azure VM에서 앱을 실행합니다. 이러한 계층은 CPU 할당량을 공유 리소스에서 실행되는 각 앱에 할당하고 리소스는 확장할 수 없습니다.

체험 및 공유 플랜은 트래픽 수요가 매우 제한적인 소규모 개인 프로젝트에 가장 적합하며, 24시간마다 165MB의 아웃바운드 데이터 제한이 설정되어 있습니다.

**전용 계산**: **기본, 표준, 프리미엄 및 Premium V2** 계층은 전용 Azure VM에서 앱을 실행합니다. 동일한 App Service 계획의 앱만이 동일한 계산 리소스를 공유합니다. 계층이 높을수록 확장을 위해 더 많은 VM 인스턴스가 제공됩니다.

표준 서비스 계획은 상업용 응용 프로그램을 고객에게 게시하는 라이브 프로덕션 워크로드에 가장 적합합니다.
프리미엄 서비스 계획은 전용(격리된) 계획의 추가 비용을 원하지 않는 대용량 웹앱을 지원합니다.

**격리**: 이 계층은 전용 Azure Virtual Networks에서 전용 Azure VM을 실행합니다. 그러면 계산 격리보다 우선하여 네트워크 격리를 앱에 제공합니다. 최대 스케일 아웃 기능을 제공합니다. 가장 높은 수준의 보안 및 성능에 대한 특정 요구 사항이 있는 경우에만 격리된 서비스 계획을 선택하는 것이 좋습니다.

다음의 경우 새 App Service 계획으로 앱을 격리합니다.

- 앱이 리소스를 많이 사용합니다.
- 기존 계획에서 다른 앱과 독립적으로 앱을 확장하려고 합니다.
- 앱에 다른 지역의 리소스가 필요합니다.

## <a name="specify-the-resource-group"></a>리소스 그룹 지정

대부분의 Azure 리소스와 마찬가지로 사용할 리소스 그룹을 지정해야 합니다. 기존 리소스 그룹을 사용하거나 Visual Studio에서 직접 그룹을 만들 수 있습니다. 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정과 같은 Azure 리소스가 배포되고 관리되는 논리적 컨테이너입니다. 이는 연관된 리소스를 함께 유지하는 데 유용한 메커니즘입니다.

## <a name="deploy-your-web-app-from-visual-studio"></a>Visual Studio에서 웹앱 배포

Visual Studio에서 Azure에 앱을 게시하는 짧은 프로세스입니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-the-project"></a>프로젝트 선택

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.

1. **게시 > Azure에 게시**를 선택합니다.

### <a name="configure-the-app-service-plan-in-windows"></a>Windows에서 App Service 계획 구성

1. App Service 계획 구성

    - 호스팅: 이 탭에서 App Service 계획을 구성합니다. 여기서 앱을 호스트하는 웹 서버의 위치, 크기 및 기능을 지정합니다. 기존 호스팅 플랜을 선택하거나 새로 만들 수 있습니다. Windows는 전역적으로 고유한 이름을 자동으로 생성하는데, 이 이름은 설정 중에 변경할 수 있습니다.
    - 서비스: 여기서 사이트에 대한 SQL 데이터베이스를 구성할 수 있습니다.

        > [!NOTE]
        > Visual Studio에서 Azure의 SQL 데이터베이스를 연결하고 관리할 수는 있지만, 이는 모듈의 범위를 벗어나는 것입니다.

1. **만들기**를 클릭하여 앱을 배포합니다. 이 작업이 완료되면, Visual Studio에서는 사이트가 호스트되는 웹 페이지를 시작합니다.

### <a name="configure-the-app-service-plan-for-mac"></a>Mac용 App Service 계획 구성

1. Azure에 설정된 기존 App Service 계획이 있는 경우 이를 선택하거나 새로 만들 수 있습니다.

1. 이 탭에서 App Service 계획을 구성합니다. 여기서 앱을 호스트하는 웹 서버의 위치, 크기 및 기능을 지정합니다. 기존 호스팅 플랜을 선택하거나 새로 만들 수 있습니다. 웹 사이트의 이름과 모든 리소스는 전역적으로 고유해야 합니다.

1. **만들기**를 클릭하여 앱을 배포합니다. 이 작업이 완료되면, Visual Studio에서는 사이트가 호스트되는 웹 페이지를 시작합니다.

## <a name="summary"></a>요약

ASP.NET Core 웹 응용 프로그램 및 Azure App Service는 ASP.NET 웹앱을 호스트하기 위한 유연하고 확장 가능한 솔루션을 제공합니다. 모든 Azure 서비스가 그렇듯이, 리소스 그룹을 제공하고 요구에 가장 잘 맞는 가격 책정 계층을 선택해야 합니다.
