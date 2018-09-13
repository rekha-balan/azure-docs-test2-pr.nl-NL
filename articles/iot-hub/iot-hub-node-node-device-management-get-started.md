---
title: Get started with Azure IoT Hub device management (Node) | Microsoft Docs
description: How to use IoT Hub device management to initiate a remote device reboot. You use the Azure IoT SDK for Node.js to implement a simulated device app that includes a direct method and a service app that invokes the direct method.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: ''
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: cf8ea2726abd9a026dcefaf9c240be6ab32be4fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662357"
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="cfc38-104">Get started with device management (Node)</span><span class="sxs-lookup"><span data-stu-id="cfc38-104">Get started with device management (Node)</span></span>
## <a name="introduction"></a><span data-ttu-id="cfc38-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="cfc38-105">Introduction</span></span>
<span data-ttu-id="cfc38-106">IoT cloud applications can use primitives in Azure IoT Hub, namely the device twin and direct methods, to remotely start and monitor device management actions on devices.</span><span class="sxs-lookup"><span data-stu-id="cfc38-106">IoT cloud applications can use primitives in Azure IoT Hub, namely the device twin and direct methods, to remotely start and monitor device management actions on devices.</span></span> <span data-ttu-id="cfc38-107">This article provides guidance and code for how an IoT cloud application and a device work together to initiate and monitor a remote device reboot using IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cfc38-107">This article provides guidance and code for how an IoT cloud application and a device work together to initiate and monitor a remote device reboot using IoT Hub.</span></span>

<span data-ttu-id="cfc38-108">To remotely start and monitor device management actions on your devices from a cloud-based, back-end app, use Azure IoT Hub primitives such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod].</span><span class="sxs-lookup"><span data-stu-id="cfc38-108">To remotely start and monitor device management actions on your devices from a cloud-based, back-end app, use Azure IoT Hub primitives such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod].</span></span> <span data-ttu-id="cfc38-109">This tutorial shows you how a back-end app and a device can work together to enable you to initiate and monitor a remote device reboot from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cfc38-109">This tutorial shows you how a back-end app and a device can work together to enable you to initiate and monitor a remote device reboot from IoT Hub.</span></span>

<span data-ttu-id="cfc38-110">You use a direct method to initiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in the cloud.</span><span class="sxs-lookup"><span data-stu-id="cfc38-110">You use a direct method to initiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in the cloud.</span></span> <span data-ttu-id="cfc38-111">The device is responsible for:</span><span class="sxs-lookup"><span data-stu-id="cfc38-111">The device is responsible for:</span></span>

* <span data-ttu-id="cfc38-112">Handling the method request sent from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cfc38-112">Handling the method request sent from IoT Hub.</span></span>
* <span data-ttu-id="cfc38-113">Initiating the corresponding device-specific action on the device.</span><span class="sxs-lookup"><span data-stu-id="cfc38-113">Initiating the corresponding device-specific action on the device.</span></span>
* <span data-ttu-id="cfc38-114">Providing status updates through the reported properties to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cfc38-114">Providing status updates through the reported properties to IoT Hub.</span></span>

<span data-ttu-id="cfc38-115">You can use a back-end app in the cloud to run device twin queries to report on the progress of your device management actions.</span><span class="sxs-lookup"><span data-stu-id="cfc38-115">You can use a back-end app in the cloud to run device twin queries to report on the progress of your device management actions.</span></span>

