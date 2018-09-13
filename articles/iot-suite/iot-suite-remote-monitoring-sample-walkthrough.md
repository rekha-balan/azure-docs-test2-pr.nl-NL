---
title: Remote Monitoring preconfigured solution walkthrough | Microsoft Docs
description: A description of the Azure IoT preconfigured solution remote monitoring and its architecture.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: dobett
ms.openlocfilehash: 53c3c3983044f43326b0bb3fb45c6b51e0540c59
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564270"
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="cf821-103">Remote monitoring preconfigured solution walkthrough</span><span class="sxs-lookup"><span data-stu-id="cf821-103">Remote monitoring preconfigured solution walkthrough</span></span>
## <a name="introduction"></a><span data-ttu-id="cf821-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="cf821-104">Introduction</span></span>
<span data-ttu-id="cf821-105">The IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span><span class="sxs-lookup"><span data-stu-id="cf821-105">The IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="cf821-106">The solution combines key Azure services to provide a generic implementation of the business scenario.</span><span class="sxs-lookup"><span data-stu-id="cf821-106">The solution combines key Azure services to provide a generic implementation of the business scenario.</span></span> <span data-ttu-id="cf821-107">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span><span class="sxs-lookup"><span data-stu-id="cf821-107">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="cf821-108">This article walks you through some of the key elements of the remote monitoring solution to enable you to understand how it works.</span><span class="sxs-lookup"><span data-stu-id="cf821-108">This article walks you through some of the key elements of the remote monitoring solution to enable you to understand how it works.</span></span> <span data-ttu-id="cf821-109">This knowledge helps you to:</span><span class="sxs-lookup"><span data-stu-id="cf821-109">This knowledge helps you to:</span></span>

* <span data-ttu-id="cf821-110">Troubleshoot issues in the solution.</span><span class="sxs-lookup"><span data-stu-id="cf821-110">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="cf821-111">Plan how to customize to the solution to meet your own specific requirements.</span><span class="sxs-lookup"><span data-stu-id="cf821-111">Plan how to customize to the solution to meet your own specific requirements.</span></span> 
* <span data-ttu-id="cf821-112">Design your own IoT solution that uses Azure services.</span><span class="sxs-lookup"><span data-stu-id="cf821-112">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="cf821-113">Logical architecture</span><span class="sxs-lookup"><span data-stu-id="cf821-113">Logical architecture</span></span>
<span data-ttu-id="cf821-114">The following diagram outlines the logical components of the preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="cf821-114">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Logical architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="cf821-116">Simulated devices</span><span class="sxs-lookup"><span data-stu-id="cf821-116">Simulated devices</span></span>
<span data-ttu-id="cf821-117">In the preconfigured solution, the simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span><span class="sxs-lookup"><span data-stu-id="cf821-117">In the preconfigured solution, the simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="cf821-118">When you deploy the preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="cf821-118">When you deploy the preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="cf821-119">The simulated devices make it easy for you to explore the behavior of the solution without the need to deploy any physical devices.</span><span class="sxs-lookup"><span data-stu-id="cf821-119">The simulated devices make it easy for you to explore the behavior of the solution without the need to deploy any physical devices.</span></span> <span data-ttu-id="cf821-120">To deploy a real physical device, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="cf821-120">To deploy a real physical device, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="cf821-121">Device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="cf821-121">Device-to-cloud messages</span></span>
<span data-ttu-id="cf821-122">Each simulated device can send the following message types to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="cf821-122">Each simulated device can send the following message types to IoT Hub:</span></span>

