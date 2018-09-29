<span data-ttu-id="615df-101">이제 Event Hub에 대한 게시자 및 소비자 응용 프로그램을 구성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-101">You're now ready to configure your publisher and consumer applications for your Event Hub.</span></span>

<span data-ttu-id="615df-102">이 단원에서는 Event Hub를 통해 메시지를 보내거나 받도록 이러한 응용 프로그램을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-102">In this unit, you'll configure these applications to send or receive messages through your Event Hub.</span></span> <span data-ttu-id="615df-103">이러한 응용 프로그램은 GitHub 리포지토리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-103">These applications are stored in a GitHub repository.</span></span>

<span data-ttu-id="615df-104">두 개의 개별 응용 프로그램을 구성합니다. 하나는 메시지 발신자(**SimpleSend**)로 사용되고 다른 하나는 메시지 수신자(**EventProcessorSample**)로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-104">You'll configure two separate applications; one acts as the message sender (**SimpleSend**), the other as the message receiver (**EventProcessorSample**).</span></span> <span data-ttu-id="615df-105">이는 브라우저 내에서 모든 작업을 수행할 수 있는 Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="615df-105">These are Java applications, which enable you to do everything within the browser.</span></span> <span data-ttu-id="615df-106">그러나 .NET과 같은 모든 플랫폼에 대한 동일한 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-106">However, the same configuration is needed for any platform, such as .NET.</span></span>

## <a name="create-a-general-purpose-standard-storage-account"></a><span data-ttu-id="615df-107">범용 표준 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="615df-107">Create a general-purpose, standard storage account</span></span>

<span data-ttu-id="615df-108">이 단원에서 구성하는 Java 수신자 응용 프로그램은 Azure Blob Storage에 메시지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-108">The Java receiver application, that you'll configure in this unit, stores messages in Azure Blob Storage.</span></span> <span data-ttu-id="615df-109">Blob Storage를 사용하려면 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-109">Blob Storage requires a storage account.</span></span>

