이 단원에서는 .NET Core 콘솔 응용 프로그램과 Azure Storage 계정을 만듭니다.

## <a name="create-a-net-core-console-application"></a>.NET Core 콘솔 응용 프로그램 만들기

Visual Studio 2017을 사용하여 앱을 만듭니다.

1. Visual Studio 2017에서 **파일** > **새로 만들기** > **프로젝트** 메뉴 옵션을 선택합니다.

1. **Visual C# - .NET Core** 범주 내에서 **콘솔 앱(.NET Core)** 을 선택하고 앱 이름을 입력한 다음, **확인**을 선택합니다.
  ![새 앱](..\media-draft\3-new-console-app.png)

## <a name="create-an-azure-storage-account"></a>Azure Storage 계정 만들기

Azure Storage 계정에 연결하려면 먼저 연결할 저장소 계정을 만들어야 합니다.

1. Azure Portal의 왼쪽 위에서 '리소스 만들기'를 선택합니다.

1. 표시되는 선택 창에서 ‘저장소’를 선택합니다.

1. 해당 창의 오른쪽에서 ‘저장소 계정 - Blob, File, Table, Queue’를 선택합니다.
  ![포털 선택](..\media-draft\3-portal-storage-select.png)

1. 저장소 계정의 세부 정보를 입력해야 합니다. 저장소 계정에 사용할 이름을 입력합니다.

1. 리소스 그룹은 리소스의 논리 컨테이너입니다. 선택한 리소스 그룹에 대해 **새로 만들기**를 선택하고 리소스 그룹의 이름을 입력합니다.

1. 다른 모든 옵션은 기본값으로 남겨 두고 **만들기**를 클릭합니다.
  ![포털 세부 정보](..\media-draft\3-portal-storage-details.png).

이제 리소스 그룹이 프로비전되고 있습니다. 그런 다음, 저장소 계정이 리소스 그룹 내에서 생성됩니다.
또한 응용 프로그램을 만들었으며, 해당 응용 프로그램을 구성하고 저장소 계정에 연결할 준비가 되었습니다.
