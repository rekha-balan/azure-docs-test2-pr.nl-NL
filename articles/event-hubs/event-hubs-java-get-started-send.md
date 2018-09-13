---
title: Send events to Azure Event Hubs using Java | Microsoft Docs
description: Get started sending to Event Hubs using Java
services: event-hubs
documentationcenter: ''
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jotaub;sethm
ms.openlocfilehash: fe10aaca3232e5baa0b726b7262a6e9e8ce6b638
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550217"
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="26767-103">Send events to Azure Event Hubs using Java</span><span class="sxs-lookup"><span data-stu-id="26767-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="26767-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="26767-104">Introduction</span></span>
<span data-ttu-id="26767-105">Event Hubs is a highly scalable ingestion system that can intake millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="26767-105">Event Hubs is a highly scalable ingestion system that can intake millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="26767-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span><span class="sxs-lookup"><span data-stu-id="26767-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="26767-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="26767-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="26767-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span><span class="sxs-lookup"><span data-stu-id="26767-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="26767-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span><span class="sxs-lookup"><span data-stu-id="26767-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="26767-110">In order to complete this tutorial, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="26767-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="26767-111">A Java development environment.</span><span class="sxs-lookup"><span data-stu-id="26767-111">A Java development environment.</span></span> <span data-ttu-id="26767-112">For this tutorial, we will assume [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="26767-112">For this tutorial, we will assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="26767-113">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="26767-113">An active Azure account.</span></span> <br/><span data-ttu-id="26767-114">If you don't have an account, you can create a free account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="26767-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="26767-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span><span class="sxs-lookup"><span data-stu-id="26767-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="26767-116">Send messages to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="26767-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="26767-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22), and can be referenced using the following dependency declaration inside your Maven project file:</span><span class="sxs-lookup"><span data-stu-id="26767-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22), and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

``` XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="26767-118">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="26767-118">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

<span data-ttu-id="26767-119">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span><span class="sxs-lookup"><span data-stu-id="26767-119">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="26767-120">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span><span class="sxs-lookup"><span data-stu-id="26767-120">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="26767-121">The class will be called ```Send```.</span><span class="sxs-lookup"><span data-stu-id="26767-121">The class will be called ```Send```.</span></span>     

``` Java

import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

<span data-ttu-id="26767-122">Replace the namespace and event hub names with the values used when you created the event hub.</span><span class="sxs-lookup"><span data-stu-id="26767-122">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

``` Java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="26767-123">Then, create a singular event by turning a string into its UTF-8 byte encoding.</span><span class="sxs-lookup"><span data-stu-id="26767-123">Then, create a singular event by turning a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="26767-124">We then create a new Event Hubs client instance from the connection string and send the message.</span><span class="sxs-lookup"><span data-stu-id="26767-124">We then create a new Event Hubs client instance from the connection string and send the message.</span></span>   

``` Java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md

## <a name="next-steps"></a><span data-ttu-id="26767-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="26767-125">Next steps</span></span>
<span data-ttu-id="26767-126">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="26767-126">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="26767-127">Receive events using the EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="26767-127">Receive events using the EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* [<span data-ttu-id="26767-128">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="26767-128">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="26767-129">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="26767-129">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="26767-130">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="26767-130">Event Hubs FAQ</span></span>](event-hubs-faq.md)