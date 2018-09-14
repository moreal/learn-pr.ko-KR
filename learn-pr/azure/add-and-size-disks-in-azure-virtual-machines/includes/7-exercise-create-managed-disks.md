이 짧은 연습에서는 관리 되는 VHD를 기존, 관리 되지 않는 VHD를 마이그레이션하는 방법을 알아보겠습니다. 

## <a name="sign-in-to-azure"></a>Azure에 로그인

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.

## <a name="migrate-our-disks-to-managed-disks"></a>디스크를 managed disks로 마이그레이션

1. 왼쪽 탐색 창에서 Azure portal에서 선택 **가상 머신**합니다.

1. 가상 컴퓨터의 목록에서 가상 컴퓨터를 선택 **MailSenderVM**합니다.

1. 에 **MailSenderVM** 창 아래에 있는 **설정**를 선택 **디스크**합니다.

1. 에 **MailSenderVM-디스크** 페이지에서 **managed disks로 마이그레이션**합니다.

1. 에 **managed disks로 마이그레이션** 페이지에서 **마이그레이션**합니다. Azure VM을 중지 하 고 디스크를 마이그레이션합니다 다음 VM을 다시 시작 합니다. 이 프로세스에는 몇 분 정도 걸릴 수 있습니다.

이 연습에서 managed disks로 디스크 마이그레이션 했습니다. 관리 디스크를 사용 하 여 Azure를 관리 하기 때문에 해당 디스크에 대 한 저장소 계정을 구성할 필요가 없습니다.
