---
title: Write a program that uses Azure Service Bus queues | Microsoft Docs
description: How to write a C# console application for Service Bus messaging
services: service-bus-messaging
documentationcenter: .net
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 03/23/2017
ms.author: jotaub;sethm
ms.openlocfilehash: 4c65d0d0078e107d7c27b5dd782beee151528536
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554619"
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="78409-103">Get started with Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="78409-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="78409-104">What will be accomplished</span><span class="sxs-lookup"><span data-stu-id="78409-104">What will be accomplished</span></span>
<span data-ttu-id="78409-105">In this tutorial, we will complete the following:</span><span class="sxs-lookup"><span data-stu-id="78409-105">In this tutorial, we will complete the following:</span></span>

1. <span data-ttu-id="78409-106">Create a Service Bus namespace, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="78409-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="78409-107">Create a Service Bus Messaging queue, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="78409-107">Create a Service Bus Messaging queue, using the Azure portal.</span></span>
3. <span data-ttu-id="78409-108">Write a console application to send a message.</span><span class="sxs-lookup"><span data-stu-id="78409-108">Write a console application to send a message.</span></span>
4. <span data-ttu-id="78409-109">Write a console application to receive messages.</span><span class="sxs-lookup"><span data-stu-id="78409-109">Write a console application to receive messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78409-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="78409-110">Prerequisites</span></span>
1. <span data-ttu-id="78409-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="78409-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="78409-112">The examples in this tutorial use Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="78409-112">The examples in this tutorial use Visual Studio 2015.</span></span>
2. <span data-ttu-id="78409-113">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="78409-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="78409-114">1. Create a namespace using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="78409-114">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="78409-115">If you already have a Service Bus namespace created, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="78409-115">If you already have a Service Bus namespace created, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-the-azure-portal"></a><span data-ttu-id="78409-116">2. Create a queue using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="78409-116">2. Create a queue using the Azure portal</span></span>
<span data-ttu-id="78409-117">If you already have a Service Bus queue created, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span><span class="sxs-lookup"><span data-stu-id="78409-117">If you already have a Service Bus queue created, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-to-the-queue"></a><span data-ttu-id="78409-118">3. Send messages to the queue</span><span class="sxs-lookup"><span data-stu-id="78409-118">3. Send messages to the queue</span></span>
<span data-ttu-id="78409-119">To send messages to the queue, we will write a C# console application using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78409-119">To send messages to the queue, we will write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="78409-120">Create a console application</span><span class="sxs-lookup"><span data-stu-id="78409-120">Create a console application</span></span>

- <span data-ttu-id="78409-121">Launch Visual Studio and create a new Console application.</span><span class="sxs-lookup"><span data-stu-id="78409-121">Launch Visual Studio and create a new Console application.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="78409-122">Add the Service Bus NuGet package</span><span class="sxs-lookup"><span data-stu-id="78409-122">Add the Service Bus NuGet package</span></span>
1. <span data-ttu-id="78409-123">Right-click the newly created project and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="78409-123">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="78409-124">Click the **Browse** tab, then search for “Microsoft Azure Service Bus” and select the **Microsoft Azure Service Bus** item.</span><span class="sxs-lookup"><span data-stu-id="78409-124">Click the **Browse** tab, then search for “Microsoft Azure Service Bus” and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="78409-125">Click **Install** to complete the installation, then close this dialog box.</span><span class="sxs-lookup"><span data-stu-id="78409-125">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Select a NuGet package][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-queue"></a><span data-ttu-id="78409-127">Write some code to send a message to the queue</span><span class="sxs-lookup"><span data-stu-id="78409-127">Write some code to send a message to the queue</span></span>
1. <span data-ttu-id="78409-128">Add the following using statement to the top of the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="78409-128">Add the following using statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="78409-129">Add the following code to the `Main` method, set the **connectionString** variable as the connection string that was obtained when creating the namespace, and set **queueName** as the queue name that used when creating the queue.</span><span class="sxs-lookup"><span data-stu-id="78409-129">Add the following code to the `Main` method, set the **connectionString** variable as the connection string that was obtained when creating the namespace, and set **queueName** as the queue name that used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<Your connection string>";
    var queueName = "<Your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");
    client.Send(message);
    ```
   
    <span data-ttu-id="78409-130">Here is what your Program.cs should look like.</span><span class="sxs-lookup"><span data-stu-id="78409-130">Here is what your Program.cs should look like.</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "<Your connection string>";
                var queueName = "<Your queue name>";
   
                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");
   
                client.Send(message);
            }
        }
    }
    ```
3. <span data-ttu-id="78409-131">Run the program, and check the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="78409-131">Run the program, and check the Azure portal.</span></span> <span data-ttu-id="78409-132">Click the name of your queue in the namespace **Overview** blade.</span><span class="sxs-lookup"><span data-stu-id="78409-132">Click the name of your queue in the namespace **Overview** blade.</span></span> <span data-ttu-id="78409-133">Notice that the **Active message count** value should now be 1.</span><span class="sxs-lookup"><span data-stu-id="78409-133">Notice that the **Active message count** value should now be 1.</span></span>
   
      ![Message count][queue-message]

## <a name="4-receive-messages-from-the-queue"></a><span data-ttu-id="78409-135">4. Receive messages from the queue</span><span class="sxs-lookup"><span data-stu-id="78409-135">4. Receive messages from the queue</span></span>
1. <span data-ttu-id="78409-136">Create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sending application.</span><span class="sxs-lookup"><span data-stu-id="78409-136">Create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sending application.</span></span>
2. <span data-ttu-id="78409-137">Add the following `using` statement to the top of the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="78409-137">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="78409-138">Add the following code to the `Main` method, set the **connectionString** variable as the connection string that was obtained when creating the namespace, and set **queueName** as the queue name that you used when creating the queue.</span><span class="sxs-lookup"><span data-stu-id="78409-138">Add the following code to the `Main` method, set the **connectionString** variable as the connection string that was obtained when creating the namespace, and set **queueName** as the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "";
    var queueName = "samplequeue";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.ReadLine();
    ```
   
    <span data-ttu-id="78409-139">Here is what your Program.cs file should look like:</span><span class="sxs-lookup"><span data-stu-id="78409-139">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "";
          var queueName = "samplequeue";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });
   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="78409-140">Run the program, and check the portal.</span><span class="sxs-lookup"><span data-stu-id="78409-140">Run the program, and check the portal.</span></span> <span data-ttu-id="78409-141">Notice that the **Queue Length** value should now be 0.</span><span class="sxs-lookup"><span data-stu-id="78409-141">Notice that the **Queue Length** value should now be 0.</span></span>
   
    ![Queue length][queue-message-receive]

<span data-ttu-id="78409-143">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="78409-143">Congratulations!</span></span> <span data-ttu-id="78409-144">You have now created a queue, sent a message, and received a message.</span><span class="sxs-lookup"><span data-stu-id="78409-144">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78409-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="78409-145">Next steps</span></span>
<span data-ttu-id="78409-146">Check out our [GitHub repository with samples](https://github.com/Azure-Samples/azure-servicebus-messaging-samples) that demonstrate some of the more advanced features of Azure Service Bus Messaging.</span><span class="sxs-lookup"><span data-stu-id="78409-146">Check out our [GitHub repository with samples](https://github.com/Azure-Samples/azure-servicebus-messaging-samples) that demonstrate some of the more advanced features of Azure Service Bus Messaging.</span></span>

<!--Image references-->

[nuget-pkg]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples



