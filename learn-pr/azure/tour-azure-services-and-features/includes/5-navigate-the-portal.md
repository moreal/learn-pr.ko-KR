이제 계정이 있으니 **Azure Portal**에 로그인할 수 있습니다. 이 포털은 웹 기반 관리 사이트로, 여러분이 만든 모든 구독 및 리소스와 상호 작용이 가능합니다. Azure에서 수행하는 거의 모든 작업은 이 웹 인터페이스를 통해 수행할 수 있습니다.

## <a name="azure-portal-layout"></a>Azure Portal 레이아웃

Azure Portal은 Microsoft Azure를 제어하기 위한 기본 GUI(그래픽 사용자 인터페이스)입니다. 포털에서 대부분의 관리 작업을 수행할 수 있고, 포털은 일반적으로 단일 작업을 수행하거나 구성 옵션을 자세히 보기에 가장 적합한 인터페이스입니다.

![Azure Portal](../media-draft/5-portal.png)

:::row:::

    :::column:::
    ![The resources and favorites](../media-draft/5-favorites.png)
    :::column-end:::

    :::column span="3":::
    **Resource Panel**
    
    In the left-hand sidebar of the portal is the resource pane, which lists the main resource types. Note that Azure has more resource types than just those shown. The resources listed are part of your _favorites_. 

    You can customize this with the specific resource types you tend to create or administer most often. 

    You can also collapse this pane; with the **<<** caret. This will minimize it to just icons which can be convenient if you are working with limited screen real-estate.
    :::column-end:::

:::row-end:::

포털 보기의 나머지 부분은 여러분이 사용하는 특정 요소와 관련이 있습니다. 기본(주) 페이지는 _대시보드_입니다. 이 내용은 조금 후에 설명하겠지만, 리소스에 대해 사용자 지정이 가능한 조감도를 나타냅니다. 이 페이지를 사용하여 관리하려는 특정 리소스로 이동하거나, 리소스 패널에서 **모든 리소스** 항목을 사용하여 리소스를 검색할 수 있습니다. 가상 머신이나 웹앱 같은 리소스를 관리할 때에는 리소스에 대한 구체적인 정보를 표시하는 _블레이드_를 사용합니다.

## <a name="what-is-a-blade"></a>블레이드란?

Azure Portal에서는 탐색을 위해 블레이드 모델을 사용합니다. _블레이드_는 탐색 시퀀스의 한 수준에 사용되는 UI가 포함된 슬라이드 아웃 패널입니다. 예를 들어 이 시퀀스의 각 요소는 **가상 머신** > **계산** > **Ubuntu Server** 같은 블레이드로 표시됩니다.

각 블레이드에는 몇 가지 정보와 구성 가능한 옵션이 포함되어 있습니다. 이러한 옵션 중 일부는 기존 블레이드의 오른쪽에 자신을 표시하는 다른 블레이드를 생성합니다. 새 블레이드에서는 모든 추가 구성 가능한 옵션이 또 다른 블레이드를 생성하는 방식으로 수행됩니다. 금방 여러 블레이드가 동시에 열려 있는 상태가 될 수 있습니다. 블레이드를 최대화하여 전체 화면을 채울 수도 있습니다.

새 블레이드는 항상 소유자의 오른쪽에 추가되므로 창의 맨 아래에 있는 스크롤 막대를 사용하여 뒤로 이동하면 구성에서 이 지점까지 어떻게 도달했는지 확인할 수 있습니다. 또는 블레이드의 맨 위 모서리에 있는 `X` 단추를 클릭하여 블레이드를 개별적으로 닫을 수 있습니다. 변경 내용을 저장하지 않고 계속하면 변경 내용이 손실될 수 있다고 알려주는 메시지가 Azure에 표시됩니다.

## <a name="configuring-settings-in-the-azure-portal"></a>Azure Portal에서 설정 구성

