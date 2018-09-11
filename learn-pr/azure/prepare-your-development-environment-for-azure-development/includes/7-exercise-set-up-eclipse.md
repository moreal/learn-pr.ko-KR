<span data-ttu-id="48954-101">이 연습에서는 로컬 머신에 Eclipse를 설치한 후 Azure Toolkit를 설치하여 Azure 통합을 통해 Java 응용 프로그램을 개발할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-101">In this exercise, you will install Eclipse on your local machine and then install the Azure Toolkit, preparing you for developing Java applications with Azure integration.</span></span> <span data-ttu-id="48954-102">설치는 빠르고 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-102">The installation is quick and simple.</span></span> <span data-ttu-id="48954-103">이 연습을 마치면 첫 번째 Java 응용 프로그램을 시작하는 데 필요한 모든 것이 설정되어 Azure의 기능과 서비스를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48954-103">At the end of the exercise, you will have everything set up that you need to start your first Java application, taking advantage of the features and services of Azure.</span></span>

## <a name="install-eclipse-ide"></a><span data-ttu-id="48954-104">Eclipse IDE 설치</span><span class="sxs-lookup"><span data-stu-id="48954-104">Install Eclipse IDE</span></span>

1. <span data-ttu-id="48954-105">http://www.eclipse.org/downloads/packages/installer에서 운영 체제에 맞는 Eclipse 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-105">Download the Eclipse version that suits your operating system from http://www.eclipse.org/downloads/packages/installer.</span></span>
2. <span data-ttu-id="48954-106">다운로드한 후 Eclipse 설치 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-106">Start the Eclipse installer once downloaded.</span></span>

    1. <span data-ttu-id="48954-107">Windows에서 다운로드한 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-107">On Windows, double-click the downloaded file.</span></span>
    2. <span data-ttu-id="48954-108">macOS 및 Linux에서, 다운로드된 파일의 설치 관리자 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="48954-108">On macOS and Linux, unzip the installer from the downloaded file.</span></span> <span data-ttu-id="48954-109">압축이 풀리면 설치 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-109">Then start the installer once unzipped.</span></span>

        > [!NOTE]
        > <span data-ttu-id="48954-110">Java Development Kit가 누락된 경우 설치 관리자에서 설치하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-110">The installer may prompt you to install the Java Development Kit, if it is missing.</span></span>

3. <span data-ttu-id="48954-111">설치할 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-111">Select the packages to install.</span></span> <span data-ttu-id="48954-112">Java 개발자의 경우 Java 또는 Java EE Eclipse IDE 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-112">For Java developers, choose either the Java or Java EE Eclipse IDE option.</span></span>
4. <span data-ttu-id="48954-113">머신에서 설치 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-113">Select the installation destination on your machine.</span></span>
5. <span data-ttu-id="48954-114">Eclipse를 시작하여 제대로 설치되었는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-114">Launch Eclipse to validate that it installed correctly.</span></span>

## <a name="install-azure-toolkit-for-eclipse"></a><span data-ttu-id="48954-115">Eclipse용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="48954-115">Install Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="48954-116">Azure Toolkit는 Windows, macOS 및 Linux에서 동일하게 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="48954-116">Installing the Azure Toolkit is the same across Windows, macOS, and Linux.</span></span>

1. <span data-ttu-id="48954-117">Eclipse를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-117">Start Eclipse.</span></span>
2. <span data-ttu-id="48954-118">**도움말** > **새 소프트웨어 설치...** 로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-118">Go to **Help** > **Install New Software...**.</span></span>

    <span data-ttu-id="48954-119">다음 스크린샷은 **새 소프트웨어 설치...** 항목의 메뉴 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="48954-119">The following screenshot shows the menu location of the **Install New Software...** item.</span></span>

    ![Eclipse 도움말 메뉴에 새 소프트웨어 설치 옵션이 강조되어 있는 스크린샷입니다.](../media/7-eclipse-install-new-software.png)

3. <span data-ttu-id="48954-121">**사용 가능한 소프트웨어** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="48954-121">The **Available Software** dialog will open.</span></span> <span data-ttu-id="48954-122">**작업:** 텍스트 상자에 `http://dl.microsoft.com/eclipse/`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="48954-122">In the **Work with:** text box, type `http://dl.microsoft.com/eclipse/` and press Enter.</span></span>
4. <span data-ttu-id="48954-123">결과에서 **Azure Toolkit for Java** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-123">In the results, check the **Azure Toolkit for Java** option.</span></span> <span data-ttu-id="48954-124">**Contact all update sites during install to find required software**(설치 중 모든 업데이트 사이트에 문의하여 필요한 소프트웨어 찾기) 옵션이 선택 취소되어 있지 않은 경우 선택 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-124">Make sure you uncheck the **Contact all update sites during install to find required software** option, if it isn't already.</span></span>

    <span data-ttu-id="48954-125">다음 스크린샷은 위에 설명된 **사용 가능한 소프트웨어** 설치 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="48954-125">The following screenshot shows the **Available Software** install configuration as described above.</span></span>

    ![Azure Toolkit for Java를 찾아 설치하는 데 필요한 구성이 강조되어 있는 상자가 포함된 Eclipse의 사용 가능한 소프트웨어 창 스크린샷입니다.](../media/7-eclipse-download-azure-toolkit-for-java.png)

5. <span data-ttu-id="48954-127">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-127">Click **Next**.</span></span>
6. <span data-ttu-id="48954-128">메시지가 표시되면 사용권 계약을 검토 및 동의하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-128">Review and accept the license agreements when prompted, and click **Finish**.</span></span>
7. <span data-ttu-id="48954-129">Eclipse는 Azure Toolkit를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-129">Eclipse will download and install the Azure Toolkit.</span></span>
8. <span data-ttu-id="48954-130">필요한 경우 Eclipse를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-130">Restart Eclipse if required.</span></span>
9. <span data-ttu-id="48954-131">Eclipse에서 **도구** > **Azure** 메뉴 옵션을 찾을 수 있는지 확인하여 Azure Toolkit 설치 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="48954-131">Validate installation of Azure Toolkit by verifying that you can find a **Tools** > **Azure** menu option in Eclipse.</span></span>

## <a name="summary"></a><span data-ttu-id="48954-132">요약</span><span class="sxs-lookup"><span data-stu-id="48954-132">Summary</span></span>

<span data-ttu-id="48954-133">이 단원에서는 Java용 Eclipse를 설치하고 Azure 서비스 및 제품과 통합하여 활용할 수 있도록 준비했습니다.</span><span class="sxs-lookup"><span data-stu-id="48954-133">In this unit, you installed Eclipse for Java, and prepared it to take advantage of the integration with Azure services and products.</span></span> <span data-ttu-id="48954-134">설치가 빠르고 간편한 Eclipse는 클라우드 서비스 통합을 통한 Java 개발 작업에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="48954-134">The installation is quick and straightforward, making Eclipse ideal for the task of Java development with cloud services integration.</span></span>
