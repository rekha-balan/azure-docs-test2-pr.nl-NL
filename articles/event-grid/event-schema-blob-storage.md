---
title: Azure Event Grid blob storage event schema
description: Describes the properties that are provided for blob storage events with Azure Event Grid
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: reference
ms.date: 08/17/2018
ms.author: tomfitz
ms.openlocfilehash: 11524f8868a0102e30b06f3385a26b1bd06aae6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870005"
---
# <a name="azure-event-grid-event-schema-for-blob-storage"></a><span data-ttu-id="04485-103">Azure Event Grid event schema for Blob storage</span><span class="sxs-lookup"><span data-stu-id="04485-103">Azure Event Grid event schema for Blob storage</span></span>

<span data-ttu-id="04485-104">This article provides the properties and schema for blob storage events.</span><span class="sxs-lookup"><span data-stu-id="04485-104">This article provides the properties and schema for blob storage events.</span></span> <span data-ttu-id="04485-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="04485-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span></span>

<span data-ttu-id="04485-106">For a list of sample scripts and tutorials, see [Storage event source](event-sources.md#storage).</span><span class="sxs-lookup"><span data-stu-id="04485-106">For a list of sample scripts and tutorials, see [Storage event source](event-sources.md#storage).</span></span>

## <a name="available-event-types"></a><span data-ttu-id="04485-107">Available event types</span><span class="sxs-lookup"><span data-stu-id="04485-107">Available event types</span></span>

<span data-ttu-id="04485-108">Blob storage emits the following event types:</span><span class="sxs-lookup"><span data-stu-id="04485-108">Blob storage emits the following event types:</span></span>

| <span data-ttu-id="04485-109">Event type</span><span class="sxs-lookup"><span data-stu-id="04485-109">Event type</span></span> | <span data-ttu-id="04485-110">Description</span><span class="sxs-lookup"><span data-stu-id="04485-110">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="04485-111">Microsoft.Storage.BlobCreated</span><span class="sxs-lookup"><span data-stu-id="04485-111">Microsoft.Storage.BlobCreated</span></span> | <span data-ttu-id="04485-112">Raised when a blob is created.</span><span class="sxs-lookup"><span data-stu-id="04485-112">Raised when a blob is created.</span></span> |
| <span data-ttu-id="04485-113">Microsoft.Storage.BlobDeleted</span><span class="sxs-lookup"><span data-stu-id="04485-113">Microsoft.Storage.BlobDeleted</span></span> | <span data-ttu-id="04485-114">Raised when a blob is deleted.</span><span class="sxs-lookup"><span data-stu-id="04485-114">Raised when a blob is deleted.</span></span> |

## <a name="example-event"></a><span data-ttu-id="04485-115">Example event</span><span class="sxs-lookup"><span data-stu-id="04485-115">Example event</span></span>

<span data-ttu-id="04485-116">The following example shows the schema of a blob created event:</span><span class="sxs-lookup"><span data-stu-id="04485-116">The following example shows the schema of a blob created event:</span></span> 

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobCreated",
  "eventTime": "2017-06-26T18:41:00.9584103Z",
  "id": "831e1650-001e-001b-66ab-eeb76e069631",
  "data": {
    "api": "PutBlockList",
    "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
    "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
    "eTag": "0x8D4BCC2E4835CD0",
    "contentType": "text/plain",
    "contentLength": 524288,
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "00000000000004420000000000028963",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  },
  "dataVersion": "",
  "metadataVersion": "1"
}]
```

<span data-ttu-id="04485-117">The schema for a blob deleted event is similar:</span><span class="sxs-lookup"><span data-stu-id="04485-117">The schema for a blob deleted event is similar:</span></span> 

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobDeleted",
  "eventTime": "2017-11-07T20:09:22.5674003Z",
  "id": "4c2359fe-001e-00ba-0e04-58586806d298",
  "data": {
    "api": "DeleteBlob",
    "requestId": "4c2359fe-001e-00ba-0e04-585868000000",
    "contentType": "text/plain",
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "0000000000000281000000000002F5CA",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  },
  "dataVersion": "",
  "metadataVersion": "1"
}]
```
 
## <a name="event-properties"></a><span data-ttu-id="04485-118">Event properties</span><span class="sxs-lookup"><span data-stu-id="04485-118">Event properties</span></span>

<span data-ttu-id="04485-119">An event has the following top-level data:</span><span class="sxs-lookup"><span data-stu-id="04485-119">An event has the following top-level data:</span></span>

