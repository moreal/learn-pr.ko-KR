예상 업무에 맞게 가상 머신의 크기를 적절히 조정해야 합니다. 올바른 메모리 또는 CPU가 없는 VM은 로드되지 않거나, 실행 속도가 너무 느려서 효과적이지 않습니다. 

## <a name="pre-defined-vm-sizes"></a>미리 정의된 VM 크기

가상 머신을 만들 때, VM에 사용할 계산 리소스의 양을 결정하는 _VM 크기_ 값을 제공할 수 있습니다. 여기에는 Azure에서 가상 머신에 사용할 수 있는 CPU, GPU 및 메모리가 포함됩니다.

Azure는 예상 사용량을 기반으로 선택할 수 있도록 Linux 및 Windows용 미리 정의된 VM 크기 집합을 정의합니다. 

| 형식 | 크기 | 설명 |
|------|-------|-------------|
| 범용 가상 컴퓨터   | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | CPU 대 메모리 비율이 적당합니다. 개발/테스트와 소규모에서 중간 정도의 응용 프로그램 및 데이터 솔루션에 적합합니다. |
| 계산 최적화 | Fs, F | CPU 대 메모리 비율이 높습니다. 트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다. |
| 메모리 최적화  | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | 메모리 대 코어 비율이 높습니다. 관계형 데이터베이스, 중대형 캐시 및 메모리 내 분석에 적합합니다. |
| 저장소 최적화 | Ls | 높은 디스크 처리량 및 IO 빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다. |
| GPU에 최적화 | NV, NC | 대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다. |
| 고성능 | H, A8-11 | 당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다. | 

사용 가능한 크기는 VM을 만들고 있는 지역에 따라 달라집니다. `vm list-sizes` 명령을 사용하여 사용 가능한 크기 목록을 가져올 수 있습니다. Azure Cloud Shell에 이 명령을 입력해 보세요.

```azurecli
az vm list-sizes --location eastus --output table
```

다음은 `eastus`에 대한 간략한 응답입니다.

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

## <a name="specifying-a-size-during-vm-creation"></a>VM 생성 중 크기 지정

VM을 만들 때 크기를 지정하지 않았으므로, Azure에서는 `Standard_DS1_v2`의 기본 범용 크기를 선택했습니다. 그러나 `--size` 매개 변수를 사용하여 `vm create` 명령의 일부로 크기를 지정할 수 있습니다. 예를 들어, 다음 명령을 사용하여 16코어 가상 머신을 만들 수 있습니다.

```azurecli
az vm create --resource-group <rgn>[Sandbox resource group name]</rgn> --name SampleVM2 \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

> [!WARNING]
> 구독 계층은 생성할 수 있는 리소스 수와 해당 리소스의 전체 크기에 대한 [제한을 적용](https://docs.microsoft.com/azure/azure-subscription-service-limits)합니다. 예를 들어, 종량제 구독에서는 **20개의 가상 CPU**로, 평가판 계층에는 **4개의 vCPU**만으로 제한합니다. Azure CLI는 이 한도를 초과할 때 **할당량이 초과됨** 오류로 알려줍니다. 유료 구독에서 이 오류가 발생하면 [평가판 온라인 요청](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-quota-errors)을 통해 유료 구독과 관련된 제한(최대 10,000개의 vCPU!)을 올리도록 요청할 수 있습니다.

## <a name="resizing-an-existing-vm"></a>기존 VM 크기 조정
워크로드가 변경되거나 생성 시 크기가 잘못 조정된 경우에도 기존 VM의 크기를 조정할 수 있습니다. 크기를 조정하기 전에 먼저 VM이 포함된 클러스터에서 원하는 크기를 사용할 수 있는지 확인해야 합니다. 이 경우 `vm list-vm-resize-options` 명령을 사용할 수 있습니다.

```azurecli
az vm list-vm-resize-options --resource-group <rgn>[Sandbox resource group name]</rgn> --name SampleVM --output table
```

이 명령은 리소스 그룹에서 사용 가능한 모든 크기 구성의 목록을 반환합니다. 클러스터에서는 사용할 수 없지만 지역에서는 사용할 수 _있는_ 크기인 경우 [VM 할당을 취소](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate)할 수 있습니다. 이 명령은 실행 중인 VM을 중지한 후 리소스의 손실 없이 현재 클러스터에서 제거합니다. 그런 다음, 크기를 조정할 수 있습니다. 그러면 크기 구성을 사용할 수 있는 새 클러스터에서 VM이 다시 만들어집니다.

> [!NOTE]
> Azure 샌드박스 몇 가지 VM 크기로 제한됩니다. 무료 Microsoft Learning 구독에서는 대부분의 가능성이 허용되지 않습니다.

VM의 크기를 조정하려면 `vm resize` 명령을 사용합니다. 예를 들어 수행하려는 작업에 대해 VM의 성능이 부족한 것을 알게 될 수도 있습니다. vCore가 4개 메모리가 14G인 DS3_v2 계층으로 몇 단계를 높일 수 있습니다. 다음 명령을 Cloud Shell에 입력하세요.

```azurecli
az vm resize --resource-group <rgn>[Sandbox resource group name]</rgn> --name SampleVM --size Standard_DS3_v2
```

이 명령으로 VM의 리소스를 줄이는 데 몇 분 정도 소요되며, 완료되면 새 JSON 구성이 반환됩니다.