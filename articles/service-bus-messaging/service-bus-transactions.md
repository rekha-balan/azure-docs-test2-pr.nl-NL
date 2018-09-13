---
title: Overview of transaction processing in Azure Service Bus | Microsoft Docs
description: Overview of Azure Service Bus atomic transactions and send via
services: service-bus-messaging
documentationcenter: .net
author: spelluru
manager: timlt
editor: ''
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/22/2018
ms.author: spelluru
ms.openlocfilehash: bc0e0bfb8d4dc8637c191785a98f5d15e086cbf5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774455"
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="f233b-103">Overview of Service Bus transaction processing</span><span class="sxs-lookup"><span data-stu-id="f233b-103">Overview of Service Bus transaction processing</span></span>

<span data-ttu-id="f233b-104">This article discusses the transaction capabilities of Microsoft Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f233b-104">This article discusses the transaction capabilities of Microsoft Azure Service Bus.</span></span> <span data-ttu-id="f233b-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="f233b-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="f233b-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span><span class="sxs-lookup"><span data-stu-id="f233b-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="f233b-107">Transactions in Service Bus</span><span class="sxs-lookup"><span data-stu-id="f233b-107">Transactions in Service Bus</span></span>

<span data-ttu-id="f233b-108">A [*transaction*](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span><span class="sxs-lookup"><span data-stu-id="f233b-108">A [*transaction*](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="f233b-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span><span class="sxs-lookup"><span data-stu-id="f233b-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="f233b-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span><span class="sxs-lookup"><span data-stu-id="f233b-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="f233b-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span><span class="sxs-lookup"><span data-stu-id="f233b-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="f233b-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span><span class="sxs-lookup"><span data-stu-id="f233b-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="f233b-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span><span class="sxs-lookup"><span data-stu-id="f233b-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="f233b-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span><span class="sxs-lookup"><span data-stu-id="f233b-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="f233b-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span><span class="sxs-lookup"><span data-stu-id="f233b-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="f233b-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span><span class="sxs-lookup"><span data-stu-id="f233b-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="f233b-117">Operations within a transaction scope</span><span class="sxs-lookup"><span data-stu-id="f233b-117">Operations within a transaction scope</span></span>

<span data-ttu-id="f233b-118">The operations that can be performed within a transaction scope are as follows:</span><span class="sxs-lookup"><span data-stu-id="f233b-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="f233b-119">**[QueueClient](/dotnet/api/microsoft.azure.servicebus.queueclient), [MessageSender](/dotnet/api/microsoft.azure.servicebus.core.messagesender), [TopicClient](/dotnet/api/microsoft.azure.servicebus.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="f233b-119">**[QueueClient](/dotnet/api/microsoft.azure.servicebus.queueclient), [MessageSender](/dotnet/api/microsoft.azure.servicebus.core.messagesender), [TopicClient](/dotnet/api/microsoft.azure.servicebus.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="f233b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="f233b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="f233b-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.azure.servicebus.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage) callback, and only then opens a transaction scope for processing the message.</span><span class="sxs-lookup"><span data-stu-id="f233b-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.azure.servicebus.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="f233b-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span><span class="sxs-lookup"><span data-stu-id="f233b-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="f233b-123">Transfers and "send via"</span><span class="sxs-lookup"><span data-stu-id="f233b-123">Transfers and "send via"</span></span>

<span data-ttu-id="f233b-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span><span class="sxs-lookup"><span data-stu-id="f233b-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="f233b-125">In a transfer operation, a sender first sends a message to a *transfer queue*, and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span><span class="sxs-lookup"><span data-stu-id="f233b-125">In a transfer operation, a sender first sends a message to a *transfer queue*, and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="f233b-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span><span class="sxs-lookup"><span data-stu-id="f233b-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="f233b-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span><span class="sxs-lookup"><span data-stu-id="f233b-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="f233b-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span><span class="sxs-lookup"><span data-stu-id="f233b-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="f233b-129">See it in code</span><span class="sxs-lookup"><span data-stu-id="f233b-129">See it in code</span></span>

<span data-ttu-id="f233b-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span><span class="sxs-lookup"><span data-stu-id="f233b-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="f233b-131">You also have a receiver that pulls messages from that same queue.</span><span class="sxs-lookup"><span data-stu-id="f233b-131">You also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="f233b-132">For example:</span><span class="sxs-lookup"><span data-stu-id="f233b-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="f233b-133">A simple transaction then uses these elements, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="f233b-133">A simple transaction then uses these elements, as in the following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f233b-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="f233b-134">Next steps</span></span>

<span data-ttu-id="f233b-135">See the following articles for more information about Service Bus queues:</span><span class="sxs-lookup"><span data-stu-id="f233b-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="f233b-136">How to use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="f233b-136">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="f233b-137">Chaining Service Bus entities with auto-forwarding</span><span class="sxs-lookup"><span data-stu-id="f233b-137">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="f233b-138">Auto-forward sample</span><span class="sxs-lookup"><span data-stu-id="f233b-138">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="f233b-139">Atomic Transactions with Service Bus sample</span><span class="sxs-lookup"><span data-stu-id="f233b-139">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="f233b-140">Azure Queues and Service Bus queues compared</span><span class="sxs-lookup"><span data-stu-id="f233b-140">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)


