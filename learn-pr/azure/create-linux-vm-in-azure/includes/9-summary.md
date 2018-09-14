이 모듈에서는 Azure Portal을 사용하여 Linux VM을 만드는 방법을 배웠습니다. 그런 다음, 해당 VM의 공용 IP 주소에 연결하고 SSH 연결을 통해 관리했습니다. 

SSH를 사용하면 가상 머신의 운영 체제 및 소프트웨어를 조작할 수 있고 포털을 사용하면 가상 하드웨어 및 연결을 구성할 수 있다는 것을 알았습니다. 명령줄이나 스크립트 가능 환경을 선호하는 경우 PowerShell 또는 Azure CLI를 사용할 수도 있습니다.

## <a name="clean-up-the-resources"></a>리소스 정리

VM이 실행되는 동안 VM 요금이 청구되고, 사용량에 따라 저장소 요금이 청구됩니다. VM을 사용하지 않을 때에는 항상 VM을 중지하고 할당을 취소해야 하며, 더 이상 리소스가 필요 없으면 리소스를 삭제하는 것이 좋습니다. 생성한 모든 리소스를 제거하려면 하나씩 삭제하거나 리소스 그룹을 삭제하면 됩니다.

1. Azure Portal에 로그인합니다.

1. 왼쪽 메뉴에서 **모든 서비스**를 선택합니다.

1. **리소스 그룹**을 선택합니다.

1. 첫 번째 연습에서 만든 리소스 그룹을 찾습니다. 목록 보기 오른쪽에 있는 줄임표(...)를 클릭합니다.

1. **리소스 그룹 삭제**를 선택합니다.

1. 다음 화면에서 리소스 그룹 이름을 입력하여 삭제를 확인합니다.

1. **삭제**를 클릭합니다.