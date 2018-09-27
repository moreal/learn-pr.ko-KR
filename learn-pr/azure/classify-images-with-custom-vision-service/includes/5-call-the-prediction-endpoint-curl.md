마지막 연습에서 Custom Vision Service 포털의 **빠른 테스트** 기능을 사용하여 학습된 모델을 테스트하였습니다. 이 방법은 몇 가지 테스트 이미지를 사용하여 모델의 정확도를 신속하게 확인할 수 있는 좋은 방법입니다. 조금 더 진도를 나가 HTTP를 통한 모델의 예측 엔드포인트를 호출해보겠습니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

1. Custom Vision Service 포털에서 *아트워크** 프로젝트로 돌아가서 **성능** 탭을 선택합니다.

    ![성능 탭 선택](../media/5-performance-tab.png)

1. **기본값으로 설정**을 선택하여 모델의 최신 반복이 기본 반복인지 확인합니다.

1. **예측 URL**을 선택합니다. 그러면 호출하는 데 필요한 정보의 대화 상자가 표시됩니다. 

    ![예측 URL 정보 보기](../media/5-portal-prediction-url.png)

    대화 상자에 표시된 것처럼 예측 엔드포인트를 호출하고 이미지 URL을 전달할 수 있습니다. 또한 원시 이미지를 요청 본문의 엔드포인트로 전달할 수 있습니다.

    이 대화 상자에서 세 가지 정보를 기록해둡니다.
     - **예측-키**: 이 키는 모든 요청에서 헤더로 설정돼야 합니다. 그렇게 해서 엔드포인트에 대한 액세스 권한을 제공합니다.
    - **요청 URL**: 대화 상자에 두 가지 다른 URL이 표시됩니다. 이미지 URL을 게시하는 경우 `/url`에서 종료되는 첫 번째 URL을 사용합니다. 요청 본문의 원시 이미지를 게시하려는 경우 `/image`에서 종료되는 두 번째 URL을 사용합니다.
    - **콘텐츠-형식**: 원시 이미지를 게시하는 경우 요청 본문을 `application/octet-stream`에 대한 콘텐츠 형식과 이미지의 이진 표현으로 설정합니다. 이미지 URL을 게시하는 경우 본문에 JSON으로 삽입하고 콘텐츠 유형을 `application/json`으로 설정합니다.
    

3. **예측 API 사용 방법** 대화 상자에서 첫 번째 URL 및 `Prediction-Key` 값을 복사하고 저장합니다. 

> [!TIP]
> **cURL**은 파일을 보내거나 받는 데 사용할 수 있는 명령줄 도구입니다. Linux, macOS 및 Windows 10에 포함되어 있으며 대부분의 다른 운영 체제에 다운로드할 수 있습니다. cURL은 HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 등과 같은 많은 프로토콜을 지원합니다. 자세한 내용은 아래 링크를 참조하세요.
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/> 
> 
> cURL은 샌드박스의 Azure Cloud Shell에 이미 설치되어 있습니다. 따라서 이 연습에서는 해당 엔드포인트에 대해 HTTP를 호출하기 위해 cURL을 사용하겠습니다.

2. Cloud Shell에서 다음 명령을 실행합니다. **[엔드포인트-URL]** 을 마지막 단계에서 저장한 URL로 바꿉니다. **[예측-키]** 를 마지막 단계에서 저장한 `Prediction-Key`의 값으로 바꿉니다. 

    ```azurecli
    curl [endpoint-URL] \
    -H "Prediction-Key: [Prediction-Key]" \
    -H "Content-Type: application/json" \
    -d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/VanGoghTest_02.jpg'}" \
    | jq '.'
    ```

    명령이 완료되면 다음 스크린샷과 유사한 JSON 응답이 표시됩니다. API는 모델의 모든 태그에 대한 확률을 반환합니다. 알 수 있듯이 `"painting"` **tagName** 값에 대해 1에 가까운 확률로 이 이미지는 명백하게 그림입니다. 그러나 해당 모델을 학습한 아티스트가 그린 그림은 아닙니다. 

    ![피카소 테스트 이미지 썸네일](../media/5-prediction-json.png) 

3. 위의 요청 본문의 URL을 다음 표의 URL로 바꿔 더 자주 예측을 시도합니다. 

    |이미지  | URL  |
    |---------|---------|
    |![피카소 테스트 이미지 썸네일](../media/picasso-test-02-thumb.jpg)     | `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PicassoTest_02.jpg`        |
    |![렘브란트 테스트 이미지 썸네일](../media/rembrandt-test-01-thumb.jpg)     |  `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/RembrandtTest_01.jpg`       |
    |![폴록 테스트 이미지 썸네일](../media/pollock-test-01-thumb.jpg)  |   `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PollockTest_01.jpg`     |
   

해당 예측 엔드포인트가 예상대로 작동합니다. API를 호출하는 것은 예측-키 및 이미지 URL을 사용하여 엔드포인트에 대해 HTTP 요청을 하는 것만큼 간단합니다.