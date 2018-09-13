---
title: Schedule jobs with Azure IoT Hub (.NET/Node) | Microsoft Docs
description: How to schedule an Azure IoT Hub job to invoke a direct method on multiple devices. You use the Azure IoT device SDK for Node.js to implement the simulated device apps and the Azure IoT service SDK for .NET to implement a service app to run the job.
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
ms.date: 03/30/2017
ms.author: juanpere
ms.openlocfilehash: 783cd82a9e32688824b4fe617094dfb318de0477
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548935"
---
# <a name="schedule-and-broadcast-jobs"></a><span data-ttu-id="ba9db-104">Schedule and broadcast jobs</span><span class="sxs-lookup"><span data-stu-id="ba9db-104">Schedule and broadcast jobs</span></span>
[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

## <a name="introduction"></a><span data-ttu-id="ba9db-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="ba9db-105">Introduction</span></span>
<span data-ttu-id="ba9db-106">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span><span class="sxs-lookup"><span data-stu-id="ba9db-106">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="ba9db-107">Jobs can be used for the following actions:</span><span class="sxs-lookup"><span data-stu-id="ba9db-107">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="ba9db-108">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="ba9db-108">Update desired properties</span></span>
* <span data-ttu-id="ba9db-109">Update tags</span><span class="sxs-lookup"><span data-stu-id="ba9db-109">Update tags</span></span>
* <span data-ttu-id="ba9db-110">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="ba9db-110">Invoke direct methods</span></span>

<span data-ttu-id="ba9db-111">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span><span class="sxs-lookup"><span data-stu-id="ba9db-111">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="ba9db-112">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span><span class="sxs-lookup"><span data-stu-id="ba9db-112">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="ba9db-113">It can then track progress as each of those devices receive and execute the reboot method.</span><span class="sxs-lookup"><span data-stu-id="ba9db-113">It can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="ba9db-114">Learn more about each of these capabilities in these articles:</span><span class="sxs-lookup"><span data-stu-id="ba9db-114">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="ba9db-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="ba9db-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="ba9db-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="ba9db-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="ba9db-117">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="ba9db-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ba9db-118">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the back-end app.</span><span class="sxs-lookup"><span data-stu-id="ba9db-118">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the back-end app.</span></span>
* <span data-ttu-id="ba9db-119">Create a .NET console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span><span class="sxs-lookup"><span data-stu-id="ba9db-119">Create a .NET console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="ba9db-120">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span><span class="sxs-lookup"><span data-stu-id="ba9db-120">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="ba9db-121">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span><span class="sxs-lookup"><span data-stu-id="ba9db-121">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="ba9db-122">**ScheduleJob**, which calls a direct method in the simulated device app and updates the device twin's desired properties using a job.</span><span class="sxs-lookup"><span data-stu-id="ba9db-122">**ScheduleJob**, which calls a direct method in the simulated device app and updates the device twin's desired properties using a job.</span></span>

<span data-ttu-id="ba9db-123">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="ba9db-123">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ba9db-124">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ba9db-124">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ba9db-125">Node.js version 0.12.x or later.</span><span class="sxs-lookup"><span data-stu-id="ba9db-125">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="ba9db-126">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="ba9db-126">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ba9db-127">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="ba9db-127">An active Azure account.</span></span> <span data-ttu-id="ba9db-128">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="ba9db-128">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="ba9db-129">Schedule jobs for calling a direct method and updating a device twin's properties</span><span class="sxs-lookup"><span data-stu-id="ba9db-129">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="ba9db-130">In this section, you create a .NET console app (using C#) that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="ba9db-130">In this section, you create a .NET console app (using C#) that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="ba9db-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="ba9db-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="ba9db-132">Name the project **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="ba9db-132">Name the project **ScheduleJob**.</span></span>

    ![New Visual C# Windows Classic Desktop project][img-createapp]

1. <span data-ttu-id="ba9db-134">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="ba9db-134">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="ba9db-135">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="ba9db-135">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="ba9db-136">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="ba9db-136">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window][img-servicenuget]
1. <span data-ttu-id="ba9db-138">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="ba9db-138">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="ba9db-139">Add the following `using` statement if not already present in the default statements.</span><span class="sxs-lookup"><span data-stu-id="ba9db-139">Add the following `using` statement if not already present in the default statements.</span></span>

        using System.Threading.Tasks;
        
1. <span data-ttu-id="ba9db-140">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="ba9db-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="ba9db-141">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ba9db-141">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        
1. <span data-ttu-id="ba9db-142">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="ba9db-142">Add the following method to the **Program** class:</span></span>
   
        public static async Task MonitorJob(string jobId)
        {
            JobResponse result;
            do
            {
                result = await jobClient.GetJobAsync(jobId);
                Console.WriteLine("Job Status : " + result.Status.ToString());
                Thread.Sleep(2000);
            } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
        }
                
1. <span data-ttu-id="ba9db-143">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="ba9db-143">Add the following method to the **Program** class:</span></span>

        public static async Task StartMethodJob(string jobId)
        {
            CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

            JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
                "deviceId='myDeviceId'",
                directMethod,
                DateTime.Now,
                10);

            Console.WriteLine("Started Method Job");
        }

