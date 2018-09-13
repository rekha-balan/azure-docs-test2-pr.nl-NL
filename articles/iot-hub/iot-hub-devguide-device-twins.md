---
title: Understand Azure IoT Hub device twins | Microsoft Docs
description: Developer guide - use device twins to synchronize state and configuration data between IoT Hub and your devices
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: ''
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 031cd45e27d6ae3b2d0d06820deacffac7fa465b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550469"
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="4eb58-103">Understand and use device twins in IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4eb58-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="4eb58-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4eb58-104">Overview</span></span>
<span data-ttu-id="4eb58-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span><span class="sxs-lookup"><span data-stu-id="4eb58-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="4eb58-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4eb58-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="4eb58-107">This article describes:</span><span class="sxs-lookup"><span data-stu-id="4eb58-107">This article describes:</span></span>

* <span data-ttu-id="4eb58-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span><span class="sxs-lookup"><span data-stu-id="4eb58-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="4eb58-109">The operations that device apps and back ends can perform on device twins.</span><span class="sxs-lookup"><span data-stu-id="4eb58-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="4eb58-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="4eb58-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="4eb58-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span><span class="sxs-lookup"><span data-stu-id="4eb58-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="4eb58-112">When to use</span><span class="sxs-lookup"><span data-stu-id="4eb58-112">When to use</span></span>
<span data-ttu-id="4eb58-113">Use device twins to:</span><span class="sxs-lookup"><span data-stu-id="4eb58-113">Use device twins to:</span></span>

* <span data-ttu-id="4eb58-114">Store device-specific metadata in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4eb58-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="4eb58-115">For example, the deployment location of a vending machine.</span><span class="sxs-lookup"><span data-stu-id="4eb58-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="4eb58-116">Report current state information such as available capabilities and conditions from your device app.</span><span class="sxs-lookup"><span data-stu-id="4eb58-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="4eb58-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span><span class="sxs-lookup"><span data-stu-id="4eb58-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="4eb58-118">Synchronize the state of long-running workflows between device app and back-end app.</span><span class="sxs-lookup"><span data-stu-id="4eb58-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="4eb58-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span><span class="sxs-lookup"><span data-stu-id="4eb58-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="4eb58-120">Query your device metadata, configuration, or state.</span><span class="sxs-lookup"><span data-stu-id="4eb58-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="4eb58-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span><span class="sxs-lookup"><span data-stu-id="4eb58-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="4eb58-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="4eb58-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="4eb58-123">Device twins</span><span class="sxs-lookup"><span data-stu-id="4eb58-123">Device twins</span></span>
<span data-ttu-id="4eb58-124">Device twins store device-related information that:</span><span class="sxs-lookup"><span data-stu-id="4eb58-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="4eb58-125">Device and back ends can use to synchronize device conditions and configuration.</span><span class="sxs-lookup"><span data-stu-id="4eb58-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="4eb58-126">The solution back end can use to query and target long-running operations.</span><span class="sxs-lookup"><span data-stu-id="4eb58-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="4eb58-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="4eb58-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="4eb58-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4eb58-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="4eb58-129">A device twin is a JSON document that includes:</span><span class="sxs-lookup"><span data-stu-id="4eb58-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="4eb58-130">**Tags**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-130">**Tags**.</span></span> <span data-ttu-id="4eb58-131">A section of the JSON document that the solution back end can read from and write to.</span><span class="sxs-lookup"><span data-stu-id="4eb58-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="4eb58-132">Tags are not visible to device apps.</span><span class="sxs-lookup"><span data-stu-id="4eb58-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="4eb58-133">**Desired properties**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-133">**Desired properties**.</span></span> <span data-ttu-id="4eb58-134">Used along with reported properties to synchronize device configuration or conditions.</span><span class="sxs-lookup"><span data-stu-id="4eb58-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="4eb58-135">Desired properties can only be set by the solution back end and can be read by the device app.</span><span class="sxs-lookup"><span data-stu-id="4eb58-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="4eb58-136">The device app can also be notified in real time of changes in the desired properties.</span><span class="sxs-lookup"><span data-stu-id="4eb58-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="4eb58-137">**Reported properties**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-137">**Reported properties**.</span></span> <span data-ttu-id="4eb58-138">Used along with desired properties to synchronize device configuration or conditions.</span><span class="sxs-lookup"><span data-stu-id="4eb58-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="4eb58-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="4eb58-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="4eb58-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="4eb58-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="4eb58-141">The following example shows a device twin JSON document:</span><span class="sxs-lookup"><span data-stu-id="4eb58-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="4eb58-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span><span class="sxs-lookup"><span data-stu-id="4eb58-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="4eb58-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span><span class="sxs-lookup"><span data-stu-id="4eb58-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="4eb58-144">Reported property example</span><span class="sxs-lookup"><span data-stu-id="4eb58-144">Reported property example</span></span>
<span data-ttu-id="4eb58-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span><span class="sxs-lookup"><span data-stu-id="4eb58-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="4eb58-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span><span class="sxs-lookup"><span data-stu-id="4eb58-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="4eb58-147">Other examples include the device app reporting device capabilities or connectivity options.</span><span class="sxs-lookup"><span data-stu-id="4eb58-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="4eb58-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span><span class="sxs-lookup"><span data-stu-id="4eb58-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="4eb58-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span><span class="sxs-lookup"><span data-stu-id="4eb58-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="4eb58-150">Desired property example</span><span class="sxs-lookup"><span data-stu-id="4eb58-150">Desired property example</span></span>
<span data-ttu-id="4eb58-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span><span class="sxs-lookup"><span data-stu-id="4eb58-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="4eb58-152">For example:</span><span class="sxs-lookup"><span data-stu-id="4eb58-152">For example:</span></span>

