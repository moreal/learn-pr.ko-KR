Azure AD를 배포하고 어떤 사용자가 Azure Portal에 액세스할 때 Azure에서 Multi-Factor Authentication을 요구하는 조건부 액세스 정책을 사용하도록 결정했습니다. 디렉터리를 만들고 임시 라이선스를 가져와야 합니다.

## <a name="create-a-directory"></a>디렉터리 만들기
프로덕션 사용자에게 영향을 주지 않고 테스트할 수 있는 First Up Consultants에 대한 새 디렉터리를 만듭니다.

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.

1. 왼쪽 탐색 창에서 **리소스 만들기** > **ID** > **Azure Active Directory**를 차례로 클릭합니다.

1. **디렉터리 만들기** 블레이드에서 **조직 이름** 및 **초기 도메인 이름**에 대해 다음 값을 제공합니다.

   1. 조직 이름: `First Up Consultants`
   1. 초기 도메인 이름: `firstupconsultants<XXXX>.onmicrosoft.com`

1. 디렉터리가 만들어질 때까지 기다립니다. 링크를 클릭하여 새 디렉터리로 전환하거나 창 위쪽에서 **디렉터리 및 구독 필터**를 클릭한 다음, 새로 만든 디렉터리를 선택합니다.

## <a name="get-trial-licenses"></a>평가판 라이선스 가져오기

조건부 액세스 및 Multi-Factor Authentication과 같은 기능을 사용하려면 최소한 평가판 라이선스가 필요합니다. 다음 단계에서는 평가판 라이선스를 사용하도록 설정하는 방법을 안내합니다.

1. Azure AD **개요** 창에서 **평가판 시작** 링크를 클릭합니다.

1. **Azure AD Premium P2** 항목 아래에서 **평가판**을 클릭한 다음, **활성화**를 클릭합니다.

## <a name="create-a-test-user"></a>테스트 사용자 만들기

여기서는 사용자를 통해 테스트해야 합니다. 팀의 다른 멤버인 Isabella Simonsen이 자원하여 도움을 주었습니다. 디렉터리에 그녀의 계정이 필요하므로 계정을 만드는 단계를 거치게 됩니다.

1. **Azure Active Directory** > **사용자** > **모든 사용자**로 차례로 이동합니다.

1. **새 사용자**를 클릭합니다.

1. 사용자 이름이 **Isabella Simonsen**인 사용자를 만듭니다.

   * `Isabella@firstupconsultants<XXXX>.onmicrosoft.com`

1. 사용자에 대한 **암호 표시** 확인란을 선택합니다. 나중에 테스트할 때 사용할 수 있도록 암호를 적어 둡니다.

1. **만들기**를 클릭합니다.

## <a name="create-a-pilot-group"></a>파일럿 그룹 만들기

만든 정책을 사용자 그룹에 할당하지만 이 정책에 대한 그룹을 만들어야 합니다. 파일럿 배포에 대한 보안 그룹을 만드는 데 도움이 되는 단계는 다음과 같습니다.

1. **Azure Active Directory** > **그룹** > **모든 그룹**으로 차례로 이동합니다.

1. **새 그룹**을 클릭합니다.

1. 그룹 유형: **보안**

1. 그룹 이름: **AzurePortal-CA-MFA**

1. 멤버 자격 유형: **할당됨**

1. 이전 단계에서 만든 사용자를 선택하고 **선택**을 선택합니다.

1. **만들기**를 클릭합니다.

## <a name="summary"></a>요약

이 단원에서는 Azure Portal에 평가판 사용이 허가된 디렉터리, 테스트 사용자 및 파일럿 그룹을 만드는 방법을 알아보았습니다.
