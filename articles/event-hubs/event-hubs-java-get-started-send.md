---
title: Send events to Azure Event Hubs using Java | Microsoft Docs
description: Get started sending to Event Hubs using Java
services: event-hubs
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 08/27/2018
ms.author: shvija
ms.openlocfilehash: f67982eda60a8fdfdf0d50785827c513275fd202
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811955"
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="e0bd8-103">Send events to Azure Event Hubs using Java</span><span class="sxs-lookup"><span data-stu-id="e0bd8-103">Send events to Azure Event Hubs using Java</span></span>

<span data-ttu-id="e0bd8-104">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-104">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="e0bd8-105">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-105">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="e0bd8-106">For more information, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="e0bd8-106">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="e0bd8-107">This tutorial shows how to send events to an event hub by using a console application in Java.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-107">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="e0bd8-108">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-108">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0bd8-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0bd8-109">Prerequisites</span></span>

<span data-ttu-id="e0bd8-110">In order to complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="e0bd8-111">A Java development environment.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-111">A Java development environment.</span></span> <span data-ttu-id="e0bd8-112">This tutorial uses [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-112">This tutorial uses [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="e0bd8-113">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-113">An active Azure account.</span></span> <span data-ttu-id="e0bd8-114">If you do not have an Azure subscription, create a [free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-114">If you do not have an Azure subscription, create a [free account][] before you begin.</span></span>

<span data-ttu-id="e0bd8-115">The code in this tutorial is based on the [SimpleSend GitHub sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/Java/Basic/SimpleSend), which you can examine to see the full working application.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-115">The code in this tutorial is based on the [SimpleSend GitHub sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/Java/Basic/SimpleSend), which you can examine to see the full working application.</span></span>

## <a name="send-events-to-event-hubs"></a><span data-ttu-id="e0bd8-116">Send events to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e0bd8-116">Send events to Event Hubs</span></span>

<span data-ttu-id="e0bd8-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="e0bd8-118">You can reference this library using the following dependency declaration inside your Maven project file.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-118">You can reference this library using the following dependency declaration inside your Maven project file.</span></span> <span data-ttu-id="e0bd8-119">The current version is 1.0.2:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-119">The current version is 1.0.2:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>1.0.2</version>
</dependency>
```

<span data-ttu-id="e0bd8-120">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="e0bd8-120">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="e0bd8-121">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-121">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

### <a name="declare-the-send-class"></a><span data-ttu-id="e0bd8-122">Declare the Send class</span><span class="sxs-lookup"><span data-stu-id="e0bd8-122">Declare the Send class</span></span>

<span data-ttu-id="e0bd8-123">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-123">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="e0bd8-124">Name the class `SimpleSend`:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-124">Name the class `SimpleSend`:</span></span>     

```java
package com.microsoft.azure.eventhubs.samples.send;

import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.microsoft.azure.eventhubs.ConnectionStringBuilder;
import com.microsoft.azure.eventhubs.EventData;
import com.microsoft.azure.eventhubs.EventHubClient;
import com.microsoft.azure.eventhubs.EventHubException;

import java.io.IOException;
import java.nio.charset.Charset;
import java.time.Instant;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;

public class SimpleSend {

    public static void main(String[] args)
            throws EventHubException, ExecutionException, InterruptedException, IOException {
            
            
    }
 }
```

### <a name="construct-connection-string"></a><span data-ttu-id="e0bd8-125">Construct connection string</span><span class="sxs-lookup"><span data-stu-id="e0bd8-125">Construct connection string</span></span>

<span data-ttu-id="e0bd8-126">Use the ConnectionStringBuilder class to construct a connection string value to pass to the Event Hubs client instance.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-126">Use the ConnectionStringBuilder class to construct a connection string value to pass to the Event Hubs client instance.</span></span> <span data-ttu-id="e0bd8-127">Replace the placeholders with the values you obtained when you created the namespace and event hub:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-127">Replace the placeholders with the values you obtained when you created the namespace and event hub:</span></span>

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
        .setNamespaceName("Your Event Hubs namespace name")
        .setEventHubName("Your event hub")
        .setSasKeyName("Your policy name")
        .setSasKey("Your primary SAS key");
```

### <a name="send-events"></a><span data-ttu-id="e0bd8-128">Send events</span><span class="sxs-lookup"><span data-stu-id="e0bd8-128">Send events</span></span>

<span data-ttu-id="e0bd8-129">Create a singular event by transforming a string into its UTF-8 byte encoding.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-129">Create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="e0bd8-130">Then, create a new Event Hubs client instance from the connection string and send the message:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-130">Then, create a new Event Hubs client instance from the connection string and send the message:</span></span>   

```java 
String payload = "Message " + Integer.toString(i);
byte[] payloadBytes = gson.toJson(payload).getBytes(Charset.defaultCharset());
EventData sendEvent = EventData.create(payloadBytes);

final EventHubClient ehClient = EventHubClient.createSync(connStr.toString(), executorService);
ehClient.sendSync(sendEvent);
    
// close the client at the end of your program
ehClient.closeSync();

``` 

### <a name="how-messages-are-routed-to-eventhub-partitions"></a><span data-ttu-id="e0bd8-131">How messages are routed to EventHub partitions</span><span class="sxs-lookup"><span data-stu-id="e0bd8-131">How messages are routed to EventHub partitions</span></span>

<span data-ttu-id="e0bd8-132">Before messages are retrieved by consumers, they have to be published to the partitions first by the publishers.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-132">Before messages are retrieved by consumers, they have to be published to the partitions first by the publishers.</span></span> <span data-ttu-id="e0bd8-133">When messages are published to event hub synchronously using the sendSync() method on the com.microsoft.azure.eventhubs.EventHubClient object, the message could be sent to a specific partition or distributed to all available partitions in a round-robin manner depending on whether the partition key is specified or not.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-133">When messages are published to event hub synchronously using the sendSync() method on the com.microsoft.azure.eventhubs.EventHubClient object, the message could be sent to a specific partition or distributed to all available partitions in a round-robin manner depending on whether the partition key is specified or not.</span></span>

<span data-ttu-id="e0bd8-134">When a string representing the partition key is specified, the key will be hashed to determine which partition to send the event to.</span><span class="sxs-lookup"><span data-stu-id="e0bd8-134">When a string representing the partition key is specified, the key will be hashed to determine which partition to send the event to.</span></span>

<span data-ttu-id="e0bd8-135">When the partition key is not set, then messages will round-robined to all available partitions</span><span class="sxs-lookup"><span data-stu-id="e0bd8-135">When the partition key is not set, then messages will round-robined to all available partitions</span></span>

```java
// Serialize the event into bytes
byte[] payloadBytes = gson.toJson(messagePayload).getBytes(Charset.defaultCharset());

// Use the bytes to construct an {@link EventData} object
EventData sendEvent = EventData.create(payloadBytes);

// Transmits the event to event hub without a partition key
// If a partition key is not set, then we will round-robin to all topic partitions
eventHubClient.sendSync(sendEvent);

//  the partitionKey will be hash'ed to determine the partitionId to send the eventData to.
eventHubClient.sendSync(sendEvent, partitionKey);

// close the client at the end of your program
eventHubClient.closeSync();

```

## <a name="next-steps"></a><span data-ttu-id="e0bd8-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0bd8-136">Next steps</span></span>

<span data-ttu-id="e0bd8-137">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="e0bd8-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="e0bd8-138">Receive events using the EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e0bd8-138">Receive events using the EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="e0bd8-139">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="e0bd8-139">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="e0bd8-140">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="e0bd8-140">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="e0bd8-141">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="e0bd8-141">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio

