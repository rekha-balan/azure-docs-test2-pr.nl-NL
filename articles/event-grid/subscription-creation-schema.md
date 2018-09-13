---
title: Azure Event Grid subscription schema
description: Describes the properties for subscribing to an event with Azure Event Grid.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 05/02/2018
ms.author: babanisa
ms.openlocfilehash: cfb4dabea12f2988108d24b025e324cf05afb325
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856816"
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="90d28-103">Event Grid subscription schema</span><span class="sxs-lookup"><span data-stu-id="90d28-103">Event Grid subscription schema</span></span>

<span data-ttu-id="90d28-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span><span class="sxs-lookup"><span data-stu-id="90d28-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="90d28-105">Use the following format:</span><span class="sxs-lookup"><span data-stu-id="90d28-105">Use the following format:</span></span>

```HTTP
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2018-01-01
``` 

<span data-ttu-id="90d28-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span><span class="sxs-lookup"><span data-stu-id="90d28-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```HTTP
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2018-01-01
``` 

<span data-ttu-id="90d28-107">The article describes the properties and schema for the body of the request.</span><span class="sxs-lookup"><span data-stu-id="90d28-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="90d28-108">Event subscription properties</span><span class="sxs-lookup"><span data-stu-id="90d28-108">Event subscription properties</span></span>

| <span data-ttu-id="90d28-109">Property</span><span class="sxs-lookup"><span data-stu-id="90d28-109">Property</span></span> | <span data-ttu-id="90d28-110">Type</span><span class="sxs-lookup"><span data-stu-id="90d28-110">Type</span></span> | <span data-ttu-id="90d28-111">Description</span><span class="sxs-lookup"><span data-stu-id="90d28-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="90d28-112">destination</span><span class="sxs-lookup"><span data-stu-id="90d28-112">destination</span></span> | <span data-ttu-id="90d28-113">object</span><span class="sxs-lookup"><span data-stu-id="90d28-113">object</span></span> | <span data-ttu-id="90d28-114">The object that defines the endpoint.</span><span class="sxs-lookup"><span data-stu-id="90d28-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="90d28-115">filter</span><span class="sxs-lookup"><span data-stu-id="90d28-115">filter</span></span> | <span data-ttu-id="90d28-116">object</span><span class="sxs-lookup"><span data-stu-id="90d28-116">object</span></span> | <span data-ttu-id="90d28-117">An optional field for filtering the types of events.</span><span class="sxs-lookup"><span data-stu-id="90d28-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="90d28-118">destination object</span><span class="sxs-lookup"><span data-stu-id="90d28-118">destination object</span></span>

| <span data-ttu-id="90d28-119">Property</span><span class="sxs-lookup"><span data-stu-id="90d28-119">Property</span></span> | <span data-ttu-id="90d28-120">Type</span><span class="sxs-lookup"><span data-stu-id="90d28-120">Type</span></span> | <span data-ttu-id="90d28-121">Description</span><span class="sxs-lookup"><span data-stu-id="90d28-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="90d28-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="90d28-122">endpointType</span></span> | <span data-ttu-id="90d28-123">string</span><span class="sxs-lookup"><span data-stu-id="90d28-123">string</span></span> | <span data-ttu-id="90d28-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span><span class="sxs-lookup"><span data-stu-id="90d28-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="90d28-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="90d28-125">endpointUrl</span></span> | <span data-ttu-id="90d28-126">string</span><span class="sxs-lookup"><span data-stu-id="90d28-126">string</span></span> | <span data-ttu-id="90d28-127">The destination URL for events in this event subscription.</span><span class="sxs-lookup"><span data-stu-id="90d28-127">The destination URL for events in this event subscription.</span></span> | 

### <a name="filter-object"></a><span data-ttu-id="90d28-128">filter object</span><span class="sxs-lookup"><span data-stu-id="90d28-128">filter object</span></span>

| <span data-ttu-id="90d28-129">Property</span><span class="sxs-lookup"><span data-stu-id="90d28-129">Property</span></span> | <span data-ttu-id="90d28-130">Type</span><span class="sxs-lookup"><span data-stu-id="90d28-130">Type</span></span> | <span data-ttu-id="90d28-131">Description</span><span class="sxs-lookup"><span data-stu-id="90d28-131">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="90d28-132">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="90d28-132">includedEventTypes</span></span> | <span data-ttu-id="90d28-133">array</span><span class="sxs-lookup"><span data-stu-id="90d28-133">array</span></span> | <span data-ttu-id="90d28-134">Match when the event type in the event message is an exact match to one of these event type names.</span><span class="sxs-lookup"><span data-stu-id="90d28-134">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="90d28-135">Raises an error when event name does not match the registered event type names for the event source.</span><span class="sxs-lookup"><span data-stu-id="90d28-135">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="90d28-136">Default matches all event types.</span><span class="sxs-lookup"><span data-stu-id="90d28-136">Default matches all event types.</span></span> |
| <span data-ttu-id="90d28-137">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="90d28-137">subjectBeginsWith</span></span> | <span data-ttu-id="90d28-138">string</span><span class="sxs-lookup"><span data-stu-id="90d28-138">string</span></span> | <span data-ttu-id="90d28-139">A prefix-match filter to the subject field in the event message.</span><span class="sxs-lookup"><span data-stu-id="90d28-139">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="90d28-140">The default or empty string matches all.</span><span class="sxs-lookup"><span data-stu-id="90d28-140">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="90d28-141">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="90d28-141">subjectEndsWith</span></span> | <span data-ttu-id="90d28-142">string</span><span class="sxs-lookup"><span data-stu-id="90d28-142">string</span></span> | <span data-ttu-id="90d28-143">A suffix-match filter to the subject field in the event message.</span><span class="sxs-lookup"><span data-stu-id="90d28-143">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="90d28-144">The default or empty string matches all.</span><span class="sxs-lookup"><span data-stu-id="90d28-144">The default or empty string matches all.</span></span> |
| <span data-ttu-id="90d28-145">isSubjectCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="90d28-145">isSubjectCaseSensitive</span></span> | <span data-ttu-id="90d28-146">string</span><span class="sxs-lookup"><span data-stu-id="90d28-146">string</span></span> | <span data-ttu-id="90d28-147">Controls case-sensitive matching for filters.</span><span class="sxs-lookup"><span data-stu-id="90d28-147">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="90d28-148">Example subscription schema</span><span class="sxs-lookup"><span data-stu-id="90d28-148">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "Microsoft.Storage.BlobCreated", "Microsoft.Storage.BlobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "isSubjectCaseSensitive ": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="90d28-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="90d28-149">Next steps</span></span>

* <span data-ttu-id="90d28-150">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="90d28-150">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>