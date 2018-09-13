---
title: Azure Event Hubs samples | Microsoft Docs
description: Azure Event Hubs samples
services: event-hubs
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/07/2017
ms.author: jotaub;sethm
ms.openlocfilehash: 2eaf642d3d6617c8500aee283809209a5f31ef88
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555835"
---
# <a name="event-hubs-samples"></a><span data-ttu-id="4dfdf-103">Event Hubs samples</span><span class="sxs-lookup"><span data-stu-id="4dfdf-103">Event Hubs samples</span></span> 

<span data-ttu-id="4dfdf-104">The Azure Event Hubs samples demonstrate key features in [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="4dfdf-104">The Azure Event Hubs samples demonstrate key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="4dfdf-105">This article categorizes and describes the samples available, with links to each.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="4dfdf-106">At the time of this writing, Event Hubs samples are located in several different places:</span><span class="sxs-lookup"><span data-stu-id="4dfdf-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="4dfdf-107">MSDN developer code samples</span><span class="sxs-lookup"><span data-stu-id="4dfdf-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="4dfdf-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="4dfdf-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-dotnet/tree/master/samples)

<span data-ttu-id="4dfdf-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="4dfdf-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="4dfdf-110">More samples will be added over time, so check back here frequently for updates.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="4dfdf-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4dfdf-111">.NET Standard</span></span>

<span data-ttu-id="4dfdf-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="4dfdf-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="4dfdf-113">Send events</span><span class="sxs-lookup"><span data-stu-id="4dfdf-113">Send events</span></span> 

<span data-ttu-id="4dfdf-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="4dfdf-115">Receive events</span><span class="sxs-lookup"><span data-stu-id="4dfdf-115">Receive events</span></span> 

<span data-ttu-id="4dfdf-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the `Event Processor Host`.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the `Event Processor Host`.</span></span>

## <a name="net-framework"></a><span data-ttu-id="4dfdf-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4dfdf-117">.NET Framework</span></span>   

<span data-ttu-id="4dfdf-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](https://msdn.microsoft.com/library/w0x726c2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dfdf-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](https://msdn.microsoft.com/library/w0x726c2.aspx).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="4dfdf-119">Notify users of events received</span><span class="sxs-lookup"><span data-stu-id="4dfdf-119">Notify users of events received</span></span>

<span data-ttu-id="4dfdf-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="4dfdf-121">Get started with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4dfdf-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="4dfdf-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="4dfdf-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="4dfdf-123">Scale out event processing</span><span class="sxs-lookup"><span data-stu-id="4dfdf-123">Scale out event processing</span></span> 

<span data-ttu-id="4dfdf-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="4dfdf-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="4dfdf-126">Pull data from SQL into an event hub</span><span class="sxs-lookup"><span data-stu-id="4dfdf-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="4dfdf-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="4dfdf-128">Pull web data into an event hub</span><span class="sxs-lookup"><span data-stu-id="4dfdf-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="4dfdf-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span><span class="sxs-lookup"><span data-stu-id="4dfdf-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dfdf-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="4dfdf-130">Next steps</span></span>

<span data-ttu-id="4dfdf-131">Learn more about .NET Framework versions by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="4dfdf-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="4dfdf-132">Frameworks and Targets</span><span class="sxs-lookup"><span data-stu-id="4dfdf-132">Frameworks and Targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="4dfdf-133">.NET Framework 4.6 and 4.5</span><span class="sxs-lookup"><span data-stu-id="4dfdf-133">.NET Framework 4.6 and 4.5</span></span>](https://msdn.microsoft.com/library/w0x726c2.aspx)

<span data-ttu-id="4dfdf-134">You can learn more about Event Hubs in the following articles:</span><span class="sxs-lookup"><span data-stu-id="4dfdf-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="4dfdf-135">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="4dfdf-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="4dfdf-136">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="4dfdf-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="4dfdf-137">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="4dfdf-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)