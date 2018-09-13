---
title: Azure Event Grid event hubs event schema
description: Describes the properties that are provided for event hubs events with Azure Event Grid
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: reference
ms.date: 08/17/2018
ms.author: tomfitz
ms.openlocfilehash: e301f3895126ed52b8d4c1f046f69dfcedb3563c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968348"
---
# <a name="azure-event-grid-event-schema-for-event-hubs"></a><span data-ttu-id="2f5b4-103">Azure Event Grid event schema for event hubs</span><span class="sxs-lookup"><span data-stu-id="2f5b4-103">Azure Event Grid event schema for event hubs</span></span>

<span data-ttu-id="2f5b4-104">This article provides the properties and schema for event hubs events.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-104">This article provides the properties and schema for event hubs events.</span></span> <span data-ttu-id="2f5b4-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b4-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span></span>

<span data-ttu-id="2f5b4-106">For a list of sample scripts and tutorials, see [Event Hubs event source](event-sources.md#event-hubs).</span><span class="sxs-lookup"><span data-stu-id="2f5b4-106">For a list of sample scripts and tutorials, see [Event Hubs event source](event-sources.md#event-hubs).</span></span>

### <a name="available-event-types"></a><span data-ttu-id="2f5b4-107">Available event types</span><span class="sxs-lookup"><span data-stu-id="2f5b4-107">Available event types</span></span>

<span data-ttu-id="2f5b4-108">Event Hubs emits the **Microsoft.EventHub.CaptureFileCreated** event type when a capture file is created.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-108">Event Hubs emits the **Microsoft.EventHub.CaptureFileCreated** event type when a capture file is created.</span></span>

## <a name="example-event"></a><span data-ttu-id="2f5b4-109">Example event</span><span class="sxs-lookup"><span data-stu-id="2f5b4-109">Example event</span></span>

<span data-ttu-id="2f5b4-110">This sample event shows the schema of an event hubs event raised when the capture feature stores a file:</span><span class="sxs-lookup"><span data-stu-id="2f5b4-110">This sample event shows the schema of an event hubs event raised when the capture feature stores a file:</span></span> 

```json
[
    {
        "topic": "/subscriptions/<guid>/resourcegroups/rgDataMigrationSample/providers/Microsoft.EventHub/namespaces/tfdatamigratens",
        "subject": "eventhubs/hubdatamigration",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-08-31T19:12:46.0498024Z",
        "id": "14e87d03-6fbf-4bb2-9a21-92bd1281f247",
        "data": {
            "fileUrl": "https://tf0831datamigrate.blob.core.windows.net/windturbinecapture/tfdatamigratens/hubdatamigration/1/2017/08/31/19/11/45.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 249168,
            "eventCount": 1500,
            "firstSequenceNumber": 2400,
            "lastSequenceNumber": 3899,
            "firstEnqueueTime": "2017-08-31T19:12:14.674Z",
            "lastEnqueueTime": "2017-08-31T19:12:44.309Z"
        },
        "dataVersion": "",
        "metadataVersion": "1"
    }
]
```

## <a name="event-properties"></a><span data-ttu-id="2f5b4-111">Event properties</span><span class="sxs-lookup"><span data-stu-id="2f5b4-111">Event properties</span></span>

<span data-ttu-id="2f5b4-112">An event has the following top-level data:</span><span class="sxs-lookup"><span data-stu-id="2f5b4-112">An event has the following top-level data:</span></span>

| <span data-ttu-id="2f5b4-113">Property</span><span class="sxs-lookup"><span data-stu-id="2f5b4-113">Property</span></span> | <span data-ttu-id="2f5b4-114">Type</span><span class="sxs-lookup"><span data-stu-id="2f5b4-114">Type</span></span> | <span data-ttu-id="2f5b4-115">Description</span><span class="sxs-lookup"><span data-stu-id="2f5b4-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="2f5b4-116">topic</span><span class="sxs-lookup"><span data-stu-id="2f5b4-116">topic</span></span> | <span data-ttu-id="2f5b4-117">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-117">string</span></span> | <span data-ttu-id="2f5b4-118">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-118">Full resource path to the event source.</span></span> <span data-ttu-id="2f5b4-119">This field is not writeable.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-119">This field is not writeable.</span></span> <span data-ttu-id="2f5b4-120">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-120">Event Grid provides this value.</span></span> |
| <span data-ttu-id="2f5b4-121">subject</span><span class="sxs-lookup"><span data-stu-id="2f5b4-121">subject</span></span> | <span data-ttu-id="2f5b4-122">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-122">string</span></span> | <span data-ttu-id="2f5b4-123">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-123">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="2f5b4-124">eventType</span><span class="sxs-lookup"><span data-stu-id="2f5b4-124">eventType</span></span> | <span data-ttu-id="2f5b4-125">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-125">string</span></span> | <span data-ttu-id="2f5b4-126">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-126">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="2f5b4-127">eventTime</span><span class="sxs-lookup"><span data-stu-id="2f5b4-127">eventTime</span></span> | <span data-ttu-id="2f5b4-128">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-128">string</span></span> | <span data-ttu-id="2f5b4-129">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-129">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="2f5b4-130">id</span><span class="sxs-lookup"><span data-stu-id="2f5b4-130">id</span></span> | <span data-ttu-id="2f5b4-131">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-131">string</span></span> | <span data-ttu-id="2f5b4-132">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-132">Unique identifier for the event.</span></span> |
| <span data-ttu-id="2f5b4-133">data</span><span class="sxs-lookup"><span data-stu-id="2f5b4-133">data</span></span> | <span data-ttu-id="2f5b4-134">object</span><span class="sxs-lookup"><span data-stu-id="2f5b4-134">object</span></span> | <span data-ttu-id="2f5b4-135">Event hub event data.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-135">Event hub event data.</span></span> |
| <span data-ttu-id="2f5b4-136">dataVersion</span><span class="sxs-lookup"><span data-stu-id="2f5b4-136">dataVersion</span></span> | <span data-ttu-id="2f5b4-137">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-137">string</span></span> | <span data-ttu-id="2f5b4-138">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-138">The schema version of the data object.</span></span> <span data-ttu-id="2f5b4-139">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-139">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="2f5b4-140">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="2f5b4-140">metadataVersion</span></span> | <span data-ttu-id="2f5b4-141">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-141">string</span></span> | <span data-ttu-id="2f5b4-142">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-142">The schema version of the event metadata.</span></span> <span data-ttu-id="2f5b4-143">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-143">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="2f5b4-144">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-144">Event Grid provides this value.</span></span> |

<span data-ttu-id="2f5b4-145">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="2f5b4-145">The data object has the following properties:</span></span>

| <span data-ttu-id="2f5b4-146">Property</span><span class="sxs-lookup"><span data-stu-id="2f5b4-146">Property</span></span> | <span data-ttu-id="2f5b4-147">Type</span><span class="sxs-lookup"><span data-stu-id="2f5b4-147">Type</span></span> | <span data-ttu-id="2f5b4-148">Description</span><span class="sxs-lookup"><span data-stu-id="2f5b4-148">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="2f5b4-149">fileUrl</span><span class="sxs-lookup"><span data-stu-id="2f5b4-149">fileUrl</span></span> | <span data-ttu-id="2f5b4-150">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-150">string</span></span> | <span data-ttu-id="2f5b4-151">The path to the capture file.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-151">The path to the capture file.</span></span> |
| <span data-ttu-id="2f5b4-152">fileType</span><span class="sxs-lookup"><span data-stu-id="2f5b4-152">fileType</span></span> | <span data-ttu-id="2f5b4-153">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-153">string</span></span> | <span data-ttu-id="2f5b4-154">The file type of the capture file.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-154">The file type of the capture file.</span></span> |
| <span data-ttu-id="2f5b4-155">partitionId</span><span class="sxs-lookup"><span data-stu-id="2f5b4-155">partitionId</span></span> | <span data-ttu-id="2f5b4-156">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-156">string</span></span> | <span data-ttu-id="2f5b4-157">The shard ID.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-157">The shard ID.</span></span> |
| <span data-ttu-id="2f5b4-158">sizeInBytes</span><span class="sxs-lookup"><span data-stu-id="2f5b4-158">sizeInBytes</span></span> | <span data-ttu-id="2f5b4-159">integer</span><span class="sxs-lookup"><span data-stu-id="2f5b4-159">integer</span></span> | <span data-ttu-id="2f5b4-160">The file size.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-160">The file size.</span></span> |
| <span data-ttu-id="2f5b4-161">eventCount</span><span class="sxs-lookup"><span data-stu-id="2f5b4-161">eventCount</span></span> | <span data-ttu-id="2f5b4-162">integer</span><span class="sxs-lookup"><span data-stu-id="2f5b4-162">integer</span></span> | <span data-ttu-id="2f5b4-163">The number of events in the file.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-163">The number of events in the file.</span></span> |
| <span data-ttu-id="2f5b4-164">firstSequenceNumber</span><span class="sxs-lookup"><span data-stu-id="2f5b4-164">firstSequenceNumber</span></span> | <span data-ttu-id="2f5b4-165">integer</span><span class="sxs-lookup"><span data-stu-id="2f5b4-165">integer</span></span> | <span data-ttu-id="2f5b4-166">The smallest sequence number from the queue.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-166">The smallest sequence number from the queue.</span></span> |
| <span data-ttu-id="2f5b4-167">lastSequenceNumber</span><span class="sxs-lookup"><span data-stu-id="2f5b4-167">lastSequenceNumber</span></span> | <span data-ttu-id="2f5b4-168">integer</span><span class="sxs-lookup"><span data-stu-id="2f5b4-168">integer</span></span> | <span data-ttu-id="2f5b4-169">The last sequence number from the queue.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-169">The last sequence number from the queue.</span></span> |
| <span data-ttu-id="2f5b4-170">firstEnqueueTime</span><span class="sxs-lookup"><span data-stu-id="2f5b4-170">firstEnqueueTime</span></span> | <span data-ttu-id="2f5b4-171">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-171">string</span></span> | <span data-ttu-id="2f5b4-172">The first time from the queue.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-172">The first time from the queue.</span></span> |
| <span data-ttu-id="2f5b4-173">lastEnqueueTime</span><span class="sxs-lookup"><span data-stu-id="2f5b4-173">lastEnqueueTime</span></span> | <span data-ttu-id="2f5b4-174">string</span><span class="sxs-lookup"><span data-stu-id="2f5b4-174">string</span></span> | <span data-ttu-id="2f5b4-175">The last time from the queue.</span><span class="sxs-lookup"><span data-stu-id="2f5b4-175">The last time from the queue.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f5b4-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f5b4-176">Next steps</span></span>

* <span data-ttu-id="2f5b4-177">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="2f5b4-177">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="2f5b4-178">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b4-178">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
* <span data-ttu-id="2f5b4-179">For information about handling event hubs events, see [Stream big data into a data warehouse](event-grid-event-hubs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b4-179">For information about handling event hubs events, see [Stream big data into a data warehouse](event-grid-event-hubs-integration.md).</span></span>