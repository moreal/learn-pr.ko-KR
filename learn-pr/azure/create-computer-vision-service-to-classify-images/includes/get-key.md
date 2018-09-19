## <a name="get-an-access-key"></a><span data-ttu-id="68fcf-101">선택키 가져오기</span><span class="sxs-lookup"><span data-stu-id="68fcf-101">Get an access key</span></span>

<span data-ttu-id="68fcf-102">아직 수행하지 않은 경우에는 Azure Cloud Shell에서 다음 명령을 실행하여 API 액세스 키를 `key` 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="68fcf-102">If you haven't done so already, run the following command in Azure Cloud Shell to store the API access key in a variable called `key`.</span></span> <span data-ttu-id="68fcf-103">이 변수는 후속 호출에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68fcf-103">We'll use this variable in subsequent calls.</span></span>

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
