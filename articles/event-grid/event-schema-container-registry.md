---
title: Azure Event Grid Container Registry event schema
description: Describes the properties that are provided for Container Reigstry events with Azure Event Grid
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 08/13/2018
ms.author: tomfitz
ms.openlocfilehash: d18a6718e4c29f3d04639644dc752b0733f15ba8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968882"
---
# <a name="azure-event-grid-event-schema-for-container-registry"></a><span data-ttu-id="5759c-103">Azure Event Grid event schema for Container Registry</span><span class="sxs-lookup"><span data-stu-id="5759c-103">Azure Event Grid event schema for Container Registry</span></span>

<span data-ttu-id="5759c-104">This article provides the properties and schema for Container Registry events.</span><span class="sxs-lookup"><span data-stu-id="5759c-104">This article provides the properties and schema for Container Registry events.</span></span> <span data-ttu-id="5759c-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5759c-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span></span>

## <a name="available-event-types"></a><span data-ttu-id="5759c-106">Available event types</span><span class="sxs-lookup"><span data-stu-id="5759c-106">Available event types</span></span>

<span data-ttu-id="5759c-107">Blob storage emits the following event types:</span><span class="sxs-lookup"><span data-stu-id="5759c-107">Blob storage emits the following event types:</span></span>

| <span data-ttu-id="5759c-108">Event type</span><span class="sxs-lookup"><span data-stu-id="5759c-108">Event type</span></span> | <span data-ttu-id="5759c-109">Description</span><span class="sxs-lookup"><span data-stu-id="5759c-109">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="5759c-110">Microsoft.ContainerRegistry.ImagePushed</span><span class="sxs-lookup"><span data-stu-id="5759c-110">Microsoft.ContainerRegistry.ImagePushed</span></span> | <span data-ttu-id="5759c-111">Raised when an image is pushed.</span><span class="sxs-lookup"><span data-stu-id="5759c-111">Raised when an image is pushed.</span></span> |
| <span data-ttu-id="5759c-112">Microsoft.ContainerRegistry.ImageDeleted</span><span class="sxs-lookup"><span data-stu-id="5759c-112">Microsoft.ContainerRegistry.ImageDeleted</span></span> | <span data-ttu-id="5759c-113">Raised when an image is deleted.</span><span class="sxs-lookup"><span data-stu-id="5759c-113">Raised when an image is deleted.</span></span> |

## <a name="example-event"></a><span data-ttu-id="5759c-114">Example event</span><span class="sxs-lookup"><span data-stu-id="5759c-114">Example event</span></span>

<span data-ttu-id="5759c-115">The following example shows the schema of an image pushed event:</span><span class="sxs-lookup"><span data-stu-id="5759c-115">The following example shows the schema of an image pushed event:</span></span> 

```json
[{
  "id": "831e1650-001e-001b-66ab-eeb76e069631",
  "topic": "/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.ContainerRegistry/registries/<name>",
  "subject": "aci-helloworld:v1",
  "eventType": "ImagePushed",
  "eventTime": "2018-04-25T21:39:47.6549614Z",
  "data": {
    "id": "31c51664-e5bd-416a-a5df-e5206bc47ed0",
    "timestamp": "2018-04-25T21:39:47.276585742Z",
    "action": "push",
    "target": {
      "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
      "size": 3023,
      "digest": "sha256:213bbc182920ab41e18edc2001e06abcca6735d87782d9cef68abd83941cf0e5",
      "length": 3023,
      "repository": "aci-helloworld",
      "tag": "v1"
    },
    "request": {
      "id": "7c66f28b-de19-40a4-821c-6f5f6c0003a4",
      "host": "demo.azurecr.io",
      "method": "PUT",
      "useragent": "docker/18.03.0-ce go/go1.9.4 git-commit/0520e24 os/windows arch/amd64 UpstreamClient(Docker-Client/18.03.0-ce \\\\(windows\\\\))"
    }
  },
  "dataVersion": "1.0",
  "metadataVersion": "1"
}]
```

<span data-ttu-id="5759c-116">The schema for an image deleted event is similar:</span><span class="sxs-lookup"><span data-stu-id="5759c-116">The schema for an image deleted event is similar:</span></span>

```json
[{
  "id": "f06e3921-301f-42ec-b368-212f7d5354bd",
  "topic": "/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.ContainerRegistry/registries/<name>",
  "subject": "aci-helloworld",
  "eventType": "ImageDeleted",
  "eventTime": "2018-04-26T17:56:01.8211268Z",
  "data": {
    "id": "f06e3921-301f-42ec-b368-212f7d5354bd",
    "timestamp": "2018-04-26T17:56:00.996603117Z",
    "action": "delete",
    "target": {
      "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
      "digest": "sha256:213bbc182920ab41e18edc2001e06abcca6735d87782d9cef68abd83941cf0e5",
      "repository": "aci-helloworld"
    },
    "request": {
      "id": "aeda5b99-4197-409f-b8a8-ff539edb7de2",
      "host": "demo.azurecr.io",
      "method": "DELETE",
      "useragent": "python-requests/2.18.4"
    }
  },
  "dataVersion": "1.0",
  "metadataVersion": "1"
}]
```

