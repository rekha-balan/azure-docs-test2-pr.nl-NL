---
title: Understand Azure IoT Hub module twins | Microsoft Docs
description: Developer guide - use module twins to synchronize state and configuration data between IoT Hub and your devices
author: chrissie926
manager: ''
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 04/26/2018
ms.author: menchi
ms.openlocfilehash: 8f567ba43c1657783f9898863aef980627800481
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855621"
---
# <a name="understand-and-use-module-twins-in-iot-hub"></a><span data-ttu-id="16679-103">Understand and use module twins in IoT Hub</span><span class="sxs-lookup"><span data-stu-id="16679-103">Understand and use module twins in IoT Hub</span></span>

<span data-ttu-id="16679-104">This article assumes you've read [understand and use device twins in IoT Hub][lnk-devguide-device-twins] first.</span><span class="sxs-lookup"><span data-stu-id="16679-104">This article assumes you've read [understand and use device twins in IoT Hub][lnk-devguide-device-twins] first.</span></span> <span data-ttu-id="16679-105">In IoT Hub, under each device identity, you can create up to 20 module identities.</span><span class="sxs-lookup"><span data-stu-id="16679-105">In IoT Hub, under each device identity, you can create up to 20 module identities.</span></span> <span data-ttu-id="16679-106">Each module identity implicitly generates a module twin.</span><span class="sxs-lookup"><span data-stu-id="16679-106">Each module identity implicitly generates a module twin.</span></span> <span data-ttu-id="16679-107">Very similar to device twins, module twins are JSON documents that store module state information including metadata, configurations, and conditions.</span><span class="sxs-lookup"><span data-stu-id="16679-107">Very similar to device twins, module twins are JSON documents that store module state information including metadata, configurations, and conditions.</span></span> <span data-ttu-id="16679-108">Azure IoT Hub maintains a module twin for each module that you connect to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="16679-108">Azure IoT Hub maintains a module twin for each module that you connect to IoT Hub.</span></span> 

<span data-ttu-id="16679-109">On the device side, the IoT Hub device SDKs enable you to create modules which each opens an independent connection to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="16679-109">On the device side, the IoT Hub device SDKs enable you to create modules which each opens an independent connection to IoT Hub.</span></span> <span data-ttu-id="16679-110">This enables you to use separate namespaces for different components on your device.</span><span class="sxs-lookup"><span data-stu-id="16679-110">This enables you to use separate namespaces for different components on your device.</span></span> <span data-ttu-id="16679-111">For example, you have a vending machine that has three different sensors.</span><span class="sxs-lookup"><span data-stu-id="16679-111">For example, you have a vending machine that has three different sensors.</span></span> <span data-ttu-id="16679-112">Each sensor is controlled by different departments in your company.</span><span class="sxs-lookup"><span data-stu-id="16679-112">Each sensor is controlled by different departments in your company.</span></span> <span data-ttu-id="16679-113">You can create a module for each sensor.</span><span class="sxs-lookup"><span data-stu-id="16679-113">You can create a module for each sensor.</span></span> <span data-ttu-id="16679-114">This way, each department is only able to send jobs or direct methods to the sensor that they control, avoiding conflicts and user errors.</span><span class="sxs-lookup"><span data-stu-id="16679-114">This way, each department is only able to send jobs or direct methods to the sensor that they control, avoiding conflicts and user errors.</span></span>

 <span data-ttu-id="16679-115">Module identity and module twin provides the same capabilities as device identity and device twin but at a finer granularity.</span><span class="sxs-lookup"><span data-stu-id="16679-115">Module identity and module twin provides the same capabilities as device identity and device twin but at a finer granularity.</span></span> <span data-ttu-id="16679-116">This finer granularity enables capable devices, such as operating system based devices or firmware devices managing multiple components, to isolate configuration and conditions for each of those components.</span><span class="sxs-lookup"><span data-stu-id="16679-116">This finer granularity enables capable devices, such as operating system based devices or firmware devices managing multiple components, to isolate configuration and conditions for each of those components.</span></span> <span data-ttu-id="16679-117">Module identity and module twins provide a management separation of concerns when working with IoT devices that have modular software components.</span><span class="sxs-lookup"><span data-stu-id="16679-117">Module identity and module twins provide a management separation of concerns when working with IoT devices that have modular software components.</span></span> <span data-ttu-id="16679-118">We aim at supporting all the device twin functionality at module twin level by module twin general availability.</span><span class="sxs-lookup"><span data-stu-id="16679-118">We aim at supporting all the device twin functionality at module twin level by module twin general availability.</span></span> 

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="16679-119">This article describes:</span><span class="sxs-lookup"><span data-stu-id="16679-119">This article describes:</span></span>