1. <span data-ttu-id="ba9db-144">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="ba9db-144">Add the following method to the **Program** class:</span></span>

        public static async Task StartTwinUpdateJob(string jobId)
        {
            var twin = new Twin();
            twin.Properties.Desired["Building"] = "43";
            twin.Properties.Desired["Floor"] = "3";
            twin.ETag = "*";

            JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
                "deviceId='myDeviceId'",
                twin,
                DateTime.Now,
                10);

            Console.WriteLine("Started Twin Update Job");
        }
 

1. <span data-ttu-id="ba9db-145">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="ba9db-145">Finally, add the following lines to the **Main** method:</span></span>
   
        jobClient = JobClient.CreateFromConnectionString(connString);

        string methodJobId = Guid.NewGuid().ToString();

        StartMethodJob(methodJobId);
        MonitorJob(methodJobId).Wait();
        Console.WriteLine("Press ENTER to run the next job.");
        Console.ReadLine();

        string twinUpdateJobId = Guid.NewGuid().ToString();

        StartTwinUpdateJob(twinUpdateJobId);
        MonitorJob(twinUpdateJobId).Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();

1. <span data-ttu-id="ba9db-146">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span><span class="sxs-lookup"><span data-stu-id="ba9db-146">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="ba9db-147">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="ba9db-147">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ba9db-148">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="ba9db-148">Create a simulated device app</span></span>
<span data-ttu-id="ba9db-149">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span><span class="sxs-lookup"><span data-stu-id="ba9db-149">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="ba9db-150">Create a new empty folder called **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="ba9db-150">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="ba9db-151">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="ba9db-151">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="ba9db-152">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="ba9db-152">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="ba9db-153">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span><span class="sxs-lookup"><span data-stu-id="ba9db-153">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="ba9db-154">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span><span class="sxs-lookup"><span data-stu-id="ba9db-154">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
1. <span data-ttu-id="ba9db-155">Add the following 'require' statements at the start of the **simDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="ba9db-155">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
1. <span data-ttu-id="ba9db-156">Add a **connectionString** variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="ba9db-156">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="ba9db-157">Make sure to replace the placeholders with values appropriate to your setup.</span><span class="sxs-lookup"><span data-stu-id="ba9db-157">Make sure to replace the placeholders with values appropriate to your setup.</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
1. <span data-ttu-id="ba9db-158">Add the following function to handle the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="ba9db-158">Add the following function to handle the **lockDoor** method.</span></span>
   
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
1. <span data-ttu-id="ba9db-159">Add the following code to register the handler for the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="ba9db-159">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
1. <span data-ttu-id="ba9db-160">Save and close the **simDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="ba9db-160">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ba9db-161">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="ba9db-161">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ba9db-162">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ba9db-162">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="ba9db-163">Run the apps</span><span class="sxs-lookup"><span data-stu-id="ba9db-163">Run the apps</span></span>
<span data-ttu-id="ba9db-164">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="ba9db-164">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="ba9db-165">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="ba9db-165">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
1. <span data-ttu-id="ba9db-166">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="ba9db-166">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="ba9db-167">You see the output from both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="ba9db-167">You see the output from both device and back-end apps.</span></span>

    ![Run the apps to schedule jobs][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="ba9db-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba9db-169">Next steps</span></span>
<span data-ttu-id="ba9db-170">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="ba9db-170">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="ba9db-171">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="ba9db-171">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="ba9db-172">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span><span class="sxs-lookup"><span data-stu-id="ba9db-172">To continue getting started with IoT Hub, see [Getting started with the IoT Gateway SDK][lnk-gateway-SDK].</span></span>

<!-- images -->
[img-servicenuget]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/



