<span data-ttu-id="011a5-101">실제 환경에서는 Azure IoT Central을 실제 장치(여기서는 실제 커피 머신)에 연결하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-101">In real life, it's assumed that you will connect Azure IoT Central to a real device or in this case, a real coffee machine.</span></span> <span data-ttu-id="011a5-102">하지만 이 모듈에서는 실제 커피 머신을 나타내는 일반 Node.js 응용 프로그램에 Azure IoT Central 응용 프로그램을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-102">But for the purpose of this module, you connect the Azure IoT Central application to a generic Node.js application representing a physical coffee machine.</span></span> <span data-ttu-id="011a5-103">이와 같이 연결하면 커피 머신의 센서 관련 데이터가 모니터링 및 분석을 위해 IoT Central로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-103">As a result of this connection, sensory data from the coffee machine is sent to IoT Central for monitoring and analysis.</span></span>

![커피 머신](../images/3-coffee-machine.png) 

## <a name="add-the-simulated-coffee-machine-in-iot-central"></a><span data-ttu-id="011a5-105">IoT Central에 시뮬레이션된 커피 머신 추가</span><span class="sxs-lookup"><span data-stu-id="011a5-105">Add the simulated coffee machine in IoT Central</span></span> 
<span data-ttu-id="011a5-106">시뮬레이션된 커피 머신을 응용 프로그램에 추가하려면 이전 모듈에서 만든 **연결된 커피 메이커** 장치 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-106">To add your simulated coffee machine to your application, you use the **Connected Coffee Maker** device template you created in the previous module.</span></span>

1. <span data-ttu-id="011a5-107">운영자로서 새 장치를 추가하려면 왼쪽 탐색 메뉴에서 **Device Explorer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-107">To add a new device as an operator choose **Device Explorer** in the left navigation menu:</span></span>

    <span data-ttu-id="011a5-108">**Device Explorer**에는 작성기가 장치 템플릿을 만들 때 자동으로 생성된 장치 시뮬레이터 및 **연결된 커피 머신** 장치 템플릿이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-108">The **Device Explorer** shows the **Connected Coffee Maker** device template and the device simulator that was automatically created when the builder created the device template.</span></span>

1.  <span data-ttu-id="011a5-109">시뮬레이션된 커피 머신 연결을 시작하려면 **새로 만들기**, **실제**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-109">To start connecting your simulated coffee machine, choose **New**, then **Real**.</span></span>

1.  <span data-ttu-id="011a5-110">필요에 따라 장치 이름을 선택하고 값을 편집하여 새 장치 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-110">Optionally, you can rename your new device by choosing the device name and editing the value:</span></span>
 
## <a name="get-connection-string-for-the-coffee-machine-from-your-application"></a><span data-ttu-id="011a5-111">응용 프로그램에서 커피 머신용 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="011a5-111">Get connection string for the coffee machine from your application</span></span>
<span data-ttu-id="011a5-112">장치에서 실행되는 코드에 실제 커피 머신용 연결 문자열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-112">You embed the connection string for your real coffee machine in the code that runs on the device.</span></span> <span data-ttu-id="011a5-113">연결 문자열을 사용하면 커피 머신을 Azure IoT Central 응용 프로그램에 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-113">The connection string enables the coffee machine to connect securely to your Azure IoT Central application.</span></span> <span data-ttu-id="011a5-114">모든 장치 인스턴스에는 고유 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-114">Every device instance has a unique connection string.</span></span> <span data-ttu-id="011a5-115">응용 프로그램에서 장치 인스턴스용 연결 문자열을 찾는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-115">Here is how to find the connection string for a device instance in your application:</span></span>

1.  <span data-ttu-id="011a5-116">실제 연결된 커피 머신의 장치 화면에서 **이 장치 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-116">On the Device screen for your real connected coffee machine, choose **Connect this device**.</span></span>

