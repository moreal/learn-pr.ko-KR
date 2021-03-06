Azure Portal은 단일 작업을 수행하고 리소스 상태에 대한 빠른 개요를 확인하는 데 적합합니다. 그러나 매일 또는 매시간 반복해야 하는 작업의 경우 명령줄 및 테스트된 명령 또는 스크립트 집합을 사용하면 작업을 더욱 빠르게 수행하고 오류를 방지할 수 있습니다.

Azure Web Apps를 개발하는 회사에서 근무한다고 가정합니다. 이러한 응용 프로그램은 Azure에서 호스트되고 자동으로 구성된 보안, 부하 분산, 관리 등의 모든 혜택을 포함합니다. 현재 다른 데이터베이스 및 다른 데이터 원본의 입력 범위를 기반으로 판매 예측을 생성하는 웹앱을 테스트 중입니다. 개발자는 Windows, Linux 및 Mac 컴퓨터를 사용하고 일상적인 응용 프로그램 빌드에 GitHub 리포지토리를 사용합니다.

테스트의 일부로 다양한 데이터 원본 및 다양한 유형의 데이터 연결에 대한 앱 성능을 비교하려고 합니다. 개발 팀이 Azure Portal을 사용하여 앱의 새 테스트 인스턴스를 만들 때 항상 똑같은 매개 변수를 사용하는 것은 아님을 확인했습니다. 각 앱 테스트에 표준 배포 명령 집합을 사용하여 이 문제를 해결하려고 합니다. 이 명령 집합은 필요한 경우 자동화할 수 있고 소프트웨어 팀이 사용하는 모든 컴퓨터에서 동일한 방식으로 작동합니다.

이 모듈에서는 Azure CLI를 사용하여 Azure 리소스를 관리하는 방법을 보여 줍니다.

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- Linux, macOS 및/또는 Windows에 Azure CLI 설치
- Azure CLI를 사용하여 Azure 구독에 연결
- Azure CLI를 사용하여 Azure 리소스 만들기

## <a name="prerequisites"></a>필수 구성 요소

- PowerShell 또는 Bash와 같은 명령줄 인터페이스 경험
- 리소스 그룹과 같은 기본 Azure 개념에 대한 지식
- Azure Portal을 사용하여 Azure 리소스 관리 경험