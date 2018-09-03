<span data-ttu-id="020c8-101">사진작가로서 그날그날의 사진을 게시하는 웹 사이트를 가지고 있다고 상상해 보세요.</span><span class="sxs-lookup"><span data-stu-id="020c8-101">Imagine you're a photographer and you have a website where you display your pictures of the day.</span></span> <span data-ttu-id="020c8-102">바빠서 사진 업로드 일정이 일관되지 않지만, 사진을 올리면 팬에게 알림을 보내고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-102">Because you're busy, you don't have a consistent upload schedule, but you want to notify your fans when you upload a picture.</span></span> <span data-ttu-id="020c8-103">Azure Storage Blob 컨테이너에 이미지를 업로드할 때마다 자동으로 트윗을 전송하도록 하는 Azure 함수를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-103">You decide to create an Azure function to automatically send a tweet whenever you upload an image to your Azure Storage blob container.</span></span>

<span data-ttu-id="020c8-104">여기서는 Blob 트리거를 만들고 Azure Storage Blob 컨테이너 내 특정 위치를 모니터링하도록 이 트리거에 지시하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-104">Here, you learn how to create a blob trigger and instruct it to monitor a specific location in your Azure Storage blob container.</span></span>

## <a name="what-is-azure-storage"></a><span data-ttu-id="020c8-105">Azure Storage란?</span><span class="sxs-lookup"><span data-stu-id="020c8-105">What is Azure Storage?</span></span>

<span data-ttu-id="020c8-106">Azure Storage는 Blob, 큐 및 NoSQL을 비롯한 모든 형식의 데이터를 지원하는 Microsoft 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-106">Azure Storage is Microsoft's cloud storage solution that supports all types of data, including: blobs, queues, and NoSQL.</span></span> <span data-ttu-id="020c8-107">Azure Storage의 목표는 다음과 같은 데이터 저장소를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-107">The goal of Azure Storage is to provide data storage that's:</span></span>

- <span data-ttu-id="020c8-108">고가용성</span><span class="sxs-lookup"><span data-stu-id="020c8-108">Highly available</span></span>
- <span data-ttu-id="020c8-109">보안</span><span class="sxs-lookup"><span data-stu-id="020c8-109">Secure</span></span>
- <span data-ttu-id="020c8-110">확장성</span><span class="sxs-lookup"><span data-stu-id="020c8-110">Scalable</span></span>
- <span data-ttu-id="020c8-111">관리</span><span class="sxs-lookup"><span data-stu-id="020c8-111">Managed</span></span>

<span data-ttu-id="020c8-112">Azure Storage 자체에 너무 집중하지 않겠습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-112">We're not going to focus on Azure Storage too much.</span></span> <span data-ttu-id="020c8-113">대신, Azure Storage를 사용하여 함수 실행을 트리거할 Blob을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-113">Instead, we use it to create blobs that will trigger our function to run.</span></span>

## <a name="what-is-azure-blob-storage"></a><span data-ttu-id="020c8-114">Azure Blob Storage란?</span><span class="sxs-lookup"><span data-stu-id="020c8-114">What is Azure Blob storage?</span></span>

<span data-ttu-id="020c8-115">Azure Blob Storage는 구조화되지 않은 데이터를 대량으로 저장하도록 설계된 개체 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-115">Azure Blob storage is an object storage solution that's designed to store large amounts of unstructured data.</span></span> 

<span data-ttu-id="020c8-116">예를 들어 Azure Blob Storage는 다음과 같은 작업을 수행하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-116">For example, Azure Blob storage is great at doing things like:</span></span>

- <span data-ttu-id="020c8-117">파일 저장</span><span class="sxs-lookup"><span data-stu-id="020c8-117">Storing files.</span></span>
- <span data-ttu-id="020c8-118">파일 제공</span><span class="sxs-lookup"><span data-stu-id="020c8-118">Serving files.</span></span>
- <span data-ttu-id="020c8-119">동영상 및 오디오 스트리밍</span><span class="sxs-lookup"><span data-stu-id="020c8-119">Streaming video and audio.</span></span>
- <span data-ttu-id="020c8-120">데이터 기록</span><span class="sxs-lookup"><span data-stu-id="020c8-120">Logging data.</span></span>

<span data-ttu-id="020c8-121">**블록 Blob**, **추가 Blob** 및 **페이지 Blob** 등 세 가지 Blob 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-121">There are three types of blobs: **block blobs**, **append blobs**, and **page blobs**.</span></span> <span data-ttu-id="020c8-122">블록 Blob은 가장 일반적인 유형으로,</span><span class="sxs-lookup"><span data-stu-id="020c8-122">Block blobs are the most common type.</span></span> <span data-ttu-id="020c8-123">이를 통해 텍스트 또는 이진 데이터를 효율적으로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-123">They allow you to store text or binary data efficiently.</span></span> <span data-ttu-id="020c8-124">추가 Blob은 블록 Blob과 비슷하지만, 지속적으로 업데이트되는 로그 파일을 만드는 등의 추가 작업을 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-124">Append blobs are like block blobs, but they're designed more for append operations like creating a log file that's being constantly updated.</span></span> <span data-ttu-id="020c8-125">마지막으로, 페이지 Blob은 페이지로 구성되며 빈번한 임의의 읽기 및 쓰기 작업에 맞게 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-125">Finally, page blobs are made up of pages and are designed for frequent random read and write operations.</span></span>

