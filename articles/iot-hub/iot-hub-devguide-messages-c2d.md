---
title: Understand Azure IoT Hub cloud-to-device messaging | Microsoft Docs
description: Developer guide - how to use cloud-to-device messaging with IoT Hub. Includes information about the message lifecycle, and configuration options.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 03/15/2018
ms.author: dobett
ms.openlocfilehash: d3d8df0d1e00fdff4d0e1e93715e1a408116d1e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966452"
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a><span data-ttu-id="ec765-104">Send cloud-to-device messages from IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ec765-104">Send cloud-to-device messages from IoT Hub</span></span>

<span data-ttu-id="ec765-105">To send one-way notifications to the device app from your solution back end, send cloud-to-devices messages from your IoT hub to your device.</span><span class="sxs-lookup"><span data-stu-id="ec765-105">To send one-way notifications to the device app from your solution back end, send cloud-to-devices messages from your IoT hub to your device.</span></span> <span data-ttu-id="ec765-106">For a discussion of other cloud-to-devices options supported by IoT Hub, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="ec765-106">For a discussion of other cloud-to-devices options supported by IoT Hub, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="ec765-107">You send cloud-to-device messages through a service-facing endpoint (**/messages/devicebound**).</span><span class="sxs-lookup"><span data-stu-id="ec765-107">You send cloud-to-device messages through a service-facing endpoint (**/messages/devicebound**).</span></span> <span data-ttu-id="ec765-108">A device then receives the messages through a device-specific endpoint (**/devices/{deviceId}/messages/devicebound**).</span><span class="sxs-lookup"><span data-stu-id="ec765-108">A device then receives the messages through a device-specific endpoint (**/devices/{deviceId}/messages/devicebound**).</span></span>

<span data-ttu-id="ec765-109">To target each cloud-to-device message at a single device, IoT Hub sets the **to** property to **/devices/{deviceId}/messages/devicebound**.</span><span class="sxs-lookup"><span data-stu-id="ec765-109">To target each cloud-to-device message at a single device, IoT Hub sets the **to** property to **/devices/{deviceId}/messages/devicebound**.</span></span>

<span data-ttu-id="ec765-110">Each device queue holds at most 50 cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-110">Each device queue holds at most 50 cloud-to-device messages.</span></span> <span data-ttu-id="ec765-111">Trying to send more messages to the same device results in an error.</span><span class="sxs-lookup"><span data-stu-id="ec765-111">Trying to send more messages to the same device results in an error.</span></span>

## <a name="the-cloud-to-device-message-lifecycle"></a><span data-ttu-id="ec765-112">The cloud-to-device message lifecycle</span><span class="sxs-lookup"><span data-stu-id="ec765-112">The cloud-to-device message lifecycle</span></span>

<span data-ttu-id="ec765-113">To guarantee at-least-once message delivery, IoT Hub persists cloud-to-device messages in per-device queues.</span><span class="sxs-lookup"><span data-stu-id="ec765-113">To guarantee at-least-once message delivery, IoT Hub persists cloud-to-device messages in per-device queues.</span></span> <span data-ttu-id="ec765-114">Devices must explicitly acknowledge *completion* for IoT Hub to remove them from the queue.</span><span class="sxs-lookup"><span data-stu-id="ec765-114">Devices must explicitly acknowledge *completion* for IoT Hub to remove them from the queue.</span></span> <span data-ttu-id="ec765-115">This approach guarantees resiliency against connectivity and device failures.</span><span class="sxs-lookup"><span data-stu-id="ec765-115">This approach guarantees resiliency against connectivity and device failures.</span></span>

<span data-ttu-id="ec765-116">The following diagram shows the lifecycle state graph for a cloud-to-device message in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ec765-116">The following diagram shows the lifecycle state graph for a cloud-to-device message in IoT Hub.</span></span>

![Cloud-to-device message lifecycle][img-lifecycle]

