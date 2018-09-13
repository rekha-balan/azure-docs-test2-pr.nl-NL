---
title: Service Bus messaging samples overview | Microsoft Docs
description: Categorizes and describes Service Bus messaging samples with links to each.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 0b420343-2d2a-4c65-98f1-ee0e39ef55c8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/07/2016
ms.author: sethm
ms.openlocfilehash: c14f6d93d680808b9152f139c5276cb4c9bec747
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671064"
---
# <a name="service-bus-messaging-samples"></a>Service Bus messaging samples
The Service Bus messaging samples demonstrate key features in [Service Bus messaging](https://azure.microsoft.com/services/service-bus/) (cloud service) and [Service Bus for Windows Server](https://msdn.microsoft.com/library/dn282144.aspx). This article categorizes and describes the samples available, with links to each.

> [!NOTE]
> Service Bus samples are not installed with the SDK. To obtain the samples, visit the [Azure SDK samples page](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5).
> 
> Additionally, there is an updated set of Service Bus messaging samples [here](https://github.com/Azure-Samples/azure-servicebus-messaging-samples) (as of this writing, they are not described in this article).  
> 
> 

For relay samples, see [Service Bus relay samples](../service-bus-relay/service-bus-relay-samples.md).

## <a name="service-bus-messaging"></a>Service Bus messaging
The following samples illustrate how to write applications that use Service Bus messaging.

Note that the messaging samples require a connection string to access your Service Bus namespace.

### <a name="to-obtain-a-connection-string-for-azure-service-bus"></a>To obtain a connection string for Azure Service Bus
1. Log on to the [Azure portal](http://portal.azure.com).
2. In the left-hand column, click **Service Bus**.
3. Click the name of your namespace in the list.
4. In the namespace blade, click **Shared access policies**.
5. In the **Shared access policies** blade, click **RootManageSharedAccessKey**.
6. Copy the connection string to the clipboard.

### <a name="to-obtain-a-connection-string-for-service-bus-for-windows-server"></a>To obtain a connection string for Service Bus for Windows Server
1. Run the following PowerShell cmdlet:
   
    ```
    get-sbClientConfiguration
    ```
2. Paste the connection string into the App.config file for the sample.

### <a name="getting-started-samples"></a>Getting started samples
These samples describe basic messaging functionality.

| Sample Name | Description | Minimum SDK Version | Availability |
| --- | --- | --- | --- |
| [Getting Started: Messaging with Queues](http://code.msdn.microsoft.com/Getting-Started-Brokered-aa7a0ac3) |Demonstrates how to use Microsoft Azure Service Bus to send and receive messages from a queue. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Getting Started: Messaging With Topics](http://code.msdn.microsoft.com/Getting-Started-Brokered-614d42e5) |Demonstrates how to use Microsoft Azure Service Bus to send and receive messages from a topic with multiple subscriptions. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |

### <a name="exploring-features"></a>Exploring features
The following samples demonstrate various features of Service Bus.

| Sample Name | Description | Minimum SDK Version | Availability |
| --- | --- | --- | --- |
| [HTTP Token Providers](http://code.msdn.microsoft.com/Service-Bus-HTTP-Token-38f2cfc5) |Demonstrates the different ways of authenticating an HTTP/REST client with Service Bus. |2.1 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Service Bus HTTP Client](http://code.msdn.microsoft.com/Service-Bus-HTTP-client-fe7da74a) |Demonstrates how to send messages to and receive messages from Service Bus via HTTP/REST. |2.3 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Service Bus Autoforwarding](http://code.msdn.microsoft.com/Service-Bus-Autoforwarding-b9df470b) |Demonstrates how to automatically forward messages from a queue, subscription, or deadletter queue into another queue or topic. It also demonstrates how to send a message into a queue or topic via a transfer queue. |2.3 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: WCF Channel Session Sample](http://code.msdn.microsoft.com/Brokered-Messaging-WCF-0a526451) |Demonstrates how to use Microsoft Azure Service Bus using Windows Communication Foundation (WCF) channels. The sample shows the use of WCF channels to send and receive messages via a Service Bus queue. The sample shows both session and non-session communication over the Service Bus. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Transactions](http://code.msdn.microsoft.com/Brokered-Messaging-8cd41d1e) |Demonstrates how to use the Microsoft Azure Service Bus messaging features within a transaction scope in order to ensure batches of messaging operations are committed atomically. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Management Operations Using REST](http://code.msdn.microsoft.com/Brokered-Messaging-569cff88) |Demonstrates how to perform management operations on Service Bus using REST. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Resource Provider REST APIs](http://code.msdn.microsoft.com/Service-Bus-Resource-5d887203) |Demonstrates how to use the new Service Bus RDFE REST APIs to manage namespaces and messaging entities. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: WCF Service Session Sample](http://code.msdn.microsoft.com/Brokered-Messaging-WCF-db4262c2) |Demonstrates how to use Microsoft Azure Service Bus using the WCF service model. The sample shows the use of the WCF service model to accomplish session-based communication via a Service Bus queue. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Request Response](http://code.msdn.microsoft.com/Brokered-Messaging-Request-2b4ff5d8) |Demonstrates how to use the Microsoft Azure Service Bus and the request/response functionality. The sample shows simple clients and servers communicating via a Service Bus queue. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Dead Letter Queue](http://code.msdn.microsoft.com/Brokered-Messaging-Dead-22536dd8) |Demonstrates how to use Microsoft Azure Service Bus and the messaging "dead letter queue" functionality. The sample shows a simple sender and receiver communicating via a Service Bus queue. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Deferred Messages](http://code.msdn.microsoft.com/Brokered-Messaging-ccc4f879) |Demonstrates how to use the message deferral feature of Microsoft Azure Service Bus. The sample shows a simple sender and receiver communicating via a Service Bus queue. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Session Messages](http://code.msdn.microsoft.com/Brokered-Messaging-Session-41c43fb4) |Demonstrates how to use Microsoft Azure Service Bus and the Messaging Session functionality. The sample shows simple senders and receivers communicating via a Service Bus queue. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Request Response Topic](http://code.msdn.microsoft.com/Brokered-Messaging-Request-6759a36e) |Demonstrates how to implement the request/response pattern using Microsoft Azure Service Bus topics and subscriptions. The sample shows simple clients and servers communicating via a Service Bus topic. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Request Response Queue](http://code.msdn.microsoft.com/Brokered-Messaging-Request-0ce8fcaf) |Demonstrates how to use Microsoft Azure Service Bus and the request/response functionality. The sample shows simple clients and servers communicating via two Service Bus queues. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Duplicate Detection](http://code.msdn.microsoft.com/Brokered-Messaging-c0acea25) |Demonstrates how to use Microsoft Azure Service Bus duplicate message detection with queues. It creates two queues, one with duplicate detection enabled and other one without duplicate detection. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Async Messaging](http://code.msdn.microsoft.com/Brokered-Messaging-Async-211c1e74) |Demonstrates how to use Microsoft Azure Service Bus to send and receive messages asynchronously from a queue. The queue provides decoupled, asynchronous communication between a sender and any number of receivers (here, a single receiver). |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) |Demonstrates how to use Microsoft Azure Service Bus publish/subscribe advanced filters. It creates a topic and 3 subscriptions with different filter definitions, sends messages to the topic, and receives all messages from subscriptions. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Brokered Messaging: Messages Prefetch](http://code.msdn.microsoft.com/Brokered-Messaging-be2dac1d) |Demonstrates how to use the Microsoft Azure Service Bus messages prefetch feature. It demonstrates how to use the messages prefetch feature upon receive. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |

## <a name="service-bus-reference-tools"></a>Service Bus reference tools
The following samples demonstrate various other features of the service.

| Sample Name | Description | Minimum SDK Version | Availability |
| --- | --- | --- | --- |
| [Service Bus Explorer](http://code.msdn.microsoft.com/Service-Bus-Explorer-f2abca5a) |The Service Bus Explorer allows users to connect to a Service Bus service namespace and manage messaging entities in an easy manner. The tool provides advanced features such as import/export functionality, and the ability to test messaging entities and relay services. |1.8 |Microsoft Azure Service Bus; Service Bus for Windows Server |
| [Authorization: SBAzTool](http://code.msdn.microsoft.com/Authorization-SBAzTool-6fd76d93) |This sample demonstrates how to create and manage service identities in Microsoft Azure Active Directory Access Control (also known as Access Control Service or ACS) for use with Service Bus. |N/A |Microsoft Azure Service Bus |

## <a name="next-steps"></a>Next steps
See the following topics for conceptual overviews of Service Bus.

* [Service Bus messaging overview](service-bus-messaging-overview.md)
* [Service Bus architecture](service-bus-architecture.md)
* [Service Bus fundamentals](service-bus-fundamentals-hybrid-solutions.md)

