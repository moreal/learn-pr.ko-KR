Azure CLI에는 Azure의 가상 머신에서 작동하는 `vm` 명령이 포함되어 있습니다. 여러 하위 명령을 제공하여 특정 작업을 수행할 수 있습니다. 가장 일반적인 하위 명령은 다음과 같습니다.

| 하위 명령 | 설명 |
|-------------|-------------|
| `create`    | 새 가상 머신 만들기 |
| `deallocate` | 가상 머신 할당 취소 |
| `delete` | 가상 머신 삭제 |
| `list` | 구독에 있는 생성된 가상 머신 나열 |
| `open-port` | 인바운드 트래픽에 대해 특정 네트워크 포트 열기 |
| `restart` | 가상 머신 다시 시작 |
| `show` | 가상 머신에 대한 세부 정보 가져오기 |
| `start` | 중지된 가상 머신 시작 |
| `stop` | 실행 중인 가상 머신 중지 |
| `update` | 가상 머신의 속성 업데이트 |

> [!NOTE]
> 전체 명령 목록은 [Azure CLI 참조 설명서](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)에서 확인할 수 있습니다.

첫 번째 항목(`az vm create`)으로 시작하겠습니다. 이 명령은 리소스 그룹에서 가상 머신을 만드는 데 사용됩니다. 새 VM의 모든 측면을 구성하기 위해 전달할 수 있는 여러 매개 변수가 있습니다. 제공해야 하는 세 개의 매개 변수는 다음과 같습니다.

| 매개 변수 | 설명 |
|-----------|-------------|
| `resource-group` | 가상 머신을 소유할 리소스 그룹입니다. |
| `name` | 가상 머신의 이름은 리소스 그룹 내에서 고유해야 합니다. |
| `image` | VM을 만드는 데 사용할 운영 체제 이미지입니다. |

또한 VM이 만들어지는 동안 진행률을 확인하기 위해 `--verbose` 플래그를 추가하는 것이 좋습니다. 

## <a name="create-a-linux-virtual-machine"></a>Linux 가상 머신 만들기

새 Linux 가상 머신을 만들어 보겠습니다. Azure Cloud Shell에서 다음 명령을 실행합니다.

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

이 명령은 이름이 `SampleVM`인 새 **Debian** Linux 가상 머신을 만듭니다. VM을 만드는 동안 Azure CLI 도구가 차단되었습니다. 기다리지 않으려면 `--no-wait` 옵션을 사용하여 즉시 반환하도록 Azure CLI 도구에 지시할 수 있습니다(예: 스크립트에서 명령을 실행 중인 경우). 스크립트의 뒷부분에서 `azure vm wait --name [vm-name]` 명령을 사용하여 VM이 만들어질 때까지 기다리세요.

자세한 응답 내용을 살펴보면 VM에 대한 다양한 종속성을 명명하는 데 `SampleVM` 이름이 사용되는 것을 알 수 있습니다.

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

자동 생성된 이러한 리소스 이름을 재정의하려면 `vm create`에 대한 선택적 매개 변수(예: `--vnet-name` 및 `--public-ip-address-dns-name`)를 사용할 수 있습니다.

여기서는 `admin-username` 플래그를 통해 관리자 계정 이름을 “aldis”로 지정하겠습니다. 이를 생략하면 `vm create` 명령이 _현재 사용자 이름_을 사용합니다. 계정 이름에 대한 규칙이 OS마다 다르므로 고유한 이름을 지정하는 것이 안전합니다. “root” 및 “admin”과 같은 일반적인 이름은 대부분의 이미지에서 허용되지 않습니다.

현재 `generate-ssh-keys` 플래그도 사용하고 있습니다. 이 매개 변수는 Linux 배포에 사용되며, `ssh` 도구를 사용하여 원격으로 가상 머신에 액세스할 수 있도록 보안 키 쌍을 생성합니다. 두 파일은 사용자 머신의 `.ssh` 폴더와 VM에 배치됩니다. 대상 폴더에 이미 `id_rsa`라는 SSH 키가 있는 경우 새 키를 생성하는 대신 이 키가 사용됩니다.

VM 만들기가 완료되면, 가상 머신의 현재 상태와 Azure에서 할당한 공용 및 개인 IP 주소를 포함하는 JSON 응답을 가져올 것입니다.

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

