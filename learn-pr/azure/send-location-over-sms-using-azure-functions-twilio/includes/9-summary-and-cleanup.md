<span data-ttu-id="58a3a-101">Xamarin 및 Azure 함수와 Twilio 바인딩을 사용하여 플랫폼 간 모바일 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-101">You've successfully created a cross-platform mobile app using Xamarin and an Azure function with a Twilio binding.</span></span>

## <a name="clean-up"></a><span data-ttu-id="58a3a-102">정리</span><span class="sxs-lookup"><span data-stu-id="58a3a-102">Clean up</span></span>

<!---TODO: Update for sandbox?--->

<span data-ttu-id="58a3a-103">이 Azure Functions 응용 프로그램의 작업이 완료되면 Azure Portal에서 모듈 진행 중에 만든 모든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-103">When you're done working with this Azure Functions application, you can delete all resources created during the module from the Azure portal.</span></span>

1. <span data-ttu-id="58a3a-104">Visual Studio에서 *보기->클라우드 탐색기*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-104">From Visual Studio, select *View->Cloud Explorer*.</span></span>

1. <span data-ttu-id="58a3a-105">이 패널의 맨 위 드롭다운에서 ‘리소스 그룹’을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-105">From the drop-down at the top of this panel, select *Resource Groups*.</span></span>

1. <span data-ttu-id="58a3a-106">리소스 그룹을 만드는 데 사용한 구독을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-106">Expand the subscription that you used to create the resource group.</span></span> <span data-ttu-id="58a3a-107">“ImHere” 리소스 그룹을 마우스 오른쪽 단추로 클릭하고 ‘포털에서 열기’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-107">Right-click on the "ImHere" resource group and select *Open in Portal*.</span></span>

    ![클라우드 탐색기 창에서 포털의 리소스 그룹을 엽니다.](../media/9-open-resource-group-in-portal.png)

1. <span data-ttu-id="58a3a-109">필요한 경우 브라우저에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-109">Log into the Azure portal in your browser, if necessary.</span></span>

1. <span data-ttu-id="58a3a-110">포털이 “ImHere” 리소스 그룹에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-110">The portal will open on the "ImHere" resource group.</span></span> <span data-ttu-id="58a3a-111">**리소스 그룹 삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-111">Click the **Delete Resource Group** button.</span></span>

1. <span data-ttu-id="58a3a-112">리소스 그룹의 이름을 입력하여 삭제를 확인하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-112">Enter the name of the resource group to confirm the deletion and click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="58a3a-113">요약</span><span class="sxs-lookup"><span data-stu-id="58a3a-113">Summary</span></span>

<span data-ttu-id="58a3a-114">이 모듈에서는 다음을 수행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-114">In this module, you learned how to:</span></span>

- <span data-ttu-id="58a3a-115">Xamarin.Essentials를 사용하는 플랫폼 간 Xamarin.Forms 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-115">Create a cross-platform Xamarin.Forms app that uses Xamarin.Essentials.</span></span>
- <span data-ttu-id="58a3a-116">ViewModel에서 응용 프로그램 논리와 함께 XAML을 사용하여 플랫폼 간 UI를 만들고 ViewModel의 속성을 UI에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-116">Create a cross-platform UI using XAML with application logic in a ViewModel, as well as bind properties in a ViewModel to the UI.</span></span>
- <span data-ttu-id="58a3a-117">사용자 위치를 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-117">Detect the user's location.</span></span>
- <span data-ttu-id="58a3a-118">HTTP 트리거를 사용하여 Azure 함수를 만들고 로컬에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-118">Create an Azure Function with an HTTP trigger and run it locally.</span></span>
- <span data-ttu-id="58a3a-119">모바일 앱에서 Azure 함수를 호출하고 데이터를 JSON으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-119">Call an Azure Function from a mobile app, passing data as JSON.</span></span>
- <span data-ttu-id="58a3a-120">Azure 함수를 Twilio에 바인딩하여 SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-120">Bind an Azure Function to Twilio to send an SMS message.</span></span>
- <span data-ttu-id="58a3a-121">Azure 함수를 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="58a3a-121">Publish an Azure Function to Azure.</span></span>