<span data-ttu-id="ec765-118">When the IoT Hub service sends a message to a device, the service sets the message state to **Enqueued**.</span><span class="sxs-lookup"><span data-stu-id="ec765-118">When the IoT Hub service sends a message to a device, the service sets the message state to **Enqueued**.</span></span> <span data-ttu-id="ec765-119">When a device wants to *receive* a message, IoT Hub *locks* the message (by setting the state to **Invisible**), which allows other threads on the device to start receiving other messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-119">When a device wants to *receive* a message, IoT Hub *locks* the message (by setting the state to **Invisible**), which allows other threads on the device to start receiving other messages.</span></span> <span data-ttu-id="ec765-120">When a device thread completes the processing of a message, it notifies IoT Hub by *completing* the message.</span><span class="sxs-lookup"><span data-stu-id="ec765-120">When a device thread completes the processing of a message, it notifies IoT Hub by *completing* the message.</span></span> <span data-ttu-id="ec765-121">IoT Hub then sets the state to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="ec765-121">IoT Hub then sets the state to **Completed**.</span></span>

<span data-ttu-id="ec765-122">A device can also choose to:</span><span class="sxs-lookup"><span data-stu-id="ec765-122">A device can also choose to:</span></span>

* <span data-ttu-id="ec765-123">*Reject* the message, which causes IoT Hub to set it to the **Dead lettered** state.</span><span class="sxs-lookup"><span data-stu-id="ec765-123">*Reject* the message, which causes IoT Hub to set it to the **Dead lettered** state.</span></span> <span data-ttu-id="ec765-124">Devices that connect over the MQTT protocol cannot reject cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-124">Devices that connect over the MQTT protocol cannot reject cloud-to-device messages.</span></span>
* <span data-ttu-id="ec765-125">*Abandon* the message, which causes IoT Hub to put the message back in the queue, with the state set to **Enqueued**.</span><span class="sxs-lookup"><span data-stu-id="ec765-125">*Abandon* the message, which causes IoT Hub to put the message back in the queue, with the state set to **Enqueued**.</span></span> <span data-ttu-id="ec765-126">Devices that connect over the MQTT protocol cannot abandon cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-126">Devices that connect over the MQTT protocol cannot abandon cloud-to-device messages.</span></span>

<span data-ttu-id="ec765-127">A thread could fail to process a message without notifying IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ec765-127">A thread could fail to process a message without notifying IoT Hub.</span></span> <span data-ttu-id="ec765-128">In this case, messages automatically transition from the **Invisible** state back to the **Enqueued** state after a *visibility (or lock) timeout*.</span><span class="sxs-lookup"><span data-stu-id="ec765-128">In this case, messages automatically transition from the **Invisible** state back to the **Enqueued** state after a *visibility (or lock) timeout*.</span></span> <span data-ttu-id="ec765-129">The default value of this timeout is one minute.</span><span class="sxs-lookup"><span data-stu-id="ec765-129">The default value of this timeout is one minute.</span></span>

<span data-ttu-id="ec765-130">The **max delivery count** property on IoT Hub determines the maximum number of times a message can transition between the **Enqueued** and **Invisible** states.</span><span class="sxs-lookup"><span data-stu-id="ec765-130">The **max delivery count** property on IoT Hub determines the maximum number of times a message can transition between the **Enqueued** and **Invisible** states.</span></span> <span data-ttu-id="ec765-131">After that number of transitions, IoT Hub sets the state of the message to **Dead lettered**.</span><span class="sxs-lookup"><span data-stu-id="ec765-131">After that number of transitions, IoT Hub sets the state of the message to **Dead lettered**.</span></span> <span data-ttu-id="ec765-132">Similarly, IoT Hub sets the state of a message to **Dead lettered** after its expiration time (see [Time to live][lnk-ttl]).</span><span class="sxs-lookup"><span data-stu-id="ec765-132">Similarly, IoT Hub sets the state of a message to **Dead lettered** after its expiration time (see [Time to live][lnk-ttl]).</span></span>

<span data-ttu-id="ec765-133">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial] shows you how to send cloud-to-device messages from the cloud and receive them on a device.</span><span class="sxs-lookup"><span data-stu-id="ec765-133">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial] shows you how to send cloud-to-device messages from the cloud and receive them on a device.</span></span>

