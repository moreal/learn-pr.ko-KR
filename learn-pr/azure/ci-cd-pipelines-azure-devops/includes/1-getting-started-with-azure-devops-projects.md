CI/CD 파이프라인을 빠르게 설정하는 것은 항상 어려운 과제였습니다. 이제 전체 종단간 Azure DevOps 프로젝트를 처음부터 수행하여 완료하는 것이 믿을 수 없을 정도로 매우 쉽습니다. 그리고 Azure DevOps 프로젝트에서 다음을 얻을 수 있습니다.

1. Azure에서 프로비전되는 인프라

2. VSTS 인스턴스의 팀 프로젝트

3. VSTS 인스턴스의 리포지토리에서 선택한 언어로 된 샘플 앱의 소스 코드

4. 선택한 기술에 적합한 빌드 및 릴리스 파이프라인

그리고 완료되면 Azure DevOps 프로젝트에서 샘플 앱을 가져와서 파이프라인을 통해 Azure에서 프로비전하는 인프라로 빌드하고 릴리스합니다. 그리고 이 모든 것을 몇 번의 클릭만으로 얻을 수 있습니다.

## <a name="create-an-azure-devops-project"></a>Azure DevOps 프로젝트 만들기

Azure Portal에서 Azure DevOps 프로젝트를 만듭니다.

