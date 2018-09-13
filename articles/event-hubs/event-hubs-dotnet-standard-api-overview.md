---
title: Overview of the Azure Event Hubs .NET Standard APIs | Microsoft Docs
description: .NET Standard API overview
services: event-hubs
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: jotaub
ms.openlocfilehash: 4e05b1cc41038b2239f9314c17b93d20eed33844
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550209"
---
# <a name="event-hubs-net-standard-api-overview"></a>Event Hubs .NET Standard API overview
This article summarizes some of the key Event Hubs .NET Standard client APIs. There are currently two .NET Standard client libraries:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  This library provides all basic runtime operations.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * This library adds additional functionality that allows for keeping track of processed events, and is the easiest way to read from an event hub.

## <a name="event-hub-client"></a>Event Hub client
[**EventHubClient**](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get runtime information. This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.

### <a name="create-an-event-hub-client"></a>Create an event hub client
An [**EventHubClient**](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string. The simplest way to instantiate a new client is shown in the following example:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hub connection string}");
```

To programmatically edit the connection string, you can use the [**EventHubsConnectionStringBuilder**](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [**EventHubClient.CreateFromConnectionString**](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hub connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Send events
To send events to an event hub, use the [**EventData**](/dotnet/api/microsoft.azure.eventhubs.eventdata) class. The body must be a `byte` array, or a `byte` array segment.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Receive events
The recommended way to receive events from Event Hubs is using the [**EventProcessorHost**](##Event-Processor-Host-APIs), which provides functionality to automatically keep track of offset, and partition information. However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.

#### <a name="create-a-receiver"></a>Create a receiver
Receivers are tied to specific partitions, so in order to receive all events in an event hub, you will need to create multiple instances. Generally speaking, it is a good practice to get the partition information programatically, rather than hard-coding the partition ids. In order to do so, you can use the [**GetRuntimeInformationAsync**](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.

```csharp

// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

Since events are never removed from an event hub (and only expire), you will need to specify the proper starting point. The following example shows possible combinations.

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant 'PartitionReceiver.EndOfStream' will only receive all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Consume an event
```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a>Event Processor Host APIs
These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{Event Hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a>Next steps
To learn more about Event Hubs scenarios, visit these links:

* [What is Azure Event Hubs?](event-hubs-what-is-event-hubs.md)
* [Available Event Hubs apis](event-hubs-api-overview.md)

The .NET API references are here:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)