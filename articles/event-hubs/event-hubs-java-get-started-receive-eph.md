---
title: Receive events from Azure Event Hubs using Java | Microsoft Docs
description: Get started receiving from Event Hubs using Java
services: event-hubs
documentationcenter: ''
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jotaub;sethm
ms.openlocfilehash: 4fc5146ba39206770e54419aa30a53746a0ec684
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564268"
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="a0986-103">Receive events from Azure Event Hubs using Java</span><span class="sxs-lookup"><span data-stu-id="a0986-103">Receive events from Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="a0986-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="a0986-104">Introduction</span></span>
<span data-ttu-id="a0986-105">Event Hubs is a highly scalable ingestion system that can intake millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="a0986-105">Event Hubs is a highly scalable ingestion system that can intake millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="a0986-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span><span class="sxs-lookup"><span data-stu-id="a0986-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="a0986-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="a0986-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="a0986-108">This tutorial shows how to receive events into an Event Hub using a console application written in Java.</span><span class="sxs-lookup"><span data-stu-id="a0986-108">This tutorial shows how to receive events into an Event Hub using a console application written in Java.</span></span>

<span data-ttu-id="a0986-109">In order to complete this tutorial, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="a0986-109">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="a0986-110">A Java development environment.</span><span class="sxs-lookup"><span data-stu-id="a0986-110">A Java development environment.</span></span> <span data-ttu-id="a0986-111">For this tutorial, we will assume [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="a0986-111">For this tutorial, we will assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="a0986-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="a0986-112">An active Azure account.</span></span> <br/><span data-ttu-id="a0986-113">If you don't have an account, you can create a free account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="a0986-113">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="a0986-114">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span><span class="sxs-lookup"><span data-stu-id="a0986-114">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="a0986-115">Receive messages with EventProcessorHost in Java</span><span class="sxs-lookup"><span data-stu-id="a0986-115">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="a0986-116">EventProcessorHost is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="a0986-116">EventProcessorHost is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="a0986-117">Using EventProcessorHost you can split events across multiple receivers, even when hosted in different nodes.</span><span class="sxs-lookup"><span data-stu-id="a0986-117">Using EventProcessorHost you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="a0986-118">This example shows how to use EventProcessorHost for a single receiver.</span><span class="sxs-lookup"><span data-stu-id="a0986-118">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="a0986-119">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="a0986-119">Create a storage account</span></span>
<span data-ttu-id="a0986-120">In order to use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="a0986-120">In order to use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="a0986-121">Log on to the [Azure classic portal][Azure classic portal], and click **NEW** at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="a0986-121">Log on to the [Azure classic portal][Azure classic portal], and click **NEW** at the bottom of the screen.</span></span>
2. <span data-ttu-id="a0986-122">Click **Data Services**, then **Storage**, then **Quick Create**, and then type a name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="a0986-122">Click **Data Services**, then **Storage**, then **Quick Create**, and then type a name for your storage account.</span></span> <span data-ttu-id="a0986-123">Select your desired region, and then click **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="a0986-123">Select your desired region, and then click **Create Storage Account**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="a0986-124">Click the newly created storage account, and then click **Manage Access Keys**:</span><span class="sxs-lookup"><span data-stu-id="a0986-124">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="a0986-125">Copy the primary access key to use later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a0986-125">Copy the primary access key to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="a0986-126">Create a Java project using the EventProcessor Host</span><span class="sxs-lookup"><span data-stu-id="a0986-126">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="a0986-127">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span><span class="sxs-lookup"><span data-stu-id="a0986-127">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="a0986-128">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="a0986-128">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="a0986-129">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span><span class="sxs-lookup"><span data-stu-id="a0986-129">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="a0986-130">The class will be called ```ErrorNotificationHandler```.</span><span class="sxs-lookup"><span data-stu-id="a0986-130">The class will be called ```ErrorNotificationHandler```.</span></span>     
   
    ```Java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="a0986-131">Use the following code to create a new class called ```EventProcessor```.</span><span class="sxs-lookup"><span data-stu-id="a0986-131">Use the following code to create a new class called ```EventProcessor```.</span></span>
   
    ```Java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="a0986-132">Create one final class called ```EventProcessorSample```, using the following code.</span><span class="sxs-lookup"><span data-stu-id="a0986-132">Create one final class called ```EventProcessorSample```, using the following code.</span></span>
   
    ```Java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter to stop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="a0986-133">Replace the following fields with the values used when you created the Event Hub and storage account.</span><span class="sxs-lookup"><span data-stu-id="a0986-133">Replace the following fields with the values used when you created the Event Hub and storage account.</span></span>
   
    ```Java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="a0986-134">This tutorial uses a single instance of EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="a0986-134">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="a0986-135">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="a0986-135">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost.</span></span> <span data-ttu-id="a0986-136">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span><span class="sxs-lookup"><span data-stu-id="a0986-136">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="a0986-137">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span><span class="sxs-lookup"><span data-stu-id="a0986-137">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="a0986-138">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span><span class="sxs-lookup"><span data-stu-id="a0986-138">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md
[Azure Storage account]: ../storage/storage-create-storage-account.md
[Azure classic portal]: http://manage.windowsazure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png

## <a name="next-steps"></a><span data-ttu-id="a0986-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0986-139">Next steps</span></span>
<span data-ttu-id="a0986-140">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="a0986-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a0986-141">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="a0986-141">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a0986-142">Create an Event Hub</span><span class="sxs-lookup"><span data-stu-id="a0986-142">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a0986-143">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="a0986-143">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md
