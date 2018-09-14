<span data-ttu-id="cbae6-101">이제 이벤트 허브에 대한 게시자 및 소비자 응용 프로그램을 구성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-101">You're now ready to configure your publisher and consumer applications for your event hub.</span></span>

<span data-ttu-id="cbae6-102">이 연습에서는 이벤트 허브를 통해 메시지를 보내거나 받도록 이러한 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-102">In this exercise, you'll configure these applications to send or receive messages through your event hub.</span></span> <span data-ttu-id="cbae6-103">이러한 응용 프로그램은 GitHub 리포지토리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-103">These applications are stored in a GitHub repository.</span></span>

<span data-ttu-id="cbae6-104">두 개의 개별 응용 프로그램을 구성합니다. 하나는 메시지 발신자(**SimpleSend**)로 사용되고 다른 하나는 메시지 수신자(**EventProcessorSample**)로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-104">You'll configure two separate applications; one acts as the message sender (**SimpleSend**), the other as the message receiver (**EventProcessorSample**).</span></span> <span data-ttu-id="cbae6-105">이는 브라우저 내에서 모든 작업을 수행할 수 있는 Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-105">These are Java applications, which enable you to do everything within the browser.</span></span> <span data-ttu-id="cbae6-106">그러나 .NET과 같은 모든 플랫폼에 대한 동일한 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-106">However, the same configuration is needed for any platform, such as .NET.</span></span>

## <a name="create-a-general-purpose-standard-storage-account"></a><span data-ttu-id="cbae6-107">범용 표준 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cbae6-107">Create a general-purpose, standard storage account</span></span>

<span data-ttu-id="cbae6-108">이 단원에서 구성하는 Java 수신자 응용 프로그램은 Azure Blob Storage에 메시지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-108">The Java receiver application, that you'll configure in this unit, stores messages in Azure Blob Storage.</span></span> <span data-ttu-id="cbae6-109">Blob Storage를 사용하려면 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-109">Blob Storage requires a storage account.</span></span>

