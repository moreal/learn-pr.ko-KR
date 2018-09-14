Azure DevOps 프로젝트를 만들면 모든 사용자에 게 문의 가장 먼저 어떻게 하면 교체 샘플 앱은 사용자 고유의 앱을 사용 하 여은? 매우 간단 하 고 작업을 수행 하는 두 가지 방법으로이 단위로 배웁니다.

1. 실제 코드를 사용 하 여 VSTS git 리포지토리에 코드를 대체합니다.

2. 빌드 파이프라인을 실제 코드를 보유 하는 외부 git 리포지토리를 가리키는

## <a name="replacing-code-in-vsts-git-repository"></a>VSTS git 리포지토리에 코드를 대체합니다.

한 가지 간단한 방법은 VSTS를 다시 누르고 업로드를 고유한 코드로 대체 하는 모든 하드 드라이브에 VSTS에서 git 리포지토리를 복제 하는 것입니다. 코드 빌드 및 CI/CD 파이프라인을 통해 배포할 이제 됩니다.

이 장치에 대 한 다운로드 하 고 하드 드라이브에 node.js 앱 소스 코드를 저장 하 여 시작 합니다.

1. 소스 코드를 다운로드 합니다. <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip>

2. 하드 드라이브에서 MicrosoftLearnDevOps.zip의 콘텐츠를 추출 합니다. 이 예제에 대 한 `C:\users\abel\Downloads\MicrosoftLearnDevOps` 사용한  
![압축 푼된 디렉터리](../media-drafts/2-unzippedfolder.png)

다음으로, 하드 드라이브에 리포지토리를 복제 하 여 실제 node.js 앱을 사용 하 여 샘플 앱을 대체 해야 합니다. 이 단위는 이미 컴퓨터에 설치 된 git가 가정 합니다.

1. Azure portal에서 Azure DevOps Project로 이동 하 고 코드 리포지토리 링크를 클릭 합니다.  
![](../media-drafts/2-browsetorepolink.png)

2. 복제본에서 클릭 하 고 오른쪽 상단에 있는 git 리포지토리에 대 한 url을 복사 합니다.  
![리포지토리를 복제](../media-drafts/2-clonerepo2.png) 리포지토리 url을 클립보드에 복사 하는

3. 하드 드라이브에 리포지토리 복제  
![Git 복제](../media-drafts/2-gitclone.png)  
이 예제의 리포지토리 C:\Users\abel\Source\TripleCrown\DevOps에 복제

4. 모든 항목을 제외 하 고 로컬 리포지토리에서 삭제는 `.git` 디렉터리  
![모든 리포지토리 삭제](..//media-drafts/2-deleterepoofeverything.png)

5. 다운로드 한 node.js 앱에 대 한 소스 코드 리포지토리 폴더에 복사  
![대체 코드](../media-drafts/2-replacedeverything.png)

6. 입력 하 여 모든 변경 내용을 로컬 리포지토리에 추가 `git add *` 명령줄에서  
![모든 Git 추가](../media-drafts/2-gitaddall.png)

7. 입력 하 여 로컬 리포지토리에 변경 내용 커밋 `git commit -m "replace sample app with real code"`  
![Git 커밋](../media-drafts/2-gitcommit.png)

8. 사용 하 여 VSTS에서 git 리포지토리를 다시 변경 내용 푸시 `git push`  
![Git 푸시](../media-drafts/2-gitpush.png)

9. VSTS에 변경 내용을 다시 푸시 하면,이 보내야 하는 빌드를 통해 실제 앱 코드  
![빌드 시작](../media-drafts/2-buildkickedoff2.png)
![빌드 실행](../media-drafts/2-buildrunning2.png) 및 azure까지 릴리스 파이프라인  
 ![실행 중인 릴리스](../media-drafts/2-releaserunning2.png)

 배포가 완료 되 면 실제 앱이 Azure portal로 다시 이동 하 여 배포 된 확인할 수 있습니다.

 1. Azure DevOps 프로젝트를 Azure portal로 이동 하 고 오른쪽에 있는 배포 된 앱 클릭 이동  
 ![샘플 앱 링크를 시작 합니다.](../media-drafts/2-launchapp.png)

 2. 그러면 브라우저에서 실행 중인 앱  
 ![실행 중인 앱](../media-drafts/2-apprunning.png)

## <a name="using-external-git-repo"></a>외부 git 리포지토리 사용

실제 앱 코드를 사용 하 여 샘플 응용 프로그램 교체 하는 다른 방법은 앱 코드를 포함 하는 외부 git 리포지토리에 빌드 파이프라인을 가리켜서 것입니다. 예를 들어 github 리포지토리에 실제 응용 프로그램 코드를 업로드 합니다.

실제 코드를 github에 업로드 한 후 빌드 파이프라인이 github 리포지토리를 가리키도록 다음을 수행

1. Azure portal에서 Azure DevOps project로 이동 하 고 빌드 링크 클릭  
![링크 작성](../media-drafts/2-buildlink.png)

2. 이렇게 하면 빌드 파이프라인을 빌드 파이프라인을 클릭 한 다음 `Edit`  
![편집 빌드 파이프라인을 클릭 합니다.](../media-drafts/2-editbuildpipelinelink.png)

3. 이렇게 하면 빌드 편집기에서를 클릭 합니다. `Get sources`  
![원본 작업 가져오기를 클릭 합니다.](../media-drafts/2-clickgetsourcetask.png)

4. 이렇게 하면 선택 된 원본 페이지. 어떻게 사용할 수 없습니다만 VSTS Git 하지만 또한 GitHub, GitHub Enterprise, Subversion, Bitbucket 클라우드 및 모든 외부 Git 기반 리포지토리 빌드 파이프라인에 대 한 알 수 있습니다. 이 연습에서는 GitHub를 선택 합니다.  
![GitHub를 선택 합니다.](../media-drafts/2-selectgithub2.png)

5. 이 GitHub 연결 페이지로 이동 합니다. GitHub 계정과 연결할 OAuth 또는 개인용 액세스 토큰 사용

6. 실제 응용 프로그램 코드를 보유 하는 github 리포지토리를 선택 하 고 클릭 `Save & queue`  
![저장 및 큐](../media-drafts/2-saveandqueue2.png)

7. 클릭 된 `Save & queue` 단추  
![저장 및 큐 단추](../media-drafts/2-saveandqueuebutton.png)

8. 이 작업을 저장 하 고 빌드를 실제 앱 보내기 시작 빌드를 통해 호스트에서 GitHub 코드 및 릴리스 파이프라인에 Azure  
![빌드 실행](../media-drafts/2-buildpipelinerunning.png)

## <a name="summary"></a>요약

이 단위에 두 가지 방법으로 실제 앱 코드를 사용 하 여 DevOps 프로젝트의 샘플 코드를 바꾸려면 알아보았습니다. VSTS git 리포지토리에 코드를 대체 하거나 앱 코드를 포함 하는 다른 외부 리포지토리를 사용 하 여 빌드 파이프라인을 연결 하 여 수행할 수 있습니다.

다음 빌드 사용자 지정 파이프라인을 릴리스 하는 방법을 알아봅니다.