1. <span data-ttu-id="4eb58-153">The solution back end sets the desired property with the desired configuration value.</span><span class="sxs-lookup"><span data-stu-id="4eb58-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="4eb58-154">Here is the portion of the document with the desired property set:</span><span class="sxs-lookup"><span data-stu-id="4eb58-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="4eb58-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span><span class="sxs-lookup"><span data-stu-id="4eb58-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="4eb58-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span><span class="sxs-lookup"><span data-stu-id="4eb58-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="4eb58-157">Here is the portion of the reported properties:</span><span class="sxs-lookup"><span data-stu-id="4eb58-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="4eb58-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span><span class="sxs-lookup"><span data-stu-id="4eb58-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="4eb58-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span><span class="sxs-lookup"><span data-stu-id="4eb58-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="4eb58-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span><span class="sxs-lookup"><span data-stu-id="4eb58-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="4eb58-161">You can use twins to synchronize long-running operations such as firmware updates.</span><span class="sxs-lookup"><span data-stu-id="4eb58-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="4eb58-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="4eb58-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="4eb58-163">Back-end operations</span><span class="sxs-lookup"><span data-stu-id="4eb58-163">Back-end operations</span></span>
<span data-ttu-id="4eb58-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span><span class="sxs-lookup"><span data-stu-id="4eb58-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="4eb58-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span><span class="sxs-lookup"><span data-stu-id="4eb58-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="4eb58-166">**Partially update device twin**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-166">**Partially update device twin**.</span></span> <span data-ttu-id="4eb58-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span><span class="sxs-lookup"><span data-stu-id="4eb58-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="4eb58-168">The partial update is expressed as a JSON document that adds or updates any property.</span><span class="sxs-lookup"><span data-stu-id="4eb58-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="4eb58-169">Properties set to `null` are removed.</span><span class="sxs-lookup"><span data-stu-id="4eb58-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="4eb58-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="4eb58-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="4eb58-171">No other changes are made to existing desired properties or tags:</span><span class="sxs-lookup"><span data-stu-id="4eb58-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="4eb58-172">**Replace desired properties**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-172">**Replace desired properties**.</span></span> <span data-ttu-id="4eb58-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="4eb58-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="4eb58-174">**Replace tags**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-174">**Replace tags**.</span></span> <span data-ttu-id="4eb58-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span><span class="sxs-lookup"><span data-stu-id="4eb58-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>

