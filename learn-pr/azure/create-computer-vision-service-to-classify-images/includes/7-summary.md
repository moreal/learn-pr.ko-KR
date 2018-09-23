
Computer Vision API는 이미지를 처리하기 위한 강력한 도구입니다. 자체 빌드 대신 이 서비스를 사용하면 개발 및 유지 관리 비용을 크게 절감할 수 있습니다. 비즈니스 논리 작성에 집중하여 비즈니스와 관련된 의사 결정을 내리고 Computer Vision API에서 이미지의 풍부한 정보를 추출하여 시각적 데이터를 분류하고 처리합니다.

이 모듈에서는 이미지, 추출된 텍스트 및 생성된 미리 보기를 분석했습니다. Computer Vision API를 호출하기 위해 Azure 구독에서 인지 서비스 계정을 만들었습니다. 이 계정은 호출을 수행하는 데 필요한 액세스 키를 제공합니다.

다음 단계로 사용자 고유의 이미지로 동일한 호출을 하는 데 약간의 시간이 소요됩니다. 그런 다음, 각 호출에 대한 매개 변수를 조정하여 결과에 미치는 효과를 확인합니다. 더 나아가서 `describe` 및 `tag`와 같은 API에서 다른 작업을 시도할 수 있습니다.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="further-reading"></a>추가 참고 자료

- [Azure CLI 개요](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Azure CLI 명령 참조](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
- [Computer Vision API 참조 설명서](https://westus2.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb/console)