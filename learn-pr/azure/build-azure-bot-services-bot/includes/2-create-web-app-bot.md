봇을 만드는 첫 번째 단계는 Azure에서 봇이 호스트되는 위치를 제공하는 것입니다. Azure App Service의 [Web Apps](https://azure.microsoft.com/services/app-service/web/) 기능은 봇 응용 프로그램을 호스팅하는 데 적합하며 Azure Bot Service는 이러한 응용 프로그램을 자동으로 프로비전하도록 디자인되었습니다. 이 단원에서는 Azure Portal을 사용하여 Azure 웹앱 봇을 프로비전합니다.

1. 브라우저에서 [Azure Portal](https://portal.azure.com/?azure-portal=true)을 엽니다. 로그인하라는 메시지가 표시되면 Microsoft 계정을 사용하여 로그인합니다.

1. **+ 리소스 만들기**, **AI + 기계 학습** 및 **웹앱 봇**을 차례로 클릭합니다.
 
    ![새 Azure 웹앱 봇 만들기](../media-draft/2-new-bot-service.png)

1. **앱 이름** 상자에 “qa-factbot”와 같은 이름을 입력합니다. *이 이름은 Azure 내에서 고유해야 하므로 녹색 확인 표시가 옆에 나타나는지 확인해야 합니다.* **리소스 그룹** 아래에서 **새로 만들기**를 선택하고 리소스 그룹 이름으로 “factbot-rg”를 입력합니다. 내게 가장 가까운 위치를 선택하고 무료 **F0** 가격 책정 계층을 선택합니다. 그런 다음, **봇 템플릿**을 클릭합니다.

    ![Azure 웹앱 봇 구성](../media-draft/2-portal-start-bot-creation.png)

1. SDK 언어로 **Node.js**를 선택하고 템플릿 유형으로 **질문 및 답변**을 선택합니다. 그런 다음, 블레이드 맨 아래에서 **선택**을 클릭합니다.   
  
    ![언어 및 템플릿 선택](../media-draft/2-portal-select-template.png)

1. 이제 **App Service 계획/위치**, **새로 만들기**를 차례로 클릭하고 3단계에서 선택한 것과 동일한 지역에서 이름이 “qa-factbot-service-plan”이거나 비슷한 이름을 갖는 App Service 계획을 만듭니다. 완료되면 “웹앱 봇” 블레이드 맨 아래에서 **만들기**를 클릭하여 배포를 시작합니다. 

1. 포털 왼쪽에 있는 리본에서 **리소스 그룹**을 클릭합니다. 그런 다음, **factbot-rg**를 클릭하여 Azure 웹앱 봇용으로 만든 리소스 그룹을 엽니다. 블레이드 위쪽에서 “배포 중”이 “성공함”으로 바뀔 때까지 기다립니다. 이것은 Azure 웹앱 봇이 성공적으로 배포되었음을 나타냅니다. 배포에는 일반적으로 2분 정도의 시간이 필요합니다. 블레이드 위쪽에 있는 **새로 고침**을 주기적으로 클릭하여 배포 상태를 새로 고칩니다.

    ![배포 정상 완료](../media-draft/2-deployment-succeeded.png)
  
Azure 웹앱 봇이 배포될 때 내부적으로 많은 작업이 수행되었습니다. 봇이 생성되어 등록되고, 봇을 호스트할 [Azure 웹앱](https://azure.microsoft.com/services/app-service/web/)이 생성되고, 봇이 [Microsoft QnA Maker](https://www.qnamaker.ai/)를 사용하도록 구성됩니다. 다음 단계에서는 QnA Maker를 사용하여 질문과 답변 기술 자료를 만들고 봇에 인텔리전스를 불어넣습니다.