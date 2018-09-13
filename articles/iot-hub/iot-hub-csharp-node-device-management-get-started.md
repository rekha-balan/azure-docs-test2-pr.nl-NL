---
title: Get started with Azure IoT Hub device management (.NET/Node) | Microsoft Docs
description: How to use Azure IoT Hub device management to initiate a remote device reboot. You use the Azure IoT device SDK for Node.js to implement a simulated device app that includes a direct method and the Azure IoT service SDK for .NET to implement a service app that invokes the direct method.
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: c46540a5ccf0218a041ec219e381fd43952c48a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550832"
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="6c4b0-104">Get started with device management (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="6c4b0-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]
## <a name="introduction"></a><span data-ttu-id="6c4b0-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="6c4b0-105">Introduction</span></span>
<span data-ttu-id="6c4b0-106">Back-end apps can use primitives in Azure IoT Hub, namely the device twin and direct methods, to remotely start and monitor device management actions on devices.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-106">Back-end apps can use primitives in Azure IoT Hub, namely the device twin and direct methods, to remotely start and monitor device management actions on devices.</span></span>  <span data-ttu-id="6c4b0-107">This article provides guidance and code for how back-end apps and devices work together to initiate and monitor a remote device reboot using IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-107">This article provides guidance and code for how back-end apps and devices work together to initiate and monitor a remote device reboot using IoT Hub.</span></span>

<span data-ttu-id="6c4b0-108">To remotely start and monitor device management actions on your devices from a cloud-based, back-end app, use IoT Hub primitives such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod].</span><span class="sxs-lookup"><span data-stu-id="6c4b0-108">To remotely start and monitor device management actions on your devices from a cloud-based, back-end app, use IoT Hub primitives such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod].</span></span> <span data-ttu-id="6c4b0-109">This tutorial shows you how a back-end app and a device can work together to enable you to initiate and monitor a remote device reboot from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-109">This tutorial shows you how a back-end app and a device can work together to enable you to initiate and monitor a remote device reboot from IoT Hub.</span></span>

<span data-ttu-id="6c4b0-110">You use a direct method to initiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in the cloud.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-110">You use a direct method to initiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in the cloud.</span></span> <span data-ttu-id="6c4b0-111">The device is responsible for:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-111">The device is responsible for:</span></span>

* <span data-ttu-id="6c4b0-112">Handling the method request sent from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-112">Handling the method request sent from IoT Hub.</span></span>
* <span data-ttu-id="6c4b0-113">Initiating the corresponding device-specific action on the device.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-113">Initiating the corresponding device-specific action on the device.</span></span>
* <span data-ttu-id="6c4b0-114">Providing status updates through the reported properties to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-114">Providing status updates through the reported properties to IoT Hub.</span></span>

<span data-ttu-id="6c4b0-115">You can use a back-end app in the cloud to run device twin queries to report on the progress of your device management actions.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-115">You can use a back-end app in the cloud to run device twin queries to report on the progress of your device management actions.</span></span>

