이 연습에서는 가상 머신을 만들고 포털 및 Azure PowerShell을 사용하여 크기를 조정합니다.

## <a name="create-a-vm"></a>VM 만들기

1. 웹 브라우저에서 [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하고 계정에 로그인합니다.

1. Azure Portal에서 새 리소스를 만듭니다. **새로 만들기** 블레이드에서 검색 상자에 **가상 머신**를 입력한 후 Enter 키를 누릅니다.

1. **모든 항목** 블레이드의 **결과** 아래에서 **Windows Server 2016 Datacenter**를 클릭합니다.

1. **Windows Server 2016 Datacenter** 블레이드에서 **만들기**를 클릭합니다.

1. **기본 사항** 블레이드에서 다음 정보를 사용하여 세부 정보를 작성한 후 **확인**을 클릭합니다.

    |설정|값|
    |---|---|
    |이름|DB01|
    |사용자 이름|LocalAdmin|
    |암호 및 암호 확인|Adm1nPa$$word|
    |리소스 그룹|ExerciseRG|
    |위치|미국 중부|

1. **크기 선택** 블레이드에서 **D2s_v3**을 선택하고 **선택**을 클릭합니다.

1. **설정** 블레이드의 **공용 인바운드 포트 선택** 아래에서 **HTTP**, **HTTPS** 및 **RDP(3389)** 를 선택하고, **부트 진단** 아래에서 **사용 안 함**을 클릭하고, 모든 다른 설정을 기본값으로 유지한 후, **확인**을 클릭합니다.

1. **만들기** 블레이드에서 **만들기**를 클릭합니다.

1. 배포가 완료될 때까지 기다린 후에 연습을 계속 진행하세요.

## <a name="resize-using-the-portal"></a>포털을 사용하여 크기 조정

1. Azure Portal에서 ExerciseRG 리소스 그룹으로 이동하고 **ExerciseRG** 블레이드에서 **DB01** 가상 머신 개체를 클릭합니다.

1. **DB01** 블레이드에서 **크기**를 클릭합니다. 현재 강조 표시된 크기는 가상 머신을 만들 때 선택한 크기입니다.

1. **크기 선택** 블레이드에서 **F2s_v2** 크기를 찾아보세요. VM이 현재 실행 중이고 해당 크기가 다른 패밀리에 속하므로 크기 목록에 이 크기가 제공되지 않습니다. **크기 선택** 블레이드를 닫습니다.

1. **DB01** 블레이드에서 **중지**를 클릭합니다. **이 가상 머신 중지** 대화 상자에서 **예**를 클릭하고 가상 머신 상태가 **중지됨(할당 취소됨)** 으로 표시될 때까지 기다립니다.

1. **DB01** 블레이드에서 **크기**를 클릭합니다. **크기 선택** 블레이드에서 **F2s_v2**를 선택하고 **선택**을 클릭합니다. 가상 머신의 크기 조정에 대한 알림을 확인하세요.

1. **DB01** 블레이드에서 **개요**를 클릭한 후 **시작**을 클릭합니다.

## <a name="resize-using-powershell"></a>PowerShell을 사용하여 크기 조정

1. Azure Portal에서 Cloud Shell을 엽니다.

1. 다음 cmdlet을 사용하여 사용 가능한 가상 머신 목록을 가져옵니다.

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName ExerciseRG -VMName DB01
    ```

1. 다음 cmdlet을 실행하여 가상 머신의 크기를 F4s_v2 크기로 조정합니다.

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName ExerciseRG -VMName DB01
    $vm.HardwareProfile.VmSize = "Standard_F4s_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName ExerciseRG
    ```

1. PowerShell 명령이 완료될 때까지 기다리는 동안 DB01 블레이드에서 [새로 고침] 단추를 클릭합니다. 가상 머신이 변경된 크기를 적용하도록 다시 시작되고 있음을 알 수 있습니다.

이 연습에서는 가상 머신을 만들고 두 개의 다른 도구로 크기를 조정했습니다. 가상 머신이 실행되는 동안에는 대상 크기를 사용할 수 없다는 점을 기억하는 것이 좋습니다. 가상 머신을 중지하면 더 많은 크기를 선택할 수 있습니다.