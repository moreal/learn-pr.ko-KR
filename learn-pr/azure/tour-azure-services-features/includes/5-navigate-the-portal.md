<span data-ttu-id="ed164-101">Azure 제품은 여러 계층으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-101">Azure products have a deep hierarchy.</span></span> <span data-ttu-id="ed164-102">예를 들어 Linux 가상 머신을 만들어야 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-102">For example, suppose you need to create a Linux virtual machine.</span></span> <span data-ttu-id="ed164-103">**홈** > **가상 머신** > **계산** > **Ubuntu Server**와 같이 여러 수준에서 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-103">You might navigate through these levels: **Home** > **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span> <span data-ttu-id="ed164-104">Azure Portal은 해당 UI를 최적화하여 이러한 유형의 탐색 시퀀스를 쉽게 이해할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-104">The Azure portal optimizes its UI to make this type of navigation sequence intuitive.</span></span> <span data-ttu-id="ed164-105">여기서는 이를 가능하게 하는 주요 UI 요소를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-105">Here, you will survey the key UI elements that make this possible.</span></span> <span data-ttu-id="ed164-106">메뉴 및 하위 메뉴를 탐색하고 블레이드를 사용하여 서비스를 찾아 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-106">You will navigate through menus and submenus and use blades to find and configure services.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="ed164-107">Azure Portal 레이아웃</span><span class="sxs-lookup"><span data-stu-id="ed164-107">Azure portal layout</span></span>

<span data-ttu-id="ed164-108">Azure Portal은 Microsoft Azure를 제어하기 위한 기본 GUI(그래픽 사용자 인터페이스)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-108">The Azure portal is the main graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="ed164-109">포털에서는 대부분의 관리 작업을 수행할 수 있으며 포털은 일반적으로 단일 작업을 수행하거나 구성 옵션을 자세히 보기에 가장 적합한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-109">You can carry out the large majority of management actions on the portal, and the portal is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

<span data-ttu-id="ed164-110">포털의 왼쪽 창은 기본 리소스 종류가 나열된 리소스 창입니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-110">In the left-hand pane of the portal is the resource pane, which lists the main resource types.</span></span> <span data-ttu-id="ed164-111">Azure의 리소스 종류는 표시된 것보다 훨씬 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-111">Note that Azure has far many more resource types than just those shown.</span></span>

## <a name="using-blades-in-the-azure-portal"></a><span data-ttu-id="ed164-112">Azure Portal에서 블레이드 사용</span><span class="sxs-lookup"><span data-stu-id="ed164-112">Using blades in the Azure portal</span></span>

<span data-ttu-id="ed164-113">Azure Portal에서는 탐색을 위해 블레이드 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-113">The Azure portal uses a blades model for navigation.</span></span> <span data-ttu-id="ed164-114">_블레이드_는 탐색 시퀀스의 한 수준에 사용되는 UI가 포함된 슬라이드 아웃 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-114">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="ed164-115">예를 들어 이 시퀀스의 각 요소는 **가상 머신** > **계산** > **Ubuntu Server**와 같은 블레이드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-115">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span>

<span data-ttu-id="ed164-116">UI 내 각 블레이드에는 일반적으로 여러 구성 가능한 옵션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-116">Each blade within the UI typically contains a number of configurable options.</span></span> <span data-ttu-id="ed164-117">이러한 옵션 중 일부는 기존 블레이드의 오른쪽에 자신을 표시하는 다른 블레이드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-117">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="ed164-118">새 블레이드에서는 모든 추가 구성 가능한 옵션이 또 다른 블레이드를 생성하는 방식으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-118">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="ed164-119">금방 여러 블레이드가 동시에 열려 있는 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-119">Pretty soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="ed164-120">블레이드를 최대화하여 전체 화면을 채울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-120">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="ed164-121">구성 변경을 수행하고 저장하지 않은 상태로 블레이드를 닫으려고 하면 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-121">If you try to close a blade without saving any configuration changes that you have made, you will receive a prompt.</span></span>

## <a name="configuring-settings-in-the-azure-portal"></a><span data-ttu-id="ed164-122">Azure Portal에서 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ed164-122">Configuring settings in the Azure portal</span></span>

<span data-ttu-id="ed164-123">Azure Portal은 대개 화면의 오른쪽 맨 위에 있는 상태 표시줄에 여러 구성 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-123">The Azure portal displays several configuration options, mostly in the status bar to the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="ed164-124">공지</span><span class="sxs-lookup"><span data-stu-id="ed164-124">Notifications</span></span>

<span data-ttu-id="ed164-125">벨 아이콘을 클릭하면 **알림** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-125">Clicking the bell icon displays the **Notifications** pane.</span></span> <span data-ttu-id="ed164-126">이 창에는 수행한 마지막 작업이 해당 상태와 함께 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-126">This pane lists the last actions that have been carried out, along with their status.</span></span>

![알림 블레이드](../media-draft/2-notifications-blade.PNG)

### <a name="cloud-shell"></a><span data-ttu-id="ed164-128">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ed164-128">Cloud Shell</span></span>

<span data-ttu-id="ed164-129">**Cloud Shell** 아이콘(>_)을 클릭하면 새 Azure Cloud Shell 세션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-129">If you click the **Cloud Shell** icon (>_), you will create a new Azure Cloud Shell session.</span></span> <span data-ttu-id="ed164-130">해당 세션에서 Linux Bash 또는 Linux 기반 PowerShell을 사용하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-130">You are prompted to use either Linux Bash or PowerShell on Linux in that session.</span></span>

![Cloud Shell](../media-draft/2-choose-shell.PNG)

### <a name="settings"></a><span data-ttu-id="ed164-132">설정</span><span class="sxs-lookup"><span data-stu-id="ed164-132">Settings</span></span>

<span data-ttu-id="ed164-133">Azure Portal 설정을 변경하려면 **톱니** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-133">Click the **gear** icon to change the Azure portal settings.</span></span> <span data-ttu-id="ed164-134">이러한 설정에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-134">These settings include:</span></span>

* <span data-ttu-id="ed164-135">로그아웃 시간</span><span class="sxs-lookup"><span data-stu-id="ed164-135">Logout time</span></span>
* <span data-ttu-id="ed164-136">색 구성표</span><span class="sxs-lookup"><span data-stu-id="ed164-136">Color scheme</span></span>
* <span data-ttu-id="ed164-137">고대비 테마</span><span class="sxs-lookup"><span data-stu-id="ed164-137">High contrast themes</span></span>
* <span data-ttu-id="ed164-138">알림 메시지(모바일 장치 대상)</span><span class="sxs-lookup"><span data-stu-id="ed164-138">Toast notifications (to a mobile device)</span></span>
* <span data-ttu-id="ed164-139">테마를 변경하려면 두 번 클릭</span><span class="sxs-lookup"><span data-stu-id="ed164-139">Double-click to change theme</span></span>
* <span data-ttu-id="ed164-140">언어</span><span class="sxs-lookup"><span data-stu-id="ed164-140">Language</span></span>
* <span data-ttu-id="ed164-141">사용지역 언어</span><span class="sxs-lookup"><span data-stu-id="ed164-141">Regional format</span></span>

![포털 설정](../media-draft/2-settings-blade.PNG)

<span data-ttu-id="ed164-143">설정을 변경한 경우 **적용**을 클릭하여 변경을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-143">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="ed164-144">피드백 블레이드</span><span class="sxs-lookup"><span data-stu-id="ed164-144">Feedback blade</span></span>

<span data-ttu-id="ed164-145">**웃는 얼굴** 아이콘을 클릭하면 **피드백 보내기** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-145">The **smiley face** icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="ed164-146">여기에서 Azure에 대한 피드백을 Microsoft로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-146">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="ed164-147">Microsoft가 메일로 피드백에 응답할 수 있는지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-147">Note that you can specify whether Microsoft can respond to your feedback by email.</span></span>

![사용자 의견](../media-draft/2-feedback-blade.PNG)

### <a name="help-blade"></a><span data-ttu-id="ed164-149">도움말 블레이드</span><span class="sxs-lookup"><span data-stu-id="ed164-149">Help blade</span></span>

<span data-ttu-id="ed164-150">**물음표** 아이콘을 클릭하여 **도움말** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-150">Click the **question mark** icon to show the **Help** blade.</span></span> <span data-ttu-id="ed164-151">여기서 다음과 같은 여러 항목 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-151">Here you choose from a number of topics, including:</span></span>