<span data-ttu-id="cfc38-116">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="cfc38-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="cfc38-117">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cfc38-117">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="cfc38-118">Create a simulated device app that contains a direct method that reboots that device.</span><span class="sxs-lookup"><span data-stu-id="cfc38-118">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="cfc38-119">Direct methods are invoked from the cloud.</span><span class="sxs-lookup"><span data-stu-id="cfc38-119">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="cfc38-120">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cfc38-120">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="cfc38-121">At the end of this tutorial, you have two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="cfc38-121">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="cfc38-122">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span><span class="sxs-lookup"><span data-stu-id="cfc38-122">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="cfc38-123">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="cfc38-123">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="cfc38-124">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="cfc38-124">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="cfc38-125">Node.js version 0.12.x or later,</span><span class="sxs-lookup"><span data-stu-id="cfc38-125">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="cfc38-126">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="cfc38-126">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cfc38-127">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="cfc38-127">An active Azure account.</span></span> <span data-ttu-id="cfc38-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="cfc38-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="cfc38-129">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="cfc38-129">Create a simulated device app</span></span>
<span data-ttu-id="cfc38-130">In this section, you will</span><span class="sxs-lookup"><span data-stu-id="cfc38-130">In this section, you will</span></span>

* <span data-ttu-id="cfc38-131">Create a Node.js console app that responds to a direct method called by the cloud</span><span class="sxs-lookup"><span data-stu-id="cfc38-131">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="cfc38-132">Trigger a simulated device reboot</span><span class="sxs-lookup"><span data-stu-id="cfc38-132">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="cfc38-133">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span><span class="sxs-lookup"><span data-stu-id="cfc38-133">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="cfc38-134">Create an empty folder called **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="cfc38-134">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="cfc38-135">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="cfc38-135">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="cfc38-136">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="cfc38-136">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cfc38-137">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="cfc38-137">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="cfc38-138">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span><span class="sxs-lookup"><span data-stu-id="cfc38-138">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="cfc38-139">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span><span class="sxs-lookup"><span data-stu-id="cfc38-139">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="cfc38-140">Add a **connectionString** variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="cfc38-140">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="cfc38-141">Replace the connection string with your device connection string.</span><span class="sxs-lookup"><span data-stu-id="cfc38-141">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="cfc38-142">Add the following function to implement the direct method on the device</span><span class="sxs-lookup"><span data-stu-id="cfc38-142">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="cfc38-143">Open the connection to your IoT hub and start the direct method listener:</span><span class="sxs-lookup"><span data-stu-id="cfc38-143">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="cfc38-144">Save and close the **dmpatterns_getstarted_device.js** file.</span><span class="sxs-lookup"><span data-stu-id="cfc38-144">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="cfc38-145">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="cfc38-145">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="cfc38-146">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="cfc38-146">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="cfc38-147">Trigger a remote reboot on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="cfc38-147">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="cfc38-148">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span><span class="sxs-lookup"><span data-stu-id="cfc38-148">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="cfc38-149">The app uses device twin queries to discover the last reboot time for that device.</span><span class="sxs-lookup"><span data-stu-id="cfc38-149">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="cfc38-150">Create an empty folder called **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="cfc38-150">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="cfc38-151">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="cfc38-151">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="cfc38-152">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="cfc38-152">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cfc38-153">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="cfc38-153">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="cfc38-154">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span><span class="sxs-lookup"><span data-stu-id="cfc38-154">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="cfc38-155">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="cfc38-155">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="cfc38-156">Add the following variable declarations and replace the placeholder values:</span><span class="sxs-lookup"><span data-stu-id="cfc38-156">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="cfc38-157">Add the following function to invoke the device method to reboot the target device:</span><span class="sxs-lookup"><span data-stu-id="cfc38-157">Add the following function to invoke the device method to reboot the target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="cfc38-158">Add the following function to query for the device and get the last reboot time:</span><span class="sxs-lookup"><span data-stu-id="cfc38-158">Add the following function to query for the device and get the last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="cfc38-159">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span><span class="sxs-lookup"><span data-stu-id="cfc38-159">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="cfc38-160">Save and close the **dmpatterns_getstarted_service.js** file.</span><span class="sxs-lookup"><span data-stu-id="cfc38-160">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="cfc38-161">Run the apps</span><span class="sxs-lookup"><span data-stu-id="cfc38-161">Run the apps</span></span>
<span data-ttu-id="cfc38-162">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="cfc38-162">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="cfc38-163">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="cfc38-163">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="cfc38-164">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span><span class="sxs-lookup"><span data-stu-id="cfc38-164">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="cfc38-165">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="cfc38-165">You see the device response to the direct method in the console.</span></span>

