Azure DevOps 프로젝트를 만든 후에 모든 사람들이 가장 먼저 문의한 것은 샘플 앱을 자신의 앱으로 바꾸는 방법이었습니다. 이 방법은 매우 간단하며 이 단원에서는 두 가지 방법을 배우게 됩니다.

1. VSTS Git 리포지토리의 코드를 실제 코드로 바꾸기

2. 빌드 파이프라인에서 실제 코드가 있는 외부 Git 리포지토리 가리키기

## <a name="replacing-code-in-vsts-git-repository"></a>VSTS Git 리포지토리의 코드 바꾸기

한 가지 간단한 방법은 VSTS에서 Git 리포지토리를 하드 드라이브에 복제하고, 모든 코드를 사용자 고유의 코드로 바꾸고, VSTS로 다시 업로드하는 것입니다. 잘 보세요! 이제 코드가 CI/CD 파이프라인을 통해 빌드 및 배포됩니다.

이 단원에서는 Node.js 앱에 대한 소스 코드를 다운로드하여 하드 드라이브에 저장하는 것으로 시작하겠습니다.

1. <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip>에서 소스 코드 다운로드

2. 하드 드라이브의 어딘가에 있는 MicrosoftLearnDevOps.zip의 콘텐츠를 추출합니다. 이 예에서는 `C:\users\abel\Downloads\MicrosoftLearnDevOps`가 사용되었습니다.  
![압축을 푼 디렉터리](/media-draft/2-unzippedfolder.png)

그런 다음, 리포지토리를 하드 드라이브에 복제하고, 샘플 앱을 실제 Node.js 앱으로 바꿔야 합니다. 이 단원에서는 git가 이미 컴퓨터에 설치되어 있다고 가정합니다.

1. Azure Portal에서 Azure DevOps 프로젝트로 이동하여 코드 리포지토리 링크를 클릭합니다.  
![](/media-draft/2-browsetorepolink.png)

2. [복제]를 클릭하고, 오른쪽 위에 있는 Git 리포지토리에 대한 URL을 복사합니다.  
![복제 URL 복사](/media-draft/2-copycloneurl.png)  
리포지토리 URL이 클립보드에 복사됩니다.

3. 하드 드라이브에 리포지토리 복제  
![Git 복제](/media-draft/2-gitclone.png)  
이 예에서 리포지토리는 C:\Users\abel\Source\TripleCrown\DevOps에 복제되었습니다.

4. 로컬 리포지토리에서 `.git` 디렉터리를 제외한 모든 항목 삭제  
![모든 리포지토리 삭제](/media-draft/2-deleterepoofeverything.png)

5. 다운로드한 Node.js 앱에 대한 소스 코드를 리포지토리 폴더에 복사합니다.  
![대체된 코드](/media-draft/2-replacedeverything.png)

6. 명령줄에서 `git add *`를 입력하여 모든 변경 내용을 로컬 리포지토리에 추가합니다  
![Git에 모든 변경 내용 추가](/media-draft/2-gitaddall.png)

7. `git commit -m "replace sample app with real code"`를 입력하여 변경 내용을 로컬 리포지토리에 커밋합니다.  
![Git 커밋](/media-draft/2-gitcommit.png)

8. `git push`를 사용하여 변경 내용을 VSTS의 Git 리포지토리로 푸시합니다.  
![Git 푸시](/media-draft/2-gitpush.png)

9. 변경 내용이 VSTS로 다시 푸시되면 빌드를 통해 실제 앱 코드를 보냅니다.  
![빌드 시작](/media-draft/2-buildkickedoff.png)  
![실행 중인 빌드](/media-draft/2-buildinaction.png) 및 Azure로의 릴리스 파이프라인  
 ![릴리스 실행](/media-draft/2-releaserunning.png)

 배포가 완료되면 Azure Portal로 돌아가서 실제 앱이 배포되었는지 확인할 수 있습니다

 1. Azure Portal로 이동하고, Azure DevOps 프로젝트를 찾고, 오른쪽에 있는 배포된 앱을 클릭합니다.  
 ![샘플 앱 시작 링크](/media-draft/2-launchapp.png)

 2. 브라우저에서 앱 실행을 시작합니다.  
 ![앱 실행](/media-draft/2-apprunning.png)

## <a name="using-external-git-repo"></a>외부 Git 리포지토리 사용

샘플 앱을 실제 앱 코드로 바꾸는 또 다른 방법은 빌드 파이프라인에서 앱 코드가 있는 외부 Git 리포지토리를 가리키는 것입니다. 이 예의 경우 실제 앱 코드를 GitHub 리포지토리에 업로드합니다.

실제 코드가 GitHub에 업로드되면 다음을 수행하여 빌드 파이프라인에서 이 GitHub 리포지토리를 가리키도록 지정합니다.

1. Azure Portal에서 Azure DevOps 프로젝트를 찾아 빌드 링크를 클릭합니다.  
![빌드 링크](/media-draft/2-buildlink.png)

2. 빌드 파이프라인으로 이동하고, 빌드 파이프라인, `Edit`을 차례로 클릭합니다.  
![빌드 편집 클릭](/media-draft/2-clickeditbuildlink.png)

3. 빌드 편집기로 이동하고, `Get sources`를 클릭합니다.  
![원본 가져오기 클릭](/media-draft/2-clickgetsource.png)

4. [원본 선택] 페이지로 이동합니다. VSTS Git뿐만 아니라 GitHub, GitHub Enterprise, Subversion, Bitbucket Cloud 및 빌드 파이프라인에 대한 외부 Git 기반 리포지토리도 사용할 수 있습니다. 이 연습에서는 GitHub를 선택합니다.  
![GitHub 선택](/media-draft/2-selectgithub.png)

5. [GitHub 연결] 페이지로 이동합니다. OAuth 또는 개인 액세스 토큰을 사용하여 GitHub 계정에 연결합니다.

6. 실제 앱 코드가 있는 GitHub 리포지토리를 선택하고 `Save & queue`를 클릭합니다.  
![저장 및 큐에 넣기](/media-draft/2-saveandqueue.png)

7. `Save & queue` 단추를 클릭합니다.  
![](/media-draft/2-saveandqueuedialog.png)

8. 이 작업은 빌드를 저장하고 시작하여 빌드 및 릴리스 파이프라인을 통해 GitHub에서 호스팅되는 실제 앱 코드를 Azure로 보냅니다.  
![빌드 실행](/media-draft/2-buildrunning.png)

## <a name="summary"></a>요약

이 단원에서는 DevOps 프로젝트의 샘플 코드를 실제 앱 코드로 바꾸는 두 가지 방법을 알아보았습니다. 이 작업은 VSTS Git 리포지토리의 코드를 바꾸거나 빌드 파이프라인을 앱 코드가 있는 다른 외부 리포지토리와 연결하여 수행할 수 있습니다.

다음으로, 빌드 및 릴리스 파이프라인을 사용자 지정하는 방법을 알아봅니다.