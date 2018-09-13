---
title: Schedule jobs with Azure IoT Hub (Node) | Microsoft Docs
description: How to schedule an Azure IoT Hub job to invoke a direct method on multiple devices. You use the Azure IoT SDKs for Node.js to implement the simulated device apps and a service app to run the job.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: ''
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8b7c108cef383fc737784e42ef2adfc6af1b7824
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556525"
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="69427-104">Schedule and broadcast jobs (Node)</span><span class="sxs-lookup"><span data-stu-id="69427-104">Schedule and broadcast jobs (Node)</span></span>

## <a name="introduction"></a><span data-ttu-id="69427-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="69427-105">Introduction</span></span>
<span data-ttu-id="69427-106">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span><span class="sxs-lookup"><span data-stu-id="69427-106">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="69427-107">Jobs can be used for the following actions:</span><span class="sxs-lookup"><span data-stu-id="69427-107">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="69427-108">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="69427-108">Update desired properties</span></span>
* <span data-ttu-id="69427-109">Update tags</span><span class="sxs-lookup"><span data-stu-id="69427-109">Update tags</span></span>
* <span data-ttu-id="69427-110">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="69427-110">Invoke direct methods</span></span>

<span data-ttu-id="69427-111">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span><span class="sxs-lookup"><span data-stu-id="69427-111">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="69427-112">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span><span class="sxs-lookup"><span data-stu-id="69427-112">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="69427-113">That application can then track progress as each of those devices receive and execute the reboot method.</span><span class="sxs-lookup"><span data-stu-id="69427-113">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="69427-114">Learn more about each of these capabilities in these articles:</span><span class="sxs-lookup"><span data-stu-id="69427-114">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="69427-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="69427-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="69427-116">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="69427-116">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="69427-117">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="69427-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="69427-118">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="69427-118">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span></span>
* <span data-ttu-id="69427-119">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span><span class="sxs-lookup"><span data-stu-id="69427-119">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="69427-120">At the end of this tutorial, you have two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="69427-120">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="69427-121">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span><span class="sxs-lookup"><span data-stu-id="69427-121">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="69427-122">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span><span class="sxs-lookup"><span data-stu-id="69427-122">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span></span>

<span data-ttu-id="69427-123">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="69427-123">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="69427-124">Node.js version 0.12.x or later,</span><span class="sxs-lookup"><span data-stu-id="69427-124">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="69427-125">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="69427-125">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="69427-126">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="69427-126">An active Azure account.</span></span> <span data-ttu-id="69427-127">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="69427-127">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="69427-128">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="69427-128">Create a simulated device app</span></span>
<span data-ttu-id="69427-129">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span><span class="sxs-lookup"><span data-stu-id="69427-129">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="69427-130">Create a new empty folder called **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="69427-130">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="69427-131">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="69427-131">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="69427-132">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="69427-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="69427-133">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="69427-133">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="69427-134">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span><span class="sxs-lookup"><span data-stu-id="69427-134">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="69427-135">Add the following 'require' statements at the start of the **simDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="69427-135">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="69427-136">Add a **connectionString** variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="69427-136">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="69427-137">Add the following function to handle the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="69427-137">Add the following function to handle the **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="69427-138">Add the following code to register the handler for the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="69427-138">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="69427-139">Save and close the **simDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="69427-139">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="69427-140">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="69427-140">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="69427-141">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="69427-141">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="69427-142">Schedule jobs for calling a direct method and updating a device twin's properties</span><span class="sxs-lookup"><span data-stu-id="69427-142">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="69427-143">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="69427-143">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="69427-144">Create a new empty folder called **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="69427-144">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="69427-145">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="69427-145">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="69427-146">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="69427-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="69427-147">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="69427-147">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="69427-148">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span><span class="sxs-lookup"><span data-stu-id="69427-148">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="69427-149">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="69427-149">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="69427-150">Add the following variable declarations and replace the placeholder values:</span><span class="sxs-lookup"><span data-stu-id="69427-150">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="69427-151">Add the following function that will be used to monitor the execution of the job:</span><span class="sxs-lookup"><span data-stu-id="69427-151">Add the following function that will be used to monitor the execution of the job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="69427-152">Add the following code to schedule the job that calls the device method:</span><span class="sxs-lookup"><span data-stu-id="69427-152">Add the following code to schedule the job that calls the device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable to process method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="69427-153">Add the following code to schedule the job to update the device twin:</span><span class="sxs-lookup"><span data-stu-id="69427-153">Add the following code to schedule the job to update the device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="69427-154">Save and close the **scheduleJobService.js** file.</span><span class="sxs-lookup"><span data-stu-id="69427-154">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="69427-155">Run the applications</span><span class="sxs-lookup"><span data-stu-id="69427-155">Run the applications</span></span>
<span data-ttu-id="69427-156">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="69427-156">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="69427-157">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="69427-157">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="69427-158">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span><span class="sxs-lookup"><span data-stu-id="69427-158">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="69427-159">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="69427-159">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69427-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="69427-160">Next steps</span></span>
<span data-ttu-id="69427-161">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="69427-161">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="69427-162">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span><span class="sxs-lookup"><span data-stu-id="69427-162">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="69427-163">[Tutorial: How to do a firmware update][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="69427-163">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="69427-164">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span><span class="sxs-lookup"><span data-stu-id="69427-164">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
