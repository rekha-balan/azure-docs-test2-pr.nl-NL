---
title: Understand Azure IoT Hub direct methods | Microsoft Docs
description: Developer guide - use direct methods to invoke code on your devices from a service app.
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: ''
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 690c1631e7b348a6e9b68e995ee68c15ea491bcf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551311"
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="eb07e-103">Understand and invoke direct methods from IoT Hub</span><span class="sxs-lookup"><span data-stu-id="eb07e-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="eb07e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="eb07e-104">Overview</span></span>
<span data-ttu-id="eb07e-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="eb07e-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="eb07e-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span><span class="sxs-lookup"><span data-stu-id="eb07e-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="eb07e-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span><span class="sxs-lookup"><span data-stu-id="eb07e-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="eb07e-108">Each device method targets a single device.</span><span class="sxs-lookup"><span data-stu-id="eb07e-108">Each device method targets a single device.</span></span> <span data-ttu-id="eb07e-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span><span class="sxs-lookup"><span data-stu-id="eb07e-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="eb07e-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span><span class="sxs-lookup"><span data-stu-id="eb07e-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="eb07e-111">When to use</span><span class="sxs-lookup"><span data-stu-id="eb07e-111">When to use</span></span>
<span data-ttu-id="eb07e-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span><span class="sxs-lookup"><span data-stu-id="eb07e-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="eb07e-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="eb07e-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="eb07e-114">Method lifecycle</span><span class="sxs-lookup"><span data-stu-id="eb07e-114">Method lifecycle</span></span>
<span data-ttu-id="eb07e-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span><span class="sxs-lookup"><span data-stu-id="eb07e-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="eb07e-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="eb07e-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="eb07e-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="eb07e-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="eb07e-118">We may support direct methods on additional device-side networking protocols in the future.</span><span class="sxs-lookup"><span data-stu-id="eb07e-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="eb07e-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="eb07e-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="eb07e-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span><span class="sxs-lookup"><span data-stu-id="eb07e-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="eb07e-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span><span class="sxs-lookup"><span data-stu-id="eb07e-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="eb07e-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="eb07e-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="eb07e-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span><span class="sxs-lookup"><span data-stu-id="eb07e-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="eb07e-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span><span class="sxs-lookup"><span data-stu-id="eb07e-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="eb07e-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span><span class="sxs-lookup"><span data-stu-id="eb07e-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="eb07e-126">The payload for method requests and responses is a JSON document up to 8KB.</span><span class="sxs-lookup"><span data-stu-id="eb07e-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="eb07e-127">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="eb07e-127">Reference topics:</span></span>
<span data-ttu-id="eb07e-128">The following reference topics provide you with more information about using direct methods.</span><span class="sxs-lookup"><span data-stu-id="eb07e-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="eb07e-129">Invoke a direct method from a back-end app</span><span class="sxs-lookup"><span data-stu-id="eb07e-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="eb07e-130">Method invocation</span><span class="sxs-lookup"><span data-stu-id="eb07e-130">Method invocation</span></span>
<span data-ttu-id="eb07e-131">Direct method invocations on a device are HTTP calls which comprise:</span><span class="sxs-lookup"><span data-stu-id="eb07e-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="eb07e-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="eb07e-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="eb07e-133">The POST *method*</span><span class="sxs-lookup"><span data-stu-id="eb07e-133">The POST *method*</span></span>
* <span data-ttu-id="eb07e-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span><span class="sxs-lookup"><span data-stu-id="eb07e-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="eb07e-135">A transparent JSON *body* in the following format:</span><span class="sxs-lookup"><span data-stu-id="eb07e-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="eb07e-136">Timeout is in seconds.</span><span class="sxs-lookup"><span data-stu-id="eb07e-136">Timeout is in seconds.</span></span> <span data-ttu-id="eb07e-137">If timeout is not set, it defaults to 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="eb07e-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="eb07e-138">Response</span><span class="sxs-lookup"><span data-stu-id="eb07e-138">Response</span></span>
<span data-ttu-id="eb07e-139">The back-end app receives a response which comprises:</span><span class="sxs-lookup"><span data-stu-id="eb07e-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="eb07e-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span><span class="sxs-lookup"><span data-stu-id="eb07e-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="eb07e-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span><span class="sxs-lookup"><span data-stu-id="eb07e-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="eb07e-142">A JSON *body* in the following format:</span><span class="sxs-lookup"><span data-stu-id="eb07e-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="eb07e-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span><span class="sxs-lookup"><span data-stu-id="eb07e-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="eb07e-144">Handle a direct method on a device</span><span class="sxs-lookup"><span data-stu-id="eb07e-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="eb07e-145">Method invocation</span><span class="sxs-lookup"><span data-stu-id="eb07e-145">Method invocation</span></span>
<span data-ttu-id="eb07e-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="eb07e-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="eb07e-147">The body which the device receives is in the following format:</span><span class="sxs-lookup"><span data-stu-id="eb07e-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="eb07e-148">Method requests are QoS 0.</span><span class="sxs-lookup"><span data-stu-id="eb07e-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="eb07e-149">Response</span><span class="sxs-lookup"><span data-stu-id="eb07e-149">Response</span></span>
<span data-ttu-id="eb07e-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span><span class="sxs-lookup"><span data-stu-id="eb07e-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="eb07e-151">The `status` property is the device-supplied status of method execution.</span><span class="sxs-lookup"><span data-stu-id="eb07e-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="eb07e-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="eb07e-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="eb07e-153">The body is set by the device and can be any status.</span><span class="sxs-lookup"><span data-stu-id="eb07e-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="eb07e-154">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="eb07e-154">Additional reference material</span></span>
<span data-ttu-id="eb07e-155">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="eb07e-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="eb07e-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="eb07e-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="eb07e-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span><span class="sxs-lookup"><span data-stu-id="eb07e-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="eb07e-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="eb07e-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="eb07e-159">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="eb07e-159">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="eb07e-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="eb07e-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb07e-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb07e-161">Next steps</span></span>
<span data-ttu-id="eb07e-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span><span class="sxs-lookup"><span data-stu-id="eb07e-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="eb07e-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="eb07e-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="eb07e-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span><span class="sxs-lookup"><span data-stu-id="eb07e-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="eb07e-165">[Use direct methods][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="eb07e-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
