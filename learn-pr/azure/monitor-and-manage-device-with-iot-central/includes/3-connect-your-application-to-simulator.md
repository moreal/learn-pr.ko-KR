[!include[](../../../includes/azure-sandbox-activate.md)]

연습에서는 물리적 장치, 즉 IoT를 지원하는 커피 머신에 Azure IoT Central을 연결합니다. 여기에서는 Node.js 응용 프로그램이 설치된 장치를 시뮬레이션하고 Azure IoT Central 응용 프로그램에 연결합니다. 시뮬레이션된 커피 머신의 원격 분석 측정값이 IoT Central로 전송되어 모니터링 및 분석에 사용됩니다.

![커피 머신을 보여주는 일러스트레이션.](../media/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a>IoT Central에서 커피 머신 추가 
커피 머신을 응용 프로그램에 추가하려면 이전 모듈에서 만든 **연결된 커피 메이커** 장치 템플릿을 사용합니다.

1. 새 장치를 추가하려면 왼쪽 탐색 메뉴에서 **Device Explorer**를 선택합니다.

    커피 머신 연결을 시작하려면 **+ 새로 만들기**, **실제**, **만들기**를 차례로 선택합니다. 과정을 완료하면 동일한 연결된 커피 메이커 템플릿을 사용하여 만든 장치 목록이 표시됩니다.
   
    *   **+ 새로 만들기**, **실제**를 차례로 선택하면 연결된 커피 메이커가 목록에 추가됩니다. 
    *   IoT Central이 테스트를 목적으로 연결된 커피 메이커(시뮬레이션)를 자동으로 만듭니다. 

1.  필요에 따라 이름에 "실제"라는 단어를 추가하여 새로 추가된 커피 머신을 구별할 수 있습니다. 새 장치 이름을 변경하려면 장치를 선택하고 이름 필드에서 이름을 편집합니다. 

    ![커피 머신](../media/3-connect-device-a.png) 

    그 다음 섹션에서 커피 머신을 연결할 수 있도록 **이 장치 연결**의 위치를 기록해 둡니다. 현재는 커피 머신에 연결하지 않았기 때문에 화면에 "데이터 없음"이 표시됩니다. 연결이 설정되면 실제 원격 분석이 시작되고 화면이 채워집니다. 
 
## <a name="generate-connection-string-for-the-coffee-machine-from-your-application"></a>응용 프로그램에서 커피 머신용 연결 문자열 생성
장치에서 실행되는 코드에 실제 커피 머신용 연결 문자열을 포함합니다. 연결 문자열을 사용하면 커피 머신을 Azure IoT Central 응용 프로그램에 안전하게 연결할 수 있습니다. 모든 장치 인스턴스에는 고유 연결 문자열이 있습니다. 다음 단계에서는 node.js 응용 프로그램을 만들기 위해 연결 문자열을 생성합니다.

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기
다음 단계에서는 응용 프로그램에 추가한 커피 머신을 구현하는 클라이언트 응용 프로그램을 만드는 방법을 보여줍니다.

> [!TIP]
> 이 연습에서는 Azure Cloud Shell에 앱을 만들므로 로컬 컴퓨터에 아무것도 설치할 필요가 없습니다. 

1. Azure Cloud Shell에서 다음 명령을 실행하여 `coffee-maker` 폴더를 만들고 해당 폴더로 이동합니다.

    ```azurecli
    mkdir ~/coffee-maker
    cd ~/coffee-maker
    ```

1. Cloud Shell의 `coffee-maker` 폴더에서 다음 명령을 실행하여 DPS 키 생성기를 설치합니다. 

   ```azurecli
    npm install dps-keygen
   ```
    이 명령은 로컬 폴더 `coffee-maker`에 dps-keygen 패키지를 설치합니다. 글로벌 패키지로 설치할 권한이 없으므로 `-g` 옵션은 유지합니다.

    <!-- TODO: Add more information about the DPS key generator and what it's used for -->
 
1. Cloud Shell에서 다음 명령을 실행하여 GitHub에서 DPS 연결 문자열 유틸리티를 다운로드합니다. 

    ```azurecli
    wget https://github.com/Azure/dps-keygen/blob/master/bin/linux/dps_cstr?raw=true -O dps_cstr 
    ```

    > [!NOTE]
    > Cloud Shell에서 실행 중이므로 Linux 버전의 **dps_cstr**을 다운로드했습니다.

1. 다음 명령을 실행하여 `dps_cstr`에 실행 권한을 부여합니다.

    ```azurecli
    chmod +x dps_cstr
    ```

    장치의 연결 문자열을 생성하려면 Azure IoT Central 포털의 세 가지 정보가 필요합니다.
    - **범위 ID**
    - **장치 ID**
    - **기본 키**

1. IoT Central 포털로 돌아갑니다. *연결된 커피 메이커 - 실제* 장치의 화면 오른쪽 맨 위에 있는 **연결**을 선택합니다.

1. 장치 연결 대화 상자가 열리면 **범위 ID**, **장치 ID** 및 **기본 키** 값을 어딘가에 저장합니다. 나중에 이 연습에서 사용할 예정이기 때문입니다. 

1. Cloud Shell에서 다음 명령을 실행하고 **<scope_id>**, **<device_id>** 및 **<primary_key>** 를 이전 단계에서 저장한 값으로 바꿉니다. 

   ```azurecli
   ./dps_cstr [scope_id] [device_id] [primary_key] > connection.txt
   ```
  
    이 명령은 지정된 값에 따라 연결 문자열을 생성하고 **connection.txt**라는 파일에 기록합니다.

    > [!IMPORTANT]
    > `dps_cstr` 명령은 셸의 PATH에 있지 않습니다. 따라서 `./dps_cstr`을 사용하여 호출해야 합니다.

1. Cloud Shell에서 다음 명령을 실행하여 통합된 코드 편집기를 엽니다. 

    ```azurecli
    code
    ```
1. 편집기의 **파일** 메뉴에 있는 파일 목록에서 **connection.txt**를 선택합니다.

1. **connection.txt**에 ``HostName=``로 시작되는 연결 문자열이 포함되어 있는지 확인합니다.

1. 편집기 오른쪽 맨 위에 있는 메뉴(*...*)에서 **편집기 닫기**를 선택하여 편집기를 닫습니다. 

1. Cloud Shell에서 다음 명령을 실행하여 `coffee-maker` 폴더의 Node.js 프로젝트를 초기화합니다.

    ```azurecli
    npm init
    ```
    > [!NOTE]
    > init 스크립트에 프로젝트 속성을 입력하라는 메시지가 표시됩니다. 이 연습에서는 ENTER 키를 눌러 모든 기본값을 사용합니다.

1. 필요한 패키지를 설치하려면 `coffee-maker` 폴더에서 다음 명령을 실행합니다.

    ```azurecli
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Cloud Shell에서 다음 명령을 실행하여 새로운 파일을 만듭니다.

    ```azurecli
    touch coffeeMaker.js
    ```
1. Cloud Shell의 명령줄에서 다음을 실행하여 통합된 코드 편집기를 엽니다. 

     ```azurecli
    code
    ```
    
1. 코드 편집기가 열리면 **파일** 목록의 새로 고침 단추를 선택하고 새 파일 **coffeeMaker.js**를 선택합니다. 

1. 빈 편집기 창에 다음 코드를 복사하여 붙여넣습니다.

    ```js
    "use strict";

    // Use the Azure IoT device SDK for devices that connect to Azure IoT Central
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;

    // Connection string (TODO: CHANGE HERE)
    const connectionString = `{your device connection string}`;

    // Global variables
    var client = clientFromConnectionString(connectionString);
    var optimalTemperature = 96;
    var cupState = true;
    var brewingState = false;
    var cupTimer = 20;
    var brewingTimer = 0;
    var maintenanceState = false;
    var warrantyState = Math.random() < 0.5?0:1;

    // Helper function to produce nice numbers (##.#)
    function niceNumber(value) 
    {
        var number = (Math.round(value * 10.0)).toString();
        return number.substr(0, 2) + '.' + number.substr(2, 1);
    }

    // Send device simulated telemetry measurements
    function sendTelemetry() 
    {   
        // Simulate the telemetry values
        var temperature = optimalTemperature + (Math.random() * 4) - 2;
        var humidity = 20 + (Math.random() * 80);
        
        // Cup timer - every 20 seconds randomly decide if the cup is present or not
        cupTimer--;
        
        if (cupTimer == 0)
        {
            cupTimer = 20;
            cupState = Math.random() < 0.5?false:true;
        }
        
        // Brewing timer
        if (brewingTimer > 0)
        {
            brewingTimer--;
            
            // Finished brewing
            if (brewingTimer == 0)
            {
                brewingState = false;
            }
        }
    
        // Create the data JSON package
        var data = JSON.stringify(
        { 
            waterTemperature: temperature, 
            airHumidity: humidity, 
        });

        // Create the message with the above defined data
        var message = new Message(data);
        
        // Set the state flags
        message.properties.add('stateCupDetected', cupState);
        message.properties.add('stateBrewing', brewingState);
        
        // Show the information in console
        var infoTemperature = niceNumber(temperature);
        var infoHumidity = niceNumber(humidity);
        var infoCup = cupState ? 'Y' :'N';
        var infoBrewing = brewingState ? 'Y':'N';
        var infoMaintenance = maintenanceState ? 'Y':'N';
        
        console.log('Telemetry send: Temperature: ' + infoTemperature + 
                    ' Humidity: ' + infoHumidity + '%' + 
                    ' Cup Detected: ' + infoCup + 
                    ' Brewing: ' + infoBrewing + 
                    ' Maintenance Mode: ' + infoMaintenance);
        
        // Send the message
        client.sendEvent(message, function (errorMessage) 
        {
            // Error
            if (errorMessage) 
            {
                console.log('Failed to send message to Azure IoT Hub: ${err.toString()}');
            }
        });
    }

    // Send device properties
    function sendDeviceProperties(deviceTwin) 
    {
        var properties = 
        {
            propertyWarrantyExpired: warrantyState
        };
        
        console.log(' * Property - Warranty State: ' + warrantyState.toString());
        
        deviceTwin.properties.reported.update(properties, (errorMessage) => 
            console.log(` * Sent device properties ` + (errorMessage ? `Error: ${errorMessage.toString()}` : `(success)`)));
    }

    // Optimal temperature setting
    var settings = 
    {
        'setTemperature': (newValue, callback) => 
        {
            setTimeout(() => 
            {
                optimalTemperature = newValue;
                callback(optimalTemperature, 'completed');
            }, 1000);
        }
    };

    // Handle settings changes that come from Azure IoT Central via the device twin.
    function handleSettings(deviceTwin) 
    {
        deviceTwin.on('properties.desired', function (desiredChange) 
        {
            // Iterate all settings looking for the defined one
            for (let setting in desiredChange) 
            {
                // Setting we defined
                if (settings[setting]) 
                {
                    // Console info
                    console.log(` * Received setting: ${setting}: ${desiredChange[setting].value}`);
                    
                    // Update 
                    settings[setting](desiredChange[setting].value, (newValue, status, message) => 
                    {
                        var patch = 
                        {
                            [setting]: 
                            {
                                value: newValue,
                                status: status,
                                desiredVersion: desiredChange.$version,
                                message: message
                            }
                        }
                        deviceTwin.properties.reported.update(patch, (err) => console.log(` * Sent setting update for ${setting} ` +
                        (err ? `error: ${err.toString()}` : `(success)`)));
                    });
                }
            }
        });
    }

    // Maintenance mode command
    function onCommandMaintenance(request, response) 
    {
        // Display console info
        console.log(' * Maintenance command received');

        // Console warning
        if (maintenanceState)
        {
            console.log(' - Warning: The device is already in the maintenance mode.');
        }
        
        // Set state
        maintenanceState = true;

        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    function onCommandStartBrewing(request, response) 
    {
        // Display console info
        console.log(' * Brewing command received');

        // Console warning
        if (brewingState == true)
        {
            console.log(' - Warning: The device is already brewing.');
        }
        
        if (cupState == false)
        {
            console.log(' - Warning: The cup has not been detected.');
        }
        
        if (maintenanceState == true)
        {
            console.log(' - Warning: The device is in maintenance state.');
        }
        
        // Set state - brew for 30 seconds
        if ((cupState == true) && (brewingState == false) && (maintenanceState == false))
        {
            brewingState = true;
            brewingTimer = 30;
        }
        
        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    // Handle device connection to Azure IoT Central
    var connectCallback = (errorMessage) => 
    {
        // Connection error
        if (errorMessage) 
        {
            console.log(`Device could not connect to Azure IoT Central: ${errorMessage.toString()}`);
        } 
        // Successfully connected
        else 
        {
            // Notify the user
            console.log('Device successfully connected to Azure IoT Central');

            // Send telemetry measurements to Azure IoT Central every 1 second.
            setInterval(sendTelemetry, 1000);
            
            // Set up device command callbacks
            client.onDeviceMethod('cmdSetMaintenance', onCommandMaintenance);
            client.onDeviceMethod('cmdStartBrewing', onCommandStartBrewing);
            
            // Get device twin from Azure IoT Central
            client.getTwin((errorMessage, deviceTwin) => 
            {
                // Failed to retrieve device twin
                if (errorMessage) 
                {
                    console.log(`Error getting device twin: ${errorMessage.toString()}`);
                } 
                // Success
                else 
                {
                    // Notify the user
                    console.log('Device Twin successfully retrieved from Azure IoT Central');
                
                    // Send device properties once on device startup
                    sendDeviceProperties(deviceTwin);
                    
                    // Apply device settings and handle changes to device settings
                    handleSettings(deviceTwin);
                }
            });
        }
    };

    // Start the device (connect it to Azure IoT Central)
    client.open(connectCallback);

    ```

    이 커피 머신은 Node.js로 작성됩니다. 먼저 Azure IoT Central에 연결합니다. 그러면 앱에서 Azure IoT Central에 초기 속성을 보내고, 설정을 동기화하고, 유지 관리/커피 끓이기용으로 명령 처리기 2개를 등록하고, 마지막으로 1초마다 원격 분석 정보를 전송하기 위한 타이머를 시작합니다.

1.  이 코드 맨 위쪽에 있는 자리 표시자 `{your device connection string}`을 앞서 만들어 **connection.txt**에 저장한 연결 문자열로 업데이트합니다. 이 연결 문자열은 `HostName=`으로 시작됩니다.

1. 편집기 오른쪽 맨 위에 있는 세 개의 점 `...`을 선택하여 편집기 메뉴를 확장합니다. 그런 다음, **저장**을 선택하여 편집한 내용을 `coffeeMaker.js'에 저장합니다.

1. Cloud Shell 창에서 다음 명령을 실행하여 앱을 시작합니다.

    ```azurecli
    node coffeeMaker.js
    ```
1. *장치가 Azure IoT Central에 성공적으로 연결됨* 메시지 및 *원격 분석 보내기:* 메시지와 함께 Cloud Shell 창에서 앱이 시작되는지 확인합니다. 축하합니다! 앱이 시작되어 IoT Central과 통신 중입니다.