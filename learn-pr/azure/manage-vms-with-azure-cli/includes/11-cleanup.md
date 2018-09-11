<span data-ttu-id="8672d-101">새 Linux 가상 머신을 만들고, 머신의 크기를 변경하고, 머신을 중지했다가 다시 시작하고, Azure CLI로 구성을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="8672d-102">정리</span><span class="sxs-lookup"><span data-stu-id="8672d-102">Cleanup</span></span>

<span data-ttu-id="8672d-103">이제 VM 사용을 마쳤으며 더 이상 VM이 필요하지 않으므로 리소스를 삭제하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="8672d-104">정리는 계정에 대해 계속 비용이 청구될 수 있는 계산 및 저장소 리소스에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="8672d-105">`delete` 명령을 사용하여 개별 리소스를 삭제할 수 있지만, 모든 리소스를 제거하는 가장 손쉬운 방법은 `az group delete`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="8672d-106">Azure CLI에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="8672d-107">표시되는 프롬프트에 “예”로 답하거나 `--yes` 매개 변수를 사용하여 프롬프트에 자동으로 답합니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="8672d-108">이 명령은 리소스 그룹과 연관된 모든 리소스를 삭제하며, 올바른 순서로 리소스 할당을 취소할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="8672d-109">`--no-wait` 매개 변수는 삭제가 수행되는 동안 Azure CLI가 차단되지 않도록 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-109">The `--no-wait` parameter keeps the Azure CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="8672d-110">리소스가 삭제될 때까지 대기하려면 이 매개 변수를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="8672d-111">또는 나중에 스크립트에서 `az group wait -n ExerciseResources --deleted` 명령을 사용하여 삭제가 완료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="8672d-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to finish.</span></span>


## <a name="further-reading"></a><span data-ttu-id="8672d-112">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="8672d-112">Further reading</span></span>

* [<span data-ttu-id="8672d-113">Azure CLI 개요</span><span class="sxs-lookup"><span data-stu-id="8672d-113">Azure CLI overview</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [<span data-ttu-id="8672d-114">Azure CLI 명령 참조</span><span class="sxs-lookup"><span data-stu-id="8672d-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
