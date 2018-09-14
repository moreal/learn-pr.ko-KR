이 모듈에서는 HTML 기반 사용자 인터페이스를 표시하는 간단한 웹 응용 프로그램을 배포합니다. 서버 리스 백 엔드를 사용 하면 이미지를 업로드 하 고 설명이 포함 된 캡션이 자동으로 생성 합니다.

![웹앱 실행](../media/0-app-screenshot-finished.png)

다음 다이어그램에서는 응용 프로그램에서 사용하는 Azure 서비스를 보여 줍니다.

![솔루션 아키텍처 다이어그램](../media/0-architecture.jpg)

1. Azure Blob Storage는 정적 웹 콘텐츠(HTML, CSS, JS)를 제공하고 이미지를 저장합니다.
2. Azure Functions는 이미지 업로드, 크기 조정 및 메타데이터 저장을 관리합니다.
3. Azure Cosmos DB는 이미지 메타데이터를 저장합니다.
4. Azure Logic Apps는 Cognitive Services Computer Vision API에서 이미지 캡션을 검색합니다.
5. Azure Active Directory는 사용자 인증을 관리합니다.

Azure Blob Storage는 정적 파일을 호스트하는 데 사용할 수 있는 저렴한 비용의 확장성이 매우 뛰어난 서비스입니다. 이 모듈에서는 빌드하면 웹 앱에 대 한 정적 콘텐츠 (예: HTML, JavaScript 또는 CSS)를 제공 하도록 Blob 저장소를 사용는 있습니다.

## <a name="create-an-azure-storage-account"></a>Azure Storage 계정 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

Azure Storage 계정은 테이블, 큐, 파일, Blob(개체) 및 가상 머신 디스크를 저장하도록 허용하는 Azure 리소스입니다.

1. 이 자습서에 대한 정적 콘텐츠(HTML, CSS 및 JavaScript 파일)는 Blob Storage에서 호스트됩니다. Blob Storage를 사용하려면 저장소 계정이 필요합니다. 범용 v2를 만듭니다 (GPv2) 저장소 계정 리소스 그룹에 있습니다. `<storage account name>`을 고유한 이름으로 바꿉니다.

    ```azurecli
    az storage account create -n <storage account name> -g <rgn>[Sandbox resource group name]</rgn> --kind StorageV2 --https-only true --sku Standard_LRS
    ```
    
1. [Azure Portal](https://portal.azure.com/?azure-portal=true)의 맨 위에 있는 검색 표시줄을 사용하여 방금 만든 저장소 계정을 찾습니다. 계정을 엽니다.

1. 왼쪽 탐색 영역에서 **정적 웹 사이트(미리 보기)** 를 선택하고 정적 웹 사이트 호스팅을 위한 컨테이너를 구성합니다.
    - **사용**을 선택하여 정적 웹 사이트를 사용하도록 설정합니다.
    - **index.html**을 인덱스 문서 이름으로 입력합니다. 상자에는 이미 회색 글꼴로 *index.html*이 있지만 예제 텍스트일 뿐입니다. 상자에 **index.html**을 입력해야 합니다.
    - **저장**을 클릭합니다.
    
    ![정적 웹 사이트 설정 입력](../media/1-storage-static-website.png)

1. 자습서를 진행하면서 편리하게 복사할 수 있는 위치에 **기본 엔드포인트**를 저장합니다. 이 엔드포인트는 웹 응용 프로그램의 URL입니다.

## <a name="upload-the-web-application"></a>웹 응용 프로그램 업로드

1. 이 자습서에서 빌드한 응용 프로그램에 대한 원본 파일은 [GitHub 리포지토리](https://github.com/Azure-Samples/functions-first-serverless-web-application)에 위치합니다. Cloud Shell에서 홈 디렉터리로 이동한 다음이 리포지토리를 복제 합니다.

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    리포지토리는 `/home/<username>/functions-first-serverless-web-application`에 복제됩니다.

1. 클라이언트 쪽 웹 응용 프로그램은 **www** 폴더에 위치하고 Vue.js JavaScript 프레임워크를 사용하여 빌드됩니다. 엽니다는 **www** 폴더를 열고 **npm** 응용 프로그램을 빌드하고 응용 프로그램 종속성을 설치 하는 명령입니다. 이러한 명령 중 마지막을 완료하려면 몇 분 정도 걸릴 수 있습니다.

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    응용 프로그램은 **dist** 폴더에서 생성됩니다.

1. 현재 디렉터리를 **dist** 폴더로 변경하고 응용 프로그램을 **$web** Blob 컨테이너로 업로드합니다.

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. 응용 프로그램을 보려면 웹 브라우저에서 정적 웹 사이트의 기본 끝점 URL을 엽니다.

    ![첫 번째 서버를 사용하지 않는 웹앱 홈페이지](../media/1-app-screenshot-new.png)


## <a name="summary"></a>요약

이 단위는 저장소 계정을 만들었습니다. 라는 blob 컨테이너 **$web** 저장소에서 계정을 웹 응용 프로그램에 대 한 정적 콘텐츠를 저장 하 고 콘텐츠를 공개적으로 사용할 수 있도록 합니다. 다음으로,이 웹 응용 프로그램에서 Blob storage에 이미지를 업로드 하는 서버 리스 함수를 사용 하는 방법을 배웁니다.