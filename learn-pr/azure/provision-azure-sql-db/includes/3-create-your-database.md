<span data-ttu-id="df302-101">귀하의 운송 회사는 큰 비용을 들이지 않으면서 타사와 차별화를 꾀하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-101">Your transportation company wants to set themselves apart from other companies but without breaking the bank.</span></span> <span data-ttu-id="df302-102">비용을 관리하면서 최상의 서비스를 제공하도록 데이터베이스를 설정하는 방법에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-102">You must have a good handle on how to set up the database to provide the best service while controlling costs.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="df302-103">여기서는 다음 내용을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-103">Here, you'll learn:</span></span>

- <span data-ttu-id="df302-104">Azure SQL Database를 만들 때 고려해야 할 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-104">What considerations you need to make when creating an Azure SQL database, including:</span></span>
  - <span data-ttu-id="df302-105">논리 서버가 데이터베이스의 관리 컨테이너 역할을 하는 방식</span><span class="sxs-lookup"><span data-stu-id="df302-105">How a logical server acts as an administrative container for your databases.</span></span>
  - <span data-ttu-id="df302-106">구매 모델 간 차이점</span><span class="sxs-lookup"><span data-stu-id="df302-106">The differences between purchasing models.</span></span>
  - <span data-ttu-id="df302-107">탄력적 풀을 사용하여 데이터베이스 간에 처리 성능을 공유하는 방법</span><span class="sxs-lookup"><span data-stu-id="df302-107">How elastic pools enable you to share processing power among databases.</span></span>
  - <span data-ttu-id="df302-108">데이터 정렬 규칙이 데이터의 비교 및 정렬 방법에 영향을 주는 방식</span><span class="sxs-lookup"><span data-stu-id="df302-108">How collation rules affect how data is compared and sorted.</span></span>
- <span data-ttu-id="df302-109">포털에서 Azure SQL Database를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="df302-109">How to bring up Azure SQL Database from the portal.</span></span>
- <span data-ttu-id="df302-110">신뢰받는 원본에서만 데이터베이스에 액세스할 수 있도록 방화벽 규칙을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="df302-110">How to add firewall rules so that your database is accessible from only trusted sources.</span></span>

<span data-ttu-id="df302-111">Azure SQL Database를 만들 때 고려해야 하는 몇 가지 사항을 간단히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-111">Let's take a quick look at some things you need to consider when you create an Azure SQL database.</span></span>

## <a name="one-server-many-databases"></a><span data-ttu-id="df302-112">하나의 서버, 여러 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="df302-112">One server, many databases</span></span>

<span data-ttu-id="df302-113">첫 번째 Azure SQL Database를 만들 때 _Azure SQL 논리 서버_도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df302-113">When you create your first Azure SQL database, you also create an _Azure SQL logical server_.</span></span> <span data-ttu-id="df302-114">논리 서버를 데이터베이스의 관리 컨테이너로 생각해보세요.</span><span class="sxs-lookup"><span data-stu-id="df302-114">Think of a logical server as an administrative container for your databases.</span></span> <span data-ttu-id="df302-115">논리 서버를 통해 로그인, 방화벽 규칙 및 보안 정책을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-115">You can control logins, firewall rules, and security policies through the logical server.</span></span> <span data-ttu-id="df302-116">또한 논리 서버의 각 데이터베이스에서 이러한 정책을 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-116">You can also override these policies on each database within the logical server.</span></span>

<span data-ttu-id="df302-117">지금은 데이터베이스가 하나만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df302-117">For now, you need just one database.</span></span> <span data-ttu-id="df302-118">그러나 논리 서버를 사용하여 나중에 데이터베이스를 더 추가하고, 모든 데이터베이스에서 성능을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-118">But a logical server enables you to add more later and tune performance among all your databases.</span></span>

## <a name="choose-performance-dtus-versus-vcores"></a><span data-ttu-id="df302-119">성능 선택: DTU 대 vCore</span><span class="sxs-lookup"><span data-stu-id="df302-119">Choose performance: DTUs versus vCores</span></span>

<span data-ttu-id="df302-120">Azure SQL Database에는 두 가지 구매 모델 DTU 및 vCore가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-120">Azure SQL Database has two purchasing models: DTU and vCore.</span></span>

### <a name="what-are-dtus"></a><span data-ttu-id="df302-121">DTU란?</span><span class="sxs-lookup"><span data-stu-id="df302-121">What are DTUs?</span></span>