## <a name="event-properties"></a><span data-ttu-id="5759c-117">Event properties</span><span class="sxs-lookup"><span data-stu-id="5759c-117">Event properties</span></span>

<span data-ttu-id="5759c-118">An event has the following top-level data:</span><span class="sxs-lookup"><span data-stu-id="5759c-118">An event has the following top-level data:</span></span>

| <span data-ttu-id="5759c-119">Property</span><span class="sxs-lookup"><span data-stu-id="5759c-119">Property</span></span> | <span data-ttu-id="5759c-120">Type</span><span class="sxs-lookup"><span data-stu-id="5759c-120">Type</span></span> | <span data-ttu-id="5759c-121">Description</span><span class="sxs-lookup"><span data-stu-id="5759c-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="5759c-122">topic</span><span class="sxs-lookup"><span data-stu-id="5759c-122">topic</span></span> | <span data-ttu-id="5759c-123">string</span><span class="sxs-lookup"><span data-stu-id="5759c-123">string</span></span> | <span data-ttu-id="5759c-124">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="5759c-124">Full resource path to the event source.</span></span> <span data-ttu-id="5759c-125">This field is not writeable.</span><span class="sxs-lookup"><span data-stu-id="5759c-125">This field is not writeable.</span></span> <span data-ttu-id="5759c-126">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="5759c-126">Event Grid provides this value.</span></span> |
| <span data-ttu-id="5759c-127">subject</span><span class="sxs-lookup"><span data-stu-id="5759c-127">subject</span></span> | <span data-ttu-id="5759c-128">string</span><span class="sxs-lookup"><span data-stu-id="5759c-128">string</span></span> | <span data-ttu-id="5759c-129">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="5759c-129">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="5759c-130">eventType</span><span class="sxs-lookup"><span data-stu-id="5759c-130">eventType</span></span> | <span data-ttu-id="5759c-131">string</span><span class="sxs-lookup"><span data-stu-id="5759c-131">string</span></span> | <span data-ttu-id="5759c-132">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="5759c-132">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="5759c-133">eventTime</span><span class="sxs-lookup"><span data-stu-id="5759c-133">eventTime</span></span> | <span data-ttu-id="5759c-134">string</span><span class="sxs-lookup"><span data-stu-id="5759c-134">string</span></span> | <span data-ttu-id="5759c-135">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="5759c-135">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="5759c-136">id</span><span class="sxs-lookup"><span data-stu-id="5759c-136">id</span></span> | <span data-ttu-id="5759c-137">string</span><span class="sxs-lookup"><span data-stu-id="5759c-137">string</span></span> | <span data-ttu-id="5759c-138">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="5759c-138">Unique identifier for the event.</span></span> |
| <span data-ttu-id="5759c-139">data</span><span class="sxs-lookup"><span data-stu-id="5759c-139">data</span></span> | <span data-ttu-id="5759c-140">object</span><span class="sxs-lookup"><span data-stu-id="5759c-140">object</span></span> | <span data-ttu-id="5759c-141">Blob storage event data.</span><span class="sxs-lookup"><span data-stu-id="5759c-141">Blob storage event data.</span></span> |
| <span data-ttu-id="5759c-142">dataVersion</span><span class="sxs-lookup"><span data-stu-id="5759c-142">dataVersion</span></span> | <span data-ttu-id="5759c-143">string</span><span class="sxs-lookup"><span data-stu-id="5759c-143">string</span></span> | <span data-ttu-id="5759c-144">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="5759c-144">The schema version of the data object.</span></span> <span data-ttu-id="5759c-145">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="5759c-145">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="5759c-146">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="5759c-146">metadataVersion</span></span> | <span data-ttu-id="5759c-147">string</span><span class="sxs-lookup"><span data-stu-id="5759c-147">string</span></span> | <span data-ttu-id="5759c-148">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="5759c-148">The schema version of the event metadata.</span></span> <span data-ttu-id="5759c-149">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="5759c-149">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="5759c-150">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="5759c-150">Event Grid provides this value.</span></span> |

<span data-ttu-id="5759c-151">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="5759c-151">The data object has the following properties:</span></span>

