웹 서버를 등록 하 고 경험을 사용자에 게 유용한 되도록 추가 컴퓨팅 기능이 필요 하다 고 실행 중이지만 있습니다. 더 빠르게 실행 하는 VM에 어떻게 확인할 수 있습니까?

데이터 센터에서 성능 문제를 해결 하기 위해 더 강력한 하드웨어로 웹 서버를 이동할 수 있습니다. 문제는 구입, 랙, 및 새 시스템 전원 해야 합니다. Azure를 사용 하 여 답변 훨씬 쉽습니다.

이제 더 강력한 크기로 VM을 확장할 수 있습니다. VM의 크기를 변경 하기 전에 종료 하거나 할당을 취소 해야 합니다.

먼저 어떤 확장 의미 하 고 VM의 할당을 취소 하는 경우를 정의 해 보겠습니다.

## <a name="what-is-scale"></a>확장 이란?

_확장_ 추가 네트워크 대역폭, 메모리, 저장소 또는 성능을 개선 하기 위해 계산 능력을 가리킵니다.  

들어보았을 용어 _강화_ 하 고 _확장_합니다.

수직 또는 수직적 크기 조정, 메모리, 저장소를 늘리거나 계산 능력을 기존 가상 머신에서 의미 합니다. 예를 들어, 웹 또는 데이터베이스 서버에 더 빨리 실행 하도록 추가 메모리를 추가할 수 있습니다.

> [!TIP]
> 할 수도 있습니다 _축소_ 일시적 으로만 강화 하는 데 필요한 경우 시스템입니다.

응용 프로그램을 확장 또는 수평 확장 추가 가상 컴퓨터를 의미 합니다. 예를 들어, 정확히 동일한 방식에서으로 구성 하는 여러 가상 머신 만들기 하 고 부하 분산 장치를 사용 하 여 이들 간에 작업을 배포할 수 있습니다.

## <a name="what-is-deallocation"></a>할당 취소는 무엇입니까?

할당 취소는 VM을 종료 하 고 해당 계산 리소스를 해제 하는 프로세스입니다.

직장에 있든 집에 PC를 종료 하면 운영 체제 프로그램을 닫고 전원 관리 하드웨어 전원을 껐다가를 알립니다.

가상 컴퓨터 할당을 취소 하는 것은 유사 합니다. VM 종료 된 후 Azure 전원을 데 하드웨어를 회수 합니다. 데이터 디스크 및 저장소에 그대로 유지 됩니다. 백업 VM을 시작 하면 중단 했던 위치 선택, PC와 마찬가지로 합니다.

할당을 취소 하면 가상 컴퓨터를 사용 하는 계산 및 네트워크 리소스에 대 한 청구 되지 됩니다. 저장소에 연결 된 모든 디스크에 대 한 계속 지불 이지만 전체 비용을 하는 경우 VM 실행 중이 던 것 보다 훨씬 낮습니다.

여기에서는 할당 취소 하 고 VM 간단 하 게 크기를 조정할 수 있도록 합니다. 하지만 비용을 절감할 수 오랜 기간 동안 Vm 할당을 또한 취소할 수 있습니다. 예를 들어 근무 시간 동안 테스트를 위해 사용 하는 Vm의 은행을 해야 합니다. 밤 및 주말에 자동으로 할당을 취소 하려면 Vm을 예약할 수 있습니다. 런타임에 유지 해야 할 경우 수동으로 다시 시작할 수 있습니다 이러한 합니다.

## <a name="scale-up-your-vm"></a>VM 확장

크기를 지정 하는 회수 **Standard_DS2_v2** VM을 만들 때. 두 개의 가상 Cpu와 7GB 메모리에 현재 VM에 있습니다.

다음 크기를 늘려 보겠습니다 **Standard_DS3_v2**합니다. Cpu 및 14GB 메모리에 대 한 4 개의 가상 VM를 갖게 됩니다.

::: 영역 피벗 = "windows 클라우드"

1. Cloud Shell에서 실행 `az vm deallocate` 할당을 취소 하거나 VM을 중지 합니다.

    ```azurecli
    az vm deallocate \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM
    ```
    이 프로세스는 몇 분 정도 걸립니다.
1. 실행할 `az vm resize` VM의 크기를 늘리려면 **Standard_DS3_v2**합니다.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM \
      --size Standard_DS3_v2
    ```
    업데이트 프로세스는 약 1 분이 걸립니다.
1. 실행 `az vm start` 에 VM을 다시 시작 합니다.

    ```azurecli
    az vm start \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM
    ```
    프로세스는 약 1 분이 걸립니다.
1. 실행 `az vm show` VM가 새 크기를 실행 중인지 확인 합니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myWindowsVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    새 VM 크기를 표시 **Standard_DS3_v2**합니다.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

::: 영역 피벗 = "linux 클라우드"

1. Cloud Shell에서 실행 `az vm deallocate` 할당을 취소 하거나 VM을 중지 합니다.

    ```azurecli
    az vm deallocate \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM
    ```
    이 프로세스는 몇 분 정도 걸립니다.
1. 실행할 `az vm resize` VM의 크기를 늘리려면 **Standard_DS3_v2**합니다.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM \
      --size Standard_DS3_v2
    ```
    업데이트 프로세스는 약 1 분이 걸립니다.
1. 실행 `az vm start` 에 VM을 다시 시작 합니다.

    ```azurecli
    az vm start \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM
    ```
    프로세스는 약 1 분이 걸립니다.
1. 실행 `az vm show` VM가 새 크기를 실행 중인지 확인 합니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myLinuxVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    새 VM 크기를 표시 **Standard_DS3_v2**합니다.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

> [!NOTE]
> 중지 및 다시 시작 하는 경우 기본적으로 Azure VM에 새 공용 IP 주소를 할당 합니다. 학습 목적으로 확인 됩니다. 실제로 VM 다시 시작 하는 경우에 vm에서 유지 되는 공용 IP 주소를 예약할 수 있습니다.

## <a name="summary"></a>요약

잘 하셨습니다! 몇 가지 명령을 사용 하 여 VM이 이제 두 번 강력 합니다.

수직 확장 및 수평 확장 성능을 향상 시키기 위해 두 가지 방법 이며 여기의 계산 능력을 높이기 위해 VM을 확장 합니다.

크기를 조정할 수 전에 VM 할당 취소 합니다. 비용 절감을 위해 사용에서 되지 경우 또한 Vm을 할당 취소 수 있습니다.