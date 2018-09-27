<span data-ttu-id="0c03f-101">컴퓨팅 환경이 고객 제어 데이터 센터에서 클라우드 데이터 센터로 이동함에 따라 보안 책임도 바뀌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-101">As computing environments move from customer-controlled data centers to cloud data centers, the responsibility of security also shifts.</span></span> <span data-ttu-id="0c03f-102">이제 보안은 클라우드 공급자와 고객 모두의 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-102">Security is now a concern shared both by cloud providers and customers.</span></span> <span data-ttu-id="0c03f-103">모든 응용 프로그램 및 솔루션에 있어 사용자의 책임이 무엇인지, Azure의 책임은 무엇인지 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-103">For every application and solution, it's important to understand what's your responsibility and what's Azure's responsibility.</span></span>

#### <a name="understand-security-threats"></a><span data-ttu-id="0c03f-104">보안 위협 이해</span><span class="sxs-lookup"><span data-stu-id="0c03f-104">Understand security threats</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWkotg]

#### <a name="azure-security-you-versus-the-cloud"></a><span data-ttu-id="0c03f-105">Azure 보안: 사용자 대 클라우드</span><span class="sxs-lookup"><span data-stu-id="0c03f-105">Azure security: you versus the cloud</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvj]

## <a name="share-security-responsibility-with-azure"></a><span data-ttu-id="0c03f-106">Azure와 보안 책임 공유</span><span class="sxs-lookup"><span data-stu-id="0c03f-106">Share security responsibility with Azure</span></span>

<span data-ttu-id="0c03f-107">첫 번째 변화는 온-프레미스 데이터 센터에서 IaaS(infrastructure as a service)로의 전환입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-107">The first shift you’ll make is from on-premises data centers to infrastructure as a service (IaaS).</span></span> <span data-ttu-id="0c03f-108">IaaS를 사용하면 가장 낮은 수준의 서비스를 활용하고, Azure에 VM(가상 머신) 및 가상 네트워크를 만들도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-108">With IaaS, you are leveraging the lowest-level service and asking Azure to create virtual machines (VMs) and virtual networks.</span></span> <span data-ttu-id="0c03f-109">이 수준에서는 여전히 운영 체제와 소프트웨어를 패치 및 보호하고 네트워크를 안전하게 유지하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-109">At this level, it's still your responsibility to patch and secure your operating systems and software, as well as configure your network to be secure.</span></span> <span data-ttu-id="0c03f-110">Contoso Shipping에서는 온-프레미스 실제 서버 대신 Azure VM을 사용할 때 IaaS를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-110">At Contoso Shipping, you are taking advantage of IaaS when you start using Azure VMs instead of your on-premises physical servers.</span></span> <span data-ttu-id="0c03f-111">운영상의 이점 외에도 네트워크의 물리적 부분을 보호하는 것과 관련하여 문제를 아웃소싱하는 보안상의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-111">In addition to the operational advantages, you receive the security advantage of having outsourced concern over protecting the physical parts of the network.</span></span>

<span data-ttu-id="0c03f-112">PaaS(platform as a service)로의 이전은 많은 보안 문제를 아웃소싱합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-112">Moving to platform as a service (PaaS) outsources a lot of security concerns.</span></span> <span data-ttu-id="0c03f-113">이 수준에서 Azure는 운영 체제 및 데이터베이스 관리 시스템과 같은 대부분의 기본 소프트웨어를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-113">At this level, Azure is taking care of the operating system and of most foundational software like database management systems.</span></span> <span data-ttu-id="0c03f-114">모든 소프트웨어는 최신 보안 패치로 업데이트되며, 액세스 제어를 위해 Azure Active Directory와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-114">Everything is updated with the latest security patches and can be integrated with Azure Active Directory for access controls.</span></span> <span data-ttu-id="0c03f-115">PaaS도 운영상의 많은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-115">PaaS also comes with a lot of operational advantages.</span></span> <span data-ttu-id="0c03f-116">사용자 환경에 맞게 전체 인프라와 서브넷을 직접 빌드하는 대신, Azure Portal 내에서 "가리킨 다음, 클릭"하거나 자동화된 스크립트를 실행하여 복잡한 보안 시스템을 위아래로 가져오고 필요에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-116">Rather than building whole infrastructures and subnets for your environments by hand, you can "point and click" within the Azure portal or run automated scripts to bring complex, secured systems up and down, and scale them as needed.</span></span> <span data-ttu-id="0c03f-117">Contoso Shipping은 Azure Event Hubs를 사용하여 드론 및 트럭 &mdash;의 원격 분석 데이터는 물론 PaaS의 모든 예제인, 모바일 앱 &mdash;가 포함된 Azure Cosmos DB 백 엔드를 사용하는 웹앱을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-117">Contoso Shipping uses Azure Event Hubs for ingesting telemetry data from drones and trucks &mdash; as well as a web app with an Azure Cosmos DB back end with their mobile apps &mdash; which are all examples of PaaS.</span></span>