<span data-ttu-id="ec765-134">Typically, a device completes a cloud-to-device message when the loss of the message does not affect the application logic.</span><span class="sxs-lookup"><span data-stu-id="ec765-134">Typically, a device completes a cloud-to-device message when the loss of the message does not affect the application logic.</span></span> <span data-ttu-id="ec765-135">For example, when the device has persisted the message content locally or has successfully executed an operation.</span><span class="sxs-lookup"><span data-stu-id="ec765-135">For example, when the device has persisted the message content locally or has successfully executed an operation.</span></span> <span data-ttu-id="ec765-136">The message could also carry transient information, whose loss would not impact the functionality of the application.</span><span class="sxs-lookup"><span data-stu-id="ec765-136">The message could also carry transient information, whose loss would not impact the functionality of the application.</span></span> <span data-ttu-id="ec765-137">Sometimes, for long-running tasks, you can:</span><span class="sxs-lookup"><span data-stu-id="ec765-137">Sometimes, for long-running tasks, you can:</span></span>

* <span data-ttu-id="ec765-138">Complete the cloud-to-device message after persisting the task description in local storage.</span><span class="sxs-lookup"><span data-stu-id="ec765-138">Complete the cloud-to-device message after persisting the task description in local storage.</span></span>
* <span data-ttu-id="ec765-139">Notify the solution back end with one or more device-to-cloud messages at various stages of progress of the task.</span><span class="sxs-lookup"><span data-stu-id="ec765-139">Notify the solution back end with one or more device-to-cloud messages at various stages of progress of the task.</span></span>

## <a name="message-expiration-time-to-live"></a><span data-ttu-id="ec765-140">Message expiration (time to live)</span><span class="sxs-lookup"><span data-stu-id="ec765-140">Message expiration (time to live)</span></span>

<span data-ttu-id="ec765-141">Every cloud-to-device message has an expiration time.</span><span class="sxs-lookup"><span data-stu-id="ec765-141">Every cloud-to-device message has an expiration time.</span></span> <span data-ttu-id="ec765-142">This time is set by one of:</span><span class="sxs-lookup"><span data-stu-id="ec765-142">This time is set by one of:</span></span>

* <span data-ttu-id="ec765-143">The **ExpiryTimeUtc** property in the service.</span><span class="sxs-lookup"><span data-stu-id="ec765-143">The **ExpiryTimeUtc** property in the service.</span></span>
* <span data-ttu-id="ec765-144">IoT Hub using the default *time to live* specified as an IoT Hub property.</span><span class="sxs-lookup"><span data-stu-id="ec765-144">IoT Hub using the default *time to live* specified as an IoT Hub property.</span></span>

<span data-ttu-id="ec765-145">See [Cloud-to-device configuration options][lnk-c2d-configuration].</span><span class="sxs-lookup"><span data-stu-id="ec765-145">See [Cloud-to-device configuration options][lnk-c2d-configuration].</span></span>

<span data-ttu-id="ec765-146">A common way to take advantage of message expiration and avoid sending messages to disconnected devices, is to set short time to live values.</span><span class="sxs-lookup"><span data-stu-id="ec765-146">A common way to take advantage of message expiration and avoid sending messages to disconnected devices, is to set short time to live values.</span></span> <span data-ttu-id="ec765-147">This approach achieves the same result as maintaining the device connection state, while being more efficient.</span><span class="sxs-lookup"><span data-stu-id="ec765-147">This approach achieves the same result as maintaining the device connection state, while being more efficient.</span></span> <span data-ttu-id="ec765-148">When you request message acknowledgements, IoT Hub notifies you which devices are:</span><span class="sxs-lookup"><span data-stu-id="ec765-148">When you request message acknowledgements, IoT Hub notifies you which devices are:</span></span>

* <span data-ttu-id="ec765-149">Able to receive messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-149">Able to receive messages.</span></span>
* <span data-ttu-id="ec765-150">Are not online or have failed.</span><span class="sxs-lookup"><span data-stu-id="ec765-150">Are not online or have failed.</span></span>

## <a name="message-feedback"></a><span data-ttu-id="ec765-151">Message feedback</span><span class="sxs-lookup"><span data-stu-id="ec765-151">Message feedback</span></span>

<span data-ttu-id="ec765-152">When you send a cloud-to-device message, the service can request the delivery of per-message feedback regarding the final state of that message.</span><span class="sxs-lookup"><span data-stu-id="ec765-152">When you send a cloud-to-device message, the service can request the delivery of per-message feedback regarding the final state of that message.</span></span>

