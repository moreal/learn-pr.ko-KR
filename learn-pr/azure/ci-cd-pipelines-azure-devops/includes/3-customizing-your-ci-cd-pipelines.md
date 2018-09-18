Azure DevOps 프로젝트의 즉시 사용 가능한 환경은 선택된 방법에 적합한 빌드 및 릴리스 파이프라인을 만듭니다. 이 모듈에서는 Kubernetes 클러스터에 호스트되는 컨테이너에서 실행되는 node.js 앱에 적합한 빌드 및 릴리스 파이프라인을 만들었습니다. 

종종 프로젝트와 관련된 작업을 수행하기 위해 빌드 및 릴리스 파이프라인을 사용자 지정해야 할 때가 종종 있습니다. VSTS의 빌드 및 릴리스 파이프라인은 100% 사용자 지정이 가능합니다. 파이프라인으로 필요한 모든 일을 할 수 있습니다.

이 모듈에서는 빌드 및 릴리스 파이프라인을 사용자 지정하는 방법을 알아보겠습니다.

## <a name="customize-the-build-pipeline"></a>빌드 파이프라인 사용자 지정

VSTS의 빌드 엔진은 작업을 하나씩 차례로 수행하는 작업 실행기입니다. 빌드를 사용자 지정하려면 작업을 추가 또는 제거하고 작업의 올바른 매개 변수를 채워야 합니다.

기본적으로 VSTS는 사용 가능한 약 100개의 작업을 제공합니다. 기본 제공되지 않는 다른 작업을 해야 하는 경우 700개가 넘는 빌드 및 릴리스 작업을 다운로드하여 사용할 수 있는 마켓플레이스를 확인하세요. 사용자 고유의 사용자 지정 작업을 작성하는 기능도 있습니다.

이 모듈에서는 코드의 보안을 검사하는 마켓플레이스 작업 WhiteSource Bolt를 설치하여 빌드 파이프라인을 사용자 지정할 것입니다.

1. Azure Portal에서 Azure DevOps 프로젝트를 찾아 빌드 정의 링크를 클릭합니다.  
![빌드 링크](/media-draft/3-buildlink.png)

2. 빌드 파이프라인 페이지로 이동됩니다. 빌드를 클릭하고 `Edit`를 선택합니다.  
![빌드 편집](/media-draft/3-editbuild.png)

3. 빌드 정의로 이동됩니다. `+`를 클릭하여 에이전트 작업 1에 작업을 추가합니다.  
![작업 추가](/media-draft/3-addtask.png)

4. 텍스트 필드에 `bolt`를 입력하고 `Get it free`를 클릭합니다.  
![무료 다운로드](/media-draft/3-getitfree.png)

5. WhiteSource Bolt 마켓플레이스 페이지로 이동됩니다. `Get it free`를 클릭합니다.  
![White Source Bolt 무료 다운로드](/media-draft/3-getwhitesourceboltfree.png)

6. VSTS 조직을 선택하고 `Install`을 클릭합니다.  
![설치](/media-draft/3-install.png)

7. <https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate>의 지침에 따라 WhiteSource Bolt를 활성화합니다.

8. DevOps 프로젝트가 로드되어 있는 Azure Portal로 돌아가서 빌드 파이프라인 링크를 클릭합니다.  
![빌드 파이프라인 링크](/media-draft/3-buildpipelinelink.png)

9. 빌드를 선택하고 `Edit`를 클릭합니다.  
![빌드 편집](/media-draft/3-editbuild.png)

10. `+` 에이전트 작업 1에 작업 추가를 클릭하고, 검색 필드에 `bolt`를 입력하고, `Add`를 클릭합니다.  
![Bolt 추가](/media-draft/3-addbolt.png)

11. 작업 목록의 맨 아래에 WhiteSource Bolt 작업이 추가됩니다. 맨 위로 끌어다 놓습니다.  
![맨 위에 Bolt](/media-draft/3-boltattop.png)

12. `Save & queue`를 클릭하고 `Save & queue`를 선택합니다.  
![저장 및 큐에 넣기](/media-draft/3-saveandqueue.png)

13. `Save & queue`를 클릭합니다.  
![저장 및 큐에 넣기 대화 상자](/media-draft/3-saveandqueuedialog.png)

수정된 빌드 파이프라인을 저장하고 빌드를 큐에 넣습니다. 빌드가 완료된 후 `WhiteSource Bolt Build Report` 빌드를 살펴보면 WhiteSource Bolt가 보안 취약점을 찾기 위해 소스 코드를 검사한 것을 알 수 있습니다.

![빌드 보고서](/media-draft/3-buildreport.png)

## <a name="customize-the-release-pipeline"></a>릴리스 파이프라인 사용자 지정

빌드와 마찬가지로, 릴리스 파이프라인은 작업 실행 기이며 동일한 방식으로 사용자 지정할 수 있습니다. 이 모듈에서는 릴리스 끝부분에 웹 성능 테스트를 추가할 것입니다. 이렇게 하면 앱이 Kubernetes 클러스터에 성공적으로 배포되어 실행되는지 확인할 수 있습니다.

1. Azure Portal에서 DevOps 프로젝트를 찾아 릴리스 파이프라인 링크를 클릭합니다.  
![릴리스 링크](/media-draft/3-releaselink.png)

2. 릴리스 파이프라인 페이지로 이동됩니다. 릴리스 파이프라인을 클릭하고 `Edit`를 클릭합니다.  
![릴리스 파이프라인 편집](/media-draft/3-editreleasepipeline.png)

3. 릴리스 `Dev` 단계에서 작업을 클릭합니다.  
![릴리스 단계](/media-draft/3-releasestage.png)

4. `+` 1단계에 작업 추가를 클릭하고, 검색 필드에 `web test`를 입력하고, 클라우드 기반 웹 성능 테스트 작업에 대한 `Add`를 클릭합니다.  
![웹 테스트 추가](/media-draft/3-addwebtest.png)

5. 빠른 웹 성능 테스트 작업을 클릭하고, 웹 사이트 URL의 앱 url(url을 찾으려면 Azure Portal DevOps 프로젝트 페이지를 이동한 후 오른쪽에서 샘플 앱 외부 엔드포인트를 마우스 오른쪽 단추로 클릭하고 링크 복사) 및 TestName에 대한 url을 추가하고, `Ping Test`를 입력합니다.  
![URL 복사](/media-draft/3-copyurl.png)  
![웹 테스트 작업 편집](/media-draft/3-editwebtesttask.png)

6. `Save`를 클릭합니다.  
![릴리스 저장](/media-draft/3-saverelease.png)

이제 릴리스를 실행하면 새 helm 패키지가 배포된 후 웹 테스트가 실행되고 성공적으로 앱 url에 도달합니다.

![웹 테스트](/media-draft/3-webtest.png)


## <a name="summary"></a>요약

이 모듈에서는 빌드 및 릴리스 파이프라인을 사용자 지정하는 방법을 알아보았습니다. 마켓플레이스에서 작업을 설치하고 사용하는 방법도 알아보았습니다.