* <span data-ttu-id="16679-120">The structure of the module twin: *tags*, *desired* and *reported properties*.</span><span class="sxs-lookup"><span data-stu-id="16679-120">The structure of the module twin: *tags*, *desired* and *reported properties*.</span></span>
* <span data-ttu-id="16679-121">The operations that the modules and back ends can perform on module twins.</span><span class="sxs-lookup"><span data-stu-id="16679-121">The operations that the modules and back ends can perform on module twins.</span></span>

<span data-ttu-id="16679-122">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span><span class="sxs-lookup"><span data-stu-id="16679-122">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="16679-123">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="16679-123">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="module-twins"></a><span data-ttu-id="16679-124">Module twins</span><span class="sxs-lookup"><span data-stu-id="16679-124">Module twins</span></span>
<span data-ttu-id="16679-125">Module twins store module-related information that:</span><span class="sxs-lookup"><span data-stu-id="16679-125">Module twins store module-related information that:</span></span>

* <span data-ttu-id="16679-126">Modules on the device and IoT Hub can use to synchronize module conditions and configuration.</span><span class="sxs-lookup"><span data-stu-id="16679-126">Modules on the device and IoT Hub can use to synchronize module conditions and configuration.</span></span>
* <span data-ttu-id="16679-127">The solution back end can use to query and target long-running operations.</span><span class="sxs-lookup"><span data-stu-id="16679-127">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="16679-128">The lifecycle of a module twin is linked to the corresponding [module identity][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="16679-128">The lifecycle of a module twin is linked to the corresponding [module identity][lnk-identity].</span></span> <span data-ttu-id="16679-129">Modules twins are implicitly created and deleted when a module identity is created or deleted in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="16679-129">Modules twins are implicitly created and deleted when a module identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="16679-130">A module twin is a JSON document that includes:</span><span class="sxs-lookup"><span data-stu-id="16679-130">A module twin is a JSON document that includes:</span></span>

* <span data-ttu-id="16679-131">**Tags**.</span><span class="sxs-lookup"><span data-stu-id="16679-131">**Tags**.</span></span> <span data-ttu-id="16679-132">A section of the JSON document that the solution back end can read from and write to.</span><span class="sxs-lookup"><span data-stu-id="16679-132">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="16679-133">Tags are not visible to modules on the device.</span><span class="sxs-lookup"><span data-stu-id="16679-133">Tags are not visible to modules on the device.</span></span> <span data-ttu-id="16679-134">Tags are set for querying purpose.</span><span class="sxs-lookup"><span data-stu-id="16679-134">Tags are set for querying purpose.</span></span>
* <span data-ttu-id="16679-135">**Desired properties**.</span><span class="sxs-lookup"><span data-stu-id="16679-135">**Desired properties**.</span></span> <span data-ttu-id="16679-136">Used along with reported properties to synchronize module configuration or conditions.</span><span class="sxs-lookup"><span data-stu-id="16679-136">Used along with reported properties to synchronize module configuration or conditions.</span></span> <span data-ttu-id="16679-137">The solution back end can set desired properties, and the module app can read them.</span><span class="sxs-lookup"><span data-stu-id="16679-137">The solution back end can set desired properties, and the module app can read them.</span></span> <span data-ttu-id="16679-138">The module app can also receive notifications of changes in the desired properties.</span><span class="sxs-lookup"><span data-stu-id="16679-138">The module app can also receive notifications of changes in the desired properties.</span></span>
* <span data-ttu-id="16679-139">**Reported properties**.</span><span class="sxs-lookup"><span data-stu-id="16679-139">**Reported properties**.</span></span> <span data-ttu-id="16679-140">Used along with desired properties to synchronize module configuration or conditions.</span><span class="sxs-lookup"><span data-stu-id="16679-140">Used along with desired properties to synchronize module configuration or conditions.</span></span> <span data-ttu-id="16679-141">The module app can set reported properties, and the solution back end can read and query them.</span><span class="sxs-lookup"><span data-stu-id="16679-141">The module app can set reported properties, and the solution back end can read and query them.</span></span>
* <span data-ttu-id="16679-142">**Module identity properties**.</span><span class="sxs-lookup"><span data-stu-id="16679-142">**Module identity properties**.</span></span> <span data-ttu-id="16679-143">The root of the module twin JSON document contains the read-only properties from the corresponding module identity stored in the [identity registry][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="16679-143">The root of the module twin JSON document contains the read-only properties from the corresponding module identity stored in the [identity registry][lnk-identity].</span></span>

![][img-module-twin]

<span data-ttu-id="16679-144">The following example shows a module twin JSON document:</span><span class="sxs-lookup"><span data-stu-id="16679-144">The following example shows a module twin JSON document:</span></span>

```json
{
    "deviceId": "devA",
    "moduleId": "moduleA",
    "etag": "AAAAAAAAAAc=", 
    "status": "enabled",
    "statusReason": "provisioned",
    "statusUpdateTime": "0001-01-01T00:00:00",
    "connectionState": "connected",
    "lastActivityTime": "2015-02-30T16:24:48.789Z",
    "cloudToDeviceMessageCount": 0, 
    "authenticationType": "sas",
    "x509Thumbprint": {     
        "primaryThumbprint": null, 
        "secondaryThumbprint": null 
    }, 
    "version": 2, 
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
```

<span data-ttu-id="16679-145">In the root object are the module identity properties, and container objects for `tags` and both `reported` and `desired` properties.</span><span class="sxs-lookup"><span data-stu-id="16679-145">In the root object are the module identity properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="16679-146">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Module twin metadata][lnk-module-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span><span class="sxs-lookup"><span data-stu-id="16679-146">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Module twin metadata][lnk-module-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="16679-147">Reported property example</span><span class="sxs-lookup"><span data-stu-id="16679-147">Reported property example</span></span>
<span data-ttu-id="16679-148">In the previous example, the module twin contains a `batteryLevel` property that is reported by the module app.</span><span class="sxs-lookup"><span data-stu-id="16679-148">In the previous example, the module twin contains a `batteryLevel` property that is reported by the module app.</span></span> <span data-ttu-id="16679-149">This property makes it possible to query and operate on modules based on the last reported battery level.</span><span class="sxs-lookup"><span data-stu-id="16679-149">This property makes it possible to query and operate on modules based on the last reported battery level.</span></span> <span data-ttu-id="16679-150">Other examples include the module app reporting module capabilities or connectivity options.</span><span class="sxs-lookup"><span data-stu-id="16679-150">Other examples include the module app reporting module capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="16679-151">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span><span class="sxs-lookup"><span data-stu-id="16679-151">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="16679-152">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process module telemetry in the form of sequences of timestamped events, such as time series.</span><span class="sxs-lookup"><span data-stu-id="16679-152">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process module telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="16679-153">Desired property example</span><span class="sxs-lookup"><span data-stu-id="16679-153">Desired property example</span></span>
<span data-ttu-id="16679-154">In the previous example, the `telemetryConfig` module twin desired and reported properties are used by the solution back end and the module app to synchronize the telemetry configuration for this module.</span><span class="sxs-lookup"><span data-stu-id="16679-154">In the previous example, the `telemetryConfig` module twin desired and reported properties are used by the solution back end and the module app to synchronize the telemetry configuration for this module.</span></span> <span data-ttu-id="16679-155">For example:</span><span class="sxs-lookup"><span data-stu-id="16679-155">For example:</span></span>

1. <span data-ttu-id="16679-156">The solution back end sets the desired property with the desired configuration value.</span><span class="sxs-lookup"><span data-stu-id="16679-156">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="16679-157">Here is the portion of the document with the desired property set:</span><span class="sxs-lookup"><span data-stu-id="16679-157">Here is the portion of the document with the desired property set:</span></span>

    ```json
    ...
    "desired": {
        "telemetryConfig": {
            "sendFrequency": "5m"
        },
        ...
    },
    ...
    ```

2. <span data-ttu-id="16679-158">The module app is notified of the change immediately if connected, or at the first reconnect.</span><span class="sxs-lookup"><span data-stu-id="16679-158">The module app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="16679-159">The module app then reports the updated configuration (or an error condition using the `status` property).</span><span class="sxs-lookup"><span data-stu-id="16679-159">The module app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="16679-160">Here is the portion of the reported properties:</span><span class="sxs-lookup"><span data-stu-id="16679-160">Here is the portion of the reported properties:</span></span>

    ```json
    ...
    "reported": {
        "telemetryConfig": {
            "sendFrequency": "5m",
            "status": "success"
        }
        ...
    }
    ...
    ```

3. <span data-ttu-id="16679-161">The solution back end can track the results of the configuration operation across many modules, by [querying][lnk-query] module twins.</span><span class="sxs-lookup"><span data-stu-id="16679-161">The solution back end can track the results of the configuration operation across many modules, by [querying][lnk-query] module twins.</span></span>

> [!NOTE]
> <span data-ttu-id="16679-162">The preceding snippets are examples, optimized for readability, of one way to encode a module configuration and its status.</span><span class="sxs-lookup"><span data-stu-id="16679-162">The preceding snippets are examples, optimized for readability, of one way to encode a module configuration and its status.</span></span> <span data-ttu-id="16679-163">IoT Hub does not impose a specific schema for the module twin desired and reported properties in the module twins.</span><span class="sxs-lookup"><span data-stu-id="16679-163">IoT Hub does not impose a specific schema for the module twin desired and reported properties in the module twins.</span></span>
> 
> 

## <a name="back-end-operations"></a><span data-ttu-id="16679-164">Back-end operations</span><span class="sxs-lookup"><span data-stu-id="16679-164">Back-end operations</span></span>
<span data-ttu-id="16679-165">The solution back end operates on the module twin using the following atomic operations, exposed through HTTPS:</span><span class="sxs-lookup"><span data-stu-id="16679-165">The solution back end operates on the module twin using the following atomic operations, exposed through HTTPS:</span></span>

* <span data-ttu-id="16679-166">**Retrieve module twin by ID**.</span><span class="sxs-lookup"><span data-stu-id="16679-166">**Retrieve module twin by ID**.</span></span> <span data-ttu-id="16679-167">This operation returns the module twin document, including tags and desired and reported system properties.</span><span class="sxs-lookup"><span data-stu-id="16679-167">This operation returns the module twin document, including tags and desired and reported system properties.</span></span>
* <span data-ttu-id="16679-168">**Partially update module twin**.</span><span class="sxs-lookup"><span data-stu-id="16679-168">**Partially update module twin**.</span></span> <span data-ttu-id="16679-169">This operation enables the solution back end to partially update the tags or desired properties in a module twin.</span><span class="sxs-lookup"><span data-stu-id="16679-169">This operation enables the solution back end to partially update the tags or desired properties in a module twin.</span></span> <span data-ttu-id="16679-170">The partial update is expressed as a JSON document that adds or updates any property.</span><span class="sxs-lookup"><span data-stu-id="16679-170">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="16679-171">Properties set to `null` are removed.</span><span class="sxs-lookup"><span data-stu-id="16679-171">Properties set to `null` are removed.</span></span> <span data-ttu-id="16679-172">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="16679-172">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="16679-173">No other changes are made to existing desired properties or tags:</span><span class="sxs-lookup"><span data-stu-id="16679-173">No other changes are made to existing desired properties or tags:</span></span>

    ```json
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
    ```

* <span data-ttu-id="16679-174">**Replace desired properties**.</span><span class="sxs-lookup"><span data-stu-id="16679-174">**Replace desired properties**.</span></span> <span data-ttu-id="16679-175">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="16679-175">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
* <span data-ttu-id="16679-176">**Replace tags**.</span><span class="sxs-lookup"><span data-stu-id="16679-176">**Replace tags**.</span></span> <span data-ttu-id="16679-177">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span><span class="sxs-lookup"><span data-stu-id="16679-177">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
* <span data-ttu-id="16679-178">**Receive twin notifications**.</span><span class="sxs-lookup"><span data-stu-id="16679-178">**Receive twin notifications**.</span></span> <span data-ttu-id="16679-179">This operation allows the solution back end to be notified when the twin is modified.</span><span class="sxs-lookup"><span data-stu-id="16679-179">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="16679-180">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="16679-180">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="16679-181">By default, no twin notifications are sent, that is, no such routes pre-exist.</span><span class="sxs-lookup"><span data-stu-id="16679-181">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="16679-182">If the rate of change is too high, or for other reasons such as internal failures, the IoT Hub might send only one notification that contains all changes.</span><span class="sxs-lookup"><span data-stu-id="16679-182">If the rate of change is too high, or for other reasons such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="16679-183">Therefore, if your application needs reliable auditing and logging of all intermediate states, you should use device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="16679-183">Therefore, if your application needs reliable auditing and logging of all intermediate states, you should use device-to-cloud messages.</span></span> <span data-ttu-id="16679-184">The twin notification message includes properties and body.</span><span class="sxs-lookup"><span data-stu-id="16679-184">The twin notification message includes properties and body.</span></span>

    - <span data-ttu-id="16679-185">Properties</span><span class="sxs-lookup"><span data-stu-id="16679-185">Properties</span></span>

    | <span data-ttu-id="16679-186">Name</span><span class="sxs-lookup"><span data-stu-id="16679-186">Name</span></span> | <span data-ttu-id="16679-187">Value</span><span class="sxs-lookup"><span data-stu-id="16679-187">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="16679-188">$content-type</span><span class="sxs-lookup"><span data-stu-id="16679-188">$content-type</span></span> | <span data-ttu-id="16679-189">application/json</span><span class="sxs-lookup"><span data-stu-id="16679-189">application/json</span></span> |
    <span data-ttu-id="16679-190">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="16679-190">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="16679-191">Time when the notification was sent</span><span class="sxs-lookup"><span data-stu-id="16679-191">Time when the notification was sent</span></span> |
    <span data-ttu-id="16679-192">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="16679-192">$iothub-message-source</span></span> | <span data-ttu-id="16679-193">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="16679-193">twinChangeEvents</span></span> |
    <span data-ttu-id="16679-194">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="16679-194">$content-encoding</span></span> | <span data-ttu-id="16679-195">utf-8</span><span class="sxs-lookup"><span data-stu-id="16679-195">utf-8</span></span> |
    <span data-ttu-id="16679-196">deviceId</span><span class="sxs-lookup"><span data-stu-id="16679-196">deviceId</span></span> | <span data-ttu-id="16679-197">ID of the device</span><span class="sxs-lookup"><span data-stu-id="16679-197">ID of the device</span></span> |
    <span data-ttu-id="16679-198">moduleId</span><span class="sxs-lookup"><span data-stu-id="16679-198">moduleId</span></span> | <span data-ttu-id="16679-199">ID of the module</span><span class="sxs-lookup"><span data-stu-id="16679-199">ID of the module</span></span> |
    <span data-ttu-id="16679-200">hubName</span><span class="sxs-lookup"><span data-stu-id="16679-200">hubName</span></span> | <span data-ttu-id="16679-201">Name of IoT Hub</span><span class="sxs-lookup"><span data-stu-id="16679-201">Name of IoT Hub</span></span> |
    <span data-ttu-id="16679-202">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="16679-202">operationTimestamp</span></span> | <span data-ttu-id="16679-203">[ISO8601] timestamp of operation</span><span class="sxs-lookup"><span data-stu-id="16679-203">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="16679-204">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="16679-204">iothub-message-schema</span></span> | <span data-ttu-id="16679-205">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="16679-205">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="16679-206">opType</span><span class="sxs-lookup"><span data-stu-id="16679-206">opType</span></span> | <span data-ttu-id="16679-207">"replaceTwin" or "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="16679-207">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="16679-208">Message system properties are prefixed with the `'$'` symbol.</span><span class="sxs-lookup"><span data-stu-id="16679-208">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="16679-209">Body</span><span class="sxs-lookup"><span data-stu-id="16679-209">Body</span></span>
        
    <span data-ttu-id="16679-210">This section includes all the twin changes in a JSON format.</span><span class="sxs-lookup"><span data-stu-id="16679-210">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="16679-211">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span><span class="sxs-lookup"><span data-stu-id="16679-211">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="16679-212">For example,</span><span class="sxs-lookup"><span data-stu-id="16679-212">For example,</span></span>

    ```json
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ```

<span data-ttu-id="16679-213">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span><span class="sxs-lookup"><span data-stu-id="16679-213">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="16679-214">In addition to these operations, the solution back end can:</span><span class="sxs-lookup"><span data-stu-id="16679-214">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="16679-215">Query the module twins using the SQL-like [IoT Hub query language][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="16679-215">Query the module twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>

## <a name="module-operations"></a><span data-ttu-id="16679-216">Module operations</span><span class="sxs-lookup"><span data-stu-id="16679-216">Module operations</span></span>
<span data-ttu-id="16679-217">The module app operates on the module twin using the following atomic operations:</span><span class="sxs-lookup"><span data-stu-id="16679-217">The module app operates on the module twin using the following atomic operations:</span></span>

* <span data-ttu-id="16679-218">**Retrieve module twin**.</span><span class="sxs-lookup"><span data-stu-id="16679-218">**Retrieve module twin**.</span></span> <span data-ttu-id="16679-219">This operation returns the module twin document (including tags and desired and reported system properties) for the currently connected module.</span><span class="sxs-lookup"><span data-stu-id="16679-219">This operation returns the module twin document (including tags and desired and reported system properties) for the currently connected module.</span></span>
* <span data-ttu-id="16679-220">**Partially update reported properties**.</span><span class="sxs-lookup"><span data-stu-id="16679-220">**Partially update reported properties**.</span></span> <span data-ttu-id="16679-221">This operation enables the partial update of the reported properties of the currently connected module.</span><span class="sxs-lookup"><span data-stu-id="16679-221">This operation enables the partial update of the reported properties of the currently connected module.</span></span> <span data-ttu-id="16679-222">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span><span class="sxs-lookup"><span data-stu-id="16679-222">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
* <span data-ttu-id="16679-223">**Observe desired properties**.</span><span class="sxs-lookup"><span data-stu-id="16679-223">**Observe desired properties**.</span></span> <span data-ttu-id="16679-224">The currently connected module can choose to be notified of updates to the desired properties when they happen.</span><span class="sxs-lookup"><span data-stu-id="16679-224">The currently connected module can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="16679-225">The module receives the same form of update (partial or full replacement) executed by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="16679-225">The module receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="16679-226">All the preceding operations require the **ModuleConnect** permission, as defined in the [Security][lnk-security] article.</span><span class="sxs-lookup"><span data-stu-id="16679-226">All the preceding operations require the **ModuleConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="16679-227">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span><span class="sxs-lookup"><span data-stu-id="16679-227">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="16679-228">Tags and properties format</span><span class="sxs-lookup"><span data-stu-id="16679-228">Tags and properties format</span></span>
<span data-ttu-id="16679-229">Tags, desired properties, and reported properties are JSON objects with the following restrictions:</span><span class="sxs-lookup"><span data-stu-id="16679-229">Tags, desired properties, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="16679-230">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span><span class="sxs-lookup"><span data-stu-id="16679-230">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="16679-231">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span><span class="sxs-lookup"><span data-stu-id="16679-231">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="16679-232">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span><span class="sxs-lookup"><span data-stu-id="16679-232">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="16679-233">Arrays are not allowed.</span><span class="sxs-lookup"><span data-stu-id="16679-233">Arrays are not allowed.</span></span> <span data-ttu-id="16679-234">The maximum value for integers is 4503599627370495 and the minimum value for integers is -4503599627370496.</span><span class="sxs-lookup"><span data-stu-id="16679-234">The maximum value for integers is 4503599627370495 and the minimum value for integers is -4503599627370496.</span></span>
* <span data-ttu-id="16679-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span><span class="sxs-lookup"><span data-stu-id="16679-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="16679-236">For instance, the following object is valid:</span><span class="sxs-lookup"><span data-stu-id="16679-236">For instance, the following object is valid:</span></span>

    ```json
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
    ```

* <span data-ttu-id="16679-237">All string values can be at most 4 KB in length.</span><span class="sxs-lookup"><span data-stu-id="16679-237">All string values can be at most 4 KB in length.</span></span>

## <a name="module-twin-size"></a><span data-ttu-id="16679-238">Module twin size</span><span class="sxs-lookup"><span data-stu-id="16679-238">Module twin size</span></span>
<span data-ttu-id="16679-239">IoT Hub enforces an 8KB size limitation on each of the respective total values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span><span class="sxs-lookup"><span data-stu-id="16679-239">IoT Hub enforces an 8KB size limitation on each of the respective total values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="16679-240">The size is computed by counting all characters, excluding UNICODE control characters (segments C0 and C1) and spaces that are outside of string constants.</span><span class="sxs-lookup"><span data-stu-id="16679-240">The size is computed by counting all characters, excluding UNICODE control characters (segments C0 and C1) and spaces that are outside of string constants.</span></span>
<span data-ttu-id="16679-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span><span class="sxs-lookup"><span data-stu-id="16679-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="module-twin-metadata"></a><span data-ttu-id="16679-242">Module twin metadata</span><span class="sxs-lookup"><span data-stu-id="16679-242">Module twin metadata</span></span>
<span data-ttu-id="16679-243">IoT Hub maintains the timestamp of the last update for each JSON object in module twin desired and reported properties.</span><span class="sxs-lookup"><span data-stu-id="16679-243">IoT Hub maintains the timestamp of the last update for each JSON object in module twin desired and reported properties.</span></span> <span data-ttu-id="16679-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="16679-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="16679-245">For example:</span><span class="sxs-lookup"><span data-stu-id="16679-245">For example:</span></span>

```json
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
```

<span data-ttu-id="16679-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span><span class="sxs-lookup"><span data-stu-id="16679-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="16679-247">Optimistic concurrency</span><span class="sxs-lookup"><span data-stu-id="16679-247">Optimistic concurrency</span></span>
<span data-ttu-id="16679-248">Tags, desired, and reported properties all support optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="16679-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="16679-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span><span class="sxs-lookup"><span data-stu-id="16679-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="16679-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span><span class="sxs-lookup"><span data-stu-id="16679-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="16679-251">Module twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span><span class="sxs-lookup"><span data-stu-id="16679-251">Module twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="16679-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span><span class="sxs-lookup"><span data-stu-id="16679-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="16679-253">For example, a module app for a reported property or the solution back end for a desired property.</span><span class="sxs-lookup"><span data-stu-id="16679-253">For example, a module app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="16679-254">Versions are also useful when an observing agent (such as the module app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span><span class="sxs-lookup"><span data-stu-id="16679-254">Versions are also useful when an observing agent (such as the module app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="16679-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span><span class="sxs-lookup"><span data-stu-id="16679-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="16679-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="16679-256">Next steps</span></span>
<span data-ttu-id="16679-257">To try out some of the concepts described in this article, see the following IoT Hub tutorials:</span><span class="sxs-lookup"><span data-stu-id="16679-257">To try out some of the concepts described in this article, see the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="16679-258">[Get started with IoT Hub module identity and module twin using .NET back end and .NET device][lnk-module-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="16679-258">[Get started with IoT Hub module identity and module twin using .NET back end and .NET device][lnk-module-twin-tutorial]</span></span>

<!-- links and images -->

[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232

[lnk-module-twin-tutorial]: iot-hub-csharp-csharp-module-twin-getstarted.md
[lnk-module-twin-metadata]: iot-hub-devguide-module-twins.md#module-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[img-module-twin]: media/iot-hub-devguide-device-twins/module-twin.jpg
