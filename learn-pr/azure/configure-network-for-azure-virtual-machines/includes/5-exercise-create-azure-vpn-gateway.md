<span data-ttu-id="a6454-101">공용 인터넷을 통해 암호화된 터널을 사용하여 사용자 환경 내의 클라이언트 또는 사이트를 Azure에 연결할 수 있는지 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-101">You want to ensure that you can connect clients or sites within your environment into Azure using encrypted tunnels across the public internet.</span></span> <span data-ttu-id="a6454-102">이 단원에서는 지점 및 사이트 간 VPN Gateway를 만든 다음, 클라이언트 컴퓨터에서 해당 게이트웨이에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-102">In this unit, you'll create a point-to-site VPN gateway, and then connect to that gateway from a client computer.</span></span> <span data-ttu-id="a6454-103">보안을 위해 네이티브 Azure 인증서 인증 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-103">You'll use native Azure certificate authentication connections for security.</span></span>

<span data-ttu-id="a6454-104">다음 프로세스를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-104">You will carry out the following process:</span></span>

1. <span data-ttu-id="a6454-105">RouteBased VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-105">Create a RouteBased VPN gateway.</span></span>

1. <span data-ttu-id="a6454-106">인증을 위해 루트 인증서의 공개 키를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-106">Upload the public key for a root certificate for authentication purposes.</span></span>

1. <span data-ttu-id="a6454-107">루트 인증서에서 클라이언트 인증서를 생성한 다음, 인증을 위해 가상 네트워크에 연결할 각 클라이언트 컴퓨터에 클라이언트 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-107">Generate a client certificate from the root certificate, and then install the client certificate on each client computer that will connect to the virtual network for authentication purposes.</span></span>

1. <span data-ttu-id="a6454-108">클라이언트를 가상 네트워크에 연결하는 데 필요한 정보가 포함된 VPN 클라이언트 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-108">Create VPN client configuration files, which contain the necessary information for the client to connect to the virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6454-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a6454-109">Before you begin</span></span>
<!---TODO: These should be prerequisites in the first unit and on the index.yml--->

<span data-ttu-id="a6454-110">이 모듈을 완료하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-110">To complete this module, you must have:</span></span>

- <span data-ttu-id="a6454-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6454-111">Azure PowerShell</span></span>

- <span data-ttu-id="a6454-112">C:\cert라는 폴더</span><span class="sxs-lookup"><span data-stu-id="a6454-112">A folder called C:\cert</span></span>

<span data-ttu-id="a6454-113">Azure PowerShell을 설치하려면:</span><span class="sxs-lookup"><span data-stu-id="a6454-113">To install Azure PowerShell:</span></span>

1. <span data-ttu-id="a6454-114">Windows 단추를 마우스 오른쪽 단추로 클릭하고 **PowerShell(관리자)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-114">Right-click the Windows button and click **PowerShell (Admin)**.</span></span>

1. <span data-ttu-id="a6454-115">**사용자 계정 컨트롤** 메시지 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-115">In the **User Account Control** message box, click **Yes**.</span></span>

1. <span data-ttu-id="a6454-116">PowerShell 창에서 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-116">In the PowerShell window, type the following command and press Enter:</span></span>

    ```PowerShell
    Import-Module AzureRM
    ```

1. <span data-ttu-id="a6454-117">보안 프롬프트에 A를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-117">At the security prompt, type A and press Enter.</span></span>

## <a name="sign-in-and-set-variables"></a><span data-ttu-id="a6454-118">로그인 및 변수 설정</span><span class="sxs-lookup"><span data-stu-id="a6454-118">Sign in and set variables</span></span>

<span data-ttu-id="a6454-119">로그인하고 변수를 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-119">To sign in and set variables, carry out the following steps:</span></span>

1. <span data-ttu-id="a6454-120">다음 명령을 입력하고 Enter 키를 눌러 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-120">Connect to Azure by entering the following command and pressing Enter:</span></span>

    ```PowerShell
    Connect-AzureRmAccount
    ```

1. <span data-ttu-id="a6454-121">Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-121">Get a list of your Azure subscriptions.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
1. <span data-ttu-id="a6454-122">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-122">Specify the subscription that you want to use.</span></span>

    ```PowerShell
    Select-AzureRmSubscription -SubscriptionName "{Name of your subscription}"
    ```

    <span data-ttu-id="a6454-123">"구독 이름"을 사용자 구독 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-123">Replace "Name of subscription" with your subscription name.</span></span>

