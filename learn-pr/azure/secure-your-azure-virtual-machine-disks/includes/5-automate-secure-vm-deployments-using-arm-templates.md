회사에서 클라우드로 전환하는 과정의 일환으로 여러 서버를 배포하는 경우를 가정해 보겠습니다. 디스크가 항상 취약성이 없는 상태로 유지되도록 배포 중에 VM 디스크를 암호화해야 합니다. 이 프로세스를 자동화하고 암호화를 자동으로 사용하도록 Azure Resource Manager 템플릿을 수정해야 합니다.

여기서는 Azure Resource Manager 템플릿을 사용하여 새 Windows VM에 대한 암호화를 자동으로 활성화하는 방법을 살펴보겠습니다.

## <a name="what-are-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿이란?

Resource Manager 템플릿은 Azure에 배포할 리소스 집합을 정의하는 데 사용되는 JSON 파일입니다. 템플릿을 새로 작성할 수도 있고, VM을 비롯한 일부 Azure 리소스의 경우에는 Azure Portal을 사용하여 템플릿을 생성할 수도 있습니다. 수동 VM 배포에 필요한 정보 작성을 완료해야 하지만 VM을 Azure에 배포하는 대신 템플릿을 저장합니다. 그런 다음, 해당 특정 VM 구성을 만들려면 템플릿을 _다시 사용_할 수 있습니다.

모든 종류의 관리 태스크를 자동화하기 위해 [문서에서 사용 가능한 예제 템플릿](https://azure.microsoft.com/resources/templates)이 있습니다. 실제로 수동으로 관리한 VM을 암호화하려면 이러한 템플릿 중 하나를 사용했을 수 있습니다!

![Azure 템플릿을 보여 주는 스크린샷](../media/5-browse-templates.png)

## <a name="using-github-templates"></a>GitHub 템플릿 사용

실제 템플릿 원본은 GitHub에 저장됩니다. GitHub의 템플릿으로 이동하고 페이지에서 Azure로 바로 배포할 수 있습니다.

![강조 표시된 Azure 단추에 배포되는 GitHub 템플릿을 보여 주는 스크린샷](../media/5-deploy-from-github.png)

템플릿이 배포될 때 Azure는 필수 입력 필드 목록을 표시합니다.

![Azure Portal에서 템플릿을 보여 주는 스크린샷](../media/5-fill-in-template.png)

그런 다음, 템플릿을 실행하여 리소스를 만들거나 수정하거나 제거할 수 있습니다.

### <a name="running-templates-in-the-azure-portal"></a>Azure Portal에서 템플릿 실행

사용하려는 템플릿을 이미 알고 있거나 Azure 계정에 템플릿을 저장한 경우 **리소스 만들기** > **템플릿 배포** 리소스를 사용하여 포털에서 정의된 템플릿을 찾아 실행할 수 있습니다. 이름으로 템플릿을 검색할 수 있으며, GUI에서 템플릿을 실행하고 매개 변수 또는 동작을 변경하기 위해 템플릿을 편집할 수 있습니다.

### <a name="running-templates-from-the-command-line"></a>명령줄에서 템플릿 실행

템플릿에 URL을 지정하면 Azure PowerShell에서 템플릿을 실행할 수 있습니다. 예를 들어 다음과 같은 PowerShell 명령을 사용하여 디스크 암호화 템플릿을 실행할 수 있습니다.

```powershell
New-AzureRmResourceGroupDeployment `
    -Name encrypt-disk `
    -ResourceGroupName <resource-group-name> `
    -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

또는 Azure CLI를 선호하는 경우 `group deployment create` 명령을 사용하여 실행할 수 있습니다.

```azurecli
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> \ 
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

