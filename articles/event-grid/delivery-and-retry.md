---
title: Azure Event Grid delivery and retry
description: Describes how Azure Event Grid delivers events and how it handles undelivered messages.
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: conceptual
ms.date: 09/05/2018
ms.author: tomfitz
ms.openlocfilehash: 2a9ff23e5182c8cb7c91ad93e368f61f258c84f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865492"
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="0c560-103">Event Grid message delivery and retry</span><span class="sxs-lookup"><span data-stu-id="0c560-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="0c560-104">This article describes how Azure Event Grid handles events when delivery isn't acknowledged.</span><span class="sxs-lookup"><span data-stu-id="0c560-104">This article describes how Azure Event Grid handles events when delivery isn't acknowledged.</span></span>

<span data-ttu-id="0c560-105">Event Grid provides durable delivery.</span><span class="sxs-lookup"><span data-stu-id="0c560-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="0c560-106">It delivers each message at least once for each subscription.</span><span class="sxs-lookup"><span data-stu-id="0c560-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="0c560-107">Events are sent to the registered webhook of each subscription immediately.</span><span class="sxs-lookup"><span data-stu-id="0c560-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="0c560-108">If a webhook doesn't acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span><span class="sxs-lookup"><span data-stu-id="0c560-108">If a webhook doesn't acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span> 

<span data-ttu-id="0c560-109">Currently, Event Grid sends each event individually to subscribers.</span><span class="sxs-lookup"><span data-stu-id="0c560-109">Currently, Event Grid sends each event individually to subscribers.</span></span> <span data-ttu-id="0c560-110">The subscriber receives an array with a single event.</span><span class="sxs-lookup"><span data-stu-id="0c560-110">The subscriber receives an array with a single event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="0c560-111">Message delivery status</span><span class="sxs-lookup"><span data-stu-id="0c560-111">Message delivery status</span></span>

<span data-ttu-id="0c560-112">Event Grid uses HTTP response codes to acknowledge receipt of events.</span><span class="sxs-lookup"><span data-stu-id="0c560-112">Event Grid uses HTTP response codes to acknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="0c560-113">Success codes</span><span class="sxs-lookup"><span data-stu-id="0c560-113">Success codes</span></span>

<span data-ttu-id="0c560-114">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span><span class="sxs-lookup"><span data-stu-id="0c560-114">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span></span> <span data-ttu-id="0c560-115">Event Grid considers delivery complete.</span><span class="sxs-lookup"><span data-stu-id="0c560-115">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="0c560-116">200 OK</span><span class="sxs-lookup"><span data-stu-id="0c560-116">200 OK</span></span>
- <span data-ttu-id="0c560-117">202 Accepted</span><span class="sxs-lookup"><span data-stu-id="0c560-117">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="0c560-118">Failure codes</span><span class="sxs-lookup"><span data-stu-id="0c560-118">Failure codes</span></span>

<span data-ttu-id="0c560-119">The following HTTP response codes indicate that an event delivery attempt failed.</span><span class="sxs-lookup"><span data-stu-id="0c560-119">The following HTTP response codes indicate that an event delivery attempt failed.</span></span>

- <span data-ttu-id="0c560-120">400 Bad Request</span><span class="sxs-lookup"><span data-stu-id="0c560-120">400 Bad Request</span></span>
- <span data-ttu-id="0c560-121">401 Unauthorized</span><span class="sxs-lookup"><span data-stu-id="0c560-121">401 Unauthorized</span></span>
- <span data-ttu-id="0c560-122">404 Not Found</span><span class="sxs-lookup"><span data-stu-id="0c560-122">404 Not Found</span></span>
- <span data-ttu-id="0c560-123">408 Request timeout</span><span class="sxs-lookup"><span data-stu-id="0c560-123">408 Request timeout</span></span>
- <span data-ttu-id="0c560-124">413 Request Entity Too Large</span><span class="sxs-lookup"><span data-stu-id="0c560-124">413 Request Entity Too Large</span></span>
- <span data-ttu-id="0c560-125">414 URI Too Long</span><span class="sxs-lookup"><span data-stu-id="0c560-125">414 URI Too Long</span></span>
- <span data-ttu-id="0c560-126">429 Too Many Requests</span><span class="sxs-lookup"><span data-stu-id="0c560-126">429 Too Many Requests</span></span>
- <span data-ttu-id="0c560-127">500 Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="0c560-127">500 Internal Server Error</span></span>
- <span data-ttu-id="0c560-128">503 Service Unavailable</span><span class="sxs-lookup"><span data-stu-id="0c560-128">503 Service Unavailable</span></span>
- <span data-ttu-id="0c560-129">504 Gateway Timeout</span><span class="sxs-lookup"><span data-stu-id="0c560-129">504 Gateway Timeout</span></span>