| <span data-ttu-id="cf821-123">Message</span><span class="sxs-lookup"><span data-stu-id="cf821-123">Message</span></span> | <span data-ttu-id="cf821-124">Description</span><span class="sxs-lookup"><span data-stu-id="cf821-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf821-125">Startup</span><span class="sxs-lookup"><span data-stu-id="cf821-125">Startup</span></span> |<span data-ttu-id="cf821-126">When the device starts, it sends a **device-info** message containing information about itself to the back end.</span><span class="sxs-lookup"><span data-stu-id="cf821-126">When the device starts, it sends a **device-info** message containing information about itself to the back end.</span></span> <span data-ttu-id="cf821-127">This data includes the device id and a list of the commands and methods the device supports.</span><span class="sxs-lookup"><span data-stu-id="cf821-127">This data includes the device id and a list of the commands and methods the device supports.</span></span> |
| <span data-ttu-id="cf821-128">Presence</span><span class="sxs-lookup"><span data-stu-id="cf821-128">Presence</span></span> |<span data-ttu-id="cf821-129">A device periodically sends a **presence** message to report whether the device can sense the presence of a sensor.</span><span class="sxs-lookup"><span data-stu-id="cf821-129">A device periodically sends a **presence** message to report whether the device can sense the presence of a sensor.</span></span> |
| <span data-ttu-id="cf821-130">Telemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-130">Telemetry</span></span> |<span data-ttu-id="cf821-131">A device periodically sends a **telemetry** message that reports simulated values for the temperature and humidity collected from the device's simulated sensors.</span><span class="sxs-lookup"><span data-stu-id="cf821-131">A device periodically sends a **telemetry** message that reports simulated values for the temperature and humidity collected from the device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="cf821-132">The solution stores the list of commands supported by the device in a DocumentDB database and not in the device twin.</span><span class="sxs-lookup"><span data-stu-id="cf821-132">The solution stores the list of commands supported by the device in a DocumentDB database and not in the device twin.</span></span>
> 
> 

### <a name="properties-and-device-twins"></a><span data-ttu-id="cf821-133">Properties and device twins</span><span class="sxs-lookup"><span data-stu-id="cf821-133">Properties and device twins</span></span>
<span data-ttu-id="cf821-134">The simulated devices send the following device properties to the [twin][lnk-device-twins] in the IoT hub as *reported properties*.</span><span class="sxs-lookup"><span data-stu-id="cf821-134">The simulated devices send the following device properties to the [twin][lnk-device-twins] in the IoT hub as *reported properties*.</span></span> <span data-ttu-id="cf821-135">The device sends reported properties at startup and in response to a **Change Device State** command or method.</span><span class="sxs-lookup"><span data-stu-id="cf821-135">The device sends reported properties at startup and in response to a **Change Device State** command or method.</span></span>

| <span data-ttu-id="cf821-136">Property</span><span class="sxs-lookup"><span data-stu-id="cf821-136">Property</span></span> | <span data-ttu-id="cf821-137">Purpose</span><span class="sxs-lookup"><span data-stu-id="cf821-137">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="cf821-138">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="cf821-138">Config.TelemetryInterval</span></span> | <span data-ttu-id="cf821-139">Frequency (seconds) the device sends telemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-139">Frequency (seconds) the device sends telemetry</span></span> |
| <span data-ttu-id="cf821-140">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="cf821-140">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="cf821-141">Specifies the mean value for the simulated temperature telemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-141">Specifies the mean value for the simulated temperature telemetry</span></span> |
| <span data-ttu-id="cf821-142">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="cf821-142">Device.DeviceID</span></span> |<span data-ttu-id="cf821-143">Id that is either provided or assigned when a device is created in the solution</span><span class="sxs-lookup"><span data-stu-id="cf821-143">Id that is either provided or assigned when a device is created in the solution</span></span> |
| <span data-ttu-id="cf821-144">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="cf821-144">Device.DeviceState</span></span> | <span data-ttu-id="cf821-145">State reported by the device</span><span class="sxs-lookup"><span data-stu-id="cf821-145">State reported by the device</span></span> |
| <span data-ttu-id="cf821-146">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="cf821-146">Device.CreatedTime</span></span> |<span data-ttu-id="cf821-147">Time the device was created in the solution</span><span class="sxs-lookup"><span data-stu-id="cf821-147">Time the device was created in the solution</span></span> |
| <span data-ttu-id="cf821-148">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="cf821-148">Device.StartupTime</span></span> |<span data-ttu-id="cf821-149">Time the device was started</span><span class="sxs-lookup"><span data-stu-id="cf821-149">Time the device was started</span></span> |
| <span data-ttu-id="cf821-150">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="cf821-150">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="cf821-151">The version number of the last desired property change</span><span class="sxs-lookup"><span data-stu-id="cf821-151">The version number of the last desired property change</span></span> |
| <span data-ttu-id="cf821-152">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="cf821-152">Device.Location.Latitude</span></span> |<span data-ttu-id="cf821-153">Latitude location of the device</span><span class="sxs-lookup"><span data-stu-id="cf821-153">Latitude location of the device</span></span> |
| <span data-ttu-id="cf821-154">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="cf821-154">Device.Location.Longitude</span></span> |<span data-ttu-id="cf821-155">Longitude location of the device</span><span class="sxs-lookup"><span data-stu-id="cf821-155">Longitude location of the device</span></span> |
| <span data-ttu-id="cf821-156">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="cf821-156">System.Manufacturer</span></span> |<span data-ttu-id="cf821-157">Device manufacturer</span><span class="sxs-lookup"><span data-stu-id="cf821-157">Device manufacturer</span></span> |
| <span data-ttu-id="cf821-158">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="cf821-158">System.ModelNumber</span></span> |<span data-ttu-id="cf821-159">Model number of the device</span><span class="sxs-lookup"><span data-stu-id="cf821-159">Model number of the device</span></span> |
| <span data-ttu-id="cf821-160">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="cf821-160">System.SerialNumber</span></span> |<span data-ttu-id="cf821-161">Serial number of the device</span><span class="sxs-lookup"><span data-stu-id="cf821-161">Serial number of the device</span></span> |
| <span data-ttu-id="cf821-162">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="cf821-162">System.FirmwareVersion</span></span> |<span data-ttu-id="cf821-163">Current version of firmware on the device</span><span class="sxs-lookup"><span data-stu-id="cf821-163">Current version of firmware on the device</span></span> |
| <span data-ttu-id="cf821-164">System.Platform</span><span class="sxs-lookup"><span data-stu-id="cf821-164">System.Platform</span></span> |<span data-ttu-id="cf821-165">Platform architecture of the device</span><span class="sxs-lookup"><span data-stu-id="cf821-165">Platform architecture of the device</span></span> |
| <span data-ttu-id="cf821-166">System.Processor</span><span class="sxs-lookup"><span data-stu-id="cf821-166">System.Processor</span></span> |<span data-ttu-id="cf821-167">Processor running the device</span><span class="sxs-lookup"><span data-stu-id="cf821-167">Processor running the device</span></span> |
| <span data-ttu-id="cf821-168">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="cf821-168">System.InstalledRAM</span></span> |<span data-ttu-id="cf821-169">Amount of RAM installed on the device</span><span class="sxs-lookup"><span data-stu-id="cf821-169">Amount of RAM installed on the device</span></span> |

