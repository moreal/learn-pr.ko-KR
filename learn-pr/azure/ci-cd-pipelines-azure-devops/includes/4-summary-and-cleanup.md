Azure DevOps Projects를 사용하여 사용자 지정 응용 프로그램에 대한 CI/CD 파이프라인을 성공적으로 만들었습니다. 

## <a name="clean-up-resources"></a>리소스 정리

CI/CD 파이프라인의 작업이 완료되면 자습서 중에 만들어진 모든 리소스를 삭제할 수 있습니다.

1. Azure Portal에서 `Resource Groups`로 이동하고 `VstsResourceGroup-LearnCluster-xxxx`를 클릭합니다. 여기서 xxx는 문자와 숫자의 무작위 그룹입니다.  
![LearnClusterRG](/media-draft/4-learnclusterrg.png)

2. `Learn`이라는 DevOps 프로젝트를 클릭합니다.  
![자세한 정보 링크](/media-draft/4-learnlink.png)

3. `Delete`을 클릭합니다.  
![삭제](/media-draft/4-deleteproj.png)

4. `Yes`을 클릭합니다.  
![예](/media-draft/4-yes.png)

Azure에서 만들어진 모든 리소스가 삭제됩니다.

## <a name="summary"></a>요약

이 자습서에서는 다음 방법에 대해 알아보았습니다.
> [!div class="checklist"]
> * Azure DevOps 프로젝트 만들기
> * Azure DevOps 프로젝트의 샘플 앱을 고유한 앱으로 바꿉니다.
> * 빌드 및 릴리스 파이프라인 사용자 지정
