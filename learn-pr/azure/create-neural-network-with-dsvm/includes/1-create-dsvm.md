### <a name="create-an-ubuntu-data-science-vm"></a>Ubuntu Data Science VM 만들기

Linux용 Data Science Virtual Machine은 데이터 과학을 간편하게 시작하도록 하는 가상 머신 이미지입니다. 빠르게 가동하고 실행하기 위해 이미 여러 도구가 빌드되고, 설치되고, 구성되어 있습니다. [Jupyter](http://jupyter.org/), 일부 샘플 Jupyter 노트 및 [TensorFlow](https://www.tensorflow.org/)와 마찬가지로 NVIDIA GPU 드라이버, [NVIDIA CUDA](https://developer.nvidia.com/cuda-downloads) 및 [NVIDIA cuDNN](https://developer.nvidia.com/cudnn)(CUDA Deep Neural Network) 라이브러리도 포함되어 있습니다. 미리 설치된 모든 프레임워크는 GPU를 지원하지만 CPU에서도 작동합니다. 이 단원은 Azure에서 Linux용 DSVM(Data Science Virtual Machine) 인스턴스를 만듭니다.

1. 브라우저에서 [Azure Portal](https://portal.azure.com/?azure-portal=true)을 엽니다.

1. 포털 왼쪽에 있는 메뉴에서 **리소스 만들기**를 클릭한 다음, 검색 상자에 "data science"(따옴표 제외)를 입력합니다. 결과 목록에서 **Linux용 Data Science Virtual Machine(Ubuntu)** 을 선택합니다.

    ![Ubuntu Data Science VM 찾기](../media-draft/1-new-data-science-vm.png)

1. 잠시 VM에 포함된 도구 목록을 검토하세요. 그런 다음, 블레이드 아래쪽에서 **만들기**를 클릭합니다.

1. 아래 표시된 것처럼 "기본 사항" 블레이드를 채웁니다. 대문자, 소문자, 숫자 및 특수 문자를 혼합하여 12자 이상의 암호를 입력합니다. *모듈에서 나중에 필요하므로 입력한 사용자 이름과 암호를 기억해야 합니다.*

    ![VM에 대한 기본 정보 입력](../media-draft/1-create-data-science-vm-1.png)

1. "크기 선택" 블레이드에서 Data Science VM을 저비용으로 실험해 볼 방법을 제공하는 **DS1_V2 표준**을 선택합니다. 그런 다음, 블레이드 하단에서 **선택** 단추를 클릭합니다.

    ![VM 크기 선택](../media-draft/1-create-data-science-vm-2.png)

1. 에 **설정을** 블레이드에서 기본값을 적용 하 고 클릭 합니다 **확인** 단추입니다.

1. **만들기** 블레이드에서 잠시 VM에 대해 선택한 옵션을 검토하고 **만들기**를 클릭하여 VM 만들기 프로세스를 시작합니다.

    ![VM 만들기](../media-draft/1-create-data-science-vm-4.png)

1. 포털 왼쪽에 있는 메뉴에서 **리소스 그룹**을 클릭합니다. 그런 다음, **data-science-rg** 리소스 그룹을 클릭합니다.

    ![리소스 그룹 열기](../media-draft/1-open-resource-group.png)

  
1. "배포 중" 상태가 DSVM 및 지원 Azure 리소스가 생성되었음을 나타내는 "성공"으로 변경될 때까지 기다립니다. 배포는 일반적으로 5분 이내에 완료됩니다. 블레이드 위쪽에 있는 **새로 고침**을 주기적으로 클릭하여 배포 상태를 새로 고칩니다.

    ![배포 상태 모니터링](../media-draft/1-deployment-succeeded.png)
