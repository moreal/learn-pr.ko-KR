<span data-ttu-id="cb64a-101">응용 프로그램을 클라우드 플랫폼에 호스트하면 기존 온-프레미스 배포보다 훨씬 많은 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-101">Hosting applications on a cloud platform provides a number of advantages when compared to traditional on-premises deployments.</span></span> <span data-ttu-id="cb64a-102">클라우드의 공유 책임 모델은 클라우드 공급자의 제어 하에서 물리적 네트워크, 빌딩 및 호스트 수준에서 보안을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-102">The cloud's shared-responsibility model moves security at the physical network, building and host levels under the control of the cloud provider.</span></span> <span data-ttu-id="cb64a-103">이 수준에서 플랫폼을 약화시키려고 시도하는 공격자는 얻는 것이 점점 줄어드는 데 반해, 공급자는 인프라를 보호하고 모니터링하기 위해 상장한 투자를 하고 인사이트를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-103">An attacker trying to compromise the platform at this level would see diminishing returns versus the considerable investment and insight providers make in securing and monitoring their infrastructure.</span></span>

<span data-ttu-id="cb64a-104">그러므로 공격자는 응용 프로그램 수준에서 클라우드 플랫폼 고객 때문에 생기는 취약성을 노리는 것이 훨씬 더 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-104">It's therefore far more effective for attackers to pursue vulnerabilities introduced at the application level by cloud-platform customers.</span></span> <span data-ttu-id="cb64a-105">또한 PaaS(Platform as a Service)를 도입하여 응용 프로그램을 호스트하는 고객은 운영 체제 보안을 관리하는 데 사용되는 리소스를 회수하여 응용 프로그램 코드를 강화하고 응용 프로그램 주변의 ID 경계를 모니터링하는 데 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-105">Furthermore, by adopting Platform as a Service (PaaS) to host their applications, customers are able to free resources from managing operating system security and deploy them to harden application code and monitor the identity perimeter around the application.</span></span> <span data-ttu-id="cb64a-106">이 섹션에서는 설계를 통해 응용 프로그램 보안을 강화하는 몇 가지 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-106">In this unit we will discuss some of the ways application security can be improved through design.</span></span>

## <a name="scenario"></a><span data-ttu-id="cb64a-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="cb64a-107">Scenario</span></span>

<span data-ttu-id="cb64a-108">Lamna Healthcare 고객은 온라인 웹 포털을 통해 개인 의료 기록에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-108">Lamna Healthcare customers require access to their personal medical records through an online web portal.</span></span> <span data-ttu-id="cb64a-109">HIPAA(Health Insurance Portability and Accountability Act)를 준수해야 하며, 개인 데이터 보안 위반이 발생하면 회사에 엄청난 재정적 처벌이 부과되므로 Lamna Healthcare가 취급하는 응용 프로그램 및 개인 데이터를 반드시 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-109">Compliance with the Health Insurance Portability and Accountability Act (HIPAA) is mandatory and puts the company at significant risk of financial penalties if a breach of personal data occurs, therefore securing the application and personal data it interacts with is paramount.</span></span>

<span data-ttu-id="cb64a-110">고객 응용 프로그램과 관련된 기본 영역은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-110">The primary areas that concern customer applications are:</span></span>

- <span data-ttu-id="cb64a-111">응용 프로그램 설계 보안</span><span class="sxs-lookup"><span data-stu-id="cb64a-111">Secure application design</span></span>
- <span data-ttu-id="cb64a-112">데이터 보안</span><span class="sxs-lookup"><span data-stu-id="cb64a-112">Data security</span></span>
- <span data-ttu-id="cb64a-113">ID 및 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="cb64a-113">Identity & access management</span></span>
- <span data-ttu-id="cb64a-114">엔드포인트 보안</span><span class="sxs-lookup"><span data-stu-id="cb64a-114">Endpoint security</span></span>

## <a name="security-development-lifecycle"></a><span data-ttu-id="cb64a-115">보안 개발 수명 주기</span><span class="sxs-lookup"><span data-stu-id="cb64a-115">Security Development Lifecycle</span></span>

