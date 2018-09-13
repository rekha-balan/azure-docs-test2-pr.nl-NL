---
title: Azure Service Bus messaging overview | Microsoft Docs
description: Description of Service Bus messaging
services: service-bus-messaging
documentationcenter: ''
author: spelluru
manager: timlt
editor: ''
ms.service: service-bus-messaging
ms.topic: overview
ms.date: 05/22/2018
ms.custom: mvc
ms.author: spelluru
ms.openlocfilehash: a291d4d7ecafde366a20b7e7f1f12a95303da90d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797880"
---
# <a name="what-is-azure-service-bus"></a><span data-ttu-id="c8a3f-103">What is Azure Service Bus?</span><span class="sxs-lookup"><span data-stu-id="c8a3f-103">What is Azure Service Bus?</span></span>

<span data-ttu-id="c8a3f-104">Microsoft Azure Service Bus is a fully managed enterprise integration message broker.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-104">Microsoft Azure Service Bus is a fully managed enterprise integration message broker.</span></span> <span data-ttu-id="c8a3f-105">Service Bus is most commonly used to decouple applications and services from each other, and is a reliable and secure platform for asynchronous data and state transfer.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-105">Service Bus is most commonly used to decouple applications and services from each other, and is a reliable and secure platform for asynchronous data and state transfer.</span></span> <span data-ttu-id="c8a3f-106">Data is transferred between different applications and services using *messages*.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-106">Data is transferred between different applications and services using *messages*.</span></span> <span data-ttu-id="c8a3f-107">A message is in binary format, which can contain JSON, XML, or just text.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-107">A message is in binary format, which can contain JSON, XML, or just text.</span></span> 

<span data-ttu-id="c8a3f-108">Some common messaging scenarios are:</span><span class="sxs-lookup"><span data-stu-id="c8a3f-108">Some common messaging scenarios are:</span></span>

* <span data-ttu-id="c8a3f-109">Messaging: transfer business data, such as sales or purchase orders, journals, or inventory movements.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-109">Messaging: transfer business data, such as sales or purchase orders, journals, or inventory movements.</span></span>
* <span data-ttu-id="c8a3f-110">Decouple applications: improve reliability and scalability of applications and services (client and service do not have to be online at the same time).</span><span class="sxs-lookup"><span data-stu-id="c8a3f-110">Decouple applications: improve reliability and scalability of applications and services (client and service do not have to be online at the same time).</span></span>
* <span data-ttu-id="c8a3f-111">Topics and subscriptions: enable 1:*n* relationships between publishers and subscribers.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-111">Topics and subscriptions: enable 1:*n* relationships between publishers and subscribers.</span></span>
* <span data-ttu-id="c8a3f-112">Message sessions: implement workflows that require message ordering or message deferral.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-112">Message sessions: implement workflows that require message ordering or message deferral.</span></span>

## <a name="namespaces"></a><span data-ttu-id="c8a3f-113">Namespaces</span><span class="sxs-lookup"><span data-stu-id="c8a3f-113">Namespaces</span></span>

<span data-ttu-id="c8a3f-114">A namespace is a scoping container for all messaging components.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-114">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="c8a3f-115">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-115">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span>

## <a name="queues"></a><span data-ttu-id="c8a3f-116">Queues</span><span class="sxs-lookup"><span data-stu-id="c8a3f-116">Queues</span></span>

<span data-ttu-id="c8a3f-117">Messages are sent to and received from *queues*.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-117">Messages are sent to and received from *queues*.</span></span> <span data-ttu-id="c8a3f-118">Queues enable you to store messages until the receiving application is available to receive and process them.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-118">Queues enable you to store messages until the receiving application is available to receive and process them.</span></span>

![Queue](./media/service-bus-messaging-overview/about-service-bus-queue.png)

