VM에서 시도하려는 마지막 항목은 웹 서버를 설치하는 것입니다. 설치할 가장 쉬운 패키지 중 하나는 `nginx` 입니다.

1. Linux 가상 머신의 공용 IP 주소를 찾습니다. `vm list-ip-addresses` 명령을 사용하여 검색할 수 있습니다.

2. 그런 다음, 테스트할 때 수행한 것처럼 머신에 대한 `ssh` 연결을 엽니다. 관리자 이름(“**aldis**”)을 전달해야 합니다.

3. 제공된 셸에서 다음 명령을 실행하여 `nginx` 웹 서버를 설치합니다.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. Azure Cloud Shell에서 `curl`을 사용하여 Linux 웹 서버의 기본 페이지를 읽어보세요. 또는 새 브라우저 탭을 열고 공용 IP 주소로 이동할 수 있습니다.

```azurecli
curl 168.61.54.62
```

Linux 가상 머신이 기본 제공 방화벽을 통해 포트 80(`http`)을 노출하지 않기 때문에 이동에 실패합니다. 다행히 Azure CLI에는 이를 위한 `vm open-port` 명령이 있습니다. 

5. Cloud Shell에 다음을 입력하여 포트 80을 엽니다.

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

마지막으로 `curl`을 다시 시도합니다. 이번에는 데이터가 반환됩니다. 브라우저에서도 페이지를 볼 수 있습니다.