<span data-ttu-id="0c03f-118">SaaS(software as a service)를 사용하면 거의 모든 요소를 아웃소싱할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-118">With software as a service (SaaS), you outsource almost everything.</span></span> <span data-ttu-id="0c03f-119">SaaS는 인터넷 인프라와 함께 실행되는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-119">SaaS is software that runs with an internet infrastructure.</span></span> <span data-ttu-id="0c03f-120">코드는 공급 업체가 제어하지만 고객이 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-120">The code is controlled by the vendor but configured to be used by the customer.</span></span> <span data-ttu-id="0c03f-121">대부분의 회사와 마찬가지로 Contoso Shipping은 SaaS의 훌륭한 예제인 Office 365를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-121">Like so many companies, Contoso Shipping uses Office 365, which is a great example of SaaS!</span></span>

![shared_responsibility.png](../media/shared_responsibilities.png)

## <a name="a-layered-approach-to-security"></a><span data-ttu-id="0c03f-123">보안에 대한 계층화된 접근 방법</span><span class="sxs-lookup"><span data-stu-id="0c03f-123">A layered approach to security</span></span>

<span data-ttu-id="0c03f-124">‘심층 방어’는 정보에 무단으로 액세스하기 위한 공격 진행 속도를 늦추는 여러 메커니즘을 사용하는 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-124">*Defense in depth* is a strategy that employs a series of mechanisms to slow the advance of an attack aimed at acquiring unauthorized access to information.</span></span> <span data-ttu-id="0c03f-125">각 레이어가 보호를 제공하므로 한 레이어에서 침해 사고가 발생하더라도 후속 레이어가 이미 작동하고 있기 때문에 추가 노출을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-125">Each layer provides protection so that if one layer is breached, a subsequent layer is already in place to prevent further exposure.</span></span> <span data-ttu-id="0c03f-126">Microsoft는 실제 데이터 센터 및 Azure 서비스 전반에 걸쳐 계층화된 접근 방식을 보안에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-126">Microsoft applies a layered approach to security, both in physical data centers and across Azure services.</span></span> <span data-ttu-id="0c03f-127">심층 방어의 목적은 액세스 권한이 없는 개인으로부터 정보를 보호하고 도난을 방지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-127">The objective of defense in depth is to protect and prevent information from being stolen by individuals who are not authorized to access it.</span></span>

<span data-ttu-id="0c03f-128">심층 방어를 일련의 동심원으로 시각화할 수 있으며, 그 중심에 데이터를 배치하여 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-128">Defense in depth can be visualized as a set of concentric rings, with the data to be secured at the center.</span></span> <span data-ttu-id="0c03f-129">각 원은 데이터 주변에 추가 보안 계층을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-129">Each ring adds an additional layer of security around the data.</span></span> <span data-ttu-id="0c03f-130">이 방법을 사용하면 단일 보호 레이어에 의존하지 않고 공격 속도를 늦출 수 있으며, 자동으로 또는 수동으로 작업할 수 있는 경고 원격 분석을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-130">This approach removes reliance on any single layer of protection and acts to slow down an attack and provide alert telemetry that can be acted upon, either automatically or manually.</span></span> <span data-ttu-id="0c03f-131">각 레이어를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-131">Let's take a look at each of the layers.</span></span>