<span data-ttu-id="cf821-170">The simulator seeds these properties in simulated devices with sample values.</span><span class="sxs-lookup"><span data-stu-id="cf821-170">The simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="cf821-171">Each time the simulator initializes a simulated device, the device reports the pre-defined metadata to IoT Hub as reported properties.</span><span class="sxs-lookup"><span data-stu-id="cf821-171">Each time the simulator initializes a simulated device, the device reports the pre-defined metadata to IoT Hub as reported properties.</span></span> <span data-ttu-id="cf821-172">Reported properties can only be updated by the device.</span><span class="sxs-lookup"><span data-stu-id="cf821-172">Reported properties can only be updated by the device.</span></span> <span data-ttu-id="cf821-173">To change a reported property, you set a desired property in solution portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-173">To change a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="cf821-174">It is the responsibility of the device to:</span><span class="sxs-lookup"><span data-stu-id="cf821-174">It is the responsibility of the device to:</span></span>
1. <span data-ttu-id="cf821-175">Periodically retrieve desired properties from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cf821-175">Periodically retrieve desired properties from the IoT hub.</span></span>
2. <span data-ttu-id="cf821-176">Update its configuration with the desired property value.</span><span class="sxs-lookup"><span data-stu-id="cf821-176">Update its configuration with the desired property value.</span></span>
3. <span data-ttu-id="cf821-177">Send the new value back to the hub as a reported property.</span><span class="sxs-lookup"><span data-stu-id="cf821-177">Send the new value back to the hub as a reported property.</span></span>

