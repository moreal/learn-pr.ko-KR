[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="64b91-101">연습에서는 물리적 장치, 즉 IoT를 지원하는 커피 머신에 Azure IoT Central을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-101">In practice, you will connect Azure IoT Central to a physical device, i.e. an IoT enabled coffee machine.</span></span> <span data-ttu-id="64b91-102">여기에서는 Node.js 응용 프로그램이 설치된 장치를 시뮬레이션하고 Azure IoT Central 응용 프로그램에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-102">Here, you'll simualate a device with a Node.js applicatio and connect it to the Azure IoT Central application.</span></span> <span data-ttu-id="64b91-103">시뮬레이션된 커피 머신의 원격 분석 측정값이 IoT Central로 전송되어 모니터링 및 분석에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-103">Telemetry measurements from the simulated coffee machine are sent to IoT Central for monitoring and analysis.</span></span>

![커피 머신을 보여주는 일러스트레이션.](../media/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a><span data-ttu-id="64b91-105">IoT Central에서 커피 머신 추가</span><span class="sxs-lookup"><span data-stu-id="64b91-105">Add the coffee machine in IoT Central</span></span> 
<span data-ttu-id="64b91-106">커피 머신을 응용 프로그램에 추가하려면 이전 모듈에서 만든 **연결된 커피 메이커** 장치 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-106">To add your coffee machine to your application, you use the **Connected Coffee Maker** device template you created in the previous unit.</span></span>

1. <span data-ttu-id="64b91-107">새 장치를 추가하려면 왼쪽 탐색 메뉴에서 **Device Explorer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-107">To add a new device, choose **Device Explorer** in the left navigation menu.</span></span>

    <span data-ttu-id="64b91-108">커피 머신 연결을 시작하려면 **+ 새로 만들기**, **실제**, **만들기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-108">To start connecting your coffee machine, choose **+ New**, **Real**, and then **Create**.</span></span> <span data-ttu-id="64b91-109">과정을 완료하면 동일한 연결된 커피 메이커 템플릿을 사용하여 만든 장치 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-109">When you're finished, you see a list of devices you've created using the same Connected Coffee Maker template.</span></span>
   
    *   <span data-ttu-id="64b91-110">**+ 새로 만들기**, **실제**를 차례로 선택하면 연결된 커피 메이커가 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-110">The Connected Coffee Maker is added to the list when you choose **+ New** and then **Real**.</span></span> 
    *   <span data-ttu-id="64b91-111">IoT Central이 테스트를 목적으로 연결된 커피 메이커(시뮬레이션)를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-111">The Connected Coffee Maker (Simulate) is automatically created by IoT Central for testing purposes.</span></span> 

1.  <span data-ttu-id="64b91-112">필요에 따라 이름에 "실제"라는 단어를 추가하여 새로 추가된 커피 머신을 구별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-112">Optionally, you can differentiate the newly added coffee machine by appending the word “Real” in its name.</span></span> <span data-ttu-id="64b91-113">새 장치 이름을 변경하려면 장치를 선택하고 이름 필드에서 이름을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-113">To rename your new device, choose the device and edit the name in the name field.</span></span> 

    ![커피 머신](../media/3-connect-device-a.png) 

    <span data-ttu-id="64b91-115">그 다음 섹션에서 커피 머신을 연결할 수 있도록 **이 장치 연결**의 위치를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-115">Note the location of **Connect this device** for connecting your coffee machine in the next section.</span></span> <span data-ttu-id="64b91-116">현재는 커피 머신에 연결하지 않았기 때문에 화면에 "데이터 없음"이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-116">For now, the screen displays "Missing Data" because you haven't connected to the coffee machine.</span></span> <span data-ttu-id="64b91-117">연결이 설정되면 실제 원격 분석이 시작되고 화면이 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-117">The real telemetry begins to populate the screen once the connection is made.</span></span> 
 
## <a name="generate-connection-string-for-the-coffee-machine-from-your-application"></a><span data-ttu-id="64b91-118">응용 프로그램에서 커피 머신용 연결 문자열 생성</span><span class="sxs-lookup"><span data-stu-id="64b91-118">Generate connection string for the coffee machine from your application</span></span>
<span data-ttu-id="64b91-119">장치에서 실행되는 코드에 실제 커피 머신용 연결 문자열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-119">You embed the connection string for your real coffee machine in the code that runs on the device.</span></span> <span data-ttu-id="64b91-120">연결 문자열을 사용하면 커피 머신을 Azure IoT Central 응용 프로그램에 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-120">The connection string enables the coffee machine to connect securely to your Azure IoT Central application.</span></span> <span data-ttu-id="64b91-121">모든 장치 인스턴스에는 고유 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-121">Every device instance has a unique connection string.</span></span> <span data-ttu-id="64b91-122">다음 단계에서는 node.js 응용 프로그램을 만들기 위해 연결 문자열을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-122">In the next steps, you generate the connection string as part of creating your node.js application.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="64b91-123">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="64b91-123">Create a Node.js application</span></span>
<span data-ttu-id="64b91-124">다음 단계에서는 응용 프로그램에 추가한 커피 머신을 구현하는 클라이언트 응용 프로그램을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-124">The following steps show you how to create a client application that implements the coffee machine you added to the application.</span></span>

> [!TIP]
> <span data-ttu-id="64b91-125">이 연습에서는 Azure Cloud Shell에 앱을 만들므로 로컬 컴퓨터에 아무것도 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-125">In this exercise, we'll create the app in the Azure Cloud Shell so that you don't have to install anything on your local machine.</span></span> 

1. <span data-ttu-id="64b91-126">Azure Cloud Shell에서 다음 명령을 실행하여 `coffee-maker` 폴더를 만들고 해당 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-126">Execute the following command in the Azure Cloud Shell to create a `coffee-maker` folder and navigate to it:</span></span>

    ```azurecli
    mkdir ~/coffee-maker
    cd ~/coffee-maker
    ```

1. <span data-ttu-id="64b91-127">Cloud Shell의 `coffee-maker` 폴더에서 다음 명령을 실행하여 DPS 키 생성기를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-127">From the `coffee-maker` folder in Cloud Shell, execute the following command to install the DPS key generator:</span></span> 

   ```azurecli
    npm install dps-keygen
   ```
    <span data-ttu-id="64b91-128">이 명령은 로컬 폴더 `coffee-maker`에 dps-keygen 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-128">This command installs the dps-keygen package to our local folder, `coffee-maker`.</span></span> <span data-ttu-id="64b91-129">글로벌 패키지로 설치할 권한이 없으므로 `-g` 옵션은 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-129">We leave out the `-g` option because we don't have permissions to install as a global package.</span></span>

    <!-- TODO: Add more information about the DPS key generator and what it's used for -->
 
1. <span data-ttu-id="64b91-130">Cloud Shell에서 다음 명령을 실행하여 GitHub에서 DPS 연결 문자열 유틸리티를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-130">Execute the following command in the Cloud Shell to download the DPS connection string utility from GitHub:</span></span> 

    ```azurecli
    wget https://github.com/Azure/dps-keygen/blob/master/bin/linux/dps_cstr?raw=true -O dps_cstr 
    ```

    > [!NOTE]
    > <span data-ttu-id="64b91-131">Cloud Shell에서 실행 중이므로 Linux 버전의 **dps_cstr**을 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-131">We downloaded the Linux version of **dps_cstr** because we're running in the Cloud Shell.</span></span>

1. <span data-ttu-id="64b91-132">다음 명령을 실행하여 `dps_cstr`에 실행 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-132">Execute the following command to give `dps_cstr` execute permissions:</span></span>

    ```azurecli
    chmod +x dps_cstr
    ```

    <span data-ttu-id="64b91-133">장치의 연결 문자열을 생성하려면 Azure IoT Central 포털의 세 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-133">To generate a connection string for our device, we need three pieces of information from the Azure IoT Central portal:</span></span>
    - <span data-ttu-id="64b91-134">**범위 ID**</span><span class="sxs-lookup"><span data-stu-id="64b91-134">**Scope ID**</span></span>
    - <span data-ttu-id="64b91-135">**장치 ID**</span><span class="sxs-lookup"><span data-stu-id="64b91-135">**Device ID**</span></span>
    - <span data-ttu-id="64b91-136">**기본 키**</span><span class="sxs-lookup"><span data-stu-id="64b91-136">**Primary Key**</span></span>

1. <span data-ttu-id="64b91-137">IoT Central 포털로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-137">Return to the IoT Central portal.</span></span> <span data-ttu-id="64b91-138">*연결된 커피 메이커 - 실제* 장치의 화면 오른쪽 맨 위에 있는 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-138">On the device screen for the *Connected Coffee Maker - Real* device, select **Connect** in the top right of the screen.</span></span>

1. <span data-ttu-id="64b91-139">장치 연결 대화 상자가 열리면 **범위 ID**, **장치 ID** 및 **기본 키** 값을 어딘가에 저장합니다. 나중에 이 연습에서 사용할 예정이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-139">On the Device Connection dialog that opens, save the values **Scope ID**, **Device ID** and **Primary Key** somewhere, because we'll use them later in this exercise.</span></span> 

1. <span data-ttu-id="64b91-140">Cloud Shell에서 다음 명령을 실행하고 **<scope_id>**, **<device_id>** 및 **<primary_key>** 를 이전 단계에서 저장한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-140">Execute the following command in the Cloud Shell, replacing **<scope_id>**, **<device_id>**, and **<primary_key>** with the values you saved in the last step.</span></span> 

   ```azurecli
   ./dps_cstr [scope_id] [device_id] [primary_key] > connection.txt
   ```
  
    <span data-ttu-id="64b91-141">이 명령은 지정된 값에 따라 연결 문자열을 생성하고 **connection.txt**라는 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-141">This command generates a connection string based on the values you gave it and writes them to a file that we've named **connection.txt**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="64b91-142">`dps_cstr` 명령은 셸의 PATH에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-142">The command `dps_cstr` is not in your PATH in the shell.</span></span> <span data-ttu-id="64b91-143">따라서 `./dps_cstr`을 사용하여 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-143">So, make sure to call it with `./dps_cstr`</span></span>

1. <span data-ttu-id="64b91-144">Cloud Shell에서 다음 명령을 실행하여 통합된 코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-144">Open the integrated code editor in the Cloud Shell by running the following command:</span></span> 

    ```azurecli
    code
    ```
1. <span data-ttu-id="64b91-145">편집기의 **파일** 메뉴에 있는 파일 목록에서 **connection.txt**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-145">Select **connection.txt** from the list of files in the **FILES** menu of the editor.</span></span>

1. <span data-ttu-id="64b91-146">**connection.txt**에 ``HostName=``로 시작되는 연결 문자열이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-146">Verify that **connection.txt** contains a connection string that starts with ``HostName=``.</span></span>

1. <span data-ttu-id="64b91-147">편집기 오른쪽 맨 위에 있는 메뉴(*...*)에서 **편집기 닫기**를 선택하여 편집기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-147">Close the editor by selecting **Close Editor** from the menu (*...*) at the top right of the editor.</span></span> 

1. <span data-ttu-id="64b91-148">Cloud Shell에서 다음 명령을 실행하여 `coffee-maker` 폴더의 Node.js 프로젝트를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-148">Execute the following command in the Cloud Shell to initialize a Node.js project in our `coffee-maker` folder:</span></span>

    ```azurecli
    npm init
    ```
    > [!NOTE]
    > <span data-ttu-id="64b91-149">init 스크립트에 프로젝트 속성을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-149">The init script prompts you to enter project properties.</span></span> <span data-ttu-id="64b91-150">이 연습에서는 ENTER 키를 눌러 모든 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-150">For this exercise, press ENTER to use all default values.</span></span>

1. <span data-ttu-id="64b91-151">필요한 패키지를 설치하려면 `coffee-maker` 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-151">To install the necessary packages, run the following command in our `coffee-maker` folder:</span></span>

    ```azurecli
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="64b91-152">Cloud Shell에서 다음 명령을 실행하여 새로운 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-152">Execute the following command to create a new file in the Cloud Shell:</span></span>

    ```azurecli
    touch coffeeMaker.js
    ```
1. <span data-ttu-id="64b91-153">Cloud Shell의 명령줄에서 다음을 실행하여 통합된 코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-153">Open the integrated code editor by executing the following at the command line in the Cloud Shell:</span></span> 

     ```azurecli
    code
    ```
    
1. <span data-ttu-id="64b91-154">코드 편집기가 열리면 **파일** 목록의 새로 고침 단추를 선택하고 새 파일 **coffeeMaker.js**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-154">When the code editor opens, select the refresh button on the **FILES** list and select our new file **coffeeMaker.js**.</span></span> 

1. <span data-ttu-id="64b91-155">빈 편집기 창에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-155">Copy and paste the following code into the empty editor window:</span></span>

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

    <span data-ttu-id="64b91-156">이 커피 머신은 Node.js로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-156">Our coffee machine is written in Node.js.</span></span> <span data-ttu-id="64b91-157">먼저 Azure IoT Central에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-157">It first connects to Azure IoT Central.</span></span> <span data-ttu-id="64b91-158">그러면 앱에서 Azure IoT Central에 초기 속성을 보내고, 설정을 동기화하고, 유지 관리/커피 끓이기용으로 명령 처리기 2개를 등록하고, 마지막으로 1초마다 원격 분석 정보를 전송하기 위한 타이머를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-158">Then the app sends initial properties to Azure IoT Central, synchronizes settings, registers two command handlers for maintenance and brewing, and finally starts the timer for sending the telemetry information every second.</span></span>

1.  <span data-ttu-id="64b91-159">이 코드 맨 위쪽에 있는 자리 표시자 `{your device connection string}`을 앞서 만들어 **connection.txt**에 저장한 연결 문자열로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-159">Update the placeholder `{your device connection string}` at the top of this code with the connection string you created earlier and saved in **connection.txt**.</span></span> <span data-ttu-id="64b91-160">이 연결 문자열은 `HostName=`으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-160">The connection string begins with `HostName=`.</span></span>

1. <span data-ttu-id="64b91-161">편집기 오른쪽 맨 위에 있는 세 개의 점 `...`을 선택하여 편집기 메뉴를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-161">Select the three dots `...` to the top right of the editor to expand the editor menu.</span></span> <span data-ttu-id="64b91-162">그런 다음, **저장**을 선택하여 편집한 내용을 \`coffeeMaker.js'에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-162">Then select **Save** to save the edits we made to \`coffeeMaker.js'</span></span>

1. <span data-ttu-id="64b91-163">Cloud Shell 창에서 다음 명령을 실행하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-163">Execute the following command in the Cloud Shell window to start the app:</span></span>

    ```azurecli
    node coffeeMaker.js
    ```
1. <span data-ttu-id="64b91-164">*장치가 Azure IoT Central에 성공적으로 연결됨* 메시지 및 *원격 분석 보내기:* 메시지와 함께 Cloud Shell 창에서 앱이 시작되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-164">Verify that the app starts in the Cloud Shell window with the message *Device successfully connected to Azure IoT Central* along with *Telemetry send:* messages.</span></span> <span data-ttu-id="64b91-165">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="64b91-165">Congratulations!</span></span> <span data-ttu-id="64b91-166">앱이 시작되어 IoT Central과 통신 중입니다.</span><span class="sxs-lookup"><span data-stu-id="64b91-166">Your app is up and running and communicating with IoT Central!</span></span>