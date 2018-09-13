---
title: Get started with Azure Service Bus queues | Microsoft Docs
description: Write a C# console application that uses Service Bus messaging queues.
services: service-bus-messaging
documentationcenter: .net
author: spelluru
manager: timlt
editor: ''
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 12/7/2017
ms.author: spelluru
ms.openlocfilehash: d75d1937ca0450f3eedd2c5ba4e91caf3b473a9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793876"
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="6eec4-103">Get started with Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="6eec4-103">Get started with Service Bus queues</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="6eec4-104">This tutorial covers the following steps:</span><span class="sxs-lookup"><span data-stu-id="6eec4-104">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="6eec4-105">Create a Service Bus namespace, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6eec4-105">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="6eec4-106">Create a Service Bus queue, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6eec4-106">Create a Service Bus queue, using the Azure portal.</span></span>
3. <span data-ttu-id="6eec4-107">Write a .NET Core console application to send a set of messages to the queue.</span><span class="sxs-lookup"><span data-stu-id="6eec4-107">Write a .NET Core console application to send a set of messages to the queue.</span></span>
4. <span data-ttu-id="6eec4-108">Write a .NET Core console application to receive those messages from the queue.</span><span class="sxs-lookup"><span data-stu-id="6eec4-108">Write a .NET Core console application to receive those messages from the queue.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eec4-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6eec4-109">Prerequisites</span></span>

