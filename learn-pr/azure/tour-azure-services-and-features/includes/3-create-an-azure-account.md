<span data-ttu-id="1ead4-101">Azure 체험 계정을 사용하면 엔터프라이즈 응용 프로그램을 빌드, 테스트 및 배포하고 사용자 지정 웹 및 모바일 환경을 만들며 기계 학습 및 강력한 분석을 통해 데이터에서 통찰력을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-101">With a free Azure account, you can build, test, and deploy enterprise applications, create custom web and mobile experiences, and gain insights from your data through machine learning and powerful analytics.</span></span>

## <a name="what-is-an-azure-account"></a><span data-ttu-id="1ead4-102">Azure 계정이란?</span><span class="sxs-lookup"><span data-stu-id="1ead4-102">What is an Azure account?</span></span>

<span data-ttu-id="1ead4-103">_Azure 계정_은 특정 ID와 연결되며 다음과 같은 정보를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-103">An _Azure account_ is tied to a specific identity and holds information like:</span></span>

- <span data-ttu-id="1ead4-104">이름, 이메일 및 연락처 기본 설정</span><span class="sxs-lookup"><span data-stu-id="1ead4-104">Name, email, and contact preferences</span></span>
- <span data-ttu-id="1ead4-105">신용 카드와 같은 대금 청구 정보</span><span class="sxs-lookup"><span data-stu-id="1ead4-105">Billing information such as a credit card</span></span>

<span data-ttu-id="1ead4-106">Azure 계정은 하나 이상의 _구독_과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-106">An Azure account is associated with one more  _subscriptions_.</span></span>

## <a name="what-is-an-azure-subscription"></a><span data-ttu-id="1ead4-107">Azure 구독이란?</span><span class="sxs-lookup"><span data-stu-id="1ead4-107">What is an Azure subscription?</span></span>

<span data-ttu-id="1ead4-108">_Azure 구독_은 Microsoft Azure에서 리소스를 프로비전하는 데 사용되는 논리적인 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-108">An _Azure subscription_ is a logical container used to provision resources in Microsoft Azure.</span></span> <span data-ttu-id="1ead4-109">가상 머신, 데이터베이스 등 모든 리소스에 대한 세부 정보를 보유합니다. 또한 구독에 포함된 리소스에 대한 사용자 및 역할을 인증하는 데 사용되는 단일 Azure AD _테넌트_와 트러스트 관계를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-109">It holds the details of all your resources like virtual machines, databases, etc. It also has a trust relationship to a single Azure AD _tenant_ which is used to authenticate users and roles for the resources held in the subscription.</span></span>

<span data-ttu-id="1ead4-110">대금 청구는 구독 수준에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-110">Billing occurs at the subscription level.</span></span> <span data-ttu-id="1ead4-111">월말에 놀라지 않도록 각 구독에 대한 지출 한도를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-111">You can set spending limits on each subscription to ensure you aren't surprised at the end of the month.</span></span> 

## <a name="what-is-an-azure-ad-tenant"></a><span data-ttu-id="1ead4-112">Azure AD 테넌트란?</span><span class="sxs-lookup"><span data-stu-id="1ead4-112">What is an Azure AD tenant?</span></span>

<span data-ttu-id="1ead4-113">Azure AD(Azure Active Directory)는 클라우드에서 응용 프로그램 및 서비스를 보호하기 위해 여러 인증 프로토콜을 지원하는 최신 ID 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-113">Azure AD (Azure Active Directory) is a modern identity provider that supports multiple authentication protocols to secure applications and services in the cloud.</span></span> <span data-ttu-id="1ead4-114">Windows 데스크톱 및 서버 보안에 중점을 둔 Windows Active Directory와 같지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="1ead4-114">It's _not_ the same as Windows Active Directory, which is focused on securing Windows desktops and servers.</span></span> <span data-ttu-id="1ead4-115">대신, Azure AD는 OpenID 및 OAuth와 같은 웹 기반 인증 표준에 관한 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-115">Instead, Azure AD is all about web-based authentication standards such as OpenID and OAuth.</span></span>

<span data-ttu-id="1ead4-116">단일 테넌트는 논리적 조직을 나타내며 여러 ID가 해당 테넌트에 의해 보호되는 리소스에 액세스하고 리소스를 활용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-116">A single tenant represents a logical organization and allows multiple identities to access and utilize resources protected by that tenant.</span></span> <span data-ttu-id="1ead4-117">Azure 구독은 항상 _단일_ Azure AD 테넌트와 트러스트 관계를 갖지만 _여러_ 구독이 단일 테넌트를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-117">An Azure subscription always has a trust relationship with a _single_ Azure AD tenant, but _multiple_ subscriptions can share a single tenant.</span></span> <span data-ttu-id="1ead4-118">이 구조를 통해 조직이 여러 구독을 관리하고 구독 내에 포함된 모든 리소스 간에 보안 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-118">This structure allows the organization to manage multiple subscriptions and set security rules across all the resources contained within them.</span></span>

<span data-ttu-id="1ead4-119">다음은 계정, 구독, 테넌트 및 리소스를 간단하게 나타낸 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-119">Here's a simple representation of accounts, subscriptions, tenants, and resources.</span></span>

![계정, 테넌트, 구독 및 리소스가 어떻게 함께 작동하는지에 대한 다이어그램](../media/3-azure-ad-tenant.png)

