<span data-ttu-id="2f7d3-101">입력 바인딩과 마찬가지로 출력 바인딩에도 여러 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-101">As with input bindings, there are multiple types of output bindings.</span></span> <span data-ttu-id="2f7d3-102">그러나 모든 유형이 입력과 출력 둘 다를 지원하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-102">However not all types support both input and output.</span></span> <span data-ttu-id="2f7d3-103">데이터를 보내거나 저장하고자 할 때마다 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-103">You'll use them anytime you want to send or store data.</span></span> <span data-ttu-id="2f7d3-104">여기에서는 출력 바인딩을 지원하는 형식과 사용 시기에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-104">Here, we'll look at the types that support output bindings and when to use them.</span></span>

## <a name="output-binding-types"></a><span data-ttu-id="2f7d3-105">출력 바인딩 형식</span><span class="sxs-lookup"><span data-stu-id="2f7d3-105">Output binding types</span></span>

- <span data-ttu-id="2f7d3-106">**Blob Storage** - Blob 출력 바인딩을 사용하여 Blob를 작성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-106">**Blob Storage** - You can use the blob output binding to write blobs.</span></span>

- <span data-ttu-id="2f7d3-107">**Cosmos DB** - Azure Cosmos DB 출력 바인딩을 사용하면 Azure Cosmos DB 데이터베이스에 SQL API를 사용하여 새 문서를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-107">**Cosmos DB** - The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.</span></span>

- <span data-ttu-id="2f7d3-108">**Event Hubs** - Event Hubs 출력 바인딩을 사용하여 이벤트 스트림에 이벤트를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-108">**Event Hubs** - Use the Event Hubs output binding to write events to an event stream.</span></span> <span data-ttu-id="2f7d3-109">이벤트를 쓰려면 이벤트 허브에 대한 보내기 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-109">You must have send permission to an event hub to write events to it.</span></span>

- <span data-ttu-id="2f7d3-110">**HTTP** - HTTP 요청 발신기(sender)에 응답하려면 HTTP 출력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-110">**HTTP** - Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="2f7d3-111">이 바인딩에는 HTTP 트리거가 필요하며 트리거 요청과 관련된 응답을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-111">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="2f7d3-112">웹 후크에 연결하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-112">This can also be used to connect to web hooks.</span></span>

- <span data-ttu-id="2f7d3-113">**Microsoft Graph** - Microsoft Graph 출력 바인딩을 통해 OneDrive에 파일을 쓰고, Excel 데이터를 수정하며, Outlook을 통해 이메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-113">**Microsoft Graph** - Microsoft Graph output bindings allow you to write to files in OneDrive, modify Excel data, and send email through Outlook.</span></span>

- <span data-ttu-id="2f7d3-114">**Mobile Apps** - Mobile Apps 출력 바인딩을 사용하여 Mobile Apps 테이블에 새 레코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-114">**Mobile Apps** - The Mobile Apps output binding writes a new record to a Mobile Apps table.</span></span>

- <span data-ttu-id="2f7d3-115">**Notification Hubs** - Notification Hubs 출력 바인딩을 사용하여 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-115">**Notification Hubs** - You can send push notifications with Notification Hubs output bindings.</span></span>

- <span data-ttu-id="2f7d3-116">**Queue Storage** - Azure Queue Storage 출력 바인딩을 사용하여 메시지를 큐에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-116">**Queue Storage** - Use the Azure Queue storage output binding to write messages to a queue.</span></span>

- <span data-ttu-id="2f7d3-117">**Send Grid** - SendGrid 바인딩을 사용하여 이메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-117">**Send Grid** - Send emails using SendGrid bindings.</span></span>

- <span data-ttu-id="2f7d3-118">**Service Bus** - Azure Service Bus 출력 바인딩을 사용하여 큐 또는 토픽 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-118">**Service Bus** - Use Azure Service Bus output binding to send queue or topic messages.</span></span>

- <span data-ttu-id="2f7d3-119">**Table storage** - Azure Table Storage 출력 바인딩을 사용하여 Azure Storage 계정에서 테이블에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-119">**Table storage** - Use an Azure Table storage output binding to write to a table in an Azure Storage account.</span></span>

- <span data-ttu-id="2f7d3-120">**Twilio** - Twilio를 사용하여 문자 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-120">**Twilio** - Send text messages with Twilio.</span></span>

<span data-ttu-id="2f7d3-121">바인딩을 출력으로 만들려면 `direction`을 `out`으로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-121">To create a binding as an output, you must define the `direction` as `out`.</span></span> <span data-ttu-id="2f7d3-122">바인딩 형식별로 매개 변수가 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-122">The parameters for each type of binding may vary.</span></span>

## <a name="combining-input-and-output-bindings"></a><span data-ttu-id="2f7d3-123">입력 및 출력 바인딩 결합</span><span class="sxs-lookup"><span data-stu-id="2f7d3-123">Combining input and output bindings</span></span> 

<span data-ttu-id="2f7d3-124">단일 함수에 여러 바인딩을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-124">It's possible to apply multiple bindings to a single function.</span></span> <span data-ttu-id="2f7d3-125">이렇게 하면 입력 및 출력 바인딩을 모두 정의할 수 있으며, 입력 및 출력의 바인딩 형식을 동일하게 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f7d3-125">This allows you to define both input and output bindings, and the input and output can even be the same binding type.</span></span>