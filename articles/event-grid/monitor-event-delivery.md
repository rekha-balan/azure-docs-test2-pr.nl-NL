---
title: Monitor Azure Event Grid message delivery
description: Describes how to monitor the delivery of Azure Event Grid messages.
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: conceptual
ms.date: 05/24/2018
ms.author: tomfitz
ms.openlocfilehash: 625f3e228bb28c85e68fb592914fb2191baf3e4e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857840"
---
# <a name="monitor-event-grid-message-delivery"></a><span data-ttu-id="9d975-103">Monitor Event Grid message delivery</span><span class="sxs-lookup"><span data-stu-id="9d975-103">Monitor Event Grid message delivery</span></span> 

<span data-ttu-id="9d975-104">This article describes how to use the portal to see the status of event deliveries.</span><span class="sxs-lookup"><span data-stu-id="9d975-104">This article describes how to use the portal to see the status of event deliveries.</span></span>

<span data-ttu-id="9d975-105">Event Grid provides durable delivery.</span><span class="sxs-lookup"><span data-stu-id="9d975-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="9d975-106">It delivers each message at least once for each subscription.</span><span class="sxs-lookup"><span data-stu-id="9d975-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="9d975-107">Events are sent to the registered webhook of each subscription immediately.</span><span class="sxs-lookup"><span data-stu-id="9d975-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="9d975-108">If a webhook doesn't acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span><span class="sxs-lookup"><span data-stu-id="9d975-108">If a webhook doesn't acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span>

<span data-ttu-id="9d975-109">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span><span class="sxs-lookup"><span data-stu-id="9d975-109">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>

## <a name="delivery-metrics"></a><span data-ttu-id="9d975-110">Delivery metrics</span><span class="sxs-lookup"><span data-stu-id="9d975-110">Delivery metrics</span></span>

<span data-ttu-id="9d975-111">The portal displays metrics for the status of delivering event messages.</span><span class="sxs-lookup"><span data-stu-id="9d975-111">The portal displays metrics for the status of delivering event messages.</span></span>

<span data-ttu-id="9d975-112">For topics, the metrics are:</span><span class="sxs-lookup"><span data-stu-id="9d975-112">For topics, the metrics are:</span></span>

* <span data-ttu-id="9d975-113">**Publish Succeeded**: Event successfully sent to the topic, and processed with a 2xx response.</span><span class="sxs-lookup"><span data-stu-id="9d975-113">**Publish Succeeded**: Event successfully sent to the topic, and processed with a 2xx response.</span></span>
* <span data-ttu-id="9d975-114">**Publish Failed**: Event sent to the topic but rejected with an error code.</span><span class="sxs-lookup"><span data-stu-id="9d975-114">**Publish Failed**: Event sent to the topic but rejected with an error code.</span></span>
* <span data-ttu-id="9d975-115">**Unmatched**: Event successfully published to the topic, but not matched to an event subscription.</span><span class="sxs-lookup"><span data-stu-id="9d975-115">**Unmatched**: Event successfully published to the topic, but not matched to an event subscription.</span></span> <span data-ttu-id="9d975-116">The event was dropped.</span><span class="sxs-lookup"><span data-stu-id="9d975-116">The event was dropped.</span></span>

<span data-ttu-id="9d975-117">For subscriptions, the metrics are:</span><span class="sxs-lookup"><span data-stu-id="9d975-117">For subscriptions, the metrics are:</span></span>

* <span data-ttu-id="9d975-118">**Delivery Succeeded**: Event successfully delivered to the subscription's endpoint, and received a 2xx response.</span><span class="sxs-lookup"><span data-stu-id="9d975-118">**Delivery Succeeded**: Event successfully delivered to the subscription's endpoint, and received a 2xx response.</span></span>
* <span data-ttu-id="9d975-119">**Delivery Failed**: Event sent to subscription's endpoint, but received a 4xx or 5xx response.</span><span class="sxs-lookup"><span data-stu-id="9d975-119">**Delivery Failed**: Event sent to subscription's endpoint, but received a 4xx or 5xx response.</span></span>
* <span data-ttu-id="9d975-120">**Expired Events**: Event was not delivered and all retry attempts were sent.</span><span class="sxs-lookup"><span data-stu-id="9d975-120">**Expired Events**: Event was not delivered and all retry attempts were sent.</span></span> <span data-ttu-id="9d975-121">The event was dropped.</span><span class="sxs-lookup"><span data-stu-id="9d975-121">The event was dropped.</span></span>
* <span data-ttu-id="9d975-122">**Matched Events**: Event in the topic was matched by the event subscription.</span><span class="sxs-lookup"><span data-stu-id="9d975-122">**Matched Events**: Event in the topic was matched by the event subscription.</span></span>