<span data-ttu-id="df302-122">DTU는 데이터베이스 트랜잭션 단위를 나타내며 계산, 저장소 및 IO 리소스가 결합된 측정값입니다.</span><span class="sxs-lookup"><span data-stu-id="df302-122">DTU stands for Database Transaction Unit and is a combined measure of compute, storage, and IO resources.</span></span> <span data-ttu-id="df302-123">DTU 모델을 미리 구성된 단순한 구매 옵션으로 생각하세요.</span><span class="sxs-lookup"><span data-stu-id="df302-123">Think of the DTU model as a simple, preconfigured purchase option.</span></span>

<span data-ttu-id="df302-124">논리 서버가 하나를 초과하는 데이터베이스를 보유할 수 있으므로, eDTU 또는 탄력적 데이터베이스 트랜잭션 단위 개념도 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-124">Because your logical server can hold more than one database, there's also the idea of eDTUs, or elastic Database Transaction Units.</span></span> <span data-ttu-id="df302-125">이 옵션을 사용하면 한 가지 가격을 선택할 수 있지만, 풀의 각 데이터베이스가 현재 부하에 따라 더 적거나 더 많은 리소스를 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-125">This option enables you to choose one price, but allow each database in the pool to consume fewer or greater resources depending on current load.</span></span>

### <a name="what-are-vcores"></a><span data-ttu-id="df302-126">vCore란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="df302-126">What are vCores?</span></span>

<span data-ttu-id="df302-127">vCore는 만들고 비용을 지불하는 계산 및 저장소 리소스를 보다 강력하게 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-127">vCore gives you greater control over what compute and storage resources you create and pay for.</span></span>

<span data-ttu-id="df302-128">DTU 모델은 고정된 계산, 저장소 및 IO 리소스 조합을 제공하지만 vCore 모델을 사용하여 리소스를 독립적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-128">While the DTU model provides fixed combinations of compute, storage, and IO resources, the vCore model enables you to configure resources independently.</span></span> <span data-ttu-id="df302-129">예를 들어, vCore 모델을 사용하여 저장소 용량을 늘리면서 계산 및 IO 처리량은 기존 상태로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-129">For example, with the vCore model you can increase storage capacity but keep the existing amount of compute and IO throughput.</span></span>

<span data-ttu-id="df302-130">운송 및 물류 프로토타입에는 하나의 Azure SQL Database 인스턴스만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-130">Your transportation and logistics prototype only needs one Azure SQL Database instance.</span></span> <span data-ttu-id="df302-131">DTU 옵션은 계산, 저장소 및 IO 성능의 적절한 균형을 제공하고 초기 비용이 덜 들기 때문에 사용하기로 결정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-131">You decide on the DTU option because it provides a good balance of compute, storage, and IO performance and is less expensive to get started.</span></span>

## <a name="what-are-sql-elastic-pools"></a><span data-ttu-id="df302-132">SQL 탄력적 풀이란?</span><span class="sxs-lookup"><span data-stu-id="df302-132">What are SQL elastic pools?</span></span>

<span data-ttu-id="df302-133">Azure SQL 데이터베이스를 만들 때 _SQL 탄력적 풀_을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-133">When you create your Azure SQL database, you can create a _SQL elastic pool_.</span></span>

<span data-ttu-id="df302-134">SQL 탄력적 풀은 eDTU와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-134">SQL elastic pools relate to eDTUs.</span></span> <span data-ttu-id="df302-135">이 풀을 사용하면 풀의 모든 데이터베이스에서 공유되는 계산 및 저장소 리소스 집합을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-135">They enable you to buy a set of compute and storage resources that are shared among all the databases in the pool.</span></span> <span data-ttu-id="df302-136">각 데이터베이스는 현재 부하에 따라 설정한 한도 내에서 필요한 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-136">Each database can use the resources they need, within the limits you set, depending on current load.</span></span>

<span data-ttu-id="df302-137">프로토타입의 경우 하나의 SQL 데이터베이스만 필요하므로 SQL 탄력적 풀이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-137">For your prototype, you won't need a SQL elastic pool because you need only one SQL database.</span></span>

## <a name="what-is-collation"></a><span data-ttu-id="df302-138">데이터 정렬이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="df302-138">What is collation?</span></span>