| <span data-ttu-id="04485-120">Property</span><span class="sxs-lookup"><span data-stu-id="04485-120">Property</span></span> | <span data-ttu-id="04485-121">Type</span><span class="sxs-lookup"><span data-stu-id="04485-121">Type</span></span> | <span data-ttu-id="04485-122">Description</span><span class="sxs-lookup"><span data-stu-id="04485-122">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="04485-123">topic</span><span class="sxs-lookup"><span data-stu-id="04485-123">topic</span></span> | <span data-ttu-id="04485-124">string</span><span class="sxs-lookup"><span data-stu-id="04485-124">string</span></span> | <span data-ttu-id="04485-125">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="04485-125">Full resource path to the event source.</span></span> <span data-ttu-id="04485-126">This field is not writeable.</span><span class="sxs-lookup"><span data-stu-id="04485-126">This field is not writeable.</span></span> <span data-ttu-id="04485-127">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="04485-127">Event Grid provides this value.</span></span> |
| <span data-ttu-id="04485-128">subject</span><span class="sxs-lookup"><span data-stu-id="04485-128">subject</span></span> | <span data-ttu-id="04485-129">string</span><span class="sxs-lookup"><span data-stu-id="04485-129">string</span></span> | <span data-ttu-id="04485-130">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="04485-130">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="04485-131">eventType</span><span class="sxs-lookup"><span data-stu-id="04485-131">eventType</span></span> | <span data-ttu-id="04485-132">string</span><span class="sxs-lookup"><span data-stu-id="04485-132">string</span></span> | <span data-ttu-id="04485-133">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="04485-133">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="04485-134">eventTime</span><span class="sxs-lookup"><span data-stu-id="04485-134">eventTime</span></span> | <span data-ttu-id="04485-135">string</span><span class="sxs-lookup"><span data-stu-id="04485-135">string</span></span> | <span data-ttu-id="04485-136">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="04485-136">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="04485-137">id</span><span class="sxs-lookup"><span data-stu-id="04485-137">id</span></span> | <span data-ttu-id="04485-138">string</span><span class="sxs-lookup"><span data-stu-id="04485-138">string</span></span> | <span data-ttu-id="04485-139">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="04485-139">Unique identifier for the event.</span></span> |
| <span data-ttu-id="04485-140">data</span><span class="sxs-lookup"><span data-stu-id="04485-140">data</span></span> | <span data-ttu-id="04485-141">object</span><span class="sxs-lookup"><span data-stu-id="04485-141">object</span></span> | <span data-ttu-id="04485-142">Blob storage event data.</span><span class="sxs-lookup"><span data-stu-id="04485-142">Blob storage event data.</span></span> |
| <span data-ttu-id="04485-143">dataVersion</span><span class="sxs-lookup"><span data-stu-id="04485-143">dataVersion</span></span> | <span data-ttu-id="04485-144">string</span><span class="sxs-lookup"><span data-stu-id="04485-144">string</span></span> | <span data-ttu-id="04485-145">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="04485-145">The schema version of the data object.</span></span> <span data-ttu-id="04485-146">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="04485-146">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="04485-147">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="04485-147">metadataVersion</span></span> | <span data-ttu-id="04485-148">string</span><span class="sxs-lookup"><span data-stu-id="04485-148">string</span></span> | <span data-ttu-id="04485-149">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="04485-149">The schema version of the event metadata.</span></span> <span data-ttu-id="04485-150">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="04485-150">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="04485-151">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="04485-151">Event Grid provides this value.</span></span> |

<span data-ttu-id="04485-152">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="04485-152">The data object has the following properties:</span></span>