<span data-ttu-id="c8a3f-120">Messages in queues are ordered and timestamped on arrival.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-120">Messages in queues are ordered and timestamped on arrival.</span></span> <span data-ttu-id="c8a3f-121">Once accepted, the message is held safely in redundant storage.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-121">Once accepted, the message is held safely in redundant storage.</span></span> <span data-ttu-id="c8a3f-122">Messages are delivered in *pull* mode, which delivers messages on request.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-122">Messages are delivered in *pull* mode, which delivers messages on request.</span></span>

## <a name="topics"></a><span data-ttu-id="c8a3f-123">Topics</span><span class="sxs-lookup"><span data-stu-id="c8a3f-123">Topics</span></span>

<span data-ttu-id="c8a3f-124">You can also use *topics* to send and receive messages.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-124">You can also use *topics* to send and receive messages.</span></span> <span data-ttu-id="c8a3f-125">While a queue is often used for point-to-point communication, topics are useful in publish/subscribe scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-125">While a queue is often used for point-to-point communication, topics are useful in publish/subscribe scenarios.</span></span>

![Topic](./media/service-bus-messaging-overview/about-service-bus-topic.png)

<span data-ttu-id="c8a3f-127">Topics can have multiple, independent subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-127">Topics can have multiple, independent subscriptions.</span></span> <span data-ttu-id="c8a3f-128">A subscriber to a topic can receive a copy of each message sent to that topic.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-128">A subscriber to a topic can receive a copy of each message sent to that topic.</span></span> <span data-ttu-id="c8a3f-129">Subscriptions are named entities, which are durably created but can optionally expire or auto-delete.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-129">Subscriptions are named entities, which are durably created but can optionally expire or auto-delete.</span></span>

