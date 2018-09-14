
## <a name="what-is-microsoft-cognitive-services"></a>Microsoft Cognitive Services란?

Microsoft Cognitive Services는 집합의 기계 학습 알고리즘을 사용 하기 위한 서비스로 사용할 수 있습니다. 처음부터 응용 프로그램에 대 한 이러한 인텔리전스를 구축 하는 대신 시각, 음성, 언어, 지식 및 검색에 이러한 서비스를 사용할 수 있습니다. 각 서비스를 무료로 설치할 수 있습니다. 서비스를 앱에 통합 하려는 경우에 가입 하면 유료 구독 합니다. 집중 존경이 모델에서은 Computer Vision API입니다.

> [!TIP]
> 모든 Cognitive Services의 목록을 보려면 확인 합니다 [Cognitive Services 디렉토리](https://azure.microsoft.com/services/cognitive-services/directory/)합니다. 

## <a name="what-is-the-computer-vision-api"></a>Computer Vision API 란?

Computer Vision API는 이미지를 처리 하 고 정보를 반환 하는 알고리즘을 제공 합니다. 예를 들어 이미지 완성도 높은 콘텐츠가 또는 이미지의 모든 얼굴을 찾는 데 사용할 수 있습니다 하는 경우 찾을 수 있습니다. 또한 예측 지배적인 및 악센트 구분 색, 이미지의 콘텐츠를 분류, 전체 영어 문장 사용 하 여 이미지를 설명 하는 등 기능도 있습니다. 또한 큰 이미지를 효과적으로 표시 하는 것에 대 한 미리 보기 이미지도 지능적으로 생성할 수 있습니다.

> [!TIP]
> Computer Vision API 제품은 여러 지역에서 전 세계에 걸쳐입니다. 가장 가까운 지역에 참조를 [지역별 사용 가능한 제품](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all)합니다.

Computer Vision API를 사용할 수 있습니다.

- 정보에 대 한 이미지를 분석 합니다.
- OCR (광학 문자 인식)을 사용 하 여 이미지에서 인쇄 된 텍스트를 추출 합니다.
- 이미지에서 인쇄 및 필기 한 텍스트 인식
- 유명인 및 랜드마크 인식
- 비디오를 분석합니다 
- 이미지의 미리 보기를 생성 합니다. 

## <a name="how-to-call-the-computer-vision-api"></a>Computer Vision API를 호출 하는 방법

클라이언트 라이브러리 또는 REST API를 직접 사용 하 여 응용 프로그램에서 Computer Vision을 호출 합니다. 이 모듈에서는 REST API를 호출 합니다. 호출을 수행 합니다.

1. API 액세스 키 가져오기

    Computer Vision 서비스 계정에 등록할 때에 액세스 키를 할당 됩니다. 키의 헤더에 전달 해야 합니다 **마다** 요청 합니다. 

1. API에 대 한 POST 호출을 확인

    URL 형식을 다음과 같이 지정 합니다. **지역**.api.cognitive.microsoft.com/vision/v2.0/**resource**/**[매개 변수]** 

    - **지역** -예를 들어 계정의 만들 지역 *westus*합니다.
    - **리소스** -Computer Vision 리소스와 같은 호출 하는 `analyze`, `describe`, `generateThumbnail`를 `ocr`를 `models`를 `recognizeText`, `tag`합니다.

    원시 이미지 이진 파일 또는 이미지 URL로 처리 되도록 이미지를 제공할 수 있습니다.

    요청 헤더에는이 API에 대 한 액세스를 제공 하는 구독 키를 포함 해야 합니다.

1. 응답을 구문 분석

    Computer Vision API가 JSON 페이로드로 이미지에 대 한 정보를 포함 하는 응답 합니다.

My Computer Vision 구독을 만든 경우 가정해 보겠습니다를 `westus` 지역 및 API에 액세스 하려면 등록 키를 가져왔습니다. 키 값이 가상의 봅시다 `xxxx-xxxxx-xxxx-xxxx`합니다. 에 있는 이미지에 대 한 미리 보기를 생성 하려는 `http://example.com/images/test.jpg`합니다. 사용 하 여 `generateThumbnail`, 요청은 다음과 같습니다.

```
curl POST "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {xxxx-xxxxx-xxxx-xxxx}"
-d "{'url':'http://example.com/images/test.jpg'}"
```

이 모듈에서는 실행 Azure CLI에서 모든 연습 통합된 Cloud Shell을 사용 하 여. 살펴보겠습니다이 설치에 대 한 좀 더 제한 합니다.

## <a name="what-is-the-azure-cli"></a>Azure CLI는 무엇입니까

Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다. macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.

> [!IMPORTANT]
> Azure CLI 도구는 현재 Azure CLI 1.0 및 Azure CLI 2.0의 두 가지 버전이 있습니다. 레거시 스크립트를 실행하는 경우가 아니라면 최신 버전인 Azure CLI 2.0을 사용하는 것이 좋습니다. Azure CLI 1.0은 `azure` 명령으로 시작되고 Azure CLI 2.0은 `az` 명령으로 시작됩니다.

## <a name="az-cognitiveservices-commands"></a>az cognitiveservices 명령

Azure CLI를 포함 합니다 `cognitiveservices` Azure에서 Cognitive Services 계정을 관리 하는 명령입니다. 여러 하위 명령을 제공하여 특정 작업을 수행할 수 있습니다. 가장 일반적인 하위 명령은 다음과 같습니다.

| 하위 명령 | 설명 |
|-------------|-------------|
| `list` | 사용 가능한 Azure Cognitive Services 계정을 나열 합니다. |
| `account show` | Azure Cognitive Services 계정의 세부 정보를 가져옵니다. |
| `account create` | Azure Cognitive Services 계정을 만듭니다. |
| `account delete` | Azure Cognitive Services 계정을 삭제 합니다. |
| `keys list` | Azure Cognitive Services 계정의 키를 나열 합니다. |

Azure CLI를 사용 하 여 Cognitive Services를 만들어 보겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a>Cognitive Services 계정 만들기

Computer Vision API를 호출 하는 API 선택키가 필요 합니다. 액세스 키를 가져오려면 Computer Vision API에 대 한 Cognitive Services 계정이 필요 합니다. 사용 하 여 `az cognitiveservices create` 구독에는 계정을 만들 수 있습니다.

 이 명령은 `az cognitiveservices create` 리소스 그룹에서 Cognitive Services 계정을 만드는 데 사용 됩니다.  다음 5 개의 매개 변수는이 명령을 호출할 때 제공 되어야 합니다.

> [!Tip]
> Azure CLI 매개 변수에 대 한 대부분의 플래그는 단일 문자로 축약할 수 있습니다. 예를 들어 입력할 수 있습니다 `-l` 대신 `--location`합니다. 긴 형식인 명확성을 위해 사용 됩니다.

| 매개 변수 | 설명 |
|-----------|-------------|
| `resource-group` | Cognitive services 계정을 소유 하는 리소스 그룹. 이 대화형 샌드박스 세션에서는 <rgn>[샌드박스 리소스 그룹 이름]</rgn> |
| `kind` | Cognitive services 계정의 API 이름입니다. |
| `location` | 위치 또는이 API 호출 하려는 지역입니다. |
| `name` | Cognitive 서비스 계정 이름입니다. |
| `sku` | Cognitive services 계정의 Sku입니다.|

1. Azure Cloud Shell에서 다음 명령을 실행합니다.

> [!Tip]
> 이 단원에서는 Azure CLI 명령에는 가로 스크롤 크기를 줄이기 위해 여러 줄 명령을으로 기록 됩니다. 하려는 경우 이러한 명령은 한 줄 명령이 변환할 수 있습니다. 

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--location westus2 \
--name ComputerVisionService \
--sku F0 \
--resource-group <rgn>[Sandbox resource group name]</rgn>
```

에 대 한 cognitive services 계정을 만든 다음 합니다 **ComputerVision** API. 무료 sku를 선택 했습니다 *F0* 계좌 이라는 **ComputerVisionService**합니다. 리소스 그룹에서이 계정을 소유 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 에서 설정 된 위치에서 API를 호출할 수 있습니다 하 고는 `--location` 매개 변수입니다. 이 예에서는 westus2에서 호출할 수 있습니다. 다른 지역에서 호출 하면 오류가 발생 합니다.

JSON 응답을 포함 하는 명령을 cognitive services 계정 만들기가 완료 되 면 얻게 **provisioningState** 속성으로 설정 **Succeeded**합니다. 성공적인 응답의 모양은의 예는 다음과 같습니다.

<!-- TODO: find out the default location! -->

```json
{
  "endpoint": "https://westus2.api.cognitive.microsoft.com/vision/v2.0",
  "etag": "\"5c0070e5-0000-0000-0000-5b98cafa0000\"",
  "id": "/subscriptions/ae49d8aa-de86-418a-ba8c-4e9f3add2620/resourceGroups/ComputerVisionRG/providers/Microsoft.CognitiveServices/accounts/ComputerVisionService",
  "internalId": "437c9519bead47e6ba4b8e0842c1f76f",
  "kind": "ComputerVision",
  "location": "westus2",
  "name": "ComputerVisionService",
  "provisioningState": "Succeeded",
  "resourceGroup": "ComputerVisionRG",
  "sku": {
    "name": "F0",
    "tier": null
  },
  "tags": null,
  "type": "Microsoft.CognitiveServices/accounts"
}
```

> [!NOTE]
> 이미 Azure 구독에 Computer Vision cognitive services 계정을 사용 하 여 설정 합니다 **F0** Sku 하기 전에이 명령을 실행, 다음 메시지가 표시 됩니다.
>
> `Only one free account is allowed for account type 'ComputerVision'` 
>
> 이 모듈에 대 한 해당 계정을 사용 하거나에서 Sku를 변경 해야 합니다 `az cognitiveservices account create` 명령도 *S1* 또는 다른 Sku입니다.

## <a name="get-an-access-key"></a>선택키 가져오기

계좌 성공적으로 생성 되 면 구독 키를 검색 하거나이 계정에 대 한 키에 액세스할 수 있습니다.

1. Azure Cloud Shell에서 다음 명령을 실행합니다.

```azurecli
az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn>
```

위의 명령이 호출 cognitive services 계정과 연결 된 키를 반환 합니다. **ComputerVisionService**, 지정된 된 리소스 그룹에서 소유한 합니다. 두 키 반환-하나는 여분의 키입니다. 첫 번째 키 API에 대 한 모든 호출에 사용 되는 변수에 저장 하겠습니다 키는 기억 하기 어렵습니다.

2.  Azure Cloud Shell에서 다음 명령을 실행합니다.

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--query key1 -o tsv)
```

Azure CLI 2.0을 사용 하 여 `--query` 명령의 결과에 대해 JMESPath 쿼리를 실행 하는 인수입니다. JMESPath는 JSON의 쿼리 언어이며, CLI 출력의 데이터를 선택하고 표시하는 기능을 제공합니다. 이러한 쿼리는 모든 표시 서식을 지정 하기 전에 JSON 출력에서 실행 됩니다.
`--query` 인수는 Azure CLI의 모든 명령에서 지원됩니다. 

예제에서는 쿼리할 키 목록을 진입점 "key1" 라는 결과를 출력에 대 한 **tsv** 형식입니다. 이 형식은 문자열 값을 묶는 따옴표를 제거합니다. 결과 변수에 할당할 것 **키**합니다.

> [!IMPORTANT]
> 모듈 전체에서이 키를 사용 하 여 좋은 생각은 변수에 저장 하려고 합니다. 다시 명령을 실행 하는 값을 잊은 경우 변수의 해제 됩니다.  

3. 이 키의 값을 보려면 Azure Cloud Shell에서 다음 명령을 실행 합니다.

```azurecli
echo $key
```

이제는 계정 및 키를 한 API에 일부 호출을 수행 하는 시간입니다.