1. <span data-ttu-id="615df-110">`storage account create` 명령을 사용하여 저장소 계정(범용 V2)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="615df-110">Create a storage account (general-purpose V2) using the `storage account create` command.</span></span> <span data-ttu-id="615df-111">기본 리소스 그룹 및 위치를 설정했으므로 해당 매개 변수가 일반적으로 _필요_하더라도 해제한 상태로 유지해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-111">Remember we set a default resource group and location, so even though those parameters are normally _required_, we can leave them off.</span></span>

    |<span data-ttu-id="615df-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="615df-112">Parameter</span></span>      |<span data-ttu-id="615df-113">설명</span><span class="sxs-lookup"><span data-stu-id="615df-113">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="615df-114">--name(필수)</span><span class="sxs-lookup"><span data-stu-id="615df-114">--name (required)</span></span>  | <span data-ttu-id="615df-115">저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="615df-115">A name for your storage account.</span></span> |
    |<span data-ttu-id="615df-116">--resource-group(필수)</span><span class="sxs-lookup"><span data-stu-id="615df-116">--resource-group (required)</span></span>  |<span data-ttu-id="615df-117">리소스 그룹 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="615df-117">The resource group owner.</span></span> <span data-ttu-id="615df-118">미리 생성된 샌드박스 리소스 그룹을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-118">We'll use the pre-created sandbox resource group.</span></span>|
    |<span data-ttu-id="615df-119">--location(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="615df-119">--location (optional)</span></span>    |<span data-ttu-id="615df-120">특정 위치 및 리소스 그룹 위치에서 저장소 계정을 사용하려는 경우 선택 사항 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="615df-120">An optional location if you want the storage account in a specific place vs. the resource group location.</span></span>|

    <span data-ttu-id="615df-121">저장소 계정 이름을 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-121">Set the storage account name into a variable.</span></span> <span data-ttu-id="615df-122">하이픈 구분 기호가 허용되고 모든 소문자, 숫자로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-122">It must be composed of all lower-case letters, numbers, with hyphen separators allowed.</span></span> <span data-ttu-id="615df-123">또한 Azure 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-123">It also must be unique within Azure.</span></span>

    ```azurecli
    STORAGE_NAME=[name]
    ```

    <span data-ttu-id="615df-124">그런 다음, 이 명령을 사용하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="615df-124">Then use this command to create the storage account.</span></span>

    ```azurecli
    az storage account create --name $STORAGE_NAME --sku Standard_RAGRS --encryption blob
    ```

    > [!TIP]
    > <span data-ttu-id="615df-125">저장소 계정 만들기에 실패하면 환경 변수를 변경하고 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="615df-125">If the storage account creation fails, change your environment variable and try again.</span></span>

1. <span data-ttu-id="615df-126">`account keys list` 명령을 사용하여 저장소 계정과 연결된 모든 액세스 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-126">List all the access keys associated with your storage account using the `account keys list` command.</span></span> <span data-ttu-id="615df-127">사용자 계정 이름 및 리소스 그룹을 사용합니다(기본 설정됨).</span><span class="sxs-lookup"><span data-stu-id="615df-127">It takes your account name and the resource group (which is defaulted).</span></span>

    ```azurecli
    az storage account keys list --account-name $STORAGE_NAME
    ```

     <span data-ttu-id="615df-128">저장소 계정과 연결된 액세스 키가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-128">Access keys associated with your storage account are listed.</span></span> <span data-ttu-id="615df-129">나중에 사용할 수 있도록 **key** 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-129">Copy and save the value of **key** for future use.</span></span> <span data-ttu-id="615df-130">저장소 계정에 액세스하려면 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-130">You'll need this key to access your storage account.</span></span>

1. <span data-ttu-id="615df-131">다음 명령을 사용하여 저장소 계정의 연결 문자열을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="615df-131">View the connections string for your storage account using the following command:</span></span>

    ```azurecli
    az storage account show-connection-string -n $STORAGE_NAME
    ```

    <span data-ttu-id="615df-132">이 명령은 저장소 계정의 연결 세부 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-132">This command returns the connection details for the storage account.</span></span> <span data-ttu-id="615df-133">**connectionString** _값_을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-133">Copy and save the _value_ of **connectionString**.</span></span> <span data-ttu-id="615df-134">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-134">It should look something like:</span></span>

    ```output
    "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=storage_account_name;AccountKey=VZjXuMeuDqjCkT60xX6L5fmtXixYuY2wiPmsrXwYHIhwo736kSAUAj08XBockRZh7CZwYxuYBPe31hi8XfHlWw=="
    ```

1. 다음 명령을 사용하여 저장소 계정에서 **messages**라는 컨테이너를 만듭니다. <span data-ttu-id="615df-136">이전 단계에서 복사한 **connectionString**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-136">Use the **connectionString** you copied in the previous step:</span></span>

    ```azurecli
    az storage container create -n messages --connection-string "<connection string here>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a><span data-ttu-id="615df-137">Event Hubs GitHub 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="615df-137">Clone the Event Hubs GitHub repository</span></span>

<span data-ttu-id="615df-138">`git`를 사용하여 Event Hubs GitHub 리포지토리를 복제하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-138">Use the following steps to clone the Event Hubs GitHub repository with `git`.</span></span> <span data-ttu-id="615df-139">이 권한을 Cloud Shell에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-139">You can execute this right in the Cloud Shell.</span></span>

1. <span data-ttu-id="615df-140">이 단원에서 빌드할 응용 프로그램의 원본 파일은 [GitHub 리포지토리](https://github.com/Azure/azure-event-hubs)에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-140">The source files for the applications that you'll build in this unit are located in a [GitHub repository](https://github.com/Azure/azure-event-hubs).</span></span> <span data-ttu-id="615df-141">다음 명령을 사용하여 Cloud Shell의 홈 디렉터리에 있는지 확인한 다음, 다음 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-141">Use the following commands to make sure that you are in your home directory in Cloud Shell, and then to clone this repository:</span></span>

    ```bash
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    <span data-ttu-id="615df-142">리포지토리는 홈 폴더에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-142">The repository is cloned to your home folder.</span></span>

## <a name="edit-simplesendjava"></a><span data-ttu-id="615df-143">SimpleSend.java 편집</span><span class="sxs-lookup"><span data-stu-id="615df-143">Edit SimpleSend.java</span></span>

<span data-ttu-id="615df-144">기본 제공 Cloud Shell 코드 편집기를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-144">We're going to use the built-in Cloud Shell Code editor.</span></span> <span data-ttu-id="615df-145">Monaco 편집기를 기반으로 하며, Visual Studio Code와 비슷하지만 완전히 온라인 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="615df-145">This is based on the Monaco editor and is similar to Visual Studio Code, but completely online.</span></span>

<span data-ttu-id="615df-146">편집기를 사용하여 SimpleSend 응용 프로그램을 수정하고 Event Hubs 네임스페이스, Event Hub 이름, 공유 액세스 정책 이름 및 기본 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-146">We'll use the editor to modify the SimpleSend application and add your Event Hubs namespace, Event Hub name, shared access policy name, and primary key.</span></span> <span data-ttu-id="615df-147">주요 명령은 편집기 창의 맨 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-147">The main commands are displayed at the bottom of the editor window.</span></span> 

<span data-ttu-id="615df-148"><kbd>Ctrl+O</kbd>를 사용하여 편집한 내용을 작성한 다음, <kbd>ENTER</kbd> 키를 눌러 출력 파일 이름을 확인하고, <kbd>Ctrl+X</kbd>를 사용하여 편집기를 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-148">You'll need to write out your edits using <kbd>Ctrl+O</kbd>, and then <kbd>ENTER</kbd> to confirm the output file name, and exit the editor using <kbd>Ctrl+X</kbd>.</span></span> <span data-ttu-id="615df-149">편집기에는 모든 편집 명령의 위쪽/오른쪽 모서리에서 "..." 메뉴도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-149">Alternatively, the editor has a "..." menu in the top/right corner for all the editing commands.</span></span>

1. <span data-ttu-id="615df-150">**SimpleSend** 폴더로 변경합니다</span><span class="sxs-lookup"><span data-stu-id="615df-150">Change to the **SimpleSend** folder.</span></span>

    ```bash
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. <span data-ttu-id="615df-151">현재 폴더에서 코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="615df-151">Open the code editor in the current folder.</span></span> <span data-ttu-id="615df-152">그러면 왼쪽에 있는 파일의 목록 및 오른쪽에 있는 편집기 공간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-152">This will show a list of files on the left and an editor space on the right.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="615df-153">파일 목록에서 **SimpleSend.java** 파일을 선택하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="615df-153">Open the **SimpleSend.java** file by selecting it from the file list.</span></span>

1. <span data-ttu-id="615df-154">편집기에서 다음 문자열을 찾아서 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-154">In the editor, locate and replace the following strings:</span></span>

    - <span data-ttu-id="615df-155">`"Your Event Hubs namespace name"`을 Event Hub 네임스페이스의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-155">`"Your Event Hubs namespace name"` with the name of your Event Hub namespace.</span></span>
    - <span data-ttu-id="615df-156">`"Your Event Hub"`를 Event Hub 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-156">`"Your Event Hub"` with the name of your Event Hub.</span></span>
    - <span data-ttu-id="615df-157">`"Your policy name"`을 **RootManageSharedAccessKey**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-157">`"Your policy name"` with **RootManageSharedAccessKey**.</span></span>
    - <span data-ttu-id="615df-158">`"Your primary SAS key"`를 이전에 저장한 Event Hub 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-158">`"Your primary SAS key"` with the value of the **primaryKey** key for your Event Hub namespace that you saved earlier.</span></span>
 
    > [!TIP]
    > <span data-ttu-id="615df-159">터미널 창과 달리 편집기는 OS에서 일반적인 복사/붙여넣기 키보드 액셀러레이터 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-159">Unlike the terminal window, the editor can use typical copy/paste keyboard accelerator keys for your OS.</span></span>

    <span data-ttu-id="615df-160">일부 작업을 잊은 경우 편집기 아래에 있는 터미널 창으로 전환하고 `echo` 명령을 사용하여 환경 변수 중 하나를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-160">If you've forgotten some of them, you can switch down to the terminal window below the editor and use the `echo` command to list out one of the environment variables.</span></span> <span data-ttu-id="615df-161">예:</span><span class="sxs-lookup"><span data-stu-id="615df-161">For example:</span></span>

    ```bash
    echo $NS_NAME
    ```
    <span data-ttu-id="615df-162">Event Hubs 네임스페이스를 만들 때 **RootManageSharedAccessKey**라는 256비트 SAS 키가 만들어지고, 여기에는 네임스페이스에 대해 전송, 수신 대기 및 관리 권한을 부여하는 연결된 기본 키 및 보조 키 쌍이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="615df-162">When you create an Event Hubs namespace, a 256-bit SAS key called **RootManageSharedAccessKey** is created that has an associated pair of primary and secondary keys that grant send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="615df-163">이전 단원에서 Azure CLI 명령을 사용하여 키를 표시했으므로 Azure Portal의 Event Hubs 네임스페이스에 대한 **공유 액세스 정책** 페이지를 열어 이 키를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-163">In the previous unit, you displayed the key using an Azure CLI command, and you can also find this key by opening the **Shared access policies** page for your Event Hubs namespace in the Azure portal.</span></span>

1. <span data-ttu-id="615df-164">"..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 **SimpleSend.java**를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-164">Save **SimpleSend.java** either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="615df-165">"..." 메뉴 또는 액셀러레이터 키(<kbd>CTRL+Q</kbd>)를 통해 편집기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-165">Close the editor through the "..." menu, or the accelerator key <kbd>CTRL+Q</kbd>.</span></span>

## <a name="use-maven-to-build-simplesendjava"></a><span data-ttu-id="615df-166">Maven을 사용하여 SimpleSend.java 빌드</span><span class="sxs-lookup"><span data-stu-id="615df-166">Use Maven to build SimpleSend.java</span></span>

<span data-ttu-id="615df-167">이제 **mvn** 명령을 사용하여 Java 응용 프로그램을 빌드하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-167">You'll now build the Java application using **mvn** commands.</span></span>

1. <span data-ttu-id="615df-168">기본 **SimpleSend** 폴더로 다시 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-168">Change back to the main **SimpleSend** folder.</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. <span data-ttu-id="615df-169">Java SimpleSend 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-169">Build the Java SimpleSend application.</span></span> <span data-ttu-id="615df-170">이렇게 하면 응용 프로그램이 Event Hub에 대한 연결 세부 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-170">This ensures that your application  uses the connection details for your Event Hub:</span></span>

    ```bash
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="615df-171">빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-171">The build process may take several minutes to complete.</span></span> <span data-ttu-id="615df-172">계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-172">Ensure that you see the **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![발신자 응용 프로그램에 대한 빌드 결과](../media/5-sender-build.png)

## <a name="edit-eventprocessorsamplejava"></a><span data-ttu-id="615df-174">EventProcessorSample.java 편집</span><span class="sxs-lookup"><span data-stu-id="615df-174">Edit EventProcessorSample.java</span></span>

<span data-ttu-id="615df-175">Event Hub에서 데이터를 수집하도록 **수신자**(**구독자** 또는 **소비자**라고도 함) 응용 프로그램을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-175">You'll now configure a **receiver** (also known as **subscribers** or **consumers**) application to ingest data from your Event Hub.</span></span>

<span data-ttu-id="615df-176">수신자 응용 프로그램의 경우 **EventHubReceiver** 및 **EventProcessorHost**라는 두 개의 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-176">For the receiver application, two methods are available; **EventHubReceiver** and **EventProcessorHost**.</span></span> <span data-ttu-id="615df-177">EventProcessorHost는 EventHubReceiver의 맨 위에 빌드되지만 EventHubReceiver보다 더 단순한 프로그래밍 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-177">EventProcessorHost is built on top of EventHubReceiver, but provides simpler programmatic interface than EventHubReceiver.</span></span> <span data-ttu-id="615df-178">EventProcessorHost는 동일한 저장소 계정을 사용하여 EventProcessorHost의 여러 인스턴스에서 자동으로 메시지 파티션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-178">EventProcessorHost can automatically distribute message partitions across multiple instances of EventProcessorHost using the same storage account.</span></span>

<span data-ttu-id="615df-179">이 단원에서는 EventProcessorHost 메서드를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-179">In this unit, you’ll use the EventProcessorHost method.</span></span> <span data-ttu-id="615df-180">EventProcessorSample 응용 프로그램을 편집하여 Event Hubs 네임스페이스, Event Hub 이름, 공유 액세스 정책 이름 및 기본 키, 저장소 계정 이름, 연결 문자열, 컨테이너 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-180">You'll edit the EventProcessorSample application to add your Event Hubs namespace, Event Hub name, shared access policy name and primary key, storage account name, connection string, and container name.</span></span>

1. <span data-ttu-id="615df-181">다음 명령을 사용하여 **EventProcessorSample** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-181">Change to the **EventProcessorSample** folder using the following command:</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. <span data-ttu-id="615df-182">코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="615df-182">Open the code editor.</span></span>

    ```bash
    code .
    ```
    
1. <span data-ttu-id="615df-183">**EventProcessorSample.java** 파일을 선택합니다</span><span class="sxs-lookup"><span data-stu-id="615df-183">Select the **EventProcessorSample.java** file.</span></span>

1. <span data-ttu-id="615df-184">편집기에서 다음 문자열을 찾아서 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-184">Locate and replace the following strings in the editor:</span></span>

    - <span data-ttu-id="615df-185">`----ServiceBusNamespaceName----`을 Event Hubs 네임스페이스 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-185">`----ServiceBusNamespaceName----` with the name of your Event Hubs namespace.</span></span>
    - <span data-ttu-id="615df-186">`----EventHubName----`를 Event Hub 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-186">`----EventHubName----` with the name of your Event Hub.</span></span>
    - <span data-ttu-id="615df-187">`----SharedAccessSignatureKeyName----`을 **RootManageSharedAccessKey**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-187">`----SharedAccessSignatureKeyName----` with **RootManageSharedAccessKey**.</span></span>
    - <span data-ttu-id="615df-188">`----SharedAccessSignatureKey----`를 이전에 저장한 Event Hubs 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-188">`----SharedAccessSignatureKey----` with the value of the **primaryKey** key for your Event Hubs namespace that you saved earlier.</span></span>
    - <span data-ttu-id="615df-189">`----AzureStorageConnectionString----`을 이전에 저장한 저장소 계정 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-189">`----AzureStorageConnectionString----` with your storage account connection string that you saved earlier.</span></span>
    - <span data-ttu-id="615df-190">`----StorageContainerName----`을 **messages**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-190">`----StorageContainerName----` with **messages**.</span></span>
    - <span data-ttu-id="615df-191">`----HostNamePrefix----`를 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="615df-191">`----HostNamePrefix----` with the name of your storage account.</span></span>

1. <span data-ttu-id="615df-192">"..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 **EventProcessorSample.java**를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-192">Save **EventProcessorSample.java** either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="615df-193">편집기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-193">Close the editor.</span></span>

## <a name="use-maven-to-build-eventprocessorsamplejava"></a><span data-ttu-id="615df-194">Maven을 사용하여 EventProcessorSample.java 빌드</span><span class="sxs-lookup"><span data-stu-id="615df-194">Use Maven to build EventProcessorSample.java</span></span>

1. <span data-ttu-id="615df-195">다음 명령을 사용하여 기본 **EventProcessorSample** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-195">Change to the main **EventProcessorSample** folder using the following command:</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. <span data-ttu-id="615df-196">다음 명령을 사용하여 Java SimpleSend 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-196">Build the Java SimpleSend application using the following command.</span></span> <span data-ttu-id="615df-197">이렇게 하면 응용 프로그램이 Event Hub에 대한 연결 세부 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-197">This ensures that your application uses the connection details for your Event Hub:</span></span>

    ```bash
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="615df-198">빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-198">The build process may take several minutes to complete.</span></span> <span data-ttu-id="615df-199">계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-199">Ensure that you see a **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![수신자 응용 프로그램에 대한 빌드 결과](../media/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a><span data-ttu-id="615df-201">발신자 및 수신자 앱 시작</span><span class="sxs-lookup"><span data-stu-id="615df-201">Start the sender and receiver apps</span></span>

1. <span data-ttu-id="615df-202">**java** 명령을 사용하고 .jar 패키지를 지정하여 명령줄에서 Java 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-202">Run Java application from the command line by using the **java** command, and specifying a .jar package.</span></span> <span data-ttu-id="615df-203">다음 명령을 사용하여 SimpleSend 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-203">Use the following commands to start the SimpleSend application:</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="615df-204">**보내기 완료...** 가 표시되면 <kbd>ENTER</kbd> 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="615df-204">When you see **Send Complete...**, press <kbd>ENTER</kbd>.</span></span>

    ```output
    jar-with-dependencies.jar
    SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    SLF4J: Defaulting to no-operation (NOP) logger implementation
    SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    2018-09-18T19:42:15.146Z: Send Complete...
    ```

1. <span data-ttu-id="615df-205">다음 명령을 사용하여 EventProcessorSample 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-205">Start the EventProcessorSample application using the following command.</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="615df-206">메시지가 콘솔에 표시되지 않으면 <kbd>ENTER</kbd> 키나 <kbd>CTRL+C</kbd>를 눌러서 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="615df-206">When messages stop being displayed to the console, press <kbd>ENTER</kbd> or <kbd>CTRL+C</kbd> to end the program.</span></span>

    ```output
    ...
    SAMPLE: Partition 0 checkpointing at 1064,19
    SAMPLE (3,1120,20): "Message 80"
    SAMPLE (3,1176,21): "Message 84"
    SAMPLE (3,1232,22): "Message 88"
    SAMPLE (3,1288,23): "Message 92"
    SAMPLE (3,1344,24): "Message 96"
    SAMPLE: Partition 3 checkpointing at 1344,24
    SAMPLE (2,1120,20): "Message 83"
    SAMPLE (2,1176,21): "Message 87"
    SAMPLE (2,1232,22): "Message 91"
    SAMPLE (2,1288,23): "Message 95"
    SAMPLE (2,1344,24): "Message 99"
    SAMPLE: Partition 2 checkpointing at 1344,24
    SAMPLE: Partition 1 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE (0,1120,20): "Message 81"
    SAMPLE (0,1176,21): "Message 85"
    SAMPLE: Partition 0 batch size was 10 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 got event batch
    SAMPLE (0,1232,22): "Message 89"
    SAMPLE (0,1288,23): "Message 93"
    SAMPLE (0,1344,24): "Message 97"
    SAMPLE: Partition 0 checkpointing at 1344,24
    SAMPLE: Partition 3 batch size was 8 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 2 batch size was 9 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    ```

## <a name="summary"></a><span data-ttu-id="615df-207">요약</span><span class="sxs-lookup"><span data-stu-id="615df-207">Summary</span></span>

<span data-ttu-id="615df-208">이제 Event Hub로 메시지를 보낼 수 있도록 발신자 응용 프로그램이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-208">You've now configured a sender application ready to send messages to your Event Hub.</span></span> <span data-ttu-id="615df-209">이제 Event Hub에서 메시지를 받을 수 있도록 수신자 응용 프로그램이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="615df-209">You've also configured a receiver application ready to receive messages from your Event Hub.</span></span>