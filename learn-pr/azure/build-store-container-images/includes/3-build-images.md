Azure Container Registry 빌드가 있으면 로컬 Docker 도구를 사용하지 않고도 클라우드에 컨테이너 이미지를 빌드할 수 있습니다. Container Registry 빌드를 사용하면 소스 코드 커밋에서 DevOps 프로세스를 자동화된 빌드와 통합할 수도 있습니다.

이 단원에서는 Azure Container Registry 빌드를 사용하여 컨테이너 이미지 만들기를 자동화합니다.

## <a name="create-a-container-image-with-build"></a>빌드를 사용하여 컨테이너 이미지 만들기

Azure Container Registry 빌드를 사용하는 경우 표준 Dockerfile이 빌드 지침을 제공하는 데 사용됩니다. 다단계 빌드를 포함하여 현재 환경에서 사용되는 모든 Dockerfile은 Azure Container Registry 빌드에서 작동합니다.

`Dockerfile`이라는 파일을 만들고 텍스트 편집기를 사용하여 엽니다.

```bash
code Dockerfile
```

다음 콘텐츠에서 복사하고 파일을 저장한 후 텍스트 편집기를 종료합니다. 이 Dockerfile은 `node:9-alpine` 이미지에 Node.js 응용 프로그램을 추가하고 포트 80에서 해당 응용 프로그램을 제공하도록 컨테이너를 구성합니다.

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

다음 명령을 실행하여 Dockerfile에서 컨테이너 이미지를 빌드합니다.

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

이 작업을 실행하면 빌드되어 Container Registry로 푸시되는 이미지가 표시됩니다.

## <a name="verify-the-image"></a>이미지 확인

빌드 작업이 완료되면 다음 명령을 실행하여 이미지가 만들어졌고 레지스트리에 저장되었는지 확인합니다.

```azurecli
az acr repository list --name <acrName> --output table
```

출력은 다음과 비슷해야 합니다.

```console
Result
-------------
helloacrbuild
```

이제 `helloacrbuild` 이미지를 사용할 준비가 되었습니다.

## <a name="summary"></a>요약

이 단원에서는 Azure Container Registry 빌드를 사용하여 컨테이너 이미지 만들기를 자동화했습니다. 그런 다음, 해당 이미지를 Azure Container Registry에 저장했습니다. 다음 단원에서는 새 컨테이너 이미지 인스턴스를 Azure Container Instances에 배포합니다.