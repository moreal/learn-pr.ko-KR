<span data-ttu-id="f5948-101">TheMojifier는 다음과 같이 이미지의 사람 얼굴을 감정과 일치하는 이모지로 바꾸는 Slack _slash_ 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-101">TheMojifier is a Slack _slash_ command which replaces peoples faces in images with emojis matching their emotion, like so:</span></span>

![예제 이미지](/media-drafts/example-mojify-image.png)

<span data-ttu-id="f5948-103">Slack에서 사용자 지정 명령으로 작동하도록 설계되었으며, 명령의 이름을 원하는 대로 지정할 수 있습니다. 이 문서에서는 `mojify`라고 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-103">It's designed to work from Slack as a custom command, you can name the command how you want, for this document I've named it `mojify`.</span></span>

<span data-ttu-id="f5948-104">명령을 실행하려면 다음과 같이 `/mojify <image to mojify>`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-104">To execute the commmand type `/mojify <image to mojify>`, like so:</span></span>

![예제 이미지](/media-drafts/9.slack-type-mojify.png)

<span data-ttu-id="f5948-106">그러면 mojifier가 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-106">The mojifier then:</span></span>

1.  <span data-ttu-id="f5948-107">이미지 속 사람의 감정을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-107">Calculates the emotion of any people in the image.</span></span>
2.  <span data-ttu-id="f5948-108">감정을 이모지와 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-108">Matches emotions to emojis.</span></span>
3.  <span data-ttu-id="f5948-109">얼굴을 이모지로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-109">Replaces the faces with emojis.</span></span>
4.  <span data-ttu-id="f5948-110">이미지를 다시 Twitter에 응답으로 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-110">Posts the image back to Twitter as a reply.</span></span>

<span data-ttu-id="f5948-111">TheMojifier는 [Azure Functions](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai) 및 [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)를 포함한 여러 Azure 기술과 TypeScript를 사용하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-111">It’s written using TypeScript and several Azure technologies including [Azure Functions](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai) and [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)</span></span>

<span data-ttu-id="f5948-112">이 자습서에서는 TheMojifier를 만드는 방법을 설명하고 Azure 기술을 사용하여 사용자 고유의 Slack 명령을 만드는 방법을 보여드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-112">In this tutorial I’m going to explain how TheMojifier was made and show you how to create your own Slack command using Azure technologies.</span></span>

> <span data-ttu-id="f5948-113">TODO, 여기서는 어디일까요?</span><span class="sxs-lookup"><span data-stu-id="f5948-113">TODO, where will this be now?</span></span>
> <span data-ttu-id="f5948-114">Mojifier의 모든 코드는 [GitHub](https://github.com/jawache/mojifier)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-114">All the code for Mojifier is available on [GitHub](https://github.com/jawache/mojifier)</span></span>

# <a name="requirements"></a><span data-ttu-id="f5948-115">요구 사항</span><span class="sxs-lookup"><span data-stu-id="f5948-115">Requirements</span></span>

<span data-ttu-id="f5948-116">mojifier을 빌드하려면 여러 Azure 서비스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-116">To build the mojifier, we need to use several Azure services.</span></span>

## <a name="azure-cognitive-services"></a><span data-ttu-id="f5948-117">Azure Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="f5948-117">Azure Cognitive Services</span></span>

<span data-ttu-id="f5948-118">Azure Cognitive Services는 신속하게 응용 프로그램에 고급 AI 기능을 추가하는 데 사용할 수 있는 고급 API 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-118">Azure Cognitive Services are a set of high-level APIs you can use to add advanced AI functionality into your application quickly.</span></span> <span data-ttu-id="f5948-119">HTTP 요청을 만들 수 있으면 Cognitive Services를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-119">If you can make an HTTP request, you can use Cognitive Services.</span></span>

[<span data-ttu-id="f5948-120">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f5948-120">More info</span></span>](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)

## <a name="azure-functions"></a><span data-ttu-id="f5948-121">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f5948-121">Azure Functions</span></span>

<span data-ttu-id="f5948-122">Logic Apps만큼 강력하기 때문에 때로는 프로그래밍 언어의 전체 표현을 사용하여 비즈니스 논리를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-122">As powerful as Logic Apps are sometimes you need to write business logic using the full expressiveness of a programming language.</span></span> <span data-ttu-id="f5948-123">Azure Functions는 이벤트 또는 HTTP 요청에 응답할 수 있는 코드 조각을 호스트하는 기술입니다. Azure가 모든 크기 조정 문제를 자동으로 처리하므로 사용자는 사용한 만큼 요금을 지불하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5948-123">Azure Functions is a technology that lets you host snippets of code that can respond to events or HTTP requests, Azure handles all of the scaling issues for you and you only pay for what you use.</span></span>

[<span data-ttu-id="f5948-124">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f5948-124">More info</span></span>](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai)
