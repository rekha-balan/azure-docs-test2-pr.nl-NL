---
title: Understand Azure IoT Hub custom endpoints | Microsoft Docs
description: Developer guide - using routing rules to route device-to-cloud messages to custom endpoints.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 04/09/2018
ms.author: dobett
ms.openlocfilehash: b035c7ef6dfe56c4b4534e081e70d95ea7c14847
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866319"
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="1611c-103">Use message routes and custom endpoints for device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="1611c-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="1611c-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span><span class="sxs-lookup"><span data-stu-id="1611c-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="1611c-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services or custom code.</span><span class="sxs-lookup"><span data-stu-id="1611c-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services or custom code.</span></span> <span data-ttu-id="1611c-106">Each routing rule you configure has the following properties:</span><span class="sxs-lookup"><span data-stu-id="1611c-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="1611c-107">Property</span><span class="sxs-lookup"><span data-stu-id="1611c-107">Property</span></span>      | <span data-ttu-id="1611c-108">Description</span><span class="sxs-lookup"><span data-stu-id="1611c-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="1611c-109">**Name**</span><span class="sxs-lookup"><span data-stu-id="1611c-109">**Name**</span></span>      | <span data-ttu-id="1611c-110">The unique name that identifies the rule.</span><span class="sxs-lookup"><span data-stu-id="1611c-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="1611c-111">**Source**</span><span class="sxs-lookup"><span data-stu-id="1611c-111">**Source**</span></span>    | <span data-ttu-id="1611c-112">The origin of the data stream to be acted upon.</span><span class="sxs-lookup"><span data-stu-id="1611c-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="1611c-113">For example, device telemetry.</span><span class="sxs-lookup"><span data-stu-id="1611c-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="1611c-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="1611c-114">**Condition**</span></span> | <span data-ttu-id="1611c-115">The query expression for the routing rule that is run against the message's headers and body and determines if it is a match for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="1611c-115">The query expression for the routing rule that is run against the message's headers and body and determines if it is a match for the endpoint.</span></span> <span data-ttu-id="1611c-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="1611c-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="1611c-117">**Endpoint**</span><span class="sxs-lookup"><span data-stu-id="1611c-117">**Endpoint**</span></span>  | <span data-ttu-id="1611c-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span><span class="sxs-lookup"><span data-stu-id="1611c-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="1611c-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span><span class="sxs-lookup"><span data-stu-id="1611c-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="1611c-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span><span class="sxs-lookup"><span data-stu-id="1611c-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="1611c-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that have the same destination, it is only written once to that destination.</span><span class="sxs-lookup"><span data-stu-id="1611c-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that have the same destination, it is only written once to that destination.</span></span>

## <a name="endpoints-and-routing"></a><span data-ttu-id="1611c-122">Endpoints and routing</span><span class="sxs-lookup"><span data-stu-id="1611c-122">Endpoints and routing</span></span>

<span data-ttu-id="1611c-123">An IoT hub has a default [built-in endpoint][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="1611c-123">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="1611c-124">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span><span class="sxs-lookup"><span data-stu-id="1611c-124">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="1611c-125">IoT Hub currently supports Azure Storage containers, Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="1611c-125">IoT Hub currently supports Azure Storage containers, Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

<span data-ttu-id="1611c-126">When you use routing and custom endpoints, messages are only delivered to the built-in endpoint if they don't match any rules.</span><span class="sxs-lookup"><span data-stu-id="1611c-126">When you use routing and custom endpoints, messages are only delivered to the built-in endpoint if they don't match any rules.</span></span> <span data-ttu-id="1611c-127">To deliver messages to the built-in endpoint as well as to a custom endpoint, add a route that sends messages to the **events** endpoint.</span><span class="sxs-lookup"><span data-stu-id="1611c-127">To deliver messages to the built-in endpoint as well as to a custom endpoint, add a route that sends messages to the **events** endpoint.</span></span>

> [!NOTE]
> <span data-ttu-id="1611c-128">IoT Hub only supports writing data to Azure Storage containers as blobs.</span><span class="sxs-lookup"><span data-stu-id="1611c-128">IoT Hub only supports writing data to Azure Storage containers as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="1611c-129">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="1611c-129">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="1611c-130">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="1611c-130">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="1611c-131">For more information about reading from custom endpoints, see:</span><span class="sxs-lookup"><span data-stu-id="1611c-131">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="1611c-132">Reading from [Azure Storage containers][lnk-getstarted-storage].</span><span class="sxs-lookup"><span data-stu-id="1611c-132">Reading from [Azure Storage containers][lnk-getstarted-storage].</span></span>
* <span data-ttu-id="1611c-133">Reading from [Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="1611c-133">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="1611c-134">Reading from [Service Bus queues][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="1611c-134">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="1611c-135">Reading from [Service Bus topics][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="1611c-135">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

## <a name="latency"></a><span data-ttu-id="1611c-136">Latency</span><span class="sxs-lookup"><span data-stu-id="1611c-136">Latency</span></span>

<span data-ttu-id="1611c-137">When you route device-to-cloud telemetry messages using built-in endpoints, there is a slight increase in the end-to-end latency after the creation of the first route.</span><span class="sxs-lookup"><span data-stu-id="1611c-137">When you route device-to-cloud telemetry messages using built-in endpoints, there is a slight increase in the end-to-end latency after the creation of the first route.</span></span>

<span data-ttu-id="1611c-138">In most cases, the average increase in latency is less than one second.</span><span class="sxs-lookup"><span data-stu-id="1611c-138">In most cases, the average increase in latency is less than one second.</span></span> <span data-ttu-id="1611c-139">You can monitor the latency using **d2c.endpoints.latency.builtIn.events** [IoT Hub metric](https://docs.microsoft.com/azure/iot-hub/iot-hub-metrics).</span><span class="sxs-lookup"><span data-stu-id="1611c-139">You can monitor the latency using **d2c.endpoints.latency.builtIn.events** [IoT Hub metric](https://docs.microsoft.com/azure/iot-hub/iot-hub-metrics).</span></span> <span data-ttu-id="1611c-140">Creating or deleting any route after the first one does not impact the end-to-end latency.</span><span class="sxs-lookup"><span data-stu-id="1611c-140">Creating or deleting any route after the first one does not impact the end-to-end latency.</span></span>

### <a name="next-steps"></a><span data-ttu-id="1611c-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="1611c-141">Next steps</span></span>

<span data-ttu-id="1611c-142">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="1611c-142">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="1611c-143">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="1611c-143">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="1611c-144">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="1611c-144">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: tutorial-routing.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
[lnk-getstarted-storage]: ../storage/blobs/storage-blobs-introduction.md
