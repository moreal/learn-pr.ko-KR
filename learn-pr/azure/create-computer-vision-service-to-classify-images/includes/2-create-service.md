
## <a name="what-is-microsoft-cognitive-services"></a>Microsoft Cognitive Services란?

Microsoft Cognitive Services는 누구나 사용할 수 있도록 서비스로 제공되는 기계 학습 알고리즘 집합입니다. 앱에 사용할 인텔리전스를 처음부터 구축하는 대신 시각, 음성, 언어, 지식 및 검색에 이 서비스를 사용할 수 있습니다. 각 서비스를 체험해볼 수 있습니다. 서비스를 앱에 통합하기로 결정하면 유료 구독에 등록합니다. 이 모델에서는 Computer Vision API에 중점을 둡니다.

> [!TIP]
> 모든 Cognitive Services 목록을 보려면 [Cognitive Services 디렉터리](https://azure.microsoft.com/services/cognitive-services/directory/)를 참조하세요. 

## <a name="what-is-the-computer-vision-api"></a>Computer Vision API란?

Computer Vision API는 이미지를 처리하고 인사이트 반환하는 알고리즘을 제공합니다. 예를 들어, 이미지에 완성도 높은 콘텐츠가 있는지 알아 내거나 서비스를 사용하여 이미지에 있는 얼굴을 모두 찾을 수 있습니다. 또한 지배적인 색과 강조 색을 판단하고, 이미지의 콘텐츠를 분류하며, 완전한 영어 문장으로 이미지를 기술하는 것과 같은 다른 기능도 있습니다. 큰 이미지를 효율적으로 표시할 수 있도록 이미지 썸네일을 지능적으로 생성할 수 있습니다.

> [!TIP]
> Computer Vision API는 전세계 많은 지역에서 사용할 수 있습니다. 가장 가까운 위치를 찾으려면 [지역별 사용 가능한 제품](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all)을 참조하세요.

Computer Vision API를 사용하여 가능한 작업:

- 인사이트를 위한 이미지 분석
- OCR(광학 문자 인식)을 사용한 이미지의 인쇄 텍스트 추출합니다.
- 이미지의 인쇄 텍스트 및 필기 텍스트 인식
- 유명인 및 랜드마크 인식
- 비디오 분석 
- 이미지의 썸네일 생성 

## <a name="how-to-call-the-computer-vision-api"></a>Computer Vision API를 호출하는 방법

클라이언트 라이브러리 또는 REST API를 직접 사용하여 응용 프로그램에서 Computer Vision을 호출합니다. 이 모듈에서는 REST API를 호출합니다. 호출을 수행하려면:

1. API 액세스 키 가져오기

    Computer Vision 서비스 계정을 등록할 때 액세스 키가 할당됩니다. **모든** 요청의 헤더에는 키가 전달되어야 합니다. 

1. API에 POST 호출 수행

    URL을 다음과 같은 형식으로 지정합니다 **지역**.api.cognitive.microsoft.com/vision/v2.0/**리소스**/**[매개 변수]** 

    - **지역** - 계정을 만든 지역, 예: *westus*.
    - **리소스** - 호출하는 Computer Vision 리소스(예: `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText`, `tag`)입니다.

    처리할 이미지는 원시 이미지 바이너리나 이미지 URL로 제공할 수 있습니다.

    요청 헤더에는 구독 키가 있어야 합니다. 구독 키는 이 API에 대한 액세스를 제공합니다.

1. 응답 구문 분석

    응답에는 내 이미지에 대해 Computer Vision API에 있는 인사이트가 JSON 페이로드로 보관됩니다.

`westus` 지역에서 내 Computer Vision 구독을 만들어서 API에 액세스할 구독 키를 확보했다고 가정합니다. 키에 `xxxx-xxxxx-xxxx-xxxx`라는 가상의 값을 부여하겠습니다. 이제 `http://example.com/images/test.jpg`에 있는 이미지의 썸네일을 생성해보겠습니다. `generateThumbnail`을 사용하는 요청은 다음과 같은 모양입니다.

```
curl POST "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {xxxx-xxxxx-xxxx-xxxx}"
-d "{'url':'http://example.com/images/test.jpg'}"
```

이 모듈에서는 통합된 Cloud Shell을 사용하여 Azure CLI의 모든 연습을 실행합니다. 이 설정에 대해 좀 더 알아보겠습니다.

## <a name="what-is-the-azure-cli"></a>Azure CLI란?

Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다. macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.

> [!IMPORTANT]
> Azure CLI 도구는 현재 Azure CLI 1.0 및 Azure CLI 2.0의 두 가지 버전이 있습니다. 레거시 스크립트를 실행하는 경우가 아니라면 최신 버전인 Azure CLI 2.0을 사용하는 것이 좋습니다. Azure CLI 1.0은 `azure` 명령으로 시작되고 Azure CLI 2.0은 `az` 명령으로 시작됩니다.

## <a name="az-cognitiveservices-commands"></a>az cognitiveservices 명령

Azure CLI에는 Azure의 Cognitive Services 계정을 관리하는 `cognitiveservices` 명령이 포함됩니다. 여러 하위 명령을 제공하여 특정 작업을 수행할 수 있습니다. 가장 일반적인 하위 명령은 다음과 같습니다.

| 하위 명령 | 설명 |
|-------------|-------------|
| `list` | 사용 가능한 Azure Cognitive Services 계정을 나열합니다. |
| `account show` | Azure Cognitive Services 계정의 세부 정보를 가져옵니다. |
| `account create` | Azure Cognitive Services 계정을 생성합니다. |
| `account delete` | Azure Cognitive Services 계정을 삭제합니다. |
| `keys list` | Azure Cognitive Services 계정의 키를 나열합니다. |

Azure CLI로 Cognitive Services를 생성해보겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a>Cognitive Services 계정 만들기

Computer Vision API를 호출하려면 API 액세스 키가 필요합니다. 액세스 키를 확보하려면 Computer Vision API에 대한 Cognitive Services 계정이 필요합니다. `az cognitiveservices create`을 사용하여 내 구독에 계정을 만들겠습니다.

 `az cognitiveservices create` 명령은 리소스 그룹에 Cognitive Services 계정을 만드는 데 사용됩니다.  이 명령을 호출할 때는 다음 다섯 가지 매개 변수를 제공해야 합니다.

> [!Tip]
> Azure CLI 매개 변수에 대한 대부분의 플래그는 단일 문자로 축약이 가능합니다. 예를 들어 `--location` 대신 `-l`이라고 입력할 수 있습니다. 긴 양식은 명확성을 위해 사용됩니다.

| 매개 변수 | 설명 |
|-----------|-------------|
| `resource-group` | Cognitive Services 계정을 소유할 리소스 그룹입니다. 이 대화형 샌드박스 세션에서는 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 사용합니다. |
| `kind` | Cognitive Services 계정의 API 이름입니다. |
| `name` | Cognitive Services 계정 이름입니다. |
| `sku` | Cognitive Services 계정의 SKU입니다.|
| `location` | 이 API를 호출할 위치 또는 지역입니다. 아래 목록에 있는 위치 중 하나를 선택합니다. |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

Azure Cloud Shell에서 다음 명령을 실행합니다. `[location]`은 나와 가까운 위치로 대체해야 합니다.

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--name ComputerVisionService \
--sku S1 \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--location [location]
```

> [!NOTE]
> 선택한 위치를 기억해 두세요. 이 위치에서 API에 대한 모든 호출을 수행하게 됩니다.

**ComputerVision** API에 대한 Cognitive Services 계정을 만들었습니다. *S1* sku를 선택하고 내 계정의 이름을 **ComputerVisionService**라고 지정했습니다. 계정은 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 이라는 리소스 그룹이 소유하며 `--location` 매개 변수에 설정한 위치에서 API를 호출합니다. 

명령을 통해 Cognitive Services 계정이 생성되면, JSON 응답을 받게 되며, 여기에는 **Succeeded**로 설정된 **provisioningState** 속성이 포함됩니다.

## <a name="get-an-access-key"></a>액세스 키 가져오기

계정이 성공적으로 만들어지면 이 계정에 대한 구독 키 또는 액세스 키를 검색할 수 있습니다.

1. Azure Cloud Shell에서 다음 명령을 실행합니다.

    ```azurecli
    az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
    ```
    
    위의 명령은 주어진 리소스 그룹이 소유하는 **ComputerVisionService**라는 Cognitive Services 계정과 연결된 키를 반환합니다. 두 가지 키가 반환되며 그 중 하나는 여분의 키입니다. 키는 기억하기 어려우니 첫 번째 키를 API에 대한 모든 호출에 사용할 변수에 저장하겠습니다.

2.  Azure Cloud Shell에서 다음 명령을 실행합니다.

    ```azurecli
    key=$(az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --query key1 -o tsv)
    ```
    
    Azure CLI 2.0은 `--query` 인수를 사용하여 명령의 결과에 대해 JMESPath 쿼리를 실행합니다. JMESPath는 JSON의 쿼리 언어이며, CLI 출력의 데이터를 선택하고 표시하는 기능을 제공합니다. 다른 표시 형식 전에 이러한 쿼리를 JSON 출력에서 실행합니다.
    `--query` 인수는 Azure CLI의 모든 명령에서 지원됩니다. 
    
    이 예제에서는 "key1" 항목에 대한 키 목록을 쿼리하고 그 결과를 **tsv** 형식으로 출력합니다. 이 형식은 문자열 값을 묶는 따옴표를 제거합니다. 결과는 변수 **키**에 할당합니다.
    
    > [!IMPORTANT]
    > 이 키는 모듈 전반에서 사용되기 때문에 변수 내에 저장하는 것이 좋습니다. 값을 잊어버리거나 변수에 대한 설정이 해제되면 명령을 다시 실행하여 변수를 설정합니다.  

3. 키의 값을 보려면 Azure Cloud Shell에서 다음 명령을 실행합니다.

    ```azurecli
    echo $key
    ```

계정과 키가 준비되었으면 API에 호출을 보낼 차례입니다.