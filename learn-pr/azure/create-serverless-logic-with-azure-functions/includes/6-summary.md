Azure Functions를 사용하여 클라우드에서 비즈니스 논리 서비스를 호스트하는 방법을 배웠습니다. 비즈니스와 함께 확장 및 성장할 수 있는 솔루션에 호스트된 서비스를 추가하기 좋은 방법입니다. 원하는 언어를 사용하여 코드에 초점을 맞추면 되고, 인프라 관리는 Azure에서 합니다. Functions는 Event Grid, GitHub, Twilio, Microsoft Graph 및 Logic Apps 같은 다른 서비스와 통합되어 복잡하고 강력한 서버리스 워크플로를 신속하고 간편하게 만들 수 있습니다.

## <a name="clean-up"></a>정리
Azure 함수는 트리거될 때만 실행되지만, 연습에서 만든 리소스를 제거해야 할 수 있습니다.

1. Azure 계정을 사용하여 [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

2. 왼쪽 메뉴에서 **모든 리소스**를 선택한 후 **escalator-functions-group**을 선택하여 첫 번째 연습에서 만든 리소스 그룹에 액세스합니다.

3. 도구 모음에서 **리소스 그룹 삭제** 단추를 누릅니다. 삭제할 리소스 그룹의 이름을 입력하라는 메시지가 표시됩니다. 완료되면 **삭제** 단추를 누릅니다.  

![리소스 그룹 삭제](../media-draft/6-cleanup.png)