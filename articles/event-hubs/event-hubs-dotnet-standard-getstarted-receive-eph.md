---
title: Receive events from Azure Event Hubs using .NET Standard | Microsoft Docs
description: Get started receiving messages with the EventProcessorHost in .NET Standard
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
ms.date: 03/27/2017
ms.author: jotaub;sethm
ms.openlocfilehash: 8e6b128d72b5224f2d899464b034afaa13b360db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552345"
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="af0a0-103">Get started receiving messages with the Event Processor Host in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="af0a0-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="af0a0-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="af0a0-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleEphReceiver).</span></span>

<span data-ttu-id="af0a0-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="af0a0-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span><span class="sxs-lookup"><span data-stu-id="af0a0-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="af0a0-107">Or you can follow the steps in this tutorial to create your own.</span><span class="sxs-lookup"><span data-stu-id="af0a0-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af0a0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af0a0-108">Prerequisites</span></span>

* <span data-ttu-id="af0a0-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="af0a0-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="af0a0-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span><span class="sxs-lookup"><span data-stu-id="af0a0-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="af0a0-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="af0a0-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="af0a0-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="af0a0-112">An Azure subscription.</span></span>
* <span data-ttu-id="af0a0-113">An Azure Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="af0a0-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="af0a0-114">An Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="af0a0-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="af0a0-115">Create an Event Hubs namespace and an event hub</span><span class="sxs-lookup"><span data-stu-id="af0a0-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="af0a0-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span><span class="sxs-lookup"><span data-stu-id="af0a0-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="af0a0-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span><span class="sxs-lookup"><span data-stu-id="af0a0-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="af0a0-118">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="af0a0-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="af0a0-119">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af0a0-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="af0a0-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="af0a0-121">Complete the fields in the storage account blade, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Create storage account][1]

4. <span data-ttu-id="af0a0-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span><span class="sxs-lookup"><span data-stu-id="af0a0-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="af0a0-124">In the **Essentials** blade, click **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="af0a0-125">When the **Blob service** blade opens, click **+ Container** at the top.</span><span class="sxs-lookup"><span data-stu-id="af0a0-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="af0a0-126">Give the container a name, and then close the **Blob service** blade.</span><span class="sxs-lookup"><span data-stu-id="af0a0-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="af0a0-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="af0a0-128">Save these values to Notepad or some other temporary location.</span><span class="sxs-lookup"><span data-stu-id="af0a0-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="af0a0-129">Create a console application</span><span class="sxs-lookup"><span data-stu-id="af0a0-129">Create a console application</span></span>

<span data-ttu-id="af0a0-130">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af0a0-130">Start Visual Studio.</span></span> <span data-ttu-id="af0a0-131">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="af0a0-132">Create a .NET Core console application.</span><span class="sxs-lookup"><span data-stu-id="af0a0-132">Create a .NET Core console application.</span></span>

![New project][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="af0a0-134">Add the Event Hubs NuGet package</span><span class="sxs-lookup"><span data-stu-id="af0a0-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="af0a0-135">Add the following NuGet packages to the project:</span><span class="sxs-lookup"><span data-stu-id="af0a0-135">Add the following NuGet packages to the project:</span></span>
* [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/)
* [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/)

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="af0a0-136">Implement the IEventProcessor interface</span><span class="sxs-lookup"><span data-stu-id="af0a0-136">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="af0a0-137">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-137">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="af0a0-138">Name the new class **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="af0a0-138">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="af0a0-139">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span><span class="sxs-lookup"><span data-stu-id="af0a0-139">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="af0a0-140">Implement the `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="af0a0-140">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="af0a0-141">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span><span class="sxs-lookup"><span data-stu-id="af0a0-141">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="af0a0-142">Write a main console method that uses the SimpleEventProcessor class to receive messages</span><span class="sxs-lookup"><span data-stu-id="af0a0-142">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="af0a0-143">Add the following `using` statements to the top of the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="af0a0-143">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="af0a0-144">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span><span class="sxs-lookup"><span data-stu-id="af0a0-144">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="af0a0-145">Add the following code, replacing the placeholders with their corresponding values.</span><span class="sxs-lookup"><span data-stu-id="af0a0-145">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="af0a0-146">Add a new method named `MainAsync` to the `Program` class, as follows:</span><span class="sxs-lookup"><span data-stu-id="af0a0-146">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="af0a0-147">Add the following line of code to the `Main` method:</span><span class="sxs-lookup"><span data-stu-id="af0a0-147">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="af0a0-148">Here is what your Program.cs file should look like:</span><span class="sxs-lookup"><span data-stu-id="af0a0-148">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="af0a0-149">Run the program, and ensure that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="af0a0-149">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="af0a0-150">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="af0a0-150">Congratulations!</span></span> <span data-ttu-id="af0a0-151">You have now received messages from an event hub by using the Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="af0a0-151">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af0a0-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="af0a0-152">Next steps</span></span>
<span data-ttu-id="af0a0-153">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="af0a0-153">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="af0a0-154">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="af0a0-154">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="af0a0-155">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="af0a0-155">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="af0a0-156">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="af0a0-156">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png


