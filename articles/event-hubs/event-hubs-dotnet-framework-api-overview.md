---
title: Overview of the Azure Event Hubs .NET Framework APIs | Microsoft Docs
description: A summary of some of the key Event Hubs .NET Framework client APIs.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: jotaub;sethm
ms.openlocfilehash: e6251a44a77267d0b64b0752dbe664786e6bb157
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563245"
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="2b951-103">Event Hubs .NET Framework API overview</span><span class="sxs-lookup"><span data-stu-id="2b951-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="2b951-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span><span class="sxs-lookup"><span data-stu-id="2b951-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="2b951-105">There are two categories: management and run-time APIs.</span><span class="sxs-lookup"><span data-stu-id="2b951-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="2b951-106">Run-time APIs consist of all operations needed to send and receive a message.</span><span class="sxs-lookup"><span data-stu-id="2b951-106">Run-time APIs consist of all operations needed to send and receive a message.</span></span> <span data-ttu-id="2b951-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span><span class="sxs-lookup"><span data-stu-id="2b951-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="2b951-108">Monitoring scenarios span both management and run-time.</span><span class="sxs-lookup"><span data-stu-id="2b951-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="2b951-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api) and [EventProcessorHost API](/dotnet/api) references.</span><span class="sxs-lookup"><span data-stu-id="2b951-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api) and [EventProcessorHost API](/dotnet/api) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="2b951-110">Management APIs</span><span class="sxs-lookup"><span data-stu-id="2b951-110">Management APIs</span></span>
<span data-ttu-id="2b951-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span><span class="sxs-lookup"><span data-stu-id="2b951-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="2b951-112">Create</span><span class="sxs-lookup"><span data-stu-id="2b951-112">Create</span></span>
```csharp
// Create the event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="2b951-113">Update</span><span class="sxs-lookup"><span data-stu-id="2b951-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="2b951-114">Delete</span><span class="sxs-lookup"><span data-stu-id="2b951-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="2b951-115">Run-time APIs</span><span class="sxs-lookup"><span data-stu-id="2b951-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="2b951-116">Create publisher</span><span class="sxs-lookup"><span data-stu-id="2b951-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="2b951-117">Publish message</span><span class="sxs-lookup"><span data-stu-id="2b951-117">Publish message</span></span>
```csharp
// Create the device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="2b951-118">Create consumer</span><span class="sxs-lookup"><span data-stu-id="2b951-118">Create consumer</span></span>
```csharp
// Create the Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get the default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="2b951-119">Consume message</span><span class="sxs-lookup"><span data-stu-id="2b951-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="2b951-120">Event Processor Host APIs</span><span class="sxs-lookup"><span data-stu-id="2b951-120">Event Processor Host APIs</span></span>
<span data-ttu-id="2b951-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span><span class="sxs-lookup"><span data-stu-id="2b951-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use the EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// To close
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="2b951-122">The [IEventProcessor](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="2b951-122">The [IEventProcessor](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2b951-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b951-123">Next steps</span></span>
<span data-ttu-id="2b951-124">To learn more about Event Hubs scenarios, visit these links:</span><span class="sxs-lookup"><span data-stu-id="2b951-124">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="2b951-125">What is Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="2b951-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2b951-126">Event Hubs programming guide</span><span class="sxs-lookup"><span data-stu-id="2b951-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="2b951-127">The .NET API references are here:</span><span class="sxs-lookup"><span data-stu-id="2b951-127">The .NET API references are here:</span></span>

* [<span data-ttu-id="2b951-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="2b951-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="2b951-129">Microsoft.Azure.ServiceBus.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="2b951-129">Microsoft.Azure.ServiceBus.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.servicebus.eventprocessorhost)
