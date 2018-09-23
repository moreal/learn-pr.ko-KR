다른 컴퓨터와 마찬가지로, Azure에서 가상 머신은 운영 체제, 응용 프로그램 및 데이터를 저장하는 장소로 디스크를 사용합니다. 이러한 디스크를 VHD(가상 하드 디스크)라고 합니다.

법률 회사에서 사용하는 판례 기록 데이터베이스를 호스트하는 VM(가상 머신)을 Azure에서 만들었다고 가정해봅시다. SQL Server의 성능과 복원력을 높이려면 잘 설계된 디스크 구성이 필수입니다.

이 모듈에서는 디스크에 적절한 구성 값을 선택하는 방법 및 해당 디스크를 VM에 연결하는 방법을 알아보겠습니다.

## <a name="how-disks-are-used-by-vms"></a>VM에서 디스크를 사용하는 방법

VM은 다음과 같은 세 가지 용도로 디스크를 사용합니다.

- **운영 체제 저장소**. 모든 VM은 운영 체제를 저장하는 디스크를 하나 갖고 있습니다. 이 드라이브는 SATA 드라이브로 등록되고 Windows에서 C: 드라이브로 레이블이 지정되며 Unix와 비슷한 운영 체제에서는 "/"에 탑재됩니다. 최대 용량은 2048GB이고, 콘텐츠는 VM을 만들 때 사용한 VM 이미지에서 가져옵니다.
- **임시 저장소**. 모든 VM은 페이지 및 스왑 파일에 사용되는 임시 VHD를 포함하고 있습니다. 유지 관리 이벤트 또는 다시 배포하는 동안 이 드라이브의 데이터가 손실될 수 있습니다. 드라이브는 기본적으로 Windows VM에서 D:로 레이블이 지정됩니다. 손실되면 안 되는 중요한 데이터를 저장하는 용도로 이 드라이브를 사용하지 마세요.
- **데이터 저장소**. VM에 연결되는 그 외의 모든 디스크는 데이터 디스크입니다. 데이터 디스크는 파일, 데이터베이스 및 재부팅 간에 유지해야 하는 모든 데이터를 저장하는 데 사용됩니다. 일부 VM 이미지는 기본적으로 데이터 디스크를 포함하고 있습니다. 또한 VM의 크기에 따라 지정된 최대 개수까지 추가 데이터 디스크를 추가할 수 있습니다. 각 데이터 디스크는 SCSI 드라이브로 등록되고 최대 용량은 4095GB입니다. 드라이브 문자를 선택하거나 데이터 드라이브의 탑재 지점을 선택할 수 있습니다.

## <a name="storing-vhd-files"></a>VHD 파일 저장

Azure에서 VHD는 Azure 저장소 계정에 **페이지 Blob**으로 저장됩니다.

이 표에서는 개체에서 사용할 수 있는 다양한 종류의 저장소 계정을 보여줍니다.

|**저장소 계정의 유형**|**범용 표준**|**범용 프리미엄**|**Blob Storage, 핫 및 쿨 액세스 계층**|
|-----|-----|-----|-----|
|**지원되는 서비스**| Azure Blob 저장소, Azure Files, Azure Queue 저장소 | Blob 저장소 | Blob 저장소|
|**지원되는 Blob 유형**|블록 Blob, 페이지 Blob 및 추가 Blob | 페이지 Blob | 블록 Blob 및 추가 Blob|

범용 표준 및 프리미엄 저장소는 모두 페이지 Blob을 지원합니다. 비용이 주요 관심사인 경우 표준 저장소 계정을 선택합니다. 프리미엄 저장소는 더 많은 비용이 들지만 훨씬 더 높은 IOPS(I/O 작업/초)를 제공합니다. 성능 데이터가 VM에 대한 요구 사항인 경우 프리미엄 저장소를 선호합니다.

## <a name="attach-data-disks-to-vms"></a>VM에 데이터 디스크 연결

언제든지 VM에 디스크를 연결하여 가상 머신에 데이터 디스크를 추가할 수 있습니다. 디스크를 연결하면 VHD 파일이 VM에 연결됩니다. 

연결된 VHD는 저장소에서 삭제할 수 없습니다.

### <a name="attach-an-existing-data-disk-to-an-azure-vm"></a>Azure VM에 기존 데이터 디스크 연결

Azure VM에서 사용하려는 데이터를 저장하는 VHD를 이미 만든 분도 계실 것입니다. 법률 회사 시나리오를 예로 들자면, 이미 물리적 디스크를 로컬로 VHD로 변환한 것입니다. 이 경우 PowerShell `Add-AzureRmVhd` cmdlet을 사용하여 VHD를 저장소 계정에 업로드할 수 있습니다. 이 cmdlet은 VHD 파일을 전송하는 데 최적화되었으며 다른 방법보다 더 빨리 업로드를 완료할 수 있습니다. 최상의 성능을 위해 여러 스레드를 사용하여 전송이 완료됩니다. VHD가 업로드되면 기존 VM에 데이터 디스크로 연결합니다. 이 방법은 모든 종류의 데이터를 Azure VM에 배포하는 훌륭한 방법입니다. 데이터가 VM에 자동으로 표시되므로 새 디스크를 분할하거나 포맷할 필요가 없습니다.

### <a name="attach-a-new-data-disk-to-an-azure-vm"></a>Azure VM에 새 데이터 디스크 연결

Azure Portal을 사용하여 비어 있는 새 데이터 디스크를 VM에 추가할 수 있습니다. 

이 프로세스를 통해 사용자가 지정한 저장소 계정에 **.vhd** 파일이 페이지 Blob으로 생성되고, 해당 .vhd 파일은 VM에 데이터 디스크로 연결됩니다.

새 VHD를 사용하여 데이터를 저장하려면 먼저 새 디스크를 초기화하고, 분할하고, 포맷해야 합니다. 이 단계는 그 다음 연습에서 실습하겠습니다.

물리적 온-프레미스 서버에서는 데이터를 실제 하드 디스크에 저장합니다. VHD(가상 하드 디스크)의 Azure VM(가상 머신)에 데이터를 저장합니다. 이러한 VHD는 Azure 저장소 계정에 페이지 Blob으로 저장됩니다. 예를 들어 법률 회사의 판례 기록 데이터베이스를 Azure로 마이그레이션할 때 데이터베이스 파일을 저장할 VHD를 만들어야 합니다.