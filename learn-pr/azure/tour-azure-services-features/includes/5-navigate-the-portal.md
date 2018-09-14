<span data-ttu-id="7fcc1-101">이제 계정이 있으니 **Azure Portal**에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-101">Now that we have an account, we can sign into the **Azure portal**.</span></span> <span data-ttu-id="7fcc1-102">이 포털은 웹 기반 관리 사이트며, 자신이 만든 모든 구독 및 리소스와 상호 작용이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-102">The portal is a web-based administration site that lets you interact with all of your subscriptions and resources you have created.</span></span> <span data-ttu-id="7fcc1-103">Azure에서 수행하는 거의 모든 작업은 이 웹 인터페이스를 통해서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-103">Almost everything you do with Azure can be done through this web interface.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="7fcc1-104">Azure Portal 레이아웃</span><span class="sxs-lookup"><span data-stu-id="7fcc1-104">Azure portal layout</span></span>

<span data-ttu-id="7fcc1-105">Azure Portal은 Microsoft Azure를 제어하기 위한 기본 GUI(그래픽 사용자 인터페이스)입니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-105">The Azure portal is the primary graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="7fcc1-106">포털에서 대부분의 관리 작업을 수행할 수 있고, 포털은 일반적으로 단일 작업을 수행하거나 구성 옵션을 자세히 보기에 가장 적합한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-106">You can carry out the majority of management actions in the portal, and it is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

![Azure Portal](../media-draft/5-portal.png)

:::row:::

    :::column:::
    ![The resources and favorites](../media-draft/5-favorites.png)
    :::column-end:::

    :::column span="3":::
    **Resource Panel**
    
    In the left-hand sidebar of the portal is the resource pane, which lists the main resource types. Note that Azure has more resource types than just those shown. The resources listed are part of your _favorites_. 

    You can customize this with the specific resource types you tend to create or administer most often. 

    You can also collapse this pane; with the **<<** caret. This will minimize it to just icons which can be convenient if you are working with limited screen real-estate.
    :::column-end:::

:::row-end:::

<span data-ttu-id="7fcc1-108">포털 보기의 나머지 부분은 사용하는 특정 요소에 대한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-108">The remainder of the portal view is for the specific elements you are working with.</span></span> <span data-ttu-id="7fcc1-109">기본(주) 페이지는 _대시보드_입니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-109">The default (main) page is the _dashboard_.</span></span> <span data-ttu-id="7fcc1-110">이 내용은 조금 후에 설명하겠지만, 리소스에 대해 사용자 지정이 가능한 조감도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-110">We'll cover this a bit later, but this represents a customizable birds-eye-view of your resources.</span></span> <span data-ttu-id="7fcc1-111">관리하려는 특정 리소스로 이동하거나 리소스 패널에서 **모든 리소스** 항목을 사용하여 리소스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-111">You can use it to jump into specific resources you want to manage, or search for resources with the **All resources** entry in the resource panel.</span></span> <span data-ttu-id="7fcc1-112">가상 머신이나 웹앱과 같은 리소스를 관리하는 경우에는 _블레이드_를 사용합니다. 여기에는 리소스에 대한 구체적인 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-112">When you are managing a resource, such as a virtual machine or a web app, you will work with a _blade_ that presents specific information about the resource.</span></span>

## <a name="what-is-a-blade"></a><span data-ttu-id="7fcc1-113">블레이드란?</span><span class="sxs-lookup"><span data-stu-id="7fcc1-113">What is a blade?</span></span>

<span data-ttu-id="7fcc1-114">Azure Portal에서는 탐색에 블레이드 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-114">The Azure portal uses a blades model for navigation.</span></span> <span data-ttu-id="7fcc1-115">_블레이드_는 탐색 시퀀스의 한 수준에 사용되는 UI가 포함된 슬라이드 아웃 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-115">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="7fcc1-116">예를 들어 이 시퀀스의 각 요소는 **가상 머신** > **계산** > **Ubuntu Server** 블레이드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-116">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span>

<span data-ttu-id="7fcc1-117">각 블레이드에는 몇 가지 정보와 구성 가능한 옵션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-117">Each blade contains some information and configurable options.</span></span> <span data-ttu-id="7fcc1-118">이러한 옵션 중 일부는 또 다른 블레이드를 생성하며 기존 블레이드의 오른쪽에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-118">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="7fcc1-119">새 블레이드에서는 모든 추가 구성 가능한 옵션이 또 다른 블레이드를 생성하는 방식으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-119">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="7fcc1-120">금방 여러 블레이드가 동시에 열려 있는 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-120">Pretty soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="7fcc1-121">블레이드를 최대화하여 전체 화면을 채울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-121">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="7fcc1-122">새 블레이드는 항상 소유자의 오른쪽에 추가되므로 창의 맨 아래에 있는 스크롤 막대를 사용하여 뒤로 이동하여 구성을 통해 이 지점까지 어떻게 도달했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-122">Since new blades are always added to the right of the owner, you can use the scrollbar at the bottom of the window to go backwards to see how you got to this spot in the configuration.</span></span> <span data-ttu-id="7fcc1-123">또는 블레이드의 맨 위 모서리에 있는 `X` 단추를 클릭하여 블레이드를 개별적으로 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-123">Alternatively, you can close blades individually by clicking the `X` button in the top corner of the blade.</span></span> <span data-ttu-id="7fcc1-124">변경 내용을 저장하지 않은 경우에는 계속하면 변경 내용이 손실될 수 있다고 알려주는 메시지가 Azure에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-124">If you have unsaved changes, Azure will prompt you to let you know that the changes will be lost if you continue.</span></span>

## <a name="configuring-settings-in-the-azure-portal"></a><span data-ttu-id="7fcc1-125">Azure Portal에서 설정 구성</span><span class="sxs-lookup"><span data-stu-id="7fcc1-125">Configuring settings in the Azure portal</span></span>

<span data-ttu-id="7fcc1-126">Azure Portal에는 여러 구성 옵션을 표시되며, 대개 화면의 맨 위 오른쪽에 있는 상태 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-126">The Azure portal displays several configuration options, mostly in the status bar at the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="7fcc1-127">공지</span><span class="sxs-lookup"><span data-stu-id="7fcc1-127">Notifications</span></span>

<span data-ttu-id="7fcc1-128">벨 아이콘을 클릭하면 **알림** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-128">Clicking the bell icon displays the **Notifications** pane.</span></span> <span data-ttu-id="7fcc1-129">이 창에는 수행한 마지막 작업이 해당 상태와 함께 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-129">This pane lists the last actions that have been carried out, along with their status.</span></span>

![알림 블레이드](../media-draft/5-notifications-blade.png)

### <a name="cloud-shell"></a><span data-ttu-id="7fcc1-131">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7fcc1-131">Cloud Shell</span></span>

<span data-ttu-id="7fcc1-132">**Cloud Shell** 아이콘(>_)을 클릭하면 새 Azure Cloud Shell 세션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-132">If you click the **Cloud Shell** icon (>_), you will create a new Azure Cloud Shell session.</span></span> <span data-ttu-id="7fcc1-133">Azure Cloud Shell은 Azure 리소스를 관리하기 위한 브라우저에서 액세스할 수 있는 대화형 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-133">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span> <span data-ttu-id="7fcc1-134">작업 방식에 가장 적합한 셸 환경을 유연하게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-134">It provides the flexibility of choosing the shell experience that best suits the way you work.</span></span> <span data-ttu-id="7fcc1-135">Linux 사용자는 Bash 환경을 선택할 수 있고, Windows 사용자는 PowerShell을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-135">Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.</span></span> <span data-ttu-id="7fcc1-136">이 브라우저 기반 터미널을 사용하면 포털에 내장된 명령줄 인터페이스를 통해 현재 구독에 포함된 모든 Azure 리소스를 제어하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-136">This browser-based terminal lets you control and administer all of your Azure resources in the current subscription through a command-line interface built right into the portal.</span></span>

