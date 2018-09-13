---
title: Azure Event Grid Service Bus event schema
description: Describes the properties that are provided for Service Bus events with Azure Event Grid
services: event-grid
author: banisadr
manager: darosa
ms.service: event-grid
ms.topic: reference
ms.date: 08/17/2018
ms.author: babanisa
ms.openlocfilehash: afb85f20c49821ca98e078791730a3376198e9e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965672"
---
# <a name="azure-event-grid-event-schema-for-service-bus"></a><span data-ttu-id="d7c87-103">Azure Event Grid event schema for Service Bus</span><span class="sxs-lookup"><span data-stu-id="d7c87-103">Azure Event Grid event schema for Service Bus</span></span>

<span data-ttu-id="d7c87-104">This article provides the properties and schema for Service Bus events.</span><span class="sxs-lookup"><span data-stu-id="d7c87-104">This article provides the properties and schema for Service Bus events.</span></span> <span data-ttu-id="d7c87-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d7c87-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span></span>

<span data-ttu-id="d7c87-106">For a list of sample scripts and tutorials, see [Service Bus event source](event-sources.md#service-bus).</span><span class="sxs-lookup"><span data-stu-id="d7c87-106">For a list of sample scripts and tutorials, see [Service Bus event source](event-sources.md#service-bus).</span></span>

## <a name="available-event-types"></a><span data-ttu-id="d7c87-107">Available event types</span><span class="sxs-lookup"><span data-stu-id="d7c87-107">Available event types</span></span>

<span data-ttu-id="d7c87-108">Service Bus emits the following event types:</span><span class="sxs-lookup"><span data-stu-id="d7c87-108">Service Bus emits the following event types:</span></span>

| <span data-ttu-id="d7c87-109">Event type</span><span class="sxs-lookup"><span data-stu-id="d7c87-109">Event type</span></span> | <span data-ttu-id="d7c87-110">Description</span><span class="sxs-lookup"><span data-stu-id="d7c87-110">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="d7c87-111">Microsoft.ServiceBus.ActiveMessagesAvailableWithNoListeners</span><span class="sxs-lookup"><span data-stu-id="d7c87-111">Microsoft.ServiceBus.ActiveMessagesAvailableWithNoListeners</span></span> | <span data-ttu-id="d7c87-112">Raised when there are active messages in a Queue or Subscription and no receivers listening.</span><span class="sxs-lookup"><span data-stu-id="d7c87-112">Raised when there are active messages in a Queue or Subscription and no receivers listening.</span></span> |
| <span data-ttu-id="d7c87-113">Microsoft.ServiceBus.DeadletterMessagesAvailableWithNoListener</span><span class="sxs-lookup"><span data-stu-id="d7c87-113">Microsoft.ServiceBus.DeadletterMessagesAvailableWithNoListener</span></span> | <span data-ttu-id="d7c87-114">Raised when there are active messages in a Dead Letter Queue and no active listeners.</span><span class="sxs-lookup"><span data-stu-id="d7c87-114">Raised when there are active messages in a Dead Letter Queue and no active listeners.</span></span> |

## <a name="example-event"></a><span data-ttu-id="d7c87-115">Example event</span><span class="sxs-lookup"><span data-stu-id="d7c87-115">Example event</span></span>

<span data-ttu-id="d7c87-116">The following example shows the schema of active messages with no listeners event:</span><span class="sxs-lookup"><span data-stu-id="d7c87-116">The following example shows the schema of active messages with no listeners event:</span></span>

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourcegroups/{your-rg}/providers/Microsoft.ServiceBus/namespaces/{your-service-bus-namespace}",
  "subject": "topics/{your-service-bus-topic}/subscriptions/{your-service-bus-subscription}",
  "eventType": "Microsoft.ServiceBus.ActiveMessagesAvailableWithNoListeners",
  "eventTime": "2018-02-14T05:12:53.4133526Z",
  "id": "dede87b0-3656-419c-acaf-70c95ddc60f5",
  "data": {
    "namespaceName": "YOUR SERVICE BUS NAMESPACE WILL SHOW HERE",
    "requestUri": "https://{your-service-bus-namespace}.servicebus.windows.net/{your-topic}/subscriptions/{your-service-bus-subscription}/messages/head",
    "entityType": "subscriber",
    "queueName": "QUEUE NAME IF QUEUE",
    "topicName": "TOPIC NAME IF TOPIC",
    "subscriptionName": "SUBSCRIPTION NAME"
  },
  "dataVersion": "1",
  "metadataVersion": "1"
}]
```

<span data-ttu-id="d7c87-117">The schema for a dead letter queue event is similar:</span><span class="sxs-lookup"><span data-stu-id="d7c87-117">The schema for a dead letter queue event is similar:</span></span>

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourcegroups/{your-rg}/providers/Microsoft.ServiceBus/namespaces/{your-service-bus-namespace}",
  "subject": "topics/{your-service-bus-topic}/subscriptions/{your-service-bus-subscription}",
  "eventType": "Microsoft.ServiceBus.DeadletterMessagesAvailableWithNoListener",
  "eventTime": "2018-02-14T05:12:53.4133526Z",
  "id": "dede87b0-3656-419c-acaf-70c95ddc60f5",
  "data": {
    "namespaceName": "YOUR SERVICE BUS NAMESPACE WILL SHOW HERE",
    "requestUri": "https://{your-service-bus-namespace}.servicebus.windows.net/{your-topic}/subscriptions/{your-service-bus-subscription}/$deadletterqueue/messages/head",
    "entityType": "subscriber",
    "queueName": "QUEUE NAME IF QUEUE",
    "topicName": "TOPIC NAME IF TOPIC",
    "subscriptionName": "SUBSCRIPTION NAME"
  },
  "dataVersion": "1",
  "metadataVersion": "1"
}]
```

