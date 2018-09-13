---
title: Send events to Azure Event Hubs using the .NET Framework | Microsoft Docs
description: Get started sending events to Event Hubs using the .NET Framework
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2018
ms.author: shvija
ms.openlocfilehash: 7b5a4298ee4c67f0300bd4aabb7fc6373d8edba0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830401"
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="089dc-103">Send events to Azure Event Hubs using the .NET Framework</span><span class="sxs-lookup"><span data-stu-id="089dc-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

<span data-ttu-id="089dc-104">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="089dc-104">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="089dc-105">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span><span class="sxs-lookup"><span data-stu-id="089dc-105">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="089dc-106">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span><span class="sxs-lookup"><span data-stu-id="089dc-106">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="089dc-107">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span><span class="sxs-lookup"><span data-stu-id="089dc-107">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="089dc-108">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="089dc-108">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="089dc-109">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span><span class="sxs-lookup"><span data-stu-id="089dc-109">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="089dc-110">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="089dc-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="089dc-111">[Microsoft Visual Studio 2017 or higher](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="089dc-111">[Microsoft Visual Studio 2017 or higher](http://visualstudio.com).</span></span>
* <span data-ttu-id="089dc-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="089dc-112">An active Azure account.</span></span> <span data-ttu-id="089dc-113">If you don't have one, you can create a free account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="089dc-113">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="089dc-114">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="089dc-114">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="089dc-115">Create an Event Hubs namespace and an event hub</span><span class="sxs-lookup"><span data-stu-id="089dc-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="089dc-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span><span class="sxs-lookup"><span data-stu-id="089dc-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="089dc-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="089dc-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="089dc-118">Create a sender console application</span><span class="sxs-lookup"><span data-stu-id="089dc-118">Create a sender console application</span></span>

<span data-ttu-id="089dc-119">In this section, you write a Windows console app that sends events to your event hub.</span><span class="sxs-lookup"><span data-stu-id="089dc-119">In this section, you write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="089dc-120">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="089dc-120">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="089dc-121">Name the project **Sender**.</span><span class="sxs-lookup"><span data-stu-id="089dc-121">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="089dc-122">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="089dc-122">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="089dc-123">Click the **Browse** tab, then search for `WindowsAzure.ServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="089dc-123">Click the **Browse** tab, then search for `WindowsAzure.ServiceBus`.</span></span> <span data-ttu-id="089dc-124">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="089dc-124">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="089dc-125">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="089dc-125">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="089dc-126">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="089dc-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="089dc-127">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span><span class="sxs-lookup"><span data-stu-id="089dc-127">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "Your Event Hub name";
  static string connectionString = "namespace connection string";
  ```
6. <span data-ttu-id="089dc-128">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="089dc-128">Add the following method to the **Program** class:</span></span>
   
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
   
  <span data-ttu-id="089dc-129">This method continuously sends events to your event hub with a 200-ms delay.</span><span class="sxs-lookup"><span data-stu-id="089dc-129">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="089dc-130">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="089dc-130">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="089dc-131">Run the program, and ensure that there are no errors.</span><span class="sxs-lookup"><span data-stu-id="089dc-131">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="089dc-132">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="089dc-132">Congratulations!</span></span> <span data-ttu-id="089dc-133">You have now sent messages to an event hub.</span><span class="sxs-lookup"><span data-stu-id="089dc-133">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="089dc-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="089dc-134">Next steps</span></span>

<span data-ttu-id="089dc-135">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="089dc-135">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="089dc-136">Receive events using the Event Processor Host</span><span class="sxs-lookup"><span data-stu-id="089dc-136">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="089dc-137">Event Processor Host reference</span><span class="sxs-lookup"><span data-stu-id="089dc-137">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="089dc-138">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="089dc-138">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

