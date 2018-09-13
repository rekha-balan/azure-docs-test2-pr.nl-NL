---
title: Get started with Azure IoT Hub (Node) | Microsoft Docs
description: How to send device-to-cloud messages from a device to an Azure IoT hub using the Azure IoT SDKs for Node.js. You create a simulated device app to send messages, a service app to register your device in the identity registry, and a service app to read the device-to-cloud messages from the IoT hub.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4da04bbde48cab2924c37ffbebaa70d7c719b1aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556560"
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="93731-104">Connect your simulated device to your IoT hub using Node</span><span class="sxs-lookup"><span data-stu-id="93731-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="93731-105">At the end of this tutorial, you have three Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="93731-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="93731-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="93731-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="93731-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="93731-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="93731-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="93731-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="93731-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span><span class="sxs-lookup"><span data-stu-id="93731-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="93731-110">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="93731-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="93731-111">Node.js version 0.10.x or later.</span><span class="sxs-lookup"><span data-stu-id="93731-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="93731-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="93731-112">An active Azure account.</span></span> <span data-ttu-id="93731-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="93731-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="93731-114">You have now created your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-114">You have now created your IoT hub.</span></span> <span data-ttu-id="93731-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="93731-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="93731-116">Create a device identity</span><span class="sxs-lookup"><span data-stu-id="93731-116">Create a device identity</span></span>
<span data-ttu-id="93731-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="93731-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="93731-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="93731-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="93731-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="93731-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="93731-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="93731-121">Create a new empty folder called **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="93731-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="93731-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="93731-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="93731-123">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="93731-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="93731-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span><span class="sxs-lookup"><span data-stu-id="93731-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="93731-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span><span class="sxs-lookup"><span data-stu-id="93731-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="93731-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span><span class="sxs-lookup"><span data-stu-id="93731-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="93731-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span><span class="sxs-lookup"><span data-stu-id="93731-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="93731-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="93731-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span><span class="sxs-lookup"><span data-stu-id="93731-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
    ```
    var device = new iothub.Device(null);
    device.deviceId = 'myFirstNodeDevice';
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
7. <span data-ttu-id="93731-130">Save and close **CreateDeviceIdentity.js** file.</span><span class="sxs-lookup"><span data-stu-id="93731-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="93731-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span><span class="sxs-lookup"><span data-stu-id="93731-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="93731-132">Make a note of the **Device ID** and **Device key**.</span><span class="sxs-lookup"><span data-stu-id="93731-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="93731-133">You need these values later when you create an application that connects to IoT Hub as a device.</span><span class="sxs-lookup"><span data-stu-id="93731-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="93731-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="93731-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span><span class="sxs-lookup"><span data-stu-id="93731-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="93731-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span><span class="sxs-lookup"><span data-stu-id="93731-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="93731-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="93731-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="93731-138">Receive device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="93731-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="93731-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="93731-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="93731-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="93731-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="93731-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span><span class="sxs-lookup"><span data-stu-id="93731-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="93731-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span><span class="sxs-lookup"><span data-stu-id="93731-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="93731-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span><span class="sxs-lookup"><span data-stu-id="93731-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="93731-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span><span class="sxs-lookup"><span data-stu-id="93731-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="93731-145">Create an empty folder called **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="93731-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="93731-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="93731-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="93731-147">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="93731-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="93731-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span><span class="sxs-lookup"><span data-stu-id="93731-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="93731-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span><span class="sxs-lookup"><span data-stu-id="93731-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="93731-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span><span class="sxs-lookup"><span data-stu-id="93731-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="93731-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span><span class="sxs-lookup"><span data-stu-id="93731-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="93731-152">Add the following two functions that print output to the console:</span><span class="sxs-lookup"><span data-stu-id="93731-152">Add the following two functions that print output to the console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="93731-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span><span class="sxs-lookup"><span data-stu-id="93731-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="93731-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span><span class="sxs-lookup"><span data-stu-id="93731-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="93731-155">This filter is useful in a test environment so you see just the current set of messages.</span><span class="sxs-lookup"><span data-stu-id="93731-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="93731-156">In a production environment, your code should make sure that it processes all the messages.</span><span class="sxs-lookup"><span data-stu-id="93731-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="93731-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span><span class="sxs-lookup"><span data-stu-id="93731-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="93731-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span><span class="sxs-lookup"><span data-stu-id="93731-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="93731-159">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="93731-159">Create a simulated device app</span></span>
<span data-ttu-id="93731-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="93731-161">Create an empty folder called **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="93731-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="93731-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="93731-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="93731-163">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="93731-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="93731-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="93731-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="93731-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span><span class="sxs-lookup"><span data-stu-id="93731-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="93731-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="93731-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="93731-167">Add a **connectionString** variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="93731-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="93731-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span><span class="sxs-lookup"><span data-stu-id="93731-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="93731-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="93731-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="93731-170">Add the following function to display output from the application:</span><span class="sxs-lookup"><span data-stu-id="93731-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="93731-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span><span class="sxs-lookup"><span data-stu-id="93731-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="93731-172">Open the connection to your IoT Hub and start sending messages:</span><span class="sxs-lookup"><span data-stu-id="93731-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="93731-173">Save and close the **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="93731-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="93731-174">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="93731-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="93731-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="93731-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="93731-176">Run the apps</span><span class="sxs-lookup"><span data-stu-id="93731-176">Run the apps</span></span>
<span data-ttu-id="93731-177">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="93731-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="93731-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="93731-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IoT Hub service app to monitor device-to-cloud messages][7]
2. <span data-ttu-id="93731-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="93731-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IoT Hub device app to send device-to-cloud messages][8]
3. <span data-ttu-id="93731-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span><span class="sxs-lookup"><span data-stu-id="93731-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![Azure portal Usage tile showing number of messages sent to IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="93731-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="93731-184">Next steps</span></span>
<span data-ttu-id="93731-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="93731-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="93731-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="93731-187">You also created an app that displays the messages received by the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="93731-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="93731-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="93731-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="93731-189">[Connecting your device][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="93731-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="93731-190">[Getting started with device management][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="93731-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="93731-191">[Getting started with the IoT Gateway SDK][lnk-gateway-SDK]</span><span class="sxs-lookup"><span data-stu-id="93731-191">[Getting started with the IoT Gateway SDK][lnk-gateway-SDK]</span></span>

<span data-ttu-id="93731-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="93731-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

<!-- Images. -->
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-getstarted/runapp1.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-getstarted/runapp2.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/