<span data-ttu-id="0c560-130">If you have [configured a dead-letter endpoint](manage-event-delivery.md) and Event Grid receives either a 400 or 413 response code, Event Grid immediately sends the event to the dead-letter endpoint.</span><span class="sxs-lookup"><span data-stu-id="0c560-130">If you have [configured a dead-letter endpoint](manage-event-delivery.md) and Event Grid receives either a 400 or 413 response code, Event Grid immediately sends the event to the dead-letter endpoint.</span></span> <span data-ttu-id="0c560-131">Otherwise, Event Grid retries all errors.</span><span class="sxs-lookup"><span data-stu-id="0c560-131">Otherwise, Event Grid retries all errors.</span></span>

## <a name="retry-intervals-and-duration"></a><span data-ttu-id="0c560-132">Retry intervals and duration</span><span class="sxs-lookup"><span data-stu-id="0c560-132">Retry intervals and duration</span></span>

<span data-ttu-id="0c560-133">Event Grid uses an exponential backoff retry policy for event delivery.</span><span class="sxs-lookup"><span data-stu-id="0c560-133">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="0c560-134">If your webhook doesn't respond or returns a failure code, Event Grid retries delivery on the following schedule:</span><span class="sxs-lookup"><span data-stu-id="0c560-134">If your webhook doesn't respond or returns a failure code, Event Grid retries delivery on the following schedule:</span></span>

1. <span data-ttu-id="0c560-135">10 seconds</span><span class="sxs-lookup"><span data-stu-id="0c560-135">10 seconds</span></span>
2. <span data-ttu-id="0c560-136">30 seconds</span><span class="sxs-lookup"><span data-stu-id="0c560-136">30 seconds</span></span>
3. <span data-ttu-id="0c560-137">1 minute</span><span class="sxs-lookup"><span data-stu-id="0c560-137">1 minute</span></span>
4. <span data-ttu-id="0c560-138">5 minutes</span><span class="sxs-lookup"><span data-stu-id="0c560-138">5 minutes</span></span>
5. <span data-ttu-id="0c560-139">10 minutes</span><span class="sxs-lookup"><span data-stu-id="0c560-139">10 minutes</span></span>
6. <span data-ttu-id="0c560-140">30 minutes</span><span class="sxs-lookup"><span data-stu-id="0c560-140">30 minutes</span></span>
7. <span data-ttu-id="0c560-141">1 hour</span><span class="sxs-lookup"><span data-stu-id="0c560-141">1 hour</span></span>

<span data-ttu-id="0c560-142">Event Grid adds a small randomization to all retry intervals.</span><span class="sxs-lookup"><span data-stu-id="0c560-142">Event Grid adds a small randomization to all retry intervals.</span></span> <span data-ttu-id="0c560-143">After one hour, event delivery is retried once an hour.</span><span class="sxs-lookup"><span data-stu-id="0c560-143">After one hour, event delivery is retried once an hour.</span></span>

<span data-ttu-id="0c560-144">By default, Event Grid expires all events that aren't delivered within 24 hours.</span><span class="sxs-lookup"><span data-stu-id="0c560-144">By default, Event Grid expires all events that aren't delivered within 24 hours.</span></span> <span data-ttu-id="0c560-145">You can [customize the retry policy](manage-event-delivery.md) when creating an event subscription.</span><span class="sxs-lookup"><span data-stu-id="0c560-145">You can [customize the retry policy](manage-event-delivery.md) when creating an event subscription.</span></span> <span data-ttu-id="0c560-146">You provide the maximum number of delivery attempts (default is 30) and the event time-to-live (default is 1440 minutes).</span><span class="sxs-lookup"><span data-stu-id="0c560-146">You provide the maximum number of delivery attempts (default is 30) and the event time-to-live (default is 1440 minutes).</span></span>

## <a name="dead-letter-events"></a><span data-ttu-id="0c560-147">Dead-letter events</span><span class="sxs-lookup"><span data-stu-id="0c560-147">Dead-letter events</span></span>

<span data-ttu-id="0c560-148">When Event Grid can't deliver an event, it can send the undelivered event to a storage account.</span><span class="sxs-lookup"><span data-stu-id="0c560-148">When Event Grid can't deliver an event, it can send the undelivered event to a storage account.</span></span> <span data-ttu-id="0c560-149">This process is known as dead-lettering.</span><span class="sxs-lookup"><span data-stu-id="0c560-149">This process is known as dead-lettering.</span></span> <span data-ttu-id="0c560-150">To see undelivered events, you can pull them from the dead-letter location.</span><span class="sxs-lookup"><span data-stu-id="0c560-150">To see undelivered events, you can pull them from the dead-letter location.</span></span> <span data-ttu-id="0c560-151">For more information, see [Dead letter and retry policies](manage-event-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="0c560-151">For more information, see [Dead letter and retry policies](manage-event-delivery.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c560-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c560-152">Next steps</span></span>

* <span data-ttu-id="0c560-153">To view the status of event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="0c560-153">To view the status of event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).</span></span>
* <span data-ttu-id="0c560-154">To customize event delivery options, see [Manage Event Grid delivery settings](manage-event-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="0c560-154">To customize event delivery options, see [Manage Event Grid delivery settings](manage-event-delivery.md).</span></span>
* <span data-ttu-id="0c560-155">For an introduction to Event Grid, see [About Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c560-155">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="0c560-156">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="0c560-156">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>