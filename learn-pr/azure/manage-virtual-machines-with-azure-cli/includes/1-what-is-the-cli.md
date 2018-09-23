IT 부서에서 Azure Virtual Machines부터 관리형 웹 사이트까지 다양한 Azure 리소스 집합을 관리하는 것은 매우 흔한 풍경입니다.

Azure Portal은 일회성 작업에 간편하게 사용할 수 있지만, 여러 항목을 생성, 변경 또는 삭제해야 할 때 다양한 블레이드를 탐색하려면 시간이 걸립니다. 이러한 상황에서 명령줄이 진가를 발휘합니다. 빠르고 효율적으로 명령을 실행할 수 있으며, 스크립트를 사용하여 반복 작업을 실행할 수도 있습니다. Azure에서는 두 가지 명령줄 도구를 사용할 수 있는데, 그것은 바로 Azure PowerShell과 Azure CLI입니다.

둘 중 하나를 사용하여 클라우드 서버 상태를 확인하고, 새 구성을 배포하고, 방화벽에서 포트를 열고, 가상 머신에 연결하여 설정을 변경하는 스크립트를 작성할 수 있습니다. Windows 관리자는 Azure PowerShell을 선호하는 경향이 있고, 개발자와 Linux 관리자는 Azure CLI를 자주 사용합니다.

이 모듈에서는 Azure CLI를 사용하여 Azure에 호스팅되는 가상 머신을 만들고 관리하는 방법을 집중적으로 다루겠습니다. Azure CLI의 개요, 설치 방법, Azure 구독에서 사용하는 방법을 알아보려면 **CLI를 사용하여 Azure 서비스 제어** 교육 모듈을 확인하세요.

## <a name="what-is-the-azure-cli"></a>Azure CLI란?

Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다. macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.

Azure CLI를 사용하면 명령줄이나 스크립트를 통해 가상 머신 및 디스크와 같은 Azure 리소스를 관리할 수 있습니다. 지금부터 Azure Virtual Machines로 무엇을 할 수 있는지 알아보겠습니다.

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- Azure CLI를 사용하여 가상 머신 만들기
- Azure CLI를 사용하여 가상 머신 크기 조정
- Azure CLI를 사용하여 기본 관리 작업 수행
- SSH 및 Azure CLI를 사용하여 실행 중인 VM에 연결

## <a name="prerequsites"></a>필수 구성 요소

- **CLI를 사용하여 Azure 서비스 제어** 모듈에서 Azure CLI 도구의 기본 사항을 이해합니다.