<span data-ttu-id="cf821-178">From the solution dashboard, you can use *desired properties* to set properties on a device by using the [device twin][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="cf821-178">From the solution dashboard, you can use *desired properties* to set properties on a device by using the [device twin][lnk-device-twins].</span></span> <span data-ttu-id="cf821-179">Typically, a device reads a desired property value from the hub to update its internal state and report the change back as a reported property.</span><span class="sxs-lookup"><span data-stu-id="cf821-179">Typically, a device reads a desired property value from the hub to update its internal state and report the change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="cf821-180">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf821-180">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="cf821-181">All other desired property change requests are ignored in the simulated device.</span><span class="sxs-lookup"><span data-stu-id="cf821-181">All other desired property change requests are ignored in the simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="cf821-182">Methods</span><span class="sxs-lookup"><span data-stu-id="cf821-182">Methods</span></span>
<span data-ttu-id="cf821-183">The simulated devices can handle the following methods ([direct methods][lnk-direct-methods]) invoked from the solution portal through the IoT hub:</span><span class="sxs-lookup"><span data-stu-id="cf821-183">The simulated devices can handle the following methods ([direct methods][lnk-direct-methods]) invoked from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="cf821-184">Method</span><span class="sxs-lookup"><span data-stu-id="cf821-184">Method</span></span> | <span data-ttu-id="cf821-185">Description</span><span class="sxs-lookup"><span data-stu-id="cf821-185">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf821-186">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="cf821-186">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="cf821-187">Instructs the device to perform a firmware update</span><span class="sxs-lookup"><span data-stu-id="cf821-187">Instructs the device to perform a firmware update</span></span> |
| <span data-ttu-id="cf821-188">Reboot</span><span class="sxs-lookup"><span data-stu-id="cf821-188">Reboot</span></span> |<span data-ttu-id="cf821-189">Instructs the device to reboot</span><span class="sxs-lookup"><span data-stu-id="cf821-189">Instructs the device to reboot</span></span> |
| <span data-ttu-id="cf821-190">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="cf821-190">FactoryReset</span></span> |<span data-ttu-id="cf821-191">Instructs the device to perform a factory reset</span><span class="sxs-lookup"><span data-stu-id="cf821-191">Instructs the device to perform a factory reset</span></span> |

<span data-ttu-id="cf821-192">Some methods use reported properties to report on progress.</span><span class="sxs-lookup"><span data-stu-id="cf821-192">Some methods use reported properties to report on progress.</span></span> <span data-ttu-id="cf821-193">For example, the **InitiateFirmwareUpdate** method simulates running the update asynchronously on the device.</span><span class="sxs-lookup"><span data-stu-id="cf821-193">For example, the **InitiateFirmwareUpdate** method simulates running the update asynchronously on the device.</span></span> <span data-ttu-id="cf821-194">The method returns immediately on the device, while the asynchronous task continues to send status updates back to the solution dashboard using reported properties.</span><span class="sxs-lookup"><span data-stu-id="cf821-194">The method returns immediately on the device, while the asynchronous task continues to send status updates back to the solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="cf821-195">Commands</span><span class="sxs-lookup"><span data-stu-id="cf821-195">Commands</span></span> 
<span data-ttu-id="cf821-196">The simulated devices can handle the following commands (cloud-to-device messages) sent from the solution portal through the IoT hub:</span><span class="sxs-lookup"><span data-stu-id="cf821-196">The simulated devices can handle the following commands (cloud-to-device messages) sent from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="cf821-197">Command</span><span class="sxs-lookup"><span data-stu-id="cf821-197">Command</span></span> | <span data-ttu-id="cf821-198">Description</span><span class="sxs-lookup"><span data-stu-id="cf821-198">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf821-199">PingDevice</span><span class="sxs-lookup"><span data-stu-id="cf821-199">PingDevice</span></span> |<span data-ttu-id="cf821-200">Sends a *ping* to the device to check it is alive</span><span class="sxs-lookup"><span data-stu-id="cf821-200">Sends a *ping* to the device to check it is alive</span></span> |
| <span data-ttu-id="cf821-201">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-201">StartTelemetry</span></span> |<span data-ttu-id="cf821-202">Starts the device sending telemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-202">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="cf821-203">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-203">StopTelemetry</span></span> |<span data-ttu-id="cf821-204">Stops the device from sending telemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-204">Stops the device from sending telemetry</span></span> |
| <span data-ttu-id="cf821-205">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="cf821-205">ChangeSetPointTemp</span></span> |<span data-ttu-id="cf821-206">Changes the set point value around which the random data is generated</span><span class="sxs-lookup"><span data-stu-id="cf821-206">Changes the set point value around which the random data is generated</span></span> |
| <span data-ttu-id="cf821-207">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="cf821-207">DiagnosticTelemetry</span></span> |<span data-ttu-id="cf821-208">Triggers the device simulator to send an additional telemetry value (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="cf821-208">Triggers the device simulator to send an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="cf821-209">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="cf821-209">ChangeDeviceState</span></span> |<span data-ttu-id="cf821-210">Changes an extended state property for the device and sends the device info message from the device</span><span class="sxs-lookup"><span data-stu-id="cf821-210">Changes an extended state property for the device and sends the device info message from the device</span></span> |

> [!NOTE]
> <span data-ttu-id="cf821-211">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="cf821-211">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
> 
> 

## <a name="iot-hub"></a><span data-ttu-id="cf821-212">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf821-212">IoT Hub</span></span>
<span data-ttu-id="cf821-213">The [IoT hub][lnk-iothub] ingests data sent from the devices into the cloud and makes it available to the Azure Stream Analytics (ASA) jobs.</span><span class="sxs-lookup"><span data-stu-id="cf821-213">The [IoT hub][lnk-iothub] ingests data sent from the devices into the cloud and makes it available to the Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="cf821-214">Each stream ASA job uses a separate IoT Hub consumer group to read the stream of messages from your devices.</span><span class="sxs-lookup"><span data-stu-id="cf821-214">Each stream ASA job uses a separate IoT Hub consumer group to read the stream of messages from your devices.</span></span>

<span data-ttu-id="cf821-215">The IoT hub in the solution also:</span><span class="sxs-lookup"><span data-stu-id="cf821-215">The IoT hub in the solution also:</span></span>

- <span data-ttu-id="cf821-216">Maintains an identity registry that stores the ids and authentication keys of all the devices permitted to connect to the portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-216">Maintains an identity registry that stores the ids and authentication keys of all the devices permitted to connect to the portal.</span></span> <span data-ttu-id="cf821-217">You can enable and disable devices through the identity registry.</span><span class="sxs-lookup"><span data-stu-id="cf821-217">You can enable and disable devices through the identity registry.</span></span>
- <span data-ttu-id="cf821-218">Sends commands to your devices on behalf of the solution portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-218">Sends commands to your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="cf821-219">Invokes methods on your devices on behalf of the solution portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-219">Invokes methods on your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="cf821-220">Maintains device twins for all registered devices.</span><span class="sxs-lookup"><span data-stu-id="cf821-220">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="cf821-221">A device twin stores the property values reported by a device.</span><span class="sxs-lookup"><span data-stu-id="cf821-221">A device twin stores the property values reported by a device.</span></span> <span data-ttu-id="cf821-222">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span><span class="sxs-lookup"><span data-stu-id="cf821-222">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span></span>
- <span data-ttu-id="cf821-223">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="cf821-223">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="cf821-224">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cf821-224">Azure Stream Analytics</span></span>
<span data-ttu-id="cf821-225">In the remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by the IoT hub to other back-end components for processing or storage.</span><span class="sxs-lookup"><span data-stu-id="cf821-225">In the remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by the IoT hub to other back-end components for processing or storage.</span></span> <span data-ttu-id="cf821-226">Different ASA jobs perform specific functions based on the content of the messages.</span><span class="sxs-lookup"><span data-stu-id="cf821-226">Different ASA jobs perform specific functions based on the content of the messages.</span></span>

<span data-ttu-id="cf821-227">**Job 1: Device Info** filters device information messages from the incoming message stream and sends them to an Event Hub endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf821-227">**Job 1: Device Info** filters device information messages from the incoming message stream and sends them to an Event Hub endpoint.</span></span> <span data-ttu-id="cf821-228">A device sends device information messages at startup and in response to a **SendDeviceInfo** command.</span><span class="sxs-lookup"><span data-stu-id="cf821-228">A device sends device information messages at startup and in response to a **SendDeviceInfo** command.</span></span> <span data-ttu-id="cf821-229">This job uses the following query definition to identify **device-info** messages:</span><span class="sxs-lookup"><span data-stu-id="cf821-229">This job uses the following query definition to identify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="cf821-230">This job sends its output to an Event Hub for further processing.</span><span class="sxs-lookup"><span data-stu-id="cf821-230">This job sends its output to an Event Hub for further processing.</span></span>

<span data-ttu-id="cf821-231">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span><span class="sxs-lookup"><span data-stu-id="cf821-231">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="cf821-232">Threshold values are set in the rules editor available in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-232">Threshold values are set in the rules editor available in the solution portal.</span></span> <span data-ttu-id="cf821-233">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span><span class="sxs-lookup"><span data-stu-id="cf821-233">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="cf821-234">The job compares any non-empty value against the set threshold for the device.</span><span class="sxs-lookup"><span data-stu-id="cf821-234">The job compares any non-empty value against the set threshold for the device.</span></span> <span data-ttu-id="cf821-235">If it exceeds the '>' condition, the job outputs an **alarm** event that indicates that the threshold is exceeded and provides the device, value, and timestamp values.</span><span class="sxs-lookup"><span data-stu-id="cf821-235">If it exceeds the '>' condition, the job outputs an **alarm** event that indicates that the threshold is exceeded and provides the device, value, and timestamp values.</span></span> <span data-ttu-id="cf821-236">This job uses the following query definition to identify telemetry messages that should trigger an alarm:</span><span class="sxs-lookup"><span data-stu-id="cf821-236">This job uses the following query definition to identify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="cf821-237">The job sends its output to an Event Hub for further processing and saves details of each alert to blob storage from where the solution portal can read the alert information.</span><span class="sxs-lookup"><span data-stu-id="cf821-237">The job sends its output to an Event Hub for further processing and saves details of each alert to blob storage from where the solution portal can read the alert information.</span></span>

<span data-ttu-id="cf821-238">**Job 3: Telemetry** operates on the incoming device telemetry stream in two ways.</span><span class="sxs-lookup"><span data-stu-id="cf821-238">**Job 3: Telemetry** operates on the incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="cf821-239">The first sends all telemetry messages from the devices to persistent blob storage for long-term storage.</span><span class="sxs-lookup"><span data-stu-id="cf821-239">The first sends all telemetry messages from the devices to persistent blob storage for long-term storage.</span></span> <span data-ttu-id="cf821-240">The second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data to blob storage.</span><span class="sxs-lookup"><span data-stu-id="cf821-240">The second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data to blob storage.</span></span> <span data-ttu-id="cf821-241">The solution portal reads the telemetry data from blob storage to populate the charts.</span><span class="sxs-lookup"><span data-stu-id="cf821-241">The solution portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="cf821-242">This job uses the following query definition:</span><span class="sxs-lookup"><span data-stu-id="cf821-242">This job uses the following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="cf821-243">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cf821-243">Event Hubs</span></span>
<span data-ttu-id="cf821-244">The **device info** and **rules** ASA jobs output their data to Event Hubs to reliably forward on to the **Event Processor** running in the WebJob.</span><span class="sxs-lookup"><span data-stu-id="cf821-244">The **device info** and **rules** ASA jobs output their data to Event Hubs to reliably forward on to the **Event Processor** running in the WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="cf821-245">Azure storage</span><span class="sxs-lookup"><span data-stu-id="cf821-245">Azure storage</span></span>
<span data-ttu-id="cf821-246">The solution uses Azure blob storage to persist all the raw and summarized telemetry data from the devices in the solution.</span><span class="sxs-lookup"><span data-stu-id="cf821-246">The solution uses Azure blob storage to persist all the raw and summarized telemetry data from the devices in the solution.</span></span> <span data-ttu-id="cf821-247">The portal reads the telemetry data from blob storage to populate the charts.</span><span class="sxs-lookup"><span data-stu-id="cf821-247">The portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="cf821-248">To display alerts, the solution portal reads the data from blob storage that records when telemetry values exceeded the configured threshold values.</span><span class="sxs-lookup"><span data-stu-id="cf821-248">To display alerts, the solution portal reads the data from blob storage that records when telemetry values exceeded the configured threshold values.</span></span> <span data-ttu-id="cf821-249">The solution also uses blob storage to record the threshold values you set in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-249">The solution also uses blob storage to record the threshold values you set in the solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="cf821-250">WebJobs</span><span class="sxs-lookup"><span data-stu-id="cf821-250">WebJobs</span></span>
<span data-ttu-id="cf821-251">In addition to hosting the device simulators, the WebJobs in the solution also host the **Event Processor** running in an Azure WebJob that handles command responses.</span><span class="sxs-lookup"><span data-stu-id="cf821-251">In addition to hosting the device simulators, the WebJobs in the solution also host the **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="cf821-252">It uses command response messages to update the device command history (stored in the DocumentDB database).</span><span class="sxs-lookup"><span data-stu-id="cf821-252">It uses command response messages to update the device command history (stored in the DocumentDB database).</span></span>

## <a name="documentdb"></a><span data-ttu-id="cf821-253">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cf821-253">DocumentDB</span></span>
<span data-ttu-id="cf821-254">The solution uses a DocumentDB database to store information about the devices connected to the solution.</span><span class="sxs-lookup"><span data-stu-id="cf821-254">The solution uses a DocumentDB database to store information about the devices connected to the solution.</span></span> <span data-ttu-id="cf821-255">This information includes the history of commands sent to devices from the solution portal and of methods invoked from the solution portal.</span><span class="sxs-lookup"><span data-stu-id="cf821-255">This information includes the history of commands sent to devices from the solution portal and of methods invoked from the solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="cf821-256">Solution portal</span><span class="sxs-lookup"><span data-stu-id="cf821-256">Solution portal</span></span>

<span data-ttu-id="cf821-257">The solution portal is a web app deployed as part of the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="cf821-257">The solution portal is a web app deployed as part of the preconfigured solution.</span></span> <span data-ttu-id="cf821-258">The key pages in the solution portal are the dashboard and the device list.</span><span class="sxs-lookup"><span data-stu-id="cf821-258">The key pages in the solution portal are the dashboard and the device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="cf821-259">Dashboard</span><span class="sxs-lookup"><span data-stu-id="cf821-259">Dashboard</span></span>
<span data-ttu-id="cf821-260">This page in the web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) to visualize the telemetry data from the devices.</span><span class="sxs-lookup"><span data-stu-id="cf821-260">This page in the web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) to visualize the telemetry data from the devices.</span></span> <span data-ttu-id="cf821-261">The solution uses the ASA telemetry job to write the telemetry data to blob storage.</span><span class="sxs-lookup"><span data-stu-id="cf821-261">The solution uses the ASA telemetry job to write the telemetry data to blob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="cf821-262">Device list</span><span class="sxs-lookup"><span data-stu-id="cf821-262">Device list</span></span>
<span data-ttu-id="cf821-263">From this page in the solution portal you can:</span><span class="sxs-lookup"><span data-stu-id="cf821-263">From this page in the solution portal you can:</span></span>

