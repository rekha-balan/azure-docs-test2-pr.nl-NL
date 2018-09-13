---
title: Receive events from Azure Event Hubs using the .NET Framework | Microsoft Docs
description: Follow this tutorial to receive events from Azure Event Hubs using the .NET Framework.
services: event-hubs
documentationcenter: ''
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: jotaub;sethm
ms.openlocfilehash: 35e03e499c0da5f72f64d0aeb4e1ae93dba5aa38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554063"
---
# <a name="receive-events-from-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="6a7a7-103">Receive events from Azure Event Hubs using the .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6a7a7-103">Receive events from Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="6a7a7-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="6a7a7-104">Introduction</span></span>
<span data-ttu-id="6a7a7-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="6a7a7-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="6a7a7-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span><span class="sxs-lookup"><span data-stu-id="6a7a7-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="6a7a7-108">This tutorial shows how to write a .NET Framework console application that receives messages from an event hub using the **[Event Processor Host][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-108">This tutorial shows how to write a .NET Framework console application that receives messages from an event hub using the **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="6a7a7-109">To send events using the .NET Framework, see the [Send events to Azure Event Hubs using the .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click the appropriate sending language in the left-hand table of contents.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-109">To send events using the .NET Framework, see the [Send events to Azure Event Hubs using the .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click the appropriate sending language in the left-hand table of contents.</span></span>

<span data-ttu-id="6a7a7-110">The [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-110">The [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="6a7a7-111">Using the [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-111">Using the [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="6a7a7-112">This example shows how to use the [Event Processor Host][EventProcessorHost] for a single receiver.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-112">This example shows how to use the [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="6a7a7-113">The [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how to use the [Event Processor Host][EventProcessorHost] with multiple receivers.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-113">The [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how to use the [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a7a7-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a7a7-114">Prerequisites</span></span>

<span data-ttu-id="6a7a7-115">To complete this tutorial, you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="6a7a7-115">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="6a7a7-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6a7a7-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="6a7a7-117">The screen shots in this tutorial use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-117">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="6a7a7-118">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-118">An active Azure account.</span></span> <span data-ttu-id="6a7a7-119">If you don't have one, you can create a free account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="6a7a7-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6a7a7-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="6a7a7-121">Create an Event Hubs namespace and an event hub</span><span class="sxs-lookup"><span data-stu-id="6a7a7-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="6a7a7-122">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-122">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="6a7a7-123">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-123">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="6a7a7-124">Create an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="6a7a7-124">Create an Azure Storage account</span></span>

<span data-ttu-id="6a7a7-125">To use the [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="6a7a7-125">To use the [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="6a7a7-126">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-126">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
2. <span data-ttu-id="6a7a7-127">Click **Storage**, then click **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="6a7a7-128">In the **Create storage account** blade, type a name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-128">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="6a7a7-129">Choose an Azure subscription, resource group, and location in which to create the resource.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-129">Choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="6a7a7-130">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-130">Then click **Create**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="6a7a7-131">In the list of storage accounts, click the newly-created storage account.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-131">In the list of storage accounts, click the newly-created storage account.</span></span>
5. <span data-ttu-id="6a7a7-132">In the storage account blade, click **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-132">In the storage account blade, click **Access keys**.</span></span> <span data-ttu-id="6a7a7-133">Copy the value of **key1** to use later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-133">Copy the value of **key1** to use later in this tutorial.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)
6. <span data-ttu-id="6a7a7-134">In Visual Studio, create a new Visual C# Desktop App project using the **Console  Application** project template.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-134">In Visual Studio, create a new Visual C# Desktop App project using the **Console  Application** project template.</span></span> <span data-ttu-id="6a7a7-135">Name the project **Receiver**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-135">Name the project **Receiver**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
7. <span data-ttu-id="6a7a7-136">In Solution Explorer, right-click the **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-136">In Solution Explorer, right-click the **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
8. <span data-ttu-id="6a7a7-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="6a7a7-138">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-138">Click **Install**, and accept the terms of use.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="6a7a7-139">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-139">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
9. <span data-ttu-id="6a7a7-140">Right-click the **Receiver** project, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-140">Right-click the **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="6a7a7-141">Name the new class **SimpleEventProcessor**, and then click **Add** to create the class.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-141">Name the new class **SimpleEventProcessor**, and then click **Add** to create the class.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
10. <span data-ttu-id="6a7a7-142">Add the following statements at the top of the SimpleEventProcessor.cs file:</span><span class="sxs-lookup"><span data-stu-id="6a7a7-142">Add the following statements at the top of the SimpleEventProcessor.cs file:</span></span>
    
     ```csharp
     using Microsoft.ServiceBus.Messaging;
     using System.Diagnostics;
     ```
    
     <span data-ttu-id="6a7a7-143">Then, substitute the following code for the body of the class:</span><span class="sxs-lookup"><span data-stu-id="6a7a7-143">Then, substitute the following code for the body of the class:</span></span>
    
     ```csharp
     class SimpleEventProcessor : IEventProcessor
     {
         Stopwatch checkpointStopWatch;
    
         async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
         {
             Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
             if (reason == CloseReason.Shutdown)
             {
                 await context.CheckpointAsync();
             }
         }
    
         Task IEventProcessor.OpenAsync(PartitionContext context)
         {
             Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
             this.checkpointStopWatch = new Stopwatch();
             this.checkpointStopWatch.Start();
             return Task.FromResult<object>(null);
         }
    
         async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
         {
             foreach (EventData eventData in messages)
             {
                 string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
                 Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                     context.Lease.PartitionId, data));
             }
    
             //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
             if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
             {
                 await context.CheckpointAsync();
                 this.checkpointStopWatch.Restart();
             }
         }
     }
     ```
    
     <span data-ttu-id="6a7a7-144">This class will be called by the **EventProcessorHost** to process events received from the event hub.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-144">This class will be called by the **EventProcessorHost** to process events received from the event hub.</span></span> <span data-ttu-id="6a7a7-145">Note that the `SimpleEventProcessor` class uses a stopwatch to periodically call the checkpoint method on the **EventProcessorHost** context.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-145">Note that the `SimpleEventProcessor` class uses a stopwatch to periodically call the checkpoint method on the **EventProcessorHost** context.</span></span> <span data-ttu-id="6a7a7-146">This ensures that, if the receiver is restarted, it will lose no more than five minutes of processing work.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-146">This ensures that, if the receiver is restarted, it will lose no more than five minutes of processing work.</span></span>
11. <span data-ttu-id="6a7a7-147">In the **Program** class, add the following `using` statement at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="6a7a7-147">In the **Program** class, add the following `using` statement at the top of the file:</span></span>
    
     ```csharp
     using Microsoft.ServiceBus.Messaging;
     ```
    
     <span data-ttu-id="6a7a7-148">Then, replace the `Main` method in the `Program` class with the following code, substituting the event hub name and the namespace-level connection string that you saved previously, and the storage account and key that you copied in the previous sections.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-148">Then, replace the `Main` method in the `Program` class with the following code, substituting the event hub name and the namespace-level connection string that you saved previously, and the storage account and key that you copied in the previous sections.</span></span> 
    
     ```csharp
     static void Main(string[] args)
     {
       string eventHubConnectionString = "{Event Hubs namespace connection string}";
       string eventHubName = "{Event Hub name}";
       string storageAccountName = "{storage account name}";
       string storageAccountKey = "{storage account key}";
       string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
       string eventProcessorHostName = Guid.NewGuid().ToString();
       EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
       Console.WriteLine("Registering EventProcessor...");
       var options = new EventProcessorOptions();
       options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
       eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
       Console.WriteLine("Receiving. Press enter key to stop worker.");
       Console.ReadLine();
       eventProcessorHost.UnregisterEventProcessorAsync().Wait();
     }
     ```

12. <span data-ttu-id="6a7a7-149">Run the program, and ensure that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-149">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="6a7a7-150">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6a7a7-150">Congratulations!</span></span> <span data-ttu-id="6a7a7-151">You have now received messages from an event hub using the Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-151">You have now received messages from an event hub using the Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="6a7a7-152">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="6a7a7-152">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="6a7a7-153">To increase throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in the [Scaled out event processing][Scaled out event processing] sample.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-153">To increase throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in the [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="6a7a7-154">In those cases, the various instances automatically coordinate with each other to load balance the received events.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-154">In those cases, the various instances automatically coordinate with each other to load balance the received events.</span></span> <span data-ttu-id="6a7a7-155">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-155">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="6a7a7-156">When receiving events from different machines, it might be useful to specify names for [EventProcessorHost][EventProcessorHost] instances based on the machines (or roles) in which they are deployed.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-156">When receiving events from different machines, it might be useful to specify names for [EventProcessorHost][EventProcessorHost] instances based on the machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="6a7a7-157">For more information about these topics, see the [Event Hubs Overview][Event Hubs Overview] and [Event Hubs Programming Guide][Event Hubs Programming Guide] topics.</span><span class="sxs-lookup"><span data-stu-id="6a7a7-157">For more information about these topics, see the [Event Hubs Overview][Event Hubs Overview] and [Event Hubs Programming Guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

<!-- Links -->
[Event Hubs Overview]: event-hubs-overview.md
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]: ../storage/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="6a7a7-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a7a7-158">Next steps</span></span>
<span data-ttu-id="6a7a7-159">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="6a7a7-159">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting the following links:</span></span>

* [<span data-ttu-id="6a7a7-160">Event Processor Host</span><span class="sxs-lookup"><span data-stu-id="6a7a7-160">Event Processor Host</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* <span data-ttu-id="6a7a7-161">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="6a7a7-161">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="6a7a7-162">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="6a7a7-162">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-overview.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3









