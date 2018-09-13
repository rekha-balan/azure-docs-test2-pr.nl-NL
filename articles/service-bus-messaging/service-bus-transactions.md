---
title: Overview of transaction processing in Azure Service Bus | Microsoft Docs
description: Overview of Azure Service Bus atomic transactions and send via
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 8d0f3818831a22550fb0eea9bcbc1f62b133003a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556331"
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="6c7b0-103">Overview of Service Bus transaction processing</span><span class="sxs-lookup"><span data-stu-id="6c7b0-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="6c7b0-104">This article discusses the transaction capabilities of Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="6c7b0-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="6c7b0-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions).</span></span> <span data-ttu-id="6c7b0-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="6c7b0-107">Transactions in Service Bus</span><span class="sxs-lookup"><span data-stu-id="6c7b0-107">Transactions in Service Bus</span></span>
<span data-ttu-id="6c7b0-108">A [transaction](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-108">A [transaction](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="6c7b0-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="6c7b0-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="6c7b0-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="6c7b0-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="6c7b0-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="6c7b0-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="6c7b0-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="6c7b0-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="6c7b0-117">Operations within a transaction scope</span><span class="sxs-lookup"><span data-stu-id="6c7b0-117">Operations within a transaction scope</span></span>
<span data-ttu-id="6c7b0-118">The operations that can be performed within a transaction scope are as follows:</span><span class="sxs-lookup"><span data-stu-id="6c7b0-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="6c7b0-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="6c7b0-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="6c7b0-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="6c7b0-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="6c7b0-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="6c7b0-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="6c7b0-123">Transfers and "send via"</span><span class="sxs-lookup"><span data-stu-id="6c7b0-123">Transfers and "send via"</span></span>
<span data-ttu-id="6c7b0-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="6c7b0-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="6c7b0-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="6c7b0-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="6c7b0-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="6c7b0-129">See it in code</span><span class="sxs-lookup"><span data-stu-id="6c7b0-129">See it in code</span></span>
<span data-ttu-id="6c7b0-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="6c7b0-131">You will also have a receiver that pulls messages from that same queue.</span><span class="sxs-lookup"><span data-stu-id="6c7b0-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="6c7b0-132">For example:</span><span class="sxs-lookup"><span data-stu-id="6c7b0-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="6c7b0-133">A simple transaction then uses these elements, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="6c7b0-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="6c7b0-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c7b0-134">Next steps</span></span>

<span data-ttu-id="6c7b0-135">See the following articles for more information about Service Bus queues:</span><span class="sxs-lookup"><span data-stu-id="6c7b0-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="6c7b0-136">Chaining Service Bus entities with auto-forwarding</span><span class="sxs-lookup"><span data-stu-id="6c7b0-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="6c7b0-137">Auto-forward sample</span><span class="sxs-lookup"><span data-stu-id="6c7b0-137">Auto-forward sample</span></span>](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AutoForward)
* [<span data-ttu-id="6c7b0-138">Atomic Transactions with Service Bus sample</span><span class="sxs-lookup"><span data-stu-id="6c7b0-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions)
* [<span data-ttu-id="6c7b0-139">Azure Queues and Service Bus queues compared</span><span class="sxs-lookup"><span data-stu-id="6c7b0-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="6c7b0-140">How to use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="6c7b0-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

