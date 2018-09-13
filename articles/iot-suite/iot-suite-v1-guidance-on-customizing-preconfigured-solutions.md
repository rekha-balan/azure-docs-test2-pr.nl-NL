---
title: Customizing preconfigured solutions | Microsoft Docs
description: Provides guidance on how to customize the Azure IoT Suite preconfigured solutions.
services: ''
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: corywink
ms.openlocfilehash: cb5955111cb3954f71f11602042b5153ccee3473
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856972"
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="9f916-103">Customize a preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="9f916-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="9f916-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span><span class="sxs-lookup"><span data-stu-id="9f916-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="9f916-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span><span class="sxs-lookup"><span data-stu-id="9f916-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="9f916-106">The following sections describe these common customization points.</span><span class="sxs-lookup"><span data-stu-id="9f916-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="9f916-107">Find the source code</span><span class="sxs-lookup"><span data-stu-id="9f916-107">Find the source code</span></span>

<span data-ttu-id="9f916-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span><span class="sxs-lookup"><span data-stu-id="9f916-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="9f916-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="9f916-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="9f916-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="9f916-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="9f916-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="9f916-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="9f916-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="9f916-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="9f916-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span><span class="sxs-lookup"><span data-stu-id="9f916-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="9f916-114">Change the preconfigured rules</span><span class="sxs-lookup"><span data-stu-id="9f916-114">Change the preconfigured rules</span></span>

