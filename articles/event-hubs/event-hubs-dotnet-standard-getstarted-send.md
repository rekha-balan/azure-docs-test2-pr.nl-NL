---
title: Send events to Azure Event Hubs using .NET Standard | Microsoft Docs
description: Get started sending events to Event Hubs in .NET Standard
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
ms.openlocfilehash: 909d4c8cbb8ba9df9d7eeba49443ed82853edcaa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553465"
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="42bf8-103">Get started sending messages to Azure Event Hubs in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="42bf8-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="42bf8-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="42bf8-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleSender).</span></span>

<span data-ttu-id="42bf8-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span><span class="sxs-lookup"><span data-stu-id="42bf8-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="42bf8-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span><span class="sxs-lookup"><span data-stu-id="42bf8-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="42bf8-107">Or you can follow the steps in this tutorial to create your own.</span><span class="sxs-lookup"><span data-stu-id="42bf8-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42bf8-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42bf8-108">Prerequisites</span></span>

* <span data-ttu-id="42bf8-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="42bf8-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="42bf8-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span><span class="sxs-lookup"><span data-stu-id="42bf8-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="42bf8-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="42bf8-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="42bf8-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="42bf8-112">An Azure subscription.</span></span>
* <span data-ttu-id="42bf8-113">An event hub namespace.</span><span class="sxs-lookup"><span data-stu-id="42bf8-113">An event hub namespace.</span></span>

<span data-ttu-id="42bf8-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span><span class="sxs-lookup"><span data-stu-id="42bf8-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="42bf8-115">Create an Event Hubs namespace and an event hub</span><span class="sxs-lookup"><span data-stu-id="42bf8-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="42bf8-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span><span class="sxs-lookup"><span data-stu-id="42bf8-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="42bf8-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span><span class="sxs-lookup"><span data-stu-id="42bf8-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="42bf8-118">Create a console application</span><span class="sxs-lookup"><span data-stu-id="42bf8-118">Create a console application</span></span>

<span data-ttu-id="42bf8-119">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42bf8-119">Start Visual Studio.</span></span> <span data-ttu-id="42bf8-120">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="42bf8-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="42bf8-121">Create a .NET Core console application.</span><span class="sxs-lookup"><span data-stu-id="42bf8-121">Create a .NET Core console application.</span></span>

![New project][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="42bf8-123">Add the Event Hubs NuGet package</span><span class="sxs-lookup"><span data-stu-id="42bf8-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="42bf8-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) NuGet package to your project.</span><span class="sxs-lookup"><span data-stu-id="42bf8-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) NuGet package to your project.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="42bf8-125">Write some code to send messages to the event hub</span><span class="sxs-lookup"><span data-stu-id="42bf8-125">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="42bf8-126">Add the following `using` statements to the top of the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="42bf8-126">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="42bf8-127">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span><span class="sxs-lookup"><span data-stu-id="42bf8-127">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="42bf8-128">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span><span class="sxs-lookup"><span data-stu-id="42bf8-128">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="42bf8-129">Add a new method named `MainAsync` to the `Program` class, as follows:</span><span class="sxs-lookup"><span data-stu-id="42bf8-129">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="42bf8-130">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span><span class="sxs-lookup"><span data-stu-id="42bf8-130">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="42bf8-131">Add the following code to the `Main` method in the `Program` class.</span><span class="sxs-lookup"><span data-stu-id="42bf8-131">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="42bf8-132">Here is what your Program.cs should look like.</span><span class="sxs-lookup"><span data-stu-id="42bf8-132">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="42bf8-133">Run the program, and ensure that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="42bf8-133">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="42bf8-134">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="42bf8-134">Congratulations!</span></span> <span data-ttu-id="42bf8-135">You have now sent messages to an event hub.</span><span class="sxs-lookup"><span data-stu-id="42bf8-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42bf8-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="42bf8-136">Next steps</span></span>
<span data-ttu-id="42bf8-137">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="42bf8-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="42bf8-138">Receive events from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="42bf8-138">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="42bf8-139">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="42bf8-139">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="42bf8-140">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="42bf8-140">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="42bf8-141">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="42bf8-141">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-standard-getstarted-send/netcore.png

