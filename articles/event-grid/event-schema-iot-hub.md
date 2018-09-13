---
title: Azure Event Grid schema for IoT Hub | Microsoft Docs
description: Reference page for the event schema format and properties of IoT Hub
services: iot-hub
documentationcenter: ''
author: kgremban
manager: timlt
editor: ''
ms.service: event-grid
ms.topic: reference
ms.date: 08/17/2018
ms.author: kgremban
ms.openlocfilehash: a86b22b3327b2353dd37a9f9863337d12a009434
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871531"
---
# <a name="azure-event-grid-event-schema-for-iot-hub"></a><span data-ttu-id="27bdb-103">Azure Event Grid event schema for IoT Hub</span><span class="sxs-lookup"><span data-stu-id="27bdb-103">Azure Event Grid event schema for IoT Hub</span></span>

<span data-ttu-id="27bdb-104">This article provides the properties and schema for Azure IoT Hub events.</span><span class="sxs-lookup"><span data-stu-id="27bdb-104">This article provides the properties and schema for Azure IoT Hub events.</span></span> <span data-ttu-id="27bdb-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="27bdb-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span></span> 

<span data-ttu-id="27bdb-106">For a list of sample scripts and tutorials, see [IoT Hub event source](event-sources.md#iot-hub).</span><span class="sxs-lookup"><span data-stu-id="27bdb-106">For a list of sample scripts and tutorials, see [IoT Hub event source](event-sources.md#iot-hub).</span></span>

## <a name="available-event-types"></a><span data-ttu-id="27bdb-107">Available event types</span><span class="sxs-lookup"><span data-stu-id="27bdb-107">Available event types</span></span>

<span data-ttu-id="27bdb-108">Azure IoT Hub emits the following event types:</span><span class="sxs-lookup"><span data-stu-id="27bdb-108">Azure IoT Hub emits the following event types:</span></span>

| <span data-ttu-id="27bdb-109">Event type</span><span class="sxs-lookup"><span data-stu-id="27bdb-109">Event type</span></span> | <span data-ttu-id="27bdb-110">Description</span><span class="sxs-lookup"><span data-stu-id="27bdb-110">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="27bdb-111">Microsoft.Devices.DeviceCreated</span><span class="sxs-lookup"><span data-stu-id="27bdb-111">Microsoft.Devices.DeviceCreated</span></span> | <span data-ttu-id="27bdb-112">Published when a device is registered to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="27bdb-112">Published when a device is registered to an IoT hub.</span></span> |
| <span data-ttu-id="27bdb-113">Microsoft.Devices.DeviceDeleted</span><span class="sxs-lookup"><span data-stu-id="27bdb-113">Microsoft.Devices.DeviceDeleted</span></span> | <span data-ttu-id="27bdb-114">Published when a device is deleted from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="27bdb-114">Published when a device is deleted from an IoT hub.</span></span> | 
| <span data-ttu-id="27bdb-115">Microsoft.Devices.DeviceConnected</span><span class="sxs-lookup"><span data-stu-id="27bdb-115">Microsoft.Devices.DeviceConnected</span></span> | <span data-ttu-id="27bdb-116">Published when a device is connected to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="27bdb-116">Published when a device is connected to an IoT hub.</span></span> |
| <span data-ttu-id="27bdb-117">Microsoft.Devices.DeviceDisconnected</span><span class="sxs-lookup"><span data-stu-id="27bdb-117">Microsoft.Devices.DeviceDisconnected</span></span> | <span data-ttu-id="27bdb-118">Published when a device is disconnected from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="27bdb-118">Published when a device is disconnected from an IoT hub.</span></span> | 

## <a name="example-event"></a><span data-ttu-id="27bdb-119">Example event</span><span class="sxs-lookup"><span data-stu-id="27bdb-119">Example event</span></span>

<span data-ttu-id="27bdb-120">The schema for DeviceConnected and DeviceDisconnected events have the same structure.</span><span class="sxs-lookup"><span data-stu-id="27bdb-120">The schema for DeviceConnected and DeviceDisconnected events have the same structure.</span></span> <span data-ttu-id="27bdb-121">This sample event shows the schema of an event raised when a device is connected to an IoT hub:</span><span class="sxs-lookup"><span data-stu-id="27bdb-121">This sample event shows the schema of an event raised when a device is connected to an IoT hub:</span></span>

```json
[{
  "id": "f6bbf8f4-d365-520d-a878-17bf7238abd8", 
  "topic": "/SUBSCRIPTIONS/<subscription ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/<hub name>", 
  "subject": "devices/LogicAppTestDevice", 
  "eventType": "Microsoft.Devices.DeviceConnected", 
  "eventTime": "2018-06-02T19:17:44.4383997Z", 
  "data": {
    "deviceConnectionStateEventInfo": {
      "sequenceNumber":
        "000000000000000001D4132452F67CE200000002000000000000000000000001"
    },
    "hubName": "egtesthub1",
    "deviceId": "LogicAppTestDevice",
    "moduleId" : "DeviceModuleID"
  }, 
  "dataVersion": "1", 
  "metadataVersion": "1" 
}]
```

<span data-ttu-id="27bdb-122">The schema for DeviceCreated and DeviceDeleted events have the same structure.</span><span class="sxs-lookup"><span data-stu-id="27bdb-122">The schema for DeviceCreated and DeviceDeleted events have the same structure.</span></span> <span data-ttu-id="27bdb-123">This sample event shows the schema of an event raised when a device is registered to an IoT hub:</span><span class="sxs-lookup"><span data-stu-id="27bdb-123">This sample event shows the schema of an event raised when a device is registered to an IoT hub:</span></span>

```json
[{
  "id": "56afc886-767b-d359-d59e-0da7877166b2",
  "topic": "/SUBSCRIPTIONS/<subscription ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/<hub name>",
  "subject": "devices/LogicAppTestDevice",
  "eventType": "Microsoft.Devices.DeviceCreated",
  "eventTime": "2018-01-02T19:17:44.4383997Z",
  "data": {
    "twin": {
      "deviceId": "LogicAppTestDevice",
      "etag": "AAAAAAAAAAE=",
      "deviceEtag": "null",
      "status": "enabled",
      "statusUpdateTime": "0001-01-01T00:00:00",
      "connectionState": "Disconnected",
      "lastActivityTime": "0001-01-01T00:00:00",
      "cloudToDeviceMessageCount": 0,
      "authenticationType": "sas",
      "x509Thumbprint": {
        "primaryThumbprint": null,
        "secondaryThumbprint": null
      },
      "version": 2,
      "properties": {
        "desired": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        },
        "reported": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        }
      }
    },
    "hubName": "egtesthub1",
    "deviceId": "LogicAppTestDevice"
  },
  "dataVersion": "1",
  "metadataVersion": "1"
}]
```

### <a name="event-properties"></a><span data-ttu-id="27bdb-124">Event properties</span><span class="sxs-lookup"><span data-stu-id="27bdb-124">Event properties</span></span>

<span data-ttu-id="27bdb-125">All events contain the same top-level data:</span><span class="sxs-lookup"><span data-stu-id="27bdb-125">All events contain the same top-level data:</span></span> 

| <span data-ttu-id="27bdb-126">Property</span><span class="sxs-lookup"><span data-stu-id="27bdb-126">Property</span></span> | <span data-ttu-id="27bdb-127">Type</span><span class="sxs-lookup"><span data-stu-id="27bdb-127">Type</span></span> | <span data-ttu-id="27bdb-128">Description</span><span class="sxs-lookup"><span data-stu-id="27bdb-128">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="27bdb-129">id</span><span class="sxs-lookup"><span data-stu-id="27bdb-129">id</span></span> | <span data-ttu-id="27bdb-130">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-130">string</span></span> | <span data-ttu-id="27bdb-131">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="27bdb-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="27bdb-132">topic</span><span class="sxs-lookup"><span data-stu-id="27bdb-132">topic</span></span> | <span data-ttu-id="27bdb-133">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-133">string</span></span> | <span data-ttu-id="27bdb-134">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="27bdb-134">Full resource path to the event source.</span></span> <span data-ttu-id="27bdb-135">This field is not writeable.</span><span class="sxs-lookup"><span data-stu-id="27bdb-135">This field is not writeable.</span></span> <span data-ttu-id="27bdb-136">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="27bdb-136">Event Grid provides this value.</span></span> |
| <span data-ttu-id="27bdb-137">subject</span><span class="sxs-lookup"><span data-stu-id="27bdb-137">subject</span></span> | <span data-ttu-id="27bdb-138">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-138">string</span></span> | <span data-ttu-id="27bdb-139">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="27bdb-139">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="27bdb-140">eventType</span><span class="sxs-lookup"><span data-stu-id="27bdb-140">eventType</span></span> | <span data-ttu-id="27bdb-141">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-141">string</span></span> | <span data-ttu-id="27bdb-142">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="27bdb-142">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="27bdb-143">eventTime</span><span class="sxs-lookup"><span data-stu-id="27bdb-143">eventTime</span></span> | <span data-ttu-id="27bdb-144">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-144">string</span></span> | <span data-ttu-id="27bdb-145">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="27bdb-145">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="27bdb-146">data</span><span class="sxs-lookup"><span data-stu-id="27bdb-146">data</span></span> | <span data-ttu-id="27bdb-147">object</span><span class="sxs-lookup"><span data-stu-id="27bdb-147">object</span></span> | <span data-ttu-id="27bdb-148">IoT Hub event data.</span><span class="sxs-lookup"><span data-stu-id="27bdb-148">IoT Hub event data.</span></span>  |
| <span data-ttu-id="27bdb-149">dataVersion</span><span class="sxs-lookup"><span data-stu-id="27bdb-149">dataVersion</span></span> | <span data-ttu-id="27bdb-150">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-150">string</span></span> | <span data-ttu-id="27bdb-151">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="27bdb-151">The schema version of the data object.</span></span> <span data-ttu-id="27bdb-152">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="27bdb-152">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="27bdb-153">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="27bdb-153">metadataVersion</span></span> | <span data-ttu-id="27bdb-154">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-154">string</span></span> | <span data-ttu-id="27bdb-155">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="27bdb-155">The schema version of the event metadata.</span></span> <span data-ttu-id="27bdb-156">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="27bdb-156">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="27bdb-157">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="27bdb-157">Event Grid provides this value.</span></span> |

<span data-ttu-id="27bdb-158">For all IoT Hub events, the data object contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="27bdb-158">For all IoT Hub events, the data object contains the following properties:</span></span>

| <span data-ttu-id="27bdb-159">Property</span><span class="sxs-lookup"><span data-stu-id="27bdb-159">Property</span></span> | <span data-ttu-id="27bdb-160">Type</span><span class="sxs-lookup"><span data-stu-id="27bdb-160">Type</span></span> | <span data-ttu-id="27bdb-161">Description</span><span class="sxs-lookup"><span data-stu-id="27bdb-161">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="27bdb-162">hubName</span><span class="sxs-lookup"><span data-stu-id="27bdb-162">hubName</span></span> | <span data-ttu-id="27bdb-163">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-163">string</span></span> | <span data-ttu-id="27bdb-164">Name of the IoT Hub where the device was created or deleted.</span><span class="sxs-lookup"><span data-stu-id="27bdb-164">Name of the IoT Hub where the device was created or deleted.</span></span> |
| <span data-ttu-id="27bdb-165">deviceId</span><span class="sxs-lookup"><span data-stu-id="27bdb-165">deviceId</span></span> | <span data-ttu-id="27bdb-166">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-166">string</span></span> | <span data-ttu-id="27bdb-167">The unique identifier of the device.</span><span class="sxs-lookup"><span data-stu-id="27bdb-167">The unique identifier of the device.</span></span> <span data-ttu-id="27bdb-168">This case-sensitive string can be up to 128 characters long, and supports ASCII 7-bit alphanumeric characters plus the following special characters: `- : . + % _ # * ? ! ( ) , = @ ; $ '`.</span><span class="sxs-lookup"><span data-stu-id="27bdb-168">This case-sensitive string can be up to 128 characters long, and supports ASCII 7-bit alphanumeric characters plus the following special characters: `- : . + % _ # * ? ! ( ) , = @ ; $ '`.</span></span> |

<span data-ttu-id="27bdb-169">The contents of the data object are different for each event publisher.</span><span class="sxs-lookup"><span data-stu-id="27bdb-169">The contents of the data object are different for each event publisher.</span></span> <span data-ttu-id="27bdb-170">For **Device Connected** and **Device Disconnected** IoT Hub events, the data object contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="27bdb-170">For **Device Connected** and **Device Disconnected** IoT Hub events, the data object contains the following properties:</span></span>

| <span data-ttu-id="27bdb-171">Property</span><span class="sxs-lookup"><span data-stu-id="27bdb-171">Property</span></span> | <span data-ttu-id="27bdb-172">Type</span><span class="sxs-lookup"><span data-stu-id="27bdb-172">Type</span></span> | <span data-ttu-id="27bdb-173">Description</span><span class="sxs-lookup"><span data-stu-id="27bdb-173">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="27bdb-174">moduleId</span><span class="sxs-lookup"><span data-stu-id="27bdb-174">moduleId</span></span> | <span data-ttu-id="27bdb-175">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-175">string</span></span> | <span data-ttu-id="27bdb-176">The unique identifier of the module.</span><span class="sxs-lookup"><span data-stu-id="27bdb-176">The unique identifier of the module.</span></span> <span data-ttu-id="27bdb-177">This field is output only for module devices.</span><span class="sxs-lookup"><span data-stu-id="27bdb-177">This field is output only for module devices.</span></span> <span data-ttu-id="27bdb-178">This case-sensitive string can be up to 128 characters long, and supports ASCII 7-bit alphanumeric characters plus the following special characters: `- : . + % _ # * ? ! ( ) , = @ ; $ '`.</span><span class="sxs-lookup"><span data-stu-id="27bdb-178">This case-sensitive string can be up to 128 characters long, and supports ASCII 7-bit alphanumeric characters plus the following special characters: `- : . + % _ # * ? ! ( ) , = @ ; $ '`.</span></span> |
| <span data-ttu-id="27bdb-179">deviceConnectionStateEventInfo</span><span class="sxs-lookup"><span data-stu-id="27bdb-179">deviceConnectionStateEventInfo</span></span> | <span data-ttu-id="27bdb-180">object</span><span class="sxs-lookup"><span data-stu-id="27bdb-180">object</span></span> | <span data-ttu-id="27bdb-181">Device connection state event information</span><span class="sxs-lookup"><span data-stu-id="27bdb-181">Device connection state event information</span></span>
| <span data-ttu-id="27bdb-182">sequenceNumber</span><span class="sxs-lookup"><span data-stu-id="27bdb-182">sequenceNumber</span></span> | <span data-ttu-id="27bdb-183">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-183">string</span></span> | <span data-ttu-id="27bdb-184">A number which helps indicate order of device connected or device disconnected events.</span><span class="sxs-lookup"><span data-stu-id="27bdb-184">A number which helps indicate order of device connected or device disconnected events.</span></span> <span data-ttu-id="27bdb-185">Latest event will have a sequence number that is higher than the previous event.</span><span class="sxs-lookup"><span data-stu-id="27bdb-185">Latest event will have a sequence number that is higher than the previous event.</span></span> <span data-ttu-id="27bdb-186">This number may change by more than 1, but is strictly increasing.</span><span class="sxs-lookup"><span data-stu-id="27bdb-186">This number may change by more than 1, but is strictly increasing.</span></span> <span data-ttu-id="27bdb-187">See [how to use sequence number](../iot-hub/iot-hub-how-to-order-connection-state-events.md).</span><span class="sxs-lookup"><span data-stu-id="27bdb-187">See [how to use sequence number](../iot-hub/iot-hub-how-to-order-connection-state-events.md).</span></span> |

<span data-ttu-id="27bdb-188">The contents of the data object are different for each event publisher.</span><span class="sxs-lookup"><span data-stu-id="27bdb-188">The contents of the data object are different for each event publisher.</span></span> <span data-ttu-id="27bdb-189">For **Device Created** and **Device Deleted** IoT Hub events, the data object contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="27bdb-189">For **Device Created** and **Device Deleted** IoT Hub events, the data object contains the following properties:</span></span>

| <span data-ttu-id="27bdb-190">Property</span><span class="sxs-lookup"><span data-stu-id="27bdb-190">Property</span></span> | <span data-ttu-id="27bdb-191">Type</span><span class="sxs-lookup"><span data-stu-id="27bdb-191">Type</span></span> | <span data-ttu-id="27bdb-192">Description</span><span class="sxs-lookup"><span data-stu-id="27bdb-192">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="27bdb-193">twin</span><span class="sxs-lookup"><span data-stu-id="27bdb-193">twin</span></span> | <span data-ttu-id="27bdb-194">object</span><span class="sxs-lookup"><span data-stu-id="27bdb-194">object</span></span> | <span data-ttu-id="27bdb-195">Information about the device twin, which is the cloud represenation of application device metadata.</span><span class="sxs-lookup"><span data-stu-id="27bdb-195">Information about the device twin, which is the cloud represenation of application device metadata.</span></span> | 
| <span data-ttu-id="27bdb-196">deviceID</span><span class="sxs-lookup"><span data-stu-id="27bdb-196">deviceID</span></span> | <span data-ttu-id="27bdb-197">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-197">string</span></span> | <span data-ttu-id="27bdb-198">The unique identifier of the device twin.</span><span class="sxs-lookup"><span data-stu-id="27bdb-198">The unique identifier of the device twin.</span></span> | 
| <span data-ttu-id="27bdb-199">etag</span><span class="sxs-lookup"><span data-stu-id="27bdb-199">etag</span></span> | <span data-ttu-id="27bdb-200">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-200">string</span></span> | <span data-ttu-id="27bdb-201">A validator for ensuring consistency of updates to a device twin.</span><span class="sxs-lookup"><span data-stu-id="27bdb-201">A validator for ensuring consistency of updates to a device twin.</span></span> <span data-ttu-id="27bdb-202">Each etag is guaranteed to be unique per device twin.</span><span class="sxs-lookup"><span data-stu-id="27bdb-202">Each etag is guaranteed to be unique per device twin.</span></span> |  
| <span data-ttu-id="27bdb-203">deviceEtag</span><span class="sxs-lookup"><span data-stu-id="27bdb-203">deviceEtag</span></span>| <span data-ttu-id="27bdb-204">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-204">string</span></span> | <span data-ttu-id="27bdb-205">A validator for ensuring consistency of updates to a device registry.</span><span class="sxs-lookup"><span data-stu-id="27bdb-205">A validator for ensuring consistency of updates to a device registry.</span></span> <span data-ttu-id="27bdb-206">Each deviceEtag is guaranteed to be unique per device registry.</span><span class="sxs-lookup"><span data-stu-id="27bdb-206">Each deviceEtag is guaranteed to be unique per device registry.</span></span> |
| <span data-ttu-id="27bdb-207">status</span><span class="sxs-lookup"><span data-stu-id="27bdb-207">status</span></span> | <span data-ttu-id="27bdb-208">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-208">string</span></span> | <span data-ttu-id="27bdb-209">Whether the device twin is enabled or disabled.</span><span class="sxs-lookup"><span data-stu-id="27bdb-209">Whether the device twin is enabled or disabled.</span></span> | 
| <span data-ttu-id="27bdb-210">statusUpdateTime</span><span class="sxs-lookup"><span data-stu-id="27bdb-210">statusUpdateTime</span></span> | <span data-ttu-id="27bdb-211">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-211">string</span></span> | <span data-ttu-id="27bdb-212">The ISO8601 timestamp of the last device twin status update.</span><span class="sxs-lookup"><span data-stu-id="27bdb-212">The ISO8601 timestamp of the last device twin status update.</span></span> |
| <span data-ttu-id="27bdb-213">connectionState</span><span class="sxs-lookup"><span data-stu-id="27bdb-213">connectionState</span></span> | <span data-ttu-id="27bdb-214">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-214">string</span></span> | <span data-ttu-id="27bdb-215">Whether the device is connected or disconnected.</span><span class="sxs-lookup"><span data-stu-id="27bdb-215">Whether the device is connected or disconnected.</span></span> | 
| <span data-ttu-id="27bdb-216">lastActivityTime</span><span class="sxs-lookup"><span data-stu-id="27bdb-216">lastActivityTime</span></span> | <span data-ttu-id="27bdb-217">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-217">string</span></span> | <span data-ttu-id="27bdb-218">The ISO8601 timestamp of the last activity.</span><span class="sxs-lookup"><span data-stu-id="27bdb-218">The ISO8601 timestamp of the last activity.</span></span> | 
| <span data-ttu-id="27bdb-219">cloudToDeviceMessageCount</span><span class="sxs-lookup"><span data-stu-id="27bdb-219">cloudToDeviceMessageCount</span></span> | <span data-ttu-id="27bdb-220">integer</span><span class="sxs-lookup"><span data-stu-id="27bdb-220">integer</span></span> | <span data-ttu-id="27bdb-221">Count of cloud to device messages sent to this device.</span><span class="sxs-lookup"><span data-stu-id="27bdb-221">Count of cloud to device messages sent to this device.</span></span> | 
| <span data-ttu-id="27bdb-222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="27bdb-222">authenticationType</span></span> | <span data-ttu-id="27bdb-223">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-223">string</span></span> | <span data-ttu-id="27bdb-224">Authentication type used for this device: either `SAS`, `SelfSigned`, or `CertificateAuthority`.</span><span class="sxs-lookup"><span data-stu-id="27bdb-224">Authentication type used for this device: either `SAS`, `SelfSigned`, or `CertificateAuthority`.</span></span> |
| <span data-ttu-id="27bdb-225">x509Thumbprint</span><span class="sxs-lookup"><span data-stu-id="27bdb-225">x509Thumbprint</span></span> | <span data-ttu-id="27bdb-226">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-226">string</span></span> | <span data-ttu-id="27bdb-227">The thumbprint is a unique value for the x509 certificate, commonly used to find a particular certificate in a certificate store.</span><span class="sxs-lookup"><span data-stu-id="27bdb-227">The thumbprint is a unique value for the x509 certificate, commonly used to find a particular certificate in a certificate store.</span></span> <span data-ttu-id="27bdb-228">The thumbprint is dynamically generated using the SHA1 algorithm, and does not physically exist in the certificate.</span><span class="sxs-lookup"><span data-stu-id="27bdb-228">The thumbprint is dynamically generated using the SHA1 algorithm, and does not physically exist in the certificate.</span></span> | 
| <span data-ttu-id="27bdb-229">primaryThumbprint</span><span class="sxs-lookup"><span data-stu-id="27bdb-229">primaryThumbprint</span></span> | <span data-ttu-id="27bdb-230">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-230">string</span></span> | <span data-ttu-id="27bdb-231">Primary thumbprint for the x509 certificate.</span><span class="sxs-lookup"><span data-stu-id="27bdb-231">Primary thumbprint for the x509 certificate.</span></span> |
| <span data-ttu-id="27bdb-232">secondaryThumbprint</span><span class="sxs-lookup"><span data-stu-id="27bdb-232">secondaryThumbprint</span></span> | <span data-ttu-id="27bdb-233">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-233">string</span></span> | <span data-ttu-id="27bdb-234">Secondary thumbprint for the x509 certificate.</span><span class="sxs-lookup"><span data-stu-id="27bdb-234">Secondary thumbprint for the x509 certificate.</span></span> | 
| <span data-ttu-id="27bdb-235">version</span><span class="sxs-lookup"><span data-stu-id="27bdb-235">version</span></span> | <span data-ttu-id="27bdb-236">integer</span><span class="sxs-lookup"><span data-stu-id="27bdb-236">integer</span></span> | <span data-ttu-id="27bdb-237">An integer that is incremented by one each time the device twin is updated.</span><span class="sxs-lookup"><span data-stu-id="27bdb-237">An integer that is incremented by one each time the device twin is updated.</span></span> |
| <span data-ttu-id="27bdb-238">desired</span><span class="sxs-lookup"><span data-stu-id="27bdb-238">desired</span></span> | <span data-ttu-id="27bdb-239">object</span><span class="sxs-lookup"><span data-stu-id="27bdb-239">object</span></span> | <span data-ttu-id="27bdb-240">A portion of the properties that can be written only by the application back-end, and read by the device.</span><span class="sxs-lookup"><span data-stu-id="27bdb-240">A portion of the properties that can be written only by the application back-end, and read by the device.</span></span> | 
| <span data-ttu-id="27bdb-241">reported</span><span class="sxs-lookup"><span data-stu-id="27bdb-241">reported</span></span> | <span data-ttu-id="27bdb-242">object</span><span class="sxs-lookup"><span data-stu-id="27bdb-242">object</span></span> | <span data-ttu-id="27bdb-243">A portion of the properties that can be written only by the device, and read by the application back-end.</span><span class="sxs-lookup"><span data-stu-id="27bdb-243">A portion of the properties that can be written only by the device, and read by the application back-end.</span></span> |
| <span data-ttu-id="27bdb-244">lastUpdated</span><span class="sxs-lookup"><span data-stu-id="27bdb-244">lastUpdated</span></span> | <span data-ttu-id="27bdb-245">string</span><span class="sxs-lookup"><span data-stu-id="27bdb-245">string</span></span> | <span data-ttu-id="27bdb-246">The ISO8601 timestamp of the last device twin property update.</span><span class="sxs-lookup"><span data-stu-id="27bdb-246">The ISO8601 timestamp of the last device twin property update.</span></span> | 

## <a name="next-steps"></a><span data-ttu-id="27bdb-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="27bdb-247">Next steps</span></span>

* <span data-ttu-id="27bdb-248">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="27bdb-248">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="27bdb-249">To learn about how IoT Hub and Event Grid work together, see [React to IoT Hub events by using Event Grid to trigger actions](../iot-hub/iot-hub-event-grid.md).</span><span class="sxs-lookup"><span data-stu-id="27bdb-249">To learn about how IoT Hub and Event Grid work together, see [React to IoT Hub events by using Event Grid to trigger actions](../iot-hub/iot-hub-event-grid.md).</span></span>