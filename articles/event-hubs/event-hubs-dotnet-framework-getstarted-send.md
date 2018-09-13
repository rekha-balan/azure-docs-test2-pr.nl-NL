---
title: Send events to Azure Event Hubs using the .NET Framework | Microsoft Docs
description: Get started sending events to Event Hubs using the .NET Framework
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
ms.openlocfilehash: 25700a8d7a41ab68df5f907b336e74fcafee159b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562822"
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="44ef3-103">Send events to Azure Event Hubs using the .NET Framework</span><span class="sxs-lookup"><span data-stu-id="44ef3-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="44ef3-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="44ef3-104">Introduction</span></span>
<span data-ttu-id="44ef3-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="44ef3-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="44ef3-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span><span class="sxs-lookup"><span data-stu-id="44ef3-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="44ef3-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span><span class="sxs-lookup"><span data-stu-id="44ef3-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="44ef3-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span><span class="sxs-lookup"><span data-stu-id="44ef3-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="44ef3-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="44ef3-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="44ef3-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span><span class="sxs-lookup"><span data-stu-id="44ef3-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="44ef3-111">To complete this tutorial, you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="44ef3-111">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="44ef3-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="44ef3-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="44ef3-113">The screen shots in this tutorial use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="44ef3-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="44ef3-114">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="44ef3-114">An active Azure account.</span></span> <span data-ttu-id="44ef3-115">If you don't have one, you can create a free account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="44ef3-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="44ef3-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="44ef3-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="44ef3-117">Create an Event Hubs namespace and an event hub</span><span class="sxs-lookup"><span data-stu-id="44ef3-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="44ef3-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span><span class="sxs-lookup"><span data-stu-id="44ef3-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="44ef3-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps.</span><span class="sxs-lookup"><span data-stu-id="44ef3-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="44ef3-120">Create a console application</span><span class="sxs-lookup"><span data-stu-id="44ef3-120">Create a console application</span></span>
<span data-ttu-id="44ef3-121">In this section, you'll write a Windows console app that sends events to your event hub.</span><span class="sxs-lookup"><span data-stu-id="44ef3-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="44ef3-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="44ef3-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="44ef3-123">Name the project **Sender**.</span><span class="sxs-lookup"><span data-stu-id="44ef3-123">Name the project **Sender**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="44ef3-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="44ef3-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="44ef3-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="44ef3-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="44ef3-126">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="44ef3-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="44ef3-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="44ef3-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="44ef3-128">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="44ef3-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.Threading;
    using Microsoft.ServiceBus.Messaging;
    ```
5. <span data-ttu-id="44ef3-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span><span class="sxs-lookup"><span data-stu-id="44ef3-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
    ```csharp
    static string eventHubName = "{Event Hub name}";
    static string connectionString = "{send connection string}";
    ```
6. <span data-ttu-id="44ef3-130">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="44ef3-130">Add the following method to the **Program** class:</span></span>
   
    ```csharp
    static void SendingRandomMessages()
    {
        var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
        while (true)
        {
            try
            {
                var message = Guid.NewGuid().ToString();
                Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
                eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
                Console.ResetColor();
            }
   
            Thread.Sleep(200);
        }
    }
    ```
   
    <span data-ttu-id="44ef3-131">This method continuously sends events to your event hub with a 200-ms delay.</span><span class="sxs-lookup"><span data-stu-id="44ef3-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="44ef3-132">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="44ef3-132">Finally, add the following lines to the **Main** method:</span></span>
   
    ```csharp
    Console.WriteLine("Press Ctrl-C to stop the sender process");
    Console.WriteLine("Press Enter to start now");
    Console.ReadLine();
    SendingRandomMessages();
    ```
8. <span data-ttu-id="44ef3-133">Run the program, and ensure that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="44ef3-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="44ef3-134">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="44ef3-134">Congratulations!</span></span> <span data-ttu-id="44ef3-135">You have now sent messages to an event hub.</span><span class="sxs-lookup"><span data-stu-id="44ef3-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44ef3-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="44ef3-136">Next steps</span></span>
<span data-ttu-id="44ef3-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="44ef3-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="44ef3-138">Receive events using the Event Processor Host</span><span class="sxs-lookup"><span data-stu-id="44ef3-138">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="44ef3-139">Event Processor Host reference</span><span class="sxs-lookup"><span data-stu-id="44ef3-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="44ef3-140">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="44ef3-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png







