---
title: Create applications that use Azure Service Bus topics and subscriptions | Microsoft Docs
description: Introduction to the publish-subscribe capabilities offered by Service Bus topics and subscriptions.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: c6b48df1cfac926db6899ec25feecbde5e8c2fa3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556094"
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Create applications that use Service Bus topics and subscriptions
Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging. This article builds on the information provided in [Create applications that use Service Bus queues](service-bus-create-queues.md) and offers an introduction to the publish/subscribe capabilities offered by Service Bus topics.

## <a name="evolving-retail-scenario"></a>Evolving retail scenario
This article continues the retail scenario used in [Create applications that use Service Bus queues](service-bus-create-queues.md). Recall that sales data from individual Point of Sale (POS) terminals must be routed to an inventory management system which uses that data to determine when stock has to be replenished. Each POS terminal reports its sales data by sending messages to the **DataCollectionQueue** queue, where they remain until they are received by the inventory management system, as shown here:

![Service Bus 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-topics-subscriptions/IC657161.gif)

To evolve this scenario, a new requirement has been added to the system: the store owner wants to be able to monitor how the store is performing in real time.

To address this requirement, the system must "tap" off the sales data stream. We still want each message sent by the POS terminals to be sent to the inventory management system as before, but we want another copy of each message that we can use to present the dashboard view to the store owner.

In any situation such as this, in which you require each message to be consumed by multiple parties, you can use Service Bus *topics*. Topics provide a publish/subscribe pattern in which each published message is made available to one or more subscriptions registered with the topic. In contrast, with queues each message is received by a single consumer.

Messages are sent to a topic in the same way as they are sent to a queue. However, messages are not received from the topic directly; they are received from subscriptions. You can think of a subscription to a topic as a virtual queue that receives copies of the messages that are sent to that topic. Messages are received from a subscription the same way as they are received from a queue.

Going back to the retail scenario, the queue is replaced by a topic, and a subscription is added, which the inventory management system component can use. The system now appears as follows:

![Service Bus 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-topics-subscriptions/IC657165.gif)

The configuration here performs identically to the previous queue-based design. That is, messages sent to the topic are routed to the **Inventory** subscription, from which the **Inventory Management System** consumes them.

In order to support the management dashboard, we create a second subscription on the topic, as shown here:

![Service Bus 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-topics-subscriptions/IC657166.gif)

With this configuration, each message from the POS terminals is made available to both the **Dashboard** and **Inventory** subscriptions.

## <a name="show-me-the-code"></a>Show me the code
The article [Create applications that use Service Bus queues](service-bus-create-queues.md) describes how to sign up for an Azure account and create a service namespace. The easiest way to reference Service Bus dependencies is to install the Service Bus [Nuget package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). You can also find the Service Bus libraries as part of the Azure SDK. The download is available at the [Azure SDK download page](https://azure.microsoft.com/downloads/).

### <a name="create-the-topic-and-subscriptions"></a>Create the topic and subscriptions
Management operations for Service Bus messaging entities (queues and publish/subscribe topics) are performed via the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class. Appropriate credentials are required in order to create a **NamespaceManager** instance for a particular namespace. Service Bus uses a [Shared Access Signature (SAS)](service-bus-sas.md) based security model. The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) class represents a security token provider with built-in factory methods returning some well-known token providers. We’ll use a [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to hold the SAS credentials. The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) instance is then constructed with the base address of the Service Bus namespace and the token provider.

The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class provides methods to create, enumerate and delete messaging entities. The code that is shown here shows how the **NamespaceManager** instance is created and used to create the **DataCollectionTopic** topic.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Note that there are overloads of the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method that enable you to set properties of the topic. For example, you can set the default time-to-live (TTL) value for messages sent to the topic. Next, add the **Inventory** and **Dashboard** subscriptions.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-to-the-topic"></a>Send messages to the topic
For run-time operations on Service Bus entities; for example, sending and receiving messages, an application must first create a [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) object. Similar to the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, the **MessagingFactory** instance is created from the base address of the service namespace and the token provider.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Messages sent to and received from Service Bus topics, are instances of the [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) class. This class consists of a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold application properties, and a body of arbitrary application data. An application can set the body by passing in any serializable object (the following example passes in a **SalesData** object that represents the sales data from the POS terminal), which will use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) to serialize the object. Alternatively, a [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) object can be provided.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

The easiest way to send messages to the topic is to use [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) to create a [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Receive messages from a subscription
Similar to using queues, to receive messages from a subscription you can use a [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) object which you create directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) using [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). You can use one of the two different receive modes (**ReceiveAndDelete** and **PeekLock**), as discussed in [Create applications that use Service Bus queues](service-bus-create-queues.md).

Note that when you create a **MessageReceiver** for subscriptions, the *entityPath* parameter is of the form `topicPath/subscriptions/subscriptionName`. Therefore, to create a **MessageReceiver** for the **Inventory** subscription of the **DataCollectionTopic** topic, *entityPath* must be set to `DataCollectionTopic/subscriptions/Inventory`. The code appears as follows:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Subscription filters
So far, in this scenario all messages sent to the topic are made available to all registered subscriptions. The key phrase here is "made available." While Service Bus subscriptions see all messages sent to the topic, you can copy only a subset of those messages to the virtual subscription queue. This is performed using subscription *filters*. When you create a subscription, you can supply a filter expression in the form of a SQL92 style predicate that operates over the properties of the message, both the system properties (for example, [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) and the application properties, such as **StoreName** in the previous example.

Evolving the scenario to illustrate this, a second store is to be added to our retail scenario. Sales data from all of the POS terminals from both stores still have to be routed to the centralized inventory management system, but a store manager using the dashboard tool is only interested in the performance of that store. You can use subscription filtering to achieve this. Note that when the POS terminals publish messages, they set the **StoreName** application property on the message. Given two stores, for example **Redmond** and **Seattle**, the POS terminals in the Redmond store stamp their sales data messages with a **StoreName** equal to **Redmond**, whereas the Seattle store POS terminals use a **StoreName** equal to **Seattle**. The store manager of the Redmond store only wants to see data from its POS terminals. The system appears as follows:

![Service-Bus4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-topics-subscriptions/IC657167.gif)

To set up this routing, you create the **Dashboard** subscription as follows:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

With this [subscription filter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), only messages that have the **StoreName** property set to **Redmond** will be copied to the virtual queue for the **Dashboard** subscription. There is much more to subscription filtering, however. Applications can have multiple filter rules per subscription in addition to the ability to modify the properties of a message as it passes to a subscription's virtual queue.

## <a name="summary"></a>Summary
All of the reasons to use queuing described in [Create applications that use Service Bus queues](service-bus-create-queues.md) also apply to topics, specifically:

* Temporal decoupling – message producers and consumers do not have to be online at the same time.
* Load leveling – peaks in load are smoothed out by the topic enabling consuming applications to be provisioned for average load instead of peak load.
* Load balancing – similar to a queue, you can have multiple competing consumers listening on a single subscription, with each message handed off to only one of the consumers, thereby balancing load.
* Loose coupling – you can evolve the messaging network without affecting existing endpoints; for example, adding subscriptions or changing filters to a topic to allow for new consumers.

## <a name="next-steps"></a>Next steps

See [Create applications that use Service Bus queues](service-bus-create-queues.md) for information about how to use queues in the POS retail scenario.





