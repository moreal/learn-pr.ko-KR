## <a name="get-an-access-key"></a>선택키 가져오기

아직 수행 하지 않았다면, 라는 변수에서 API 액세스 키를 저장 하는 Azure Cloud Shell에서 다음 명령을 실행 `key`합니다. 후속 호출에서이 변수를 사용 하겠습니다.

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
