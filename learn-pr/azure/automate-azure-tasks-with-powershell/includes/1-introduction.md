관리 스크립트 만들기는 워크플로를 최적화하는 강력한 방법입니다. 공통적인 반복 작업을 자동화할 수 있고, 스크립트가 확인된 후에는 지속적으로 실행되어 오류가 감소할 수 있습니다.

Azure VM(Virtual Machines)을 사용하여 CRM(고객 관계 관리) 소프트웨어를 테스트하는 회사에 근무한다고 가정합니다. VM은 웹 프런트 엔드, 비즈니스 논리를 구현하는 웹 서비스 및 SQL 데이터베이스를 포함하는 이미지에서 빌드됩니다.

단일 VM에서 여러 번의 테스트를 실행했지만 데이터베이스 및 구성 파일의 변경 내용으로 인해 일치하지 않는 결과가 발생할 수 있음을 알았습니다. 한 경우에 버그로 인해 데이터베이스에는 해당하는 고객 없이 전화 통화 레코드가 생성되었습니다. 고아 레코드로 인해 버그가 수정된 후에도 후속 통합 테스트가 실패했습니다. 각 테스트 주기에 새 VM 배포를 사용하여 이 문제를 해결하려고 합니다. 매주 여러 번 실행되므로 VM 만들기 설정을 자동화하려고 합니다. 

여기서 Azure PowerShell을 사용하여 Azure 리소스를 관리하는 방법을 살펴봅니다. 일회성 작업에 Azure PowerShell을 대화형으로 사용하고 반복 작업을 자동화하는 스크립트를 작성합니다. 

## <a name="learning-objectives"></a>학습 목표
이 모듈에서는 다음을 수행합니다.

- Azure PowerShell이 Azure 관리 작업에 적합한 도구인지 결정
- Linux, macOS 및 Windows에 Azure PowerShell 설치
- Azure PowerShell을 사용하여 Azure 구독에 연결
- Azure PowerShell을 사용하여 Azure 리소스 만들기

## <a name="prerequisites"></a>필수 조건

- PowerShell 또는 Bash와 같은 명령줄 인터페이스 경험
- 리소스 그룹 및 Virtual Machines와 같은 기본 Azure 개념에 대한 지식
- Azure Portal을 사용하여 Azure 리소스 관리 경험