1. [Azure Portal](https://portal.azure.com)로 이동하여 `Create a resource`를 클릭합니다.  
![](/media-draft/1-azureportal.png)

2. `DevOps Project`를 클릭합니다.  
![DevOps 프로젝트 선택](/media-draft/1-pickdevopsproject.png)

3. 다음 화면에서는 사용하려는 언어를 선택할 수 있습니다. .NET(기본), Java, Node, PHP, Python, Ruby 및 Go를 선택하는 방법에 유의하세요. Git 리포지토리에서 사용자 고유의 코드를 가져올 수도 있습니다. 이 단원에서는 Node.js 앱을 만들어 보겠습니다. Node.js를 클릭하고 [다음]을 클릭합니다.  
![언어에 대해 Node.js 선택](/media-draft/1-picknodejsforlang.png)

4. 다음으로, 사용하려는 Node.js 프레임워크를 묻습니다. 이 단원에서는 간단한 Node.js 앱을 선택하고 [다음]을 클릭합니다.  
![간단한 Node 선택](/media-draft/1-picksimplenode.png)

5. 다음으로, 앱을 프로비전하고 실행하려는 인프라를 묻습니다. 이 단원에서는 Azure Kubernetes Service를 사용하여 Kubernetes 클러스터에 프로비전하고 배포해 보겠습니다. Kubernetes Service를 선택하고 [다음]을 클릭합니다.  
![Kubernetes 선택](/media-draft/1-pickkubernetes.png)

6. 이제 완전히 새로운 VSTS 인스턴스를 만들거나 기존 VSTS 인스턴스를 선택할 수 있습니다. 또한 Kubernetes 클러스터를 실행하려는 위치와 방법을 설정할 수도 있습니다. 이 단원에서는 [새로 선택]을 선택하여 새 VSTS 인스턴스를 만들고, VSTS 인스턴스에 고유한 이름을 지정합니다. [프로젝트 학습] 이름을 입력하고, Azure 구독을 선택하고, 클러스터 이름을 LearnCluster로 지정하고, 위치를 [미국 동부]로 선택한 다음, [완료]를 클릭합니다.  
![최종 확인 화면](/media-draft/1-finalconfirmation.png)

그리고 그야말로 있는 그대로입니다! 시간이 좀 걸리므로 Azure에서 수행하도록 내버려 둔 채 잠시 휴식을 취합니다. 대부분의 시간은 Azure 인프라를 프로비전하고 구성하는 데 소요됩니다. 이 모듈의 경우 Azure Kubernetes Service와 Azure Container Registry가 됩니다.

## <a name="a-lap-around-the-finished-azure-devops-project"></a>완성된 Azure DevOps 프로젝트 주위의 환경

Azure가 완료되면 [알림]에서 알려줍니다.

1. [알림], [리소스로 이동]을 차례로 클릭합니다.  
![[알림]에서 [리소스로 이동]](/media-draft/1-gotoresourcefromalert.png)

2. 프로비전된 모든 것을 표시하는 포털 블레이드로 이동합니다. 왼쪽에는 CI/CD 파이프라인이 있습니다. 코드 리포지토리, 빌드 정의 및 릴리스 정의가 있습니다. 모든 링크는 VSTS에서 리소스로 직접 이동하는 딥 링크입니다. 오른쪽에는 Azure에서 배포한 모든 인프라가 표시됩니다. 샘플 앱이 이미 배포된 Kubernetes 클러스터와 Application Insight가 있습니다. 다시금 말하지만, 이러한 모든 링크는 Azure의 리소스에 대한 딥 링크입니다.  
![포털 DevOps 프로젝트](/media-draft/1-pickdevopsproject.png)

3. 소스 코드 링크를 클릭합니다.  
![원본에 연결](/media-draft/1-linktosource.png)

4. VSTS 프로젝트의 Git 리포지토리로 이동합니다. 이 리포지토리는 Helm 차트가 있는 Node.js 샘플 앱을 보유하고 있는 일반적인 Git 리포지토리일 뿐입니다.  
![VSTS 리포지토리](/media-draft/1-vstsrepo.png)

5. 빌드로 이동  
![빌드에 연결](/media-draft/1-navtobuild.png)

6. 빌드를 클릭한 다음, [편집]을 클릭하여 만든 빌드를 편집합니다.  
![](/media-draft/1-editbuildlink.png)

7. 선택한 기술에 적합한 빌드 파이프라인이 표시됩니다. Kubernetes 클러스터에 Node.js 앱을 선택했으므로 Docker 작업을 사용하여 Node.js 앱을 빌드하고, 이미지 컨테이너 이미지를 만든 다음, Helm 작업을 사용하여 Helm 패키지를 만드는 빌드 파이프라인을 얻습니다.  
![빌드 파이프라인](/media-draft/1-buildpipeline.png)

8. `Releases`를 클릭하여 릴리스 파이프라인으로 이동합니다.  
![릴리스로 이동](/media-draft/1-gotoreleases.png)

9. 만든 릴리스 파이프라인이 표시됩니다. 릴리스를 클릭하고 `Edit pipeline`을 선택하여 편집합니다.  
![릴리스 편집](/media-draft/1-editrelease.png)

10. Azure에서 선택한 기술에 적합한 릴리스 파이프라인을 만들었습니다. Kubernetes 클러스터에서 호스팅되는 컨테이너에서 실행되는 Node 응용 프로그램입니다.
![릴리스 파이프라인](/media-draft/1-releasepipeline.png)

11. Azure Portal로 돌아가서 Kubernetes 서비스에 대한 외부 엔드포인트를 클릭합니다.  
![](/media-draft/1-clickonendpoint.png)

12. AKS 클러스터에 빌드되고 배포된 샘플 앱이 표시됩니다.  
![앱 실행](/media-draft/1-apprunning.png)

## <a name="summary"></a>요약

이 단원에서는 다음 요소로 구성된 Azure DevOps 프로젝트를 만들었습니다.

1. 앱용 인프라 - Azure Kubernetes Service 및 Application Insight

2. VSTS 인스턴스의 팀 프로젝트

3. VSTS 인스턴스의 리포지토리에 있는 컨테이너에서 실행되는 Node.js 샘플 앱에 대한 소스 코드

4. Azure Kubernetes Service 인스턴스에서 실행되는 Node.js 컨테이너 앱에 대한 빌드 및 릴리스 파이프라인

다음으로, 샘플 앱을 실제 앱으로 바꾸는 방법을 알아봅니다.