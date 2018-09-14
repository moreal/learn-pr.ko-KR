Azure DevOps projects를 사용 하 여 사용자 지정 응용 프로그램에 대 한 CI/CD 파이프라인을 만들었습니다. 

## <a name="clean-up-resources"></a>리소스 정리

완료 되 면이 CI/CD 파이프라인을 사용 하는 자습서 중에 만든 모든 리소스를 삭제할 수 있습니다.

1. Azure portal에서 `Resource Groups` 클릭 하 고 `VstsResourceGroup-LearnCluster-xxxx` 여기서 xxx는 문자와 숫자의 임의 그룹  
![LearnClusterRG](../media-drafts/4-learnclusterrg.png)

2. DevOps 프로젝트 클릭 `Learn`  
![링크](../media-drafts/4-learnlink.png)

3. `Delete`을 클릭합니다.  
![삭제](../media-drafts/4-deleteproj.png)

4. `Yes`을 클릭합니다.  
![예](../media-drafts/4-yes.png)

Azure에서 생성 된 모든 리소스를 삭제 됩니다.

## <a name="summary"></a>요약

이 자습서에서는 다음 방법에 대해 알아보았습니다.
> [!div class="checklist"]
> * Azure DevOps 프로젝트 만들기
> * Azure DevOps 프로젝트에 샘플 앱을을 직접으로 바꿉니다.
> * 빌드 및 릴리스 파이프라인 사용자 지정
