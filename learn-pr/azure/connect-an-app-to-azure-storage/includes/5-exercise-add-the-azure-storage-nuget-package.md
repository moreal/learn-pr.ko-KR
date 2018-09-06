이 연습에서는 Azure Storage 클라이언트 라이브러리를 .NET Core 콘솔 응용 프로그램에 통합합니다.

## <a name="add-the-azure-storage-nuget-package"></a>Azure Storage NuGet 패키지 추가

1. 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리 …** 를 선택합니다.
  ![Manage NuGet packages]/' (..\media-draft\1-manage-nuget-packages.png)

1. 현재 설치된 NuGet 패키지를 보여 주는 페이지가 표시됩니다. **찾아보기** 옵션을 클릭하고 검색 필드에 **저장소**를 입력합니다. 검색 결과에 **WindowsAzure.Storage** 패키지가 표시됩니다.

1. **WindowsAzure.Storage** 패키지를 선택합니다. 오른쪽의 창에는 기본적으로 최신 버전이 표시됩니다(이 문서가 작성되는 시점의 최신 버전은 9.3.0임). **설치** 단추를 클릭하여 패키지에 대한 참조를 프로젝트에 추가합니다.
  ![패키지 찾기](..\media-draft\3-find-package.png)

1. 패키지가 복원될 때 Visual Studio에서 **출력** 창이 열립니다. 네트워크 속도에 따라 몇 초 정도 시간이 걸립니다. 프로젝트에 추가될 패키지를 보여 주는 **변경 내용 미리 보기** 대화 상자가 표시됩니다. **확인**을 클릭합니다.
  ![변경 내용 미리 보기](..\media-draft\4-preview-changes.png)

1. 라이선스에 동의할 것인지 묻는 또 다른 대화 상자가 표시됩니다. **동의함**을 클릭합니다.
  ![라이선스](..\media-draft\5-licence.png)

몇 초 후 일부 추가 작업이 Visual Studio의 출력 창에 표시되고 패키지는 프로젝트에 추가되었습니다.
프로젝트에서 **종속성** 옵션을 확장한 후 **NuGet** 옵션을 확장하여 패키지가 성공적으로 추가된 것을 확인할 수 있습니다. **WindowsAzure.Storage**에 대한 참조가 나열됩니다.

![패키지 확인](..\media-draft\6-package-check.png)

