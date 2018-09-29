> [!TIP]
> <span data-ttu-id="4e172-101">VM에 로그인하는 데 필요한 사용자 이름 및 암호는 **리소스** 탭에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-101">The username and password you need to sign in to the VM are located on the **Resources** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="4e172-102">Mac을 사용 하는 경우 VM을 시작한 후 도구 모음에서 번개 아이콘이나, VM의 잠금을 해제하는 지침 옆에 있는 **리소스** 탭에서 **Ctrl+Alt+Delete** 옵션을 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-102">If you are using a Mac, after launching the VM you may need to use either the lightning icon on the toolbar, or the **Ctrl+Alt+Delete** option from the **Resources** tab next to the instructions to unlock the VM.</span></span>


<span data-ttu-id="4e172-103">이 모듈에서는 서버리스 백 엔드를 사용하여 플랫폼 간 Xamarin.Forms 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-103">In this module, you'll create a cross-platform Xamarin.Forms app with a serverless back end.</span></span> <span data-ttu-id="4e172-104">이 앱은 사용자의 장치에서 사용자 위치를 가져와 전화 번호 목록과 함께 Azure 함수로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-104">This app will get the user's location from their device and send it with a list of phone numbers to an Azure function.</span></span> <span data-ttu-id="4e172-105">그러면 해당 함수가 타사 서비스(Twilio)에 대한 바인딩을 사용하여 사용자 위치를 제공된 모든 전화 번호에 SMS 메시지로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-105">The function will then use a binding to a third-party service (Twilio) to send your location as an SMS message to all the phone numbers provided.</span></span>

<span data-ttu-id="4e172-106">이 프로세스는 다음 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-106">This process involves the following steps:</span></span>

1. <span data-ttu-id="4e172-107">앱은 장치별 위치 API에 대한 추상화로 Xamarin.Essentials를 사용하여 위치를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-107">The app captures your location using Xamarin.Essentials as an abstraction over device-specific location APIs.</span></span>

1. <span data-ttu-id="4e172-108">위치 및 전화 번호는 JSON 페이로드로 패키지되어 Azure 함수로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-108">The location and phone numbers are packaged up into a JSON payload and sent to an Azure function.</span></span>

1. <span data-ttu-id="4e172-109">Azure 함수는 JSON 페이로드를 디코딩하고 SMS 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-109">The Azure function decodes the JSON payload and creates SMS messages.</span></span>

