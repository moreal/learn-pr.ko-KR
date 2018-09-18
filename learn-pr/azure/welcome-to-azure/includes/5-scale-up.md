웹 서버가 등록되고 실행되지만 사용자에게 적합한 환경을 만들려면 더 많은 컴퓨팅 기능이 필요함을 인식하고 있습니다. 어떻게 VM을 더 빠르게 실행하게 할 수 있나요?

데이터 센터에서 성능 문제를 해결하려면 웹 서버를 더 강력한 하드웨어로 이동시킬 수 있습니다. 문제는 새 시스템을 구입하고 보관하고 전원을 제공해야 한다는 것입니다. Azure를 사용하면 답변이 훨씬 간단합니다.

이제 VM을 더 강력한 크기로 확장하겠습니다. VM의 크기를 변경하기 전에 종료하거나 할당을 취소해야 합니다.

먼저 크기 조정이 어떤 의미인지, VM 할당을 취소하는 경우 무슨 일이 발생하는지를 정의해보겠습니다.

## <a name="what-is-scale"></a>크기 조정이란?

_크기 조정_은 네트워크 대역폭, 메모리, 저장소 또는 계산 능력을 추가하여 성능을 개선하는 것을 말합니다.  

_확장_ 및 _스케일 아웃_이란 용어를 들어보았을 수 있습니다.

수직적 크기 조정 즉, 확장은 기존 가상 머신의 메모리, 저장소 또는 계산 능력을 향상시키는 것을 의미합니다. 예를 들어 웹 또는 데이터베이스 서버에 추가 메모리를 추가하여 더 빨리 실행되도록 할 수 있습니다.

> [!TIP]
> 일시적으로 확장해야 하는 경우 시스템을 _축소_할 수도 있습니다.

수평적 크기 조정 즉, 스케일 아웃은 응용 프로그램에 전원을 제공하기 위해 가상 머신을 추가하는 것을 의미합니다. 예를 들어, 정확히 동일한 방식으로 구성된 여러 가상 머신을 만들고 부하 분산 장치를 사용하여 가상 머신에 작업을 분산할 수 있습니다.

## <a name="what-is-deallocation"></a>할당 취소란?

할당 취소는 VM을 종료하고 해당 계산 리소스를 릴리스하는 프로세스입니다.

직장이나 집의 PC를 종료하는 경우 운영 체제는 프로그램을 닫은 다음, 전원 관리 하드웨어에 전원을 끄도록 지시합니다.

가상 머신 할당 취소는 유사합니다. VM이 종료된 후 Azure는 VM에 전원을 제공하는 데 사용된 하드웨어를 회수합니다. 데이터 디스크 및 저장소는 그대로 유지됩니다. VM 백업을 시작하면 PC와 마찬가지로 중단했던 위치를 선택합니다.

할당을 취소하면 가상 머신이 사용하는 계산 및 네트워크 리소스에 대해 청구되지 않습니다. 저장소에 연결된 모든 디스크에 대해서는 여전히 지불하지만 전체 비용은 VM이 실행 중인 경우보다 훨씬 저렴합니다.

여기에는 크기를 조정할 수 있도록 간단히 VM의 할당을 취소합니다. 하지만 비용을 절감하려면 오랜 기간 동안 VM의 할당을 취소할 수도 있습니다. 근무 시간 동안 테스트를 위해 사용하는 VM의 은행이 있다고 가정해봅시다. 밤 및 주말에도 자동으로 할당이 취소되도록 VM을 예약할 수 있습니다. 밤을 세워야 할 경우 수동으로 VM을 다시 시작할 수 있습니다.

## <a name="scale-up-your-vm"></a>VM 확장

앞서 언급한 것처럼 VM을 만들 때 **Standard_DS2_v2** 크기를 지정했습니다. 현재 VM에는 두 개의 가상 CPU와 7GB 메모리가 있습니다.

다음 크기 **Standard_DS3_v2**로 늘려보겠습니다. 그러면, VM에는 4개의 가상 CPU 및 14GB 메모리가 있게 됩니다.

::: zone pivot="windows-cloud"

1. Cloud Shell에서 `az vm deallocate`를 실행하여 VM의 할당을 취소하거나 중지합니다.

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    이 프로세스는 완료되는 데 몇 분이 걸립니다.
1. `az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 늘립니다.

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --size Standard_DS3_v2
    ```
    업데이트 프로세스는 약 1분이 걸립니다.
1. `az vm start`를 실행하여 VM 다시 시작합니다.

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myWindowsVM
    ```
    이 프로세스는 약 1분이 걸립니다.
1. `az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myWindowsVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    새 VM 크기 **Standard_DS3_v2**를 확인합니다.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

::: zone pivot="linux-cloud"

1. Cloud Shell에서 `az vm deallocate`를 실행하여 VM의 할당을 취소하거나 중지합니다.

    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    이 프로세스는 완료되는 데 몇 분이 걸립니다.
1. `az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 늘립니다.

    ```azurecli
    az vm resize \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --size Standard_DS3_v2
    ```
    업데이트 프로세스는 약 1분이 걸립니다.
1. `az vm start`를 실행하여 VM 다시 시작합니다.

    ```azurecli
    az vm start \
      --resource-group myResourceGroup \
      --name myLinuxVM
    ```
    이 프로세스는 약 1분이 걸립니다.
1. `az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.

    ```azurecli
    az vm show \
      --resource-group myResourceGroup \
      --name myLinuxVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    새 VM 크기 **Standard_DS3_v2**를 확인합니다.
    ```console
    Standard_DS3_v2
    ```

::: zone-end

> [!NOTE]
> 기본적으로 VM을 중지하고 다시 시작하는 경우 Azure는 VM에 새 공용 IP 주소를 할당합니다. 이 과정은 학습 목적으로 좋습니다. 실제로 VM을 다시 시작하는 경우에도 VM에 포함된 공용 IP 주소를 예약할 수 있습니다.

## <a name="summary"></a>요약

잘 하셨습니다! 단 몇 가지 명령으로 이제 VM이 두 배 강력해집니다.

확장 및 스케일 아웃은 성능을 향상시키기 위한 두 가지 방법입니다. 여기서 VM을 확장하여 계산 능력을 향상시킵니다.

크기를 조정할 수 있기 전에 VM의 할당을 취소합니다. VM이 비용 절감을 위해 사용되지 않는 경우에도 VM의 할당을 취소할 수 있습니다.