<span data-ttu-id="df302-139">데이터 정렬은 데이터를 정렬하고 비교하는 규칙을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-139">Collation refers to the rules that sort and compare data.</span></span> <span data-ttu-id="df302-140">데이터 정렬은 대/소문자 구분, 악센트 표시 및 기타 언어 특성이 중요한 경우 정렬 규칙을 정의하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df302-140">Collation helps you define sorting rules when case sensitivity, accent marks, and other language characteristics are important.</span></span>

<span data-ttu-id="df302-141">기본 데이터 정렬인 **SQL_Latin1_General_CP1_CI_AS**가 무엇을 의미하는지 잠시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-141">Let's take a moment to consider what the default collation, **SQL_Latin1_General_CP1_CI_AS**, means.</span></span>

- <span data-ttu-id="df302-142">**Latin1_General**은 서부 유럽 언어 제품군을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="df302-142">**Latin1_General** refers to the family of Western European languages.</span></span>
- <span data-ttu-id="df302-143">**CP1**은 라틴 알파벳의 인기 있는 문자 인코딩인 코드 페이지 1252를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="df302-143">**CP1** refers to code page 1252, a popular character encoding of the Latin alphabet.</span></span>
- <span data-ttu-id="df302-144">**CI**는 비교가 대/소문자를 구분하지 않음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-144">**CI** means that comparisons are case insensitive.</span></span> <span data-ttu-id="df302-145">예를 들어, “HELLO”는 “hello”와 동일한 것으로 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="df302-145">For example, "HELLO" compares equally to "hello".</span></span>
- <span data-ttu-id="df302-146">**AS**는 비교가 악센트를 구분함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-146">**AS** means that comparisons are accent sensitive.</span></span> <span data-ttu-id="df302-147">예를 들어 “résumé”는 “resume”와 동일한 것으로 비교되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-147">For example, "résumé" doesn't compare equally to "resume".</span></span>

<span data-ttu-id="df302-148">데이터의 정렬 및 비교 방법에 대한 특정 요구 사항이 없으므로 기본 데이터 정렬을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-148">Because you don't have specific requirements around how data is sorted and compared, you choose the default collation.</span></span>

## <a name="create-your-azure-sql-database"></a><span data-ttu-id="df302-149">Azure SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="df302-149">Create your Azure SQL database</span></span>

<span data-ttu-id="df302-150">여기서는 논리 서버 생성을 포함하는 데이터베이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-150">Here you'll set up your database, which includes creating your logical server.</span></span> <span data-ttu-id="df302-151">운송 물류 응용 프로그램을 지원하는 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-151">You'll choose settings that support your transportation logistics application.</span></span> <span data-ttu-id="df302-152">실제로 빌드하는 앱의 종류를 지원하는 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-152">In practice, you would choose settings that support the kind of app you're building.</span></span>

<span data-ttu-id="df302-153">시간이 지남에 따라 수요에 대처하기 위해 추가 계산 성능이 필요하다는 것을 알게 되면 성능 옵션을 조정하거나 DTU와 vCore 성능 모델을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-153">Over time if you you realize you need additional compute power to keep up with demand, you can adjust performance options or even switch between the DTU and vCore performance models.</span></span>

1. <span data-ttu-id="df302-154">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-154">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="df302-155">포털의 왼쪽 위 모서리에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-155">From the portal, click **Create a resource** from the upper left-hand corner.</span></span> <span data-ttu-id="df302-156">**데이터베이스**를 선택한 다음, **SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-156">Select **Databases**, then select **SQL Database**.</span></span>

   ![데이터베이스 섹션을 선택하고 리소스 만들기, 데이터베이스 및 SQL Database 단추가 강조 표시된 리소스 만들기 블레이드를 보여주는 Azure Portal 스크린샷입니다.](../media/3-create-db.png)

