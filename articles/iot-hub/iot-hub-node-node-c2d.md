---
title: Cloud-to-device messages with Azure IoT Hub (Node) | Microsoft Docs
description: How to send cloud-to-device messages to a device from an Azure IoT hub using the Azure IoT SDKs for Node.js. You modify a simulated device app to receive cloud-to-device messages and modify a back-end app to send the cloud-to-device messages.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/16/2017
ms.author: dobett
ms.openlocfilehash: 95af9eca056da6b9228a1dd359e3b1aeab4ec69e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660878"
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="621aa-104">Send cloud-to-device messages with IoT Hub (Node)</span><span class="sxs-lookup"><span data-stu-id="621aa-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="621aa-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="621aa-105">Introduction</span></span>
<span data-ttu-id="621aa-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="621aa-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="621aa-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="621aa-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="621aa-108">This tutorial builds on [Get started with IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="621aa-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="621aa-109">It shows you how to:</span><span class="sxs-lookup"><span data-stu-id="621aa-109">It shows you how to:</span></span>

* <span data-ttu-id="621aa-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="621aa-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="621aa-111">Receive cloud-to-device messages on a device.</span><span class="sxs-lookup"><span data-stu-id="621aa-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="621aa-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="621aa-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="621aa-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="621aa-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="621aa-114">At the end of this tutorial, you run two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="621aa-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="621aa-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="621aa-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="621aa-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span><span class="sxs-lookup"><span data-stu-id="621aa-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="621aa-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="621aa-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="621aa-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="621aa-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="621aa-119">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="621aa-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="621aa-120">Node.js version 0.10.x or later.</span><span class="sxs-lookup"><span data-stu-id="621aa-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="621aa-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="621aa-121">An active Azure account.</span></span> <span data-ttu-id="621aa-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="621aa-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="621aa-123">Receive messages in the simulated device app</span><span class="sxs-lookup"><span data-stu-id="621aa-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="621aa-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="621aa-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="621aa-125">Using a text editor, open the SimulatedDevice.js file.</span><span class="sxs-lookup"><span data-stu-id="621aa-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="621aa-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="621aa-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="621aa-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span><span class="sxs-lookup"><span data-stu-id="621aa-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="621aa-128">Your new version of the **connectCallback** function looks like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="621aa-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
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
   
   > [!NOTE]
   > <span data-ttu-id="621aa-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="621aa-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="621aa-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="621aa-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="621aa-131">Send a cloud-to-device message</span><span class="sxs-lookup"><span data-stu-id="621aa-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="621aa-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="621aa-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="621aa-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="621aa-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="621aa-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="621aa-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="621aa-135">Create an empty folder called **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="621aa-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="621aa-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="621aa-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="621aa-137">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="621aa-137">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="621aa-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span><span class="sxs-lookup"><span data-stu-id="621aa-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="621aa-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span><span class="sxs-lookup"><span data-stu-id="621aa-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="621aa-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span><span class="sxs-lookup"><span data-stu-id="621aa-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="621aa-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span><span class="sxs-lookup"><span data-stu-id="621aa-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="621aa-142">Replace the iot hub connection string placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="621aa-142">Replace the iot hub connection string placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="621aa-143">Replace the target device placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span><span class="sxs-lookup"><span data-stu-id="621aa-143">Replace the target device placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="621aa-144">Add the following function to print operation results to the console:</span><span class="sxs-lookup"><span data-stu-id="621aa-144">Add the following function to print operation results to the console:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="621aa-145">Add the following function to print delivery feedback messages to the console:</span><span class="sxs-lookup"><span data-stu-id="621aa-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="621aa-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span><span class="sxs-lookup"><span data-stu-id="621aa-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="621aa-147">Save and close **SendCloudToDeviceMessage.js** file.</span><span class="sxs-lookup"><span data-stu-id="621aa-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="621aa-148">Run the applications</span><span class="sxs-lookup"><span data-stu-id="621aa-148">Run the applications</span></span>
<span data-ttu-id="621aa-149">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="621aa-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="621aa-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span><span class="sxs-lookup"><span data-stu-id="621aa-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```
    node SimulatedDevice.js 
    ```
   
    ![Run the simulated device app][img-simulated-device]
2. <span data-ttu-id="621aa-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span><span class="sxs-lookup"><span data-stu-id="621aa-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Run the app to send the cloud-to-device command][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="621aa-154">For simplicity's sake, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="621aa-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="621aa-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="621aa-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="621aa-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="621aa-156">Next steps</span></span>
<span data-ttu-id="621aa-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="621aa-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="621aa-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="621aa-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="621aa-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="621aa-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[Get started with IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT Hub developer guide]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/


