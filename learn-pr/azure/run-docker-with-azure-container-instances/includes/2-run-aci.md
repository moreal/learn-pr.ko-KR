Azure Container Instances를 사용하면 가상 머신을 프로비전하거나 상위 수준 서비스를 도입하지 않고도 Azure에서 Docker 컨테이너를 쉽게 만들고 관리할 수 있습니다. 이 단원에서는 Azure에서 컨테이너를 만들어서 FQDN(정규화된 도메인 이름)으로 인터넷에 노출합니다.

## <a name="create-a-container"></a>컨테이너 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

**az container create** 명령에 이름, Docker 이미지 및 Azure 리소스 그룹을 제공하여 컨테이너를 만들 수 있습니다. 필요에 따라 DNS 이름 레이블을 지정하여 컨테이너를 인터넷에 노출할 수 있습니다. 이 예제에서는 작은 웹앱을 호스트하는 컨테이너를 배포합니다.

컨테이너 인스턴스를 시작 하려면 Cloud Shell에서 다음 명령을 실행 합니다. *--dns-name-label* 값은 인스턴스를 만드는 Azure 지역 내에서 고유해야 하므로 고유성을 유지하기 위해 이 값을 수정해야 할 수도 있습니다.

```azurecli
az container create \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label aci-demo
```

몇 초 안에 요청에 대한 응답이 있어야 합니다. 처음에는 컨테이너가 **만드는 중** 상태가 되지만 몇 초 이내 시작됩니다. `az container show` 명령을 사용하여 상태를 확인할 수 있습니다.

```azurecli
az container show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

명령을 실행하면 컨테이너의 FQDN(정규화된 도메인 이름) 및 프로비저닝 상태가 표시됩니다.

```output
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

컨테이너가 **성공** 상태로 전환되면 브라우저에서 해당 FQDN으로 이동합니다.

![Azure 컨테이너 인스턴스에서 실행되는 응용 프로그램을 보여주는 브라우저 스크린샷](../media-draft/aci-app-browser.png)

## <a name="summary"></a>요약

이 단원에서는 웹 서버 및 응용 프로그램을 실행하는 Azure 컨테이너 인스턴스를 만들었습니다. 또한 컨테이너 인스턴스의 FQDN을 사용하여 이 응용 프로그램에 액세스했습니다.

다음 단원에서는 컨테이너 인스턴스 다시 시작 정책을 구성합니다.