* <span data-ttu-id="cf821-264">Provision a new device.</span><span class="sxs-lookup"><span data-stu-id="cf821-264">Provision a new device.</span></span> <span data-ttu-id="cf821-265">This action sets the unique device id and generates the authentication key.</span><span class="sxs-lookup"><span data-stu-id="cf821-265">This action sets the unique device id and generates the authentication key.</span></span> <span data-ttu-id="cf821-266">It writes information about the device to both the IoT Hub identity registry and the solution-specific DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="cf821-266">It writes information about the device to both the IoT Hub identity registry and the solution-specific DocumentDB database.</span></span>
* <span data-ttu-id="cf821-267">Manage device properties.</span><span class="sxs-lookup"><span data-stu-id="cf821-267">Manage device properties.</span></span> <span data-ttu-id="cf821-268">This action includes viewing existing properties and updating with new properties.</span><span class="sxs-lookup"><span data-stu-id="cf821-268">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="cf821-269">Send commands to a device.</span><span class="sxs-lookup"><span data-stu-id="cf821-269">Send commands to a device.</span></span>
* <span data-ttu-id="cf821-270">View the command history for a device.</span><span class="sxs-lookup"><span data-stu-id="cf821-270">View the command history for a device.</span></span>
* <span data-ttu-id="cf821-271">Enable and disable devices.</span><span class="sxs-lookup"><span data-stu-id="cf821-271">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf821-272">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf821-272">Next steps</span></span>
<span data-ttu-id="cf821-273">The following TechNet blog posts provide more detail about the remote monitoring preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="cf821-273">The following TechNet blog posts provide more detail about the remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="cf821-274">IoT Suite - Under The Hood - Remote Monitoring</span><span class="sxs-lookup"><span data-stu-id="cf821-274">IoT Suite - Under The Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="cf821-275">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span><span class="sxs-lookup"><span data-stu-id="cf821-275">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="cf821-276">You can continue getting started with IoT Suite by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="cf821-276">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="cf821-277">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="cf821-277">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="cf821-278">[Permissions on the azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="cf821-278">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md