| <span data-ttu-id="ec765-153">Ack property</span><span class="sxs-lookup"><span data-stu-id="ec765-153">Ack property</span></span> | <span data-ttu-id="ec765-154">Behavior</span><span class="sxs-lookup"><span data-stu-id="ec765-154">Behavior</span></span> |
| ------------ | -------- |
| <span data-ttu-id="ec765-155">**positive**</span><span class="sxs-lookup"><span data-stu-id="ec765-155">**positive**</span></span> | <span data-ttu-id="ec765-156">If the cloud-to-device message reaches the **Completed** state, IoT Hub generates a feedback message.</span><span class="sxs-lookup"><span data-stu-id="ec765-156">If the cloud-to-device message reaches the **Completed** state, IoT Hub generates a feedback message.</span></span> |
| <span data-ttu-id="ec765-157">**negative**</span><span class="sxs-lookup"><span data-stu-id="ec765-157">**negative**</span></span> | <span data-ttu-id="ec765-158">If the cloud-to-device message reaches the **Dead lettered** state, IoT Hub generates a feedback message.</span><span class="sxs-lookup"><span data-stu-id="ec765-158">If the cloud-to-device message reaches the **Dead lettered** state, IoT Hub generates a feedback message.</span></span> |
| <span data-ttu-id="ec765-159">**full**</span><span class="sxs-lookup"><span data-stu-id="ec765-159">**full**</span></span>     | <span data-ttu-id="ec765-160">IoT Hub generates a feedback message in either case.</span><span class="sxs-lookup"><span data-stu-id="ec765-160">IoT Hub generates a feedback message in either case.</span></span> |

<span data-ttu-id="ec765-161">If **Ack** is **full**, and you don't receive a feedback message, it means that the feedback message expired.</span><span class="sxs-lookup"><span data-stu-id="ec765-161">If **Ack** is **full**, and you don't receive a feedback message, it means that the feedback message expired.</span></span> <span data-ttu-id="ec765-162">The service can't know what happened to the original message.</span><span class="sxs-lookup"><span data-stu-id="ec765-162">The service can't know what happened to the original message.</span></span> <span data-ttu-id="ec765-163">In practice, a service should ensure that it can process the feedback before it expires.</span><span class="sxs-lookup"><span data-stu-id="ec765-163">In practice, a service should ensure that it can process the feedback before it expires.</span></span> <span data-ttu-id="ec765-164">The maximum expiry time is two days, which leaves time to get the service running again if a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="ec765-164">The maximum expiry time is two days, which leaves time to get the service running again if a failure occurs.</span></span>

<span data-ttu-id="ec765-165">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers feedback through a service-facing endpoint (**/messages/servicebound/feedback**) as messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-165">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers feedback through a service-facing endpoint (**/messages/servicebound/feedback**) as messages.</span></span> <span data-ttu-id="ec765-166">The semantics for receiving feedback are the same as for cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-166">The semantics for receiving feedback are the same as for cloud-to-device messages.</span></span> <span data-ttu-id="ec765-167">Whenever possible, message feedback is batched in a single message, with the following format:</span><span class="sxs-lookup"><span data-stu-id="ec765-167">Whenever possible, message feedback is batched in a single message, with the following format:</span></span>

| <span data-ttu-id="ec765-168">Property</span><span class="sxs-lookup"><span data-stu-id="ec765-168">Property</span></span>     | <span data-ttu-id="ec765-169">Description</span><span class="sxs-lookup"><span data-stu-id="ec765-169">Description</span></span> |
| ------------ | ----------- |
| <span data-ttu-id="ec765-170">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="ec765-170">EnqueuedTime</span></span> | <span data-ttu-id="ec765-171">Timestamp indicating when the feedback message was received by the hub.</span><span class="sxs-lookup"><span data-stu-id="ec765-171">Timestamp indicating when the feedback message was received by the hub.</span></span> |
| <span data-ttu-id="ec765-172">UserId</span><span class="sxs-lookup"><span data-stu-id="ec765-172">UserId</span></span>       | `{iot hub name}` |
| <span data-ttu-id="ec765-173">ContentType</span><span class="sxs-lookup"><span data-stu-id="ec765-173">ContentType</span></span>  | `application/vnd.microsoft.iothub.feedback.json` |

