Jim은 다양한 플랫폼에서 운영되는 여러 웹 사이트 및 데이터베이스 서버가 포함된 회사 웹 인프라에서 실행 중인 Azure Virtual Machines 집합을 관리합니다. 

Azure Portal은 쉽게 사용할 수 있지만, Jim은 여러 블레이드를 탐색하는 경우 일부 태스크에 시간이 더 걸린다는 것을 알게 되었습니다. 

대안을 모색하는 동안 Jim은 Azure CLI 도구를 발견합니다.

Azure CLI로 작업하면서 Jim은 서버의 상태를 확인하고 새 구성을 배포하고 포트를 열거나 가상 머신에 연결하여 설정을 변경하기 위한 스크립트를 작성할 수 있습니다.

Jim과 마찬가지로 여러분도 클라우드 환경에서 태스크를 자동화하는 데 도움이 되는 도구를 찾고 있을 수 있습니다. Azure CLI를 사용하여 Azure에 호스팅되는 가상 머신을 만들고 관리하는 방법을 보여 드리겠습니다. 

## <a name="azure-cli"></a>Azure CLI

Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다. macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.

> [!IMPORTANT]
> Azure CLI 도구는 현재 Azure CLI 1.0 및 Azure CLI 2.0의 두 가지 버전이 있습니다. 1.0용으로 작성된 레거시 스크립트를 실행하는 경우가 아니라면 최신 버전인 Azure CLI 2.0을 사용하는 것이 좋습니다. Azure CLI 1.0은 `azure` 명령으로 시작되고 Azure CLI 2.0은 `az` 명령으로 시작됩니다. 

Azure CLI를 사용하면 명령줄이나 스크립트를 통해 가상 머신 및 디스크와 같은 Azure 리소스를 관리할 수 있습니다. 이제 시작하여 무엇을 할 수 있는지 살펴보겠습니다.

## <a name="learning-objectives"></a>학습 목표
> [!div class="checklist"]
> * CLI로 Azure 가상 머신 만들기
> * CLI로 VM 크기 조정
> * 명령줄에서 VM 관리 및 쿼리
> * VM에 소프트웨어 설치