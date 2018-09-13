---
title: Get started with queue storage and Visual Studio connected services (ASP.NET Core) | Microsoft Docs
description: How to get started using Azure queue storage in an ASP.NET Core project in Visual Studio
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4622496544ce6e1057ac68a2e9946917573e997e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549661"
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="6a3a2-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="6a3a2-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6a3a2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6a3a2-104">Overview</span></span>
<span data-ttu-id="6a3a2-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="6a3a2-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="6a3a2-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="6a3a2-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="6a3a2-109">To get started, you first need to create an Azure queue in your storage account.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="6a3a2-110">We'll show you how to create a queue in code.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="6a3a2-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="6a3a2-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="6a3a2-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="6a3a2-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="6a3a2-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="6a3a2-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="6a3a2-116">The code below assumes async programming methods are being used.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="6a3a2-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="6a3a2-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="6a3a2-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="6a3a2-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="6a3a2-121">Access queues in code</span><span class="sxs-lookup"><span data-stu-id="6a3a2-121">Access queues in code</span></span>
<span data-ttu-id="6a3a2-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="6a3a2-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="6a3a2-124">Get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a3a2-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="6a3a2-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="6a3a2-127">Get a **CloudQueue** object to reference a specific queue.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="6a3a2-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="6a3a2-129">Create a queue in code</span><span class="sxs-lookup"><span data-stu-id="6a3a2-129">Create a queue in code</span></span>
<span data-ttu-id="6a3a2-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="6a3a2-131">Add a message to a queue</span><span class="sxs-lookup"><span data-stu-id="6a3a2-131">Add a message to a queue</span></span>
<span data-ttu-id="6a3a2-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="6a3a2-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="6a3a2-134">Here is an example which inserts the message 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="6a3a2-135">Read a message in a queue</span><span class="sxs-lookup"><span data-stu-id="6a3a2-135">Read a message in a queue</span></span>
<span data-ttu-id="6a3a2-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="6a3a2-137">Read and remove a message in a queue</span><span class="sxs-lookup"><span data-stu-id="6a3a2-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="6a3a2-138">Your code can remove (dequeue) a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="6a3a2-139">Call **GetMessageAsync** to get the next message in a queue.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="6a3a2-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="6a3a2-141">By default, this message stays invisible for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="6a3a2-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="6a3a2-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="6a3a2-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="6a3a2-145">Leverage additional options for dequeuing messages</span><span class="sxs-lookup"><span data-stu-id="6a3a2-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="6a3a2-146">There are two ways you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="6a3a2-147">First, you can get a batch of messages (up to 32).</span><span class="sxs-lookup"><span data-stu-id="6a3a2-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="6a3a2-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="6a3a2-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="6a3a2-150">Then it processes each message using a **foreach** loop.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="6a3a2-151">It also sets the invisibility timeout to 5 minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="6a3a2-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="6a3a2-153">Get the queue length</span><span class="sxs-lookup"><span data-stu-id="6a3a2-153">Get the queue length</span></span>
<span data-ttu-id="6a3a2-154">You can get an estimate of the number of messages in a queue.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="6a3a2-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="6a3a2-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="6a3a2-157">Use the Async-Await pattern with common queue APIs</span><span class="sxs-lookup"><span data-stu-id="6a3a2-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="6a3a2-158">This example shows how to use the Async-Await pattern with common queue APIs.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="6a3a2-159">The sample calls the async version of each of the given methods.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="6a3a2-160">This can be seen by the Async post-fix of each method.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="6a3a2-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="6a3a2-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="6a3a2-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="6a3a2-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="6a3a2-164">Delete a queue</span><span class="sxs-lookup"><span data-stu-id="6a3a2-164">Delete a queue</span></span>
<span data-ttu-id="6a3a2-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span><span class="sxs-lookup"><span data-stu-id="6a3a2-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="6a3a2-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a3a2-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

