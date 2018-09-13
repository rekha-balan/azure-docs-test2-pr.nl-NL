---
title: Device information metadata in the remote monitoring solution | Microsoft Docs
description: A description of the Azure IoT preconfigured solution remote monitoring and its architecture.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: dobett
ms.openlocfilehash: 799947677326dd44df120090c06e74f4ede100d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551280"
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="11041-103">Device information metadata in the remote monitoring preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="11041-103">Device information metadata in the remote monitoring preconfigured solution</span></span>
<span data-ttu-id="11041-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span><span class="sxs-lookup"><span data-stu-id="11041-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="11041-105">This article outlines the approach this solution takes to enable you to understand:</span><span class="sxs-lookup"><span data-stu-id="11041-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="11041-106">What device metadata the solution stores.</span><span class="sxs-lookup"><span data-stu-id="11041-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="11041-107">How the solution manages the device metadata.</span><span class="sxs-lookup"><span data-stu-id="11041-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="11041-108">Context</span><span class="sxs-lookup"><span data-stu-id="11041-108">Context</span></span>
<span data-ttu-id="11041-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="11041-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="11041-110">The solution stores information about devices in three different locations:</span><span class="sxs-lookup"><span data-stu-id="11041-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="11041-111">Location</span><span class="sxs-lookup"><span data-stu-id="11041-111">Location</span></span> | <span data-ttu-id="11041-112">Information stored</span><span class="sxs-lookup"><span data-stu-id="11041-112">Information stored</span></span> | <span data-ttu-id="11041-113">Implementation</span><span class="sxs-lookup"><span data-stu-id="11041-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="11041-114">Identity registry</span><span class="sxs-lookup"><span data-stu-id="11041-114">Identity registry</span></span> | <span data-ttu-id="11041-115">Device id, authentication keys, enabled state</span><span class="sxs-lookup"><span data-stu-id="11041-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="11041-116">Built in to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="11041-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="11041-117">Device twins</span><span class="sxs-lookup"><span data-stu-id="11041-117">Device twins</span></span> | <span data-ttu-id="11041-118">Metadata: reported properties, desired properties, tags</span><span class="sxs-lookup"><span data-stu-id="11041-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="11041-119">Built in to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="11041-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="11041-120">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="11041-120">DocumentDB</span></span> | <span data-ttu-id="11041-121">Command and method history</span><span class="sxs-lookup"><span data-stu-id="11041-121">Command and method history</span></span> | <span data-ttu-id="11041-122">Custom for solution</span><span class="sxs-lookup"><span data-stu-id="11041-122">Custom for solution</span></span> |