<span data-ttu-id="4eb58-176">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span><span class="sxs-lookup"><span data-stu-id="4eb58-176">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="4eb58-177">In addition to these operations, the solution back end can:</span><span class="sxs-lookup"><span data-stu-id="4eb58-177">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="4eb58-178">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="4eb58-178">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="4eb58-179">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="4eb58-179">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="4eb58-180">Device operations</span><span class="sxs-lookup"><span data-stu-id="4eb58-180">Device operations</span></span>
<span data-ttu-id="4eb58-181">The device app operates on the device twin using the following atomic operations:</span><span class="sxs-lookup"><span data-stu-id="4eb58-181">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="4eb58-182">**Retrieve device twin**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-182">**Retrieve device twin**.</span></span> <span data-ttu-id="4eb58-183">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span><span class="sxs-lookup"><span data-stu-id="4eb58-183">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="4eb58-184">**Partially update reported properties**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-184">**Partially update reported properties**.</span></span> <span data-ttu-id="4eb58-185">This operation enables the partial update of the reported properties of the currently connected device.</span><span class="sxs-lookup"><span data-stu-id="4eb58-185">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="4eb58-186">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span><span class="sxs-lookup"><span data-stu-id="4eb58-186">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="4eb58-187">**Observe desired properties**.</span><span class="sxs-lookup"><span data-stu-id="4eb58-187">**Observe desired properties**.</span></span> <span data-ttu-id="4eb58-188">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span><span class="sxs-lookup"><span data-stu-id="4eb58-188">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="4eb58-189">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="4eb58-189">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="4eb58-190">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span><span class="sxs-lookup"><span data-stu-id="4eb58-190">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="4eb58-191">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span><span class="sxs-lookup"><span data-stu-id="4eb58-191">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="4eb58-192">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="4eb58-192">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="4eb58-193">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="4eb58-193">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="4eb58-194">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="4eb58-194">Reference topics:</span></span>
<span data-ttu-id="4eb58-195">The following reference topics provide you with more information about controlling access to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4eb58-195">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="4eb58-196">Tags and properties format</span><span class="sxs-lookup"><span data-stu-id="4eb58-196">Tags and properties format</span></span>
<span data-ttu-id="4eb58-197">Tags, desired, and reported properties are JSON objects with the following restrictions:</span><span class="sxs-lookup"><span data-stu-id="4eb58-197">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="4eb58-198">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span><span class="sxs-lookup"><span data-stu-id="4eb58-198">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="4eb58-199">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span><span class="sxs-lookup"><span data-stu-id="4eb58-199">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="4eb58-200">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span><span class="sxs-lookup"><span data-stu-id="4eb58-200">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="4eb58-201">Arrays are not allowed.</span><span class="sxs-lookup"><span data-stu-id="4eb58-201">Arrays are not allowed.</span></span>
* <span data-ttu-id="4eb58-202">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span><span class="sxs-lookup"><span data-stu-id="4eb58-202">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="4eb58-203">For instance, the following object is valid:</span><span class="sxs-lookup"><span data-stu-id="4eb58-203">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="4eb58-204">All string values can be at most 512 bytes in length.</span><span class="sxs-lookup"><span data-stu-id="4eb58-204">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="4eb58-205">Device twin size</span><span class="sxs-lookup"><span data-stu-id="4eb58-205">Device twin size</span></span>
<span data-ttu-id="4eb58-206">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span><span class="sxs-lookup"><span data-stu-id="4eb58-206">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="4eb58-207">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span><span class="sxs-lookup"><span data-stu-id="4eb58-207">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="4eb58-208">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span><span class="sxs-lookup"><span data-stu-id="4eb58-208">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="4eb58-209">Device twin metadata</span><span class="sxs-lookup"><span data-stu-id="4eb58-209">Device twin metadata</span></span>
<span data-ttu-id="4eb58-210">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span><span class="sxs-lookup"><span data-stu-id="4eb58-210">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="4eb58-211">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="4eb58-211">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="4eb58-212">For example:</span><span class="sxs-lookup"><span data-stu-id="4eb58-212">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="4eb58-213">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span><span class="sxs-lookup"><span data-stu-id="4eb58-213">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="4eb58-214">Optimistic concurrency</span><span class="sxs-lookup"><span data-stu-id="4eb58-214">Optimistic concurrency</span></span>
<span data-ttu-id="4eb58-215">Tags, desired, and reported properties all support optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="4eb58-215">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="4eb58-216">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span><span class="sxs-lookup"><span data-stu-id="4eb58-216">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="4eb58-217">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span><span class="sxs-lookup"><span data-stu-id="4eb58-217">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="4eb58-218">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span><span class="sxs-lookup"><span data-stu-id="4eb58-218">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="4eb58-219">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span><span class="sxs-lookup"><span data-stu-id="4eb58-219">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="4eb58-220">For example, a device app for a reported property or the solution back end for a desired property.</span><span class="sxs-lookup"><span data-stu-id="4eb58-220">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="4eb58-221">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span><span class="sxs-lookup"><span data-stu-id="4eb58-221">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="4eb58-222">The section [Device reconnection flow][lnk-reconnection] provides more information.</span><span class="sxs-lookup"><span data-stu-id="4eb58-222">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="4eb58-223">Device reconnection flow</span><span class="sxs-lookup"><span data-stu-id="4eb58-223">Device reconnection flow</span></span>
<span data-ttu-id="4eb58-224">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span><span class="sxs-lookup"><span data-stu-id="4eb58-224">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="4eb58-225">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span><span class="sxs-lookup"><span data-stu-id="4eb58-225">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="4eb58-226">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span><span class="sxs-lookup"><span data-stu-id="4eb58-226">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="4eb58-227">Device app connects to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4eb58-227">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="4eb58-228">Device app subscribes for desired properties update notifications.</span><span class="sxs-lookup"><span data-stu-id="4eb58-228">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="4eb58-229">Device app retrieves the full document for desired properties.</span><span class="sxs-lookup"><span data-stu-id="4eb58-229">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="4eb58-230">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span><span class="sxs-lookup"><span data-stu-id="4eb58-230">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="4eb58-231">This approach is possible because IoT Hub guarantees that versions always increment.</span><span class="sxs-lookup"><span data-stu-id="4eb58-231">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="4eb58-232">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="4eb58-232">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="4eb58-233">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span><span class="sxs-lookup"><span data-stu-id="4eb58-233">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="4eb58-234">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="4eb58-234">Additional reference material</span></span>
<span data-ttu-id="4eb58-235">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="4eb58-235">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4eb58-236">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="4eb58-236">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4eb58-237">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span><span class="sxs-lookup"><span data-stu-id="4eb58-237">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="4eb58-238">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4eb58-238">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4eb58-239">The [IoT Hub query language for device twins and jobs][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="4eb58-239">The [IoT Hub query language for device twins and jobs][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4eb58-240">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="4eb58-240">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4eb58-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="4eb58-241">Next steps</span></span>
<span data-ttu-id="4eb58-242">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span><span class="sxs-lookup"><span data-stu-id="4eb58-242">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="4eb58-243">[Invoke a direct method on a device][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="4eb58-243">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="4eb58-244">[Schedule jobs on multiple devices][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="4eb58-244">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="4eb58-245">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span><span class="sxs-lookup"><span data-stu-id="4eb58-245">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="4eb58-246">[How to use the device twin][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4eb58-246">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="4eb58-247">[How to use device twin properties][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="4eb58-247">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-devguide-device-twins/twin.png

