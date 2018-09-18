
<span data-ttu-id="dd6fe-101">이전 연습에서는 Azure Portal을 사용하여 다음 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-101">In the previous exercise, we performed the following tasks using the Azure portal.</span></span>

- <span data-ttu-id="dd6fe-102">OS 디스크 캐시 상태 보기</span><span class="sxs-lookup"><span data-stu-id="dd6fe-102">View OS disk cache status</span></span>
- <span data-ttu-id="dd6fe-103">OS 디스크 캐시 설정 변경</span><span class="sxs-lookup"><span data-stu-id="dd6fe-103">Change the cache settings of the OS disk</span></span>
- <span data-ttu-id="dd6fe-104">VM에 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="dd6fe-104">Add a data disk to the VM</span></span>
- <span data-ttu-id="dd6fe-105">새 데이터 디스크의 캐싱 유형 변경</span><span class="sxs-lookup"><span data-stu-id="dd6fe-105">Change caching type on a new data disk</span></span>

<span data-ttu-id="dd6fe-106">이제 Azure PowerShell을 사용하여 이러한 작업을 연습해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-106">Let's practice these operations using Azure PowerShell.</span></span> <span data-ttu-id="dd6fe-107">이전 연습에서 만든 VM을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-107">We're going to use the VM we created in the previous exercise.</span></span> <span data-ttu-id="dd6fe-108">이 랩의 작업은 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-108">The operations in this lab assume:</span></span>

- <span data-ttu-id="dd6fe-109">**fotoshareVM**이라고 하는 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-109">Our VM exists and is called **fotoshareVM**</span></span>
- <span data-ttu-id="dd6fe-110">VM은 **fotoshare-rg**라는 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-110">Our VM lives in a resource group called **fotoshare-rg**</span></span>

<span data-ttu-id="dd6fe-111">다른 이름 집합을 사용한 경우 이러한 값을 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-111">If you've gone with a different set of names, just replace these values with yours.</span></span> 

<span data-ttu-id="dd6fe-112">마지막 연습에서 VM 디스크의 현재 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-112">Here's the current state of our VM disks from the last exercise.</span></span> 

![OS 및 데이터 디스크의 스크린샷(모두 읽기 전용 캐싱으로 설정됨)](../media-draft/disks-final-config-portal.PNG)

<span data-ttu-id="dd6fe-114">포털을 사용하여 OS 디스크와 데이터 디스크 모두에 대해 \***호스트 캐싱** 필드를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-114">We used the portal to set the \***HOST CACHING** field for both the OS and data disks.</span></span> <span data-ttu-id="dd6fe-115">다음 단계를 진행하면서 이 초기 상태를 명심하세요.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-115">Keep this initial state in mind as we work through the following steps.</span></span> 

### <a name="set-up-some-variables"></a><span data-ttu-id="dd6fe-116">일부 변수 설정</span><span class="sxs-lookup"><span data-stu-id="dd6fe-116">Set up some variables</span></span>
<span data-ttu-id="dd6fe-117">먼저, 나중에 사용할 수 있도록 일부 리소스 이름을 저장하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-117">First, let's  store some resource names so we can use them later.</span></span>

<span data-ttu-id="dd6fe-118">오른쪽에 있는 Azure Cloud Shell 터미널을 사용하여 다음 Powershell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-118">Use the Azure Cloud Shell terminal on the right to run the following Powershell commands.</span></span> 

```powershell
$myRgName = "fotoshare-rg"
$myVMName = "fotoshareVM"
```

> [!TIP]
> <span data-ttu-id="dd6fe-119">Cloud Shell 세션의 시간이 초과되면 이러한 변수를 다시 설정해야 합니다. 따라서 가능하다면 이 전체 랩을 단일 세션에서 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-119">You'll have to set these variables again if your Cloud Shell session times out. So, if possible, work through this entire lab in a single session.</span></span> 

### <a name="get-info-about-our-vm"></a><span data-ttu-id="dd6fe-120">VM에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="dd6fe-120">Get info about our VM</span></span>

<span data-ttu-id="dd6fe-121">다음 명령을 실행하여 VM의 속성을 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-121">Run the following command to get back the properties of our VM.</span></span>
 
```powershell
$myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVMName
```
<span data-ttu-id="dd6fe-122">응답을 `$myVM` 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-122">We store the response in our `$myVM` variable.</span></span> <span data-ttu-id="dd6fe-123">다음 명령을 실행하여 여기서 지정한 속성을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-123">We can run the following command to just show us the properties we specify here.</span></span>

