---
title: Azure IoT Hub direct methods (Node) | Microsoft Docs
description: How to use Azure IoT Hub direct methods. You use the Azure IoT SDKs for Node.js to implement a simulated device app that includes a direct method and a service app that invokes the direct method.
services: iot-hub
documentationcenter: ''
author: nberdy
manager: timlt
editor: ''
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 728e365e30b21de13ce92fb562511bac0a29938b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549820"
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="420b0-104">Use direct methods on your IoT device with Node.js</span><span class="sxs-lookup"><span data-stu-id="420b0-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="420b0-105">At the end of this tutorial, you have two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="420b0-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="420b0-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span><span class="sxs-lookup"><span data-stu-id="420b0-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="420b0-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span><span class="sxs-lookup"><span data-stu-id="420b0-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="420b0-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span><span class="sxs-lookup"><span data-stu-id="420b0-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="420b0-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="420b0-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="420b0-110">Node.js version 0.10.x or later.</span><span class="sxs-lookup"><span data-stu-id="420b0-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="420b0-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="420b0-111">An active Azure account.</span></span> <span data-ttu-id="420b0-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="420b0-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="420b0-113">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="420b0-113">Create a simulated device app</span></span>
<span data-ttu-id="420b0-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span><span class="sxs-lookup"><span data-stu-id="420b0-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="420b0-115">Create a new empty folder called **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="420b0-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="420b0-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="420b0-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="420b0-117">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="420b0-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="420b0-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="420b0-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="420b0-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span><span class="sxs-lookup"><span data-stu-id="420b0-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="420b0-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="420b0-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="420b0-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span><span class="sxs-lookup"><span data-stu-id="420b0-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="420b0-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="420b0-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="420b0-123">Add the following function to implement the method on the device:</span><span class="sxs-lookup"><span data-stu-id="420b0-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="420b0-124">Open the connection to your IoT hub and start initialize the method listener:</span><span class="sxs-lookup"><span data-stu-id="420b0-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="420b0-125">Save and close the **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="420b0-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="420b0-126">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="420b0-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="420b0-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="420b0-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="420b0-128">Call a method on a device</span><span class="sxs-lookup"><span data-stu-id="420b0-128">Call a method on a device</span></span>
<span data-ttu-id="420b0-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span><span class="sxs-lookup"><span data-stu-id="420b0-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="420b0-130">Create a new empty folder called **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="420b0-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="420b0-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="420b0-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="420b0-132">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="420b0-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="420b0-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span><span class="sxs-lookup"><span data-stu-id="420b0-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="420b0-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span><span class="sxs-lookup"><span data-stu-id="420b0-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="420b0-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="420b0-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="420b0-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span><span class="sxs-lookup"><span data-stu-id="420b0-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="420b0-137">Create the client to open the connection to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="420b0-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="420b0-138">Add the following function to invoke the device method and print the device response to the console:</span><span class="sxs-lookup"><span data-stu-id="420b0-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="420b0-139">Save and close the **CallMethodOnDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="420b0-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="420b0-140">Run the apps</span><span class="sxs-lookup"><span data-stu-id="420b0-140">Run the apps</span></span>
<span data-ttu-id="420b0-141">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="420b0-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="420b0-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="420b0-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="420b0-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="420b0-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="420b0-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span><span class="sxs-lookup"><span data-stu-id="420b0-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="420b0-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="420b0-145">Next steps</span></span>
<span data-ttu-id="420b0-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="420b0-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="420b0-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span><span class="sxs-lookup"><span data-stu-id="420b0-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="420b0-148">You also created an app that invokes methods on the device and displays the response from the device.</span><span class="sxs-lookup"><span data-stu-id="420b0-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="420b0-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="420b0-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="420b0-150">[Get started with IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="420b0-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="420b0-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="420b0-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="420b0-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="420b0-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Get started with IoT Hub]: iot-hub-node-node-getstarted.md



