---
title: Azure Event Grid event schema
description: Describes the properties that are provided for events with Azure Event Grid
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 07/20/2018
ms.author: babanisa
ms.openlocfilehash: f7be7e5f5e51a47b95d39047af9bcf08e463ca34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857119"
---
# <a name="azure-event-grid-event-schema"></a><span data-ttu-id="3f74a-103">Azure Event Grid event schema</span><span class="sxs-lookup"><span data-stu-id="3f74a-103">Azure Event Grid event schema</span></span>

<span data-ttu-id="3f74a-104">This article describes the properties and schema that are present for all events.</span><span class="sxs-lookup"><span data-stu-id="3f74a-104">This article describes the properties and schema that are present for all events.</span></span> <span data-ttu-id="3f74a-105">Events consist of a set of five required string properties and a required data object.</span><span class="sxs-lookup"><span data-stu-id="3f74a-105">Events consist of a set of five required string properties and a required data object.</span></span> <span data-ttu-id="3f74a-106">The properties are common to all events from any publisher.</span><span class="sxs-lookup"><span data-stu-id="3f74a-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="3f74a-107">The data object has properties that are specific to each publisher.</span><span class="sxs-lookup"><span data-stu-id="3f74a-107">The data object has properties that are specific to each publisher.</span></span> <span data-ttu-id="3f74a-108">For system topics, these properties are specific to the resource provider, such as Azure Storage or Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3f74a-108">For system topics, these properties are specific to the resource provider, such as Azure Storage or Azure Event Hubs.</span></span>

<span data-ttu-id="3f74a-109">Event sources send events to Azure Event Grid in an array, which can have several event objects.</span><span class="sxs-lookup"><span data-stu-id="3f74a-109">Event sources send events to Azure Event Grid in an array, which can have several event objects.</span></span> <span data-ttu-id="3f74a-110">When posting events to an event grid topic, the array can have a total size of up to 1 MB.</span><span class="sxs-lookup"><span data-stu-id="3f74a-110">When posting events to an event grid topic, the array can have a total size of up to 1 MB.</span></span> <span data-ttu-id="3f74a-111">Each event in the array is limited to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="3f74a-111">Each event in the array is limited to 64 KB.</span></span> <span data-ttu-id="3f74a-112">If an event or the array is greater than the size limits, you receive the response **413 Payload Too Large**.</span><span class="sxs-lookup"><span data-stu-id="3f74a-112">If an event or the array is greater than the size limits, you receive the response **413 Payload Too Large**.</span></span>

<span data-ttu-id="3f74a-113">Event Grid sends the events to subscribers in an array that has a single event.</span><span class="sxs-lookup"><span data-stu-id="3f74a-113">Event Grid sends the events to subscribers in an array that has a single event.</span></span> <span data-ttu-id="3f74a-114">This behavior may change in the future.</span><span class="sxs-lookup"><span data-stu-id="3f74a-114">This behavior may change in the future.</span></span>

<span data-ttu-id="3f74a-115">You can find the JSON schema for the Event Grid event and each Azure publisher's data payload in the [Event Schema store](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/eventgrid/data-plane).</span><span class="sxs-lookup"><span data-stu-id="3f74a-115">You can find the JSON schema for the Event Grid event and each Azure publisher's data payload in the [Event Schema store](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/eventgrid/data-plane).</span></span>

## <a name="event-schema"></a><span data-ttu-id="3f74a-116">Event schema</span><span class="sxs-lookup"><span data-stu-id="3f74a-116">Event schema</span></span>

<span data-ttu-id="3f74a-117">The following example shows the properties that are used by all event publishers:</span><span class="sxs-lookup"><span data-stu-id="3f74a-117">The following example shows the properties that are used by all event publishers:</span></span>

```json
[
  {
    "topic": string,
    "subject": string,
    "id": string,
    "eventType": string,
    "eventTime": string,
    "data":{
      object-unique-to-each-publisher
    },
    "dataVersion": string,
    "metadataVersion": string
  }
]
```

