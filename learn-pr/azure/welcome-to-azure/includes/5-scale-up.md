웹 서버가 등록되고 실행되지만 사용자에게 적합한 환경을 만들려면 더 많은 컴퓨팅 기능이 필요함을 인식하고 있습니다. 어떻게 VM을 더 빠르게 실행하게 할 수 있나요?

데이터 센터에서 성능 문제를 해결하려면 웹 서버를 더 강력한 하드웨어로 이동시킬 수 있습니다. 문제는 새 시스템을 구입하고 보관하고 전원을 제공해야 한다는 것입니다. Azure를 사용하면 답변이 훨씬 간단합니다.

더 강력한 크기로 VM을 강화하기 전에 먼저 크기 조정의 의미를 정의하겠습니다.

## <a name="what-is-scale"></a>크기 조정이란?

_크기 조정_은 네트워크 대역폭, 메모리, 저장소 또는 계산 능력을 추가하여 성능을 개선하는 것을 의미합니다.  

_강화_ 및 _확장_이란 용어를 들어보았을 수 있습니다.

수직적 크기 조정 즉, 강화는 기존 가상 머신의 메모리, 저장소 또는 계산 능력을 향상시키는 것을 의미합니다. 예를 들어 웹 또는 데이터베이스 서버에 추가 메모리를 추가하여 더 빨리 실행되도록 할 수 있습니다.

수평적 크기 조정 즉, 확장은 응용 프로그램을 개선하기 위해 가상 머신을 추가하는 것을 의미합니다. 예를 들어, 정확히 동일한 방식으로 구성된 여러 가상 머신을 만들고 부하 분산 장치를 사용하여 가상 머신에 작업을 분산할 수 있습니다.

> [!TIP]
> 클라우드는 탄력적입니다. 일시적으로 강화하거나 확장해야 하는 경우 배포를 _축소_하거나 _감축_할 수 있습니다. 축소 또는 감축은 비용을 절약하는 데 도움이 될 수 있습니다.<br><br>**Azure Advisor** 및 **Azure Cost Management**는 클라우드를 최적화할 수 있는 두 개의 서비스입니다. 이러한 서비스를 사용하여 필요한 것보다 더 많이 사용하는 경우를 식별한 다음, 실제로 사용 중인 용량으로 다시 규모를 조정할 수 있습니다.

## <a name="scale-up-your-vm"></a>VM 강화

앞서 언급한 것처럼 VM을 만들 때 **Standard_DS2_v2** 크기를 지정했습니다. 현재 VM에는 두 개의 가상 CPU와 7GB 메모리가 있습니다.

다음 크기 **Standard_DS3_v2**로 늘려보겠습니다. 그러면, VM에는 4개의 가상 CPU 및 14GB 메모리가 있게 됩니다.

::: zone pivot="windows-cloud"

1. Cloud Shell에서 `az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 증가시킵니다.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    업데이트 프로세스에는 약 1분이 걸립니다. 이 프로세스 동안 VM이 다시 시작됩니다.

1. `az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    새 VM 크기 **Standard_DS3_v2**를 확인합니다.
    ```output
    Standard_DS3_v2
    ```

::: zone-end

::: zone pivot="linux-cloud"

1. Cloud Shell에서 `az vm resize`를 실행하여 VM의 크기를 **Standard_DS3_v2**로 증가시킵니다.

    ```azurecli
    az vm resize \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myVM \
      --size Standard_DS3_v2
    ```
    업데이트 프로세스에는 약 1분이 걸립니다. 이 프로세스 동안 VM이 다시 시작됩니다.

1. `az vm show`를 실행하여 VM이 새 크기를 실행하고 있는지 확인합니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --name myVM \
      --query "hardwareProfile" \
      --output tsv
    ```
    새 VM 크기 **Standard_DS3_v2**를 확인합니다.
    ```output
    Standard_DS3_v2
    ```

::: zone-end

## <a name="summary"></a>요약

잘했습니다! 단 하나의 명령으로 이제 VM이 두 배 강력해집니다.

강화 및 확장은 성능을 향상시키기 위한 두 가지 방법입니다. 여기서 VM을 강화하여 계산 능력을 향상시킵니다.