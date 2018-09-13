---
title: What is Azure Event Hubs and why use it | Microsoft Docs
description: Overview and introduction to Azure Event Hubs - Cloud-scale telemetry ingestion from websites, apps, and devices
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: sethm; babanisa
ms.openlocfilehash: 7dad6a142201bed307b82e4215f036978919144b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662842"
---
# <a name="what-is-event-hubs"></a>What is Event Hubs?
Azure Event Hubs is a highly scalable data streaming platform capable of ingesting millions of events per second. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. With the ability to provide publish-subscribe capabilities with low latency and at massive scale, Event Hubs serves as the "on ramp" for Big Data.

## <a name="why-use-event-hubs"></a>Why use Event Hubs?
Event Hubs event and telemetry handling capabilities make it especially useful for:

* Application instrumentation
* User experience or workflow processing
* Internet of Things (IoT) scenarios

Event Hubs also enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines or connected vehicles.

## <a name="azure-event-hubs-overview"></a>Azure Event Hubs overview
The common role that Event Hubs plays in solution architectures is the "front door" for an event pipeline, often called an *event ingestor*. An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events. The following figure depicts this architecture:

![Event Hubs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Azure Event Hubs is an event processing service that provides cloud-scale event and telemetry ingestion, with low latency and high reliability. Event Hubs provides a message stream handling capability and has characteristics that are different from traditional enterprise messaging. Event Hubs capabilities are built around high throughput and event processing scenarios. As such, Event Hubs does not implement some of the messaging capabilities that are available for messaging entities, such as topics.

An event hub is created at the namespace level, and uses AMQP and HTTP as its primary API interfaces.

## <a name="event-publishers"></a>Event publishers
Any entity that sends data to an event hub is an *event publisher*. Event publishers can publish events using HTTPS or AMQP 1.0. Event publishers use a Shared Access Signature (SAS) token to identify themselves to an event hub, and can have a unique identity, or use a common SAS token.

### <a name="publishing-an-event"></a>Publishing an event
You can publish an event via AMQP 1.0 or HTTPS. Service Bus provides an [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) class for publishing events to an event hub from .NET clients. For other runtimes and platforms, you can use any AMQP 1.0 client, such as [Apache Qpid](http://qpid.apache.org/). You can publish events individually, or batched. A single publication (event data instance) has a limit of 256 KB, regardless of whether it is a single event or a batch. Publishing events larger than this results in an error. It is a best practice for publishers to be unaware of partitions within the event hub and to only specify a *partition key* (introduced in the next section), or their identity via their SAS token.

The choice to use AMQP or HTTPS is specific to the usage scenario. AMQP requires the establishment of a persistent bidirectional socket in addition to transport level security (TLS) or SSL/TLS. AMQP has higher network costs when initializing the session, however HTTPS requires additional SSL overhead for every request. AMQP has higher performance for frequent publishers.

![Event Hubs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-what-is-event-hubs/partition_keys.png)

Event Hubs ensures that all events sharing a partition key value are delivered in order, and to the same partition. If partition keys are used with publisher policies, then the identity of the publisher and the value of the partition key must match. Otherwise, an error occurs.

### <a name="publisher-policy"></a>Publisher policy
Event Hubs enables granular control over event publishers through *publisher policies*. Publisher policies are run-time features designed to facilitate large numbers of independent event publishers. With publisher policies, each publisher uses its own unique identifier when publishing events to an event hub, using the following mechanism:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

You don't have to create publisher names ahead of time, but they must match the SAS token used when publishing an event, in order to ensure independent publisher identities. When using publisher policies, the **PartitionKey** value is set to the publisher name. To work properly, these values must match.

## <a name="partitions"></a>Partitions
Event Hubs provides message streaming through a partitioned consumer pattern in which each consumer only reads a specific subset, or partition, of the message stream. This pattern enables horizontal scale for event processing and provides other stream-focused features that are unavailable in queues and topics.

A partition is an ordered sequence of events that is held in an event hub. As newer events arrive, they are added to the end of this sequence. A partition can be thought of as a "commit log."

![Event Hubs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-what-is-event-hubs/partition.png)

Event Hubs retain data for a configured retention time that applies across all partitions in the event hub. Events expire on a time basis; you cannot explicitly delete them. Because partitions are independent and contain their own sequence of data, they often grow at different rates.

![Event Hubs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-what-is-event-hubs/multiple_partitions.png)

The number of partitions is specified at creation and must be between 2 and 32. The partition count is not changeable, so you should consider long-term scale when setting partition count. Partitions are a data organization mechanism that relates to the downstream parallelism required in consuming applications. The number of partitions in an event hub directly relates to the number of concurrent readers you expect to have. You can increase the number of partitions beyond 32 by contacting the Event Hubs team.

While partitions are identifiable and can be sent to directly, this is not recommended. Instead, you can use higher level constructs introduced in the [Event publisher](#event-publishers) and [Capacity](#capacity) sections. 

Partitions are filled with a sequence of event data which contains the body of the event, a user-defined property bag, and metadata such as its offset in the partition and its number in the stream sequence.

For more information about partitions and the trade-off between availability and reliability, see the [Event Hubs programming guide](event-hubs-programming-guide.md#partition-key) and the [Availability and consistency in Event Hubs](event-hubs-availability-and-consistency.md) article.

### <a name="partition-key"></a>Partition key
You can use a [partition key](event-hubs-programming-guide.md#partition-key) to map incoming event data into specific partitions for the purpose of data organization. The partition key is a sender-supplied value passed into an event hub. It is processed through a static hashing function, which creates the partition assignment. If you don't specify a partition key when publishing an event, a round-robin assignment is used.

The event publisher is only aware of its partition key, not the partition to which the events are published. This decoupling of key and partition insulates the sender from needing to know too much about the downstream processing. A per-device or user unique identity makes a good partition key, but other attributes such as geography can also be used to group related events into a single partition.

## <a name="sas-tokens"></a>SAS tokens
Event Hubs uses *Shared Access Signatures*, which are available at the namespace and event hub level. A SAS token is generated from a SAS key and is an SHA hash of a URL, encoded in a specific format. Using the name of the key (policy) and the token, Event Hubs can regenerate the hash and thus authenticate the sender. Normally, SAS tokens for event publishers are created with only **send** privileges on a specific event hub. This SAS token URL mechanism is the basis for publisher identification introduced in the publisher policy. For more information about working with SAS, see [Shared Access Signature Authentication with Service Bus](../service-bus-messaging/service-bus-sas.md).

## <a name="event-consumers"></a>Event consumers
Any entity that reads event data from an event hub is an *event consumer*. All Event Hubs consumers connect via the AMQP 1.0 session and events are delivered through the session as they become available. The client does not need to poll for data availability.

### <a name="consumer-groups"></a>Consumer groups
The publish/subscribe mechanism of Event Hubs is enabled through *consumer groups*. A consumer group is a view (state, position, or offset) of an entire event hub. Consumer groups enable multiple consuming applications to each have a separate view of the event stream, and to read the stream independently at their own pace and with their own offsets.

In a stream processing architecture, each downstream application equates to a consumer group. If you want to write event data to long-term storage, then that storage writer application is a consumer group. Complex event processing can then be performed by another, separate consumer group. You can only access partitions through a consumer group. Each partition can only have one active reader **from a given consumer group** at a time. There is always a default consumer group in an event hub, and you can create up to 20 consumer groups for a Standard tier event hub.

The following are examples of the consumer group URI convention:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

The following figure shows the Event Hubs stream processing architecture:

![Event Hubs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-what-is-event-hubs/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Stream offsets
An *offset* is the position of an event within a partition. You can think of an offset as a client-side cursor. The offset is a byte numbering of the event. This offset enables an event consumer (reader) to specify a point in the event stream from which they want to begin reading events. You can specify the offset as a timestamp or as an offset value. Consumers are responsible for storing their own offset values outside of the Event Hubs service. Within a partition, each event includes an offset.

![Event Hubs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-what-is-event-hubs/partition_offset.png)

### <a name="checkpointing"></a>Checkpointing
*Checkpointing* is a process by which readers mark or commit their position within a partition event sequence. Checkpointing is the responsibility of the consumer and occurs on a per-partition basis within a consumer group. This responsibility means that for each consumer group, each partition reader must keep track of its current position in the event stream, and can inform the service when it considers the data stream complete.

If a reader disconnects from a partition, when it reconnects it begins reading at the checkpoint that was previously submitted by the last reader of that partition in that consumer group. When the reader connects, it passes this offset to the event hub to specify the location at which to start reading. In this way, you can use checkpointing to both mark events as "complete" by downstream applications, and to provide resiliency if a failover between readers running on different machines occurs. It is possible to return to older data by specifying a lower offset from this checkpointing process. Through this mechanism, checkpointing enables both failover resiliency and event stream replay.

### <a name="common-consumer-tasks"></a>Common consumer tasks
All Event Hubs consumers connect via an AMQP 1.0 session and state-aware bidirectional communication channel. Each partition has an AMQP 1.0 session that facilitates the transport of events segregated by partition.

#### <a name="connect-to-a-partition"></a>Connect to a partition
When connecting to partitions, it is common practice to use a leasing mechanism to coordinate reader connections to specific partitions. This way, it is possible for every partition in a consumer group to have only one active reader. Checkpointing, leasing, and managing readers are simplified by using the [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) class for .NET clients. The Event Processor Host is an intelligent consumer agent.

#### <a name="read-events"></a>Read events
After an AMQP 1.0 session and link is opened for a specific partition, events are delivered to the AMQP 1.0 client by the Event Hubs service. This delivery mechanism enables higher throughput and lower latency than pull-based mechanisms such as HTTP GET. As events are sent to the client, each event data instance contains important metadata such as the offset and sequence number that are used to facilitate checkpointing on the event sequence.

Event data:
* Offset
* Sequence number
* Body
* User properties
* System properties

It is your responsibility to manage the offset.

## <a name="capacity"></a>Capacity
Event Hubs has a highly scalable parallel architecture and there are several key factors to consider when sizing and scaling.

### <a name="throughput-units"></a>Throughput units
The throughput capacity of Event Hubs is controlled by *throughput units*. Throughput units are pre-purchased units of capacity. A single throughput unit includes the following capacity:

* Ingress: Up to 1 MB per second or 1000 events per second (whichever comes first)
* Egress: Up to 2 MB per second

Beyond the capacity of the purchased throughput units, ingress is throttled and a [ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) is returned. Egress does not produce throttling exceptions, but is still limited to the capacity of the purchased throughput units. If you receive publishing rate exceptions or are expecting to see higher egress, be sure to check how many throughput units you have purchased for the namespace. You can manage throughput units on the **Scale** blade of the namespaces in the [Azure portal][Azure portal]. You can also manage throughput units programmatically using the Azure APIs.

Throughput units are billed per hour and are pre-purchased. Once purchased, throughput units are billed for a minimum of one hour. Up to 20 throughput units can be purchased for an Event Hubs namespace and are shared across all Event Hubs in the namespace.

More throughput units can be purchased in blocks of 20, up to 100 throughput units, by contacting Azure support. Beyond that, you can also purchase blocks of 100 throughput units.

It is recommended that you balance throughput units and partitions to achieve optimal scale. A single partition has a maximum scale of one throughput unit. The number of throughput units should be less than or equal to the number of partitions in an event hub.

For detailed pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Next steps

* Get started with an [Event Hubs tutorial][Event Hubs tutorial]
* [Event Hubs programming guide](event-hubs-programming-guide.md)
* [Availability and consistency in Event Hubs](event-hubs-availability-and-consistency.md)
* [Event Hubs FAQ](event-hubs-faq.md)
* [Sample applications that use Event Hubs]

[Event Hubs tutorial]: event-hubs-csharp-ephcs-getstarted.md
[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Azure portal]: https://portal.azure.com






