CI/CD 파이프라인 설정에 항상 신속 하 게 할 힘든 되었습니다. 이제는 전혀 전체 종단 간 Azure DevOps 프로젝트를 처음부터 이동 하기가 무척 쉬워집니다. 및 Azure DevOps 프로젝트에서 다음을 표시 합니다.

1. 인프라를 Azure에서 프로 비전 합니다.

2. VSTS 인스턴스에 팀 프로젝트입니다.

3. VSTS 인스턴스 리포지토리에서 선택한 언어로 샘플 앱에 대 한 소스 코드입니다.

4. 빌드 및 릴리스 파이프라인에 대 한 적합 한 기술을 선택 합니다.

시점과 해당 완료의 Azure DevOps 프로젝트 샘플 앱 사용, 작성 및 프로 비전 하기를 Azure에서 인프라에는 파이프라인을 통해 해제 합니다. 및 몇 번의 클릭을 사용 하 여이 모두 활용할 수 있습니다.

## <a name="create-an-azure-devops-project"></a>Azure DevOps 프로젝트 만들기

Azure portal에서 Azure DevOps 프로젝트를 만듭니다.

1. 이동 하 여 [Azure Portal](https://portal.azure.com) 클릭 `Create a resource`  
![AzurePortal](../media-drafts/1-azureportal.png)

2. `DevOps Project`을 클릭합니다.  
![DevOps 프로젝트를 선택 합니다.](../media-drafts/1-pickdevopsproject.png)

3. 다음 화면은 사용 하려는 언어를 선택 하는 단계입니다. 선택할 때.NET (물론), java, 노드, php, python, ruby 및 go 알 수 있습니다. 도 git 리포지토리에서 고유한 코드를 가져올 수 있습니다. 이 장치에 대 한 계속 해 서 Node.js 앱을 만듭니다. Node.js를 클릭 한 다음을 클릭 합니다.  
![언어에 대 한 Node.js를 선택 합니다.](../media-drafts/1-picknodejsforlang.png)

4. 다음 요청 하는 node.js 프레임 워크를 사용 하려는 것입니다. 이 장치에 대 한 간단한 Node.js 앱을 선택 하 고 클릭  
![간단한 노드를 선택 합니다.](../media-drafts/1-picksimplenode.png)

5. 다음으로 인프라 프로 비전 하려는 있으며 수에서 앱을 실행할 사용자에 게 묻는 것입니다? 이 장치에 대 한 프로 비전 하 고 Azure Kubernetes Service를 사용 하 여 Kubernetes 클러스터에 배포 해 보겠습니다. Kubernetes 서비스를 선택한 다음을 클릭 합니다.  
![Kubernetes를 선택 합니다.](../media-drafts/1-pickkubernetes.png)

6. 및 이제 VSTS의 새 인스턴스를 만들고 하거나 기존 항목을 선택 합니다. Kubernetes 클러스터를 사용할 위치와 방법을 실행 하도록 설정에 액세스할 수도 있습니다. 이 장치에 대 한 진행 하 고 새로 만들기 선택을 선택 하 여 새 VSTS 인스턴스를 만듭니다 VSTS 인스턴스는 고유한 이름을 지정 합니다. 프로젝트 이름에 대 한 학습 입력, azure 구독을 선택, 클러스터 이름을 LearnCluster 이름을, 미국 동부 위치 및 수행 하는 클릭에 대 한 선택  
![](../media-drafts/1-finalconfirmation2.png)

이며 있는 그대로! 걸립니다이 다시 시작 하므로, 완화 및만 해당 작업을 수행 하는 Azure를 사용 합니다. 대부분의 경우 프로 비전 및 Azure 인프라를 구성 하는 데 걸린 수 됩니다. 이 모듈에 대 한 Azure Kubernetes Service 및 Azure Container Registry에 됩니다.

## <a name="a-lap-around-the-finished-azure-devops-project"></a>완료 된 Azure DevOps 프로젝트 주위의 랩

Azure가 완료 되 면 알림이 표시 됩니다 경고에서

1. 경고를 클릭 하 고 리소스 이동  
![경고에서 리소스로 이동](../media-drafts/1-gotoresourcefromalert.png)

2. 이 프로 비전 된 모든 항목을 표시 하는 포털 블레이드로 이동 합니다. 왼쪽에 CI/CD 파이프라인. 코드 리포지토리, 빌드 정 및 릴리스 정의 해야합니다. 모든 링크는 VSTS에서 리소스를 직접 이동 하는 딥 링크. 및 Azure에 배포 된 모든 인프라 오른쪽에 표시 합니다. 에 이미 배포 된 샘플 앱을 사용 하 여 Kubernetes 클러스터 및 응용 프로그램 이해 해야 합니다. 이번에 이러한 모든 링크는 Azure의 리소스에 대 한 딥 링크.  
![포털 DevOps Proj](../media-drafts/1-portaldevopsproj.png)

3. 소스 코드에 대 한 링크를 클릭  
![원본에 연결](../media-drafts/1-linktosource.png)

4. Azure 코드의 git 리포지토리로 이동 합니다. 이 helm 차트를 사용 하 여 샘플 node.js 앱을 보유 하는 일반 git 리포지토리를 확인 합니다.  
![Azure 리포지토리](../media-drafts/1-azurerepo.png)

5. 빌드로 이동  
![빌드에 연결](../media-drafts/1-linktobuild.png)

6. 빌드를 클릭 하 여 생성된 된 빌드를 편집 하 고 편집을 클릭  
![빌드 링크 편집](../media-drafts/1-editbuildlink2.png)

7. 적합 한 선택 기술에 대 한 빌드 파이프라인을 볼 수 있습니다. Kubernetes 클러스터에 node.js 앱을 선택 했습니다 있으므로 Docker 작업을 사용 하 여 Node.js 앱을 빌드하고 이미지 컨테이너 이미지 만들기, Helm 패키지를 만드는 작업을 다음 Helm 하는 빌드 파이프라인을 가져옵니다.  
![파이프라인 빌드](../media-drafts/1-buildpipeline2.png)

8. 클릭 하 여 릴리스 파이프라인으로 이동 `Releases`  
![릴리스 링크](../media-drafts/1-gotoreleaselink.png)

9. 만든 릴리스 파이프라인을 볼 수 있습니다. 릴리스를 클릭 하 고 선택 하 여 편집 `Edit pipeline`  
![릴리스 편집](../media-drafts/1-editrelease2.png)

10. Azure에 적합 한 선택 기술에 대 한 릴리스 파이프라인을 만들었습니다. Kubernetes 클러스터에서 호스트 되는 컨테이너에서 실행 되는 노드 앱.
![릴리스 파이프라인](../media-drafts/1-releasepipeline2.png)  
![릴리스 파이프라인 단계](../media-drafts/1-pipelinesteps.png)

11. Azure portal로 돌아가서 kubernetes 서비스에 대 한 외부 끝점을 클릭  
![](../media-drafts/1-clickonendpoint.png)

12. 샘플 앱이 빌드 하는지 확인 하 고 AKS 클러스터에 배포  
![실행 중인 앱](../media-drafts/1-apprunning.png)

## <a name="summary"></a>요약

이 단위에 구성 된 Azure DevOps 프로젝트를 만들었습니다.

1. Azure Kubernetes Service 및 Application Insight 앱에 대 한 인프라

2. VSTS 인스턴스에 팀 프로젝트입니다.

3. VSTS 인스턴스 리포지토리에서 컨테이너에서 실행 되는 Node.js 샘플 앱에 대 한 소스 코드입니다.

4. Azure Kubernetes Service 인스턴스에서 실행 되는 Node.js 컨테이너 앱에 대 한 빌드 및 릴리스 파이프라인입니다.

다음으로 실제 앱을 사용 하 여 샘플 앱을 대체 하는 방법에 알아봅니다.