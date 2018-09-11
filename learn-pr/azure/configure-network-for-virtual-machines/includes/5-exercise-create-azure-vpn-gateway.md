공용 인터넷을 통해 암호화된 터널을 사용하여 사용자 환경 내의 클라이언트 또는 사이트를 Azure에 연결할 수 있는지 확인하려고 합니다. 이 연습에서는 지점 및 사이트 간 VPN Gateway를 만든 다음, 클라이언트 컴퓨터에서 해당 게이트웨이에 연결합니다. 보안을 위해 네이티브 Azure 인증서 인증 연결을 사용합니다.

다음 프로세스를 수행합니다.

1. RouteBased VPN Gateway 만들기

1. 인증 목적으로 루트 인증서의 공개 키 업로드

1. 루트 인증서에서 클라이언트 인증서를 생성한 다음, 인증을 위해 VNet에 연결할 각 클라이언트 컴퓨터에 클라이언트 인증서를 설치합니다.

1. VPN 클라이언트 구성 파일을 만듭니다. 여기에는 클라이언트를 VNet에 연결하는 데 필요한 정보가 포함됩니다.

## <a name="before-you-begin"></a>시작하기 전에

이 랩을 완료하려면 다음 항목이 필요합니다.

- Azure PowerShell

- C:\cert라는 폴더

Azure PowerShell을 설치하려면:

1. Windows 단추를 마우스 오른쪽 단추로 클릭하고 **PowerShell(관리자)** 을 클릭합니다.

1. **사용자 계정 컨트롤** 메시지 상자에서 **예**를 클릭합니다.

1. PowerShell 창에 다음 명령을 입력하고 Enter 키를 누릅니다.

    ```PowerShell
    Import-Module AzureRM
    ```

1. 보안 프롬프트에 A를 입력하고 Enter 키를 누릅니다.

## <a name="sign-in-and-set-variables"></a>로그인 및 변수 설정

로그인하고 변수를 설정하려면 다음 단계를 수행합니다.

1. 다음 명령을 입력하고 Enter 키를 눌러 Azure에 연결합니다.

    ```PowerShell
    Connect-AzureRmAccount
    ```

1. Azure 구독 목록을 가져옵니다.

    ```PowerShell
    Get-AzureRmSubscription
    ```
1. 사용할 구독을 지정합니다.

    ```PowerShell
    Select-AzureRmSubscription -SubscriptionName "{Name of your subscription}"
    ```

    "구독 이름"을 사용자 구독 이름으로 바꿉니다.

1. 다음 변수를 입력하고, 각각 Enter 키를 누릅니다.

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

## <a name="configure-a-vnet"></a>vNet 구성

1. 리소스 그룹을 만듭니다.

    ```PowerShell
    New-AzureRmResourceGroup -Name $RG -Location $Location
    ```

1. 가상 네트워크에 대한 서브넷 구성을 만듭니다. **FrontEnd, BackEnd** 및 **GatewaySubnet**이라는 이름입니다. 이러한 서브넷은 모두 가상 네트워크 접두사 내에 존재합니다.

    ```PowerShell
    $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
    $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
    $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
    ```

1. 서브넷 값 및 정적 DNS 서버를 사용하여 가상 네트워크를 만듭니다. 
    > [!IMPORTANT]
    > 경고 메시지를 무시한 다음, 명령이 완료될 때까지 기다립니다.

    ```PowerShell
    New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
    ```

1. 이제 방금 만든 이 네트워크의 변수를 지정합니다.

    ```PowerShell
    $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    ```

1. 동적으로 할당된 공용 IP 주소를 요청합니다.

    ```PowerShell
    $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
    $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
    ```

## <a name="create-the-vpn-gateway"></a>VPN Gateway 만들기

이 VPN Gateway를 만드는 경우:

- GatewayType은 Vpn이어야 합니다.
- VpnTpe은 RouteBased여야 합니다.

> [!NOTE]
> 연습 중 이 부분은 게이트웨이 SKU의 값에 따라 완료하는 데 최대 45분이 걸릴 수 있습니다.

1. VPN Gateway를 만들려면 다음 명령을 실행하고 Enter 키를 누릅니다.

    ```PowerShell
    New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
    -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
    -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
    ```

1. 명령 출력이 표시될 때까지 기다립니다.

## <a name="add-the-vpn-client-address-pool"></a>VPN 클라이언트 주소 풀 추가

1. 다음 명령을 실행하고 Enter 키를 누릅니다.

    ```PowerShell
    $Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
    Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
    ```

1. 명령 출력이 표시될 때까지 기다립니다.

## <a name="generate-a-client-certificate"></a>클라이언트 인증서 생성

1. 자체 서명된 루트 인증서를 만듭니다.

    ```PowerShell
    $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
    -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
    ```

1. 클라이언트 인증서를 생성합니다.

    ```PowerShell
    New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
    -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
    ```

