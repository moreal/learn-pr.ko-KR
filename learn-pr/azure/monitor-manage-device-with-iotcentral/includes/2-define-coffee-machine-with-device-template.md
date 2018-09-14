Azure IoT Central에서는 장치(여기서는 커피 머신)의 동작과 기능을 정의하는 장치 템플릿에서 장치가 응용 프로그램과 교환할 수 있는 데이터가 지정됩니다. 장치 템플릿을 만들 때는 템플릿에서 시뮬레이션된 장치가 생성됩니다. 시뮬레이션된 장치는 원격 분석을 생성하여 물리적 장치에 연결하기 전에 응용 프로그램의 동작을 테스트할 수 있습니다. 다음 모듈의 후반부에서는 실제 커피 머신을 나타내는 일반 Node.js 응용 프로그램을 연결합니다. 

이 모듈에서는 다음 기능과 동작을 지정하는 커피 머신용 장치 템플릿을 만듭니다.
* 측정값 
    * 원격 분석: 공기 습도, 물 온도
    * 상태: 끓이는 중/끓이는 중 아님, 컵이 검색됨/컵이 검색되지 않음
* 설정: 최적 온도
* 속성: 커피 머신의 최소/최대 온도, 장치 보증 만료
* 명령: 유지 관리 모드 설정, 끓이기 시작


## <a name="create-a-device-template-for-the-coffee-maker"></a>커피 메이커용 장치 템플릿 만들기
장치(여기서는 커피 메이커)의 동작과 기능을 정의하는 장치 템플릿을 만듭니다.

1. 홈페이지로 이동한 후 장치 템플릿 만들기를 선택합니다.
![장치 템플릿 만들기](../images/2-device-template-a1.png)

1. 사용자 지정 장치 템플릿의 이름을 입력합니다. 이 모듈에서는 연결된 커피 메이커 등의 이름을 입력합니다.
![장치 템플릿 만들기](../images/2-device-template-a2.png)
 
1. 커피 머신의 동작과 기능을 정의할 커피메이커용 새 장치 템플릿을 만들었습니다. 

## <a name="define-telemetry-measurement-temperature-and-humidity"></a>원격 분석 측정 온도 및 습도 정의
1.  **연결된 커피 메이커** 장치 템플릿에서 원격 분석을 정의할 **측정값** 페이지가 표시되어 있는지 확인합니다. 정의하는 각 장치 템플릿에는 다음 작업을 위한 별도 페이지가 있습니다.
    * 장치에서 보내는 원격 분석, 이벤트 및 상태와 같은 측정값 지정
    * 장치를 제어하는 데 사용하는 설정 정의
    * 장치 관련 정보를 기록하는 데 사용되는 속성과 장치에서 전송하는 장치 속성 정의
    * 장치와 연결된 규칙 정의
    * 장치 관련 정보를 확인할 수 있도록 장치 대시보드 사용자 지정 

1.  온도 원격 분석 측정을 추가하려면 **새 측정**을 선택합니다. 그런 다음 측정 유형으로 **원격 분석**을 선택합니다. ![장치 템플릿 만들기](../images/2-device-template-c.png)

1.  장치 템플릿에 대해 정의하는 각 유형의 원격 분석은 다음과 같은 구성 옵션을 포함합니다.
    * 옵션 표시
    * 원격 분석의 세부 정보
    * 시뮬레이션 매개 변수

    온도 및 습도 원격 분석을 구성하려면 다음 표의 정보를 사용합니다.
    
    |표시 이름|필드 이름|단위|최소값|최대값|소수 자릿수|
    |---|---|---|---|---|---|
    |물 온도|waterTemperature|섭씨|90|98|1|
    |공기 습도|airHumidity|%|20|100|0|
   
    원격 분석 표시용 색을 선택할 수도 있습니다. 원격 분석 정의를 저장하려면 **저장**을 선택합니다. ![장치 템플릿 만들기](../images/2-device-template-d.png)

    테이블에 표시된 필드 이름을 장치 템플릿에 똑같이 입력합니다. 필드 이름이 일치하지 않으면 응용 프로그램에서 원격 분석 데이터를 표시할 수 없습니다. 설정 및 속성 정보를 입력할 때도 동일한 작업을 수행합니다. 

