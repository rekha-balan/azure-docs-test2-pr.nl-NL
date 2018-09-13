---
title: Device firmware update with Azure IoT Hub (Node) | Microsoft Docs
description: How to use device management on Azure IoT Hub to initiate a device firmware update. You use the Azure IoT SDKs for Node.js to implement a simulated device app and a service app that triggers the firmware update.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: ''
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 30a707ec15d592c8a10905e13a75ea2f6e52cccc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552229"
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="02170-104">Use device management to initiate a device firmware update (Node/Node)</span><span class="sxs-lookup"><span data-stu-id="02170-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="02170-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="02170-105">Introduction</span></span>
<span data-ttu-id="02170-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span><span class="sxs-lookup"><span data-stu-id="02170-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="02170-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span><span class="sxs-lookup"><span data-stu-id="02170-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="02170-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span><span class="sxs-lookup"><span data-stu-id="02170-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="02170-109">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="02170-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="02170-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="02170-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="02170-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span><span class="sxs-lookup"><span data-stu-id="02170-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="02170-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span><span class="sxs-lookup"><span data-stu-id="02170-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="02170-113">During each stage of the update, the device uses the reported properties to report on progress.</span><span class="sxs-lookup"><span data-stu-id="02170-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="02170-114">At the end of this tutorial, you have two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="02170-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="02170-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="02170-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="02170-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span><span class="sxs-lookup"><span data-stu-id="02170-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="02170-117">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="02170-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="02170-118">Node.js version 0.12.x or later,</span><span class="sxs-lookup"><span data-stu-id="02170-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="02170-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="02170-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="02170-120">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="02170-120">An active Azure account.</span></span> <span data-ttu-id="02170-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="02170-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="02170-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span><span class="sxs-lookup"><span data-stu-id="02170-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="02170-123">Trigger a remote firmware update on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="02170-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="02170-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span><span class="sxs-lookup"><span data-stu-id="02170-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="02170-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span><span class="sxs-lookup"><span data-stu-id="02170-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="02170-126">Create an empty folder called **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="02170-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="02170-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="02170-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="02170-128">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="02170-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="02170-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span><span class="sxs-lookup"><span data-stu-id="02170-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-hub --save
    ```
3. <span data-ttu-id="02170-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span><span class="sxs-lookup"><span data-stu-id="02170-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="02170-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="02170-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="02170-132">Add the following variable declarations and replace the placeholder values:</span><span class="sxs-lookup"><span data-stu-id="02170-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="02170-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span><span class="sxs-lookup"><span data-stu-id="02170-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="02170-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span><span class="sxs-lookup"><span data-stu-id="02170-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="02170-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span><span class="sxs-lookup"><span data-stu-id="02170-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="02170-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span><span class="sxs-lookup"><span data-stu-id="02170-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="02170-137">Run the apps</span><span class="sxs-lookup"><span data-stu-id="02170-137">Run the apps</span></span>
<span data-ttu-id="02170-138">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="02170-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="02170-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="02170-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="02170-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span><span class="sxs-lookup"><span data-stu-id="02170-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="02170-141">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="02170-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02170-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="02170-142">Next steps</span></span>
<span data-ttu-id="02170-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span><span class="sxs-lookup"><span data-stu-id="02170-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="02170-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="02170-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