## <a name="customize-and-extend-the-device-management-actions"></a><span data-ttu-id="cfc38-166">Customize and extend the device management actions</span><span class="sxs-lookup"><span data-stu-id="cfc38-166">Customize and extend the device management actions</span></span>
<span data-ttu-id="cfc38-167">Your IoT solutions can expand the defined set of device management patterns or enable custom patterns by using the device twin and cloud-to-device method primitives.</span><span class="sxs-lookup"><span data-stu-id="cfc38-167">Your IoT solutions can expand the defined set of device management patterns or enable custom patterns by using the device twin and cloud-to-device method primitives.</span></span> <span data-ttu-id="cfc38-168">Other examples of device management actions include factory reset, firmware update, software update, power management, network and connectivity management, and data encryption.</span><span class="sxs-lookup"><span data-stu-id="cfc38-168">Other examples of device management actions include factory reset, firmware update, software update, power management, network and connectivity management, and data encryption.</span></span>

## <a name="device-maintenance-windows"></a><span data-ttu-id="cfc38-169">Device maintenance windows</span><span class="sxs-lookup"><span data-stu-id="cfc38-169">Device maintenance windows</span></span>
<span data-ttu-id="cfc38-170">Typically, you configure devices to perform actions at a time that minimizes interruptions and downtime.</span><span class="sxs-lookup"><span data-stu-id="cfc38-170">Typically, you configure devices to perform actions at a time that minimizes interruptions and downtime.</span></span>  <span data-ttu-id="cfc38-171">Device maintenance windows are a commonly used pattern to define the time when a device should update its configuration.</span><span class="sxs-lookup"><span data-stu-id="cfc38-171">Device maintenance windows are a commonly used pattern to define the time when a device should update its configuration.</span></span> <span data-ttu-id="cfc38-172">Your back-end solutions can use the desired properties of the device twin to define and activate a policy on your device that enables a maintenance window.</span><span class="sxs-lookup"><span data-stu-id="cfc38-172">Your back-end solutions can use the desired properties of the device twin to define and activate a policy on your device that enables a maintenance window.</span></span> <span data-ttu-id="cfc38-173">When a device receives the maintenance window policy, it can use the reported property of the device twin to report the status of the policy.</span><span class="sxs-lookup"><span data-stu-id="cfc38-173">When a device receives the maintenance window policy, it can use the reported property of the device twin to report the status of the policy.</span></span> <span data-ttu-id="cfc38-174">The back-end app can then use device twin queries to attest to compliance of devices and each policy.</span><span class="sxs-lookup"><span data-stu-id="cfc38-174">The back-end app can then use device twin queries to attest to compliance of devices and each policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfc38-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="cfc38-175">Next steps</span></span>
<span data-ttu-id="cfc38-176">In this tutorial, you used a direct method to trigger a remote reboot on a device.</span><span class="sxs-lookup"><span data-stu-id="cfc38-176">In this tutorial, you used a direct method to trigger a remote reboot on a device.</span></span> <span data-ttu-id="cfc38-177">You used the reported properties to report the last reboot time from the device, and queried the device twin to discover the last reboot time of the device from the cloud.</span><span class="sxs-lookup"><span data-stu-id="cfc38-177">You used the reported properties to report the last reboot time from the device, and queried the device twin to discover the last reboot time of the device from the cloud.</span></span>

<span data-ttu-id="cfc38-178">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span><span class="sxs-lookup"><span data-stu-id="cfc38-178">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="cfc38-179">[Tutorial: How to do a firmware update][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="cfc38-179">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="cfc38-180">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="cfc38-180">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<span data-ttu-id="cfc38-181">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span><span class="sxs-lookup"><span data-stu-id="cfc38-181">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span></span>

<!-- images and links -->
[img-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx


