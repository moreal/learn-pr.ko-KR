<span data-ttu-id="964b2-101">이제 가상 머신이 생성되었으므로 다른 명령을 통해 가상 머신에 대한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="964b2-102">먼저 `vm list`를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="964b2-103">이 명령은 이 구독에 정의된 ‘모든’ 가상 머신을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="964b2-104">`--resource-group` 매개 변수를 통해 출력을 특정 리소스 그룹으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="964b2-105">출력 형식</span><span class="sxs-lookup"><span data-stu-id="964b2-105">Output types</span></span>
<span data-ttu-id="964b2-106">지금까지 수행한 모든 명령의 기본 응답 유형은 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="964b2-107">이는 스크립팅에 적합하지만 대부분의 사용자가 읽기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="964b2-108">`--output` 플래그를 통해 응답의 출력 스타일을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="964b2-109">예를 들어 Azure Cloud Shell에서 다음 명령을 시도하여 다른 출력 스타일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="964b2-110">`table`과 함께 `json`(기본값), `jsonc`(색으로 표시된 JSON) 또는 `tsv`(테이블로 구분된 값)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="964b2-111">위 명령에서 몇 가지 변형을 시도하여 차이를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="964b2-112">IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="964b2-112">Getting the IP address</span></span>

<span data-ttu-id="964b2-113">또 다른 유용한 명령은 `vm list-ip-addresses`로, VM의 공용 및 개인 IP 주소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="964b2-114">주소가 변경되거나 만드는 동안 주소를 캡처하지 않은 경우 언제든지 주소를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="964b2-115">반환 결과</span><span class="sxs-lookup"><span data-stu-id="964b2-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="964b2-116">`--output` 플래그의 줄임 구문을 `-o`로 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="964b2-117">Azure CLI 명령에 대한 대부분의 매개 변수는 하나의 대시 및 문자로 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="964b2-118">예를 들어 `--name`은 `-n`으로 줄이고 `--resource-group`은 `-g`로 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="964b2-119">이는 편리하게 입력할 수 있지만 분명하게 하기 위해 스크립트에서는 전체 옵션 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="964b2-120">각 명령에 대한 자세한 내용은 설명서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="964b2-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="964b2-121">VM 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="964b2-121">Getting VM details</span></span>

<span data-ttu-id="964b2-122">`vm show` 명령을 사용하여 이름 또는 ID별로 특정 가상 머신에 대한 자세한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="964b2-123">이 명령은 연결된 저장소 장치, 네트워크 인터페이스 및 VM이 연결된 리소스의 모든 개체 ID를 포함하여 VM에 대한 모든 종류의 정보가 포함된 상당히 큰 JSON 블록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="964b2-124">다시 표 형식으로 변경할 수 있지만 이렇게 하면 거의 모든 흥미로운 데이터가 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="964b2-125">대신에 [JMESPath](http://jmespath.org/)라는 JSON의 기본 제공 쿼리 언어로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="964b2-126">JMESPath를 사용하여 쿼리에 필터 추가</span><span class="sxs-lookup"><span data-stu-id="964b2-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="964b2-127">JMESPath는 JSON 개체를 중심으로 빌드되는 업계 표준 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="964b2-128">가장 단순한 쿼리는 JSON 개체에서 키를 선택하는 _ID_를 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="964b2-129">예를 들어 다음과 같은 개체가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-129">For example, given the object:</span></span>

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

<span data-ttu-id="964b2-130">쿼리 `people`을 사용하여 `people` 배열에 대한 값 배열을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="964b2-131">사용자 중 ‘한 명’만 필요한 경우 인덱서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="964b2-132">예를 들어 `people[1]`은 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="964b2-133">또한 몇 가지 조건에 따라 개체의 하위 집합을 반환하는 특정 한정자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-133">We can also add specific qualifiers that would return a subset of the objects based on some criteria.</span></span> <span data-ttu-id="964b2-134">예를 들어, 한정자 `people[?age > '25']`을 추가하면 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-134">For example, adding the qualifier `people[?age > '25']` would return:</span></span>

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

<span data-ttu-id="964b2-135">마지막으로 이름만 반환하는 select: `people[?age > '25'].[name]`을 추가하여 결과를 제약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-135">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

<span data-ttu-id="964b2-136">JMESQuery에는 여러 가지 다른 흥미로운 쿼리 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-136">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="964b2-137">시간이 있는 경우 [JMESPath.org](http://jmespath.org/) 사이트에서 사용 가능한 [온라인 자습서](http://jmespath.org/tutorial.html)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="964b2-137">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="964b2-138">Azure CLI 쿼리 필터링</span><span class="sxs-lookup"><span data-stu-id="964b2-138">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="964b2-139">JMES 쿼리를 기본적으로 이해하면 `vm show` 명령과 같은 쿼리에서 반환되는 데이터에 파일러(filer)를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-139">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="964b2-140">예를 들어 관리 사용자 이름을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-140">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="964b2-141">VM에 할당된 크기를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-141">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="964b2-142">또는 네트워크 인터페이스의 모든 ID를 검색하려면 다음 쿼리를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-142">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="964b2-143">이 쿼리 방법은 Azure CLI 명령과 함께 작동하며 명령줄에서 특정 데이터를 끌어오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-143">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="964b2-144">이 방법은 스크립팅에 유용합니다. 예를 들어 Azure 계정에서 값을 끌어오고 이를 환경 또는 스크립트 변수에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-144">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="964b2-145">이 방법으로 사용하기로 한 경우 추가할 유용한 플래그는 `--output tsv` 매개 변수(`-o tsv`로 줄일 수 있음)입니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-145">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="964b2-146">이 매개 변수는 탭 구분 기호와 함께 실제 데이터 값만 포함하는 탭으로 구분된 값으로 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-146">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="964b2-147">예를 들어</span><span class="sxs-lookup"><span data-stu-id="964b2-147">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="964b2-148">`/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic` 텍스트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="964b2-148">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
