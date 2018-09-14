## <a name="introduction-to-jupyter-for-more-interactive-deep-learning"></a>보다 대화형으로 심층 학습을 진행할 수 있는 Jupyter 소개 

Jupyter Notebook은 라이브 코드, 수식, 시각화 및 내레이션 텍스트를 포함하는 문서를 만들고 공유할 수 있는 오픈 소스 웹 응용 프로그램입니다. 데이터 정리/변환, 숫자 시뮬레이션, 통계 모델링, 데이터 시각화, 기계 학습 등의 용도로 Jupyter Notebook을 사용할 수 있습니다.

## <a name="serving-jupyter-notebooks-with-nvidia-docker-on-an-azure-dsvm"></a>Azure DSVM에서 NVidia Docker를 통해 Jupyter Notebook 제공

### <a name="step-1-create-a-linux-dsvm"></a>1단계: Linux DSVM 만들기

Azure CLI에서 호출 코드 사용

```
code .
```

다음 배포 스키마에 정보를 입력한 다음 parameter_file.json으로 저장합니다.

``` 
{ 
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "adminUsername": { "value" : "YOURUSERNAME FOR NEW DSVM"},
     "adminPassword": { "value" : "PASSWORD FOR NEW DSVM"},
     "vmName": { "value" : "HOSTNAME OF DSVM"},
     "vmSize": { "value" : "VM SIZE For eg: Standard_DS2_v2"},
  }
}
```

사용 가능한 VM 크기 목록은 [Ubuntu DSVM ARM 템플릿](https://azure.microsoft.com/global-infrastructure/services/?WT.mc_id=blog-learning-abornst)에서 확인할 수 있습니다.


### <a name="create-a-resource-group-for-your-dsvm-in-a-region-of-your-choice"></a>선택한 지역에서 DSVM용 리소스 그룹을 만듭니다.
```
az group create --name [[NAME OF RESOURCE GROUP]] --location [[ Data center. For eg: "West US 2"]]
```

사용 가능한 지역 목록은 [Azure 지역](https://github.com/Azure/DataScienceVM/blob/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json)에서 확인할 수 있습니다.

### <a name="deploy-your-dsvm-to-your-new-resource-group"></a>새 리소스 그룹에 DSVM 배포

```
az group deployment create --resource-group  [[NAME OF RESOURCE GROUP ABOVE]]  --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json --parameters parameter_file.json
```

## <a name="step-2-open-the-port-8888-22-on-the-dsvm"></a>2단계: 포트 8888(DSVM에서는 22) 열기 

```
$ az vm open-port -g [[NAME OF RESOURCE GROUP]] -n [[HOSTNAME OF DSVM]] --port 22 --priority 900
$ az vm open-port -g [[NAME OF RESOURCE GROUP]] -n [[HOSTNAME OF DSVM]] --port 8888 --priority 901
```

포트 8888은 Jupyter Notebook용 기본 포트입니다. 포트를 여는 자세한 단계를 확인하려면 [여기를 클릭](https://docs.microsoft.com/azure/virtual-machines/windows/nsg-quickstart-portal?WT.mc_id=blog-medium-abornst)하세요.
 
## <a name="step-3-connect-to-the-dsvm-with-the-azure-shell"></a>3단계: Azure Shell을 사용하여 DSVM에 연결 
 
``` 
ssh myuser@[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com 
``` 

## <a name="step-4-run-jupyter-in-docker-container--link-8888-port-to-the-vm-host"></a>4단계: Docker 컨테이너에서 Jupyter 실행 및 VM 호스트에 8888 포트 연결 

VM과 Docker 컨테이너 간에 포트 8888을 연결하고 Jupyter를 설치한 다음 pytorch 자습서를 가져옵니다.  

```  
sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
  'conda install jupyter matplotlib -y &&\
  curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
  jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
``` 

## <a name="step-5-navigate-to-the-jupyter-notebook-in-the-browser"></a>5단계: 브라우저에서 Jupyter Notebook으로 이동 

Jupyter Notebook이 실행되면 다음 메시지가 표시됩니다. 

> 처음으로 연결할 때 토큰을 사용하여 로그인하려면 http://(5b8783e7911d 또는 127.0.0.1):8888/?token={토큰} URL을 복사하여 브라우저에 붙여넣습니다.

여기서 URL의 **http://(5b8783e7911d 또는 127.0.0.1)** 부분은 **[[DSVM의 호스트 이름]].westus2.cloudapp.azure.com**으로 바꾸고 브라우저의 새 탭에서 다음 주소로 이동합니다.
- [[DSVM의 호스트 이름]].westus2.cloudapp.azure.com:8888/?token={토큰}