1. <span data-ttu-id="a6454-124">다음 변수를 입력하고, 각 변수 다음에 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-124">Enter the following variables and press Enter after each one.</span></span>

    ```PowerShell
    $VNetName  = "VNetData"
    $FESubName = "FrontEnd"
    $BESubName = "Backend"
    $GWSubName = "GatewaySubnet"
    $VNetPrefix1 = "192.168.0.0/16"
    $VNetPrefix2 = "10.254.0.0/16"
    $FESubPrefix = "192.168.1.0/24"
    $BESubPrefix = "10.254.1.0/24"
    $GWSubPrefix = "192.168.200.0/26"
    $VPNClientAddressPool = "172.16.201.0/24"
    $RG = "TestRG"
    $Location = "East US"
    $GWName = "VNetDataGW"
    $GWIPName = "VNetDataGWPIP"
    $GWIPconfName = "gwipconf"
    ```

## <a name="configure-a-virtual-network"></a><span data-ttu-id="a6454-125">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="a6454-125">Configure a virtual network</span></span>

1. <span data-ttu-id="a6454-126">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-126">Create a resource group.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name $RG -Location $Location
    ```

1. <span data-ttu-id="a6454-127">가상 네트워크에 대한 서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-127">Create subnet configurations for the virtual network.</span></span> <span data-ttu-id="a6454-128">**FrontEnd, BackEnd** 및 **GatewaySubnet**이라는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-128">These have the name **FrontEnd, BackEnd**, and **GatewaySubnet**.</span></span> <span data-ttu-id="a6454-129">이러한 서브넷은 모두 가상 네트워크 접두사 내에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-129">All of these subnets exist within the virtual network prefix.</span></span>

    ```PowerShell
    $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
    $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
    $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
    ```

1. <span data-ttu-id="a6454-130">서브넷 값 및 정적 DNS 서버를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-130">Create the virtual network using the subnet values and a static DNS server.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a6454-131">경고 메시지를 무시한 다음, 명령이 종료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-131">Ignore the warning message, and then wait for the command to finish.</span></span>

    ```PowerShell
    New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
    ```

1. <span data-ttu-id="a6454-132">이제 방금 만든 이 네트워크의 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-132">Now specify the variables for this network that you have just created.</span></span>

    ```PowerShell
    $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    ```

1. <span data-ttu-id="a6454-133">동적으로 할당된 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-133">Request a dynamically assigned public IP address.</span></span>

    ```PowerShell
    $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
    $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
    ```

## <a name="create-the-vpn-gateway"></a><span data-ttu-id="a6454-134">VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="a6454-134">Create the VPN gateway</span></span>

<span data-ttu-id="a6454-135">이 VPN 게이트웨이를 만드는 경우:</span><span class="sxs-lookup"><span data-stu-id="a6454-135">When creating this VPN gateway:</span></span>

- <span data-ttu-id="a6454-136">GatewayType은 Vpn이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-136">GatewayType must be Vpn</span></span>
- <span data-ttu-id="a6454-137">VpnType은 RouteBased여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-137">VpnType must be RouteBased</span></span>

> [!NOTE]
> <span data-ttu-id="a6454-138">연습의 이 부분은 GatewaySku의 값에 따라 완료하는 데 최대 45분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-138">Note that this part of the exercise can take up to 45 minutes to complete, depending on the value of GatewaySku.</span></span>

1. <span data-ttu-id="a6454-139">VPN 게이트웨이를 만들려면 다음 명령을 실행하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-139">To create the VPN gateway, run the following command and press Enter.</span></span>

    ```PowerShell
    New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
    -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
    -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
    ```

1. <span data-ttu-id="a6454-140">명령 출력이 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-140">Wait for the command output to appear.</span></span>

## <a name="add-the-vpn-client-address-pool"></a><span data-ttu-id="a6454-141">VPN 클라이언트 주소 풀 추가</span><span class="sxs-lookup"><span data-stu-id="a6454-141">Add the VPN client address pool</span></span>

1. <span data-ttu-id="a6454-142">다음 명령을 실행하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-142">Run the following command and press Enter.</span></span>

    ```PowerShell
    $Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
    Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
    ```

1. <span data-ttu-id="a6454-143">명령 출력이 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-143">Wait for the command output to appear.</span></span>

## <a name="generate-a-client-certificate"></a><span data-ttu-id="a6454-144">클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="a6454-144">Generate a client certificate</span></span>

1. <span data-ttu-id="a6454-145">자체 서명된 루트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-145">Create the self-signed root certificate.</span></span>

    ```PowerShell
    $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
    -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
    ```

1. <span data-ttu-id="a6454-146">클라이언트 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-146">Generate a client certificate.</span></span>

    ```PowerShell
    New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
    -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
    ```

1. <span data-ttu-id="a6454-147">루트 인증서 공개 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-147">Export the root certificate public key.</span></span> <span data-ttu-id="a6454-148">클라이언트 컴퓨터에 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-148">On your client computer, type the following command and press Enter.</span></span>

    ```PowerShell
    certmgr
    ```

1. <span data-ttu-id="a6454-149">개인/인증서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-149">Navigate to Personal/Certificates.</span></span> <span data-ttu-id="a6454-150">P2SRootCert를 마우스 오른쪽 단추로 클릭하고, **모든 작업**을 클릭한 다음, **내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-150">Right-click P2SRootCert, click **All tasks**, and then select **Export**.</span></span>

1. <span data-ttu-id="a6454-151">인증서 내보내기 마법사에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-151">In the Certificate Export Wizard, click **Next**.</span></span>

1. <span data-ttu-id="a6454-152">**아니요, 개인 키를 내보내지 않습니다.** 를 선택했는지 확인한 후, **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-152">Ensure that **No, do not export the private key** is selected, and then click **Next**.</span></span>

1. <span data-ttu-id="a6454-153">**내보내기 파일 형식** 페이지에서 **Base 64로 인코딩된 X.509(.CER)** 를 선택했는지 확인한 후, **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-153">On the **Export File Format** page, ensure that **Base-64 encoded X.509 (.CER)** is selected, and then click **Next**.</span></span>

1. <span data-ttu-id="a6454-154">**내보낼 파일** 페이지의 **파일 이름**에 **C:\cert\P2SRootCert.cer**을 입력한 후, 다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-154">In the **File to Export** page, under **File name**, enter **C:\cert\P2SRootCert.cer**, and then click Next.</span></span>

1. <span data-ttu-id="a6454-155">**인증서 내보내기 마법사 완료** 페이지에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-155">On the **Completing the Certificate Export Wizard** page, click **Finish**.</span></span>

1. <span data-ttu-id="a6454-156">**인증서 내보내기 마법사** 메시지 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-156">On the **Certificate Export Wizard** message box, click **OK**.</span></span>

## <a name="upload-the-root-certificate-public-key-information"></a><span data-ttu-id="a6454-157">루트 인증서 공개 키 정보 업로드</span><span class="sxs-lookup"><span data-stu-id="a6454-157">Upload the root certificate public key information</span></span>

1. <span data-ttu-id="a6454-158">PowerShell 창에서 다음 명령을 실행하여 인증서 이름의 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-158">In the PowerShell window, execute the following command to declare a variable for the certificate name:</span></span>

    ```PowerShell
    $P2SRootCertName = "P2SRootCert.cer"
    ```

1. <span data-ttu-id="a6454-159">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-159">Execute the following command:</span></span>

    ```PowerShell
    $filePathForCert = "C:\cert\P2SRootCert.cer"
    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
    $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
    $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
    ```

1. <span data-ttu-id="a6454-160">이제 Azure에 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-160">Now upload the certificate to Azure.</span></span> <span data-ttu-id="a6454-161">그러면 Azure에서 신뢰할 수 있는 루트 인증서로 인식됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-161">Azure then recognizes it as a trusted root certificate.</span></span>

    ```PowerShell
    Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNetDataGW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
    ```

## <a name="configure-the-native-vpn-client"></a><span data-ttu-id="a6454-162">네이티브 VPN 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="a6454-162">Configure the native VPN client</span></span>

1. <span data-ttu-id="a6454-163">다음 명령을 실행하여 .ZIP 형식으로 VPN 클라이언트 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-163">Execute the following command to create VPN client configuration files in .ZIP format.</span></span>

    ```PowerShell
    $profile=New-AzureRmVpnClientConfiguration -ResourceGroupName "TestRG" -Name "VNetDataGW" -AuthenticationMethod "EapTls"
    $profile.VPNProfileSASUrl
    ```

1. <span data-ttu-id="a6454-164">이 명령의 출력에 반환된 URL을 복사하여 브라우저에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-164">Copy the URL returned in the output from this command and paste it into your browser.</span></span> <span data-ttu-id="a6454-165">브라우저에서 .ZIP 파일 다운로드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-165">Your browser should start downloading a .ZIP file.</span></span> <span data-ttu-id="a6454-166">압축을 풀고 적절한 위치에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-166">Unzip it and put it in a suitable location.</span></span>

1. <span data-ttu-id="a6454-167">추출된 폴더에서 WindowsAmd64 폴더(64비트 Windows 컴퓨터의 경우) 또는 WindowsZX86 폴더(32비트 Windows 컴퓨터의 경우) 중 하나로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-167">In the extracted folder, navigate to either the WindowsAmd64 folder (for 64-bit Windows computers) or the WindowsZX86 folder (for 32-bit computers).</span></span>

1. <span data-ttu-id="a6454-168">아키텍처에 따라 VpnClientSetupxxxxx.exe 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-168">Double-click on the VpnClientSetupxxxxx.exe file, depending on your architecture.</span></span>

1. <span data-ttu-id="a6454-169">**Windows의 PC 보호** 화면에서 **자세한 정보**를 클릭한 다음, **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-169">In the **Windows protected your PC** screen, click **More info**, and then click **Run anyway**.</span></span>

1. <span data-ttu-id="a6454-170">**사용자 계정 컨트롤** 대화 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-170">In the **User Account Control** dialog box, click **Yes**.</span></span>

1. <span data-ttu-id="a6454-171">**VNetData** 대화 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-171">In the **VNetData** dialog box, click **Yes**.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="a6454-172">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="a6454-172">Connect to Azure</span></span>

1. <span data-ttu-id="a6454-173">Windows 키를 누르고, **설정**을 입력하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-173">Press the Windows key, type **Settings** and press Enter.</span></span>

1. <span data-ttu-id="a6454-174">**설정** 창에서 **네트워크 및 인터넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-174">In the **Settings** window, click **Network and Internet**.</span></span>

1. <span data-ttu-id="a6454-175">왼쪽 창에서 **VPN**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-175">In the left-hand pane, click **VPN**.</span></span>

1. <span data-ttu-id="a6454-176">오른쪽 창에서 **VNetData**를 클릭한 다음, **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-176">In the right-hand pane, click **VNetData**, and then click **Connect**.</span></span>

1. <span data-ttu-id="a6454-177">VNetData 창에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-177">In the VNetData window, click **Connect**.</span></span>

1. <span data-ttu-id="a6454-178">다음 VNetData 창에서 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-178">In the next VNetData window, click **Continue**.</span></span>

1. <span data-ttu-id="a6454-179">**사용자 계정 컨트롤** 메시지 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-179">In the **User Account Control** message box, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="a6454-180">이 단계가 작동하지 않으면 컴퓨터를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-180">If these steps do not work, you may need to restart your computer.</span></span>

## <a name="verify-your-connection"></a><span data-ttu-id="a6454-181">연결 확인</span><span class="sxs-lookup"><span data-stu-id="a6454-181">Verify your connection</span></span>

1. <span data-ttu-id="a6454-182">Windows 키를 누르고, **cmd**를 입력하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-182">Press the Windows key, type **cmd** and press Enter.</span></span> <span data-ttu-id="a6454-183">**명령 프롬프트** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-183">The **Command Prompt** window appears.</span></span>

1. <span data-ttu-id="a6454-184">`IPCONFIG /ALL`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-184">Type `IPCONFIG /ALL` and press Enter.</span></span>

1. <span data-ttu-id="a6454-185">PPP 어댑터 VNetData의 IP 주소를 복사하거나 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-185">Copy the IP address under PPP adapter VNetData, or write it down.</span></span>

1. <span data-ttu-id="a6454-186">IP 주소가 **172.16.201.0/24 VPNClientAddressPool 범위**에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-186">Confirm that IP address is in the **VPNClientAddressPool range of 172.16.201.0/24**.</span></span>

1. <span data-ttu-id="a6454-187">Azure VPN Gateway에 성공적으로 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-187">You have successfully made a connection to the Azure VPN gateway.</span></span>

## <a name="summary"></a><span data-ttu-id="a6454-188">요약</span><span class="sxs-lookup"><span data-stu-id="a6454-188">Summary</span></span>

<span data-ttu-id="a6454-189">VPN 게이트웨이를 설정하기만 하면, Azure에서 가상 네트워크에 대해 암호화된 클라이언트 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-189">You just set up a VPN gateway, allowing you to make an encrypted client connection to a virtual network in Azure.</span></span> <span data-ttu-id="a6454-190">이 방법은 클라이언트 컴퓨터 및 소규모 사이트 간 연결에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a6454-190">This approach is great with client computers and smaller site-to-site connections.</span></span>