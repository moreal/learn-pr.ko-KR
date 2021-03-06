모든 시스템, 아키텍처 및 응용 프로그램은 보안을 고려하여 설계해야 합니다. 너무 많은 위험에 노출됩니다. 예를 들어 서비스 거부 공격으로 인해 비즈니스를 수행할 수 없습니다. 웹 사이트가 손상되면 회사의 명성이 훼손될 수 있습니다. 데이터 위반은 힘들게 얻은 신뢰를 손상시킬 수 있으므로 최악의 상황입니다. &mdash; 이 결과 상당한 개인 및 재무 위험이 초래됩니다. 관리자, 개발자 및 IT 관리자는 모두 시스템의 보안을 보장하기 위해 노력해야 합니다.

사용자가 Contoso Shipping이라는 회사에서 일하며 지방에 드론 배달 개발을 주도하고 있다고 가정하겠습니다. 반면 도시에서는 트럭 운전사가 모바일 앱을 활용하여 배달합니다. 여러 물리적 서버를 자체 데이터 센터에서 Azure Virtual Machines로 이동할 뿐만 아니라 효율성을 극대화하기 위해 많은 해당 인프라를 클라우드로 전환하는 과정에 있습니다. 사용자 팀은 온-프레미스에 남아있는 일부 서버가 결합된 하이브리드 솔루션을 만들 계획이므로 새 가상 머신과 기존 네트워크 간의 안전한 고품질 연결이 필요합니다.

![온-프레미스 네트워크에서 클라우드를 보호하는 개념](../media/1-heading.png)

또한 Contoso Shipping에는 운영과 관련된 일부 네트워크 외부 장치가 있습니다. 배달원이 모바일 앱을 사용하여 배송물 수령을 위한 경로 지도를 가져오고 서명을 기록하는 반면 사용자는 Azure Event Hubs에 데이터를 전송하는 드론에서 네트워크 사용 센서를 사용하고 있습니다. 이러한 장치와 앱은 데이터를 보내고 받기 전에 안전하게 인증되어야 합니다.

데이터 보안을 유지하려면 어떻게 하나요?

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음 방법을 알아봅니다.

- Azure와 보안 책임을 공유하는 방법
- ID 관리에서 네트워크 외부에도 보호를 제공하는 방법
- Azure에 기본 제공된 암호화 기능으로 데이터를 보호하는 방법
- 네트워크 및 가상 네트워크를 보호하려면

## <a name="prerequisites"></a>필수 구성 요소  

없음