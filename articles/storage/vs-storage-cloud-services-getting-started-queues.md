---
title: Get started with queue storage and Visual Studio connected services (cloud services) | Microsoft Docs
description: How to get started using Azure Queue storage in a cloud service project in Visual Studio after connecting to a storage account using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: d0e6e3eab312f169b1d05ba16e2e293e103df1ec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552758"
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="56d48-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span><span class="sxs-lookup"><span data-stu-id="56d48-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="56d48-104">Overview</span><span class="sxs-lookup"><span data-stu-id="56d48-104">Overview</span></span>
<span data-ttu-id="56d48-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span><span class="sxs-lookup"><span data-stu-id="56d48-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="56d48-106">We'll show you how to create a queue in code.</span><span class="sxs-lookup"><span data-stu-id="56d48-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="56d48-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span><span class="sxs-lookup"><span data-stu-id="56d48-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="56d48-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="56d48-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="56d48-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span><span class="sxs-lookup"><span data-stu-id="56d48-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="56d48-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span><span class="sxs-lookup"><span data-stu-id="56d48-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="56d48-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="56d48-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="56d48-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span><span class="sxs-lookup"><span data-stu-id="56d48-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="56d48-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span><span class="sxs-lookup"><span data-stu-id="56d48-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="56d48-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="56d48-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="56d48-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span><span class="sxs-lookup"><span data-stu-id="56d48-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="56d48-116">Access queues in code</span><span class="sxs-lookup"><span data-stu-id="56d48-116">Access queues in code</span></span>
<span data-ttu-id="56d48-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span><span class="sxs-lookup"><span data-stu-id="56d48-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="56d48-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span><span class="sxs-lookup"><span data-stu-id="56d48-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="56d48-119">Get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="56d48-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="56d48-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span><span class="sxs-lookup"><span data-stu-id="56d48-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="56d48-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span><span class="sxs-lookup"><span data-stu-id="56d48-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="56d48-122">Get a **CloudQueue** object to reference a specific queue.</span><span class="sxs-lookup"><span data-stu-id="56d48-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="56d48-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span><span class="sxs-lookup"><span data-stu-id="56d48-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="56d48-124">Create a queue in code</span><span class="sxs-lookup"><span data-stu-id="56d48-124">Create a queue in code</span></span>
<span data-ttu-id="56d48-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="56d48-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="56d48-126">Add a message to a queue</span><span class="sxs-lookup"><span data-stu-id="56d48-126">Add a message to a queue</span></span>
<span data-ttu-id="56d48-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span><span class="sxs-lookup"><span data-stu-id="56d48-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="56d48-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span><span class="sxs-lookup"><span data-stu-id="56d48-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="56d48-129">Here is an example which inserts the message 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="56d48-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="56d48-130">Read a message in a queue</span><span class="sxs-lookup"><span data-stu-id="56d48-130">Read a message in a queue</span></span>
<span data-ttu-id="56d48-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span><span class="sxs-lookup"><span data-stu-id="56d48-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="56d48-132">Read and remove a message in a queue</span><span class="sxs-lookup"><span data-stu-id="56d48-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="56d48-133">Your code can remove (de-queue) a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="56d48-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="56d48-134">Call **GetMessage** to get the next message in a queue.</span><span class="sxs-lookup"><span data-stu-id="56d48-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="56d48-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="56d48-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="56d48-136">By default, this message stays invisible for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="56d48-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="56d48-137">To finish removing the message from the queue, call **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="56d48-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="56d48-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="56d48-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="56d48-139">The following code calls **DeleteMessage** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="56d48-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="56d48-140">Use additional options to process and remove queue messages</span><span class="sxs-lookup"><span data-stu-id="56d48-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="56d48-141">There are two ways you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="56d48-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="56d48-142">You can get a batch of messages (up to 32).</span><span class="sxs-lookup"><span data-stu-id="56d48-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="56d48-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="56d48-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="56d48-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="56d48-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="56d48-145">Then it processes each message using a **foreach** loop.</span><span class="sxs-lookup"><span data-stu-id="56d48-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="56d48-146">It also sets the invisibility timeout to five minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="56d48-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="56d48-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span><span class="sxs-lookup"><span data-stu-id="56d48-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="56d48-148">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="56d48-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="56d48-149">Get the queue length</span><span class="sxs-lookup"><span data-stu-id="56d48-149">Get the queue length</span></span>
<span data-ttu-id="56d48-150">You can get an estimate of the number of messages in a queue.</span><span class="sxs-lookup"><span data-stu-id="56d48-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="56d48-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span><span class="sxs-lookup"><span data-stu-id="56d48-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="56d48-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span><span class="sxs-lookup"><span data-stu-id="56d48-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="56d48-153">Use the Async-Await Pattern with common Azure Queue APIs</span><span class="sxs-lookup"><span data-stu-id="56d48-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="56d48-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span><span class="sxs-lookup"><span data-stu-id="56d48-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="56d48-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span><span class="sxs-lookup"><span data-stu-id="56d48-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="56d48-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span><span class="sxs-lookup"><span data-stu-id="56d48-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="56d48-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span><span class="sxs-lookup"><span data-stu-id="56d48-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="56d48-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="56d48-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="56d48-159">Delete a queue</span><span class="sxs-lookup"><span data-stu-id="56d48-159">Delete a queue</span></span>
<span data-ttu-id="56d48-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span><span class="sxs-lookup"><span data-stu-id="56d48-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="56d48-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="56d48-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

