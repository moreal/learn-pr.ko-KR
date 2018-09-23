Visual Studio Code용 Azure Cosmos DB 확장은 명령 창을 사용하여 리소스를 만들 수 있게 함으로써 계정, 데이터베이스 및 컬렉션 만들기를 간소화합니다.

이 단원에서는 Visual Studio용 Azure Cosmos DB 확장을 설치한 다음, 이 확장을 사용하여 계정, 데이터베이스 및 컬렉션을 만듭니다.

## <a name="install-the-azure-cosmos-db-extension-for-visual-studio"></a>Visual Studio용 Azure Cosmos DB 확장 설치

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb)로 이동하여 Visual Studio Code용 **Azure Cosmos DB** 확장을 설치합니다.

1. 확장 탭이 Visual Studio Code에 로드되면 **설치**을 클릭합니다.

1. 설치가 완료되면 **다시 로드**를 클릭합니다.

    Visual Studio Code에서 ![Azure 아이콘 표시](../media/2-setup/visual-studio-code-explorer-icon.png) 확장을 설치하고 다시 로드한 후 화면 왼쪽에 Azure 아이콘이 표시됩니다.

## <a name="create-an-azure-cosmos-db-account-in-visual-studio-code"></a>Visual Studio Code에서 Azure Cosmos DB 계정 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

1. Visual Studio Code에서 **보기** > **명령 팔레트**를 클릭하고 **Azure: Sign In**을 입력하여 Azure에 로그인합니다. Azure: Sign In을 사용하려면 [Azure 계정](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) 확장이 설치되어 있어야 합니다.

    > [!IMPORTANT]
    > 샌드박스를 만드는 데 사용된 동일한 계정을 사용하여 Azure에 로그인합니다. 샌드박스는 컨시어지 구독에 대한 액세스 권한을 제공합니다.

    지시에 따라 웹 브라우저에 제공된 코드를 복사하고 붙여넣어 Visual Studio Code 세션을 인증합니다.

1. 왼쪽 메뉴에서 ![Azure 아이콘](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure** 아이콘을 클릭한 다음, **컨시어지 구독**을 마우스 오른쪽 단추로 클릭하고 **계정 만들기**를 클릭합니다.

    나열된 컨시어지 구독이 표시되지 않은 경우 샌드박스를 만드는 데 사용된 동일한 계정을 사용하여 Visual Studio Code의 Azure에 로그인했는지 확인합니다. 또한 Azure 계정 확장에서 Azure 구독을 필터링한 경우 `> Azure: Select Subscriptions` 명령에 컨시어지 구독이 선택되어 있는지 확인하세요.

1. __+__ 단추를 클릭하여 Cosmos DB 계정 만들기를 시작합니다. 둘 이상의 구독이 있는 경우 구독을 선택하라는 메시지가 표시됩니다.

1. 화면 맨 위에 있는 텍스트 상자에 Azure Cosmos DB 계정의 고유한 이름을 입력한 다음 Enter 키를 누릅니다. 계정 이름은 소문자, 숫자 및 '-' 문자만 포함할 수 있으며, 3자에서 31자 사이여야 합니다.

1. 다음으로, **SQL(DocumentDB)** > **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 선택한 다음, 위치를 선택합니다.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    Visual Studio Code의 출력 탭에 계정 만들기 진행률이 표시되며, 완료하는 데 몇 분 정도 걸립니다.

1. 계정을 만든 후 **Azure: Cosmos DB** 창에서 Azure 구독을 확장하면 확장 프로그램에 새 Azure Cosmos DB 계정이 표시됩니다. 다음 이미지에서 새 계정 이름은 **학습 모듈**입니다.

    ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/azure-cosmos-db-vs-code-extension.png)

## <a name="create-an-azure-cosmos-db-database-and-collection-in-visual-studio-code"></a>Visual Studio Code에서 Azure Cosmos DB 데이터베이스 및 컬렉션 만들기

이제 고객을 위한 새 데이터베이스와 컬렉션을 만들어 보겠습니다.

1. Azure: Cosmos DB 창에서 새 계정을 마우스 오른쪽 단추로 클릭한 다음, **데이터베이스 만들기**를 클릭합니다.
1. 화면 맨 위의 입력 팔레트에서 데이터베이스 이름에 `Users`를 입력하고 Enter 키를 누릅니다.
1. 컬렉션 이름에 `WebCustomers`를 입력하고 Enter 키를 누릅니다.
1. 파티션 키에 `userId`를 입력하고 Enter 키를 누릅니다.
1. 마지막으로, 초기 처리량 용량에 대해 `1000`을 확인하고 Enter 키를 누릅니다.
1. **Azure: Cosmos DB** 창에서 계정을 확장하면 새 **사용자** 데이터베이스 및 **WebCustomers** 컬렉션이 표시됩니다.

    ![Visual Studio Code의 Azure Cosmos DB 확장 프로그램에 위의 지침을 보여 주는 애니메이션이 실행됩니다.](../media/2-setup/vs-code-azure-cosmos-db-extension.gif)

Azure Cosmos DB 계정이 있으므로 Visual Studio Code에서 작업을 시작해 보겠습니다.
