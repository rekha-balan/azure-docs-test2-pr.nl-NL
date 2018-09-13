---
title: Get started with Azure Queue storage using .NET | Microsoft Docs
description: Azure Queues provide reliable, asynchronous messaging between application components. Cloud messaging enables your application components to scale independently.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 5876a22651a5ebee2d60992cf08aeae54256fb7d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671040"
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="00bdf-104">Get started with Azure Queue storage using .NET</span><span class="sxs-lookup"><span data-stu-id="00bdf-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="00bdf-105">Overview</span><span class="sxs-lookup"><span data-stu-id="00bdf-105">Overview</span></span>
<span data-ttu-id="00bdf-106">Azure Queue storage provides cloud messaging between application components.</span><span class="sxs-lookup"><span data-stu-id="00bdf-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="00bdf-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span><span class="sxs-lookup"><span data-stu-id="00bdf-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="00bdf-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="00bdf-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="00bdf-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span><span class="sxs-lookup"><span data-stu-id="00bdf-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="00bdf-110">About this tutorial</span><span class="sxs-lookup"><span data-stu-id="00bdf-110">About this tutorial</span></span>
<span data-ttu-id="00bdf-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span><span class="sxs-lookup"><span data-stu-id="00bdf-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="00bdf-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span><span class="sxs-lookup"><span data-stu-id="00bdf-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="00bdf-113">**Estimated time to complete:** 45 minutes</span><span class="sxs-lookup"><span data-stu-id="00bdf-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="00bdf-114">**Prerequisities:**</span><span class="sxs-lookup"><span data-stu-id="00bdf-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="00bdf-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00bdf-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/en-us/visual-studio-homepage-vs.aspx)
* [<span data-ttu-id="00bdf-116">Azure Storage Client Library for .NET</span><span class="sxs-lookup"><span data-stu-id="00bdf-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="00bdf-117">Azure Configuration Manager for .NET</span><span class="sxs-lookup"><span data-stu-id="00bdf-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="00bdf-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="00bdf-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="00bdf-119">Add using directives</span><span class="sxs-lookup"><span data-stu-id="00bdf-119">Add using directives</span></span>
<span data-ttu-id="00bdf-120">Add the following `using` directives to the top of the `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="00bdf-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="00bdf-121">Parse the connection string</span><span class="sxs-lookup"><span data-stu-id="00bdf-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="00bdf-122">Create the Queue service client</span><span class="sxs-lookup"><span data-stu-id="00bdf-122">Create the Queue service client</span></span>
<span data-ttu-id="00bdf-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span><span class="sxs-lookup"><span data-stu-id="00bdf-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="00bdf-124">Here's one way to create the service client:</span><span class="sxs-lookup"><span data-stu-id="00bdf-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="00bdf-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span><span class="sxs-lookup"><span data-stu-id="00bdf-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="00bdf-126">Create a queue</span><span class="sxs-lookup"><span data-stu-id="00bdf-126">Create a queue</span></span>
<span data-ttu-id="00bdf-127">This example shows how to create a queue if it does not already exist:</span><span class="sxs-lookup"><span data-stu-id="00bdf-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="00bdf-128">Insert a message into a queue</span><span class="sxs-lookup"><span data-stu-id="00bdf-128">Insert a message into a queue</span></span>
<span data-ttu-id="00bdf-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="00bdf-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="00bdf-130">Next, call the **AddMessage** method.</span><span class="sxs-lookup"><span data-stu-id="00bdf-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="00bdf-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span><span class="sxs-lookup"><span data-stu-id="00bdf-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="00bdf-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="00bdf-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="00bdf-133">Peek at the next message</span><span class="sxs-lookup"><span data-stu-id="00bdf-133">Peek at the next message</span></span>
<span data-ttu-id="00bdf-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span><span class="sxs-lookup"><span data-stu-id="00bdf-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="00bdf-135">Change the contents of a queued message</span><span class="sxs-lookup"><span data-stu-id="00bdf-135">Change the contents of a queued message</span></span>
<span data-ttu-id="00bdf-136">You can change the contents of a message in-place in the queue.</span><span class="sxs-lookup"><span data-stu-id="00bdf-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="00bdf-137">If the message represents a work task, you could use this feature to update the status of the work task.</span><span class="sxs-lookup"><span data-stu-id="00bdf-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="00bdf-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="00bdf-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="00bdf-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span><span class="sxs-lookup"><span data-stu-id="00bdf-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="00bdf-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span><span class="sxs-lookup"><span data-stu-id="00bdf-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="00bdf-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span><span class="sxs-lookup"><span data-stu-id="00bdf-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="00bdf-142">This protects against a message that triggers an application error each time it is processed.</span><span class="sxs-lookup"><span data-stu-id="00bdf-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="00bdf-143">De-queue the next message</span><span class="sxs-lookup"><span data-stu-id="00bdf-143">De-queue the next message</span></span>
<span data-ttu-id="00bdf-144">Your code de-queues a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="00bdf-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="00bdf-145">When you call **GetMessage**, you get the next message in a queue.</span><span class="sxs-lookup"><span data-stu-id="00bdf-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="00bdf-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="00bdf-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="00bdf-147">By default, this message stays invisible for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="00bdf-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="00bdf-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="00bdf-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="00bdf-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="00bdf-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="00bdf-150">Your code calls **DeleteMessage** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="00bdf-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="00bdf-151">Use Async-Await pattern with common Queue storage APIs</span><span class="sxs-lookup"><span data-stu-id="00bdf-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="00bdf-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span><span class="sxs-lookup"><span data-stu-id="00bdf-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="00bdf-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span><span class="sxs-lookup"><span data-stu-id="00bdf-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="00bdf-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span><span class="sxs-lookup"><span data-stu-id="00bdf-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="00bdf-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span><span class="sxs-lookup"><span data-stu-id="00bdf-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="00bdf-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="00bdf-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="00bdf-157">Leverage additional options for de-queuing messages</span><span class="sxs-lookup"><span data-stu-id="00bdf-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="00bdf-158">There are two ways you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="00bdf-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="00bdf-159">First, you can get a batch of messages (up to 32).</span><span class="sxs-lookup"><span data-stu-id="00bdf-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="00bdf-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="00bdf-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="00bdf-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="00bdf-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="00bdf-162">Then it processes each message using a **foreach** loop.</span><span class="sxs-lookup"><span data-stu-id="00bdf-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="00bdf-163">It also sets the invisibility timeout to five minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="00bdf-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="00bdf-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span><span class="sxs-lookup"><span data-stu-id="00bdf-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="00bdf-165">Get the queue length</span><span class="sxs-lookup"><span data-stu-id="00bdf-165">Get the queue length</span></span>
<span data-ttu-id="00bdf-166">You can get an estimate of the number of messages in a queue.</span><span class="sxs-lookup"><span data-stu-id="00bdf-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="00bdf-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span><span class="sxs-lookup"><span data-stu-id="00bdf-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="00bdf-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span><span class="sxs-lookup"><span data-stu-id="00bdf-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="00bdf-169">Delete a queue</span><span class="sxs-lookup"><span data-stu-id="00bdf-169">Delete a queue</span></span>
<span data-ttu-id="00bdf-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span><span class="sxs-lookup"><span data-stu-id="00bdf-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="00bdf-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="00bdf-171">Next steps</span></span>
<span data-ttu-id="00bdf-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span><span class="sxs-lookup"><span data-stu-id="00bdf-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="00bdf-173">View the Queue service reference documentation for complete details about available APIs:</span><span class="sxs-lookup"><span data-stu-id="00bdf-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="00bdf-174">Storage Client Library for .NET reference</span><span class="sxs-lookup"><span data-stu-id="00bdf-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="00bdf-175">REST API reference</span><span class="sxs-lookup"><span data-stu-id="00bdf-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="00bdf-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="00bdf-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="00bdf-177">View more feature guides to learn about additional options for storing data in Azure.</span><span class="sxs-lookup"><span data-stu-id="00bdf-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="00bdf-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span><span class="sxs-lookup"><span data-stu-id="00bdf-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span></span>
  * <span data-ttu-id="00bdf-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span><span class="sxs-lookup"><span data-stu-id="00bdf-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="00bdf-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span><span class="sxs-lookup"><span data-stu-id="00bdf-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
