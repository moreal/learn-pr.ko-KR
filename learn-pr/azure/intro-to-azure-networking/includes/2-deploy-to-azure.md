대체로 첫 단계는 클라우드에 온-프레미스 구성을 다시 만드는 것입니다.

이 기본 구성은 네트워크가 어떻게 구성되고, Azure에서 어떻게 네트워크 트래픽이 들어오고 나가는지 알려줍니다.

## <a name="your-e-commerce-site-at-a-glance"></a>전자상거래 사이트 개요

대규모 엔터프라이즈 시스템은 종종 상호 연결되어 함께 작동하는 여러 응용 프로그램과 서비스로 구성됩니다. 인벤토리를 표시하고 고객의 주문 작성을 허용하는 프런트 엔드 웹 시스템을 사용하는 분들이 있을 것입니다. 이 시스템은 다양한 웹 서비스와 통신하여 인벤토리 데이터를 제공하고, 사용자 프로필을 관리하고, 신용 카드를 처리하고, 처리된 주문의 이행을 요청할 수 있습니다.

소프트웨어 설계자 및 디자이너는 복잡한 시스템을 보다 쉽게 디자인, 빌드, 관리 및 유지 관리할 수 있도록 여러 가지 전략과 패턴을 사용합니다. 그 중 몇 가지를 살펴볼 것이며, 첫 번째는 _느슨하게 결합된 아키텍처_입니다.

#### <a name="benefits-of-loosely-coupled-architectures"></a>느슨하게 결합된 아키텍처의 이점

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yHrc]

### <a name="using-an-n-tier-architecture"></a>N 계층 아키텍처 사용

느슨하게 결합된 시스템을 구축하는 데 사용할 수 있는 아키텍처 패턴은 _n 계층_입니다.

[n 계층 아키텍처](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier)는 응용 프로그램을 2개 이상의 논리 계층으로 나눕니다. 아키텍처 측면에서 상위 계층은 하위 계층에서 서비스에 액세스할 수 있지만, 하위 계층에서 상위 계층에 액세스해서는 안 됩니다.

계층은 문제를 구분하는 데 도움이 되며, 재사용이 가능하도록 이상적으로 설계되었습니다. 계층화된 아키텍처를 사용하면 유지 관리도 간소화됩니다. 계층을 개별적으로 업데이트하고나 바꿀 수 있으며, 필요할 경우 새로운 계층을 삽입할 수 있습니다.

_3계층_은 3개의 계층이 있는 N 계층 응용 프로그램을 말합니다. 전자상거래 웹 응용 프로그램은 이러한 3계층 아키텍처를 따릅니다.

* **웹 계층**은 브라우저를 통해 사용자에게 웹 인터페이스를 제공합니다.
* **응용 프로그램 계층**은 비즈니스 논리를 실행합니다.
* **데이터 계층**에는 제품 정보 및 고객 주문을 저장하는 데이터베이스 및 기타 저장소가 포함됩니다.

다음 일러스트레이션은 사용자에서 데이터 계층으로 이동하는 요청 흐름을 보여줍니다.

![각 계층이 전용 가상 머신에 호스트되는 3계층 아키텍처를 보여주는 일러스트레이션.](../media/2-three-tier.png)

사용자가 단추를 클릭하여 주문을 접수하면 사용자의 주소 및 결제 정보와 함께 웹 계층으로 요청이 전송됩니다. 웹 계층은 응용 프로그램 계층에 이 정보를 전달하고, 응용 프로그램 계층은 결제 정보의 유효성을 검사하고 인벤토리를 확인합니다. 그러면 응용 프로그램 계층에서 나중에 주문을 처리할 때 선택할 주문을 데이터 계층에 저장할 수 있습니다.

## <a name="your-e-commerce-site-running-on-azure"></a>Azure에서 실행 중인 전자상거래 사이트

Azure는 사용자가 구성, 사용자 지정 및 관리하는 가상 머신에 코드를 호스트하는 완전히 미리 구성된 환경에서 웹 응용 프로그램을 호스트하는 여러 가지 방법을 제공합니다.

가상 머신에서 전자상거래 사이트를 실행하려는 경우를 가정해 보겠습니다. Azure에서 실행 중인 테스트 환경의 모습은 다음과 같습니다. 다음 일러스트레이션은 인바운드 요청을 제한하도록 보안 기능이 설정된 가상 머신에서 실행되는 3계층 아키텍처를 보여줍니다. 

![각 계층이 별도의 가상 머신에서 실행되는 3계층 아키텍처를 보여주는 일러스트레이션. 각 가상 머신은 IP 주소가 레이블로 표시되고 해당 가상 네트워크 내부에 있습니다. 각 가상 네트워크에는 열린 포트를 나열하는 네트워크 보안 그룹이 있습니다.](../media/2-test-deployment.png)