1. <span data-ttu-id="6eec4-110">[Visual Studio 2017 Update 3 (version 15.3, 26730.01)](http://www.visualstudio.com/vs) or later.</span><span class="sxs-lookup"><span data-stu-id="6eec4-110">[Visual Studio 2017 Update 3 (version 15.3, 26730.01)](http://www.visualstudio.com/vs) or later.</span></span>
2. <span data-ttu-id="6eec4-111">[NET Core SDK](https://www.microsoft.com/net/download/windows), version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="6eec4-111">[NET Core SDK](https://www.microsoft.com/net/download/windows), version 2.0 or later.</span></span>
2. <span data-ttu-id="6eec4-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6eec4-112">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="6eec4-113">1. Create a namespace using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6eec4-113">1. Create a namespace using the Azure portal</span></span>

> [!NOTE] 
> <span data-ttu-id="6eec4-114">You can also create a Service Bus namespace and messaging entities using [PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="6eec4-114">You can also create a Service Bus namespace and messaging entities using [PowerShell](/powershell/azure/get-started-azureps).</span></span> <span data-ttu-id="6eec4-115">For more information, see [Use PowerShell to manage Service Bus resources](service-bus-manage-with-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6eec4-115">For more information, see [Use PowerShell to manage Service Bus resources](service-bus-manage-with-ps.md).</span></span>

<span data-ttu-id="6eec4-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="6eec4-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-the-azure-portal"></a><span data-ttu-id="6eec4-117">2. Create a queue using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6eec4-117">2. Create a queue using the Azure portal</span></span>

<span data-ttu-id="6eec4-118">If you have already created a Service Bus queue, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span><span class="sxs-lookup"><span data-stu-id="6eec4-118">If you have already created a Service Bus queue, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-to-the-queue"></a><span data-ttu-id="6eec4-119">3. Send messages to the queue</span><span class="sxs-lookup"><span data-stu-id="6eec4-119">3. Send messages to the queue</span></span>

<span data-ttu-id="6eec4-120">To send messages to the queue, write a C# console application using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eec4-120">To send messages to the queue, write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="6eec4-121">Create a console application</span><span class="sxs-lookup"><span data-stu-id="6eec4-121">Create a console application</span></span>

<span data-ttu-id="6eec4-122">Launch Visual Studio and create a new **Console App (.NET Core)** project.</span><span class="sxs-lookup"><span data-stu-id="6eec4-122">Launch Visual Studio and create a new **Console App (.NET Core)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="6eec4-123">Add the Service Bus NuGet package</span><span class="sxs-lookup"><span data-stu-id="6eec4-123">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="6eec4-124">Right-click the newly created project and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="6eec4-124">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6eec4-125">Click the **Browse** tab, search for **[Microsoft.Azure.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus/)**, and then select the **Microsoft.Azure.ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="6eec4-125">Click the **Browse** tab, search for **[Microsoft.Azure.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus/)**, and then select the **Microsoft.Azure.ServiceBus** item.</span></span> <span data-ttu-id="6eec4-126">Click **Install** to complete the installation, then close this dialog box.</span><span class="sxs-lookup"><span data-stu-id="6eec4-126">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Select a NuGet package][nuget-pkg]

### <a name="write-code-to-send-messages-to-the-queue"></a><span data-ttu-id="6eec4-128">Write code to send messages to the queue</span><span class="sxs-lookup"><span data-stu-id="6eec4-128">Write code to send messages to the queue</span></span>

1. <span data-ttu-id="6eec4-129">In Program.cs, add the following `using` statements at the top of the namespace definition, before the class declaration:</span><span class="sxs-lookup"><span data-stu-id="6eec4-129">In Program.cs, add the following `using` statements at the top of the namespace definition, before the class declaration:</span></span>
   
    ```csharp
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.ServiceBus;
    ```

2. <span data-ttu-id="6eec4-130">Within the `Program` class, declare the following variables.</span><span class="sxs-lookup"><span data-stu-id="6eec4-130">Within the `Program` class, declare the following variables.</span></span> <span data-ttu-id="6eec4-131">Set the `ServiceBusConnectionString` variable to the connection string that you obtained when creating the namespace, and set `QueueName` to the name that you used when creating the queue:</span><span class="sxs-lookup"><span data-stu-id="6eec4-131">Set the `ServiceBusConnectionString` variable to the connection string that you obtained when creating the namespace, and set `QueueName` to the name that you used when creating the queue:</span></span>
   
    ```csharp
    const string ServiceBusConnectionString = "<your_connection_string>";
    const string QueueName = "<your_queue_name>";
    static IQueueClient queueClient;
    ``` 

3. <span data-ttu-id="6eec4-132">Replace the default contents of `Main()` with the following line of code:</span><span class="sxs-lookup"><span data-stu-id="6eec4-132">Replace the default contents of `Main()` with the following line of code:</span></span>

    ```csharp
    MainAsync().GetAwaiter().GetResult();
    ```

4. <span data-ttu-id="6eec4-133">Directly after `Main()`, add the following asynchronous `MainAsync()` method that calls the send messages method:</span><span class="sxs-lookup"><span data-stu-id="6eec4-133">Directly after `Main()`, add the following asynchronous `MainAsync()` method that calls the send messages method:</span></span>

    ```csharp
    static async Task MainAsync()
    {
        const int numberOfMessages = 10;
        queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

        Console.WriteLine("======================================================");
        Console.WriteLine("Press ENTER key to exit after sending all the messages.");
        Console.WriteLine("======================================================");

        // Send messages.
        await SendMessagesAsync(numberOfMessages);

        Console.ReadKey();

        await queueClient.CloseAsync();
    }
    ```

5. <span data-ttu-id="6eec4-134">Directly after the `MainAsync()` method, add the following `SendMessagesAsync()` method that performs the work of sending the number of messages specified by `numberOfMessagesToSend` (currently set to 10):</span><span class="sxs-lookup"><span data-stu-id="6eec4-134">Directly after the `MainAsync()` method, add the following `SendMessagesAsync()` method that performs the work of sending the number of messages specified by `numberOfMessagesToSend` (currently set to 10):</span></span>

    ```csharp
    static async Task SendMessagesAsync(int numberOfMessagesToSend)
    {
        try
        {
            for (var i = 0; i < numberOfMessagesToSend; i++)
            {
                // Create a new message to send to the queue.
                string messageBody = $"Message {i}";
                var message = new Message(Encoding.UTF8.GetBytes(messageBody));

                // Write the body of the message to the console.
                Console.WriteLine($"Sending message: {messageBody}");

                // Send the message to the queue.
                await queueClient.SendAsync(message);
            }
        }
        catch (Exception exception)
        {
            Console.WriteLine($"{DateTime.Now} :: Exception: {exception.Message}");
        }
    }
    ```
   
6. <span data-ttu-id="6eec4-135">Here is what your Program.cs file should look like.</span><span class="sxs-lookup"><span data-stu-id="6eec4-135">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    namespace CoreSenderApp
    {
        using System;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.ServiceBus;

        class Program
        {
            // Connection String for the namespace can be obtained from the Azure portal under the 
            // 'Shared Access policies' section.
            const string ServiceBusConnectionString = "<your_connection_string>";
            const string QueueName = "<your_queue_name>";
            static IQueueClient queueClient;

            static void Main(string[] args)
            {
                MainAsync().GetAwaiter().GetResult();
            }

            static async Task MainAsync()
            {
                const int numberOfMessages = 10;
                queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

                Console.WriteLine("======================================================");
                Console.WriteLine("Press ENTER key to exit after receiving all the messages.");
                Console.WriteLine("======================================================");

                // Send Messages
                await SendMessagesAsync(numberOfMessages);
                        
                Console.ReadKey();

                await queueClient.CloseAsync();
            }

            static async Task SendMessagesAsync(int numberOfMessagesToSend)
            {
                try
                {
                    for (var i = 0; i < numberOfMessagesToSend; i++)
                    {
                        // Create a new message to send to the queue
                        string messageBody = $"Message {i}";
                        var message = new Message(Encoding.UTF8.GetBytes(messageBody));

                        // Write the body of the message to the console
                        Console.WriteLine($"Sending message: {messageBody}");

                        // Send the message to the queue
                        await queueClient.SendAsync(message);
                    }
                }
                catch (Exception exception)
                {
                    Console.WriteLine($"{DateTime.Now} :: Exception: {exception.Message}");
                }
            }
        }
    }
    ```

7. <span data-ttu-id="6eec4-136">Run the program, and check the Azure portal: click the name of your queue in the namespace **Overview** window.</span><span class="sxs-lookup"><span data-stu-id="6eec4-136">Run the program, and check the Azure portal: click the name of your queue in the namespace **Overview** window.</span></span> <span data-ttu-id="6eec4-137">The queue **Essentials** screen is displayed.</span><span class="sxs-lookup"><span data-stu-id="6eec4-137">The queue **Essentials** screen is displayed.</span></span> <span data-ttu-id="6eec4-138">Notice that the **Active Message Count** value for the queue is now **10**.</span><span class="sxs-lookup"><span data-stu-id="6eec4-138">Notice that the **Active Message Count** value for the queue is now **10**.</span></span> <span data-ttu-id="6eec4-139">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 10.</span><span class="sxs-lookup"><span data-stu-id="6eec4-139">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 10.</span></span> <span data-ttu-id="6eec4-140">Also note that the current size of the queue increments the **Current** value in the **Essentials** window each time the app adds messages to the queue.</span><span class="sxs-lookup"><span data-stu-id="6eec4-140">Also note that the current size of the queue increments the **Current** value in the **Essentials** window each time the app adds messages to the queue.</span></span>
   
      ![Message size][queue-message]

## <a name="4-receive-messages-from-the-queue"></a><span data-ttu-id="6eec4-142">4. Receive messages from the queue</span><span class="sxs-lookup"><span data-stu-id="6eec4-142">4. Receive messages from the queue</span></span>

<span data-ttu-id="6eec4-143">To receive the messages you just sent, create another .NET Core console application and install the **Microsoft.Azure.ServiceBus** NuGet package, similar to the previous sender application.</span><span class="sxs-lookup"><span data-stu-id="6eec4-143">To receive the messages you just sent, create another .NET Core console application and install the **Microsoft.Azure.ServiceBus** NuGet package, similar to the previous sender application.</span></span>

### <a name="write-code-to-receive-messages-from-the-queue"></a><span data-ttu-id="6eec4-144">Write code to receive messages from the queue</span><span class="sxs-lookup"><span data-stu-id="6eec4-144">Write code to receive messages from the queue</span></span>

1. <span data-ttu-id="6eec4-145">In Program.cs, add the following `using` statements at the top of the namespace definition, before the class declaration:</span><span class="sxs-lookup"><span data-stu-id="6eec4-145">In Program.cs, add the following `using` statements at the top of the namespace definition, before the class declaration:</span></span>
   
    ```csharp
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.ServiceBus;
    ```

2. <span data-ttu-id="6eec4-146">Within the `Program` class, declare the following variables.</span><span class="sxs-lookup"><span data-stu-id="6eec4-146">Within the `Program` class, declare the following variables.</span></span> <span data-ttu-id="6eec4-147">Set the `ServiceBusConnectionString` variable to the connection string that you obtained when creating the namespace, and set `QueueName` to the name that you used when creating the queue:</span><span class="sxs-lookup"><span data-stu-id="6eec4-147">Set the `ServiceBusConnectionString` variable to the connection string that you obtained when creating the namespace, and set `QueueName` to the name that you used when creating the queue:</span></span>
   
    ```csharp
    const string ServiceBusConnectionString = "<your_connection_string>";
    const string QueueName = "<your_queue_name>";
    static IQueueClient queueClient;
    ```

3. <span data-ttu-id="6eec4-148">Replace the default contents of `Main()` with the following line of code:</span><span class="sxs-lookup"><span data-stu-id="6eec4-148">Replace the default contents of `Main()` with the following line of code:</span></span>

    ```csharp
    MainAsync().GetAwaiter().GetResult();
    ```

4. <span data-ttu-id="6eec4-149">Directly after `Main()`, add the following asynchronous `MainAsync()` method that calls the `RegisterOnMessageHandlerAndReceiveMessages()` method:</span><span class="sxs-lookup"><span data-stu-id="6eec4-149">Directly after `Main()`, add the following asynchronous `MainAsync()` method that calls the `RegisterOnMessageHandlerAndReceiveMessages()` method:</span></span>

    ```csharp
    static async Task MainAsync()
    {
        queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

        Console.WriteLine("======================================================");
        Console.WriteLine("Press ENTER key to exit after receiving all the messages.");
        Console.WriteLine("======================================================");

        // Register the queue message handler and receive messages in a loop
        RegisterOnMessageHandlerAndReceiveMessages();

        Console.ReadKey();

        await queueClient.CloseAsync();
    }
    ```

5. <span data-ttu-id="6eec4-150">Directly after the `MainAsync()` method, add the following method that registers the message handler and receives the messages sent by the sender application:</span><span class="sxs-lookup"><span data-stu-id="6eec4-150">Directly after the `MainAsync()` method, add the following method that registers the message handler and receives the messages sent by the sender application:</span></span>

    ```csharp
    static void RegisterOnMessageHandlerAndReceiveMessages()
    {
        // Configure the message handler options in terms of exception handling, number of concurrent messages to deliver, etc.
        var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
        {
            // Maximum number of concurrent calls to the callback ProcessMessagesAsync(), set to 1 for simplicity.
            // Set it according to how many messages the application wants to process in parallel.
            MaxConcurrentCalls = 1,

            // Indicates whether the message pump should automatically complete the messages after returning from user callback.
            // False below indicates the complete operation is handled by the user callback as in ProcessMessagesAsync().
            AutoComplete = false
        };

        // Register the function that processes messages.
        queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    }
    ```

6. <span data-ttu-id="6eec4-151">Directly after the previous method, add the following `ProcessMessagesAsync()` method to process the received messages:</span><span class="sxs-lookup"><span data-stu-id="6eec4-151">Directly after the previous method, add the following `ProcessMessagesAsync()` method to process the received messages:</span></span>
 
    ```csharp
    static async Task ProcessMessagesAsync(Message message, CancellationToken token)
    {
        // Process the message.
        Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");

        // Complete the message so that it is not received again.
        // This can be done only if the queue Client is created in ReceiveMode.PeekLock mode (which is the default).
        await queueClient.CompleteAsync(message.SystemProperties.LockToken);

        // Note: Use the cancellationToken passed as necessary to determine if the queueClient has already been closed.
        // If queueClient has already been closed, you can choose to not call CompleteAsync() or AbandonAsync() etc.
        // to avoid unnecessary exceptions.
    }
    ```

7. <span data-ttu-id="6eec4-152">Finally, add the following method to handle any exceptions that might occur:</span><span class="sxs-lookup"><span data-stu-id="6eec4-152">Finally, add the following method to handle any exceptions that might occur:</span></span>
 
    ```csharp
    // Use this handler to examine the exceptions received on the message pump.
    static Task ExceptionReceivedHandler(ExceptionReceivedEventArgs exceptionReceivedEventArgs)
    {
        Console.WriteLine($"Message handler encountered an exception {exceptionReceivedEventArgs.Exception}.");
        var context = exceptionReceivedEventArgs.ExceptionReceivedContext;
        Console.WriteLine("Exception context for troubleshooting:");
        Console.WriteLine($"- Endpoint: {context.Endpoint}");
        Console.WriteLine($"- Entity Path: {context.EntityPath}");
        Console.WriteLine($"- Executing Action: {context.Action}");
        return Task.CompletedTask;
    }    
    ```    
   
8. <span data-ttu-id="6eec4-153">Here is what your Program.cs file should look like:</span><span class="sxs-lookup"><span data-stu-id="6eec4-153">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    namespace CoreReceiverApp
    {
        using System;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.ServiceBus;

        class Program
        {
            // Connection String for the namespace can be obtained from the Azure portal under the 
            // 'Shared Access policies' section.
            const string ServiceBusConnectionString = "<your_connection_string>";
            const string QueueName = "<your_queue_name>";
            static IQueueClient queueClient;

            static void Main(string[] args)
            {
                MainAsync().GetAwaiter().GetResult();
            }

            static async Task MainAsync()
            {
                queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

                Console.WriteLine("======================================================");
                Console.WriteLine("Press ENTER key to exit after receiving all the messages.");
                Console.WriteLine("======================================================");

                // Register QueueClient's MessageHandler and receive messages in a loop
                RegisterOnMessageHandlerAndReceiveMessages();
                    
                Console.ReadKey();

                await queueClient.CloseAsync();
            }

            static void RegisterOnMessageHandlerAndReceiveMessages()
            {
                // Configure the MessageHandler Options in terms of exception handling, number of concurrent messages to deliver etc.
                var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
                {
                    // Maximum number of Concurrent calls to the callback `ProcessMessagesAsync`, set to 1 for simplicity.
                    // Set it according to how many messages the application wants to process in parallel.
                    MaxConcurrentCalls = 1,

                    // Indicates whether MessagePump should automatically complete the messages after returning from User Callback.
                    // False below indicates the Complete will be handled by the User Callback as in `ProcessMessagesAsync` below.
                    AutoComplete = false
                };

                // Register the function that will process messages
                queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
            }

            static async Task ProcessMessagesAsync(Message message, CancellationToken token)
            {
                // Process the message
                Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");

                // Complete the message so that it is not received again.
                // This can be done only if the queueClient is created in ReceiveMode.PeekLock mode (which is default).
                await queueClient.CompleteAsync(message.SystemProperties.LockToken);

                // Note: Use the cancellationToken passed as necessary to determine if the queueClient has already been closed.
                // If queueClient has already been Closed, you may chose to not call CompleteAsync() or AbandonAsync() etc. calls 
               // to avoid unnecessary exceptions.
            }

            static Task ExceptionReceivedHandler(ExceptionReceivedEventArgs exceptionReceivedEventArgs)
            {
                Console.WriteLine($"Message handler encountered an exception {exceptionReceivedEventArgs.Exception}.");
                var context = exceptionReceivedEventArgs.ExceptionReceivedContext;
                Console.WriteLine("Exception context for troubleshooting:");
                Console.WriteLine($"- Endpoint: {context.Endpoint}");
                Console.WriteLine($"- Entity Path: {context.EntityPath}");
                Console.WriteLine($"- Executing Action: {context.Action}");
                return Task.CompletedTask;
            }
        }
    }
    ```
4. <span data-ttu-id="6eec4-154">Run the program, and check the portal again.</span><span class="sxs-lookup"><span data-stu-id="6eec4-154">Run the program, and check the portal again.</span></span> <span data-ttu-id="6eec4-155">Notice that the **Active Message Count** and **Current** values are now **0**.</span><span class="sxs-lookup"><span data-stu-id="6eec4-155">Notice that the **Active Message Count** and **Current** values are now **0**.</span></span>
   
    ![Queue length][queue-message-receive]

<span data-ttu-id="6eec4-157">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6eec4-157">Congratulations!</span></span> <span data-ttu-id="6eec4-158">You have now created a queue, sent a set of messages to that queue, and received those messages from the same queue.</span><span class="sxs-lookup"><span data-stu-id="6eec4-158">You have now created a queue, sent a set of messages to that queue, and received those messages from the same queue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eec4-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="6eec4-159">Next steps</span></span>

<span data-ttu-id="6eec4-160">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span><span class="sxs-lookup"><span data-stu-id="6eec4-160">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png