<span data-ttu-id="ec765-174">The body is a JSON-serialized array of records, each with the following properties:</span><span class="sxs-lookup"><span data-stu-id="ec765-174">The body is a JSON-serialized array of records, each with the following properties:</span></span>

| <span data-ttu-id="ec765-175">Property</span><span class="sxs-lookup"><span data-stu-id="ec765-175">Property</span></span>           | <span data-ttu-id="ec765-176">Description</span><span class="sxs-lookup"><span data-stu-id="ec765-176">Description</span></span> |
| ------------------ | ----------- |
| <span data-ttu-id="ec765-177">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="ec765-177">EnqueuedTimeUtc</span></span>    | <span data-ttu-id="ec765-178">Timestamp indicating when the outcome of the message happened.</span><span class="sxs-lookup"><span data-stu-id="ec765-178">Timestamp indicating when the outcome of the message happened.</span></span> <span data-ttu-id="ec765-179">For example, the hub received the feedback message or the original message expired.</span><span class="sxs-lookup"><span data-stu-id="ec765-179">For example, the hub received the feedback message or the original message expired.</span></span> |
| <span data-ttu-id="ec765-180">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="ec765-180">OriginalMessageId</span></span>  | <span data-ttu-id="ec765-181">**MessageId** of the cloud-to-device message to which this feedback information relates.</span><span class="sxs-lookup"><span data-stu-id="ec765-181">**MessageId** of the cloud-to-device message to which this feedback information relates.</span></span> |
| <span data-ttu-id="ec765-182">StatusCode</span><span class="sxs-lookup"><span data-stu-id="ec765-182">StatusCode</span></span>         | <span data-ttu-id="ec765-183">Required string.</span><span class="sxs-lookup"><span data-stu-id="ec765-183">Required string.</span></span> <span data-ttu-id="ec765-184">Used in feedback messages generated by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ec765-184">Used in feedback messages generated by IoT Hub.</span></span> <br/> <span data-ttu-id="ec765-185">'Success'</span><span class="sxs-lookup"><span data-stu-id="ec765-185">'Success'</span></span> <br/> <span data-ttu-id="ec765-186">'Expired'</span><span class="sxs-lookup"><span data-stu-id="ec765-186">'Expired'</span></span> <br/> <span data-ttu-id="ec765-187">'DeliveryCountExceeded'</span><span class="sxs-lookup"><span data-stu-id="ec765-187">'DeliveryCountExceeded'</span></span> <br/> <span data-ttu-id="ec765-188">'Rejected'</span><span class="sxs-lookup"><span data-stu-id="ec765-188">'Rejected'</span></span> <br/> <span data-ttu-id="ec765-189">'Purged'</span><span class="sxs-lookup"><span data-stu-id="ec765-189">'Purged'</span></span> |
| <span data-ttu-id="ec765-190">Description</span><span class="sxs-lookup"><span data-stu-id="ec765-190">Description</span></span>        | <span data-ttu-id="ec765-191">String values for **StatusCode**.</span><span class="sxs-lookup"><span data-stu-id="ec765-191">String values for **StatusCode**.</span></span> |
| <span data-ttu-id="ec765-192">DeviceId</span><span class="sxs-lookup"><span data-stu-id="ec765-192">DeviceId</span></span>           | <span data-ttu-id="ec765-193">**DeviceId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span><span class="sxs-lookup"><span data-stu-id="ec765-193">**DeviceId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span></span> |
| <span data-ttu-id="ec765-194">DeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="ec765-194">DeviceGenerationId</span></span> | <span data-ttu-id="ec765-195">**DeviceGenerationId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span><span class="sxs-lookup"><span data-stu-id="ec765-195">**DeviceGenerationId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span></span> |

<span data-ttu-id="ec765-196">The service must specify a **MessageId** for the cloud-to-device message to be able to correlate its feedback with the original message.</span><span class="sxs-lookup"><span data-stu-id="ec765-196">The service must specify a **MessageId** for the cloud-to-device message to be able to correlate its feedback with the original message.</span></span>

<span data-ttu-id="ec765-197">The following example shows the body of a feedback message.</span><span class="sxs-lookup"><span data-stu-id="ec765-197">The following example shows the body of a feedback message.</span></span>

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a><span data-ttu-id="ec765-198">Cloud-to-device configuration options</span><span class="sxs-lookup"><span data-stu-id="ec765-198">Cloud-to-device configuration options</span></span>