## <a name="event-properties"></a><span data-ttu-id="d7c87-118">Event properties</span><span class="sxs-lookup"><span data-stu-id="d7c87-118">Event properties</span></span>

<span data-ttu-id="d7c87-119">An event has the following top-level data:</span><span class="sxs-lookup"><span data-stu-id="d7c87-119">An event has the following top-level data:</span></span>

| <span data-ttu-id="d7c87-120">Property</span><span class="sxs-lookup"><span data-stu-id="d7c87-120">Property</span></span> | <span data-ttu-id="d7c87-121">Type</span><span class="sxs-lookup"><span data-stu-id="d7c87-121">Type</span></span> | <span data-ttu-id="d7c87-122">Description</span><span class="sxs-lookup"><span data-stu-id="d7c87-122">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="d7c87-123">topic</span><span class="sxs-lookup"><span data-stu-id="d7c87-123">topic</span></span> | <span data-ttu-id="d7c87-124">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-124">string</span></span> | <span data-ttu-id="d7c87-125">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="d7c87-125">Full resource path to the event source.</span></span> <span data-ttu-id="d7c87-126">This field is not writeable.</span><span class="sxs-lookup"><span data-stu-id="d7c87-126">This field is not writeable.</span></span> <span data-ttu-id="d7c87-127">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="d7c87-127">Event Grid provides this value.</span></span> |
| <span data-ttu-id="d7c87-128">subject</span><span class="sxs-lookup"><span data-stu-id="d7c87-128">subject</span></span> | <span data-ttu-id="d7c87-129">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-129">string</span></span> | <span data-ttu-id="d7c87-130">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="d7c87-130">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="d7c87-131">eventType</span><span class="sxs-lookup"><span data-stu-id="d7c87-131">eventType</span></span> | <span data-ttu-id="d7c87-132">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-132">string</span></span> | <span data-ttu-id="d7c87-133">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="d7c87-133">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="d7c87-134">eventTime</span><span class="sxs-lookup"><span data-stu-id="d7c87-134">eventTime</span></span> | <span data-ttu-id="d7c87-135">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-135">string</span></span> | <span data-ttu-id="d7c87-136">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="d7c87-136">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="d7c87-137">id</span><span class="sxs-lookup"><span data-stu-id="d7c87-137">id</span></span> | <span data-ttu-id="d7c87-138">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-138">string</span></span> | <span data-ttu-id="d7c87-139">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="d7c87-139">Unique identifier for the event.</span></span> |
| <span data-ttu-id="d7c87-140">data</span><span class="sxs-lookup"><span data-stu-id="d7c87-140">data</span></span> | <span data-ttu-id="d7c87-141">object</span><span class="sxs-lookup"><span data-stu-id="d7c87-141">object</span></span> | <span data-ttu-id="d7c87-142">Blob storage event data.</span><span class="sxs-lookup"><span data-stu-id="d7c87-142">Blob storage event data.</span></span> |
| <span data-ttu-id="d7c87-143">dataVersion</span><span class="sxs-lookup"><span data-stu-id="d7c87-143">dataVersion</span></span> | <span data-ttu-id="d7c87-144">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-144">string</span></span> | <span data-ttu-id="d7c87-145">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="d7c87-145">The schema version of the data object.</span></span> <span data-ttu-id="d7c87-146">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="d7c87-146">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="d7c87-147">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="d7c87-147">metadataVersion</span></span> | <span data-ttu-id="d7c87-148">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-148">string</span></span> | <span data-ttu-id="d7c87-149">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="d7c87-149">The schema version of the event metadata.</span></span> <span data-ttu-id="d7c87-150">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="d7c87-150">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="d7c87-151">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="d7c87-151">Event Grid provides this value.</span></span> |