1. <span data-ttu-id="cbae6-110">다음 명령을 사용하여 리소스 그룹에서 저장소 계정(범용 V2)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-110">Create a storage account (general-purpose V2) in the resource group using the following command:</span></span>

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name>  --location <location> --sku Standard_RAGRS --encryption blob
    ```

    |<span data-ttu-id="cbae6-111">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cbae6-111">Parameter</span></span>      |<span data-ttu-id="cbae6-112">설명</span><span class="sxs-lookup"><span data-stu-id="cbae6-112">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="cbae6-113">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="cbae6-113">--name (required)</span></span>  |<span data-ttu-id="cbae6-114">저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-114">Enter a name for your storage account.</span></span>|
    |<span data-ttu-id="cbae6-115">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="cbae6-115">--resource-group (required)</span></span>  |<span data-ttu-id="cbae6-116">이전 단원에서 만든 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-116">Enter the resource group you created in the previous unit.</span></span>|
    |<span data-ttu-id="cbae6-117">--location(선택)</span><span class="sxs-lookup"><span data-stu-id="cbae6-117">--location (optional)</span></span>    |<span data-ttu-id="cbae6-118">이전 단원에서 리소스 그룹을 만드는 데 사용한 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-118">Enter the location you used to create your resource group in the previous unit.</span></span>|

1. <span data-ttu-id="cbae6-119">다음 명령을 사용하여 저장소 계정과 연결된 모든 액세스 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-119">List all the access keys associated with your storage account using the following command:</span></span>

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

    |<span data-ttu-id="cbae6-120">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cbae6-120">Parameter</span></span>      |<span data-ttu-id="cbae6-121">설명</span><span class="sxs-lookup"><span data-stu-id="cbae6-121">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="cbae6-122">--account-name(필수)</span><span class="sxs-lookup"><span data-stu-id="cbae6-122">--account-name (required)</span></span>  |<span data-ttu-id="cbae6-123">저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-123">Enter the name for your storage account.</span></span>|
    |<span data-ttu-id="cbae6-124">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="cbae6-124">--resource-group (required)</span></span>  |<span data-ttu-id="cbae6-125">이전 단원에서 만든 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-125">Enter the resource group you created in the previous unit.</span></span>|

     <span data-ttu-id="cbae6-126">저장소 계정과 연결된 액세스 키가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-126">Access keys associated with your storage account are listed.</span></span> <span data-ttu-id="cbae6-127">나중에 사용할 수 있도록 **key** 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-127">Copy and save the value of **key** for future use.</span></span> <span data-ttu-id="cbae6-128">저장소 계정에 액세스하려면 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-128">You'll need this key to access your storage account.</span></span>

1. <span data-ttu-id="cbae6-129">다음 명령을 사용하여 저장소 계정의 연결 문자열을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-129">View the connections string for your storage account using the following command:</span></span>

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

    |<span data-ttu-id="cbae6-130">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cbae6-130">Parameter</span></span>      |<span data-ttu-id="cbae6-131">설명</span><span class="sxs-lookup"><span data-stu-id="cbae6-131">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="cbae6-132">-n(필수)</span><span class="sxs-lookup"><span data-stu-id="cbae6-132">-n (required)</span></span>  |<span data-ttu-id="cbae6-133">저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-133">Enter the name for your storage account.</span></span>|
    |<span data-ttu-id="cbae6-134">-g(필수)</span><span class="sxs-lookup"><span data-stu-id="cbae6-134">-g (required)</span></span>  |<span data-ttu-id="cbae6-135">리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-135">Enter the name of your resource group.</span></span>|

    <span data-ttu-id="cbae6-136">이 명령은 저장소 계정의 연결 세부 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-136">This command returns the connection details for the storage account.</span></span> <span data-ttu-id="cbae6-137">**connectionString** 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-137">Copy and save the value of **connectionString**.</span></span>

1. <span data-ttu-id="cbae6-138">다음 명령을 사용하여 저장소 계정에서 **messages**라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-138">Create a container called **messages** in your storage account using the following command.</span></span> <span data-ttu-id="cbae6-139">이전 단계에서 복사한 **connectionString**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-139">Use the **connectionString** you copied in the previous step:</span></span>

    ```azurecli
    az storage container create -n messages --connection-string "<connection string>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a><span data-ttu-id="cbae6-140">Event Hubs GitHub 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="cbae6-140">Clone the Event Hubs GitHub repository</span></span>

<span data-ttu-id="cbae6-141">다음 단계를 사용하여 Event Hubs GitHub 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-141">Use the following steps to clone the Event Hubs GitHub repository.</span></span>

1. <span data-ttu-id="cbae6-142">Azure Cloud Shell(Bash)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-142">Sign in to Azure Cloud Shell (Bash).</span></span>