자세히 분석해 보겠습니다.

:::row:::
  :::column:::
    ![Azure 지역을 나타내는 지구 상의 고정된 위치](../media/2-azure-region.png)
  :::column-end:::
    :::column span="3"::: **Azure 지역이란?**

_Azure 지역_이란 특정 지리적 위치 내에 있는 Azure 데이터 센터입니다. 미국 동부, 미국 서부, 북유럽이 그 예입니다. 이 예에서는 응용 프로그램이 미국 동부 지역에서 실행되고 있습니다.

  :::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![가상 네트워크에서 실행 중인 두 대의 가상 머신](../media/2-azure-vnet.png)
  :::column-end:::
    :::column span="3"::: **가상 네트워크란?**

_가상 네트워크_란 Azure에서 논리적으로 격리된 네트워크입니다. Hyper-V, VMware 또는 기타 공용 클라우드에서 네트워크를 설정해보신 분들은 Azure 가상 네트워크에 익숙할 것입니다.

웹, 응용 프로그램 및 데이터 계층에는 각각 단일 VM이 있습니다. 각 VM은 가상 네트워크에 속해 있습니다.

사용자는 웹 계층과 직접 상호 작용하므로 VM에는 공용 IP 주소가 있습니다. 사용자는 응용 프로그램 또는 데이터 계층과 상호 작용하지 않습니다. 따라서 이러한 VM에는 각각 비공개 IP 주소가 있습니다.

Azure 데이터 센터는 물리적 하드웨어를 자동으로 관리합니다. 사용자는 소프트웨어를 통해 가상 네트워크를 구성하여 가상 네트워크를 자신의 네트워크처럼 취급할 수 있습니다. 예를 들어 가상 네트워크를 여러 개의 서브넷으로 나누어 네트워크의 IP 주소 할당 방식을 더 효율적으로 제어할 수 있습니다. 또한 공용 인터넷 또는 사설 IP 주소 공간의 다른 네트워크 등 가상 네트워크가 연결할 수 있는 다른 네트워크를 선택할 수도 있습니다.

  :::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![네트워크 보안 그룹을 공유하는 두 대의 가상 머신](../media/2-azure-nsg.png)
  :::column-end:::
    :::column span="3"::: **네트워크 보안 그룹이란?**

_네트워크 보안 그룹_, 즉 NSG는 Azure 리소스에 대한 인바운드 네트워크 트래픽을 허용하거나 거부합니다. 네트워크 보안 그룹은 네트워크의 클라우드 수준 방화벽으로 간주하세요.

예를 들어 웹 계층의 VM은 포트 22(SSH) 및 80(HTTP)의 인바운드 트래픽을 허용합니다. 이 VM의 네트워크 보안 그룹은 이 포트를 통해 들어오는 모든 소스의 인바운드 트래픽을 허용합니다. 신뢰할 수 있는 IP 주소 등 알려진 소스에서 들어오는 트래픽만 허용하도록 네트워크 보안 그룹을 구성할 수 있습니다.

> [!NOTE]
> 포트 22를 사용하면 SSH를 통해 Linux 시스템에 직접 연결할 수 있습니다. 여기에서는 설명을 위해 포트 22가 열려 있습니다. 실제로는 보안 강화를 위해 가상 네트워크에 대한 VPN 액세스를 구성할 수 있습니다.

  :::column-end:::
:::row-end:::

## <a name="summary"></a>요약

귀하의 3계층 응용 프로그램은 현재 미국 동부 지역의 Azure에서 실행 중입니다. _지역_이란 특정 지리적 위치 내에 있는 Azure 데이터 센터입니다.

각 계층은 하위 계층에서만 서비스에 액세스할 수 있습니다. 웹 계층에서 실행 중인 VM은 인터넷에서 트래픽을 수신하므로 공용 IP 주소가 있습니다. 하위 계층의 VM은 응용 프로그램과 데이터 계층이며, 인터넷을 통해 직접 통신하지 않으므로 개인 IP 주소가 있습니다.

_가상 네트워크_를 사용하면 관련 시스템을 그룹화하고 격리할 수 있습니다. 가상 네트워크를 통해 전달될 수 있는 트래픽을 제어하려면 _네트워크 보안 그룹_을 정의합니다.

여기서 살펴본 구성이 좋은 출발점입니다. 하지만 클라우드의 프로덕션 환경으로 전자상거래 사이트를 배포하면 온-프레미스 배포와 동일한 문제가 발생할 수 있습니다.