## <a name="event-subscription-status"></a><span data-ttu-id="9d975-123">Event subscription status</span><span class="sxs-lookup"><span data-stu-id="9d975-123">Event subscription status</span></span>

<span data-ttu-id="9d975-124">To see metrics for an event subscription, you can either search by subscription type or by subscriptions for a specific resource.</span><span class="sxs-lookup"><span data-stu-id="9d975-124">To see metrics for an event subscription, you can either search by subscription type or by subscriptions for a specific resource.</span></span>

<span data-ttu-id="9d975-125">To search by event subscription type, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="9d975-125">To search by event subscription type, select **All services**.</span></span>

![Select all services](./media/monitor-event-delivery/all-services.png)

<span data-ttu-id="9d975-127">Search for **event grid** and select **Event Grid Subscriptions** from the available options.</span><span class="sxs-lookup"><span data-stu-id="9d975-127">Search for **event grid** and select **Event Grid Subscriptions** from the available options.</span></span>

![Search for event subscriptions](./media/monitor-event-delivery/search-and-select.png)

<span data-ttu-id="9d975-129">Filter by the type of event, the subscription, and location.</span><span class="sxs-lookup"><span data-stu-id="9d975-129">Filter by the type of event, the subscription, and location.</span></span> <span data-ttu-id="9d975-130">Select **Metrics** for the subscription to view.</span><span class="sxs-lookup"><span data-stu-id="9d975-130">Select **Metrics** for the subscription to view.</span></span>

![Filter event subscriptions](./media/monitor-event-delivery/filter-events.png)

<span data-ttu-id="9d975-132">View the metrics for the event topic and subscription.</span><span class="sxs-lookup"><span data-stu-id="9d975-132">View the metrics for the event topic and subscription.</span></span>

![View event metrics](./media/monitor-event-delivery/subscription-metrics.png)

<span data-ttu-id="9d975-134">To find the metrics for a specific resource, select that resource.</span><span class="sxs-lookup"><span data-stu-id="9d975-134">To find the metrics for a specific resource, select that resource.</span></span> <span data-ttu-id="9d975-135">Then, select **Events**.</span><span class="sxs-lookup"><span data-stu-id="9d975-135">Then, select **Events**.</span></span>

![Select events for a resource](./media/monitor-event-delivery/select-events.png)

<span data-ttu-id="9d975-137">You see the metrics for subscriptions for that resource.</span><span class="sxs-lookup"><span data-stu-id="9d975-137">You see the metrics for subscriptions for that resource.</span></span>

## <a name="custom-event-status"></a><span data-ttu-id="9d975-138">Custom event status</span><span class="sxs-lookup"><span data-stu-id="9d975-138">Custom event status</span></span>

<span data-ttu-id="9d975-139">If you've published a custom topic, you can view the metrics for it.</span><span class="sxs-lookup"><span data-stu-id="9d975-139">If you've published a custom topic, you can view the metrics for it.</span></span> <span data-ttu-id="9d975-140">Select the resource group for the topic, and select the topic.</span><span class="sxs-lookup"><span data-stu-id="9d975-140">Select the resource group for the topic, and select the topic.</span></span>

![Select custom topic](./media/monitor-event-delivery/select-custom-topic.png)

<span data-ttu-id="9d975-142">View the metrics for the custom event topic.</span><span class="sxs-lookup"><span data-stu-id="9d975-142">View the metrics for the custom event topic.</span></span>

![View event metrics](./media/monitor-event-delivery/custom-topic-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="9d975-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d975-144">Next steps</span></span>

* <span data-ttu-id="9d975-145">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span><span class="sxs-lookup"><span data-stu-id="9d975-145">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>
* <span data-ttu-id="9d975-146">For an introduction to Event Grid, see [About Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d975-146">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="9d975-147">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="9d975-147">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
