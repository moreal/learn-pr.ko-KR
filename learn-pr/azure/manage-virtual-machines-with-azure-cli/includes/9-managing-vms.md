<span data-ttu-id="0d5d4-101">가상 머신을 실행하는 중에 수행할 기본 작업 중 하나는 가상 머신을 시작 및 중지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-101">One of the main tasks you'll want to do while running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="0d5d4-102">VM 중지</span><span class="sxs-lookup"><span data-stu-id="0d5d4-102">Stopping a VM</span></span>

<span data-ttu-id="0d5d4-103">`vm stop` 명령으로 실행 중인 VM을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="0d5d4-104">이름과 리소스 그룹 또는 VM의 고유 ID를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="0d5d4-105">`ssh`를 사용하거나 `vm get-instance-view` 명령을 통해 공용 IP 주소를 ping하여 중지했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="0d5d4-106">이 마지막 방법은 `vm show`와 동일한 기본 데이터를 반환하지만 인스턴스 자체에 대한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="0d5d4-107">Azure Cloud Shell에 다음 명령을 입력하여 VM의 현재 실행 상태를 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

<span data-ttu-id="0d5d4-108">이 명령은 `VM stopped`를 결과로 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="0d5d4-109">VM 시작</span><span class="sxs-lookup"><span data-stu-id="0d5d4-109">Starting a VM</span></span>

<span data-ttu-id="0d5d4-110">`vm start` 명령을 통해 되돌리기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="0d5d4-111">이 명령은 중지된 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-111">This command will start a stopped VM.</span></span> <span data-ttu-id="0d5d4-112">`vm get-instance-view` 쿼리를 통해 이제 `VM running`을 반환하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="0d5d4-113">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="0d5d4-113">Restarting a VM</span></span>

<span data-ttu-id="0d5d4-114">마지막으로 `vm restart` 명령을 사용하여 재부팅해야 하는 변경 내용이 있는 경우 VM을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="0d5d4-115">VM이 재부팅될 때까지 기다리지 않고 Azure CLI가 즉시 반환하도록 하려면 `--no-wait` 플래그를 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5d4-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

