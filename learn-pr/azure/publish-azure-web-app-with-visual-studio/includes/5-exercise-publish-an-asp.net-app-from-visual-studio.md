이제 로컬에서 ASP.NET Core 웹 응용 프로그램이 실행되고 있습니다. 이 단원에서는 Azure App Service에 응용 프로그램을 게시합니다.

### <a name="visual-studio-for-windows"></a>Windows용 Visual Studio

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.

1. 나타나는 대화 상자에서 왼쪽에 있는 **App Service**를 게시 대상으로 선택합니다.  오른쪽에서 **새로 만들기**를 선택하여 새 App Service를 만듭니다.

1. **게시** 단추를 클릭하여 새 App Service를 만듭니다.

> [!NOTE]
> 앱을 배포할 때 새 App Service 계획을 만들 수도 있고 기존 계획에 앱을 계속 추가할 수도 있습니다. 이 연습에서는 새 **Azure App Service**를 만듭니다.

### <a name="visual-studio-mac"></a>Visual Studio Mac

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.

1. **게시**를 선택합니다.

1. **Azure에 게시**를 클릭합니다. 이렇게 하면 Azure 계정에 연결됩니다. 현재 서비스를 연결하고 나열하는 데 몇 분 정도 걸릴 수 있습니다.

1. **새로 만들기**를 클릭하여 새 App Service를 만듭니다.

## <a name="configure-your-new-azure-app-service"></a>새 Azure App Service 구성

1. **App Service 만들기** 대화 상자에서 **계정 추가**를 클릭하고, Azure 구독에 로그인합니다. 이미 로그인한 경우 드롭다운 메뉴에서 원하는 구독이 포함된 계정을 선택합니다.

1. App Service 계획에 대한 필수 정보를 입력합니다.

    ![App Service 만들기](../media-draft/5-CreateAppService.png)

    **App Service 만들기** 대화 상자에서 다음 정보를 입력합니다.

    - **앱 이름**: 응용 프로그램의 이름입니다.  앱 이름은 게시된 응용 프로그램의 URL을 판별하며, https://_AppName_.azurewebsites.net 형식입니다.  고유한 값이어야 합니다. 따라서 예약되지 않은 이름을 찾으려면 여러 가지 다른 이름을 시도해야 할 수 있습니다.

    - **구독**: App Service를 배포하려는 Azure 구독입니다.

    - **리소스 그룹**: 리소스 그룹 옆의 **새로 만들기...** 단추를 클릭하고 리소스 그룹의 고유한 이름을 입력합니다.

        ![새 리소스 그룹](../media-draft/5-NewResourceGroup.png)

    - **호스팅 계획:** 호스팅 계획은 위치, 크기 및 앱을 호스트하는 웹 서버 팜의 기능을 지정합니다. 기존 호스팅 계획을 선택하거나 새 계획을 만들 수 있습니다. 이 연습에서는 새 계획을 만듭니다.

        호스팅 계획 옆에 있는 **새로 만들기...** 단추를 클릭합니다.

        ![새 호스팅 계획](../media-draft/5-NewHostingPlan.png)

        호스팅 계획에 이름을 지정한 다음 위치와 크기를 지정합니다.  
        
        > [!NOTE]
        > 다른 위치 및 크기를 지정하면 서비스 비용에 영향이 미칩니다. 이 연습에서는 **무료** 크기를 지정하여 비용이 부과되지 않도록 하는 것이 좋습니다.

    - **Application Insights:** 응용 프로그램에 Application Insights를 사용할지를 지정합니다. 이 연습에서는 **없음**을 선택하는 것이 좋습니다.

1. App Service를 프로비전하려면 **만들기** 단추를 클릭합니다. 배포 시 진행률이 표시됩니다.

    ![배포 진행률](../media-draft/5-DeployProgress.png)

1. App Service가 프로비전되면 Visual Studio에서 웹앱을 빌드하여 배포합니다.  Visual Studio 빌드 출력에서 배포 출력을 볼 수 있습니다.

    ![결과 게시](../media-draft/5-PublishResult.png)

1. 축하합니다. 이제 ASP.NET Core 웹 응용 프로그램이 게시되어 라이브 상태가 됩니다. 빌드 출력과 Visual Studio의 게시 페이지에서도 사이트의 최종 URL을 볼 수 있습니다.

    ![결과 게시](../media-draft/5-PublishPage.png)

1. 웹 사이트를 테스트하려면 표시된 URL로 이동합니다.

    ![라이브 사이트](../media-draft/5-WebPageLive.png)

## <a name="summary"></a>요약

이 연습에서는 Azure App Service를 프로비전하고 ASP.NET Core 웹 응용 프로그램을 배포하는 과정을 보여 줍니다. 이제 라이브 웹앱이 있습니다.
