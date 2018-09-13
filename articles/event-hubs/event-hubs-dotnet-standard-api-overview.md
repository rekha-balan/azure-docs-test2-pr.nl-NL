---
title: Overview of the Azure Event Hubs .NET Standard APIs | Microsoft Docs
description: .NET Standard API overview
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.topic: article
ms.date: 08/13/2018
ms.author: shvija
ms.openlocfilehash: 9b952bd96828c4f2c140cb2d75cecb9379895a63
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828802"
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="6745b-103">Event Hubs .NET Standard API overview</span><span class="sxs-lookup"><span data-stu-id="6745b-103">Event Hubs .NET Standard API overview</span></span>

<span data-ttu-id="6745b-104">This article summarizes some of the key Azure Event Hubs [.NET Standard client APIs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/).</span><span class="sxs-lookup"><span data-stu-id="6745b-104">This article summarizes some of the key Azure Event Hubs [.NET Standard client APIs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/).</span></span> <span data-ttu-id="6745b-105">There are currently two .NET Standard client libraries for Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="6745b-105">There are currently two .NET Standard client libraries for Event Hubs:</span></span>

* <span data-ttu-id="6745b-106">[Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs): Provides all basic runtime operations.</span><span class="sxs-lookup"><span data-stu-id="6745b-106">[Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs): Provides all basic runtime operations.</span></span>
* <span data-ttu-id="6745b-107">[Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor): Adds additional functionality that enables keeping track of processed events, and is the easiest way to read from an event hub.</span><span class="sxs-lookup"><span data-stu-id="6745b-107">[Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor): Adds additional functionality that enables keeping track of processed events, and is the easiest way to read from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="6745b-108">Event Hubs client</span><span class="sxs-lookup"><span data-stu-id="6745b-108">Event Hubs client</span></span>

<span data-ttu-id="6745b-109">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span><span class="sxs-lookup"><span data-stu-id="6745b-109">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span></span> <span data-ttu-id="6745b-110">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span><span class="sxs-lookup"><span data-stu-id="6745b-110">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="6745b-111">Create an Event Hubs client</span><span class="sxs-lookup"><span data-stu-id="6745b-111">Create an Event Hubs client</span></span>

<span data-ttu-id="6745b-112">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span><span class="sxs-lookup"><span data-stu-id="6745b-112">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="6745b-113">The simplest way to instantiate a new client is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="6745b-113">The simplest way to instantiate a new client is shown in the following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("Event Hubs connection string");
```

<span data-ttu-id="6745b-114">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="6745b-114">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("Event Hubs connection string")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="6745b-115">Send events</span><span class="sxs-lookup"><span data-stu-id="6745b-115">Send events</span></span>

<span data-ttu-id="6745b-116">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span><span class="sxs-lookup"><span data-stu-id="6745b-116">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="6745b-117">The body must be a `byte` array, or a `byte` array segment.</span><span class="sxs-lookup"><span data-stu-id="6745b-117">The body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="6745b-118">Receive events</span><span class="sxs-lookup"><span data-stu-id="6745b-118">Receive events</span></span>

<span data-ttu-id="6745b-119">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of the event hub offset and partition information.</span><span class="sxs-lookup"><span data-stu-id="6745b-119">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of the event hub offset and partition information.</span></span> <span data-ttu-id="6745b-120">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span><span class="sxs-lookup"><span data-stu-id="6745b-120">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="6745b-121">Create a receiver</span><span class="sxs-lookup"><span data-stu-id="6745b-121">Create a receiver</span></span>

<span data-ttu-id="6745b-122">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you must create multiple instances.</span><span class="sxs-lookup"><span data-stu-id="6745b-122">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you must create multiple instances.</span></span> <span data-ttu-id="6745b-123">It is a good practice to get the partition information programatically, rather than hard-coding the partition IDs.</span><span class="sxs-lookup"><span data-stu-id="6745b-123">It is a good practice to get the partition information programatically, rather than hard-coding the partition IDs.</span></span> <span data-ttu-id="6745b-124">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span><span class="sxs-lookup"><span data-stu-id="6745b-124">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition IDs
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

<span data-ttu-id="6745b-125">Because events are never removed from an event hub (and only expire), you must specify the proper starting point.</span><span class="sxs-lookup"><span data-stu-id="6745b-125">Because events are never removed from an event hub (and only expire), you must specify the proper starting point.</span></span> <span data-ttu-id="6745b-126">The following example shows possible combinations:</span><span class="sxs-lookup"><span data-stu-id="6745b-126">The following example shows possible combinations:</span></span>

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="6745b-127">Consume an event</span><span class="sxs-lookup"><span data-stu-id="6745b-127">Consume an event</span></span>

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

## <a name="event-processor-host-apis"></a><span data-ttu-id="6745b-128">Event Processor Host APIs</span><span class="sxs-lookup"><span data-stu-id="6745b-128">Event Processor Host APIs</span></span>

<span data-ttu-id="6745b-129">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers:</span><span class="sxs-lookup"><span data-stu-id="6745b-129">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers:</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
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

// Disposes the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="6745b-130">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor) interface:</span><span class="sxs-lookup"><span data-stu-id="6745b-130">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor) interface:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6745b-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="6745b-131">Next steps</span></span>

<span data-ttu-id="6745b-132">To learn more about Event Hubs scenarios, visit these links:</span><span class="sxs-lookup"><span data-stu-id="6745b-132">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="6745b-133">What is Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="6745b-133">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6745b-134">Available Event Hubs apis</span><span class="sxs-lookup"><span data-stu-id="6745b-134">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="6745b-135">The .NET API references are here:</span><span class="sxs-lookup"><span data-stu-id="6745b-135">The .NET API references are here:</span></span>

* [<span data-ttu-id="6745b-136">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="6745b-136">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="6745b-137">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="6745b-137">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)