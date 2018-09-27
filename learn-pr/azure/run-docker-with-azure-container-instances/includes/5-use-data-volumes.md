<span data-ttu-id="c9fde-101">기본적으로 Azure Container Instances는 상태 비저장 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-101">By default, Azure Container Instances is stateless.</span></span> <span data-ttu-id="c9fde-102">컨테이너의 작동이 중단되거나 중지되면 모든 상태가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-102">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="c9fde-103">컨테이너 수명이 지난 후에도 상태를 유지하려면 외부 저장소의 볼륨을 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-103">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span>

<span data-ttu-id="c9fde-104">여기에서는 데이터 저장 및 검색을 위해 Azure Container Instance에 Azure 파일 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-104">Here, you will mount an Azure file share to an Azure container instance for data storage and retrieval.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="c9fde-105">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="c9fde-105">Create an Azure file share</span></span>

<span data-ttu-id="c9fde-106">다음 스크립트를 실행하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-106">Run the following script to create a storage account.</span></span> <span data-ttu-id="c9fde-107">저장소 계정 이름은 글로벌로 고유해야 하므로 이 스크립트는 기준 문자열에 임의 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-107">The storage account name must be globally unique, so the script adds a random value to the base string:</span></span>

```azurecli
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM

az storage account create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --sku Standard_LRS \
    --location eastus
```

<span data-ttu-id="c9fde-108">다음 명령을 실행하여 저장소 계정 연결 문자열을 *AZURE_STORAGE_CONNECTION_STRING*이라는 환경 변수에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-108">Run the following command to place the storage account connection string into an environment variable named *AZURE_STORAGE_CONNECTION_STRING*.</span></span> <span data-ttu-id="c9fde-109">이 환경 변수는 Azure CLI에서 인식되며 저장소 관련 작업에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-109">This environment variable is understood by the Azure CLI and can be used in storage-related operations:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=$(az storage account show-connection-string --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACI_PERS_STORAGE_ACCOUNT_NAME --output tsv)
```

<span data-ttu-id="c9fde-110">`az storage share create` 명령을 실행하여 저장소 계정에 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-110">Create a file share in the storage account by running the `az storage share create` command.</span></span> <span data-ttu-id="c9fde-111">다음 예제에서는 *aci-share-demo*라는 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-111">The following example creates a share with the name *aci-share-demo*:</span></span>

```azurecli
az storage share create --name aci-share-demo
```

## <a name="get-storage-credentials"></a><span data-ttu-id="c9fde-112">저장소 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="c9fde-112">Get storage credentials</span></span>

<span data-ttu-id="c9fde-113">Azure Container Instances의 볼륨으로 Azure 파일 공유를 탑재하려면 저장소 계정 이름, 공유 이름, 저장소 계정 액세스 키라는 세 가지 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage account access key.</span></span>

<span data-ttu-id="c9fde-114">위의 스크립트를 사용한 경우 끝에 임의 값이 포함된 저장소 계정 이름이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="c9fde-115">임의 값 부분을 포함한 최종 문자열을 쿼리하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli
STORAGE_ACCOUNT=$(az storage account list --resource-group <rgn>[sandbox resource group name]</rgn> --query "[?contains(name,'$ACI_PERS_STORAGE_ACCOUNT_NAME')].[name]" --output tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="c9fde-116">공유 이름은 이미 확인되었으므로(aci-share-demo) 저장소 계정 키만 확인하면 됩니다. 다음 명령을 사용하면 키를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-116">The share name is already known (aci-share-demo), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list --resource-group <rgn>[sandbox resource group name]</rgn> --account-name $STORAGE_ACCOUNT --query "[0].value" --output tsv)
echo $STORAGE_KEY
```

## <a name="deploy-container-and-mount-volume"></a><span data-ttu-id="c9fde-117">컨테이너 배포 및 볼륨 탑재</span><span class="sxs-lookup"><span data-stu-id="c9fde-117">Deploy container and mount volume</span></span>

<span data-ttu-id="c9fde-118">Azure 파일 공유를 컨테이너의 볼륨으로 탑재하려면 컨테이너를 만들 때 공유 및 볼륨 탑재 지점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-118">To mount an Azure file share as a volume in a container, specify the share and volume mount point when you create the container:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --image microsoft/aci-hellofiles \
    --location eastus \
    --ports 80 \
    --ip-address Public \
    --azure-file-volume-account-name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --azure-file-volume-account-key $STORAGE_KEY \
    --azure-file-volume-share-name aci-share-demo \
    --azure-file-volume-mount-path /aci/logs/
```

<span data-ttu-id="c9fde-119">컨테이너가 만들어지면 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-119">Once the container has been created, get the public IP address:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --query ipAddress.ip \
    --output tsv
```

<span data-ttu-id="c9fde-120">브라우저를 열고 컨테이너 IP 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-120">Open a browser and navigate to the container's IP address.</span></span> <span data-ttu-id="c9fde-121">간단한 양식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-121">You will be presented with a simple form.</span></span> <span data-ttu-id="c9fde-122">텍스트를 입력하고 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-122">Enter some text and click **Submit**.</span></span> <span data-ttu-id="c9fde-123">이 작업을 수행하면 Azure Files 공유에 입력된 텍스트를 포함하는 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-123">This action will create a file in the Azure Files share containing the entered text.</span></span>

![Azure Container Instances 파일 공유 데모](../media/5-files-ui.png)

<span data-ttu-id="c9fde-125">유효성을 검사하려면 Azure Portal에서 파일 공유로 이동한 후 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-125">To validate, you can navigate to the file share in the Azure portal and download the file.</span></span>

1. <span data-ttu-id="c9fde-126">파일 이름 확인</span><span class="sxs-lookup"><span data-stu-id="c9fde-126">Get the filename</span></span>

    ```azurecli
    az storage file list -s aci-share-demo -o table
    ```

1. <span data-ttu-id="c9fde-127">파일을 다운로드하고 아래에서 `<filename>`을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-127">Download it, make sure to replace the `<filename>` below.</span></span>

    ```azurecli
    az storage file download -s aci-share-demo -n <filename>
    ```
    
![콘텐츠 데모 응용 프로그램이 있는 샘플 텍스트 파일](../media/5-sample-text.png)

<span data-ttu-id="c9fde-129">Azure Files 공유에 저장된 파일과 데이터가 임의의 값인 경우 상태 저장 데이터를 제공하기 위해 새 컨테이너 인스턴스에 이 공유를 다시 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9fde-129">If the files and data stored in the Azure Files share were of any value, this share could be remounted on a new container instance to provide stateful data.</span></span>