![심층 방어](../media/defense_in_depth_layers_small.PNG)

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-133">![데이터를 나타내는 이미지](../media/2-data.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-133">![Image representing data](../media/2-data.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-134">:::열 범위="3"::: **데이터**</span><span class="sxs-lookup"><span data-stu-id="0c03f-134">:::column span="3"::: **Data**</span></span>

<span data-ttu-id="0c03f-135">대부분의 경우 공격자의 목표는 다음 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-135">In almost all cases, attackers are after data:</span></span>

- <span data-ttu-id="0c03f-136">데이터베이스에 저장된 데이터</span><span class="sxs-lookup"><span data-stu-id="0c03f-136">Data stored in a database</span></span>
- <span data-ttu-id="0c03f-137">가상 머신 내부의 디스크에 저장된 데이터</span><span class="sxs-lookup"><span data-stu-id="0c03f-137">Data stored on disk inside virtual machines</span></span>
- <span data-ttu-id="0c03f-138">Office 365 같은 SaaS 응용 프로그램에 저장된 데이터</span><span class="sxs-lookup"><span data-stu-id="0c03f-138">Data stored on a SaaS application such as Office 365</span></span>
- <span data-ttu-id="0c03f-139">클라우드 저장소에 저장된 데이터</span><span class="sxs-lookup"><span data-stu-id="0c03f-139">Data stored in cloud storage</span></span>

<span data-ttu-id="0c03f-140">데이터를 저장하고 액세스를 제어하는 사람은 데이터를 적절하게 보호할 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-140">It's the responsibility of those storing and controlling access to data to ensure that it's properly secured.</span></span> <span data-ttu-id="0c03f-141">종종 데이터의 기밀성, 무결성 및 가용성을 유지하기 위한 제어 및 프로세스를 적용할 것을 지시하는 규제 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-141">Often, there are regulatory requirements that dictate the controls and processes that must be in place to ensure the confidentiality, integrity, and availability of the data.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-142">![네트워크의 파일 이미지](../media/2-application.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-142">![Image of a file on the network](../media/2-application.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-143">:::열 범위="3"::: **응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="0c03f-143">:::column span="3"::: **Application**</span></span>

- <span data-ttu-id="0c03f-144">응용 프로그램이 안전하고 취약하지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-144">Ensure applications are secure and free of vulnerabilities.</span></span>
- <span data-ttu-id="0c03f-145">중요한 응용 프로그램 비밀을 안전한 저장 매체에 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="0c03f-145">Store sensitive application secrets in a secure storage medium.</span></span>
- <span data-ttu-id="0c03f-146">모든 응용 프로그램 개발을 위한 보안을 디자인 요구 사항으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-146">Make security a design requirement for all application development.</span></span>

<span data-ttu-id="0c03f-147">응용 프로그램 개발 수명 주기에 보안을 통합하면 코드의 취약점을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-147">Integrating security into the application development life cycle will help reduce the number of vulnerabilities introduced in code.</span></span> <span data-ttu-id="0c03f-148">모든 개발 팀에게 기본적으로 응용 프로그램을 안전하게 만들고 보안 요구 사항을 협상할 수 없도록 할것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-148">We encourage all development teams to ensure their applications are secure by default, and that they're making security requirements non-negotiable.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-149">![계산을 나타내는 터미널](../media/2-compute.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-149">![A terminal representing compute](../media/2-compute.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-150">:::열 범위="3"::: **계산**</span><span class="sxs-lookup"><span data-stu-id="0c03f-150">:::column span="3"::: **Compute**</span></span>

- <span data-ttu-id="0c03f-151">가상 머신에 대한 액세스를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-151">Secure access to virtual machines.</span></span>
- <span data-ttu-id="0c03f-152">엔드포인트 보호를 구현하고 시스템을 패치하고 최신 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-152">Implement endpoint protection and keep systems patched and current.</span></span>

<span data-ttu-id="0c03f-153">맬웨어, 패치되지 않은 시스템 및 부적절한 보안 시스템 때문에 환경이 공격에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-153">Malware, unpatched systems, and improperly secured systems open your environment to attacks.</span></span> <span data-ttu-id="0c03f-154">이 레이어의 핵심은 계산 리소스를 안전하게 보호하고 보안 문제를 최소화하는 적절한 제어가 마련되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-154">The focus in this layer is on making sure your compute resources are secure, and that you have the proper controls in place to minimize security issues.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-155">![네트워킹을 나타내는 세 개의 연결된 시스템](../media/2-networking.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-155">![Three connected systems representing networking](../media/2-networking.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-156">:::열 범위="3"::: **네트워킹**</span><span class="sxs-lookup"><span data-stu-id="0c03f-156">:::column span="3"::: **Networking**</span></span>

- <span data-ttu-id="0c03f-157">리소스 간의 통신을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-157">Limit communication between resources.</span></span>
- <span data-ttu-id="0c03f-158">기본적으로 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-158">Deny by default.</span></span>
- <span data-ttu-id="0c03f-159">적절한 경우 인바운드 인터넷 액세스를 금지하고 아웃바운드를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-159">Restrict inbound internet access and limit outbound, where appropriate.</span></span>
- <span data-ttu-id="0c03f-160">온-프레미스 네트워크에 대한 보안 연결을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-160">Implement secure connectivity to on-premises networks.</span></span>

<span data-ttu-id="0c03f-161">이 레이어의 핵심은 모든 리소스에 대한 네트워크 연결을 제한하여 필요한 것만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-161">At this layer, the focus is on limiting the network connectivity across all your resources to allow only what is required.</span></span> <span data-ttu-id="0c03f-162">이 통신을 제한하여 네트워크 전체에서 횡 이동 위험을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-162">By limiting this communication, you reduce the risk of lateral movement throughout your network.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-163">![네트워크 경계를 나타내는 물리적 장벽](../media/2-perimeter.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-163">![A physical barrier representing the network perimeter](../media/2-perimeter.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-164">:::열 범위="3"::: **경계**</span><span class="sxs-lookup"><span data-stu-id="0c03f-164">:::column span="3"::: **Perimeter**</span></span>

- <span data-ttu-id="0c03f-165">DDoS(분산 서비스 거부) 보호 기능을 사용하여 최종 사용자에게 서비스 거부가 발생하기 전에 대규모 공격을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-165">Use distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for end users.</span></span>
- <span data-ttu-id="0c03f-166">경계 방화벽을 사용하여 네트워크에 대한 악의적인 공격을 식별하고 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-166">Use perimeter firewalls to identify and alert on malicious attacks against your network.</span></span>

<span data-ttu-id="0c03f-167">네트워크 경계에서, 리소스에 대한 네트워크 기반 공격을 방어합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-167">At the network perimeter, it's about protecting from network-based attacks against your resources.</span></span> <span data-ttu-id="0c03f-168">이러한 공격을 파악하여 영향을 제거하고 발생한 공격을 경고하는 것이 네트워크를 안전하게 유지하는 중요한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-168">Identifying these attacks, eliminating their impact, and alerting you when they happen are important ways to keep your network secure.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-169">![보안 액세스를 나타내는 배지](../media/2-policies-and-access.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-169">![A badge representing a secure access](../media/2-policies-and-access.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-170">:::열 범위="3"::: **정책 및 액세스**</span><span class="sxs-lookup"><span data-stu-id="0c03f-170">:::column span="3"::: **Policies and access**</span></span>

- <span data-ttu-id="0c03f-171">인프라 및 변경 제어에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-171">Control access to infrastructure and change control.</span></span>
- <span data-ttu-id="0c03f-172">Single Sign-On 및 다단계 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-172">Use single sign-on and multi-factor authentication.</span></span>
- <span data-ttu-id="0c03f-173">이벤트 및 변경 내용을 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-173">Audit events and changes.</span></span>

<span data-ttu-id="0c03f-174">정책 및 액세스 레이어는 ID를 안전하게 보호하고, 필요한 액세스 권한만 부여하고, 변경 내용을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-174">The policy and access layer is all about ensuring identities are secure, access granted is only what is needed, and changes are logged.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    <span data-ttu-id="0c03f-175">![물리적 보안을 나타내는 보안 카메라](../media/2-physical-security.png)</span><span class="sxs-lookup"><span data-stu-id="0c03f-175">![A security camera representing physical security](../media/2-physical-security.png)</span></span>
  :::column-end:::
    <span data-ttu-id="0c03f-176">:::열 범위="3"::: **물리적 보안**</span><span class="sxs-lookup"><span data-stu-id="0c03f-176">:::column span="3"::: **Physical security**</span></span>

- <span data-ttu-id="0c03f-177">물리적 빌딩 보안 및 데이터 센터 내의 컴퓨팅 하드웨어에 대한 액세스 제어가 첫 번째 방어선입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-177">Physical building security and controlling access to computing hardware within the data center is the first line of defense.</span></span>

<span data-ttu-id="0c03f-178">물리적 보안을 사용하는 의도는 자산 액세스를 물리적으로 보호하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-178">With physical security, the intent is to provide physical safeguards against access to assets.</span></span> <span data-ttu-id="0c03f-179">이렇게 하면 다른 레이어를 무시할 수 없으며, 손실 또는 도난이 적절하게 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-179">This ensures that other layers can't be bypassed, and loss or theft is handled appropriately.</span></span>
  :::column-end:::
:::row-end:::

## <a name="summary"></a><span data-ttu-id="0c03f-180">요약</span><span class="sxs-lookup"><span data-stu-id="0c03f-180">Summary</span></span>

<span data-ttu-id="0c03f-181">여기서는 Azure가 보안 문제에 많은 도움이 된다는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-181">We've seen here that Azure helps a lot with your security concerns.</span></span> <span data-ttu-id="0c03f-182">그러나 보안은 여전히 **공유 책임**입니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-182">But security is still a **shared responsibility**.</span></span> <span data-ttu-id="0c03f-183">책임의 상당한 부분이 Azure에서 사용하는 모델에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-183">How much of that responsibility falls on us depends on which model we use with Azure.</span></span>

<span data-ttu-id="0c03f-184">데이터 및 환경에 적합한 보호 수단을 고려하기 위한 지침으로 *심층 방어* 링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c03f-184">We use the *defense in depth* rings as a guideline for considering what protections are adequate for our data and environments.</span></span>