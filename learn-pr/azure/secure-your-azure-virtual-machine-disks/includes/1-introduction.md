클라우드로의 전환을 진행 중인 창고 회사에 근무 중이라고 가정해 보겠습니다. 이 회사는 현재 온-프레미스 Windows 서버, Azure VM(Virtual Machines) 및 Azure Active Directory로 구성된 하이브리드 환경을 사용하고 있습니다. 그리고 공급업체에 대한 보안 주문 관리를 지원하는 사용자 지정 내부 B2B(기업 간) 인프라를 개발했습니다. 공급업체 중 일부는 Linux를 실행하므로 이러한 공급업체를 지원하기 위해 Azure에서 여러 Linux 서버를 실행하고 있습니다.

보안 정책상 자체 암호화 키를 사용하여 데이터를 암호화해야 하며 회사에서 이러한 키를 관리해야 합니다.

관리 팀은 온-프레미스 서버 관리를 위해 PowerShell을 이미 사용하고 있습니다. 여러 Azure VM을 배포 및 테스트할 예정이며, Azure Resource Manager 템플릿을 사용하여 이 프로세스를 자동화하려고 합니다.

여기서는 지정된 시나리오에서 ADE(Azure Disk Encryption)가 최상의 선택 항목인지를 결정할 수 있도록 VM 디스크에 사용 가능한 보호 기능의 유형을 살펴볼 것입니다. 그런 다음, 기존 VM 디스크에서 ADE를 사용하도록 설정하고, 템플릿을 사용하여 새 VM 배포에 대해 ADE를 사용하도록 설정합니다.


## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- VM에 가장 적합한 암호화 방법 확인
- Azure Portal을 사용하여 기존 VM 디스크 암호화
- PowerShell을 사용하여 기존 VM 디스크 암호화
- Azure Resource Manager 템플릿을 수정하여 새 VM에서 디스크 암호화 자동화