<span data-ttu-id="1ead4-121">각 Azure AD 테넌트에는 _계정 소유자_가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-121">Notice that each Azure AD tenant has an _account owner_.</span></span> <span data-ttu-id="1ead4-122">이것은 청구를 담당하는 원래 Azure 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-122">This is the original Azure account that is responsible for billing.</span></span> <span data-ttu-id="1ead4-123">테넌트에 사용자를 더 추가할 수 있으며 다른 Azure AD 테넌트의 게스트를 초대하여 구독 중인 리소스에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-123">You can add additional users to the tenant, and even invite guests from other Azure AD tenants to access resources in subscriptions.</span></span>

## <a name="azure-account-types"></a><span data-ttu-id="1ead4-124">Azure 계정 유형</span><span class="sxs-lookup"><span data-stu-id="1ead4-124">Azure account types</span></span>

<span data-ttu-id="1ead4-125">Azure는 여러 고객 유형에 맞는 여러 가지 계정 유형을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-125">Azure has several account types that cater to different customer types.</span></span> <span data-ttu-id="1ead4-126">가장 일반적으로 사용되는 계정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-126">The most commonly used accounts are:</span></span>

- <span data-ttu-id="1ead4-127">체험</span><span class="sxs-lookup"><span data-stu-id="1ead4-127">Free</span></span>
- <span data-ttu-id="1ead4-128">Pay-As-You-Go</span><span class="sxs-lookup"><span data-stu-id="1ead4-128">Pay-As-You-Go</span></span>
- <span data-ttu-id="1ead4-129">기업 계약</span><span class="sxs-lookup"><span data-stu-id="1ead4-129">Enterprise Agreement</span></span>

### <a name="azure-free-account"></a><span data-ttu-id="1ead4-130">Azure 체험 계정</span><span class="sxs-lookup"><span data-stu-id="1ead4-130">Azure free account</span></span>

<span data-ttu-id="1ead4-131">Azure 체험 계정에는 처음 30일 동안 사용할 수 있는 **$200 크레딧**, 12개월 동안 가장 인기 있는 Azure 제품에 무료로 액세스할 수 있는 권한, 항상 무료로 사용할 수 있는 25개 초과 제품에 액세스할 수 있는 권한이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-131">An Azure free account includes a **$200 credit** to spend for the first 30 days, free access to the most popular Azure products for 12 months, and access to more than 25 products that are always free.</span></span> <span data-ttu-id="1ead4-132">신규 사용자에게 매우 유용한 시작 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-132">This is an excellent way for new users to get started.</span></span> <span data-ttu-id="1ead4-133">체험 계정을 설정하려면 전화 번호, 신용 카드, Microsoft 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-133">To set up a free account, you need a phone number, a credit card, and a Microsoft account.</span></span>

> [!NOTE]
> <span data-ttu-id="1ead4-134">신용 카드 정보는 ID 검증용으로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-134">Credit card information is used for identity verification only.</span></span> <span data-ttu-id="1ead4-135">업그레이드하기 전에는 서비스 비용이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-135">You won’t be charged for any services until you upgrade.</span></span>

### <a name="azure-pay-as-you-go-account"></a><span data-ttu-id="1ead4-136">Azure 종량제 계정</span><span class="sxs-lookup"><span data-stu-id="1ead4-136">Azure Pay-As-You-Go account</span></span>

<span data-ttu-id="1ead4-137">PAYG(종량제) 계정은 사용한 서비스에 대해 매월 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-137">A Pay-As-You-Go (PAYG) account bills you monthly for the services you used.</span></span> <span data-ttu-id="1ead4-138">이 계정 유형은 개인에서 중소기업 및 여러 대기업에 이르기까지 광범위한 사용자에게 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-138">This account type is appropriate for a wide range of users, from individuals to small businesses and many large organizations as well.</span></span>

### <a name="azure-enterprise-agreement"></a><span data-ttu-id="1ead4-139">Azure 기업계약</span><span class="sxs-lookup"><span data-stu-id="1ead4-139">Azure Enterprise Agreement</span></span>

<span data-ttu-id="1ead4-140">기업계약에서는 하나의 계약으로 새 라이선스와 Software Assurance에 대한 할인을 받아 클라우드 서비스 및 소프트웨어 라이선스를 유연하게 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-140">An Enterprise Agreement provides flexibility to buy cloud services and software licenses under one agreement, with discounts for new licenses and Software Assurance.</span></span> <span data-ttu-id="1ead4-141">엔터프라이즈급 조직을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-141">It is targeted at enterprise-scale organizations.</span></span>

## <a name="summary"></a><span data-ttu-id="1ead4-142">요약</span><span class="sxs-lookup"><span data-stu-id="1ead4-142">Summary</span></span>

<span data-ttu-id="1ead4-143">개인이든, 중소기업이든, 대기업이든, Azure 서비스를 사용하려면 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-143">Whether you are an individual, a small business, or an enterprise, you need an account to use Azure services.</span></span> <span data-ttu-id="1ead4-144">일반적으로 Azure 서비스를 평가할 수 있도록 체험 계정으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-144">The typical sequence is to start with a free account so that you can evaluate Azure services.</span></span> <span data-ttu-id="1ead4-145">평가 기간이 만료되면 체험 계정에서 종량제로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ead4-145">When your trial period expires, you will convert from the free account to Pay-As-You-Go.</span></span>