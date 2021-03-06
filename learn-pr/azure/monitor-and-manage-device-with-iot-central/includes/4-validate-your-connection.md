이제 Azure IoT Central 응용 프로그램을 사용하여 커피 머신을 Azure IoT Central에 연결했습니다. 따라서 원격 커피 머신을 모니터링하고 관리를 시작할 수 있습니다. 이 모듈에서는 앞에서 정의한 연결된 커피 메이커 템플릿을 사용하여 설정과 연결의 유효성을 검사합니다. 설정에서 최적의 온도를 업데이트하고, 머신 상태를 확인하는 명령을 실행하고, 대시보드에서 연결된 커피 머신을 살펴봅니다. 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a>응용 프로그램이 커피 머신과 동기화되도록 설정 업데이트

**설정** 페이지에서 응용 프로그램의 구성 데이터를 커피 머신으로 보냅니다. 

이 시나리오에서는 최적 온도를 변경하고 **업데이트**를 선택합니다. 변경된 설정은 커피 머신이 설정 변경에 응답했음을 승인할 때까지 UI에서 보류 중으로 표시됩니다. 

> [!NOTE]
> 설정이 정상적으로 업데이트되면 데이터 흐름을 나타내고 연결 유효성을 검사합니다. 그러면 원격 분석 측정에서 최적 온도 업데이트에 응답합니다. **측정값** 페이지에서 변경 내용을 관찰할 수 있습니다. 

## <a name="run-commands-on-the-coffee-machine"></a>커피 머신에서 명령 실행 
다음 연습의 **명령** 페이지로 이동합니다. 명령 설정의 유효성을 검사하기 위해 IoT Central에서 원격으로 커피 머신에서 명령을 실행합니다. 명령이 성공하면 커피 머신에서 확인 메시지가 전송됩니다.

1. **실행**을 선택하여 원격으로 끓이기를 시작합니다. 
    
    다음 세 가지 조건이 충족되면 커피 머신이 시작됩니다.
    - 컵이 검색됨
    - 유지 관리 중이 아님
    - 이미 커피를 끓이고 있는 상태가 아님  

    > [!NOTE]
    > 커피 끓이기가 정상적으로 시작되면 **측정값** > **상태**에 표시된 대로 머신 상태가 노란색으로 변경됩니다. 
    
    node.js 시뮬레이션된 커피 머신의 콘솔 로그에서 확인 메시지를 살펴봅니다. 

    ![명령 실행](../media/4-commands-brewing.png)

1. **실행**을 선택하여 유지 관리 모드를 설정합니다. 커피 머신이 아직 유지 관리 모드가 *아닌* 경우 유지 관리 모드로 설정됩니다.
    
    커피 머신의 콘솔 로그에서 확인 메시지를 살펴봅니다. 

    > [!NOTE]
    > 실제 상황에서 수리 기사가 커피 머신을 오프라인으로 전환하여 필요한 수리를 수행한 후 머신을 다시 온라인으로 전환하는 것처럼, 커피 머신도 클라이언트 코드를 다시 부팅할 때까지 유지 관리 모드로 계속 유지됩니다.

    ![명령 실행](../media/4-commands-maintenance.png)

> [!IMPORTANT]
> 응용 프로그램이 원치 않는 알림/이메일을 보내지 않도록 Node.js 응용 프로그램을 60분 이내로 실행하는 것이 좋습니다. 또한 모듈에서 작업하지 않을 때에는 일일 메시지 할당량이 소진되지 않도록 응용 프로그램을 중지하는 것이 좋습니다.

## <a name="view-the-coffee-machine-in-the-dashboard"></a>대시보드에서 커피 머신 확인

1. **대시보드** 탭으로 이동합니다.

1. **템플릿 편집**을 선택하여 대시보드를 편집합니다.

1. 사이드 메뉴에서 **꺾은선형 차트**를 선택합니다.

1. **차트 구성**의 **제목** 필드에 `Telemetry`를 입력합니다. 이 차트를 통해 원격 분석 데이터를 볼 수 했습니다. 

1. **시간 범위**로 **지난 30분**을 선택합니다. 

1. **측정값** 영역에서 각 측정의 오른쪽에 있는 표시 아이콘을 선택하여 해당 측정을 차트에 표시할 수 있도록 합니다. 

1. **저장**을 선택하여 구성을 저장하고 꺾은선형 차트를 표시합니다. 

    ![대시보드 확인](../media/4-dashboard-a.png)

1. 왼쪽 메뉴에서 **설정 및 속성**을 선택하여 **장치 세부 정보 구성** 패널을 엽니다. 

1. **제목** 필드에 `Device properties`를 입력합니다.

1. **추가/제거**에서 **커피 메이커 최대 온도**, **커피 메이커 최소 온도**, **장치 보증 만료**를 선택한 다음, **확인**을 선택하여 선택을 완료합니다.

1. 대시보드에서 **저장**을 선택하여 새 *장치 속성* 패널을 만듭니다. 

1. **설정 및 속성**을 다시 선택하고 제목으로 `Optimal Temperature`를 입력합니다. **추가/제거**에서 **최적 온도**를 선택합니다.

1. **저장**을 선택하여 작업을 저장하고 대시보드에 새 창을 표시합니다. 

1. **완료**를 선택하여 편집 모드를 종료하고 새 대시보드를 표시합니다. 