<span data-ttu-id="11041-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span><span class="sxs-lookup"><span data-stu-id="11041-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="11041-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span><span class="sxs-lookup"><span data-stu-id="11041-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="11041-125">The remote monitoring solution uses a [DocumentDB][lnk-docdb] database to implement a custom store for command and method history.</span><span class="sxs-lookup"><span data-stu-id="11041-125">The remote monitoring solution uses a [DocumentDB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="11041-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="11041-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the DocumentDB database.</span></span> <span data-ttu-id="11041-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="11041-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>
> 
> 

## <a name="device-metadata"></a><span data-ttu-id="11041-128">Device metadata</span><span class="sxs-lookup"><span data-stu-id="11041-128">Device metadata</span></span>
<span data-ttu-id="11041-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="11041-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="11041-130">The solution uses device twins to manage the metadata associated with devices.</span><span class="sxs-lookup"><span data-stu-id="11041-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="11041-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span><span class="sxs-lookup"><span data-stu-id="11041-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="11041-132">A device twin stores three types of metadata:</span><span class="sxs-lookup"><span data-stu-id="11041-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="11041-133">*Reported properties* are sent to an IoT hub by a device.</span><span class="sxs-lookup"><span data-stu-id="11041-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="11041-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span><span class="sxs-lookup"><span data-stu-id="11041-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="11041-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="11041-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="11041-136">Reported properties are read only.</span><span class="sxs-lookup"><span data-stu-id="11041-136">Reported properties are read only.</span></span>
- <span data-ttu-id="11041-137">*Desired properties* are retrieved from the IoT hub by devices.</span><span class="sxs-lookup"><span data-stu-id="11041-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="11041-138">It is the responsibility of the device to make any necessary configuration change on the device.</span><span class="sxs-lookup"><span data-stu-id="11041-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="11041-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span><span class="sxs-lookup"><span data-stu-id="11041-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="11041-140">You can set a desired property value through the solution portal.</span><span class="sxs-lookup"><span data-stu-id="11041-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="11041-141">*Tags* only exist in the device twin and are never synchronized with a device.</span><span class="sxs-lookup"><span data-stu-id="11041-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="11041-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span><span class="sxs-lookup"><span data-stu-id="11041-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="11041-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="11041-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="11041-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span><span class="sxs-lookup"><span data-stu-id="11041-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="11041-145">Simulated devices also return the list of supported methods as a reported property.</span><span class="sxs-lookup"><span data-stu-id="11041-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="11041-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="11041-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="11041-147">All other desired property change requests are ignored.</span><span class="sxs-lookup"><span data-stu-id="11041-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="11041-148">A device information metadata JSON document stored in the device registry DocumentDB database has the following structure:</span><span class="sxs-lookup"><span data-stu-id="11041-148">A device information metadata JSON document stored in the device registry DocumentDB database has the following structure:</span></span>

```
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```


> [!NOTE]
> <span data-ttu-id="11041-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="11041-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="11041-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="11041-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>
> 
> 

## <a name="lifecycle"></a><span data-ttu-id="11041-151">Lifecycle</span><span class="sxs-lookup"><span data-stu-id="11041-151">Lifecycle</span></span>
<span data-ttu-id="11041-152">When you first create a device in the solution portal, the solution creates an entry in the DocumentDB database to store command and method history.</span><span class="sxs-lookup"><span data-stu-id="11041-152">When you first create a device in the solution portal, the solution creates an entry in the DocumentDB database to store command and method history.</span></span> <span data-ttu-id="11041-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="11041-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="11041-154">It also creates a device twin.</span><span class="sxs-lookup"><span data-stu-id="11041-154">It also creates a device twin.</span></span>

<span data-ttu-id="11041-155">When a device first connects to the solution, it sends reported properties and a device information message.</span><span class="sxs-lookup"><span data-stu-id="11041-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="11041-156">The reported property values are automatically saved in the device twin.</span><span class="sxs-lookup"><span data-stu-id="11041-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="11041-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span><span class="sxs-lookup"><span data-stu-id="11041-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="11041-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span><span class="sxs-lookup"><span data-stu-id="11041-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="11041-159">When the solution receives this message, it updates the device information in the DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="11041-159">When the solution receives this message, it updates the device information in the DocumentDB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="11041-160">View and edit device information in the solution portal</span><span class="sxs-lookup"><span data-stu-id="11041-160">View and edit device information in the solution portal</span></span>
<span data-ttu-id="11041-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span><span class="sxs-lookup"><span data-stu-id="11041-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="11041-162">You can customize the columns by clicking **Column editor**.</span><span class="sxs-lookup"><span data-stu-id="11041-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="11041-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="11041-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Column editor in device list][img-device-list]

<span data-ttu-id="11041-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span><span class="sxs-lookup"><span data-stu-id="11041-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Device deatils pane][img-device-edit]

<span data-ttu-id="11041-167">You can use the solution portal to remove a device from your solution.</span><span class="sxs-lookup"><span data-stu-id="11041-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="11041-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span><span class="sxs-lookup"><span data-stu-id="11041-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="11041-169">The solution also removes information related to the device from the DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="11041-169">The solution also removes information related to the device from the DocumentDB database.</span></span> <span data-ttu-id="11041-170">Before you can remove a device, you must disable it.</span><span class="sxs-lookup"><span data-stu-id="11041-170">Before you can remove a device, you must disable it.</span></span>

![Remove device][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="11041-172">Device information message processing</span><span class="sxs-lookup"><span data-stu-id="11041-172">Device information message processing</span></span>
<span data-ttu-id="11041-173">Device information messages sent by a device are distinct from telemetry messages.</span><span class="sxs-lookup"><span data-stu-id="11041-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="11041-174">Device information messages include the commands a device can respond to, and any command history.</span><span class="sxs-lookup"><span data-stu-id="11041-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="11041-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span><span class="sxs-lookup"><span data-stu-id="11041-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="11041-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="11041-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="11041-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span><span class="sxs-lookup"><span data-stu-id="11041-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="11041-178">Logic in the **EventProcessorHost** instance uses the device id to find the DocumentDB record for the specific device and update the record.</span><span class="sxs-lookup"><span data-stu-id="11041-178">Logic in the **EventProcessorHost** instance uses the device id to find the DocumentDB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="11041-179">A device information message is a standard device-to-cloud message.</span><span class="sxs-lookup"><span data-stu-id="11041-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="11041-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span><span class="sxs-lookup"><span data-stu-id="11041-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="11041-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="11041-181">Next steps</span></span>
<span data-ttu-id="11041-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="11041-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="11041-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="11041-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="11041-184">[Frequently asked questions for IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="11041-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="11041-185">[IoT security from the ground up][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="11041-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md