| <span data-ttu-id="5759c-152">Property</span><span class="sxs-lookup"><span data-stu-id="5759c-152">Property</span></span> | <span data-ttu-id="5759c-153">Type</span><span class="sxs-lookup"><span data-stu-id="5759c-153">Type</span></span> | <span data-ttu-id="5759c-154">Description</span><span class="sxs-lookup"><span data-stu-id="5759c-154">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="5759c-155">id</span><span class="sxs-lookup"><span data-stu-id="5759c-155">id</span></span> | <span data-ttu-id="5759c-156">string</span><span class="sxs-lookup"><span data-stu-id="5759c-156">string</span></span> | <span data-ttu-id="5759c-157">The event ID.</span><span class="sxs-lookup"><span data-stu-id="5759c-157">The event ID.</span></span> |
| <span data-ttu-id="5759c-158">timestamp</span><span class="sxs-lookup"><span data-stu-id="5759c-158">timestamp</span></span> | <span data-ttu-id="5759c-159">string</span><span class="sxs-lookup"><span data-stu-id="5759c-159">string</span></span> | <span data-ttu-id="5759c-160">The time at which the event occurred.</span><span class="sxs-lookup"><span data-stu-id="5759c-160">The time at which the event occurred.</span></span> |
| <span data-ttu-id="5759c-161">action</span><span class="sxs-lookup"><span data-stu-id="5759c-161">action</span></span> | <span data-ttu-id="5759c-162">string</span><span class="sxs-lookup"><span data-stu-id="5759c-162">string</span></span> | <span data-ttu-id="5759c-163">The action that encompasses the provided event.</span><span class="sxs-lookup"><span data-stu-id="5759c-163">The action that encompasses the provided event.</span></span> |
| <span data-ttu-id="5759c-164">target</span><span class="sxs-lookup"><span data-stu-id="5759c-164">target</span></span> | <span data-ttu-id="5759c-165">object</span><span class="sxs-lookup"><span data-stu-id="5759c-165">object</span></span> | <span data-ttu-id="5759c-166">The target of the event.</span><span class="sxs-lookup"><span data-stu-id="5759c-166">The target of the event.</span></span> |
| <span data-ttu-id="5759c-167">request</span><span class="sxs-lookup"><span data-stu-id="5759c-167">request</span></span> | <span data-ttu-id="5759c-168">object</span><span class="sxs-lookup"><span data-stu-id="5759c-168">object</span></span> | <span data-ttu-id="5759c-169">The request that generated the event.</span><span class="sxs-lookup"><span data-stu-id="5759c-169">The request that generated the event.</span></span> |

<span data-ttu-id="5759c-170">The target object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="5759c-170">The target object has the following properties:</span></span>

| <span data-ttu-id="5759c-171">Property</span><span class="sxs-lookup"><span data-stu-id="5759c-171">Property</span></span> | <span data-ttu-id="5759c-172">Type</span><span class="sxs-lookup"><span data-stu-id="5759c-172">Type</span></span> | <span data-ttu-id="5759c-173">Description</span><span class="sxs-lookup"><span data-stu-id="5759c-173">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="5759c-174">mediaType</span><span class="sxs-lookup"><span data-stu-id="5759c-174">mediaType</span></span> | <span data-ttu-id="5759c-175">string</span><span class="sxs-lookup"><span data-stu-id="5759c-175">string</span></span> | <span data-ttu-id="5759c-176">The MIME type of the referenced object.</span><span class="sxs-lookup"><span data-stu-id="5759c-176">The MIME type of the referenced object.</span></span> |
| <span data-ttu-id="5759c-177">size</span><span class="sxs-lookup"><span data-stu-id="5759c-177">size</span></span> | <span data-ttu-id="5759c-178">integer</span><span class="sxs-lookup"><span data-stu-id="5759c-178">integer</span></span> | <span data-ttu-id="5759c-179">The number of bytes of the content.</span><span class="sxs-lookup"><span data-stu-id="5759c-179">The number of bytes of the content.</span></span> <span data-ttu-id="5759c-180">Same as Length field.</span><span class="sxs-lookup"><span data-stu-id="5759c-180">Same as Length field.</span></span> |
| <span data-ttu-id="5759c-181">digest</span><span class="sxs-lookup"><span data-stu-id="5759c-181">digest</span></span> | <span data-ttu-id="5759c-182">string</span><span class="sxs-lookup"><span data-stu-id="5759c-182">string</span></span> | <span data-ttu-id="5759c-183">The digest of the content, as defined by the Registry V2 HTTP API Specification.</span><span class="sxs-lookup"><span data-stu-id="5759c-183">The digest of the content, as defined by the Registry V2 HTTP API Specification.</span></span> |
| <span data-ttu-id="5759c-184">length</span><span class="sxs-lookup"><span data-stu-id="5759c-184">length</span></span> | <span data-ttu-id="5759c-185">integer</span><span class="sxs-lookup"><span data-stu-id="5759c-185">integer</span></span> | <span data-ttu-id="5759c-186">The number of bytes of the content.</span><span class="sxs-lookup"><span data-stu-id="5759c-186">The number of bytes of the content.</span></span> <span data-ttu-id="5759c-187">Same as Size field.</span><span class="sxs-lookup"><span data-stu-id="5759c-187">Same as Size field.</span></span> |
| <span data-ttu-id="5759c-188">repository</span><span class="sxs-lookup"><span data-stu-id="5759c-188">repository</span></span> | <span data-ttu-id="5759c-189">string</span><span class="sxs-lookup"><span data-stu-id="5759c-189">string</span></span> | <span data-ttu-id="5759c-190">The repository name.</span><span class="sxs-lookup"><span data-stu-id="5759c-190">The repository name.</span></span> |
| <span data-ttu-id="5759c-191">tag</span><span class="sxs-lookup"><span data-stu-id="5759c-191">tag</span></span> | <span data-ttu-id="5759c-192">string</span><span class="sxs-lookup"><span data-stu-id="5759c-192">string</span></span> | <span data-ttu-id="5759c-193">The tag name.</span><span class="sxs-lookup"><span data-stu-id="5759c-193">The tag name.</span></span> |

