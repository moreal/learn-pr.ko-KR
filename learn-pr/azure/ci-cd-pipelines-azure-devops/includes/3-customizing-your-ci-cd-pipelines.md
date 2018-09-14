Azure DevOps 프로젝트를 사용 하 여 첫 실행 경험 중 빌드를 만들고 릴리스 파이프라인을 선택 하는 기술에 대 한 것이 좋습니다. 이 모듈에 대 한 적합 한 Kubernetes 클러스터에서 호스트 되는 컨테이너에서 실행 되는 node.js 앱에 대 한 빌드 및 릴리스 파이프라인을 만들었습니다. 

해야 하는 경우도 많습니다 프로젝트에 대 한 특정 작업을 수행 하려면 빌드 및 릴리스 파이프라인 사용자 지정 합니다. VSTS의 빌드 및 릴리스 파이프라인은 100%를 사용자 지정할 수 있습니다. 필요한 모든 사항을 수행 작업을 수행 하도록 하는 파이프라인을 만들 수 있습니다.

이 단위 빌드 사용자 지정 파이프라인을 릴리스 하는 방법에 알아봅니다.

## <a name="customize-the-build-pipeline"></a>빌드 파이프라인 사용자 지정

VSTS에서 빌드 엔진은 방금 한 작업 실행 기 후 다른 하나의 태스크를 수행 합니다. 빌드를 사용자 지정 하려면 방금 추가 하거나 제거 작업 한 작업에 대 한 올바른 매개 변수를 채웁니다.

VSTS는 기본적으로 사용할 수 있는 약 100 개의 작업이 포함 되어 있습니다. 기본적으로 존재 하지 않는 작업을 수행 하는 경우 확인 marketplace 700 개 빌드 및 릴리스 작업을 다운로드 하 여 사용할 준비가 되었습니다. 한 부분입니다. 사용자 고유의 사용자 지정 태스크를 작성할 수가 있습니다.

이 장치에 대 한 marketplace 작업의 코드 보안 검사를 수행 하도록 WhiteSource Bolt를 설치 하 여 빌드 파이프라인을 사용자 지정할가 있습니다.

1. Azure portal에서 Azure DevOps Project로 이동 하 고 빌드 정의 링크를 클릭  
![링크 작성](../media-drafts/3-buildlink.png)

2. 이 빌드 파이프라인 페이지로 이동 합니다. 빌드에 클릭 하 고 선택 `Edit`  
![빌드 편집](../media-drafts/3-editbuild2.png)

3. 이렇게 하면 빌드 정의 됩니다. 클릭 된 `+` 에이전트 작업 1로 작업을 추가 하려면  
![태스크 추가](../media-drafts/3-addtask2.png)

4. 텍스트 필드에 입력 `bolt` 클릭 `Get it free`  
![흰색 원본 Bolt 가져오기](../media-drafts/3-getwhitesourcebolt.png)

5. 이렇게 WhiteSource Bolt Marketplace 페이지로 이동 합니다. `Get it free`을 클릭합니다.  
![WhiteSource Bolt 무료 가져오기](../media-drafts/3-getwhitesourceboltfree2.png)

6. Azure DevOps 조직을 선택 하 고 클릭 한 다음 `Install`  
![설치](../media-drafts/3-installwsb.png)

7. 다음 지침을 수행 하 여 WhiteSource Bolt를 활성화 합니다. <https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate>

8. DevOps 프로젝트 로드 하 고 빌드 파이프라인 링크 클릭을 사용 하 여 Azure portal로 다시 이동  
![파이프라인 링크 작성](../media-drafts/3-buildpipelinelink.png)

9. 빌드를 선택 하 고 클릭 `Edit`  
![빌드 편집](../media-drafts/3-editbuild2.png)

10. 클릭 합니다 `+` 에이전트 작업 1에 태스크를 추가, 입력 `bolt` 검색 필드 및 클릭 `Add`  
![Bolt를 추가 합니다.](../media-drafts/3-addwsbolt.png)

11. WhiteSource Bolt 태스크 작업 목록 맨 아래에 추가, 맨 위에 놓습니다.  
![Bolt 맨 위로 이동](../media-drafts/3-moveboltototopoftasklist.png)

12. 클릭 `Save & queue` 선택 `Save & queue`  
![저장 및 큐](../media-drafts/3-saveandqueue2.png)

13. `Save & queue`을 클릭합니다.  
![저장 및 큐 단추](../media-drafts/3-saveandqueuebutton.png)

이 수정 된 빌드 파이프라인을 저장 하 고 빌드를 큐. 빌드가 완료 되 면 빌드를 살펴보면 `WhiteSource Bolt Build Report`, 보안 취약점을 찾고 WhiteSource Bolt에서 검색 한 소스 코드를 볼 수 있습니다.

![흰색 원본 보고서](../media-drafts/3-whitesourcereport.png)

## <a name="customize-the-release-pipeline"></a>릴리스 파이프라인 사용자 지정

빌드 같은 릴리스 파이프라인 작업 실행 기 이며 동일한 방식으로 사용자 지정할 수 있습니다. 이 장치에 대 한 릴리스 후에 웹 성능 테스트를 추가 합니다. 이 앱은 배포를 확인 하 고 Kubernetes 클러스터에서 성공적으로 실행 됩니다.

1. Azure Portal에서 DevOps 프로젝트를 찾아 릴리스 파이프라인에 대 한 링크를 클릭  
![릴리스 링크](../media-drafts/3-releaselink.png)

2. 이 릴리스 파이프라인 페이지로 이동 합니다. 릴리스 파이프라인을 클릭 하 고 클릭 `Edit`  
![릴리스 편집](../media-drafts/3-editreleasebutton.png)

3. 릴리스 태스크에 대해 클릭 `Dev` 단계  
![릴리스 스테이지](../media-drafts/3-releasestage2.png)

4. 클릭 합니다 `+` 형식 단계 1 백 그라운드에 태스크를 추가 `web test` 검색 필드 및 클릭 `Add` 클라우드 기반 웹 성능 테스트 작업에 대 한  
![웹 테스트를 추가 합니다.](../media-drafts/3-addwebtest2.png)

5. 클릭 하 고 웹 사이트 URL (url을 확인 하 고, 오른쪽에 있는 Azure portal DevOps 프로젝트 페이지를 이동 하 고, 샘플 앱 외부 끝점 및 복사 링크를 마우스 오른쪽 단추로 클릭)에 앱 url 추가 기술 전달자에 대 한 하 여 빠른 웹 성능 테스트 작업 편집 tName, 입력 `Ping Test` 클릭 `Save`  
![URL 복사](../media-drafts/3-copyurl.png)  
![웹 테스트를 저장 합니다.](../media-drafts/3-savewebtest.png)

이제 새 helm 패키지를 배포한 후 릴리스를 실행할 때 웹 테스트 앱 url을 성공적으로 도달 실행 됩니다.

![웹 테스트 실행](../media-drafts/3-webtestrun.png)

## <a name="summary"></a>요약

이 단위 빌드 사용자 지정 파이프라인을 릴리스 하는 방법을 알아보았습니다. 설치 하 고 Marketplace에서 작업을 사용 하는 방법을 알아보았습니다.