<span data-ttu-id="ec765-199">Each IoT hub exposes the following configuration options for cloud-to-device messaging:</span><span class="sxs-lookup"><span data-stu-id="ec765-199">Each IoT hub exposes the following configuration options for cloud-to-device messaging:</span></span>

| <span data-ttu-id="ec765-200">Property</span><span class="sxs-lookup"><span data-stu-id="ec765-200">Property</span></span>                  | <span data-ttu-id="ec765-201">Description</span><span class="sxs-lookup"><span data-stu-id="ec765-201">Description</span></span> | <span data-ttu-id="ec765-202">Range and default</span><span class="sxs-lookup"><span data-stu-id="ec765-202">Range and default</span></span> |
| ------------------------- | ----------- | ----------------- |
| <span data-ttu-id="ec765-203">defaultTtlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="ec765-203">defaultTtlAsIso8601</span></span>       | <span data-ttu-id="ec765-204">Default TTL for cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-204">Default TTL for cloud-to-device messages.</span></span> | <span data-ttu-id="ec765-205">ISO_8601 interval up to 2D (minimum 1 minute).</span><span class="sxs-lookup"><span data-stu-id="ec765-205">ISO_8601 interval up to 2D (minimum 1 minute).</span></span> <span data-ttu-id="ec765-206">Default: 1 hour.</span><span class="sxs-lookup"><span data-stu-id="ec765-206">Default: 1 hour.</span></span> |
| <span data-ttu-id="ec765-207">maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="ec765-207">maxDeliveryCount</span></span>          | <span data-ttu-id="ec765-208">Maximum delivery count for cloud-to-device per-device queues.</span><span class="sxs-lookup"><span data-stu-id="ec765-208">Maximum delivery count for cloud-to-device per-device queues.</span></span> | <span data-ttu-id="ec765-209">1 to 100.</span><span class="sxs-lookup"><span data-stu-id="ec765-209">1 to 100.</span></span> <span data-ttu-id="ec765-210">Default: 10.</span><span class="sxs-lookup"><span data-stu-id="ec765-210">Default: 10.</span></span> |
| <span data-ttu-id="ec765-211">feedback.ttlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="ec765-211">feedback.ttlAsIso8601</span></span>     | <span data-ttu-id="ec765-212">Retention for service-bound feedback messages.</span><span class="sxs-lookup"><span data-stu-id="ec765-212">Retention for service-bound feedback messages.</span></span> | <span data-ttu-id="ec765-213">ISO_8601 interval up to 2D (minimum 1 minute).</span><span class="sxs-lookup"><span data-stu-id="ec765-213">ISO_8601 interval up to 2D (minimum 1 minute).</span></span> <span data-ttu-id="ec765-214">Default: 1 hour.</span><span class="sxs-lookup"><span data-stu-id="ec765-214">Default: 1 hour.</span></span> |
| <span data-ttu-id="ec765-215">feedback.maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="ec765-215">feedback.maxDeliveryCount</span></span> |<span data-ttu-id="ec765-216">Maximum delivery count for feedback queue.</span><span class="sxs-lookup"><span data-stu-id="ec765-216">Maximum delivery count for feedback queue.</span></span> | <span data-ttu-id="ec765-217">1 to 100.</span><span class="sxs-lookup"><span data-stu-id="ec765-217">1 to 100.</span></span> <span data-ttu-id="ec765-218">Default: 100.</span><span class="sxs-lookup"><span data-stu-id="ec765-218">Default: 100.</span></span> |

<span data-ttu-id="ec765-219">For more information about how to set these configuration options, see [Create IoT hubs][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ec765-219">For more information about how to set these configuration options, see [Create IoT hubs][lnk-portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec765-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec765-220">Next steps</span></span>

<span data-ttu-id="ec765-221">For information about the SDKs you can use to receive cloud-to-device messages, see [Azure IoT SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="ec765-221">For information about the SDKs you can use to receive cloud-to-device messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ec765-222">To try out receiving cloud-to-device messages, see the [Send cloud-to-device][lnk-c2d-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec765-222">To try out receiving cloud-to-device messages, see the [Send cloud-to-device][lnk-c2d-tutorial] tutorial.</span></span>

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