![Cloud Shell](../media-draft/5-choose-shell.png)

### <a name="settings"></a><span data-ttu-id="7fcc1-138">설정</span><span class="sxs-lookup"><span data-stu-id="7fcc1-138">Settings</span></span>

<span data-ttu-id="7fcc1-139">Azure Portal 설정을 변경하려면 **톱니** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-139">Click the **gear** icon to change the Azure portal settings.</span></span> <span data-ttu-id="7fcc1-140">이러한 설정에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-140">These settings include:</span></span>

- <span data-ttu-id="7fcc1-141">로그아웃 시간</span><span class="sxs-lookup"><span data-stu-id="7fcc1-141">Logout time</span></span>
- <span data-ttu-id="7fcc1-142">색 구성표</span><span class="sxs-lookup"><span data-stu-id="7fcc1-142">Color scheme</span></span>
- <span data-ttu-id="7fcc1-143">고대비 테마</span><span class="sxs-lookup"><span data-stu-id="7fcc1-143">High contrast themes</span></span>
- <span data-ttu-id="7fcc1-144">알림 메시지(모바일 장치 대상)</span><span class="sxs-lookup"><span data-stu-id="7fcc1-144">Toast notifications (to a mobile device)</span></span>
- <span data-ttu-id="7fcc1-145">테마를 변경하려면 두 번 클릭</span><span class="sxs-lookup"><span data-stu-id="7fcc1-145">Double-click to change the theme</span></span>
- <span data-ttu-id="7fcc1-146">언어</span><span class="sxs-lookup"><span data-stu-id="7fcc1-146">Language</span></span>
- <span data-ttu-id="7fcc1-147">사용지역 언어</span><span class="sxs-lookup"><span data-stu-id="7fcc1-147">Regional format</span></span>

![포털 설정](../media-draft/5-settings-blade.png)

<span data-ttu-id="7fcc1-149">설정을 변경한 경우 **적용**을 클릭하여 변경을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-149">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="7fcc1-150">피드백 블레이드</span><span class="sxs-lookup"><span data-stu-id="7fcc1-150">Feedback blade</span></span>

<span data-ttu-id="7fcc1-151">**웃는 얼굴** 아이콘을 클릭하면 **피드백 보내기** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-151">The **smiley face** icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="7fcc1-152">여기에서 Azure에 대한 피드백을 Microsoft로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-152">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="7fcc1-153">Microsoft가 메일로 피드백에 응답할 수 있는지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-153">Note that you can specify whether Microsoft can respond to your feedback by email.</span></span>

![사용자 의견](../media-draft/5-feedback-blade.png)

### <a name="help-blade"></a><span data-ttu-id="7fcc1-155">도움말 블레이드</span><span class="sxs-lookup"><span data-stu-id="7fcc1-155">Help blade</span></span>

<span data-ttu-id="7fcc1-156">**물음표** 아이콘을 클릭하면 **도움말** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-156">Click the **question mark** icon to show the **Help** blade.</span></span> <span data-ttu-id="7fcc1-157">여기에서 다음과 같은 몇 가지 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-157">Here you choose from several options, including:</span></span>

- <span data-ttu-id="7fcc1-158">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="7fcc1-158">What's new</span></span>
- <span data-ttu-id="7fcc1-159">Azure 로드맵</span><span class="sxs-lookup"><span data-stu-id="7fcc1-159">Azure roadmap</span></span>
- <span data-ttu-id="7fcc1-160">둘러보기 시작</span><span class="sxs-lookup"><span data-stu-id="7fcc1-160">Launch guided tour</span></span>
- <span data-ttu-id="7fcc1-161">바로 가기 키</span><span class="sxs-lookup"><span data-stu-id="7fcc1-161">Keyboard shortcuts</span></span>
- <span data-ttu-id="7fcc1-162">진단 표시</span><span class="sxs-lookup"><span data-stu-id="7fcc1-162">Show diagnostics</span></span>
- <span data-ttu-id="7fcc1-163">개인정보처리방침 및 사용 약관</span><span class="sxs-lookup"><span data-stu-id="7fcc1-163">Privacy + terms</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="7fcc1-164">디렉터리 및 구독</span><span class="sxs-lookup"><span data-stu-id="7fcc1-164">Directory and subscription</span></span>

