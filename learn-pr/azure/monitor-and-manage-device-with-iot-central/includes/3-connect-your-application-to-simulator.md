실제 환경에서는 Azure IoT Central을 실제 장치(여기서는 실제 커피 머신)에 연결하게 됩니다. 하지만이 단위 목적으로 연결한 Node.js 응용 프로그램을 Azure IoT Central 응용 프로그램에는 실제/실시간 커피 컴퓨터를 나타내는입니다. 이 연결의 결과로 커피 머신에서 출발 하 여 원격 분석 모니터링 및 분석을 위해 IoT Central에 전송 됩니다.

![커피 머신](../images/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a>IoT Central에 커피 컴퓨터 추가 
커피 컴퓨터 응용 프로그램에 추가 하려면 사용 합니다 **커피 메이커 연결** 이전 단위에서 만든 장치 템플릿을입니다.

1. 새 장치를 추가 하려면 **Device Explorer** 왼쪽된 탐색 메뉴에서.

    커피 컴퓨터 연결을 시작 하려면 선택 **+ 새로 만들기**, 한 다음 **실제**합니다. 이 과정을 완료 하는 경우 동일한 커피 메이커 연결 된 템플릿을 사용 하 여 만든 장치의 목록이 표시 됩니다.
   
    *   연결 된 커피 메이커를 선택 하면 목록 + 새로 만들기를 실시간에 추가 됩니다. 
    *   연결 된 커피 메이커 (시뮬레이션) 테스트 목적으로 IoT Central으로 자동 생성 됩니다. 

1.  필요에 따라 해당 이름에 "실시간" 라는 단어를 추가 하 여 새로 추가 된 커피 머신을 쉽게 구분할 수 있습니다. 새 장치 이름 바꾸기 장치를 선택 하 고 이름 필드에서 이름을 편집 합니다. 

    ![커피 머신](../images/3-connect-device-a.png) 

    위치를 적어 둡니다 **이 장치 연결** 다음 섹션에서 coffee 컴퓨터 연결에 대 한 합니다. 이제 화면 표시 "누락 된 데이터"에 대 한 커피 머신을에 연결 하지 않은 때문입니다. 연결이 설정 되 면 화면을 채우는 데 실제 원격 분석을 시작 합니다. 
 
## <a name="get-connection-string-for-the-coffee-machine-from-your-application"></a>응용 프로그램에서 커피 머신용 연결 문자열 가져오기
장치에서 실행되는 코드에 실제 커피 머신용 연결 문자열을 포함합니다. 연결 문자열을 사용하면 커피 머신을 Azure IoT Central 응용 프로그램에 안전하게 연결할 수 있습니다. 모든 장치 인스턴스에는 고유 연결 문자열이 있습니다. 응용 프로그램에서 장치 인스턴스용 연결 문자열을 찾는 방법은 다음과 같습니다.

1.  에 연결 된 커피 머신을 real 장치 화면에서 선택 **이 장치 연결**합니다.

1.  **연결** 페이지에서 **기본 연결 문자열**을 복사하고 저장합니다. 장치에서 실행되는 클라이언트 응용 프로그램에서 이 값을 사용합니다.

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기
다음 단계를 응용 프로그램에 추가한 커피 머신을 구현 하는 클라이언트 응용 프로그램을 만드는 방법을 보여줍니다.
1. 설치할 [Node.js](https://nodejs.org/) 버전 4.0.x 또는 나중에 컴퓨터. Node.js는 다양한 운영 체제에 사용할 수 있습니다.

1. 컴퓨터에 coffee-maker라는 폴더를 만듭니다. 명령줄 환경에서 해당 폴더로 이동합니다.

1. Node.js 프로젝트를 초기화하기 위해 다음 명령을 실행합니다.
    ```cmd/sh
    npm init
    ```
    > [!NOTE]
    > Init 스크립트를 프로젝트 속성을 입력 하 라는 메시지를 표시 합니다. 이 연습에서는 기본값을 사용 하는 충분 한 권장 합니다. 
1. 필요한 패키지를 설치하려면 다음 명령을 실행하십시오.
    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. 텍스트 편집기를 사용하여 coffee-maker 폴더에 coffeeMaker.js 파일을 만듭니다.

1. 코드를 복사하여 coffeeMaker.js 파일에 붙여넣고 파일을 **저장**합니다.

    이 단위에 실제 커피 머신을 나타내는 코드를 Node.js로 작성 됩니다. 응용 프로그램을 사용 하 여 연결을 설정 하 여 시작 후에 Azure IoT Central 송신 초기 속성, 설정을 동기화, 유지 관리 및 Brewing에 대 한 두 명의 명령 처리기를 등록 및 마지막 원격 분석을 전송 하는 것에 대 한 타이머를 시작 1 초 마다 정보입니다.

    > [!NOTE]
    > 자리 표시자를 업데이트 `{your device connection string}`합니다. 


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
        
        // Cup timer - every 20 second randomly decide if the cup is present or not
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
            
            // Setup device command callbacks
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
                
                    // Send device properties once on device start up
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

1.  {your device connection string} 자리 표시자는 실제 장치 연결 문자열로 업데이트하세요. 실제 장치를 추가할 때 연결 세부 정보 페이지에서 이 값을 복사했습니다. 

## <a name="run-your-nodejs-application"></a>Node.js 응용 프로그램 실행
```cmd/sh
node coffeeMaker.js
```

## <a name="summary"></a>요약
이 단위에 Azure IoT Central에 커피 컴퓨터를 연결 하 고 모니터링 및 분석에 대 한 데이터를 보내기 시작 합니다. 먼저 IoT Central에서 연결 문자열을 가져온 다음 커피 머신에서 문자열을 구성하여 연결을 설정했습니다.
