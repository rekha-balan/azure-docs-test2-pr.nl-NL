---
title: Understand Azure IoT Hub device-to-cloud messaging | Microsoft Docs
description: Developer guide - how to use device-to-cloud messaging with IoT Hub. Includes information about sending both telemetry and non-telemtry data, and using routing to deliver messages.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: dobett
ms.openlocfilehash: be87b00f27f0d0b25cd77a0634ab1c653a85e5ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871567"
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="3f172-104">Send device-to-cloud messages to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3f172-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="3f172-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f172-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="3f172-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="3f172-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="3f172-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="3f172-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="3f172-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f172-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="3f172-109">Routing rules use the headers and body of the device-to-cloud messages to determine where to route them.</span><span class="sxs-lookup"><span data-stu-id="3f172-109">Routing rules use the headers and body of the device-to-cloud messages to determine where to route them.</span></span> <span data-ttu-id="3f172-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="3f172-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="3f172-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span><span class="sxs-lookup"><span data-stu-id="3f172-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="3f172-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span><span class="sxs-lookup"><span data-stu-id="3f172-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="3f172-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span><span class="sxs-lookup"><span data-stu-id="3f172-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="3f172-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="3f172-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="3f172-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span><span class="sxs-lookup"><span data-stu-id="3f172-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="3f172-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span><span class="sxs-lookup"><span data-stu-id="3f172-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="3f172-117">Batches can be at most 256 KB.</span><span class="sxs-lookup"><span data-stu-id="3f172-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="3f172-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span><span class="sxs-lookup"><span data-stu-id="3f172-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="3f172-119">IoT Hub allows you to create up to 10 custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="3f172-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="3f172-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f172-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="3f172-121">For more information, see [Routing rules](iot-hub-devguide-query-language.md#device-to-cloud-message-routes-query-expressions).</span><span class="sxs-lookup"><span data-stu-id="3f172-121">For more information, see [Routing rules](iot-hub-devguide-query-language.md#device-to-cloud-message-routes-query-expressions).</span></span>
* <span data-ttu-id="3f172-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="3f172-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="3f172-123">IoT Hub does not allow arbitrary partitioning.</span><span class="sxs-lookup"><span data-stu-id="3f172-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="3f172-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="3f172-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="3f172-125">For more information about the differences between IoT Hub and Event Hubs, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="3f172-125">For more information about the differences between IoT Hub and Event Hubs, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="3f172-126">Send non-telemetry traffic</span><span class="sxs-lookup"><span data-stu-id="3f172-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="3f172-127">Often, in addition to telemetry, devices send messages and requests that require separate execution and handling in the solution back end.</span><span class="sxs-lookup"><span data-stu-id="3f172-127">Often, in addition to telemetry, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="3f172-128">For example, critical alerts that must trigger a specific action in the back end.</span><span class="sxs-lookup"><span data-stu-id="3f172-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="3f172-129">You can write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span><span class="sxs-lookup"><span data-stu-id="3f172-129">You can write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="3f172-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f172-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="3f172-131">Route device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="3f172-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="3f172-132">You have two options for routing device-to-cloud messages to your back-end apps:</span><span class="sxs-lookup"><span data-stu-id="3f172-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="3f172-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span><span class="sxs-lookup"><span data-stu-id="3f172-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="3f172-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="3f172-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="3f172-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f172-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="3f172-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span><span class="sxs-lookup"><span data-stu-id="3f172-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="3f172-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="3f172-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="3f172-138">Anti-spoofing properties</span><span class="sxs-lookup"><span data-stu-id="3f172-138">Anti-spoofing properties</span></span>

<span data-ttu-id="3f172-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span><span class="sxs-lookup"><span data-stu-id="3f172-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="3f172-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="3f172-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="3f172-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="3f172-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="3f172-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="3f172-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="3f172-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="3f172-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="3f172-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span><span class="sxs-lookup"><span data-stu-id="3f172-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device }",
  "type": "{ symkey | sas | x509 }",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="3f172-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f172-145">Next steps</span></span>

<span data-ttu-id="3f172-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="3f172-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="3f172-147">The [Quickstarts][lnk-get-started] show you how to send device-to-cloud messages from simulated devices.</span><span class="sxs-lookup"><span data-stu-id="3f172-147">The [Quickstarts][lnk-get-started] show you how to send device-to-cloud messages from simulated devices.</span></span> <span data-ttu-id="3f172-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f172-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: quickstart-send-telemetry-node.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: tutorial-routing.md