<span data-ttu-id="cb64a-116">응용 프로그램 설계 단계에서 [Microsoft SDL(Security Development Lifecycle)](https://www.microsoft.com/en-us/sdl) 프로세스를 사용하여 소프트웨어 개발 수명 주기에 보안 문제를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-116">Microsoft's [Security Development Lifecycle](https://www.microsoft.com/en-us/sdl) (SDL) process can be used during the application design stage to ensure security concerns are incorporated in the software development lifecycle.</span></span> <span data-ttu-id="cb64a-117">보안 및 규정 준수 문제는 응용 프로그램을 설계할 때 훨씬 쉽게 해결할 수 있으며 최종 제품의 보안 결함으로 이어질 수 있는 여러 일반 오류를 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-117">Security and compliance issues are far easier to address when designing an application and can mitigate many common errors that can lead to security flaws in the final product.</span></span> <span data-ttu-id="cb64a-118">또한 소프트웨어 개발 과정의 초기에 문제를 해결하면 비용이 훨씬 적게 듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-118">Fixing issues early in the software development journey is also far less costly.</span></span> <span data-ttu-id="cb64a-119">소프트웨어 프로젝트에서 사용할 수는 SDL 단계의 일반적인 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-119">The typical sequence of SDL steps a software project can use are as follows:</span></span>

1. <span data-ttu-id="cb64a-120">교육</span><span class="sxs-lookup"><span data-stu-id="cb64a-120">Training</span></span>

    - <span data-ttu-id="cb64a-121">핵심 보안 교육</span><span class="sxs-lookup"><span data-stu-id="cb64a-121">Core security training</span></span>

1. <span data-ttu-id="cb64a-122">요구 사항</span><span class="sxs-lookup"><span data-stu-id="cb64a-122">Requirements</span></span>

    - <span data-ttu-id="cb64a-123">요구 사항 및 품질 게이트 정의</span><span class="sxs-lookup"><span data-stu-id="cb64a-123">Define requirements and quality gates</span></span>
    - <span data-ttu-id="cb64a-124">보안 및 개인 정보 위험 분석</span><span class="sxs-lookup"><span data-stu-id="cb64a-124">Analyze security & privacy risks</span></span>
 
1. <span data-ttu-id="cb64a-125">설계</span><span class="sxs-lookup"><span data-stu-id="cb64a-125">Design</span></span>

    - <span data-ttu-id="cb64a-126">공격 노출 영역 분석</span><span class="sxs-lookup"><span data-stu-id="cb64a-126">Attack surface analysis</span></span>
    - <span data-ttu-id="cb64a-127">위협 모델링</span><span class="sxs-lookup"><span data-stu-id="cb64a-127">Threat modelling</span></span>
 
1. <span data-ttu-id="cb64a-128">구현</span><span class="sxs-lookup"><span data-stu-id="cb64a-128">Implementation</span></span>

    - <span data-ttu-id="cb64a-129">코드 품질을 측정할 수 있도록 도구 지정</span><span class="sxs-lookup"><span data-stu-id="cb64a-129">Specify tools to ensure code quality can be measured</span></span>
    - <span data-ttu-id="cb64a-130">금지된 API 및 함수 적용</span><span class="sxs-lookup"><span data-stu-id="cb64a-130">Enforce banned APIs & functions</span></span>
    - <span data-ttu-id="cb64a-131">정적 코드 분석 수행</span><span class="sxs-lookup"><span data-stu-id="cb64a-131">Perform Static code analysis</span></span>
    - <span data-ttu-id="cb64a-132">저장된 비밀의 리포지토리 검색</span><span class="sxs-lookup"><span data-stu-id="cb64a-132">Scan repositories for stored secrets</span></span>
 
1. <span data-ttu-id="cb64a-133">확인</span><span class="sxs-lookup"><span data-stu-id="cb64a-133">Verification</span></span>

    - <span data-ttu-id="cb64a-134">동적/퍼지 테스트</span><span class="sxs-lookup"><span data-stu-id="cb64a-134">Dynamic/Fuzz testing</span></span>
    - <span data-ttu-id="cb64a-135">위협 모델/공격 노출 영역 확인</span><span class="sxs-lookup"><span data-stu-id="cb64a-135">Verify threat models/attack surface</span></span>
 
1. <span data-ttu-id="cb64a-136">릴리스</span><span class="sxs-lookup"><span data-stu-id="cb64a-136">Release</span></span>

    - <span data-ttu-id="cb64a-137">보안 응답 계획 작성</span><span class="sxs-lookup"><span data-stu-id="cb64a-137">Form security response plan</span></span>
    - <span data-ttu-id="cb64a-138">최종 보안 검토 수행</span><span class="sxs-lookup"><span data-stu-id="cb64a-138">Perform a final security review</span></span>
    - <span data-ttu-id="cb64a-139">릴리스 보관</span><span class="sxs-lookup"><span data-stu-id="cb64a-139">Release archive</span></span>
 
1. <span data-ttu-id="cb64a-140">응답</span><span class="sxs-lookup"><span data-stu-id="cb64a-140">Response</span></span> 

    - <span data-ttu-id="cb64a-141">위협 대응 실행</span><span class="sxs-lookup"><span data-stu-id="cb64a-141">Execute threat response execution</span></span>

![보안 개발 수명 주기](../media/sdl.png)

<span data-ttu-id="cb64a-143">SDL은 프로세스 또는 도구 집합이므로 문화적 측면이 강합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-143">The SDL is as much a cultural aspect as it is a process or set of tools.</span></span> <span data-ttu-id="cb64a-144">보안이 응용 프로그램 개발의 주요 포커스이자 요구 사항인 문화를 정착시키면 보안과 관련된 조직의 역량을 크게 발전시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-144">Building a culture where security is a primary focus and requirement of any application development can make great strides in evolving an organizations capabilities around security.</span></span>

<!-- Bear in mind that the migration of un-modified applications (especially COTS procured software systems) will not be able to perform many of the steps listed above.
 -->

## <a name="operational-security-assessment"></a><span data-ttu-id="cb64a-145">운영 보안 평가</span><span class="sxs-lookup"><span data-stu-id="cb64a-145">Operational security assessment</span></span>

<span data-ttu-id="cb64a-146">응용 프로그램을 배포한 후에는 지속적으로 보안 상태를 평가하고, 발견된 문제를 완화하고 지식을 소프트웨어 개발 주기에 다시 제공하는 방법을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-146">Once an application has been deployed, it's essential to continually to evaluate its security posture, determine how to mitigate any issues that are discovered and feed the knowledge back into the software development cycle.</span></span> <span data-ttu-id="cb64a-147">이 작업을 수행하는 깊이는 데이터 개인 정보 보호 요구 사항뿐 아니라 소프트웨어 개발 및 운영 팀의 완성도 수준을 측정하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-147">The depth to which this is performed is a factor of the maturity level of the software development and operational teams as well as the data privacy requirements.</span></span>

<span data-ttu-id="cb64a-148">보안 취약성 검색 소프트웨어 서비스를 사용하면 이 프로세스를 자동화하여 팀에 침투 테스트처럼 비용이 많이 드는 수동 프로세스를 수행해야 하는 부담을 지우지 않고 주기적으로 보안 문제를 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-148">Security vulnerability scanning software services are available to help automate this process and assess security concerns on a regular cadence, without burdening teams with costly manual processes, such as penetration testing.</span></span>

<span data-ttu-id="cb64a-149">Azure Security Center는 이제 모든 Azure 구독에 기본적으로 사용되는 무료 서비스로 Azure Application Gateway 및 Azure 웹 응용 프로그램 방화벽 같은 다른 Azure 응용 프로그램 수준 서비스와 밀접하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-149">Azure Security Center is a free service, now enabled by default for all Azure subscriptions, that is tightly integrated with other Azure application level services, such as Azure Application Gateway and Azure Web Application Firewall.</span></span> <span data-ttu-id="cb64a-150">이러한 서비스 ASC의 로그를 분석하여 알려진 취약점을 실시간으로 보고하고, 취약점을 완화하기 위한 대응 방법을 추천하고, 공격에 대응하여 자동으로 플레이북을 실행하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-150">By analyzing logs from these services ASC can report on known vulnerabilities in real-time, recommend responses to mitigate them and even be configured to automatically execute playbooks in response to attacks.</span></span>

<!-- SDL culture
Key Vault / MSI
CSE = App  -> DB & App Storage
Mention approach of code scanning & SDL
Scanning for passwords - Git
 -->

## <a name="identity-as-the-perimeter"></a><span data-ttu-id="cb64a-151">경계로써의 ID</span><span class="sxs-lookup"><span data-stu-id="cb64a-151">Identity as the perimeter</span></span>

<span data-ttu-id="cb64a-152">ID 유효성 검사는 응용 프로그램에 대한 공격을 방어하는 첫 번째 방어선입니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-152">Identity validation is becoming the first line in defense for applications.</span></span> <span data-ttu-id="cb64a-153">세션을 인증하고 권한을 부여하여 웹 응용 프로그램 액세스를 제한하면 공격 노출 영역을 대폭 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-153">Restricting access to a web application by authenticating and authorizing sessions can drastically reduce the attack surface area.</span></span> <span data-ttu-id="cb64a-154">Azure AD 및 Azure AD B2C는 ID 책임을 오프로드하고 완전히 관리되는 서비스에 액세스하는 효과적인 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-154">Azure AD and Azure AD B2C offer an effective way to offload the responsibility of identity and access to a fully managed service.</span></span> <span data-ttu-id="cb64a-155">Azure AD 조건부 액세스 정책, 권한 있는 ID 관리 및 ID 보호 컨트롤은 무단 액세스를 방지하고 변경 내용을 감사하는 고객의 기능을 한층 더 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-155">Azure AD conditional access policies, privileged identity management and Identity Protection controls further enhance a customer's ability to prevent unauthorized access and audit changes.</span></span>

## <a name="data-protection"></a><span data-ttu-id="cb64a-156">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="cb64a-156">Data protection</span></span>

<span data-ttu-id="cb64a-157">웹 응용 프로그램에 대한 모든 공격이 그런 것은 아니지만, 대부분의 경우 고객 데이터가 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-157">Customer data is the target for most, if not all attacks against web applications.</span></span> <span data-ttu-id="cb64a-158">응용 프로그램과 데이터 저장 레이어 간에 데이터를 안전하게 저장하고 전송하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-158">The secure storage and transport of data between an application and its data storage layer is paramount.</span></span>

<span data-ttu-id="cb64a-159">Lamna Healthcare는 매우 중요한 환자 의료 기록 데이터를 저장하고 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-159">Lamna Healthcare stores and accesses particularly sensitive patient medical record data.</span></span> <span data-ttu-id="cb64a-160">미국 의회가 1996년에 시행한 HIPAA는 의료 서비스 공급자 및 고용주의 전자 의료 트랜잭션에 대한 국가 표준을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-160">HIPAA, enacted by the United States Congress in 1996, among other controls, defines the national standards for electronic healthcare transactions by healthcare providers and employers.</span></span> <span data-ttu-id="cb64a-161">Lamna는 환자 그리고 담당 의사처럼 권한 있는 당사자에게만 의료 데이터에 대한 보안 액세스를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-161">Lamna must ensure patients and authorized parties, such as their physicians have secure access to medical data.</span></span>

<span data-ttu-id="cb64a-162">이러한 요구 사항을 준수하기 위해 Lamna Healthcare는 모든 미사용 환자 데이터 및 전송 중 환자 데이터를 암호화하도록 응용 프로그램을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-162">To comply with these requirements, Lamna Healthcare have modified their applications to encrypt all patient data at rest and in transit.</span></span> <span data-ttu-id="cb64a-163">예를 들어 TLS(전송 계층 보안)를 사용하여 웹 응용 프로그램과 백 엔드 SQL 데이터베이스 간에 교환되는 데이터를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-163">For example, Transport Layer Security (TLS) is used to encrypt data exchanged between the web application and back-end SQL databases.</span></span> <span data-ttu-id="cb64a-164">또한 TDE(투명한 데이터 암호화)를 사용하여 SQL Server의 미사용 데이터를 암호화함으로써 환경이 손상되더라도 올바른 암호 해독 키가 없는 사람이 데이터를 사용할 수 없게 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-164">Data is also encrypted at rest in SQL Server using Transparent Data Encryption (TDE) ensuring that even if the environment is compromised, data is effectively useless to anyone without the correct decryption keys.</span></span>

<span data-ttu-id="cb64a-165">Blob 저장소에 저장된 데이터를 암호화하려면 클라이언트 쪽 암호화를 사용하여 메모리의 데이터가 저장소 서비스에 기록되기 전에 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-165">To encrypt data stored in blob storage, client side encryption can be used to encrypt the data in memory before it's written to the storage service.</span></span> <span data-ttu-id="cb64a-166">이 암호화를 지원하는 라이브러리는 .NET, Java 및 Python에 사용할 수 있으며 데이터 암호화를 응용 프로그램에 직접 통합하여 데이터 무결성을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-166">Libraries supporting this encryption are available for .NET, Java, and Python, and enable the integration of data encryption directly into applications to enhance data integrity.</span></span>

### <a name="secure-key-and-secret-storage"></a><span data-ttu-id="cb64a-167">보안 키 및 비밀 저장소</span><span class="sxs-lookup"><span data-stu-id="cb64a-167">Secure key and secret storage</span></span>

<span data-ttu-id="cb64a-168">응용 프로그램 비밀(연결 문자열, 암호 등) 및 암호화 키를 데이터 액세스에 사용되는 응용 프로그램과 분리하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-168">Separating application secrets (connection strings, passwords, etc.) and encryption keys from the application used to access data is vital.</span></span> <span data-ttu-id="cb64a-169">암호화 키 및 응용 프로그램 비밀을 구성 파일의 응용 프로그램 코드에 저장하면 절대 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-169">Encryption keys and application secrets should never be stored in the application code of configuration files.</span></span> <span data-ttu-id="cb64a-170">대신, Azure Key Vault 같은 안전한 저장소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-170">Instead, a secure store such as Azure Key Vault should be used.</span></span> <span data-ttu-id="cb64a-171">관리 서비스 ID를 통해 중요한 데이터에 대한 액세스를 응용 프로그램 ID로 제한할 수 있으며, 키를 주기적으로 순환하여 암호화 키 유출 시 노출을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-171">Access to this sensitive data can then be limited to application identities through Managed Service Identities and keys can be rotated on a regular basis to limit exposure in the case of encryption key leakage.</span></span> <span data-ttu-id="cb64a-172">또한 고객은 온-프레미스 HSM(하드웨어 보안 모듈)에서 생성한 자체 암호화 키를 사용할 수 있으며, 별도의 단일 테넌트 HSM에 Azure Key Vault 인스턴스를 구현하는 것을 필수 요건으로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb64a-172">Customers can also choose to use their own encryption keys generated by on-premies Hardware Security Modules (HSM) and even mandate that Azure Key Vault instances are implemented in single-tenant, discrete HSMs.</span></span>

<!-- ### Secure and immutable file storage

All Azure storage accounts are encrypted by default using Microsoft managed keys. Azure customers also have the ability to use their own encryption keys (BYOK) to encrypt blob, file and queue data so that even the hosting provider has no access to unencrypted data. Data immutability is often required for auditing purposes or when legal disputes call for data to be effectively frozen for a determined amount of time. Azure has recently introduced an [immutable data storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-immutable-storage) option known as Write-Once, Read many (WORM) for this scenario. -->

## <a name="application-security-at-lamna-healthcare"></a><span data-ttu-id="cb64a-173">Lamna Healthcare의 응용 프로그램 보안</span><span class="sxs-lookup"><span data-stu-id="cb64a-173">Application security at Lamna Healthcare</span></span>

## <a name="summary"></a><span data-ttu-id="cb64a-174">요약</span><span class="sxs-lookup"><span data-stu-id="cb64a-174">Summary</span></span>