Azure Portal에는 여러 구성 옵션이 표시되며, 대부분은 화면 맨 위 오른쪽의 상태 표시줄에 표시됩니다.

### <a name="notifications"></a>알림

벨 아이콘을 클릭하면 **알림** 창이 표시됩니다. 이 창에는 수행한 마지막 작업이 해당 상태와 함께 나열됩니다.

### <a name="cloud-shell"></a>Cloud Shell

**Cloud Shell** 아이콘(>_)을 클릭하면 새 Azure Cloud Shell 세션이 만들어집니다. Azure Cloud Shell은 Azure 리소스를 관리하기 위한 브라우저에서 액세스할 수 있는 대화형 셸입니다. 작업 방식에 가장 적합한 셸 환경을 유연하게 선택할 수 있습니다. Linux 사용자는 Bash 환경을 선택할 수 있으며, Windows 사용자는 PowerShell을 선택할 수 있습니다. 이 브라우저 기반 터미널을 사용하면 포털에 내장된 명령줄 인터페이스를 통해 현재 구독에 포함된 모든 Azure 리소스를 제어하고 관리할 수 있습니다.

### <a name="settings"></a>설정

Azure Portal 설정을 변경하려면 **톱니** 아이콘을 클릭합니다. 이러한 설정에는 다음이 포함됩니다.

- 로그아웃 시간
- 색상 및 대비 테마
- 알림 메시지(모바일 장치 대상)
- 언어 및 지역 형식

![포털 설정](../media-draft/5-settings-blade.png)

설정을 변경한 경우 **적용**을 클릭하여 변경을 수락합니다.

### <a name="feedback-blade"></a>피드백 블레이드

**웃는 얼굴** 아이콘을 클릭하면 **피드백 보내기** 블레이드가 열립니다. 여기에서 Azure에 대한 피드백을 Microsoft로 보낼 수 있습니다. Microsoft가 이메일로 피드백에 응답할 수 있는지 여부를 지정할 수 있습니다.

### <a name="help-blade"></a>도움말 블레이드

**물음표** 아이콘을 클릭하면 **도움말** 블레이드가 표시됩니다. 여기서 다음과 같은 몇 가지 옵션 중에 선택할 수 있습니다.

- 새로운 기능
- Azure 로드맵
- 둘러보기 시작
- 바로 가기 키
- 진단 표시
- 개인정보처리방침 및 사용 약관

### <a name="directory-and-subscription"></a>디렉터리 및 구독

**책 및 필터** 아이콘을 클릭하여 **디렉터리 + 구독** 블레이드를 표시합니다.

Azure를 사용하면 두 개 이상의 구독을 하나의 디렉터리와 연결할 수 있습니다. **디렉터리 및 구독** 블레이드에서는 구독 간을 변경할 수 있습니다. 여기서 구독을 변경하거나 다른 디렉터리로 변경할 수 있습니다.

![디렉터리](../media-draft/5-directory-blade.png)

### <a name="profile-settings"></a>프로필 설정

오른쪽 위에 있는 이름을 클릭하면 프로필 설정을 변경할 수 있습니다.
옵션은 다음과 같습니다.

- Azure에서 로그아웃
- 암호 변경
- 연락처 정보 변경
- 권한 보기
- Azure 팀에 아이디어 제출
- 청구서 보기
- 디렉터리 전환(이전 섹션처럼 **디렉터리 + 구독** 블레이드 표시)

지금 **청구서 보기**를 클릭하면 Azure에서 비용이 발생하는 부분을 분석할 수 있는 **Cost Management + 청구 - 송장** 페이지로 이동됩니다.

Azure는 대규모 제품이며 Azure Portal 사용자 인터페이스(UI)에는 이러한 특징이 잘 반영되어 있습니다. 슬라이딩 블레이드 방식이기 때문에 다양한 관리 작업을 앞뒤로 쉽게 탐색할 수 있습니다. 연습을 위해 이 UI를 조금 실험해 보겠습니다.