1. <span data-ttu-id="4e172-110">SMS 메시지는 [Twilio](https://www.twilio.com/?azure-portal=true)를 통해 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-110">The SMS messages are sent via [Twilio](https://www.twilio.com/?azure-portal=true).</span></span>

<span data-ttu-id="4e172-111">다음 일러스트레이션은 이 프로세스의 개요를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-111">The following illustration shows an overview of this process.</span></span>

![문자 메시지를 통해 위치를 공유하는 프로세스의 대략적인 아키텍처를 보여 주는 그림.](../media/1-architecture.png)

## <a name="create-a-twilio-account"></a><span data-ttu-id="4e172-113">Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4e172-113">Create a Twilio account</span></span>

<span data-ttu-id="4e172-114">Azure 함수에서 SMS 메시지를 보내려면 Twilio 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-114">To be able to send SMS messages from an Azure function, you'll need a Twilio account.</span></span> <span data-ttu-id="4e172-115">체험 계정만 있어도 충분히 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-115">The free account is more than enough to get started.</span></span>

1. <span data-ttu-id="4e172-116">[twilio.com](https://www.twilio.com?azure-portal=true)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-116">Head to [twilio.com](https://www.twilio.com?azure-portal=true).</span></span>

1. <span data-ttu-id="4e172-117">오른쪽 위에 있는 빨간색 **등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-117">Click the red **Sign Up** button in the top-right corner.</span></span>

1. <span data-ttu-id="4e172-118">세부 정보를 입력하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-118">Fill in your details and click **Get Started**.</span></span>

1. <span data-ttu-id="4e172-119">사용자는 전화 번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-119">You'll need to verify your phone number.</span></span> <span data-ttu-id="4e172-120">Twilio 체험 계정을 사용하면 확인된 전화 번호로만 메시지를 보내 전화 번호가 스팸에 사용되지 않도록 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-120">Twilio free accounts let you send messages only to verified phone numbers to stop them being used for spam.</span></span> <span data-ttu-id="4e172-121">Twilio는 사용자가 전화 확인을 위해 입력해야 하는 확인 코드를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-121">Twilio will send you a verification code that you need to enter to verify your phone.</span></span>

1. <span data-ttu-id="4e172-122">**제품** 탭을 선택하고 **프로그래밍 가능한 SMS**을 클릭한 다음, **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-122">Select the **Products** tab, and click **Programmable SMS**, then click **Continue**.</span></span>

1. <span data-ttu-id="4e172-123">첫 번째 프로젝트 이름(예: “I’m here”)을 지정한 다음, **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-123">Provide a name for your first project, such as "I'm here", then click **Continue**.</span></span>

1. <span data-ttu-id="4e172-124">팀 동료를 초대하는 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-124">Skip the step to invite a team mate.</span></span>

1. <span data-ttu-id="4e172-125">Twilio 메시징 대시보드에서 **프로젝트 정보** 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-125">From the Twilio messaging dashboard, expand the **Project Info** panel.</span></span>

1. <span data-ttu-id="4e172-126">**계정 SID** 및 **인증 토큰** 값은 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-126">Note your **ACCOUNT SID** and **AUTH TOKEN** because you will need these values later.</span></span>

    <span data-ttu-id="4e172-127">Twilio 계정을 만들 때 메시지를 보낼 수 있는 전화 번호가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-127">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="4e172-128">이 전화 번호는 Twilio **전화 번호** 대시보드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-128">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span>

1. <span data-ttu-id="4e172-129">Twilio 사이트 왼쪽 메뉴 아래쪽에 있는 줄임표를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-129">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="4e172-130">그런 다음, ‘슈퍼 네트워크->전화 번호’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-130">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="4e172-131">고정 아이콘을 사용하여 이 대시보드를 왼쪽 메뉴에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-131">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="4e172-132">Twilio 번호는 *번호 관리->활성 번호* 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-132">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span>

    ![Twilio 번호 찾기](../media/7-twilio-find-number.png)

    > [!TIP]
    > <span data-ttu-id="4e172-134">활성 번호가 아직 없는 경우 활성 번호 페이지에서 **시작**을 선택하여 번호를 만드는 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-134">If you don't have an active number yet, select **Get Started** in the Active Numbers page to begin the process of creating a number.</span></span>

1. <span data-ttu-id="4e172-135">활성 전화 번호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-135">Note your active phone number.</span></span> <span data-ttu-id="4e172-136">이 번호는 나중에 이 모듈에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-136">It will be used later in this module.</span></span>


> [!NOTE]
> <span data-ttu-id="4e172-137">등록하면 SMS 메시지를 보내는 데 사용할 Twilio 전화 번호가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-137">When you sign up, you will be assigned a Twilio phone number that will be used to send SMS messages.</span></span> <span data-ttu-id="4e172-138">일부 국가에서는 이러한 번호를 통해 SMS 메시지를 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-138">In some countries, these numbers may not be able to send SMS messages.</span></span> <span data-ttu-id="4e172-139">Twilio 설명서는 [제한이 있는 국가](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true)를 나열하고, [국가별 번호 또는 영숫자로 된 보낸 사람 ID](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true)를 사용하여 SMS 메시지를 전송하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-139">The Twilio documentation lists [which countries have restrictions](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), and shows ways to send SMS messages using an [international number or AlphaNumeric sender Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true).</span></span>

## <a name="launch-visual-studio"></a><span data-ttu-id="4e172-140">Visual Studio 시작</span><span class="sxs-lookup"><span data-stu-id="4e172-140">Launch Visual Studio</span></span>

<span data-ttu-id="4e172-141">이 모듈에서는 Visual Studio 2017을 사용하여 가상 머신에서 사용할 수 있는 모바일 앱과 Azure Functions 앱을 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-141">For this module, you'll develop the mobile app and Azure Functions app using Visual Studio 2017, available via a virtual machine.</span></span> <span data-ttu-id="4e172-142">Xamarin.Forms 앱은 iOS, Android 및 UWP(유니버설 Windows 플랫폼)에서 실행되도록 빌드될 수 있지만 이 모듈에서는 랩 가상 머신 내에서 작동하도록 UWP에만 집중하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-142">Although Xamarin.Forms apps can be built to run on iOS, Android, and Universal Windows Platform (UWP), this module will just focus on UWP so that it works inside the lab virtual machine.</span></span>

<span data-ttu-id="4e172-143">VM의 시작 메뉴 또는 바탕 화면 바로 가기에서 Visual Studio 2017을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-143">Launch Visual Studio 2017 from the VM's Start Menu, or from the desktop shortcut.</span></span>

## <a name="summary"></a><span data-ttu-id="4e172-144">요약</span><span class="sxs-lookup"><span data-stu-id="4e172-144">Summary</span></span>

<span data-ttu-id="4e172-145">이 단원에서는 SMS 메시지를 보내는 데 사용할 Twilio 계정을 만들었고 Visual Studio를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-145">In this unit, you created a Twilio account to use to send SMS messages and launched Visual Studio.</span></span> <span data-ttu-id="4e172-146">다음에는 Xamarin.Forms 앱을 만들고 Xamarin.Essentials NuGet 패키지를 추가하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-146">Next, you learn how to create a Xamarin.Forms app and add the Xamarin.Essentials NuGet package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e172-147">이 단원에서 수집한 Twilio **계정 SID**, **인증 토큰** 및 **활성 전화 번호** 값은 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4e172-147">Keep note of the Twilio  **ACCOUNT SID** and **AUTH TOKEN** and **Active Phone Number** values that you gathered in this unit, because you'll need these values later.</span></span>
