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
# <a name="monitor-event-grid-message-delivery"></a>Monitor Event Grid message delivery 

This article describes how to use the portal to see the status of event deliveries.

Event Grid provides durable delivery. It delivers each message at least once for each subscription. Events are sent to the registered webhook of each subscription immediately. If a webhook doesn't acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.

For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).

## <a name="delivery-metrics"></a>Delivery metrics

The portal displays metrics for the status of delivering event messages.

For topics, the metrics are:

* **Publish Succeeded**: Event successfully sent to the topic, and processed with a 2xx response.
* **Publish Failed**: Event sent to the topic but rejected with an error code.
* **Unmatched**: Event successfully published to the topic, but not matched to an event subscription. The event was dropped.

For subscriptions, the metrics are:

* **Delivery Succeeded**: Event successfully delivered to the subscription's endpoint, and received a 2xx response.
* **Delivery Failed**: Event sent to subscription's endpoint, but received a 4xx or 5xx response.
* **Expired Events**: Event was not delivered and all retry attempts were sent. The event was dropped.
* **Matched Events**: Event in the topic was matched by the event subscription.

## <a name="event-subscription-status"></a>Event subscription status

To see metrics for an event subscription, you can either search by subscription type or by subscriptions for a specific resource.

To search by event subscription type, select **All services**.

![Select all services](./media/monitor-event-delivery/all-services.png)

Search for **event grid** and select **Event Grid Subscriptions** from the available options.

![Search for event subscriptions](./media/monitor-event-delivery/search-and-select.png)

Filter by the type of event, the subscription, and location. Select **Metrics** for the subscription to view.

![Filter event subscriptions](./media/monitor-event-delivery/filter-events.png)

View the metrics for the event topic and subscription.

![View event metrics](./media/monitor-event-delivery/subscription-metrics.png)

To find the metrics for a specific resource, select that resource. Then, select **Events**.

![Select events for a resource](./media/monitor-event-delivery/select-events.png)

You see the metrics for subscriptions for that resource.

## <a name="custom-event-status"></a>Custom event status

If you've published a custom topic, you can view the metrics for it. Select the resource group for the topic, and select the topic.

![Select custom topic](./media/monitor-event-delivery/select-custom-topic.png)

View the metrics for the custom event topic.

![View event metrics](./media/monitor-event-delivery/custom-topic-metrics.png)

## <a name="next-steps"></a>Next steps

* For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).
* For an introduction to Event Grid, see [About Event Grid](overview.md).
* To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).
