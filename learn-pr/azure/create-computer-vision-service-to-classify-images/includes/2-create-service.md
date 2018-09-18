이 단원에서는 Azure CLI를 사용하여 Computer Vision API 서비스를 만듭니다.

# <a name="exercise-create-a-computer-vision-service"></a>연습: Computer Vision 서비스 만들기

[Computer Vision](/azure/cognitive-services/computer-vision/home)은 모든 사용자에게 서비스로 제공되는 완전한 기계 학습 알고리즘 집합인 [Azure Cognitive Services](/azure/cognitive-services/welcome)에 포함되어 있습니다. Microsoft에서는 처음부터 모델을 학습시키기에 충분한 데이터를 생성하지 않고 모든 사용자에게 미리 학습된 모델을 제공하고 있습니다.

사용 가능한 여러 서비스 중에 음성, 이미지, 비디오, 검색, 언어 등을 처리할 수 있는 서비스가 제공됩니다.

이 연습에서는 이미지를 처리하는 데 필요한 서비스를 만드는 작업을 중점적으로 진행하겠습니다. 이 연습을 마치나고 면 이미지 식별이 가능한 API 엔드포인트를 만들 수 있게 됩니다.

# <a name="create-a-computer-vision-api-service"></a>Computer Vision API 서비스 만들기

Computer Vision API 서비스를 만들려면 해당 서비스를 배포할 *리소스 그룹*이 필요합니다. 리소스 그룹은 모든 Azure 리소스가 배포 및 관리되는 논리적 컬렉션입니다.

```azurecli
az group create --name ComputerVisionRG --location westus2
```

리소스 그룹을 만든 후에는 `az cognitiveservices account create` 명령 및 서비스 이름을 사용하여 서비스를 만듭니다. 

```azurecli
az cognitiveservices account create --kind ComputerVision -l westus2 -n ComputerVisionService --sku F0 -g ComputerVisionRG
```
