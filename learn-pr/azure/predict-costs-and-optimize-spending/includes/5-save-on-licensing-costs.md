라이선스는 클라우드 지출에 크게 영향을 줄 수 있는 또 다른 영역입니다. 라이선스 비용을 줄일 수 있는 몇 가지 방법을 살펴보겠습니다.

## <a name="azure-hybrid-benefit-for-windows-server"></a>Windows Server용 Azure Hybrid Benefit

많은 고객이 Windows Server 라이선스에 대한 투자를 높이고 Azure에서 이 투자의 용도를 변경하려고 합니다. Azure 하이브리드 혜택은 고객이 Azure의 가상 머신에 대해 이러한 라이선스를 사용할 수 있는 권한을 제공합니다. 즉, Windows Server 라이선스에 대해서는 비용이 청구되지 않고 Linux 요금이 청구됩니다. 

이 혜택을 받으려면 Windows 라이선스에 Software Assurance가 적용되어야 합니다. 다음 지침도 적용됩니다.

- 각 2개 프로세서 라이선스 또는 각 16코어 라이선스 집합이 있으면 최대 8코어 인스턴스 두 개 또는 최대 16코어 인스턴스 한 개를 받을 수 있습니다.
- Standard Edition 라이선스는 온-프레미스 또는 Azure에서 한 번만 사용할 수 있습니다. 즉, Azure VM 및 로컬 컴퓨터에 동일한 라이선스를 사용할 수 없습니다.
- Datacenter Edition 혜택은 온-프레미스와 Azure 둘 다에서 동시에 사용할 수 있으므로 라이선스 한 개로 두 대의 Windows 머신을 실행할 수 있습니다.

> [!NOTE]
> 대부분의 고객은 일반적으로 코어 단위로 라이선스가 부여되므로 해당 모델을 계산에 사용합니다. 보유한 라이선스에 대해 궁금한 점이 있으면 라이선스 리셀러 또는 Microsoft 계정 팀에 문의하세요.

혜택을 쉽게 적용할 수 있습니다. 기존 VM을 사용하여 언제든지 혜택을 켜고 끄거나, 배포 시 새 VM에 대해 적용할 수 있습니다. 하이브리드 혜택(특히 예약된 인스턴스와 결합된 경우)을 통해 라이선스 비용을 훨씬 절약할 수 있습니다.

## <a name="azure-hybrid-benefit-for-sql-server"></a>SQL Server에 대한 Azure 하이브리드 혜택

SQL Server에 대한 Azure 하이브리드 혜택을 사용하면 현재 라이선스의 투자 가치를 최대화하고 클라우드로의 마이그레이션을 가속화할 수 있습니다. SQL Server에 대한 Azure 하이브리드 혜택은 활성 Software Assurance가 포함된 SQL Server 라이선스를 사용하여 할인된 요금을 지불할 수 있게 하는 Azure 기반 혜택입니다.

Azure 리소스가 활성 중인 경우에도 이 혜택을 적용할 수 있지만, 할인된 요금은 포털에서 해당 요금을 선택한 시점부터 적용됩니다. 크레딧은 소급해서 발급되지 않습니다.

### <a name="azure-sql-database-vcore-based-options"></a>Azure SQL Database vCore 기반 옵션

Azure SQL Database에 대한 Azure 하이브리드 혜택은 다음과 같습니다.

- 활성 Software Assurance를 포함하는 Standard Edition 코어 단위 라이선스가 있는 경우 온-프레미스에 소유한 라이선스 코어마다 하나의 vCore를 범용 서비스 계층에서 사용할 수 있습니다.
- 활성 Software Assurance를 포함하는 Enterprise Edition 코어 단위 라이선스가 있는 경우 온-프레미스에 소유한 라이선스 코어마다 1개의 vCore를 중요 비즈니스용 서비스 계층에서 사용할 수 있습니다. 중요 비즈니스용 서비스 계층용 SQL Server에 대한 Azure 하이브리드 혜택은 Enterprise Edition 라이선스가 있는 고객에게만 제공됩니다.
- 활성 Software Assurance를 포함하는 높은 가상화 수준의 Enterprise Edition 코어 단위 라이선스가 있는 경우 온-프레미스에 소유한 라이선스 코어마다 4개의 vCore를 범용 서비스 계층에서 사용할 수 있습니다. 이는 Azure SQL Database에서만 사용할 수 있는 고유한 가상화 혜택입니다.

다음 그림은 SQL Server 라이선스에 대한 Azure 하이브리드 혜택을 통해 각 서비스 계층에서 사용할 수 있는 vCore 기반 옵션을 보여 줍니다.

![Azure 하이브리드 혜택을 사용하여 기존 SQL Server 라이선스의 가치를 최대화하는 방법에 대한 예제를 보여 주는 그림입니다.](../media-drafts/5-sql-tradein-value.png)

Azure Virtual Machines의 SQL Server에 대한 Azure 하이브리드 혜택은 다음과 같습니다.

- 활성 Software Assurance를 포함하는 Enterprise Edition 코어 단위 라이선스가 있는 경우 온-프레미스에 소유한 라이선스 코어마다 1개의 SQL Server Enterprise Edition 코어를 Azure Virtual Machines에서 사용할 수 있습니다.
- 활성 Software Assurance를 포함하는 Standard Edition 코어 단위 라이선스가 있는 경우 온-프레미스에 소유한 라이선스 코어마다 1개의 SQL Server Standard Edition 코어를 Azure Virtual Machines에서 사용할 수 있습니다.

이는 SQL Server 워크로드에 대한 Azure 지출에 큰 영향을 미칠 수 있습니다.

## <a name="use-devtest-subscription-offers"></a>개발/테스트 구독 제안 사용

[Enterprise 개발/테스트](https://azure.microsoft.com/offers/ms-azr-0148p/) 및 [종량제 개발/테스트](https://azure.microsoft.com/offers/ms-azr-0023p/) 제안은 비프로덕션 환경에서 비용을 절약하기 위해 활용할 수 있는 혜택입니다. 이 혜택은 특히 Windows 워크로드와 관련해서 여러 가지 할인을 제공하여, 라이선스 비용 없이 가상 머신에 대한 Linux 요금만 청구합니다. 이 혜택은 SQL Server 및 Visual Studio 구독(이전의 MSDN)이 적용되는 기타 모든 Microsoft 소프트웨어에도 적용됩니다. 이 혜택에 대한 몇 가지 요구 사항이 있습니다. 비프로덕션 워크로드에만 적용되고, 이러한 환경의 모든 사용자(테스터 제외)에게 Visual Studio 구독이 있어야 한다는 것입니다. 간단히 말해, 비프로덕션 워크로드의 경우 이 혜택을 통해 Windows, SQL Server 및 기타 Microsoft 가상 머신 워크로드에서 비용을 절약할 수 있습니다.
다음은 각 제안에 대한 전체 세부 정보입니다. 기업계약 고객인 경우 Enterprise 개발/테스트 제안을 이용하고, 기업계약이 없는 고객이며 대신 PAYG 계정을 사용하는 경우 종량제 개발/테스트 제안을 이용합니다.

## <a name="bring-your-own-sql-server-license"></a>사용자 SQL Server 라이선스 필요

기업계약 고객이고 SQL Server 라이선스에 대한 기존 투자가 있으며 Azure로 리소스를 이동하는 과정에서 라이선스가 확보된 경우, Azure Marketplace에서 **BYOL**(사용자 라이선스 필요) 이미지를 프로비전하여 사용하지 않는 이러한 라이선스를 이용하고 Azure VM 비용을 줄일 수 있습니다. 언제든지 Windows VM을 프로비전하고 SQL Server를 수동으로 설치하여 이 작업을 수행할 수 있었지만, 이 경우 Microsoft 인증 이미지를 활용하여 생성 프로세스가 간소화됩니다. Marketplace에서 **BYOL**을 검색하여 해당 이미지를 찾으세요.

![Azure의 SQL Server용 BYOL](../media-drafts/5-byol-sql-server.png)

> [!IMPORTANT]
> 인증된 BYOL 이미지를 사용하려면 기업계약 구독이 필요합니다.

## <a name="use-sql-server-developer-edition"></a>SQL Server Developer Edition 사용

SQL Server Developer Edition이 **비프로덕션 용도**로 사용할 수 있는 무상 제품임을 모르는 사람들이 많습니다. Developer Edition에는 Enterprise Edition의 모든 기능이 포함되어 있으므로, 비프로덕션 워크로드의 경우 라이선스 비용을 훨씬 절약할 수 있습니다.

Azure Marketplace에서 Developer Edition용 SQL Server 이미지를 찾아 개발 또는 테스트 용도로 사용하면 이러한 경우의 SQL Server에 대한 추가 비용이 발생하지 않습니다. 

> [!NOTE]
> 전체 라이선스 정보를 보려면 [문서화된 가격 책정 지침](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance)을 확인하세요.

## <a name="use-constrained-instance-sizes-for-database-workloads"></a>데이터베이스 워크로드에 대해 제한된 인스턴스 크기 사용 

메모리, 저장소 또는 I/O 대역폭에 대한 요구 사항이 높지만 CPU 코어 개수는 적은 고객이 많습니다. 이러한 일반적인 요청에 따라, Microsoft는 가장 많이 사용되는 VM 크기(DS, ES, GS 및 MS)에 대해 동일한 메모리, 저장소 및 I/O 대역폭을 유지하면서 vCPU 개수를 원래 VM 크기의 1/2 또는 1/4로 제한하는 새로운 크기를 제공합니다.

| VM 크기 | vCPU | 메모리 | 최대 디스크 수 | 최대 I/O 처리량 | 연간 SQL Server Enterprise 라이선스 비용 | 연간 총비용(계산 + 라이선스) |
|---------|-------|--------|-----------|--------------------|-----------------------------------------------|---------------------------|
| Standard_DS14v2   | 16 | 112GB | 32 | 51,200 IOPS 또는 768MB/s |           |           |
| Standard_DS14-4v2 | **4**  | 112GB | 32 | 51,200 IOPS 또는 768MB/s | 75% 더 낮음 | 57% 더 낮음 |
| Standard_GS5      | 32 | 448    | 64 | 80,000 IOPS 또는 2GB/s   |           |           |
| Standard_GS5-8    | **8**  | 448    | 64 | 80,000 IOPS 또는 2GB/s   | 75% 더 낮음 | 42% 더 낮음 |

SQL Server 및 Oracle과 같은 데이터베이스 제품은 CPU당 라이선스가 부여되므로, 이 혜택을 통해 고객은 최대 75%까지 라이선스 비용을 절감하면서도 여전히 고성능의 데이터베이스를 유지할 수 있습니다. 