<span data-ttu-id="c8a3f-130">In some scenarios, you may not want individual subscriptions to receive all messages sent to a topic.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-130">In some scenarios, you may not want individual subscriptions to receive all messages sent to a topic.</span></span> <span data-ttu-id="c8a3f-131">If so, you can use [rules and filters](topic-filters.md) to define conditions that trigger optional [actions](topic-filters.md#actions), filter specified messages, and set or modify message properties.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-131">If so, you can use [rules and filters](topic-filters.md) to define conditions that trigger optional [actions](topic-filters.md#actions), filter specified messages, and set or modify message properties.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="c8a3f-132">Advanced features</span><span class="sxs-lookup"><span data-stu-id="c8a3f-132">Advanced features</span></span>

<span data-ttu-id="c8a3f-133">Service Bus also has advanced features that enable you to solve more complex messaging problems.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-133">Service Bus also has advanced features that enable you to solve more complex messaging problems.</span></span> <span data-ttu-id="c8a3f-134">The following sections describe these key features:</span><span class="sxs-lookup"><span data-stu-id="c8a3f-134">The following sections describe these key features:</span></span>

### <a name="message-sessions"></a><span data-ttu-id="c8a3f-135">Message sessions</span><span class="sxs-lookup"><span data-stu-id="c8a3f-135">Message sessions</span></span>

<span data-ttu-id="c8a3f-136">To realize a first-in, first-out (FIFO) guarantee in Service Bus, use sessions.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-136">To realize a first-in, first-out (FIFO) guarantee in Service Bus, use sessions.</span></span> <span data-ttu-id="c8a3f-137">[Message sessions](message-sessions.md) enable joint and ordered handling of unbounded sequences of related messages.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-137">[Message sessions](message-sessions.md) enable joint and ordered handling of unbounded sequences of related messages.</span></span> 

### <a name="auto-forwarding"></a><span data-ttu-id="c8a3f-138">Auto-forwarding</span><span class="sxs-lookup"><span data-stu-id="c8a3f-138">Auto-forwarding</span></span>

<span data-ttu-id="c8a3f-139">The [auto-forwarding](service-bus-auto-forwarding.md) feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-139">The [auto-forwarding](service-bus-auto-forwarding.md) feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="c8a3f-140">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span><span class="sxs-lookup"><span data-stu-id="c8a3f-140">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span>

### <a name="dead-lettering"></a><span data-ttu-id="c8a3f-141">Dead-lettering</span><span class="sxs-lookup"><span data-stu-id="c8a3f-141">Dead-lettering</span></span>

<span data-ttu-id="c8a3f-142">Service Bus supports a [dead-letter queue](service-bus-dead-letter-queues.md) (DLQ) to hold messages that cannot be delivered to any receiver, or messages that cannot be processed.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-142">Service Bus supports a [dead-letter queue](service-bus-dead-letter-queues.md) (DLQ) to hold messages that cannot be delivered to any receiver, or messages that cannot be processed.</span></span> <span data-ttu-id="c8a3f-143">You can then remove messages from the DLQ and inspect them.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-143">You can then remove messages from the DLQ and inspect them.</span></span>

### <a name="scheduled-delivery"></a><span data-ttu-id="c8a3f-144">Scheduled delivery</span><span class="sxs-lookup"><span data-stu-id="c8a3f-144">Scheduled delivery</span></span>

<span data-ttu-id="c8a3f-145">You can submit messages to a queue or topic [for delayed processing](message-sequencing.md#scheduled-messages); for example, to schedule a job to become available for processing by a system at a certain time.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-145">You can submit messages to a queue or topic [for delayed processing](message-sequencing.md#scheduled-messages); for example, to schedule a job to become available for processing by a system at a certain time.</span></span>

### <a name="message-deferral"></a><span data-ttu-id="c8a3f-146">Message deferral</span><span class="sxs-lookup"><span data-stu-id="c8a3f-146">Message deferral</span></span>

<span data-ttu-id="c8a3f-147">When a queue or subscription client receives a message that it is willing to process, but for which processing is not currently possible due to special circumstances within the application, the entity has the option to [defer retrieval of the message](message-deferral.md) to a later point.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-147">When a queue or subscription client receives a message that it is willing to process, but for which processing is not currently possible due to special circumstances within the application, the entity has the option to [defer retrieval of the message](message-deferral.md) to a later point.</span></span> <span data-ttu-id="c8a3f-148">The message remains in the queue or subscription, but it is set aside.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-148">The message remains in the queue or subscription, but it is set aside.</span></span>

### <a name="batching"></a><span data-ttu-id="c8a3f-149">Batching</span><span class="sxs-lookup"><span data-stu-id="c8a3f-149">Batching</span></span>

<span data-ttu-id="c8a3f-150">[Client-side batching](service-bus-performance-improvements.md#client-side-batching) enables a queue or topic client to delay sending a message for a certain period of time.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-150">[Client-side batching](service-bus-performance-improvements.md#client-side-batching) enables a queue or topic client to delay sending a message for a certain period of time.</span></span> <span data-ttu-id="c8a3f-151">If the client sends additional messages during this time period, it transmits the messages in a single batch.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-151">If the client sends additional messages during this time period, it transmits the messages in a single batch.</span></span> 

### <a name="transactions"></a><span data-ttu-id="c8a3f-152">Transactions</span><span class="sxs-lookup"><span data-stu-id="c8a3f-152">Transactions</span></span>

<span data-ttu-id="c8a3f-153">A [transaction](service-bus-transactions.md) groups two or more operations together into an execution scope.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-153">A [transaction](service-bus-transactions.md) groups two or more operations together into an execution scope.</span></span> <span data-ttu-id="c8a3f-154">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-154">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span>

### <a name="filtering-and-actions"></a><span data-ttu-id="c8a3f-155">Filtering and actions</span><span class="sxs-lookup"><span data-stu-id="c8a3f-155">Filtering and actions</span></span>

<span data-ttu-id="c8a3f-156">Subscribers can define which messages they want to receive from a topic.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-156">Subscribers can define which messages they want to receive from a topic.</span></span> <span data-ttu-id="c8a3f-157">These messages are specified in the form of one or more [named subscription rules](topic-filters.md).</span><span class="sxs-lookup"><span data-stu-id="c8a3f-157">These messages are specified in the form of one or more [named subscription rules](topic-filters.md).</span></span> <span data-ttu-id="c8a3f-158">For each matching rule condition, the subscription produces a copy of the message, which may be differently annotated for each matching rule.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-158">For each matching rule condition, the subscription produces a copy of the message, which may be differently annotated for each matching rule.</span></span>

### <a name="auto-delete-on-idle"></a><span data-ttu-id="c8a3f-159">Auto-delete on idle</span><span class="sxs-lookup"><span data-stu-id="c8a3f-159">Auto-delete on idle</span></span>

<span data-ttu-id="c8a3f-160">[Auto-delete on idle](/dotnet/api/microsoft.servicebus.messaging.queuedescription.autodeleteonidle) enables you to specify an idle interval after which the queue is automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-160">[Auto-delete on idle](/dotnet/api/microsoft.servicebus.messaging.queuedescription.autodeleteonidle) enables you to specify an idle interval after which the queue is automatically deleted.</span></span> <span data-ttu-id="c8a3f-161">The minimum duration is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-161">The minimum duration is 5 minutes.</span></span>

### <a name="duplicate-detection"></a><span data-ttu-id="c8a3f-162">Duplicate detection</span><span class="sxs-lookup"><span data-stu-id="c8a3f-162">Duplicate detection</span></span>

<span data-ttu-id="c8a3f-163">If an error occurs that causes the client to have any doubt about the outcome of a send operation, [duplicate detection](duplicate-detection.md) takes the doubt out of these situations by enabling the sender re-send the same message, and the queue or topic discards any duplicate copies.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-163">If an error occurs that causes the client to have any doubt about the outcome of a send operation, [duplicate detection](duplicate-detection.md) takes the doubt out of these situations by enabling the sender re-send the same message, and the queue or topic discards any duplicate copies.</span></span>

### <a name="sas-rbac-and-msi"></a><span data-ttu-id="c8a3f-164">SAS, RBAC, and MSI</span><span class="sxs-lookup"><span data-stu-id="c8a3f-164">SAS, RBAC, and MSI</span></span>

<span data-ttu-id="c8a3f-165">Service Bus supports security protocols such as [Shared Access Signatures](service-bus-sas.md) (SAS), [Role Based Access Control](service-bus-role-based-access-control.md) (RBAC) and [Managed Service Identity](service-bus-managed-service-identity.md) (MSI).</span><span class="sxs-lookup"><span data-stu-id="c8a3f-165">Service Bus supports security protocols such as [Shared Access Signatures](service-bus-sas.md) (SAS), [Role Based Access Control](service-bus-role-based-access-control.md) (RBAC) and [Managed Service Identity](service-bus-managed-service-identity.md) (MSI).</span></span>

### <a name="geo-disaster-recovery"></a><span data-ttu-id="c8a3f-166">Geo-disaster recovery</span><span class="sxs-lookup"><span data-stu-id="c8a3f-166">Geo-disaster recovery</span></span>

<span data-ttu-id="c8a3f-167">When Azure regions or datacenters experience downtime, [Geo-disaster recovery](service-bus-geo-dr.md) enables data processing to continue operating in a different region or datacenter.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-167">When Azure regions or datacenters experience downtime, [Geo-disaster recovery](service-bus-geo-dr.md) enables data processing to continue operating in a different region or datacenter.</span></span>

### <a name="security"></a><span data-ttu-id="c8a3f-168">Security</span><span class="sxs-lookup"><span data-stu-id="c8a3f-168">Security</span></span>

<span data-ttu-id="c8a3f-169">Service Bus supports standard [AMQP 1.0](service-bus-amqp-overview.md) and [HTTP/REST](/rest/api/servicebus/) protocols.</span><span class="sxs-lookup"><span data-stu-id="c8a3f-169">Service Bus supports standard [AMQP 1.0](service-bus-amqp-overview.md) and [HTTP/REST](/rest/api/servicebus/) protocols.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="c8a3f-170">Client libraries</span><span class="sxs-lookup"><span data-stu-id="c8a3f-170">Client libraries</span></span>

<span data-ttu-id="c8a3f-171">Service Bus supports client libraries for [.NET](https://github.com/Azure/azure-service-bus-dotnet/tree/master), [Java](https://github.com/Azure/azure-service-bus-java/tree/master), [JMS](https://github.com/Azure/azure-service-bus/tree/master/samples/Java/qpid-jms-client).</span><span class="sxs-lookup"><span data-stu-id="c8a3f-171">Service Bus supports client libraries for [.NET](https://github.com/Azure/azure-service-bus-dotnet/tree/master), [Java](https://github.com/Azure/azure-service-bus-java/tree/master), [JMS](https://github.com/Azure/azure-service-bus/tree/master/samples/Java/qpid-jms-client).</span></span>

## <a name="integration"></a><span data-ttu-id="c8a3f-172">Integration</span><span class="sxs-lookup"><span data-stu-id="c8a3f-172">Integration</span></span>

<span data-ttu-id="c8a3f-173">Service Bus fully integrates with the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="c8a3f-173">Service Bus fully integrates with the following Azure services:</span></span>

- [<span data-ttu-id="c8a3f-174">Event Grid</span><span class="sxs-lookup"><span data-stu-id="c8a3f-174">Event Grid</span></span>](https://azure.microsoft.com/services/event-grid/) 
- [<span data-ttu-id="c8a3f-175">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c8a3f-175">Logic Apps</span></span>](https://azure.microsoft.com/services/logic-apps/) 
- [<span data-ttu-id="c8a3f-176">Functions</span><span class="sxs-lookup"><span data-stu-id="c8a3f-176">Functions</span></span>](https://azure.microsoft.com/services/functions/) 
- [<span data-ttu-id="c8a3f-177">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="c8a3f-177">Dynamics 365</span></span>](https://dynamics.microsoft.com)
- [<span data-ttu-id="c8a3f-178">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c8a3f-178">Stream Analytics</span></span>](https://azure.microsoft.com/services/stream-analytics/)
 
## <a name="next-steps"></a><span data-ttu-id="c8a3f-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8a3f-179">Next steps</span></span>

<span data-ttu-id="c8a3f-180">To get started using Service Bus messaging, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="c8a3f-180">To get started using Service Bus messaging, see the following articles:</span></span>

* [<span data-ttu-id="c8a3f-181">Compare Azure messaging services</span><span class="sxs-lookup"><span data-stu-id="c8a3f-181">Compare Azure messaging services</span></span>](../event-grid/compare-messaging-services.md?toc=%2fazure%2fservice-bus-messaging%2ftoc.json&bc=%2fazure%2fservice-bus-messaging%2fbreadcrumb%2ftoc.json)
* <span data-ttu-id="c8a3f-182">Learn more about Azure Service Bus [Standard and Premium](https://azure.microsoft.com/pricing/details/service-bus/) tiers and their pricing</span><span class="sxs-lookup"><span data-stu-id="c8a3f-182">Learn more about Azure Service Bus [Standard and Premium](https://azure.microsoft.com/pricing/details/service-bus/) tiers and their pricing</span></span>
* [<span data-ttu-id="c8a3f-183">Performance and Latency of Azure Service Bus Premium tier</span><span class="sxs-lookup"><span data-stu-id="c8a3f-183">Performance and Latency of Azure Service Bus Premium tier</span></span>](https://blogs.msdn.microsoft.com/servicebus/2016/07/18/premium-messaging-how-fast-is-it/)
* <span data-ttu-id="c8a3f-184">Try the quickstarts in [.NET](service-bus-quickstart-powershell.md), [Java](service-bus-quickstart-powershell.md), or [JMS](service-bus-quickstart-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c8a3f-184">Try the quickstarts in [.NET](service-bus-quickstart-powershell.md), [Java](service-bus-quickstart-powershell.md), or [JMS](service-bus-quickstart-powershell.md)</span></span>