## <a name="define-state-measurement-for-brewingnot-brewing-cup-detectedcup-not-detected"></a>끓이는 중/끓이는 중 아님, 컵이 검색됨/컵이 검색되지 않음에 대해 상태 측정을 정의합니다.
**새 측정**을 선택하여 **측정값** 페이지에서 다음 상태를 추가합니다. 그런 다음, 측정 유형으로 **상태**를 선택합니다.
    
|표시 이름|필드 이름|값 1|표시 이름|값 2|표시 이름|
|---|---|---|---|---|---|
|끓이는 중|stateBrewing|true|끓이는 중 아님|false|끓이는 중 아님|
|컵이 검색됨|stateCupDetected|true|컵이 검색되지 않음|false|컵이 검색되지 않음|

![장치 템플릿 만들기](../images/2-device-template-f.png)

장치 템플릿을 만들 때는 템플릿에서 시뮬레이션된 장치가 생성됩니다. 시뮬레이션된 장치는 원격 분석을 생성하여 물리적 장치에 연결하기 전에 응용 프로그램의 동작을 테스트할 수 있습니다.
![장치 템플릿 만들기](../images/2-device-template-m.png)

## <a name="use-settings-to-set-the-optimal-temperature-of-the-coffee-machine"></a>설정을 사용하여 커피 머신의 최적 온도 설정
설정으로 이동합니다. **디자인 모드**를 설정합니다. **설정** 페이지에서 다음 숫자 설정을 추가합니다.

|표시 이름|필드 이름|단위|10진수|최소값|최대값|초기 값|
|---|---|---|---|---|---|---|---|
|최적 온도|setTemperature|섭씨|1|92|99|95|

![장치 템플릿 만들기](../images/2-device-template-q.png)

## <a name="use-properties-to-store-warranty-info-and-water-temperature-range"></a>속성을 사용하여 보증 정보 및 물 온도 범위 저장
먼저 **디자인 모드**를 설정하여 **속성** 페이지에서 다음 **숫자** 속성을 추가합니다.
|표시 이름|필드 이름|단위|소수 자릿수|최소값|최대값|초기 값
|---|---|---|---|---|---|---|
|커피 메이커 최소 온도|propertyMinTemperature|섭씨|1|88|92|90|    
|커피 메이커 최대 온도|propertyMaxTemperature|섭씨|1|96|99|98| 

![장치 템플릿 만들기](../images/2-device-template-n.png)

**속성** 페이지에서 다음 **장치** 속성을 추가합니다.

|표시 이름|필드 이름|데이터 형식|
|---|---|---|
|장치 보증 만료|propertyWarrantyExpired|숫자|
![장치 템플릿 만들기](../images/2-device-template-u.png)

> [!NOTE]
> 장치(여기서는 커피 머신)에서 장치 속성을 전송합니다. Azure IoT Central에 커피 머신을 연결하고 나면 장치 속성 보증이 응용 프로그램으로 전송되어 장치 보증 만료 필드에 표시됩니다. 

## <a name="use-commands-to-set-maintenance-mode-and-start-brewing"></a>명령을 사용하여 유지 관리 모드 설정 및 끓이기 시작

먼저 **디자인 모드**를 설정하여 **명령** 페이지에서 다음 명령을 추가합니다.
|표시 이름|필드 이름|입력 필드|데이터 형식|
|---|---|---|---|---|---|---|
|유지 관리 설정|cmdSetMaintance|30|텍스트| 
|끓이기 시작|cmdStartBrewing|30|텍스트|

![장치 템플릿 만들기](../images/2-device-template-s.png)


## <a name="summary"></a>요약

이 모듈에서는 장치 템플릿을 사용해 새 장치 유형(커피 머신)을 만들고 커피 머신이 응용 프로그램과 교환할 수 있는 데이터를 지정했습니다. 그리고 온도/습도 등의 원격 분석과 커피를 끓이는 중인지 여부 등의 상태도 정의했습니다. 또한 설정, 속성 및 명령을 구성하여 커피 머신의 동작과 기능을 추가로 정의했습니다. 
