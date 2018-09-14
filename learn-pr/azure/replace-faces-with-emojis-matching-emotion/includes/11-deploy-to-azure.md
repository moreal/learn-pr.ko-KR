지금이 모듈에서는 했습니다 관리는 Slack을 가져오려고 _슬래시_ 명령 ngrok를 사용 하 여이 컴퓨터에 터널링 하 여 localhost에 실행 하는 동안에 작동 합니다. 이 경우 개발 했지만 릴리스 코드를 클라우드에서 실행 합니다.

이 강의 하겠습니다 Azure 함수를 클라우드에 배포 하 여 코드의 새 프로덕션 버전을 사용 하 여 slack 구성을 업데이트 합니다.

이 강의의 끝에서 배웁니다.

- Azure에서 Azure 함수 앱을 만드는 방법
- Visual Studio Code를 사용 하 여 Azure에 배포 하는 방법
- 적용 방법 프로덕션 환경으로 로컬 설정

## <a name="create-an-azure-function-app-on-azure"></a>Azure에서 Azure 함수 앱 만들기

VS Code 및 Azure 함수 확장을 사용 하 여 azure 함수를 만들 예정입니다.

1. 사용 하 여 명령 팔레트 <kbd>Ctrl</kbd>+<kbd>P</kbd> 선택한 `Azure Function: Deploy to Function App`합니다.

   ![함수 앱에 배포](/media-drafts/10.deploy-to-function-app.png)

2. 현재 프로젝트를 업로드 하 고 계속 해 서 선택 하려는 것인지 묻는 메시지가 나타납니다.

   ![배포 폴더를 선택 합니다.](/media-drafts/10.select-folder-to-deploy.png)

3. 앱과 연결할 구독을 선택 합니다.

   Azure를 처음 접하는 경우에 구독이 두 개, 선택 해야 합니다.

4. 선택한 새 함수 앱 만들기

   ![새 함수 앱 만들기](/media-drafts/10.create-new-function-app.png)

5. 앱에 대 한 이름을 선택합니다

   이름을 선택 하 여 원하는 호출을 묻는 메시지가 나타납니다. 마이닝 호출 하려는 `mojifier-slack-function-app`합니다.

   ![앱 이름 선택](/media-drafts/10.choose-app-name.png)

6. 새 리소스 그룹 만들기

   리소스 그룹은 Azure에서 여러 서비스를 하나의 그룹화 하는 방법 _앱_합니다. 새 또는 사용 하 여 이미 만든 기존 것을 만들 수 있습니다.

   하나의 고 자동으로 채웁니다 이름을 새를 만들 경우 선택 하거나 다른 입력 합니다.

7. 선택할 _새 저장소 계정을 만드는_합니다.

   함수 앱을 저장소 계정, 데이터 저장 및 파일에 더 영구적인 위치 해야합니다. 새 또는 사용 하 여 이미 만든 기존 것을 만들 수 있습니다.

   자동-채웁니다 이름을; 선택 하거나 다른 입력 합니다.

8. 지역 선택

   함수 앱 라이브 위치 해야 합니다. 귀하 또는 사용자에 게 가장 가까운 위치를 선택는 것이 좋습니다. I 선택 `West Europe`

   ![앱 이름 선택](/media-drafts/10.select-region.png)

9. 업로드가 완료 [출력] 창을 URL을 보여 줍니다. 완료 되 면 같은 따라서 기다립니다.

```output
Deployment to "mojifier-slack-function-app" completed.
HTTP Trigger Urls:
  MojifyImage: https://mojifier-slack-function-app.azurewebsites.net/api/MojifyImage
```

## <a name="try-it-out"></a>체험

이 시점에서 적어도 리라는 `RespondToSlackCommand` 다른 종속성에 의존 하지 이후 작동 하는 함수입니다.

방문 `[deployed-app-name].azurefunctions.com/api/RespondToSlashCommand?text=[image-url]`

모두 작동 하는 경우 다음도 하는 브라우저 창에서 반환 된 일부 JSON 다음과 같이 합니다.

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "https://mojifier-slack.azurewebsites.net/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```

## <a name="upload-settings"></a>업로드 설정

일부 설정에 있다고 기억 `local.settings.json` cognitive services에 대 한 키와 URL을 얻었습니다.

`local.settings.json` 로컬이 복사 되지 통해 프로덕션에 배포 하는 경우 정확 하 게 됩니다.

포털로 이동 하 고 아마도 UI 또는 사용을 통해 설정에 수동으로 추가을 해야 일반적으로 `func` CLI를 동일한 작업을 수행 합니다.

그러나 VS Code를 사용 하기 때문에 로컬 설정을 업로드할 Azure Func 확장 하 고 명령 팔레트 사용할 수 있습니다.

1.  사용 하 여 명령 팔레트 <kbd>Ctrl</kbd>+<kbd>P</kbd> 선택한 `Azure Functions: Upload Local Settings`합니다.

    ![로컬 설정 업로드](/media-drafts/10.upload-local-settings.png)

2.  선택 `local.settings.json`

    ![로컬 설정 선택](/media-drafts/10.choose-localsettings.png)

3.  함수 앱이 연결 된 구독을 선택 합니다.

4.  함수 앱에 업로드 하려는 선택, 라고 마이닝 `mojifier-slack-function-app`

5.  모든 설정을 덮어쓰려면 요청을 하는 경우 선택 `No To All`

    이 업로드 새 설정 하는 것, 그렇지 않은 경우 개발에서 설정 사용 하 여 프로덕션 설정을 재정의 하면 위험이 있습니다.

    ![로컬 설정 선택](/media-drafts/10.choose-no-to-all.png)

## <a name="try-it-out"></a>체험

이제 모든 항목이 예상 대로 작동 하는 경우 다음 이제 MojifyImage 끝점 해야 작동 합니다.

방문 `[deployed-app-name].azurefunctions.com/api/MojifyImage?imageUrl=[image-url]`

모든 사이트가 잘 작동 하는 경우 창의 mojified 이미지를 볼 해야 있습니다.

작동 하지 않는 경우 여기에 문제 해결 시도 합니다.

## <a name="update-slack"></a>Slack 업데이트

함수를 클라우드에 배포한 이제 새 가리키도록 Slack의 설정을 업데이트할 수 있습니다 _공용_ URL입니다.

1. 공용 URL을 사용 하 여 Slack을 업데이트 하면 `RespondToSlackCommand`합니다.

![Slack 프로덕션 URL로 업데이트](/media-drafts/10.deploy-update-url.png)

> **참고**
>
> 프로덕션을 사용 하는 명령을 업데이트 _공용_의 버전을 `RespondToSlackCommand` 에서 호스트 `*.azurewebsites.net`

## <a name="try-it-out"></a>체험

Slack 로컬 앱 보다는 배포 된 앱에서 데이터를 요청 및 모든 항목이 올바르게 구성 되어 있는지를 확인 하려면을 해제할 수 있도록 `ngrok` 지금은 합니다.

다음 창 slack 및 즐겨 slack 슬래시 명령을 입력으로 이동 합니다.

`/mojify <image>`

모든 작업 예상 대로 경우 slack 창에 표시 하는 이미지 표시 다음과 같이 합니다.

![Win](/media-drafts/10.publish-success.png)