```powershell
$myVM | select-object -property ResourceGroupName, Name, Type, Location
```

<span data-ttu-id="dd6fe-124">다음 스크린샷에서 볼 수 있듯이 이 VM은 실제로 살펴볼 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-124">As the following screenshot shows, this VM is indeed the VM we're after.</span></span> <span data-ttu-id="dd6fe-125">이제 진행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-125">So, let's move on.</span></span> 

![마지막으로 실행한 4개의 명령 결과를 보여 주는 PowerShell 콘솔](../media-draft/ps-commands-1.PNG)

### <a name="view-os-disk-cache-status"></a><span data-ttu-id="dd6fe-127">OS 디스크 캐시 상태 보기</span><span class="sxs-lookup"><span data-stu-id="dd6fe-127">View OS disk cache status</span></span>

<span data-ttu-id="dd6fe-128">다음과 같이 `StorageProfile` 개체를 통해 캐싱 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-128">We can check the caching  setting through  the `StorageProfile` object as follows.</span></span>

```powershell
$myVM.StorageProfile.OsDisk.Caching
```
<span data-ttu-id="dd6fe-129">이 예제에서 현재 값은 **없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-129">In this example, the current value is **None**.</span></span> <span data-ttu-id="dd6fe-130">OS 디스크에 대한 기본값으로 다시 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-130">Let's change it back to the default for an OS disk.</span></span>

![캐싱 값이 "없음"인 OS 디스크를 보여 주는 PowerShell 콘솔](../media-draft/ps-oscaching-none.PNG)

### <a name="change-the-cache-settings-of-the-os-disk"></a><span data-ttu-id="dd6fe-132">OS 디스크 캐시 설정 변경</span><span class="sxs-lookup"><span data-stu-id="dd6fe-132">Change the cache settings of the OS disk</span></span>

<span data-ttu-id="dd6fe-133">다음과 같이 동일한 StorageProfile 개체를 사용하여 캐시 유형에 대한 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-133">We can set the value for the cache type using the same StorageProfile\` object as follows.</span></span>
 
```powershell
$myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
```

<span data-ttu-id="dd6fe-134">이 명령은 빠르게 실행되며, 작업을 로컬로 수행하고 있음을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-134">This command runs fast, which should tell you it's doing something locally.</span></span> <span data-ttu-id="dd6fe-135">이 명령은 myVM 개체의 속성만 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-135">The command just changes the property on the myVM object.</span></span> <span data-ttu-id="dd6fe-136">다음 스크린샷에서 볼 수 있듯이 `$myVM` 변수를 새로 고치더라도 VM에서 캐싱 값이 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-136">As the following screenshot shows, if you refresh the `$myVM` variable,  the caching value won't have changed on the VM.</span></span>

!["myVM" 개체를 새로 고치면 VM을 실제로 업데이트하지 않으므로 캐싱을 "없음"으로 다시 설정하는 것을 보여 주는 PowerShell 콘솔](../media-draft/ps-commands-2.PNG)

<span data-ttu-id="dd6fe-138">VM 자체를 변경하려면 다음과 같이 `Update-AzureRmVM`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-138">To  make the change on the VM itself, call `Update-AzureRmVM` as follows.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

<span data-ttu-id="dd6fe-139">이 호출은 완료하는 데 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-139">Notice that this call takes a while to complete.</span></span> <span data-ttu-id="dd6fe-140">이는 실제 VM을 업데이트하고 Azure에서 변경하기 위해 VM을 다시 시작하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-140">That's because we're updating the actual VM and Azure restarts the VM  to make the change.</span></span>

![캐싱 값이 "없음"인 OS 디스크를 보여 주는 PowerShell 콘솔](../media-draft/ps-oscaching-rw.PNG)

<span data-ttu-id="dd6fe-142">`$myVM` 변수를 다시 새로 고치면 개체에 대한 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-142">If you refresh the `$myVM` variable again, you'll see the change on the object.</span></span> <span data-ttu-id="dd6fe-143">또한 포털에서 디스크를 살펴볼 때도 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-143">Looking at the disk in the portal, you'd also see the change there.</span></span> <span data-ttu-id="dd6fe-144">이제 새 데이터 디스크를 만드는 단계로 넘어가겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-144">Ok, let's move on to creating a new data disk.</span></span>  

### <a name="list-data-disk-info"></a><span data-ttu-id="dd6fe-145">데이터 디스크 정보 나열</span><span class="sxs-lookup"><span data-stu-id="dd6fe-145">List data disk info</span></span>

<span data-ttu-id="dd6fe-146">VM에 있는 데이터 디스크를 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-146">To see what data disks we have on our VM, run the following command.</span></span> 

```powershell
$myVM.StorageProfile.DataDisks
```

<span data-ttu-id="dd6fe-147">현재 하나의 데이터 디스크만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-147">We've only one data disk at the moment.</span></span> <span data-ttu-id="dd6fe-148">`Lun` 필드가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-148">The `Lun` field is important.</span></span> <span data-ttu-id="dd6fe-149">고유한 LUN(**논리** **단위** **번호**)입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-149">It's the unique **L**ogical **U**nit **N**umber.</span></span> <span data-ttu-id="dd6fe-150">다른 데이터 디스크를 추가하는 경우 고유한 `Lun` 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-150">When we add another data disk, we'll give it a unique `Lun` value.</span></span> 

### <a name="add-a-new-data-disk-to-our-vm"></a><span data-ttu-id="dd6fe-151">VM에 새 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="dd6fe-151">Add a new data disk to our VM</span></span> 

<span data-ttu-id="dd6fe-152">편의상 새 디스크 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-152">For convenience, we'll store our new disk name.</span></span>

```powershell
$newDiskName = "fotoshareVM-data2"
```

<span data-ttu-id="dd6fe-153">다음 `Add-AzureRmVMDataDisk` 명령을 실행하여 새 디스크를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-153">Run the following `Add-AzureRmVMDataDisk` command to define a new disk.</span></span> 

```powershell
Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
```

<span data-ttu-id="dd6fe-154">이 디스크의 LUN 값을 사용되지 않은 1로 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-154">We've given this disk a Lun value of 1, since that's not taken.</span></span> <span data-ttu-id="dd6fe-155">만들려는 디스크를 정의했으므로 `Update-AzureRmVM`을 실행하여 변경 내용을 실제로 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-155">We defined the disk we want to create, so it's time to run `Update-AzureRmVM` to make the actual change.</span></span> 

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

<span data-ttu-id="dd6fe-156">데이터 디스크 정보를 다시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-156">Let's look at our data disk info again.</span></span>

```powershell
$myVM.StorageProfile.DataDisks
```

![두 데이터 디스크를 보여 주는 PowerShell 콘솔](../media-draft/2-data-disks-part1.png)

<span data-ttu-id="dd6fe-158">이제 두 개의 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-158">We now have two disks.</span></span> <span data-ttu-id="dd6fe-159">새 디스크의 **LUN** 값은 1이고 **캐싱**에 대한 기본값은 **없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-159">Our new disk has a **Lun** of 1 and the default value for **Caching** is **None**.</span></span> <span data-ttu-id="dd6fe-160">해당 값을 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-160">Let's change that value.</span></span>

### <a name="change-cache-settings-of-new-data-disk"></a><span data-ttu-id="dd6fe-161">새 데이터 디스크의 캐시 설정 변경</span><span class="sxs-lookup"><span data-stu-id="dd6fe-161">Change cache settings of new data disk</span></span>

<span data-ttu-id="dd6fe-162">다음과 같이 `Set-AzureRmVMDataDisk` cmdlet을 사용하여 가상 머신 데이터 디스크의 속성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-162">We modify properties of a virtual machine data disk with the `Set-AzureRmVMDataDisk` cmdlet as follows.</span></span>

```powershell
Set-AzureRmVMDataDisk -Lun "1" -Caching ReadWrite
```

<span data-ttu-id="dd6fe-163">언제나 그렇듯이 `Update-AzureRmVM`을 사용하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-163">As always, commit the changes with `Update-AzureRmVM`.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

<span data-ttu-id="dd6fe-164">다음은 이 연습에서 수행한 작업을 보여 주는 포털의 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-164">Here's a view from the portal of what we've accomplished in this exercise.</span></span> <span data-ttu-id="dd6fe-165">VM에는 이제 두 개의 데이터 디스크가 있고, 모든 **호스트 캐싱** 설정을 조정했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-165">Our VM now has two data disks and we've adjust all **HOST Caching** settings.</span></span> <span data-ttu-id="dd6fe-166">이 모든 작업은 단지 몇 가지 명령을 사용하여 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-166">We did all of that with just a few commands.</span></span> <span data-ttu-id="dd6fe-167">이것이 Azure PowerShell의 능력입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6fe-167">That's the power of Azure PowerShell.</span></span>

![두 데이터 디스크를 보여 주는 PowerShell 콘솔](../media-draft/disks-final-config-portal2.png)