<span data-ttu-id="5759c-194">The request object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="5759c-194">The request object has the following properties:</span></span>

| <span data-ttu-id="5759c-195">Property</span><span class="sxs-lookup"><span data-stu-id="5759c-195">Property</span></span> | <span data-ttu-id="5759c-196">Type</span><span class="sxs-lookup"><span data-stu-id="5759c-196">Type</span></span> | <span data-ttu-id="5759c-197">Description</span><span class="sxs-lookup"><span data-stu-id="5759c-197">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="5759c-198">id</span><span class="sxs-lookup"><span data-stu-id="5759c-198">id</span></span> | <span data-ttu-id="5759c-199">string</span><span class="sxs-lookup"><span data-stu-id="5759c-199">string</span></span> | <span data-ttu-id="5759c-200">The ID of the request that initiated the event.</span><span class="sxs-lookup"><span data-stu-id="5759c-200">The ID of the request that initiated the event.</span></span> |
| <span data-ttu-id="5759c-201">addr</span><span class="sxs-lookup"><span data-stu-id="5759c-201">addr</span></span> | <span data-ttu-id="5759c-202">string</span><span class="sxs-lookup"><span data-stu-id="5759c-202">string</span></span> | <span data-ttu-id="5759c-203">The IP or hostname and possibly port of the client connection that initiated the event.</span><span class="sxs-lookup"><span data-stu-id="5759c-203">The IP or hostname and possibly port of the client connection that initiated the event.</span></span> <span data-ttu-id="5759c-204">This value is the RemoteAddr from the standard http request.</span><span class="sxs-lookup"><span data-stu-id="5759c-204">This value is the RemoteAddr from the standard http request.</span></span> |
| <span data-ttu-id="5759c-205">host</span><span class="sxs-lookup"><span data-stu-id="5759c-205">host</span></span> | <span data-ttu-id="5759c-206">string</span><span class="sxs-lookup"><span data-stu-id="5759c-206">string</span></span> | <span data-ttu-id="5759c-207">The externally accessible hostname of the registry instance, as specified by the http host header on incoming requests.</span><span class="sxs-lookup"><span data-stu-id="5759c-207">The externally accessible hostname of the registry instance, as specified by the http host header on incoming requests.</span></span> |
| <span data-ttu-id="5759c-208">method</span><span class="sxs-lookup"><span data-stu-id="5759c-208">method</span></span> | <span data-ttu-id="5759c-209">string</span><span class="sxs-lookup"><span data-stu-id="5759c-209">string</span></span> | <span data-ttu-id="5759c-210">The request method that generated the event.</span><span class="sxs-lookup"><span data-stu-id="5759c-210">The request method that generated the event.</span></span> |
| <span data-ttu-id="5759c-211">useragent</span><span class="sxs-lookup"><span data-stu-id="5759c-211">useragent</span></span> | <span data-ttu-id="5759c-212">string</span><span class="sxs-lookup"><span data-stu-id="5759c-212">string</span></span> | <span data-ttu-id="5759c-213">The user agent header of the request.</span><span class="sxs-lookup"><span data-stu-id="5759c-213">The user agent header of the request.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5759c-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="5759c-214">Next steps</span></span>

* <span data-ttu-id="5759c-215">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="5759c-215">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="5759c-216">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5759c-216">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
