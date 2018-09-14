Azure Container Instances에서는 컨테이너를 배포하기가 쉽고 빠르므로 컨테이너 인스턴스에서 빌드, 테스트 및 이미지 렌더링과 같은 일회성 작업을 실행하기 위한 강력한 플랫폼을 제공합니다.

구성 가능한 다시 시작 정책을 사용하면 프로세스가 완료될 때 컨테이너가 중지되도록 지정할 수 있습니다. 컨테이너 인스턴스는 초 단위로 비용이 청구되기 때문에 작업을 실행하는 컨테이너가 실행되는 동안 사용된 계산 리소스에 대해서만 요금이 부과됩니다.

## <a name="container-restart-policies"></a>컨테이너 다시 시작 정책

Azure Container Instances에서 컨테이너를 만들 때 세 가지 다시 시작 정책 설정 중 하나를 지정할 수 있습니다.

| 다시 시작 정책   | 설명 |
| ---------------- | :---------- |
| `Always` | 컨테이너 그룹의 컨테이너가 항상 다시 시작됩니다. 컨테이너를 만들 때 다시 시작 정책이 지정되지 않은 경우 적용되는 **기본** 설정입니다. |
| `Never` | 컨테이너 그룹의 컨테이너가 절대로 다시 시작되지 않습니다. 컨테이너가 한 번만 실행됩니다. |
| `OnFailure` | 컨테이너 그룹의 컨테이너가 컨테이너에서 실행된 프로세스가 실패할 때만(0이 아닌 종료 코드로 종료될 때) 다시 시작됩니다. 컨테이너가 한 번 이상 실행됩니다. |

이 모듈의 이전 단원에서는 지정된 다시 시작 정책 없이 컨테이너가 생성되었습니다. 기본적으로 이 컨테이너는 *Always* 다시 시작 정책을 받았습니다. 컨테이너의 워크로드가 장기 실행되므로(웹 서버) 이 정책이 적합합니다.

## <a name="run-to-completion"></a>완료될 때까지 실행

다시 시작 정책이 작동하는 것을 보려면 *microsoft/aci-wordcount* 이미지에서 컨테이너 인스턴스를 만들고 *OnFailure* 다시 시작 정책을 지정합니다. 이 예제 컨테이너는 셰익스피어의 Hamlet 텍스트를 분석하고, 가장 많이 쓰이는 10개의 단어를 STDOUT에 쓰고 종료하는 Python 스크립트를 실행합니다.

다음 `az container create` 명령을 사용하여 예제 컨테이너를 실행합니다.

```azureclu
az container create \
    --resource-group myResourceGroup \
    --name mycontainer-restart-demo \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure
```

Azure Container Instances는 컨테이너를 시작한 다음, 응용 프로그램(또는 이 경우 스크립트)이 종료될 때 컨테이너를 중지합니다. Azure Container Instances가 다시 시작 정책이 *Never* 또는 *OnFailure*인 컨테이너를 중지하면 컨테이너의 상태가 **Terminated**로 설정됩니다.

다음과 같이 `az container show` 명령으로 컨테이너의 상태를 확인할 수 있습니다.

```azurecli
az container show \
    --resource-group myResourceGroup \
    --name mycontainer-restart-demo \
    --query containers[0].instanceView.currentState.state
```

예제 컨테이너의 상태가 **Terminated**로 표시되면 컨테이너 로그를 확인하여 작업 출력을 볼 수 있습니다. 스크립트의 출력을 보려면 **az container logs** 명령을 실행합니다.

```azurecli
az container logs --resource-group myResourceGroup --name mycontainer-restart-demo
```

출력:

```bash
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]
```

## <a name="summary"></a>요약

이 단원에서는 다시 시작 정책 *OnFailure*를 사용하여 컨테이너 인스턴스를 만들었습니다. 이 구성은 단기 작업을 실행하는 컨테이너에 적합합니다.

다음 단원에서는 Azure Container Instance에서 환경 변수를 설정합니다.