* <span data-ttu-id="ed164-152">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="ed164-152">What's new</span></span>
* <span data-ttu-id="ed164-153">Azure 로드맵</span><span class="sxs-lookup"><span data-stu-id="ed164-153">Azure roadmap</span></span>
* <span data-ttu-id="ed164-154">둘러보기 시작</span><span class="sxs-lookup"><span data-stu-id="ed164-154">Launch guided tour</span></span>
* <span data-ttu-id="ed164-155">바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="ed164-155">Keyboard shortcuts</span></span>
* <span data-ttu-id="ed164-156">진단 표시</span><span class="sxs-lookup"><span data-stu-id="ed164-156">Show diagnostics</span></span>
* <span data-ttu-id="ed164-157">개인정보처리방침 및 사용 약관</span><span class="sxs-lookup"><span data-stu-id="ed164-157">Privacy + terms</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="ed164-158">디렉터리 및 구독</span><span class="sxs-lookup"><span data-stu-id="ed164-158">Directory and subscription</span></span>

<span data-ttu-id="ed164-159">**책 및 필터** 아이콘을 클릭하여 **디렉터리 + 구독** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-159">Click the **Book and Filter** icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="ed164-160">Azure를 사용하면 두 개 이상의 구독을 하나의 디렉터리와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-160">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="ed164-161">**디렉터리 및 구독** 블레이드에서는 구독 간을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-161">On the **Directory + subscription** blade, you can change between subscriptions.</span></span> <span data-ttu-id="ed164-162">여기서 구독을 변경하거나 다른 디렉터리로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-162">Here, you can change your subscription or change to another directory.</span></span>

![디렉터리](../media-draft/2-directory-blade-1.PNG)

### <a name="profile-settings"></a><span data-ttu-id="ed164-164">프로필 설정</span><span class="sxs-lookup"><span data-stu-id="ed164-164">Profile settings</span></span>

<span data-ttu-id="ed164-165">오른쪽 위에 있는 이름을 클릭하면 프로필 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-165">If you click on your name in the top right-hand corner, you can then change your profile settings.</span></span>
<span data-ttu-id="ed164-166">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-166">Options include:</span></span>

* <span data-ttu-id="ed164-167">Azure에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="ed164-167">Sign out of Azure</span></span>
* <span data-ttu-id="ed164-168">암호 변경</span><span class="sxs-lookup"><span data-stu-id="ed164-168">Change password</span></span>
* <span data-ttu-id="ed164-169">연락처 정보 변경</span><span class="sxs-lookup"><span data-stu-id="ed164-169">Change contact information</span></span>
* <span data-ttu-id="ed164-170">권한 보기</span><span class="sxs-lookup"><span data-stu-id="ed164-170">View permissions</span></span>
* <span data-ttu-id="ed164-171">Azure 팀에 아이디어 제출</span><span class="sxs-lookup"><span data-stu-id="ed164-171">Submit an idea to the Azure team</span></span>
* <span data-ttu-id="ed164-172">청구서 보기</span><span class="sxs-lookup"><span data-stu-id="ed164-172">View your bill</span></span>
* <span data-ttu-id="ed164-173">디렉터리 전환(이전 섹션에서처럼 **디렉터리 + 구독** 블레이드 표시)</span><span class="sxs-lookup"><span data-stu-id="ed164-173">Switch directory (shows the **Directory + subscription** blade as in the previous section)</span></span>

![프로필 설정](../media-draft/2-portal-menu.png)

<span data-ttu-id="ed164-175">**청구서 보기**를 클릭하는 경우 **Cost Management + 청구 - 송장** 페이지로 이동하므로 Azure에서 비용이 발생하는 부분을 분석하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-175">If you now click **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

![청구 페이지](../media-draft/2-portal-billing.PNG)

## <a name="summary"></a><span data-ttu-id="ed164-177">요약</span><span class="sxs-lookup"><span data-stu-id="ed164-177">Summary</span></span>

<span data-ttu-id="ed164-178">Azure는 대규모 제품이며 Azure Portal UI에는 이러한 특징이 잘 반영되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-178">Azure is a large product, and the Azure portal UI reflects this.</span></span> <span data-ttu-id="ed164-179">포털에서 이렇게 복잡한 탐색을 지원하는 기본적인 방법은 블레이드를 통해 계층 구조를 나타내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-179">The primary way that the portal helps you navigate this complexity is with blades to indicate hierarchy.</span></span> <span data-ttu-id="ed164-180">블레이드를 사용하면 특정 작업에 집중할 수 있을 뿐만 아니라 해당 위치에 도달하게 된 경로를 명확하게 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed164-180">Blades let you focus on a specific task while clearly indicating the path you took to reach that point.</span></span>