## <a name="what-is-a-blob-trigger"></a><span data-ttu-id="020c8-126">Blob 트리거란?</span><span class="sxs-lookup"><span data-stu-id="020c8-126">What is a blob trigger?</span></span>

<span data-ttu-id="020c8-127">Blob 트리거는 Azure Blob Storage에서 파일이 업로드되거나 업데이트될 때 함수를 실행하는 트리거입니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-127">A blob trigger is a trigger that executes a function when a file is uploaded or updated in Azure Blob storage.</span></span> <span data-ttu-id="020c8-128">Blob 트리거를 만들려면 Azure Storage 계정을 만들고 트리거의 모니터링 대상이 되는 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-128">To create a blob trigger, you create an Azure Storage account and provide a location that the trigger monitors.</span></span>

## <a name="how-to-create-a-blob-trigger"></a><span data-ttu-id="020c8-129">Blob 트리거를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="020c8-129">How to create a blob trigger</span></span>

<span data-ttu-id="020c8-130">지금까지 알아본 다른 트리거와 마찬가지로 Blob 트리거도 Azure Portal에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-130">Just like the other triggers we've seen so far, we create a blob trigger in the Azure portal.</span></span> <span data-ttu-id="020c8-131">Azure 함수 내의 미리 정의된 트리거 형식 목록에서 **Blob 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-131">Inside your Azure function, select **Blob trigger** from the list of predefined trigger types.</span></span> <span data-ttu-id="020c8-132">그런 다음, Blob이 만들어지거나 업데이트될 때 실행할 논리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-132">Then enter the logic to execute when a blob is created or updated.</span></span>

<span data-ttu-id="020c8-133">한 가지 확인해야 할 설정이 **경로**입니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-133">One setting that you'll want to look at is the **Path**.</span></span> <span data-ttu-id="020c8-134">**경로**는 Blob이 업로드되거나 업데이트되었는지 여부를 확인하기 위해 모니터링할 Blob 트리거를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-134">The **Path** tells the blob trigger where to monitor to see if a blob is uploaded or updated.</span></span> <span data-ttu-id="020c8-135">기본적으로 **경로** 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-135">By default, the **Path** value is:</span></span> 

> <span data-ttu-id="020c8-136">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="020c8-136">samples-workitems/{name}</span></span>

<span data-ttu-id="020c8-137">이 개념을 *samples-workitems* 및 *{name}* 의 두 부분으로 나누어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-137">Let's break down this concept into two pieces: *samples-workitems* and *{name}*.</span></span> <span data-ttu-id="020c8-138">첫 번째 부분인 *samples-workitems*는 트리거가 모니터링하는 Blob 컨테이너를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-138">The first part, *samples-workitems*, represents the blob container that the trigger monitors.</span></span> <span data-ttu-id="020c8-139">두 번째 부분인 *{name}* 은 모든 형식의 파일이 트리거로 하여금 함수를 호출하게 만드는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-139">The second part, *{name}*, means that every type of file will cause the trigger to invoke the function.</span></span> <span data-ttu-id="020c8-140">필터가 없으므로 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-140">The function is invoked because there's no filter.</span></span> <span data-ttu-id="020c8-141">예를 들어, 다음과 같은 구문을 사용하면 PNG 파일이 추가될 때만 트리거가 함수를 호출하도록 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-141">For example, I could make the trigger invoke the function only when a PNG file is added by using syntax like:</span></span>

> <span data-ttu-id="020c8-142">samples-workitems/{name}.png</span><span class="sxs-lookup"><span data-stu-id="020c8-142">samples-workitems/{name}.png</span></span>

<span data-ttu-id="020c8-143">이 개념에서 마지막으로 가장 중요한 정보는 *name*이라는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-143">The last significant piece of information with this concept is the text *name*.</span></span> <span data-ttu-id="020c8-144">*name*은 추가된 파일의 이름을 수신하는 Azure 함수 내의 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-144">The *name* represents a parameter in your Azure function that receives the name of the added file.</span></span> <span data-ttu-id="020c8-145">예를 들어 *resume.txt*라는 파일을 업로드하는 경우 Azure 함수는 해당 값을 *name*이라는 매개 변수를 통해 문자열로 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-145">For example, if I upload a file named *resume.txt*, my Azure function receives that value as a string through a parameter called *name*.</span></span>

## <a name="summary"></a><span data-ttu-id="020c8-146">요약</span><span class="sxs-lookup"><span data-stu-id="020c8-146">Summary</span></span>

<span data-ttu-id="020c8-147">Blob 트리거는 Azure Storage Blob 계정의 특정 위치에 활동이 확인되면 Azure 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-147">A blob trigger invokes an Azure function when it sees activity at a specific location in your Azure Storage blob account.</span></span> <span data-ttu-id="020c8-148">Azure Portal에서 **경로** 값을 수정하여 모니터링할 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="020c8-148">You set the location to monitor by modifying the **Path** value in the Azure portal.</span></span>