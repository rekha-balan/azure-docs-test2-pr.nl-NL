---
title: Availability and consistency in Azure Event Hubs | Microsoft Docs
description: How to provide the maximum amount of availability and consistency with Azure Event Hubs using partitions.
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: 9b4d992d690bb3237f8c92e44020c0ac83978d7e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804731"
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="e2e38-103">Availability and consistency in Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e2e38-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="e2e38-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e2e38-104">Overview</span></span>
<span data-ttu-id="e2e38-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span><span class="sxs-lookup"><span data-stu-id="e2e38-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="e2e38-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span><span class="sxs-lookup"><span data-stu-id="e2e38-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="e2e38-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span><span class="sxs-lookup"><span data-stu-id="e2e38-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="e2e38-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span><span class="sxs-lookup"><span data-stu-id="e2e38-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="e2e38-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span><span class="sxs-lookup"><span data-stu-id="e2e38-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="e2e38-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span><span class="sxs-lookup"><span data-stu-id="e2e38-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span> <span data-ttu-id="e2e38-111">It states that for the systems partitioned by network there is always tradeoff between consistency and availability.</span><span class="sxs-lookup"><span data-stu-id="e2e38-111">It states that for the systems partitioned by network there is always tradeoff between consistency and availability.</span></span>

<span data-ttu-id="e2e38-112">Brewer's theorem defines consistency and availability as follows:</span><span class="sxs-lookup"><span data-stu-id="e2e38-112">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="e2e38-113">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span><span class="sxs-lookup"><span data-stu-id="e2e38-113">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="e2e38-114">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span><span class="sxs-lookup"><span data-stu-id="e2e38-114">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="e2e38-115">Consistency: a read is guaranteed to return the most recent write for a given client.</span><span class="sxs-lookup"><span data-stu-id="e2e38-115">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="e2e38-116">Partition tolerance</span><span class="sxs-lookup"><span data-stu-id="e2e38-116">Partition tolerance</span></span>
<span data-ttu-id="e2e38-117">Event Hubs is built on top of a partitioned data model.</span><span class="sxs-lookup"><span data-stu-id="e2e38-117">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="e2e38-118">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span><span class="sxs-lookup"><span data-stu-id="e2e38-118">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="e2e38-119">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span><span class="sxs-lookup"><span data-stu-id="e2e38-119">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="e2e38-120">Availability</span><span class="sxs-lookup"><span data-stu-id="e2e38-120">Availability</span></span>
<span data-ttu-id="e2e38-121">The simplest way to get started with Event Hubs is to use the default behavior.</span><span class="sxs-lookup"><span data-stu-id="e2e38-121">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="e2e38-122">If you create a new **[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient)** object and use the **[Send](/dotnet/api/microsoft.azure.eventhubs.eventhubclient.sendasync?view=azure-dotnet#Microsoft_Azure_EventHubs_EventHubClient_SendAsync_Microsoft_Azure_EventHubs_EventData_)** method, your events are automatically distributed between partitions in your event hub.</span><span class="sxs-lookup"><span data-stu-id="e2e38-122">If you create a new **[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient)** object and use the **[Send](/dotnet/api/microsoft.azure.eventhubs.eventhubclient.sendasync?view=azure-dotnet#Microsoft_Azure_EventHubs_EventHubClient_SendAsync_Microsoft_Azure_EventHubs_EventData_)** method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="e2e38-123">This behavior allows for the greatest amount of up time.</span><span class="sxs-lookup"><span data-stu-id="e2e38-123">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="e2e38-124">For use cases that require the maximum up time, this model is preferred.</span><span class="sxs-lookup"><span data-stu-id="e2e38-124">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="e2e38-125">Consistency</span><span class="sxs-lookup"><span data-stu-id="e2e38-125">Consistency</span></span>
<span data-ttu-id="e2e38-126">In some scenarios, the ordering of events can be important.</span><span class="sxs-lookup"><span data-stu-id="e2e38-126">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="e2e38-127">For example, you may want your back-end system to process an update command before a delete command.</span><span class="sxs-lookup"><span data-stu-id="e2e38-127">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="e2e38-128">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span><span class="sxs-lookup"><span data-stu-id="e2e38-128">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="e2e38-129">Doing so ensures that when these events are read from the partition, they are read in order.</span><span class="sxs-lookup"><span data-stu-id="e2e38-129">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="e2e38-130">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span><span class="sxs-lookup"><span data-stu-id="e2e38-130">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="e2e38-131">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span><span class="sxs-lookup"><span data-stu-id="e2e38-131">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="e2e38-132">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span><span class="sxs-lookup"><span data-stu-id="e2e38-132">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="e2e38-133">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span><span class="sxs-lookup"><span data-stu-id="e2e38-133">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="e2e38-134">The following code shows an example:</span><span class="sxs-lookup"><span data-stu-id="e2e38-134">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="e2e38-135">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span><span class="sxs-lookup"><span data-stu-id="e2e38-135">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="e2e38-136">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span><span class="sxs-lookup"><span data-stu-id="e2e38-136">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2e38-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2e38-137">Next steps</span></span>
<span data-ttu-id="e2e38-138">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="e2e38-138">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="e2e38-139">Event Hubs service overview</span><span class="sxs-lookup"><span data-stu-id="e2e38-139">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e2e38-140">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="e2e38-140">Create an event hub</span></span>](event-hubs-create.md)