1.  <span data-ttu-id="011a5-117">**연결** 페이지에서 **기본 연결 문자열**을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-117">On the **Connect** page, copy the **Primary connection string**, and save it.</span></span> <span data-ttu-id="011a5-118">장치에서 실행되는 클라이언트 응용 프로그램에서 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-118">You use this value in the client application that runs on the device.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="011a5-119">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="011a5-119">Create a Node.js application</span></span>
<span data-ttu-id="011a5-120">다음 단계에서는 응용 프로그램에 추가한 커피 머신을 구현하는 클라이언트 응용 프로그램을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-120">The following steps show how to create a client application that implements the coffee machine you added to the application.</span></span>
1. <span data-ttu-id="011a5-121">컴퓨터에 [Node.js](https://nodejs.org/) 버전 4.0.x 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-121">Install [Node.js](https://nodejs.org/) version 4.0.x or later in your machine.</span></span> <span data-ttu-id="011a5-122">Node.js는 다양한 운영 체제에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-122">Node.js is available for a wide variety of operating systems.</span></span>

1. <span data-ttu-id="011a5-123">컴퓨터에 coffee-maker라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-123">Create a folder called coffee-maker on your machine.</span></span> <span data-ttu-id="011a5-124">명령줄 환경에서 해당 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-124">Navigate to that folder in your command-line environment.</span></span>

1. <span data-ttu-id="011a5-125">Node.js 프로젝트를 초기화하기 위해 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-125">To initialize your Node.js project, run the following commands:</span></span>
    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="011a5-126">필요한 패키지를 설치하려면 다음 명령을 실행하십시오.</span><span class="sxs-lookup"><span data-stu-id="011a5-126">To install the necessary packages, run the following command:</span></span>
    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="011a5-127">텍스트 편집기를 사용하여 coffee-maker 폴더에 coffeeMaker.js 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-127">Using a text editor, create a file called coffeeMaker.js in the coffee-maker folder.</span></span>

1. <span data-ttu-id="011a5-128">코드를 복사하여 coffeeMaker.js 파일에 붙여넣고 파일을 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-128">Copy and paste the code into your coffeeMaker.js file and **Save**.</span></span>

    <span data-ttu-id="011a5-129">이 모듈에서 실제 커피 머신을 나타내는 코드는 Node.js로 작성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-129">The code representing the real coffee machine in this module is written in Node.js.</span></span> <span data-ttu-id="011a5-130">먼저 응용 프로그램과의 연결을 설정한 다음 Azure IoT Central에 초기 속성을 보내고, 설정을 동기화하고, 유지 관리/커피 끓이기용으로 명령 처리기 2개를 등록하고, 마지막으로 1초마다 원격 분석 정보를 전송하기 위한 타이머를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-130">You begin by establishing connection with the application, send initial properties to Azure IoT Central, synchronize the settings, register two command handlers for Maintenance and Brewing, and finally start the timer for sending the telemetry information every second.</span></span>

    > [!NOTE]
    > <span data-ttu-id="011a5-131">`{your device connection string}` 자리 표시자를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-131">Remeber to update the placeholder `{your device connection string}`.</span></span> 


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
    var deviceMinTemperature = 88 + (Math.random() * 4);
    var deviceMaxTemperature = 98 + (Math.random() * 2);
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

1.  <span data-ttu-id="011a5-132">{your device connection string} 자리 표시자는 실제 장치 연결 문자열로 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="011a5-132">Update the placeholder {your device connection string} with your device connection string.</span></span> <span data-ttu-id="011a5-133">실제 장치를 추가할 때 연결 세부 정보 페이지에서 이 값을 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-133">You copied this value from the connection details page when you added your real device.</span></span> 

## <a name="run-your-nodejs-application"></a><span data-ttu-id="011a5-134">Node.js 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="011a5-134">Run your Node.js application</span></span>
```cmd/sh
node coffeeMaker.js
```

## <a name="summary"></a><span data-ttu-id="011a5-135">요약</span><span class="sxs-lookup"><span data-stu-id="011a5-135">Summary</span></span>
<span data-ttu-id="011a5-136">이 모듈에서는 시뮬레이션된 커피 머신을 Azure IoT Central에 연결하고 모니터링과 분석을 위한 데이터 전송을 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-136">In this module, you connected your simulated coffee machine to Azure IoT Central and began sending data for monitoring and analysis.</span></span> <span data-ttu-id="011a5-137">먼저 IoT Central에서 연결 문자열을 가져온 다음 커피 머신에서 문자열을 구성하여 연결을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="011a5-137">You achieved the connectivity by first acquiring a connection string from IoT Central, followed by configuring the string in the coffee machine.</span></span>