1. <span data-ttu-id="cbae6-143">이 연습에서 빌드할 응용 프로그램의 원본 파일은 [GitHub 리포지토리](https://github.com/Azure/azure-event-hubs)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-143">The source files for the applications that you'll build in this exercise are located in a [GitHub repository](https://github.com/Azure/azure-event-hubs).</span></span> <span data-ttu-id="cbae6-144">다음 명령을 사용하여 Cloud Shell의 홈 디렉터리에 있는지 확인한 후 이 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-144">Use the following commands to make sure that you are in your home directory in Cloud Shell, and then to clone this repository:</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    <span data-ttu-id="cbae6-145">리포지토리는 `/home/<username>/azure-event-hubs`에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-145">The repository is cloned to `/home/<username>/azure-event-hubs`.</span></span>

## <a name="use-nano-to-edit-simplesendjava"></a><span data-ttu-id="cbae6-146">nano를 사용하여 SimpleSend.java 편집</span><span class="sxs-lookup"><span data-stu-id="cbae6-146">Use nano to edit SimpleSend.java</span></span>

<span data-ttu-id="cbae6-147">**nano** 편집기를 사용하여 SimpleSend 응용 프로그램을 편집하고 Event Hubs 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-147">Use the **nano** editor to edit the SimpleSend application and add your Event Hubs namespace, event hub name, shared access policy name, and primary key.</span></span> <span data-ttu-id="cbae6-148">기본 명령은 편집기 창의 맨 아래에 표시됩니다. 이 단원에서는 Ctrl+O를 사용하여 편집한 내용을 작성하고 Enter 키를 눌러 출력 파일 이름을 확인한 다음, Ctrl+X를 사용하여 편집기를 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-148">The main commands are displayed at the bottom of the editor window; in this unit, you'll need to write out your edits using CTRL +O, and then ENTER to confirm the output file name, and exit the editor using CTRL +X.</span></span>

1. <span data-ttu-id="cbae6-149">다음 명령을 사용하여 **SimpleSend** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-149">Change to the **SimpleSend** folder using the following command:</span></span>

    ```azurecli
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. <span data-ttu-id="cbae6-150">다음 명령을 사용하여 **nano** 편집기에서 **SimpleSend.java** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-150">Open the **SimpleSend.java** file in the **nano** editor using the following command:</span></span>

    ```azurecli
    nano SimpleSend.java
    ```

1. <span data-ttu-id="cbae6-151">nano 편집기에서 다음 문자열을 찾아서 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-151">In the nano editor, locate and replace the following strings:</span></span>

    - <span data-ttu-id="cbae6-152">`"Your Event Hubs namespace name"`을 이벤트 허브 네임스페이스의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-152">`"Your Event Hubs namespace name"` with the name of your event hub namespace.</span></span>
    - <span data-ttu-id="cbae6-153">`"Your event hub"`를 이벤트 허브 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-153">`"Your event hub"` with the name of your event hub.</span></span>
    - <span data-ttu-id="cbae6-154">`"Your primary SAS key"`를 이전에 저장한 이벤트 허브 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-154">`"Your primary SAS key"` with the value of the **primaryKey** key for your event hub namespace that you saved earlier.</span></span>
    - <span data-ttu-id="cbae6-155">`"Your policy name"`을 **RootManageSharedAccessKey**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-155">`"Your policy name"` with **RootManageSharedAccessKey**.</span></span>
 
        <span data-ttu-id="cbae6-156">Event Hubs 네임스페이스를 만들 때 **RootManageSharedAccessKey**라는 256비트 SAS 키가 만들어지고, 여기에는 네임스페이스에 대해 전송, 수신 대기 및 관리 권한을 부여하는 연결된 기본 및 보조 키 쌍이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-156">When you create an Event Hubs namespace, a 256-bit SAS key called **RootManageSharedAccessKey** is created that has an associated pair of primary and secondary keys that grant send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="cbae6-157">이전 단원에서 Azure CLI 명령을 사용하여 키를 표시했고, Azure Portal의 Event Hubs 네임스페이스에 대한 **공유 액세스 정책** 페이지를 열어 이 키를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-157">In the previous unit, you displayed the key using an Azure CLI command, and you can also find this key by opening the **Shared access policies** page for your Event Hubs namespace in the Azure portal.</span></span>

    ![발신자 응용 프로그램에 대한 구성 세부 정보](../media-draft/5-sender-configure.png)

1. <span data-ttu-id="cbae6-159">다음 명령을 사용하여 **SimpleSend.java**를 저장하고 nano를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-159">Save **SimpleSend.java** using the following command, and exit nano:</span></span>

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-simplesendjava"></a><span data-ttu-id="cbae6-160">Maven을 사용하여 SimpleSend.java 빌드</span><span class="sxs-lookup"><span data-stu-id="cbae6-160">Use Maven to build SimpleSend.java</span></span>

<span data-ttu-id="cbae6-161">이제 **mvn** 명령을 사용하여 Java 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-161">You'll now build the Java application using **mvn** commands.</span></span>

1. <span data-ttu-id="cbae6-162">다음 명령을 사용하여 기본 **SimpleSend** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-162">Change to the main **SimpleSend** folder using the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. <span data-ttu-id="cbae6-163">다음 명령을 사용하여 Java SimpleSend 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-163">Build the Java SimpleSend application using the following command.</span></span> <span data-ttu-id="cbae6-164">이렇게 하면 응용 프로그램이 이벤트 허브에 대한 연결 세부 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-164">This ensures that your application  uses the connection details for your event hub:</span></span>

    ```azurecli
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="cbae6-165">빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-165">The build process may take several minutes to complete.</span></span> <span data-ttu-id="cbae6-166">계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-166">Ensure that you see the **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![발신자 응용 프로그램에 대한 빌드 결과](../media-draft/5-sender-build.png)

## <a name="use-nano-to-edit-eventprocessorsamplejava"></a><span data-ttu-id="cbae6-168">nano를 사용하여 EventProcessorSample.java 편집</span><span class="sxs-lookup"><span data-stu-id="cbae6-168">Use nano to edit EventProcessorSample.java</span></span>

<span data-ttu-id="cbae6-169">이벤트 허브에서 데이터를 수집하도록 **수신자**(**구독자** 또는 **소비자**라고도 함) 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-169">You'll now configure a **receiver** (also known as **subscribers** or **consumers**) application to ingest data from your event hub.</span></span>

<span data-ttu-id="cbae6-170">수신자 응용 프로그램의 경우 두 개의 메서드인 **EventHubReceiver** 및 **EventProcessorHost**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-170">For the receiver application, two methods are available; **EventHubReceiver** and **EventProcessorHost**.</span></span> <span data-ttu-id="cbae6-171">EventProcessorHost는 EventHubReceiver의 맨 위에 빌드되지만 EventHubReceiver보다 더 단순한 프로그래밍 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-171">EventProcessorHost is built on top of EventHubReceiver, but provides simpler programmatic interface than EventHubReceiver.</span></span> <span data-ttu-id="cbae6-172">EventProcessorHost는 동일한 저장소 계정을 사용하여 EventProcessorHost의 여러 인스턴스에서 자동으로 메시지 파티션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-172">EventProcessorHost can automatically distribute message partitions across multiple instances of EventProcessorHost using the same storage account.</span></span>

<span data-ttu-id="cbae6-173">이 단원에서는 EventProcessorHost 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-173">In this unit, you’ll use the EventProcessorHost method.</span></span> <span data-ttu-id="cbae6-174">다시 nano를 사용하고 EventProcessorSample 응용 프로그램을 편집하여 Event Hubs 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키, 저장소 계정 이름, 연결 문자열, 컨테이너 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-174">You'll again use nano, and edit the EventProcessorSample application to add your Event Hubs namespace, event hub name, shared access policy name and primary key, storage account name, connection string, and container name.</span></span>

1. <span data-ttu-id="cbae6-175">다음 명령을 사용하여 **EventProcessorSample** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-175">Change to the **EventProcessorSample** folder using the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. <span data-ttu-id="cbae6-176">다음 명령을 사용하여 **nano** 편집기에서 **EventProcessorSample.java** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-176">Open the **EventProcessorSample.java** file in the **nano** editor using the following command:</span></span>

    ```azurecli
    nano EventProcessorSample.java
    ```
1. <span data-ttu-id="cbae6-177">nano 편집기에서 다음 문자열을 찾아서 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-177">Locate and replace the following strings in the nano editor:</span></span>

    - <span data-ttu-id="cbae6-178">`----ServiceBusNamespaceName----`을 Event Hubs 네임스페이스 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-178">`----ServiceBusNamespaceName----` with the name of your Event Hubs namespace.</span></span>
    - <span data-ttu-id="cbae6-179">`----EventHubName----`를 이벤트 허브 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-179">`----EventHubName----` with the name of your event hub.</span></span>
    - <span data-ttu-id="cbae6-180">`----SharedAccessSignatureKeyName----`을 **RootManageSharedAccessKey**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-180">`----SharedAccessSignatureKeyName----` with **RootManageSharedAccessKey**.</span></span>
    - <span data-ttu-id="cbae6-181">`----SharedAccessSignatureKey----`를 이전에 저장한 Event Hubs 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-181">`----SharedAccessSignatureKey----` with the value of the **primaryKey** key for your Event Hubs namespace that you saved earlier.</span></span>
    - <span data-ttu-id="cbae6-182">`----AzureStorageConnectionString----`을 이전에 저장한 저장소 계정 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-182">`----AzureStorageConnectionString----` with your storage account connection string that you saved earlier.</span></span>
    - <span data-ttu-id="cbae6-183">`----StorageContainerName----`을 **messages**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-183">`----StorageContainerName----` with **messages**.</span></span>
    - <span data-ttu-id="cbae6-184">`----HostNamePrefix----`를 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-184">`----HostNamePrefix----` with the name of your storage account.</span></span>

    ![수신자 응용 프로그램에 대한 구성 세부 정보](../media-draft/5-receiver-configure.png)

1. <span data-ttu-id="cbae6-186">다음 명령을 사용하여 **EventProcessorSample.java**를 저장하고 nano를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-186">Save **EventProcessorSample.java** using the following command and exit nano:</span></span>

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-eventprocessorsamplejava"></a><span data-ttu-id="cbae6-187">Maven을 사용하여 EventProcessorSample.java 빌드</span><span class="sxs-lookup"><span data-stu-id="cbae6-187">Use Maven to build EventProcessorSample.java</span></span>

1. <span data-ttu-id="cbae6-188">다음 명령을 사용하여 기본 **EventProcessorSample** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-188">Change to the main **EventProcessorSample** folder using the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. <span data-ttu-id="cbae6-189">다음 명령을 사용하여 Java SimpleSend 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-189">Build the Java SimpleSend application using the following command.</span></span> <span data-ttu-id="cbae6-190">이렇게 하면 응용 프로그램이 이벤트 허브에 대한 연결 세부 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-190">This ensures that your application uses the connection details for your event hub:</span></span>

    ```azurecli
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="cbae6-191">빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-191">The build process may take several minutes to complete.</span></span> <span data-ttu-id="cbae6-192">계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-192">Ensure that you see a **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![수신자 응용 프로그램에 대한 빌드 결과](../media-draft/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a><span data-ttu-id="cbae6-194">발신자 및 수신자 앱 시작</span><span class="sxs-lookup"><span data-stu-id="cbae6-194">Start the sender and receiver apps</span></span>

1. <span data-ttu-id="cbae6-195">**java** 명령을 사용하고 .jar 패키지를 지정하여 명령줄에서 Java 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-195">Run Java application from the command line by using the **java** command, and specifying a .jar package.</span></span> <span data-ttu-id="cbae6-196">다음 명령을 사용하여 SimpleSend 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-196">Use the following commands to start the SimpleSend application:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="cbae6-197">**보내기 완료...** 가 표시되면 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-197">When you see **Send Complete...**, press ENTER.</span></span>

    ![발신자 응용 프로그램에 대한 실행 결과](../media-draft/5-sender-run.png)

1. <span data-ttu-id="cbae6-199">다음 명령을 사용하여 EventProcessorSample 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-199">Start the EventProcessorSample application using the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="cbae6-200">메시지가 콘솔에 표시되는 작업이 중지하면 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-200">When messages stop being displayed to the console, press ENTER.</span></span>

    ![수신자 응용 프로그램에 대한 실행 결과](../media-draft/5-receiver-run.png)

## <a name="summary"></a><span data-ttu-id="cbae6-202">요약</span><span class="sxs-lookup"><span data-stu-id="cbae6-202">Summary</span></span>

<span data-ttu-id="cbae6-203">이제 이벤트 허브로 메시지를 보낼 수 있도록 발신자 응용 프로그램이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-203">You've now configured a sender application ready to send messages to your event hub.</span></span> <span data-ttu-id="cbae6-204">이제 이벤트 허브에서 메시지를 받을 수 있도록 수신자 응용 프로그램이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbae6-204">You've also configured a receiver application ready to receive messages from your event hub.</span></span>