<span data-ttu-id="7fcc1-165">**책 및 필터** 아이콘을 클릭하여 **디렉터리 + 구독** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-165">Click the **Book and Filter** icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="7fcc1-166">Azure를 사용하면 두 개 이상의 구독을 하나의 디렉터리와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-166">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="7fcc1-167">**디렉터리 및 구독** 블레이드에서는 구독 간을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-167">On the **Directory + subscription** blade, you can change between subscriptions.</span></span> <span data-ttu-id="7fcc1-168">여기서 구독을 변경하거나 다른 디렉터리로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-168">Here, you can change your subscription or change to another directory.</span></span>

![디렉터리](../media-draft/5-directory-blade-1.png)

### <a name="profile-settings"></a><span data-ttu-id="7fcc1-170">프로필 설정</span><span class="sxs-lookup"><span data-stu-id="7fcc1-170">Profile settings</span></span>

<span data-ttu-id="7fcc1-171">오른쪽 위에 있는 이름을 클릭하면 프로필 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-171">If you click on your name in the top right-hand corner, you can then change your profile settings.</span></span>
<span data-ttu-id="7fcc1-172">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-172">Options include:</span></span>

- <span data-ttu-id="7fcc1-173">Azure에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="7fcc1-173">Sign out of Azure</span></span>
- <span data-ttu-id="7fcc1-174">암호 변경</span><span class="sxs-lookup"><span data-stu-id="7fcc1-174">Change password</span></span>
- <span data-ttu-id="7fcc1-175">연락처 정보 변경</span><span class="sxs-lookup"><span data-stu-id="7fcc1-175">Change contact information</span></span>
- <span data-ttu-id="7fcc1-176">권한 보기</span><span class="sxs-lookup"><span data-stu-id="7fcc1-176">View permissions</span></span>
- <span data-ttu-id="7fcc1-177">Azure 팀에 아이디어 제출</span><span class="sxs-lookup"><span data-stu-id="7fcc1-177">Submit an idea to the Azure team</span></span>
- <span data-ttu-id="7fcc1-178">청구서 보기</span><span class="sxs-lookup"><span data-stu-id="7fcc1-178">View your bill</span></span>
- <span data-ttu-id="7fcc1-179">디렉터리 전환(이전 섹션에서처럼 **디렉터리 + 구독** 블레이드 표시)</span><span class="sxs-lookup"><span data-stu-id="7fcc1-179">Switch directory (shows the **Directory + subscription** blade as in the previous section)</span></span>

![프로필 설정](../media-draft/5-portal-menu.png)

<span data-ttu-id="7fcc1-181">**청구서 보기**를 클릭하는 경우 **Cost Management + 청구 - 송장** 페이지로 이동하므로 Azure에서 비용이 발생하는 부분을 분석하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-181">If you now click **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

![청구 페이지](../media-draft/5-portal-billing.png)

<span data-ttu-id="7fcc1-183">Azure는 대규모 제품이며 Azure Portal 사용자 인터페이스(UI)에는 이러한 특징이 잘 반영되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-183">Azure is a large product, and the Azure portal user interface (UI) reflects this.</span></span> <span data-ttu-id="7fcc1-184">슬라이딩 블레이드 방식이기 때문에 다양한 관리 작업을 앞뒤로 쉽게 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-184">The sliding blade approach allows you to navigate back and forth through the various administration tasks with ease.</span></span> <span data-ttu-id="7fcc1-185">연습을 위해 이 UI를 조금 실험해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7fcc1-185">Let's experiment a bit with this UI so you get some practice.</span></span>