<span data-ttu-id="6c4b0-116">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6c4b0-117">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-117">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="6c4b0-118">Create a simulated device app that contains a direct method that reboots that device.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-118">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="6c4b0-119">Direct methods are invoked from the cloud.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-119">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="6c4b0-120">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-120">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="6c4b0-121">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-121">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="6c4b0-122">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-122">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="6c4b0-123">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-123">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="6c4b0-124">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-124">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6c4b0-125">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-125">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6c4b0-126">Node.js version 0.12.x or later,</span><span class="sxs-lookup"><span data-stu-id="6c4b0-126">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="6c4b0-127">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-127">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="6c4b0-128">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-128">An active Azure account.</span></span> <span data-ttu-id="6c4b0-129">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="6c4b0-129">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="6c4b0-130">Trigger a remote reboot on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="6c4b0-130">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="6c4b0-131">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-131">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="6c4b0-132">The app uses device twin queries to discover the last reboot time for that device.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-132">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="6c4b0-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="6c4b0-134">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-134">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="6c4b0-135">Name the project **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-135">Name the project **TriggerReboot**.</span></span>

    ![New Visual C# Windows Classic Desktop project][img-createapp]

2. <span data-ttu-id="6c4b0-137">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-137">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="6c4b0-138">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-138">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="6c4b0-139">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-139">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window][img-servicenuget]
4. <span data-ttu-id="6c4b0-141">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-141">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        
5. <span data-ttu-id="6c4b0-142">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="6c4b0-143">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-143">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="6c4b0-144">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-144">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="6c4b0-145">This code gets the device twin for the rebooting device and outputs the reported properties.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-145">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="6c4b0-146">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-146">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="6c4b0-147">This code initiates the reboot on the device using a direct method.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-147">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="6c4b0-148">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-148">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="6c4b0-149">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6c4b0-150">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="6c4b0-150">Create a simulated device app</span></span>
<span data-ttu-id="6c4b0-151">In this section, you will</span><span class="sxs-lookup"><span data-stu-id="6c4b0-151">In this section, you will</span></span>

* <span data-ttu-id="6c4b0-152">Create a Node.js console app that responds to a direct method called by the cloud</span><span class="sxs-lookup"><span data-stu-id="6c4b0-152">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="6c4b0-153">Trigger a simulated device reboot</span><span class="sxs-lookup"><span data-stu-id="6c4b0-153">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="6c4b0-154">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span><span class="sxs-lookup"><span data-stu-id="6c4b0-154">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="6c4b0-155">Create a new empty folder called **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-155">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="6c4b0-156">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-156">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="6c4b0-157">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-157">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6c4b0-158">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-158">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="6c4b0-159">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-159">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="6c4b0-160">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-160">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="6c4b0-161">Add a **connectionString** variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-161">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="6c4b0-162">Replace the connection string with your device connection string.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-162">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="6c4b0-163">Add the following function to implement the direct method on the device</span><span class="sxs-lookup"><span data-stu-id="6c4b0-163">Add the following function to implement the direct method on the device</span></span>
   
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
7. <span data-ttu-id="6c4b0-164">Add the following code to open the connection to your IoT hub and start the direct method listener:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-164">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="6c4b0-165">Save and close the **dmpatterns_getstarted_device.js** file.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-165">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="6c4b0-166">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-166">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6c4b0-167">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="6c4b0-167">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="6c4b0-168">Run the apps</span><span class="sxs-lookup"><span data-stu-id="6c4b0-168">Run the apps</span></span>
<span data-ttu-id="6c4b0-169">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-169">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="6c4b0-170">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-170">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="6c4b0-171">Run the C# console app **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-171">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="6c4b0-172">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-172">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="6c4b0-173">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-173">You see the device response to the direct method in the console.</span></span>

## <a name="customize-and-extend-the-device-management-actions"></a><span data-ttu-id="6c4b0-174">Customize and extend the device management actions</span><span class="sxs-lookup"><span data-stu-id="6c4b0-174">Customize and extend the device management actions</span></span>
<span data-ttu-id="6c4b0-175">Your IoT solutions can expand the defined set of device management patterns or enable custom patterns by using the device twin and cloud-to-device method primitives.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-175">Your IoT solutions can expand the defined set of device management patterns or enable custom patterns by using the device twin and cloud-to-device method primitives.</span></span> <span data-ttu-id="6c4b0-176">Other examples of device management actions include factory reset, firmware update, software update, power management, network and connectivity management, and data encryption.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-176">Other examples of device management actions include factory reset, firmware update, software update, power management, network and connectivity management, and data encryption.</span></span>

## <a name="device-maintenance-windows"></a><span data-ttu-id="6c4b0-177">Device maintenance windows</span><span class="sxs-lookup"><span data-stu-id="6c4b0-177">Device maintenance windows</span></span>
<span data-ttu-id="6c4b0-178">Typically, you configure devices to perform actions at a time that minimizes interruptions and downtime.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-178">Typically, you configure devices to perform actions at a time that minimizes interruptions and downtime.</span></span>  <span data-ttu-id="6c4b0-179">Device maintenance windows are a commonly used pattern to define the time when a device should update its configuration.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-179">Device maintenance windows are a commonly used pattern to define the time when a device should update its configuration.</span></span> <span data-ttu-id="6c4b0-180">Your back-end solutions can use the desired properties of the device twin to define and activate a policy on your device that enables a maintenance window.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-180">Your back-end solutions can use the desired properties of the device twin to define and activate a policy on your device that enables a maintenance window.</span></span> <span data-ttu-id="6c4b0-181">When a device receives the maintenance window policy, it can use the reported property of the device twin to report the status of the policy.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-181">When a device receives the maintenance window policy, it can use the reported property of the device twin to report the status of the policy.</span></span> <span data-ttu-id="6c4b0-182">The back-end app can then use device twin queries to attest to compliance of devices and each policy.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-182">The back-end app can then use device twin queries to attest to compliance of devices and each policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c4b0-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c4b0-183">Next steps</span></span>
<span data-ttu-id="6c4b0-184">In this tutorial, you used a direct method to trigger a remote reboot on a device.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-184">In this tutorial, you used a direct method to trigger a remote reboot on a device.</span></span> <span data-ttu-id="6c4b0-185">You used the reported properties to report the last reboot time from the device, and queried the device twin to discover the last reboot time of the device from the cloud.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-185">You used the reported properties to report the last reboot time from the device, and queried the device twin to discover the last reboot time of the device from the cloud.</span></span>

<span data-ttu-id="6c4b0-186">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span><span class="sxs-lookup"><span data-stu-id="6c4b0-186">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="6c4b0-187">[Tutorial: How to do a firmware update][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="6c4b0-187">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="6c4b0-188">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="6c4b0-188">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<span data-ttu-id="6c4b0-189">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span><span class="sxs-lookup"><span data-stu-id="6c4b0-189">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span></span>

<!-- images and links -->
[img-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

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
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/



