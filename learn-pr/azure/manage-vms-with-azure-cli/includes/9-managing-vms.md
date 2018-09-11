가상 머신을 실행하기 위해 수행할 기본 작업 중 하나는 가상 머신을 시작 및 중지하는 것입니다.

## <a name="stopping-a-vm"></a>VM 중지

`vm stop` 명령으로 실행 중인 VM을 중지할 수 있습니다. 이름과 리소스 그룹 또는 VM의 고유 ID를 전달해야 합니다.

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

`ssh`를 사용하거나 `vm get-instance-view` 명령을 통해 공용 IP 주소를 ping하여 중지했는지 확인할 수 있습니다. 이 마지막 방법은 `vm show`와 동일한 기본 데이터를 반환하지만 인스턴스 자체에 대한 세부 정보를 포함합니다. Azure Cloud Shell에 다음 명령을 입력하여 VM의 현재 실행 상태를 확인해 보세요.

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

이 명령은 `VM stopped`를 결과로 반환해야 합니다.

## <a name="starting-a-vm"></a>VM 시작

`vm start` 명령을 통해 되돌리기를 수행할 수 있습니다.

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

이 명령은 중지된 VM을 시작합니다. `vm get-instance-view` 쿼리를 통해 이제 `VM running`을 반환하는지 확인할 수 있습니다.

## <a name="restarting-a-vm"></a>VM 다시 시작

마지막으로 `vm restart` 명령을 사용하여 재부팅해야 하는 변경 내용이 있는 경우 VM을 다시 시작할 수 있습니다. VM이 재부팅될 때까지 기다리지 않고 Azure CLI가 즉시 반환하도록 하려면 `--no-wait` 플래그를 추가하면 됩니다.

