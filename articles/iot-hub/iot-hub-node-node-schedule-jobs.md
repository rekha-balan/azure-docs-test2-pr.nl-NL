---
title: Schedule jobs with Azure IoT Hub (Node) | Microsoft Docs
description: How to schedule an Azure IoT Hub job to invoke a direct method on multiple devices. You use the Azure IoT SDKs for Node.js to implement the simulated device apps and a service app to run the job.
author: juanjperez
manager: cberlin
ms.service: iot-hub
services: iot-hub
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 10/06/2017
ms.author: juanpere
ms.openlocfilehash: 2161cd12f8bdb6aa3018d81a7864816a97ed122a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783099"
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="8d581-104">Schedule and broadcast jobs (Node)</span><span class="sxs-lookup"><span data-stu-id="8d581-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="8d581-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span><span class="sxs-lookup"><span data-stu-id="8d581-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="8d581-106">Jobs can be used for the following actions:</span><span class="sxs-lookup"><span data-stu-id="8d581-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="8d581-107">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="8d581-107">Update desired properties</span></span>
* <span data-ttu-id="8d581-108">Update tags</span><span class="sxs-lookup"><span data-stu-id="8d581-108">Update tags</span></span>
* <span data-ttu-id="8d581-109">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="8d581-109">Invoke direct methods</span></span>

<span data-ttu-id="8d581-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span><span class="sxs-lookup"><span data-stu-id="8d581-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="8d581-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span><span class="sxs-lookup"><span data-stu-id="8d581-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="8d581-112">That application can then track progress as each of those devices receive and execute the reboot method.</span><span class="sxs-lookup"><span data-stu-id="8d581-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="8d581-113">Learn more about each of these capabilities in these articles:</span><span class="sxs-lookup"><span data-stu-id="8d581-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="8d581-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="8d581-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="8d581-115">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="8d581-115">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="8d581-116">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="8d581-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="8d581-117">Create a Node.js simulated device app that has a direct method, which enables **lockDoor**, which can be called by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="8d581-117">Create a Node.js simulated device app that has a direct method, which enables **lockDoor**, which can be called by the solution back end.</span></span>
* <span data-ttu-id="8d581-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span><span class="sxs-lookup"><span data-stu-id="8d581-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="8d581-119">At the end of this tutorial, you have two Node.js apps:</span><span class="sxs-lookup"><span data-stu-id="8d581-119">At the end of this tutorial, you have two Node.js apps:</span></span>

<span data-ttu-id="8d581-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span><span class="sxs-lookup"><span data-stu-id="8d581-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="8d581-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and updates the device twin's desired properties using a job.</span><span class="sxs-lookup"><span data-stu-id="8d581-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and updates the device twin's desired properties using a job.</span></span>

<span data-ttu-id="8d581-122">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="8d581-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8d581-123">Node.js version 4.0.x or later,</span><span class="sxs-lookup"><span data-stu-id="8d581-123">Node.js version 4.0.x or later,</span></span> <br/>  <span data-ttu-id="8d581-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="8d581-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8d581-125">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="8d581-125">An active Azure account.</span></span> <span data-ttu-id="8d581-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="8d581-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8d581-127">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="8d581-127">Create a simulated device app</span></span>
<span data-ttu-id="8d581-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="8d581-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated **lockDoor** method.</span></span>

1. <span data-ttu-id="8d581-129">Create a new empty folder called **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="8d581-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="8d581-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="8d581-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="8d581-131">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="8d581-131">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8d581-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="8d581-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="8d581-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span><span class="sxs-lookup"><span data-stu-id="8d581-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="8d581-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="8d581-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="8d581-135">Add a **connectionString** variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="8d581-135">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="8d581-136">Add the following function to handle the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="8d581-136">Add the following function to handle the **lockDoor** method.</span></span>
   
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
7. <span data-ttu-id="8d581-137">Add the following code to register the handler for the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="8d581-137">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
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
8. <span data-ttu-id="8d581-138">Save and close the **simDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="8d581-138">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="8d581-139">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="8d581-139">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8d581-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="8d581-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="8d581-141">Schedule jobs for calling a direct method and updating a device twin's properties</span><span class="sxs-lookup"><span data-stu-id="8d581-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="8d581-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="8d581-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="8d581-143">Create a new empty folder called **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="8d581-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="8d581-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="8d581-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="8d581-145">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="8d581-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8d581-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="8d581-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="8d581-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span><span class="sxs-lookup"><span data-stu-id="8d581-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="8d581-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="8d581-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="8d581-149">Add the following variable declarations and replace the placeholder values:</span><span class="sxs-lookup"><span data-stu-id="8d581-149">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  300;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="8d581-150">Add the following function that is used to monitor the execution of the job:</span><span class="sxs-lookup"><span data-stu-id="8d581-150">Add the following function that is used to monitor the execution of the job:</span></span>
   
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
7. <span data-ttu-id="8d581-151">Add the following code to schedule the job that calls the device method:</span><span class="sxs-lookup"><span data-stu-id="8d581-151">Add the following code to schedule the job that calls the device method:</span></span>
   
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
8. <span data-ttu-id="8d581-152">Add the following code to schedule the job to update the device twin:</span><span class="sxs-lookup"><span data-stu-id="8d581-152">Add the following code to schedule the job to update the device twin:</span></span>
   
    ```
    var twinPatch = {
       etag: '*', 
       properties: {
           desired: {
               building: '43', 
               floor: 3
           }
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
9. <span data-ttu-id="8d581-153">Save and close the **scheduleJobService.js** file.</span><span class="sxs-lookup"><span data-stu-id="8d581-153">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="8d581-154">Run the applications</span><span class="sxs-lookup"><span data-stu-id="8d581-154">Run the applications</span></span>
<span data-ttu-id="8d581-155">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="8d581-155">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="8d581-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="8d581-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="8d581-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span><span class="sxs-lookup"><span data-stu-id="8d581-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="8d581-158">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="8d581-158">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d581-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d581-159">Next steps</span></span>
<span data-ttu-id="8d581-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="8d581-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="8d581-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span><span class="sxs-lookup"><span data-stu-id="8d581-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="8d581-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="8d581-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="8d581-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="8d581-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: tutorial-device-twins.md
[lnk-c2d-methods]: quickstart-control-device-node.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: tutorial-firmware-update.md
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
