## <a name="get-an-access-key"></a>선택키 가져오기

아직 수행하지 않은 경우에는 Azure Cloud Shell에서 다음 명령을 실행하여 API 액세스 키를 `key` 변수에 저장합니다. 이 변수는 후속 호출에서 사용됩니다.

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
