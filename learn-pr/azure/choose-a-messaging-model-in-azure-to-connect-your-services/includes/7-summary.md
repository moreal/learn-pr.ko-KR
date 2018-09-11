<span data-ttu-id="b19f6-101">이 모듈에서는 안정적이고 복원력 있는 분산 응용 프로그램을 만들 수 있는 네 가지 Azure 서비스를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-101">In this module, you have explored four different Azure services that allow you to create reliable and resilient distributed applications.</span></span> <span data-ttu-id="b19f6-102">서비스를 선택한다는 것은 구성 요소 간에 전달할 데이터 유형(메시지 또는 이벤트)과 데이터에 제공해야 하는 기능을 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-102">Choosing between them is a matter of deciding the type of data that needs to be passed between components (messages or events), and then what features you need to deliver and process the data.</span></span>

## <a name="clean-up"></a><span data-ttu-id="b19f6-103">정리</span><span class="sxs-lookup"><span data-stu-id="b19f6-103">Clean up</span></span>

<span data-ttu-id="b19f6-104">Storage 계정에는 Azure 구독 비용을 발생시키는 데이터가 포함되지만, 메시지가 몇 개 없는 작은 큐는 비용이 많이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-104">While a Storage Account contains data, it incurs a cost against your Azure subscription, although these are likely to be low for small queue with few messages.</span></span> <span data-ttu-id="b19f6-105">큐 작업을 마친 후에는 불필요한 변경을 방지할 수 있도록 반드시 큐를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-105">When you have finished with the queue, remember to remove it in order to avoid unnecessary charges.</span></span> <span data-ttu-id="b19f6-106">모든 리소스를 같은 리소스 그룹에 만들었기 때문에 Azure 구독을 정리하는 가장 쉬운 방법은 리소스 그룹을 제거하여 해당 내용을 모두 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-106">Because you created all the resources in the same resource group, the easiest way to clean up your Azure subscription is to remove the resource group which will remove all its contents:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```

<span data-ttu-id="b19f6-107">삭제를 확인하라는 메시지가 표시되면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-107">When you are asked to confirm the delete, answer **Yes**.</span></span>

<span data-ttu-id="b19f6-108">리소스가 삭제될 때 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19f6-108">The command may take several minutes to complete as resources are deleted.</span></span>