1. <span data-ttu-id="df302-158">**서버**에서 **필수 설정 구성**을 클릭하고, 양식을 채운 다음, **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-158">Under **Server**, click **Configure required settings**, fill out the form, then click **Select**.</span></span> <span data-ttu-id="df302-159">양식을 채우는 방법에 대한 자세한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-159">Here's more information on how to fill out the form:</span></span>

    | <span data-ttu-id="df302-160">설정</span><span class="sxs-lookup"><span data-stu-id="df302-160">Setting</span></span>      | <span data-ttu-id="df302-161">값</span><span class="sxs-lookup"><span data-stu-id="df302-161">Value</span></span> |
    | ------------ | ----- |
    | <span data-ttu-id="df302-162">**서버 이름**</span><span class="sxs-lookup"><span data-stu-id="df302-162">**Server name**</span></span> | <span data-ttu-id="df302-163">전역적으로 고유한 [서버 이름](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)입니다.</span><span class="sxs-lookup"><span data-stu-id="df302-163">A globally unique [server name](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
    | <span data-ttu-id="df302-164">**서버 관리자 로그인**</span><span class="sxs-lookup"><span data-stu-id="df302-164">**Server admin login**</span></span> | <span data-ttu-id="df302-165">기본 관리자 로그인 이름으로 사용되는 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)입니다.</span><span class="sxs-lookup"><span data-stu-id="df302-165">A [database identifier](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) that serves as your primary administrator login name.</span></span> |
    | <span data-ttu-id="df302-166">**암호**</span><span class="sxs-lookup"><span data-stu-id="df302-166">**Password**</span></span> | <span data-ttu-id="df302-167">대문자, 소문자, 숫자 및 영숫자가 아닌 문자 범주 중 세 가지 범주의 문자를 포함하는 8자 이상의 유효한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="df302-167">Any valid password that has at least eight characters and contains characters from three of these categories: uppercase characters, lowercase characters, numbers, and non-alphanumeric characters.</span></span> |
    | <span data-ttu-id="df302-168">**위치**</span><span class="sxs-lookup"><span data-stu-id="df302-168">**Location**</span></span> | <span data-ttu-id="df302-169">아래 목록의 유효한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="df302-169">Any valid location from the available list below.</span></span> |

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="df302-170">**가격 책정 계층**을 클릭하여 서비스 계층을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-170">Click **Pricing tier** to specify the service tier.</span></span> <span data-ttu-id="df302-171">**기본** 서비스 계층을 선택한 다음, **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-171">Select the **Basic** service tier, then click **Apply**.</span></span>

1. <span data-ttu-id="df302-172">다음 값을 사용하여 나머지 양식을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="df302-172">Use these values to fill out the rest of the form.</span></span>

    | <span data-ttu-id="df302-173">설정</span><span class="sxs-lookup"><span data-stu-id="df302-173">Setting</span></span>      | <span data-ttu-id="df302-174">값</span><span class="sxs-lookup"><span data-stu-id="df302-174">Value</span></span> |
    | ------------ | ----- |
    | <span data-ttu-id="df302-175">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="df302-175">**Database name**</span></span> | <span data-ttu-id="df302-176">**물류**</span><span class="sxs-lookup"><span data-stu-id="df302-176">**Logistics**</span></span> |
    | <span data-ttu-id="df302-177">**구독**</span><span class="sxs-lookup"><span data-stu-id="df302-177">**Subscription**</span></span> | <span data-ttu-id="df302-178">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="df302-178">Your subscription</span></span> |
    | <span data-ttu-id="df302-179">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="df302-179">**Resource group**</span></span> |  <span data-ttu-id="df302-180">기존 그룹 <rgn>[샌드박스 리소스 그룹 이름]</rgn> 사용</span><span class="sxs-lookup"><span data-stu-id="df302-180">Use the existing group <rgn>[Sandbox resource group name]</rgn></span></span> |
    | <span data-ttu-id="df302-181">**원본 선택**</span><span class="sxs-lookup"><span data-stu-id="df302-181">**Select source**</span></span> | <span data-ttu-id="df302-182">**빈 데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="df302-182">**Blank database**</span></span> |
    | <span data-ttu-id="df302-183">**SQL 탄력적 풀을 사용하고 싶나요?**</span><span class="sxs-lookup"><span data-stu-id="df302-183">**Want to use SQL elastic pool?**</span></span> | <span data-ttu-id="df302-184">**지금은 아님**</span><span class="sxs-lookup"><span data-stu-id="df302-184">**Not now**</span></span> |
    | <span data-ttu-id="df302-185">**데이터 정렬**</span><span class="sxs-lookup"><span data-stu-id="df302-185">**Collation**</span></span> | <span data-ttu-id="df302-186">**SQL_Latin1_General_CP1_CI_AS**</span><span class="sxs-lookup"><span data-stu-id="df302-186">**SQL_Latin1_General_CP1_CI_AS**</span></span> |

