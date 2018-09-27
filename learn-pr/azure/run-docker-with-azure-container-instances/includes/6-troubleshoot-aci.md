여기에서는 컨테이너 로그, 컨테이너 이벤트 끌어오기 및 컨테이너 인스턴스에 연결과 같은 몇 가지 기본적인 문제 해결 작업을 수행합니다. 이 모듈을 마치면 컨테이너 인스턴스 문제 해결을 위한 기본적인 기능을 이해할 수 있습니다.

## <a name="create-a-container"></a>컨테이너 만들기

다음 컨테이너를 만들어 시작합니다. 

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/sample-aks-helloworld \
    --ports 80 \
    --ip-address Public \
    --location eastus
```

## <a name="get-logs-from-a-container-instance"></a>컨테이너 인스턴스에서 로그 가져오기

컨테이너 내의 응용 프로그램 코드에서 로그를 보려면 `az container logs` 명령을 사용할 수 있습니다.

```azurecli
az container logs \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer
```

예제 출력:

```output
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
Running inside /app/prestart.sh, you could add migrations to this file, e.g.:

#! /usr/bin/env bash

# Let the DB start
sleep 10;
# Run migrations
alembic upgrade head
```

## <a name="get-container-events"></a>컨테이너 이벤트 가져오기

`az container attach` 명령은 컨테이너 시작 중에 진단 정보를 제공합니다. 컨테이너가 시작되면 로컬 콘솔에 STDOUT 및 STDERR도 스트리밍합니다.

```azurecli
az container attach \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer
```

예제 출력:

```output
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-09-21 23:48:14+00:00) pulling image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:09+00:00) Successfully pulled image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:12+00:00) Created container
(count: 1) (last timestamp: 2018-09-21 23:49:13+00:00) Started container

Start streaming logs:
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
```

> [!TIP]
> 연결된 컨테이너에서 연결을 끊으려면 <kbd>Ctrl+C</kbd>를 누릅니다.

## <a name="execute-a-command-in-a-container"></a>컨테이너에서 명령 실행

Azure Container Instances는 실행 중인 컨테이너에서 명령을 실행하도록 지원합니다. 시작한 컨테이너에서 명령을 실행하면 응용 프로그램 개발 및 문제 해결 중에 특히 유용합니다. 이 기능은 일반적으로 실행 중인 컨테이너에서 문제를 디버그할 수 있도록 대화형 셸을 시작하는 데 사용됩니다.

이 예제는 실행 중인 컨테이너를 사용하여 대화형 터미널 세션을 시작합니다.

```azurecli
az container exec \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --exec-command /bin/sh
```

이 명령이 완료되면 컨테이너 내부에서 효과적으로 작업할 수 있습니다. 이 예제에서는 `ls` 명령을 실행하여 작업 디렉터리의 내용을 표시하였습니다.

```output
# ls
__pycache__  main.py  prestart.sh  static  templates  uwsgi.ini
```

`exit`를 실행하여 원격 세션을 중지합니다.

## <a name="monitor-container-cpu-and-memory"></a>컨테이너 CPU 및 메모리 모니터링

CPU 및 메모리 사용량에 대한 메트릭을 끌어올 수 있습니다. 이렇게 하려면 먼저 Azure 컨테이너 인스턴스의 ID를 가져옵니다. 이 예제에서 이 ID는 `CONTAINER_ID` 변수에 있습니다.

```azurecli
CONTAINER_ID=$(az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name mycontainer --query id --output tsv)
```

이제 `az monitor metrics list` 명령을 사용하여 CPU 사용량 정보를 다시 끌어옵니다.

```azurecli
az monitor metrics list \
    --resource $CONTAINER_ID \
    --metric CPUUsage \
    --output table
```

예제 출력:

```output
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:39:00  CPU Usage
2018-08-20 21:40:00  CPU Usage
2018-08-20 21:41:00  CPU Usage
2018-08-20 21:42:00  CPU Usage
2018-08-20 21:43:00  CPU Usage      0.375
2018-08-20 21:44:00  CPU Usage      0.875
2018-08-20 21:45:00  CPU Usage      1
2018-08-20 21:46:00  CPU Usage      3.625
2018-08-20 21:47:00  CPU Usage      1.5
2018-08-20 21:48:00  CPU Usage      2.75
2018-08-20 21:49:00  CPU Usage      1.625
2018-08-20 21:50:00  CPU Usage      0.625
2018-08-20 21:51:00  CPU Usage      0.5
2018-08-20 21:52:00  CPU Usage      0.5
2018-08-20 21:53:00  CPU Usage      0.5
```

다음 명령을 사용하여 메모리 사용량 정보를 가져올 수 있습니다.

```azurecli
az monitor metrics list \
    --resource $CONTAINER_ID \
    --metric MemoryUsage \
    --output table
```

예제 출력:

```output
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:43:00  Memory Usage
2018-08-20 21:44:00  Memory Usage  0.0
2018-08-20 21:45:00  Memory Usage  15917056.0
2018-08-20 21:46:00  Memory Usage  16744448.0
2018-08-20 21:47:00  Memory Usage  16842752.0
2018-08-20 21:48:00  Memory Usage  17190912.0
2018-08-20 21:49:00  Memory Usage  17506304.0
2018-08-20 21:50:00  Memory Usage  17702912.0
2018-08-20 21:51:00  Memory Usage  17965056.0
2018-08-20 21:52:00  Memory Usage  18509824.0
2018-08-20 21:53:00  Memory Usage  18649088.0
2018-08-20 21:54:00  Memory Usage  18845696.0
2018-08-20 21:55:00  Memory Usage  19181568.0
```

이 정보는 Azure Portal에서도 사용할 수 있습니다. CPU 및 메모리 사용량 정보의 시각적 표현을 보려면 컨테이너 인스턴스에 대한 Azure Portal 개요 페이지를 방문하세요.

![Azure Container Instances CPU 및 메모리 사용량 정보의 Azure Portal 보기](../media/6-cpu-memory.png)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