1. 루트 인증서 공개 키를 내보냅니다. 클라이언트 컴퓨터에 다음 명령을 입력하고 Enter 키를 누릅니다.

    ```PowerShell
    certmgr
    ```

1. 개인/인증서로 이동합니다. P2SRootCert를 마우스 오른쪽 단추로 클릭하고, **모든 작업**을 클릭한 다음, **내보내기**를 선택합니다.

1. 인증서 내보내기 마법사에서 **다음**을 클릭합니다.

1. **아니요, 개인 키를 내보내지 않습니다.** 를 선택했는지 확인한 다음, **다음**을 클릭합니다.

1. **내보내기 파일 형식** 페이지에서 **Base 64로 인코딩된 X.509(.CER)** 를 선택했는지 확인한 다음, **다음**을 클릭합니다.

1. **내보낼 파일** 페이지의 **파일 이름**에서 **C:\cert\P2SRootCert.cer**을 입력한 다음, 다음을 클릭합니다.

1. **인증서 내보내기 마법사 완료** 페이지에서 **마침**을 클릭합니다.

1. **인증서 내보내기 마법사** 메시지 상자에서 **확인**을 클릭합니다.

## <a name="upload-the-root-certificate-public-key-information"></a>루트 인증서 공개 키 정보 업로드

1. PowerShell 창에서 다음 명령을 실행하여 인증서 이름의 변수를 선언합니다.

    ```PowerShell
    $P2SRootCertName = "P2SRootCert.cer"
    ```

1. 다음 명령을 실행합니다.

    ```PowerShell
    $filePathForCert = "C:\cert\P2SRootCert.cer"
    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
    $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
    $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
    ```

1. 이제 Azure에 인증서를 업로드합니다. 그러면 Azure에서는 해당 인증서를 신뢰할 수 있는 루트 인증서로 인식합니다.

    ```PowerShell
    Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNetDataGW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
    ```

## <a name="configure-the-native-vpn-client"></a>네이티브 VPN 클라이언트 구성

1. 다음 명령을 실행하여 .ZIP 형식으로 VPN 클라이언트 구성 파일을 생성할 수 있습니다.

    ```PowerShell
    $profile=New-AzureRmVpnClientConfiguration -ResourceGroupName "TestRG" -Name "VNetDataGW" -AuthenticationMethod "EapTls"
    $profile.VPNProfileSASUrl
    ```

1. 이 명령의 출력에 반환된 URL을 복사하고, 브라우저에 붙여넣습니다. 브라우저에서는 .ZIP 파일을 다운로드하기 시작해야 합니다. 압축을 풀고 적절한 위치에 배치합니다.

1. 추출된 폴더에서 WindowsAmd64 폴더(64비트 Windows 컴퓨터의 경우) 또는 WindowsZX86(32비트 Windows 컴퓨터의 경우) 폴더 중 하나로 이동합니다.

1. 아키텍처에 따라 VpnClientSetupxxxxx.exe 파일을 두 번 클릭합니다.

1. **Windows 보호 PC** 화면에서 **자세한 정보**를 클릭한 다음, **실행**을 클릭합니다.

1. **사용자 계정 컨트롤** 대화 상자에서 **예**를 클릭합니다.

1. **VNetData** 대화 상자에서 **예**를 클릭합니다.

## <a name="connect-to-azure"></a>Azure에 연결

1. Windows 로고 키를 누르고, **설정**을 입력하고, Enter 키를 누릅니다.

1. **설정** 창에서 **네트워크 및 인터넷**을 클릭합니다.

1. 왼쪽 창에서 **VPN**을 클릭합니다.

1. 오른쪽 창에서 **VNetData**를 클릭한 다음, **연결**을 클릭합니다.

1. VNetData 창에서 **연결**을 클릭합니다.

1. 다음 VNetData 창에서 **계속**을 클릭합니다.

1. **사용자 계정 컨트롤** 메시지 상자에서 **예**를 클릭합니다.

> [!NOTE]
> 이 단계가 작동하지 않으면 컴퓨터를 다시 시작해야 합니다.

## <a name="verify-your-connection"></a>연결 확인

1. Windows 로고 키를 누르고, **cmd**를 입력하고, Enter 키를 누릅니다. **명령 프롬프트** 창이 나타납니다.

1. `IPCONFIG /ALL`을 입력하고 Enter 키를 누릅니다.

1. PPP 어댑터 VNetData의 IP 주소를 복사하거나 적어둡니다.

1. IP 주소가 **172.16.201.0/24 VPNClientAddressPool 범위**에 있는지 확인합니다.

1. Azure VPN Gateway에 대해 성공적으로 연결했습니다.

## <a name="summary"></a>요약

방금 VPN Gateway를 설정하여 Azure에서 vNet에 대해 암호화된 클라이언트 연결을 만들 수 있습니다. 이 방법은 클라이언트 컴퓨터 및 소규모 사이트 간 연결에 적합합니다.