| <span data-ttu-id="04485-153">Property</span><span class="sxs-lookup"><span data-stu-id="04485-153">Property</span></span> | <span data-ttu-id="04485-154">Type</span><span class="sxs-lookup"><span data-stu-id="04485-154">Type</span></span> | <span data-ttu-id="04485-155">Description</span><span class="sxs-lookup"><span data-stu-id="04485-155">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="04485-156">api</span><span class="sxs-lookup"><span data-stu-id="04485-156">api</span></span> | <span data-ttu-id="04485-157">string</span><span class="sxs-lookup"><span data-stu-id="04485-157">string</span></span> | <span data-ttu-id="04485-158">The operation that triggered the event.</span><span class="sxs-lookup"><span data-stu-id="04485-158">The operation that triggered the event.</span></span> |
| <span data-ttu-id="04485-159">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="04485-159">clientRequestId</span></span> | <span data-ttu-id="04485-160">string</span><span class="sxs-lookup"><span data-stu-id="04485-160">string</span></span> | <span data-ttu-id="04485-161">A client-generated, opaque value with a 1-KB character limit.</span><span class="sxs-lookup"><span data-stu-id="04485-161">A client-generated, opaque value with a 1-KB character limit.</span></span> <span data-ttu-id="04485-162">When you have enabled storage analytics logging, it is recorded in the analytics logs.</span><span class="sxs-lookup"><span data-stu-id="04485-162">When you have enabled storage analytics logging, it is recorded in the analytics logs.</span></span> |
| <span data-ttu-id="04485-163">requestId</span><span class="sxs-lookup"><span data-stu-id="04485-163">requestId</span></span> | <span data-ttu-id="04485-164">string</span><span class="sxs-lookup"><span data-stu-id="04485-164">string</span></span> | <span data-ttu-id="04485-165">The unique identifier for the request.</span><span class="sxs-lookup"><span data-stu-id="04485-165">The unique identifier for the request.</span></span> <span data-ttu-id="04485-166">Use it for troubleshooting the request.</span><span class="sxs-lookup"><span data-stu-id="04485-166">Use it for troubleshooting the request.</span></span> |
| <span data-ttu-id="04485-167">eTag</span><span class="sxs-lookup"><span data-stu-id="04485-167">eTag</span></span> | <span data-ttu-id="04485-168">string</span><span class="sxs-lookup"><span data-stu-id="04485-168">string</span></span> | <span data-ttu-id="04485-169">The value that you can use to perform operations conditionally.</span><span class="sxs-lookup"><span data-stu-id="04485-169">The value that you can use to perform operations conditionally.</span></span> |
| <span data-ttu-id="04485-170">contentType</span><span class="sxs-lookup"><span data-stu-id="04485-170">contentType</span></span> | <span data-ttu-id="04485-171">string</span><span class="sxs-lookup"><span data-stu-id="04485-171">string</span></span> | <span data-ttu-id="04485-172">The content type specified for the blob.</span><span class="sxs-lookup"><span data-stu-id="04485-172">The content type specified for the blob.</span></span> |
| <span data-ttu-id="04485-173">contentLength</span><span class="sxs-lookup"><span data-stu-id="04485-173">contentLength</span></span> | <span data-ttu-id="04485-174">integer</span><span class="sxs-lookup"><span data-stu-id="04485-174">integer</span></span> | <span data-ttu-id="04485-175">The size of the blob in bytes.</span><span class="sxs-lookup"><span data-stu-id="04485-175">The size of the blob in bytes.</span></span> |
| <span data-ttu-id="04485-176">blobType</span><span class="sxs-lookup"><span data-stu-id="04485-176">blobType</span></span> | <span data-ttu-id="04485-177">string</span><span class="sxs-lookup"><span data-stu-id="04485-177">string</span></span> | <span data-ttu-id="04485-178">The type of blob.</span><span class="sxs-lookup"><span data-stu-id="04485-178">The type of blob.</span></span> <span data-ttu-id="04485-179">Valid values are either "BlockBlob" or "PageBlob".</span><span class="sxs-lookup"><span data-stu-id="04485-179">Valid values are either "BlockBlob" or "PageBlob".</span></span> |
| <span data-ttu-id="04485-180">url</span><span class="sxs-lookup"><span data-stu-id="04485-180">url</span></span> | <span data-ttu-id="04485-181">string</span><span class="sxs-lookup"><span data-stu-id="04485-181">string</span></span> | <span data-ttu-id="04485-182">The path to the blob.</span><span class="sxs-lookup"><span data-stu-id="04485-182">The path to the blob.</span></span> |
| <span data-ttu-id="04485-183">sequencer</span><span class="sxs-lookup"><span data-stu-id="04485-183">sequencer</span></span> | <span data-ttu-id="04485-184">string</span><span class="sxs-lookup"><span data-stu-id="04485-184">string</span></span> | <span data-ttu-id="04485-185">A user-controlled value that you can use to track requests.</span><span class="sxs-lookup"><span data-stu-id="04485-185">A user-controlled value that you can use to track requests.</span></span> |
| <span data-ttu-id="04485-186">storageDiagnostics</span><span class="sxs-lookup"><span data-stu-id="04485-186">storageDiagnostics</span></span> | <span data-ttu-id="04485-187">object</span><span class="sxs-lookup"><span data-stu-id="04485-187">object</span></span> | <span data-ttu-id="04485-188">Information about the storage diagnostics.</span><span class="sxs-lookup"><span data-stu-id="04485-188">Information about the storage diagnostics.</span></span> |
 
## <a name="next-steps"></a><span data-ttu-id="04485-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="04485-189">Next steps</span></span>

* <span data-ttu-id="04485-190">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="04485-190">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="04485-191">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="04485-191">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
* <span data-ttu-id="04485-192">For an introduction to working with blob storage events, see [Route Blob storage events - Azure CLI](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04485-192">For an introduction to working with blob storage events, see [Route Blob storage events - Azure CLI](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json).</span></span> 