<span data-ttu-id="3f74a-118">For example, the schema published for an Azure Blob storage event is:</span><span class="sxs-lookup"><span data-stu-id="3f74a-118">For example, the schema published for an Azure Blob storage event is:</span></span>

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
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
    },
    "dataVersion": "",
    "metadataVersion": "1"
  }
]
```

## <a name="event-properties"></a><span data-ttu-id="3f74a-119">Event properties</span><span class="sxs-lookup"><span data-stu-id="3f74a-119">Event properties</span></span>

<span data-ttu-id="3f74a-120">All events have the same following top-level data:</span><span class="sxs-lookup"><span data-stu-id="3f74a-120">All events have the same following top-level data:</span></span>

| <span data-ttu-id="3f74a-121">Property</span><span class="sxs-lookup"><span data-stu-id="3f74a-121">Property</span></span> | <span data-ttu-id="3f74a-122">Type</span><span class="sxs-lookup"><span data-stu-id="3f74a-122">Type</span></span> | <span data-ttu-id="3f74a-123">Description</span><span class="sxs-lookup"><span data-stu-id="3f74a-123">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="3f74a-124">topic</span><span class="sxs-lookup"><span data-stu-id="3f74a-124">topic</span></span> | <span data-ttu-id="3f74a-125">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-125">string</span></span> | <span data-ttu-id="3f74a-126">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="3f74a-126">Full resource path to the event source.</span></span> <span data-ttu-id="3f74a-127">This field isn't writeable.</span><span class="sxs-lookup"><span data-stu-id="3f74a-127">This field isn't writeable.</span></span> <span data-ttu-id="3f74a-128">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="3f74a-128">Event Grid provides this value.</span></span> |
| <span data-ttu-id="3f74a-129">subject</span><span class="sxs-lookup"><span data-stu-id="3f74a-129">subject</span></span> | <span data-ttu-id="3f74a-130">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-130">string</span></span> | <span data-ttu-id="3f74a-131">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="3f74a-131">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="3f74a-132">eventType</span><span class="sxs-lookup"><span data-stu-id="3f74a-132">eventType</span></span> | <span data-ttu-id="3f74a-133">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-133">string</span></span> | <span data-ttu-id="3f74a-134">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="3f74a-134">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="3f74a-135">eventTime</span><span class="sxs-lookup"><span data-stu-id="3f74a-135">eventTime</span></span> | <span data-ttu-id="3f74a-136">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-136">string</span></span> | <span data-ttu-id="3f74a-137">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="3f74a-137">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="3f74a-138">id</span><span class="sxs-lookup"><span data-stu-id="3f74a-138">id</span></span> | <span data-ttu-id="3f74a-139">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-139">string</span></span> | <span data-ttu-id="3f74a-140">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="3f74a-140">Unique identifier for the event.</span></span> |
| <span data-ttu-id="3f74a-141">data</span><span class="sxs-lookup"><span data-stu-id="3f74a-141">data</span></span> | <span data-ttu-id="3f74a-142">object</span><span class="sxs-lookup"><span data-stu-id="3f74a-142">object</span></span> | <span data-ttu-id="3f74a-143">Event data specific to the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f74a-143">Event data specific to the resource provider.</span></span> |
| <span data-ttu-id="3f74a-144">dataVersion</span><span class="sxs-lookup"><span data-stu-id="3f74a-144">dataVersion</span></span> | <span data-ttu-id="3f74a-145">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-145">string</span></span> | <span data-ttu-id="3f74a-146">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="3f74a-146">The schema version of the data object.</span></span> <span data-ttu-id="3f74a-147">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="3f74a-147">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="3f74a-148">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="3f74a-148">metadataVersion</span></span> | <span data-ttu-id="3f74a-149">string</span><span class="sxs-lookup"><span data-stu-id="3f74a-149">string</span></span> | <span data-ttu-id="3f74a-150">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="3f74a-150">The schema version of the event metadata.</span></span> <span data-ttu-id="3f74a-151">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="3f74a-151">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="3f74a-152">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="3f74a-152">Event Grid provides this value.</span></span> |

<span data-ttu-id="3f74a-153">To learn about the properties in the data object, see the event source:</span><span class="sxs-lookup"><span data-stu-id="3f74a-153">To learn about the properties in the data object, see the event source:</span></span>

* [<span data-ttu-id="3f74a-154">Azure subscriptions (management operations)</span><span class="sxs-lookup"><span data-stu-id="3f74a-154">Azure subscriptions (management operations)</span></span>](event-schema-subscriptions.md)
* [<span data-ttu-id="3f74a-155">Container Registry</span><span class="sxs-lookup"><span data-stu-id="3f74a-155">Container Registry</span></span>](event-schema-container-registry.md)
* [<span data-ttu-id="3f74a-156">Blob storage</span><span class="sxs-lookup"><span data-stu-id="3f74a-156">Blob storage</span></span>](event-schema-blob-storage.md)
* [<span data-ttu-id="3f74a-157">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3f74a-157">Event Hubs</span></span>](event-schema-event-hubs.md)
* [<span data-ttu-id="3f74a-158">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3f74a-158">IoT Hub</span></span>](event-schema-iot-hub.md)
* [<span data-ttu-id="3f74a-159">Media Services</span><span class="sxs-lookup"><span data-stu-id="3f74a-159">Media Services</span></span>](../media-services/latest/media-services-event-schemas.md?toc=%2fazure%2fevent-grid%2ftoc.json)
* [<span data-ttu-id="3f74a-160">Resource groups (management operations)</span><span class="sxs-lookup"><span data-stu-id="3f74a-160">Resource groups (management operations)</span></span>](event-schema-resource-groups.md)
* [<span data-ttu-id="3f74a-161">Service Bus</span><span class="sxs-lookup"><span data-stu-id="3f74a-161">Service Bus</span></span>](event-schema-service-bus.md)

<span data-ttu-id="3f74a-162">For custom topics, the event publisher determines the data object.</span><span class="sxs-lookup"><span data-stu-id="3f74a-162">For custom topics, the event publisher determines the data object.</span></span> <span data-ttu-id="3f74a-163">The top-level data should have the same fields as standard resource-defined events.</span><span class="sxs-lookup"><span data-stu-id="3f74a-163">The top-level data should have the same fields as standard resource-defined events.</span></span>

<span data-ttu-id="3f74a-164">When publishing events to custom topics, create subjects for your events that make it easy for subscribers to know whether they're interested in the event.</span><span class="sxs-lookup"><span data-stu-id="3f74a-164">When publishing events to custom topics, create subjects for your events that make it easy for subscribers to know whether they're interested in the event.</span></span> <span data-ttu-id="3f74a-165">Subscribers use the subject to filter and route events.</span><span class="sxs-lookup"><span data-stu-id="3f74a-165">Subscribers use the subject to filter and route events.</span></span> <span data-ttu-id="3f74a-166">Consider providing the path for where the event happened, so subscribers can filter by segments of that path.</span><span class="sxs-lookup"><span data-stu-id="3f74a-166">Consider providing the path for where the event happened, so subscribers can filter by segments of that path.</span></span> <span data-ttu-id="3f74a-167">The path enables subscribers to narrowly or broadly filter events.</span><span class="sxs-lookup"><span data-stu-id="3f74a-167">The path enables subscribers to narrowly or broadly filter events.</span></span> <span data-ttu-id="3f74a-168">For example, if you provide a three segment path like `/A/B/C` in the subject, subscribers can filter by the first segment `/A` to get a broad set of events.</span><span class="sxs-lookup"><span data-stu-id="3f74a-168">For example, if you provide a three segment path like `/A/B/C` in the subject, subscribers can filter by the first segment `/A` to get a broad set of events.</span></span> <span data-ttu-id="3f74a-169">Those subscribers get events with subjects like `/A/B/C` or `/A/D/E`.</span><span class="sxs-lookup"><span data-stu-id="3f74a-169">Those subscribers get events with subjects like `/A/B/C` or `/A/D/E`.</span></span> <span data-ttu-id="3f74a-170">Other subscribers can filter by `/A/B` to get a narrower set of events.</span><span class="sxs-lookup"><span data-stu-id="3f74a-170">Other subscribers can filter by `/A/B` to get a narrower set of events.</span></span>

<span data-ttu-id="3f74a-171">Sometimes your subject needs more detail about what happened.</span><span class="sxs-lookup"><span data-stu-id="3f74a-171">Sometimes your subject needs more detail about what happened.</span></span> <span data-ttu-id="3f74a-172">For example, the **Storage Accounts** publisher provides the subject `/blobServices/default/containers/<container-name>/blobs/<file>` when a file is added to a container.</span><span class="sxs-lookup"><span data-stu-id="3f74a-172">For example, the **Storage Accounts** publisher provides the subject `/blobServices/default/containers/<container-name>/blobs/<file>` when a file is added to a container.</span></span> <span data-ttu-id="3f74a-173">A subscriber could filter by the path `/blobServices/default/containers/testcontainer` to get all events for that container but not other containers in the storage account.</span><span class="sxs-lookup"><span data-stu-id="3f74a-173">A subscriber could filter by the path `/blobServices/default/containers/testcontainer` to get all events for that container but not other containers in the storage account.</span></span> <span data-ttu-id="3f74a-174">A subscriber could also filter or route by the suffix `.txt` to only work with text files.</span><span class="sxs-lookup"><span data-stu-id="3f74a-174">A subscriber could also filter or route by the suffix `.txt` to only work with text files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f74a-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f74a-175">Next steps</span></span>

* <span data-ttu-id="3f74a-176">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="3f74a-176">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="3f74a-177">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3f74a-177">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