<span data-ttu-id="9f916-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span><span class="sxs-lookup"><span data-stu-id="9f916-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="9f916-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-v1-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9f916-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-v1-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="9f916-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span><span class="sxs-lookup"><span data-stu-id="9f916-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="9f916-118">You can find the Stream Analytics jobs as follows:</span><span class="sxs-lookup"><span data-stu-id="9f916-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="9f916-119">Go to [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9f916-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f916-120">Navigate to the resource group with the same name as your IoT solution.</span><span class="sxs-lookup"><span data-stu-id="9f916-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="9f916-121">Select the Azure Stream Analytics job you'd like to modify.</span><span class="sxs-lookup"><span data-stu-id="9f916-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="9f916-122">Stop the job by selecting **Stop** in the set of commands.</span><span class="sxs-lookup"><span data-stu-id="9f916-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="9f916-123">Edit the inputs, query, and outputs.</span><span class="sxs-lookup"><span data-stu-id="9f916-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="9f916-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span><span class="sxs-lookup"><span data-stu-id="9f916-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="9f916-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span><span class="sxs-lookup"><span data-stu-id="9f916-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="9f916-126">Start the job</span><span class="sxs-lookup"><span data-stu-id="9f916-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="9f916-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span><span class="sxs-lookup"><span data-stu-id="9f916-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="9f916-128">Add your own rules</span><span class="sxs-lookup"><span data-stu-id="9f916-128">Add your own rules</span></span>

<span data-ttu-id="9f916-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span><span class="sxs-lookup"><span data-stu-id="9f916-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="9f916-130">Customize devices</span><span class="sxs-lookup"><span data-stu-id="9f916-130">Customize devices</span></span>

<span data-ttu-id="9f916-131">One of the most common extension activities is working with devices specific to your scenario.</span><span class="sxs-lookup"><span data-stu-id="9f916-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="9f916-132">There are several methods for working with devices.</span><span class="sxs-lookup"><span data-stu-id="9f916-132">There are several methods for working with devices.</span></span> <span data-ttu-id="9f916-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span><span class="sxs-lookup"><span data-stu-id="9f916-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="9f916-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-v1-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="9f916-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-v1-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="9f916-135">This sample is designed to work with the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="9f916-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="9f916-136">Create your own simulated device</span><span class="sxs-lookup"><span data-stu-id="9f916-136">Create your own simulated device</span></span>

<span data-ttu-id="9f916-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span><span class="sxs-lookup"><span data-stu-id="9f916-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="9f916-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span><span class="sxs-lookup"><span data-stu-id="9f916-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="9f916-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="9f916-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="9f916-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="9f916-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="9f916-141">Available locations for simulated devices</span><span class="sxs-lookup"><span data-stu-id="9f916-141">Available locations for simulated devices</span></span>

<span data-ttu-id="9f916-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span><span class="sxs-lookup"><span data-stu-id="9f916-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="9f916-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="9f916-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="9f916-144">Add a desired property update handler to the simulator</span><span class="sxs-lookup"><span data-stu-id="9f916-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="9f916-145">You can set a value for a desired property for a device in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="9f916-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="9f916-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span><span class="sxs-lookup"><span data-stu-id="9f916-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="9f916-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span><span class="sxs-lookup"><span data-stu-id="9f916-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="9f916-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="9f916-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="9f916-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span><span class="sxs-lookup"><span data-stu-id="9f916-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="9f916-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span><span class="sxs-lookup"><span data-stu-id="9f916-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="9f916-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="9f916-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="9f916-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span><span class="sxs-lookup"><span data-stu-id="9f916-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="9f916-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="9f916-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="9f916-154">Add support for a new method to the simulator</span><span class="sxs-lookup"><span data-stu-id="9f916-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="9f916-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="9f916-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="9f916-156">There are two key steps required:</span><span class="sxs-lookup"><span data-stu-id="9f916-156">There are two key steps required:</span></span>

- <span data-ttu-id="9f916-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span><span class="sxs-lookup"><span data-stu-id="9f916-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="9f916-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span><span class="sxs-lookup"><span data-stu-id="9f916-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="9f916-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9f916-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="9f916-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span><span class="sxs-lookup"><span data-stu-id="9f916-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="9f916-161">You can view this information about devices and invoke methods in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="9f916-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="9f916-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span><span class="sxs-lookup"><span data-stu-id="9f916-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="9f916-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="9f916-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="9f916-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span><span class="sxs-lookup"><span data-stu-id="9f916-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="9f916-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span><span class="sxs-lookup"><span data-stu-id="9f916-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="9f916-166">To delete a method, set the method signature to `null` in the reported properties.</span><span class="sxs-lookup"><span data-stu-id="9f916-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="9f916-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span><span class="sxs-lookup"><span data-stu-id="9f916-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="9f916-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span><span class="sxs-lookup"><span data-stu-id="9f916-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="9f916-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span><span class="sxs-lookup"><span data-stu-id="9f916-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="9f916-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span><span class="sxs-lookup"><span data-stu-id="9f916-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="9f916-171">Add a handler to the simulator code for each method it supports.</span><span class="sxs-lookup"><span data-stu-id="9f916-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="9f916-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span><span class="sxs-lookup"><span data-stu-id="9f916-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="9f916-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span><span class="sxs-lookup"><span data-stu-id="9f916-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="9f916-174">Method handler names must start with `On` followed by the name of the method.</span><span class="sxs-lookup"><span data-stu-id="9f916-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="9f916-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span><span class="sxs-lookup"><span data-stu-id="9f916-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="9f916-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="9f916-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="9f916-177">The **BuildMethodResponse** utility method helps you create the return value.</span><span class="sxs-lookup"><span data-stu-id="9f916-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="9f916-178">Inside the method handler, you could:</span><span class="sxs-lookup"><span data-stu-id="9f916-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="9f916-179">Start an asynchronous task.</span><span class="sxs-lookup"><span data-stu-id="9f916-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="9f916-180">Retrieve desired properties from the *device twin* in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9f916-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="9f916-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span><span class="sxs-lookup"><span data-stu-id="9f916-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="9f916-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span><span class="sxs-lookup"><span data-stu-id="9f916-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="9f916-183">The preceding firmware update example performs the following steps:</span><span class="sxs-lookup"><span data-stu-id="9f916-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="9f916-184">Checks the device is able to accept the firmware update request.</span><span class="sxs-lookup"><span data-stu-id="9f916-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="9f916-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="9f916-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="9f916-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span><span class="sxs-lookup"><span data-stu-id="9f916-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="9f916-187">Build and use your own (physical) device</span><span class="sxs-lookup"><span data-stu-id="9f916-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="9f916-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="9f916-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="9f916-189">Modify dashboard limits</span><span class="sxs-lookup"><span data-stu-id="9f916-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="9f916-190">Number of devices displayed in dashboard dropdown</span><span class="sxs-lookup"><span data-stu-id="9f916-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="9f916-191">The default is 200.</span><span class="sxs-lookup"><span data-stu-id="9f916-191">The default is 200.</span></span> <span data-ttu-id="9f916-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="9f916-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="9f916-193">Number of pins to display in Bing Map control</span><span class="sxs-lookup"><span data-stu-id="9f916-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="9f916-194">The default is 200.</span><span class="sxs-lookup"><span data-stu-id="9f916-194">The default is 200.</span></span> <span data-ttu-id="9f916-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="9f916-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="9f916-196">Time period of telemetry graph</span><span class="sxs-lookup"><span data-stu-id="9f916-196">Time period of telemetry graph</span></span>

<span data-ttu-id="9f916-197">The default is 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="9f916-197">The default is 10 minutes.</span></span> <span data-ttu-id="9f916-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="9f916-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="feedback"></a><span data-ttu-id="9f916-199">Feedback</span><span class="sxs-lookup"><span data-stu-id="9f916-199">Feedback</span></span>

<span data-ttu-id="9f916-200">Do you have a customization you'd like to see covered in this document?</span><span class="sxs-lookup"><span data-stu-id="9f916-200">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="9f916-201">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span><span class="sxs-lookup"><span data-stu-id="9f916-201">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9f916-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f916-202">Next steps</span></span>

<span data-ttu-id="9f916-203">To learn more about the options for customizing the preconfigured solutions, see:</span><span class="sxs-lookup"><span data-stu-id="9f916-203">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="9f916-204">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="9f916-204">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="9f916-205">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="9f916-205">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="9f916-206">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="9f916-206">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="9f916-207">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="9f916-207">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-v1-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-v1-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-v1-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-v1-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]:../iot-accelerators/iot-accelerators-connected-factory-customize.md