---
title: Use Azure Event Grid with events in CloudEvents schema
description: Describes how to set the CloudEvents schema for events in Azure Event Grid.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: conceptual
ms.date: 07/13/2018
ms.author: babanisa
ms.openlocfilehash: 4f1f0e95ae74ef41ed91be55f4c964671e8f723b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866594"
---
# <a name="use-cloudevents-schema-with-event-grid"></a><span data-ttu-id="34ad4-103">Use CloudEvents schema with Event Grid</span><span class="sxs-lookup"><span data-stu-id="34ad4-103">Use CloudEvents schema with Event Grid</span></span>

<span data-ttu-id="34ad4-104">In addition to its [default event schema](event-schema.md), Azure Event Grid natively supports events in the [CloudEvents JSON schema](https://github.com/cloudevents/spec/blob/master/json-format.md).</span><span class="sxs-lookup"><span data-stu-id="34ad4-104">In addition to its [default event schema](event-schema.md), Azure Event Grid natively supports events in the [CloudEvents JSON schema](https://github.com/cloudevents/spec/blob/master/json-format.md).</span></span> <span data-ttu-id="34ad4-105">[CloudEvents](http://cloudevents.io/) is an [open standard specification](https://github.com/cloudevents/spec/blob/master/spec.md) for describing event data in a common way.</span><span class="sxs-lookup"><span data-stu-id="34ad4-105">[CloudEvents](http://cloudevents.io/) is an [open standard specification](https://github.com/cloudevents/spec/blob/master/spec.md) for describing event data in a common way.</span></span>

<span data-ttu-id="34ad4-106">CloudEvents simplifies interoperability by providing a common event schema for publishing, and consuming cloud based events.</span><span class="sxs-lookup"><span data-stu-id="34ad4-106">CloudEvents simplifies interoperability by providing a common event schema for publishing, and consuming cloud based events.</span></span> <span data-ttu-id="34ad4-107">This schema allows for uniform tooling, standard ways of routing & handling events, and universal ways of deserializing the outer event schema.</span><span class="sxs-lookup"><span data-stu-id="34ad4-107">This schema allows for uniform tooling, standard ways of routing & handling events, and universal ways of deserializing the outer event schema.</span></span> <span data-ttu-id="34ad4-108">With a common schema, you can more easily integrate work across platforms.</span><span class="sxs-lookup"><span data-stu-id="34ad4-108">With a common schema, you can more easily integrate work across platforms.</span></span>

<span data-ttu-id="34ad4-109">CloudEvents is being build by several [collaborators](https://github.com/cloudevents/spec/blob/master/community/contributors.md), including Microsoft, through the [Cloud Native Compute Foundation](https://www.cncf.io/).</span><span class="sxs-lookup"><span data-stu-id="34ad4-109">CloudEvents is being build by several [collaborators](https://github.com/cloudevents/spec/blob/master/community/contributors.md), including Microsoft, through the [Cloud Native Compute Foundation](https://www.cncf.io/).</span></span> <span data-ttu-id="34ad4-110">It's currently available as version 0.1.</span><span class="sxs-lookup"><span data-stu-id="34ad4-110">It's currently available as version 0.1.</span></span>

<span data-ttu-id="34ad4-111">This article describes how to use the CloudEvents schema with Event Grid.</span><span class="sxs-lookup"><span data-stu-id="34ad4-111">This article describes how to use the CloudEvents schema with Event Grid.</span></span>

[!INCLUDE [event-grid-preview-feature-note.md](../../includes/event-grid-preview-feature-note.md)]

## <a name="cloudevent-schema"></a><span data-ttu-id="34ad4-112">CloudEvent schema</span><span class="sxs-lookup"><span data-stu-id="34ad4-112">CloudEvent schema</span></span>

<span data-ttu-id="34ad4-113">Here is an example of an Azure Blob Storage event in CloudEvents format:</span><span class="sxs-lookup"><span data-stu-id="34ad4-113">Here is an example of an Azure Blob Storage event in CloudEvents format:</span></span>

``` JSON
{
    "cloudEventsVersion" : "0.1",
    "eventType" : "Microsoft.Storage.BlobCreated",
    "eventTypeVersion" : "",
    "source" : "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-account}#blobServices/default/containers/{storage-container}/blobs/{new-file}",
    "eventID" : "173d9985-401e-0075-2497-de268c06ff25",
    "eventTime" : "2018-04-28T02:18:47.1281675Z",
    "data" : {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
}
```

<span data-ttu-id="34ad4-114">CloudEvents v0.1 has the following properties available:</span><span class="sxs-lookup"><span data-stu-id="34ad4-114">CloudEvents v0.1 has the following properties available:</span></span>

| <span data-ttu-id="34ad4-115">CloudEvents</span><span class="sxs-lookup"><span data-stu-id="34ad4-115">CloudEvents</span></span>        | <span data-ttu-id="34ad4-116">Type</span><span class="sxs-lookup"><span data-stu-id="34ad4-116">Type</span></span>     | <span data-ttu-id="34ad4-117">Example JSON Value</span><span class="sxs-lookup"><span data-stu-id="34ad4-117">Example JSON Value</span></span>             | <span data-ttu-id="34ad4-118">Description</span><span class="sxs-lookup"><span data-stu-id="34ad4-118">Description</span></span>                                                        | <span data-ttu-id="34ad4-119">Event Grid Mapping</span><span class="sxs-lookup"><span data-stu-id="34ad4-119">Event Grid Mapping</span></span>
|--------------------|----------|--------------------------------|--------------------------------------------------------------------|-------------------------
| <span data-ttu-id="34ad4-120">eventType</span><span class="sxs-lookup"><span data-stu-id="34ad4-120">eventType</span></span>          | <span data-ttu-id="34ad4-121">String</span><span class="sxs-lookup"><span data-stu-id="34ad4-121">String</span></span>   | <span data-ttu-id="34ad4-122">"com.example.someevent"</span><span class="sxs-lookup"><span data-stu-id="34ad4-122">"com.example.someevent"</span></span>          | <span data-ttu-id="34ad4-123">Type of occurrence that happened</span><span class="sxs-lookup"><span data-stu-id="34ad4-123">Type of occurrence that happened</span></span>                                   | <span data-ttu-id="34ad4-124">eventType</span><span class="sxs-lookup"><span data-stu-id="34ad4-124">eventType</span></span>
| <span data-ttu-id="34ad4-125">eventTypeVersion</span><span class="sxs-lookup"><span data-stu-id="34ad4-125">eventTypeVersion</span></span>   | <span data-ttu-id="34ad4-126">String</span><span class="sxs-lookup"><span data-stu-id="34ad4-126">String</span></span>   | <span data-ttu-id="34ad4-127">"1.0"</span><span class="sxs-lookup"><span data-stu-id="34ad4-127">"1.0"</span></span>                            | <span data-ttu-id="34ad4-128">The version of the eventType (Optional)</span><span class="sxs-lookup"><span data-stu-id="34ad4-128">The version of the eventType (Optional)</span></span>                            | <span data-ttu-id="34ad4-129">dataVersion</span><span class="sxs-lookup"><span data-stu-id="34ad4-129">dataVersion</span></span>
| <span data-ttu-id="34ad4-130">cloudEventsVersion</span><span class="sxs-lookup"><span data-stu-id="34ad4-130">cloudEventsVersion</span></span> | <span data-ttu-id="34ad4-131">String</span><span class="sxs-lookup"><span data-stu-id="34ad4-131">String</span></span>   | <span data-ttu-id="34ad4-132">"0.1"</span><span class="sxs-lookup"><span data-stu-id="34ad4-132">"0.1"</span></span>                            | <span data-ttu-id="34ad4-133">The version of the CloudEvents specification the event uses</span><span class="sxs-lookup"><span data-stu-id="34ad4-133">The version of the CloudEvents specification the event uses</span></span>        | <span data-ttu-id="34ad4-134">*passed through*</span><span class="sxs-lookup"><span data-stu-id="34ad4-134">*passed through*</span></span>
| <span data-ttu-id="34ad4-135">source</span><span class="sxs-lookup"><span data-stu-id="34ad4-135">source</span></span>             | <span data-ttu-id="34ad4-136">URI</span><span class="sxs-lookup"><span data-stu-id="34ad4-136">URI</span></span>      | <span data-ttu-id="34ad4-137">"/mycontext"</span><span class="sxs-lookup"><span data-stu-id="34ad4-137">"/mycontext"</span></span>                     | <span data-ttu-id="34ad4-138">Describes the event producer</span><span class="sxs-lookup"><span data-stu-id="34ad4-138">Describes the event producer</span></span>                                       | <span data-ttu-id="34ad4-139">topic#subject</span><span class="sxs-lookup"><span data-stu-id="34ad4-139">topic#subject</span></span>
| <span data-ttu-id="34ad4-140">eventID</span><span class="sxs-lookup"><span data-stu-id="34ad4-140">eventID</span></span>            | <span data-ttu-id="34ad4-141">String</span><span class="sxs-lookup"><span data-stu-id="34ad4-141">String</span></span>   | <span data-ttu-id="34ad4-142">"1234-1234-1234"</span><span class="sxs-lookup"><span data-stu-id="34ad4-142">"1234-1234-1234"</span></span>                 | <span data-ttu-id="34ad4-143">ID of the event</span><span class="sxs-lookup"><span data-stu-id="34ad4-143">ID of the event</span></span>                                                    | <span data-ttu-id="34ad4-144">id</span><span class="sxs-lookup"><span data-stu-id="34ad4-144">id</span></span>
| <span data-ttu-id="34ad4-145">eventTime</span><span class="sxs-lookup"><span data-stu-id="34ad4-145">eventTime</span></span>          | <span data-ttu-id="34ad4-146">Timestamp</span><span class="sxs-lookup"><span data-stu-id="34ad4-146">Timestamp</span></span>| <span data-ttu-id="34ad4-147">"2018-04-05T17:31:00Z"</span><span class="sxs-lookup"><span data-stu-id="34ad4-147">"2018-04-05T17:31:00Z"</span></span>           | <span data-ttu-id="34ad4-148">Timestamp of when the event happened (Optional)</span><span class="sxs-lookup"><span data-stu-id="34ad4-148">Timestamp of when the event happened (Optional)</span></span>                    | <span data-ttu-id="34ad4-149">eventTime</span><span class="sxs-lookup"><span data-stu-id="34ad4-149">eventTime</span></span>
| <span data-ttu-id="34ad4-150">schemaURL</span><span class="sxs-lookup"><span data-stu-id="34ad4-150">schemaURL</span></span>          | <span data-ttu-id="34ad4-151">URI</span><span class="sxs-lookup"><span data-stu-id="34ad4-151">URI</span></span>      | <span data-ttu-id="34ad4-152">"https://myschema.com"</span><span class="sxs-lookup"><span data-stu-id="34ad4-152">"https://myschema.com"</span></span>           | <span data-ttu-id="34ad4-153">A link to the schema that the data attribute adheres to (Optional)</span><span class="sxs-lookup"><span data-stu-id="34ad4-153">A link to the schema that the data attribute adheres to (Optional)</span></span> | <span data-ttu-id="34ad4-154">*not used*</span><span class="sxs-lookup"><span data-stu-id="34ad4-154">*not used*</span></span>
| <span data-ttu-id="34ad4-155">contentType</span><span class="sxs-lookup"><span data-stu-id="34ad4-155">contentType</span></span>        | <span data-ttu-id="34ad4-156">String</span><span class="sxs-lookup"><span data-stu-id="34ad4-156">String</span></span>   | <span data-ttu-id="34ad4-157">"application/json"</span><span class="sxs-lookup"><span data-stu-id="34ad4-157">"application/json"</span></span>               | <span data-ttu-id="34ad4-158">Describe the data encoding format (Optional)</span><span class="sxs-lookup"><span data-stu-id="34ad4-158">Describe the data encoding format (Optional)</span></span>                       | <span data-ttu-id="34ad4-159">*not used*</span><span class="sxs-lookup"><span data-stu-id="34ad4-159">*not used*</span></span>
| <span data-ttu-id="34ad4-160">extensions</span><span class="sxs-lookup"><span data-stu-id="34ad4-160">extensions</span></span>         | <span data-ttu-id="34ad4-161">Map</span><span class="sxs-lookup"><span data-stu-id="34ad4-161">Map</span></span>      | <span data-ttu-id="34ad4-162">{ "extA": "vA", "extB", "vB" }</span><span class="sxs-lookup"><span data-stu-id="34ad4-162">{ "extA": "vA", "extB", "vB" }</span></span>  | <span data-ttu-id="34ad4-163">Any additional metadata (Optional)</span><span class="sxs-lookup"><span data-stu-id="34ad4-163">Any additional metadata (Optional)</span></span>                                 | <span data-ttu-id="34ad4-164">*not used*</span><span class="sxs-lookup"><span data-stu-id="34ad4-164">*not used*</span></span>
| <span data-ttu-id="34ad4-165">data</span><span class="sxs-lookup"><span data-stu-id="34ad4-165">data</span></span>               | <span data-ttu-id="34ad4-166">Object</span><span class="sxs-lookup"><span data-stu-id="34ad4-166">Object</span></span>   | <span data-ttu-id="34ad4-167">{ "objA": "vA", "objB", "vB" }</span><span class="sxs-lookup"><span data-stu-id="34ad4-167">{ "objA": "vA", "objB", "vB" }</span></span>  | <span data-ttu-id="34ad4-168">The event payload (Optional)</span><span class="sxs-lookup"><span data-stu-id="34ad4-168">The event payload (Optional)</span></span>                                       | <span data-ttu-id="34ad4-169">data</span><span class="sxs-lookup"><span data-stu-id="34ad4-169">data</span></span>

<span data-ttu-id="34ad4-170">For more information, see the [CloudEvents spec](https://github.com/cloudevents/spec/blob/master/spec.md#context-attributes).</span><span class="sxs-lookup"><span data-stu-id="34ad4-170">For more information, see the [CloudEvents spec](https://github.com/cloudevents/spec/blob/master/spec.md#context-attributes).</span></span>

<span data-ttu-id="34ad4-171">The headers values for events delivered in the CloudEvents schema and the Event Grid schema are the same, with the exception of `content-type`.</span><span class="sxs-lookup"><span data-stu-id="34ad4-171">The headers values for events delivered in the CloudEvents schema and the Event Grid schema are the same, with the exception of `content-type`.</span></span> <span data-ttu-id="34ad4-172">For CloudEvents schema, that header value is `"content-type":"application/cloudevents+json; charset=utf-8"`.</span><span class="sxs-lookup"><span data-stu-id="34ad4-172">For CloudEvents schema, that header value is `"content-type":"application/cloudevents+json; charset=utf-8"`.</span></span> <span data-ttu-id="34ad4-173">For Event Grid schema, that header value is `"content-type":"application/json; charset=utf-8"`.</span><span class="sxs-lookup"><span data-stu-id="34ad4-173">For Event Grid schema, that header value is `"content-type":"application/json; charset=utf-8"`.</span></span>

## <a name="configure-event-grid-for-cloudevents"></a><span data-ttu-id="34ad4-174">Configure Event Grid for CloudEvents</span><span class="sxs-lookup"><span data-stu-id="34ad4-174">Configure Event Grid for CloudEvents</span></span>

<span data-ttu-id="34ad4-175">You can use Event Grid for both input and output of events in CloudEvents schema.</span><span class="sxs-lookup"><span data-stu-id="34ad4-175">You can use Event Grid for both input and output of events in CloudEvents schema.</span></span> <span data-ttu-id="34ad4-176">You can use CloudEvents for system events, like Blob Storage events and IoT Hub events, and custom events.</span><span class="sxs-lookup"><span data-stu-id="34ad4-176">You can use CloudEvents for system events, like Blob Storage events and IoT Hub events, and custom events.</span></span> <span data-ttu-id="34ad4-177">It can also transform those events on the wire back and forth.</span><span class="sxs-lookup"><span data-stu-id="34ad4-177">It can also transform those events on the wire back and forth.</span></span>


| <span data-ttu-id="34ad4-178">Input schema</span><span class="sxs-lookup"><span data-stu-id="34ad4-178">Input schema</span></span>       | <span data-ttu-id="34ad4-179">Output schema</span><span class="sxs-lookup"><span data-stu-id="34ad4-179">Output schema</span></span>
|--------------------|---------------------
| <span data-ttu-id="34ad4-180">CloudEvents format</span><span class="sxs-lookup"><span data-stu-id="34ad4-180">CloudEvents format</span></span> | <span data-ttu-id="34ad4-181">CloudEvents format</span><span class="sxs-lookup"><span data-stu-id="34ad4-181">CloudEvents format</span></span>
| <span data-ttu-id="34ad4-182">Event Grid format</span><span class="sxs-lookup"><span data-stu-id="34ad4-182">Event Grid format</span></span>  | <span data-ttu-id="34ad4-183">CloudEvents format</span><span class="sxs-lookup"><span data-stu-id="34ad4-183">CloudEvents format</span></span>
| <span data-ttu-id="34ad4-184">CloudEvents format</span><span class="sxs-lookup"><span data-stu-id="34ad4-184">CloudEvents format</span></span> | <span data-ttu-id="34ad4-185">Event Grid format</span><span class="sxs-lookup"><span data-stu-id="34ad4-185">Event Grid format</span></span>
| <span data-ttu-id="34ad4-186">Event Grid format</span><span class="sxs-lookup"><span data-stu-id="34ad4-186">Event Grid format</span></span>  | <span data-ttu-id="34ad4-187">Event Grid format</span><span class="sxs-lookup"><span data-stu-id="34ad4-187">Event Grid format</span></span>

<span data-ttu-id="34ad4-188">For all event schemas, Event Grid requires validation when publishing to an event grid topic and when creating an event subscription.</span><span class="sxs-lookup"><span data-stu-id="34ad4-188">For all event schemas, Event Grid requires validation when publishing to an event grid topic and when creating an event subscription.</span></span> <span data-ttu-id="34ad4-189">For more information, see [Event Grid security and authentication](security-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="34ad4-189">For more information, see [Event Grid security and authentication](security-authentication.md).</span></span>

### <a name="input-schema"></a><span data-ttu-id="34ad4-190">Input schema</span><span class="sxs-lookup"><span data-stu-id="34ad4-190">Input schema</span></span>

<span data-ttu-id="34ad4-191">To set the input schema on a custom topic to CloudEvents, use the following parameter in Azure CLI when you create your custom topic `--input-schema cloudeventv01schema`.</span><span class="sxs-lookup"><span data-stu-id="34ad4-191">To set the input schema on a custom topic to CloudEvents, use the following parameter in Azure CLI when you create your custom topic `--input-schema cloudeventv01schema`.</span></span> <span data-ttu-id="34ad4-192">The custom topic now expects incoming events in CloudEvents v0.1 format.</span><span class="sxs-lookup"><span data-stu-id="34ad4-192">The custom topic now expects incoming events in CloudEvents v0.1 format.</span></span>

<span data-ttu-id="34ad4-193">To create an event grid topic, use:</span><span class="sxs-lookup"><span data-stu-id="34ad4-193">To create an event grid topic, use:</span></span>

```azurecli
# if you have not already installed the extension, do it now.
# This extension is required for preview features.
az extension add --name eventgrid

az eventgrid topic create \
  --name <topic_name> \
  -l westcentralus \
  -g gridResourceGroup \
  --input-schema cloudeventv01schema
```

<span data-ttu-id="34ad4-194">The current version of CloudEvents doesn't support batching of events.</span><span class="sxs-lookup"><span data-stu-id="34ad4-194">The current version of CloudEvents doesn't support batching of events.</span></span> <span data-ttu-id="34ad4-195">To publish events with CloudEvent schema to a topic, publish each event individually.</span><span class="sxs-lookup"><span data-stu-id="34ad4-195">To publish events with CloudEvent schema to a topic, publish each event individually.</span></span>

### <a name="output-schema"></a><span data-ttu-id="34ad4-196">Output schema</span><span class="sxs-lookup"><span data-stu-id="34ad4-196">Output schema</span></span>

<span data-ttu-id="34ad4-197">To set the output schema on an event subscription to CloudEvents, use the following parameter in Azure CLI when you create your Event Subscription `--event-delivery-schema cloudeventv01schema`.</span><span class="sxs-lookup"><span data-stu-id="34ad4-197">To set the output schema on an event subscription to CloudEvents, use the following parameter in Azure CLI when you create your Event Subscription `--event-delivery-schema cloudeventv01schema`.</span></span> <span data-ttu-id="34ad4-198">Events for this event subscription are now be delivered in CloudEvents v0.1 format.</span><span class="sxs-lookup"><span data-stu-id="34ad4-198">Events for this event subscription are now be delivered in CloudEvents v0.1 format.</span></span>

<span data-ttu-id="34ad4-199">To create an event subscription, use:</span><span class="sxs-lookup"><span data-stu-id="34ad4-199">To create an event subscription, use:</span></span>

```azurecli
az eventgrid event-subscription create \
  --name <event_subscription_name> \
  --topic-name <topic_name> \
  -g gridResourceGroup \
  --endpoint <endpoint_URL> \
  --event-delivery-schema cloudeventv01schema
```

<span data-ttu-id="34ad4-200">The current version of the CloudEvents doesn't support batching of events.</span><span class="sxs-lookup"><span data-stu-id="34ad4-200">The current version of the CloudEvents doesn't support batching of events.</span></span> <span data-ttu-id="34ad4-201">An event subscription that's configured for CloudEvent schema receives each event individually.</span><span class="sxs-lookup"><span data-stu-id="34ad4-201">An event subscription that's configured for CloudEvent schema receives each event individually.</span></span> <span data-ttu-id="34ad4-202">Currently, you can't use an Event Grid trigger for an Azure Functions app when the event is delivered in the CloudEvents schema.</span><span class="sxs-lookup"><span data-stu-id="34ad4-202">Currently, you can't use an Event Grid trigger for an Azure Functions app when the event is delivered in the CloudEvents schema.</span></span> <span data-ttu-id="34ad4-203">You must use an HTTP trigger.</span><span class="sxs-lookup"><span data-stu-id="34ad4-203">You must use an HTTP trigger.</span></span> <span data-ttu-id="34ad4-204">For examples of implementing an HTTP trigger that receives events in the CloudEvents schema, see [Use an HTTP trigger as an Event Grid trigger](../azure-functions/functions-bindings-event-grid.md#use-an-http-trigger-as-an-event-grid-trigger).</span><span class="sxs-lookup"><span data-stu-id="34ad4-204">For examples of implementing an HTTP trigger that receives events in the CloudEvents schema, see [Use an HTTP trigger as an Event Grid trigger](../azure-functions/functions-bindings-event-grid.md#use-an-http-trigger-as-an-event-grid-trigger).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34ad4-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="34ad4-205">Next steps</span></span>

* <span data-ttu-id="34ad4-206">For information about monitoring event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="34ad4-206">For information about monitoring event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).</span></span>
* <span data-ttu-id="34ad4-207">We encourage you to test, comment on, and [contribute](https://github.com/cloudevents/spec/blob/master/CONTRIBUTING.md) to CloudEvents.</span><span class="sxs-lookup"><span data-stu-id="34ad4-207">We encourage you to test, comment on, and [contribute](https://github.com/cloudevents/spec/blob/master/CONTRIBUTING.md) to CloudEvents.</span></span>
* <span data-ttu-id="34ad4-208">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="34ad4-208">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