1. <span data-ttu-id="df302-187">**만들기**를 클릭하여 Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df302-187">Click **Create** to create your Azure SQL database.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="df302-188">나중에 사용할 수 있도록 서버 이름, 관리자 로그인 및 암호를 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-188">Remember your server name, admin login, and password for later.</span></span>

1. <span data-ttu-id="df302-189">도구 모음에서 **알림**을 클릭하여 배포 프로세스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-189">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

<span data-ttu-id="df302-190">프로세스가 완료되면 **대시보드에 고정**을 클릭하여 나중에 필요할 때 빠르게 액세스할 수 있도록 대시보드에 데이터베이스 서버를 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-190">When the process completes, click **Pin to dashboard** to pin your database server to the dashboard so that you have quick access when you need it later.</span></span>

   ![강조 표시된 최근 배포 성공 메시지에서 대시보드에 고정 단추를 사용하여 알림 메뉴를 보여주는 Azure Portal 스크린샷입니다.](../media/3-notifications-complete.png)

## <a name="set-the-server-firewall"></a><span data-ttu-id="df302-192">서버 방화벽 설정</span><span class="sxs-lookup"><span data-stu-id="df302-192">Set the server firewall</span></span>

<span data-ttu-id="df302-193">이제 Azure SQL 데이터베이스가 작동 및 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-193">Your Azure SQL database is now up and running.</span></span> <span data-ttu-id="df302-194">새 데이터베이스의 추가 구성, 보안 설정, 모니터링 및 문제 해결을 위한 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-194">You have many options to further configure, secure, monitor, and troubleshoot your new database.</span></span>

<span data-ttu-id="df302-195">방화벽을 통해 데이터베이스에 액세스할 수 있는 시스템을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-195">You can also specify which systems can access your database through the firewall.</span></span> <span data-ttu-id="df302-196">처음에는 방화벽이 Azure 외부에서 사용자 데이터베이스 서버로 시도되는 모든 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-196">Initially, the firewall prevents all access to your database server from outside of Azure.</span></span>

<span data-ttu-id="df302-197">프로토타입의 경우 사용자의 랩톱에서만 데이터베이스에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-197">For your prototype, you only need to access the database from your laptop.</span></span> <span data-ttu-id="df302-198">나중에 모바일 앱과 같은 추가 시스템을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-198">Later, you can whitelist additional systems, such as your mobile app.</span></span>

<span data-ttu-id="df302-199">지금은 개발 컴퓨터를 사용하여 방화벽을 통해 데이터베이스에 액세스하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-199">Let's enable your development computer to access the database through the firewall now.</span></span>

1. <span data-ttu-id="df302-200">Logistics 데이터베이스의 개요 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-200">Go to the overview blade of the Logistics database.</span></span> <span data-ttu-id="df302-201">이전에 데이터베이스를 고정한 경우 대시보드에서 **물류** 타일을 클릭하여 해당 타일로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df302-201">If you pinned the database earlier, you can click the **Logistics** tile on the dashboard to get there.</span></span>

1. <span data-ttu-id="df302-202">**서버 방화벽 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-202">Click **Set server firewall**.</span></span>

    ![서버 방화벽 설정 단추가 강조 표시된 SQL 데이터베이스 개요 블레이드를 보여주는 Azure Portal 스크린샷입니다.](../media/3-set-server-firewall.png)

1. <span data-ttu-id="df302-204">**클라이언트 IP 추가**를 클릭한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-204">Click **Add client IP**, and then click **Save**.</span></span>

    ![클라이언트IP 추가 단추가 강조 표시된 SQL 데이터베이스 방화벽 설정 블레이드를 보여주는 Azure Portal 스크린샷입니다.](../media/3-add-client-ip.png)

<span data-ttu-id="df302-206">다음 파트에서는 새 데이터베이스와 Azure Cloud Shell을 사용하여 몇 가지 실습을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="df302-206">In the next part, you'll get some hands-on practice with your new database and with Azure Cloud Shell.</span></span> <span data-ttu-id="df302-207">데이터베이스에 연결하고, 테이블을 만들고, 일부 샘플 데이터를 추가하고, 몇 가지 SQL 문을 실행해봅니다.</span><span class="sxs-lookup"><span data-stu-id="df302-207">You'll connect to the database, create a table, add some sample data, and execute a few SQL statements.</span></span>