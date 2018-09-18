<span data-ttu-id="6bcca-101">이 모듈에서는 Azure 디스크 캐싱과 잠재적으로 성능이 향상되는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-101">In this module, you learned about Azure disk caching and how it potentially improves performance.</span></span> <span data-ttu-id="6bcca-102">Azure Portal 및 Azure PowerShell을 사용하여 VM에 대한 디스크 캐싱을 관리했습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-102">We used the Azure portal and Azure PowerShell to manage disk caching for our VM.</span></span> 

<span data-ttu-id="6bcca-103">Azure VM 디스크 캐싱 전략을 마련하고 나면 스크립트 및 템플릿을 사용하여 최적의 디스크 캐시 설정으로 새 VM 및 디스크를 빠르고 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-103">Once you have Azure VM disk caching strategy in place, you can then quickly and easily deploy new VMs and disk with the optimum disk cache settings, by using scripts and templates.</span></span>

## <a name="further-reading"></a><span data-ttu-id="6bcca-104">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="6bcca-104">Further reading</span></span>

- [<span data-ttu-id="6bcca-105">Azure Premium Storage: 고성능을 위한 설계</span><span class="sxs-lookup"><span data-stu-id="6bcca-105">Azure Premium Storage: Design for High Performance</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage-performance)
- [<span data-ttu-id="6bcca-106">Azure PowerShell 시작</span><span class="sxs-lookup"><span data-stu-id="6bcca-106">Get started with Azure PowerShell</span></span>](https://docs.microsoft.com/powershell/azure/get-started-azureps?view=azurermps-6.8.1)
- [<span data-ttu-id="6bcca-107">Azure 컴퓨터 Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="6bcca-107">Azure Computer Cmdlets Reference</span></span>](https://docs.microsoft.com/powershell/module/azurerm.compute/?view=azurermps-6.8.1#vm_disks)


## <a name="cleanup"></a><span data-ttu-id="6bcca-108">정리</span><span class="sxs-lookup"><span data-stu-id="6bcca-108">Cleanup</span></span>
<!---TODO: Update for sandbox?--->

<span data-ttu-id="6bcca-109">Azure VM을 실행하면 구독에 대한 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-109">Running Azure VMs incurs costs against your subscription.</span></span> <span data-ttu-id="6bcca-110">불필요한 비용을 피하려면 불필요한 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-110">Remove unneeded resources to avoid unnecessary charges.</span></span> <span data-ttu-id="6bcca-111">Azure 구독을 정리하는 가장 쉬운 방법은 리소스 그룹을 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-111">The easiest way to clean up your Azure subscription is to remove the resource group.</span></span> <span data-ttu-id="6bcca-112">해당 그룹을 삭제하면 리소스 그룹에 있는 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-112">Deleting a resource group deletes all the resources in that group.</span></span> <span data-ttu-id="6bcca-113">이 모듈을 마치면 다음 Azure PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-113">When you're finished with this module, run the following Azure PowerShell cmdlet:</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name "fotoshare-rg"
    ```

<span data-ttu-id="6bcca-114">삭제를 확인하라는 메시지가 표시되면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-114">When asked to confirm the delete, answer **Yes**.</span></span> <span data-ttu-id="6bcca-115">리소스가 삭제될 때 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcca-115">The command may take several minutes to complete as resources are deleted.</span></span>
