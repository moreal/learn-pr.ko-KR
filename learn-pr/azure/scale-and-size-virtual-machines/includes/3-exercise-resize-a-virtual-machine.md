이 연습에서는 가상 컴퓨터를 만들고 포털 및 Azure PowerShell을 사용 하 여 크기를 조정 합니다.

## <a name="create-a-vm"></a>VM 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.

1. Azure portal에서 새 리소스를 만듭니다. 에 **새로 만들기** 블레이드를 입력 **가상 머신** 검색 상자에 다음 ENTER 키를 누릅니다.

1. 에 **모든** 블레이드 아래에서 **결과**, 클릭 **Windows Server 2016 Datacenter**합니다.

1. 에 **Windows Server 2016 Datacenter** 블레이드에서 클릭 **만들기**합니다.

1. 에 **기본 사항을** 블레이드에서 다음 정보를 사용 하 여 세부 정보를 완료 하 고 클릭 **확인**합니다.

    |설정|값|
    |---|---|
    |이름|DB01|
    |사용자 이름|LocalAdmin|
    |암호 및 암호 확인|Adm1nPa$$word|
    |리소스 그룹|<rgn>[샌드박스 리소스 그룹 이름]</rgn>|
    |위치|*목록에서 지역을 선택합니다*|

1. 에 **크기 선택** 블레이드에서 **D2s_v3**를 클릭 하 고 **선택**.

1. 에 **설정을** 블레이드 아래에 있는 **공용 인바운드 포트 선택** 선택 **HTTP**, **HTTPS**, 및 **RDP (3389)**. 아래 **부트 진단**, 클릭 **비활성**합니다. 다른 모든 설정은 기본값을 유지 하 고 클릭 **확인**합니다.

1. **만들기** 블레이드에서 **만들기**를 클릭합니다.

1. 연습을 계속 하기 전에 배포가 완료 될 때까지 기다립니다.

## <a name="resize-using-the-portal"></a>포털을 사용 하 여 크기 조정

1. Azure portal에서 ExerciseRG 리소스 그룹 및 이동 합니다 **ExerciseRG** 블레이드에서 클릭 합니다 **DB01** 가상 컴퓨터 개체.

1. 에 **DB01** 블레이드에서 클릭 **크기**합니다. 현재 강조 표시 된 크기 참고에는 가상 머신을 만들 때 선택한 크기입니다.

1. 에 **크기 선택** 블레이드에서 찾으려고 시도 합니다 **F2s_v2** 크기-여야 크기의 목록에서 사용할 수 있으므로 VM 현재 실행 중 이며 해당 크기를 다른 제품군에서. 닫기 합니다 **크기 선택** 블레이드입니다.

1. 에 **DB01** 블레이드에서 클릭 **중지**합니다. 에 **이 가상 컴퓨터를 중지** 대화 상자에서 클릭 **예**, 표시할 가상 머신 상태가 될 때까지 기다립니다 **중지 됨 (할당 취소)** 합니다.

1. 에 **DB01** 블레이드에서 클릭 **크기**합니다. 에 **크기 선택** 블레이드에서 **F2s_v2** 클릭 하 고 **선택**합니다. 가상 컴퓨터 크기를 조정 하는 방법에 대 한 알림을 확인할 수 있습니다.

1. 에 **DB01** 블레이드에서 클릭 **개요**를 클릭 하 고 **시작**합니다.

## <a name="resize-using-powershell"></a>PowerShell을 사용 하 여 크기 조정

1. Azure portal에서 Azure Cloud Shell을 엽니다.

1. 사용 가능한 가상 머신 크기의 목록을 가져오려면 다음 cmdlet을 사용 합니다.

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName ExerciseRG -VMName DB01
    ```

1. F4s_v2 크기를 가상 컴퓨터 크기를 조정 하려면 다음 cmdlet을 사용 합니다.

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName ExerciseRG -VMName DB01
    $vm.HardwareProfile.VmSize = "Standard_F4s_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName ExerciseRG
    ```

1. PowerShell 명령 완료를 기다리는 동안 DB01 블레이드에서 새로 고침 단추를 클릭 합니다. 가상 컴퓨터 크기 변경에 맞게 다시 시작 되는 유의 해야 합니다.

이 연습에서는 가상 컴퓨터를 만들고 두 가지 도구를 사용 하 여 크기를 조정 합니다. 염두에 유용한 팁은 가상 머신을 실행 하는 동안 대상 크기를 사용할 수 있는 아닐 수도 가상 컴퓨터를 중지 하 여 더 많은 크기를 선택할 수 있습니다.