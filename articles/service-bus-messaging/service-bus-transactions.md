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
# <a name="overview-of-service-bus-transaction-processing"></a>Overview of Service Bus transaction processing
This article discusses the transaction capabilities of Azure Service Bus. Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions). This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.

## <a name="transactions-in-service-bus"></a>Transactions in Service Bus
A [transaction](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*. By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly. In this respect transactions act as one unit, which is often referred to as *atomicity*. 

Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores. All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional. As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number. From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.

Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction. For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.

## <a name="operations-within-a-transaction-scope"></a>Operations within a transaction scope
The operations that can be performed within a transaction scope are as follows:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.

The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.

## <a name="transfers-and-send-via"></a>Transfers and "send via"
To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*. In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on. The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.

The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages. In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation. 

### <a name="see-it-in-code"></a>See it in code
To set up such transfers, you create a message sender that targets the destination queue via the transfer queue. You will also have a receiver that pulls messages from that same queue. For example:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

A simple transaction then uses these elements, as in the following example:

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

## <a name="next-steps"></a>Next steps

See the following articles for more information about Service Bus queues:

* [Chaining Service Bus entities with auto-forwarding](service-bus-auto-forwarding.md)
* [Auto-forward sample](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AutoForward)
* [Atomic Transactions with Service Bus sample](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/AtomicTransactions)
* [Azure Queues and Service Bus queues compared](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [How to use Service Bus queues](service-bus-dotnet-get-started-with-queues.md)

