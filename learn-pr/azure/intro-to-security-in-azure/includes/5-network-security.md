공격 및 무단 액세스로부터 네트워크를 보호하는 것은 아키텍처의 중요한 부분입니다. 여기서는 네트워크 보안의 특징, 계층화된 접근 방식을 아키텍처에 통합하는 방법 및 Azure에서 네트워크 보안을 환경에 제공하는 방법을 살펴보겠습니다.

## <a name="a-layered-approach-to-network-security"></a>네트워크 보안에 대한 계층화된 접근 방식

이 모듈 전체에서 공통적으로 다루는 주제는 보안에 대한 계층화된 접근 방식의 중요성이며, 이 접근 방식은 네트워크 계층에서 아무런 차이가 없습니다. 네트워크 경계 보호에만 집중하거나 또는 네트워크 내부의 서비스 간 네트워크 보안에 집중하기에 충분하지 않습니다. 계층화된 접근 방식은 여러 보호 수준을 제공하므로 공격자가 한 계층을 돌파하더라도 추가 보호가 작동하므로 추가 공격이 제한됩니다.

Azure가 어떻게 네트워크 공간을 보호하는 계층화된 접근 방식을 위한 도구를 제공하는지 살펴보겠습니다.

:::row:::
  :::column:::
    ![안전한 인터넷을 나타내는 이미지](../media/5-internet-protection.png)
  :::column-end:::
    :::column span="3":::: **인터넷 보호**

네트워크 경계에서 시작하는 경우 인터넷 공격을 제안하고 제거하는 것이 집중해야 합니다. 먼저 인터넷에 연결되는 리소스를 평가하고 필요한 경우에만 인바운드 및 아웃바운드 통신을 허용하는 것이 좋습니다. 모든 종류의 인바운드 네트워크 트래픽을 허용하는 리소스를 식별하고, 리소스를 반드시 필요한 포트/프로토콜로 제한해야 합니다. 이 정보는 Azure Security Center에서 살펴보면 좋습니다. 네트워크 보안 그룹이 연결되지 않은 인터넷 연결 리소스와 방화벽의 보호를 받지 않는 리소스를 식별하기 때문입니다.

경계에서 인바운드 보호를 제공하려면 몇 가지 선택 사항이 있습니다.

* Azure Application Gateway는 일반적인 알려진 취약점으로부터 보호하는 웹 응용 프로그램 방화벽이 포함된 부하 분산 장치입니다.

* NVA(네트워크 가상 어플라이언스)는 HTTP가 아닌 서비스 또는 고급 구성에 적합한 옵션이며, 하드웨어 방화벽 어플라이언스와 비슷합니다.

인터넷에 노출된 리소스는 서비스 거부 공격을 받을 위험이 있습니다. 이러한 유형의 공격은 네트워크 리소스에 과부하를 걸어서 리소스가 느려지거나 응답할 수 없도록 수많은 요청을 전송합니다. 이러한 공격을 완화하기 위해 Azure DDoS 보호는 모든 Azure 서비스에 기본 보호를 제공하며, 리소스를 추가로 사용자 지정할 수 있도록 향상된 보호를 제공합니다. Azure DDoS 보호는 공격 트래픽을 차단하고 나머지 트래픽을 의도하는 대상으로 전달합니다. 공격이 탐지되면 몇 분 안에 Azure Monitor 메트릭을 통해 알림을 받습니다.

![DDoS](../media/ddos.png)

 :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![안전한 가상 네트워크를 나타내는 이미지](../media/5-vnet-security.png)
  :::column-end:::
    :::column span="3":::: **가상 네트워크 보안**

VNet(가상 네트워크) 내에서는 꼭 필요한 곳에서만 리소스 간 통신이 이루어지도록 제한해야 합니다.

가상 머신 간의 통신에서는 네트워크 보안 그룹을 통해 불필요한 통신을 제한하는 것이 중요합니다. 네트워크 인터페이스 및 서브넷과 허용되거나 거부되는 통신의 목록을 제공하며 완전히 사용자 지정할 수 있습니다.

서비스 엔드포인트에 대한 액세스를 제한하여 서비스에 대한 공용 인터넷 액세스를 완전히 제거할 수 있습니다. 서비스 엔드포인트를 사용하면 Azure 서비스 액세스가 가상 네트워크로 제한될 수 있습니다.
 :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![안전한 네트워크를 나타내는 이미지](../media/5-network-integration.png)
  :::column-end:::
    :::column span="3":::: **네트워크 통합**

온-프레미스 네트워크에서 통신을 제공하기 위해 또는 Azure의 서비스 간 통신을 향상하기 위해 기존 네트워크 인프라를 통합해야 하는 경우가 자주 있습니다. 이러한 통합을 처리하고 네트워크 보안을 향상할 수 있는 몇 가지 방법이 있습니다.

VPN(가상 사설망) 연결은 네트워크 간에 보안 통신 채널을 설정하는 일반적인 방법입니다. Azure Virtual Network와 온-프레미스 VPN 장치 간의 연결은 Azure에서 네트워크와 VNet 간의 보안 통신을 제공하는 좋은 방법입니다.

네트워크와 Azure 간에 전용 사설 연결을 제공하려면 Azure ExpressRoute를 사용합니다. ExpressRoute를 사용하면 연결 공급자가 지원하는 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장할 수 있습니다. ExpressRoute를 사용하면 Microsoft Azure, Office 365 및 Dynamics 365와 같은 Microsoft 클라우드 서비스에 대한 연결을 설정할 수 있습니다. 이렇게 하면 인터넷 대신 사설 회로를 통해 이 트래픽을 전송하여 온-프레미스 통신의 보안이 향상됩니다. 최종 사용자가 인터넷을 통해 이러한 서비스에 액세스하도록 허용할 필요가 없으며, 어플라이언스를 통해 이 트래픽을 전송하여 트래픽을 추가로 검사할 수 있습니다.
 :::column-end:::
:::row-end:::

## <a name="summary"></a>요약

네트워크 보안에 계층화된 접근 방식을 사용하면 네트워크 기반 공격에 의한 노출 위험을 줄일 수 있습니다. Azure는 인터넷 연결 리소스, 내부 리소스 및 온-프레미스 네트워크 간 통신을 보호하는 여러 가지 서비스와 기능을 제공합니다. 이러한 기능을 통해 Azure에서 안전한 솔루션을 만들 수 있습니다.