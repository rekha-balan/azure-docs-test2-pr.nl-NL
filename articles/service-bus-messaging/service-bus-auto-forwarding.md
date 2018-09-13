---
title: Auto-forwarding Azure Service Bus messaging entities | Microsoft Docs
description: How to chain a Service Bus queue or subscription to another queue or topic.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 40cb1e6081d5cd88808fbea889f953b5b1b14d03
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556360"
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="47f3a-103">Chaining Service Bus entities with auto-forwarding</span><span class="sxs-lookup"><span data-stu-id="47f3a-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="47f3a-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span><span class="sxs-lookup"><span data-stu-id="47f3a-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="47f3a-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span><span class="sxs-lookup"><span data-stu-id="47f3a-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span> <span data-ttu-id="47f3a-106">Note that it is still possible to send a message to the destination entity directly.</span><span class="sxs-lookup"><span data-stu-id="47f3a-106">Note that it is still possible to send a message to the destination entity directly.</span></span> <span data-ttu-id="47f3a-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span><span class="sxs-lookup"><span data-stu-id="47f3a-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="47f3a-108">Using auto-forwarding</span><span class="sxs-lookup"><span data-stu-id="47f3a-108">Using auto-forwarding</span></span>
<span data-ttu-id="47f3a-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="47f3a-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="47f3a-110">The destination entity must exist at the time the source entity is created.</span><span class="sxs-lookup"><span data-stu-id="47f3a-110">The destination entity must exist at the time the source entity is created.</span></span> <span data-ttu-id="47f3a-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span><span class="sxs-lookup"><span data-stu-id="47f3a-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span></span>

<span data-ttu-id="47f3a-112">You can use auto-forwarding to scale out an individual topic.</span><span class="sxs-lookup"><span data-stu-id="47f3a-112">You can use auto-forwarding to scale out an individual topic.</span></span> <span data-ttu-id="47f3a-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span><span class="sxs-lookup"><span data-stu-id="47f3a-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span></span> <span data-ttu-id="47f3a-114">You can accommodate additional subscriptions by creating second-level topics.</span><span class="sxs-lookup"><span data-stu-id="47f3a-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="47f3a-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span><span class="sxs-lookup"><span data-stu-id="47f3a-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span></span>

![Auto-forwarding scenario][0]

<span data-ttu-id="47f3a-117">You can also use auto-forwarding to decouple message senders from receivers.</span><span class="sxs-lookup"><span data-stu-id="47f3a-117">You can also use auto-forwarding to decouple message senders from receivers.</span></span> <span data-ttu-id="47f3a-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span><span class="sxs-lookup"><span data-stu-id="47f3a-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="47f3a-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span><span class="sxs-lookup"><span data-stu-id="47f3a-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="47f3a-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span><span class="sxs-lookup"><span data-stu-id="47f3a-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span></span> <span data-ttu-id="47f3a-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span><span class="sxs-lookup"><span data-stu-id="47f3a-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span></span>

![Auto-forwarding scenario][1]

<span data-ttu-id="47f3a-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span><span class="sxs-lookup"><span data-stu-id="47f3a-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span></span> <span data-ttu-id="47f3a-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span><span class="sxs-lookup"><span data-stu-id="47f3a-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="47f3a-125">Auto-forwarding considerations</span><span class="sxs-lookup"><span data-stu-id="47f3a-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="47f3a-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span><span class="sxs-lookup"><span data-stu-id="47f3a-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span></span> <span data-ttu-id="47f3a-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span><span class="sxs-lookup"><span data-stu-id="47f3a-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span></span>

<span data-ttu-id="47f3a-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span><span class="sxs-lookup"><span data-stu-id="47f3a-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span></span> <span data-ttu-id="47f3a-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span><span class="sxs-lookup"><span data-stu-id="47f3a-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="47f3a-130">Service Bus bills one operation for each forwarded message.</span><span class="sxs-lookup"><span data-stu-id="47f3a-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="47f3a-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span><span class="sxs-lookup"><span data-stu-id="47f3a-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span></span>

<span data-ttu-id="47f3a-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span><span class="sxs-lookup"><span data-stu-id="47f3a-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span></span> <span data-ttu-id="47f3a-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span><span class="sxs-lookup"><span data-stu-id="47f3a-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47f3a-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="47f3a-134">Next steps</span></span>

<span data-ttu-id="47f3a-135">For detailed information about auto-forwarding, see the following reference topics:</span><span class="sxs-lookup"><span data-stu-id="47f3a-135">For detailed information about auto-forwarding, see the following reference topics:</span></span>

* <span data-ttu-id="47f3a-136">[SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="47f3a-136">[SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo]</span></span>
* <span data-ttu-id="47f3a-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="47f3a-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="47f3a-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="47f3a-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="47f3a-139">To learn more about Service Bus performance improvements, see</span><span class="sxs-lookup"><span data-stu-id="47f3a-139">To learn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="47f3a-140">Best Practices for performance improvements using Service Bus Messaging</span><span class="sxs-lookup"><span data-stu-id="47f3a-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="47f3a-141">[Partitioned messaging entities][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="47f3a-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-auto-forwarding/IC628631.gif
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md