<span data-ttu-id="d7c87-152">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="d7c87-152">The data object has the following properties:</span></span>

| <span data-ttu-id="d7c87-153">Property</span><span class="sxs-lookup"><span data-stu-id="d7c87-153">Property</span></span> | <span data-ttu-id="d7c87-154">Type</span><span class="sxs-lookup"><span data-stu-id="d7c87-154">Type</span></span> | <span data-ttu-id="d7c87-155">Description</span><span class="sxs-lookup"><span data-stu-id="d7c87-155">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="d7c87-156">namespaceName</span><span class="sxs-lookup"><span data-stu-id="d7c87-156">namespaceName</span></span> | <span data-ttu-id="d7c87-157">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-157">string</span></span> | <span data-ttu-id="d7c87-158">The Service Bus namespace the resource exists in.</span><span class="sxs-lookup"><span data-stu-id="d7c87-158">The Service Bus namespace the resource exists in.</span></span> |
| <span data-ttu-id="d7c87-159">requestUri</span><span class="sxs-lookup"><span data-stu-id="d7c87-159">requestUri</span></span> | <span data-ttu-id="d7c87-160">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-160">string</span></span> | <span data-ttu-id="d7c87-161">The URI to the specific queue or subscription emitting the event.</span><span class="sxs-lookup"><span data-stu-id="d7c87-161">The URI to the specific queue or subscription emitting the event.</span></span> |
| <span data-ttu-id="d7c87-162">entityType</span><span class="sxs-lookup"><span data-stu-id="d7c87-162">entityType</span></span> | <span data-ttu-id="d7c87-163">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-163">string</span></span> | <span data-ttu-id="d7c87-164">The type of Service Bus entity emitting events (queue or subscription).</span><span class="sxs-lookup"><span data-stu-id="d7c87-164">The type of Service Bus entity emitting events (queue or subscription).</span></span> |
| <span data-ttu-id="d7c87-165">queueName</span><span class="sxs-lookup"><span data-stu-id="d7c87-165">queueName</span></span> | <span data-ttu-id="d7c87-166">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-166">string</span></span> | <span data-ttu-id="d7c87-167">The queue with active messages if subscribing to a queue.</span><span class="sxs-lookup"><span data-stu-id="d7c87-167">The queue with active messages if subscribing to a queue.</span></span> <span data-ttu-id="d7c87-168">Value null if using topics / subscriptions.</span><span class="sxs-lookup"><span data-stu-id="d7c87-168">Value null if using topics / subscriptions.</span></span> |
| <span data-ttu-id="d7c87-169">topicName</span><span class="sxs-lookup"><span data-stu-id="d7c87-169">topicName</span></span> | <span data-ttu-id="d7c87-170">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-170">string</span></span> | <span data-ttu-id="d7c87-171">The topic the Service Bus subscription with active messages belongs to.</span><span class="sxs-lookup"><span data-stu-id="d7c87-171">The topic the Service Bus subscription with active messages belongs to.</span></span> <span data-ttu-id="d7c87-172">Value null if using a queue.</span><span class="sxs-lookup"><span data-stu-id="d7c87-172">Value null if using a queue.</span></span> |
| <span data-ttu-id="d7c87-173">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="d7c87-173">subscriptionName</span></span> | <span data-ttu-id="d7c87-174">string</span><span class="sxs-lookup"><span data-stu-id="d7c87-174">string</span></span> | <span data-ttu-id="d7c87-175">The Service Bus subscription with active messages.</span><span class="sxs-lookup"><span data-stu-id="d7c87-175">The Service Bus subscription with active messages.</span></span> <span data-ttu-id="d7c87-176">Value null if using a queue.</span><span class="sxs-lookup"><span data-stu-id="d7c87-176">Value null if using a queue.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d7c87-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7c87-177">Next steps</span></span>

* <span data-ttu-id="d7c87-178">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="d7c87-178">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="d7c87-179">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d7c87-179">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
* <span data-ttu-id="d7c87-180">For details on using Azure Event Grid with Service Bus, see the [Service Bus to Event Grid integration overview](../service-bus-messaging/service-bus-to-event-grid-integration-concept.md).</span><span class="sxs-lookup"><span data-stu-id="d7c87-180">For details on using Azure Event Grid with Service Bus, see the [Service Bus to Event Grid integration overview](../service-bus-messaging/service-bus-to-event-grid-integration-concept.md).</span></span>
* <span data-ttu-id="d7c87-181">Try [receiving Service Bus events with Functions or Logic Apps](../service-bus-messaging/service-bus-to-event-grid-integration-example.md?toc=%2fazure%2fevent-grid%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7c87-181">Try [receiving Service Bus events with Functions or Logic Apps](../service-bus-messaging/service-bus-to-event-grid-integration-example.md?toc=%2fazure%2fevent-grid%2ftoc.json).</span></span>
