---
title: How to use queue storage (C++) | Microsoft Docs
description: Learn how to use the queue storage service in Azure. Samples are written in C++.
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: f924611a707abba76e31860e8168417f1d9ebaab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550468"
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="ebb38-104">How to use Queue Storage from C++</span><span class="sxs-lookup"><span data-stu-id="ebb38-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="ebb38-105">Overview</span><span class="sxs-lookup"><span data-stu-id="ebb38-105">Overview</span></span>
<span data-ttu-id="ebb38-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span><span class="sxs-lookup"><span data-stu-id="ebb38-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="ebb38-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="ebb38-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="ebb38-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="ebb38-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="ebb38-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span><span class="sxs-lookup"><span data-stu-id="ebb38-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="ebb38-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="ebb38-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="ebb38-111">Create a C++ application</span><span class="sxs-lookup"><span data-stu-id="ebb38-111">Create a C++ application</span></span>
<span data-ttu-id="ebb38-112">In this guide, you will use storage features which can be run within a C++ application.</span><span class="sxs-lookup"><span data-stu-id="ebb38-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="ebb38-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ebb38-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="ebb38-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span><span class="sxs-lookup"><span data-stu-id="ebb38-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="ebb38-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="ebb38-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="ebb38-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="ebb38-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="ebb38-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="ebb38-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="ebb38-118">Configure your application to access Queue Storage</span><span class="sxs-lookup"><span data-stu-id="ebb38-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="ebb38-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span><span class="sxs-lookup"><span data-stu-id="ebb38-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="ebb38-120">Set up an Azure storage connection string</span><span class="sxs-lookup"><span data-stu-id="ebb38-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="ebb38-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span><span class="sxs-lookup"><span data-stu-id="ebb38-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="ebb38-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span><span class="sxs-lookup"><span data-stu-id="ebb38-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="ebb38-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ebb38-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="ebb38-124">This example shows how you can declare a static field to hold the connection string:</span><span class="sxs-lookup"><span data-stu-id="ebb38-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="ebb38-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ebb38-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="ebb38-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span><span class="sxs-lookup"><span data-stu-id="ebb38-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="ebb38-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span><span class="sxs-lookup"><span data-stu-id="ebb38-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="ebb38-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span><span class="sxs-lookup"><span data-stu-id="ebb38-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="ebb38-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span><span class="sxs-lookup"><span data-stu-id="ebb38-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="ebb38-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span><span class="sxs-lookup"><span data-stu-id="ebb38-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="ebb38-131">Retrieve your connection string</span><span class="sxs-lookup"><span data-stu-id="ebb38-131">Retrieve your connection string</span></span>
<span data-ttu-id="ebb38-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span><span class="sxs-lookup"><span data-stu-id="ebb38-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="ebb38-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span><span class="sxs-lookup"><span data-stu-id="ebb38-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="ebb38-134">How to: Create a queue</span><span class="sxs-lookup"><span data-stu-id="ebb38-134">How to: Create a queue</span></span>
<span data-ttu-id="ebb38-135">A **cloud_queue_client** object lets you get reference objects for queues.</span><span class="sxs-lookup"><span data-stu-id="ebb38-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="ebb38-136">The following code creates a **cloud_queue_client** object.</span><span class="sxs-lookup"><span data-stu-id="ebb38-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="ebb38-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span><span class="sxs-lookup"><span data-stu-id="ebb38-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="ebb38-138">You can create the queue if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="ebb38-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="ebb38-139">How to: Insert a message into a queue</span><span class="sxs-lookup"><span data-stu-id="ebb38-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="ebb38-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="ebb38-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="ebb38-141">Next, call the **add_message** method.</span><span class="sxs-lookup"><span data-stu-id="ebb38-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="ebb38-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span><span class="sxs-lookup"><span data-stu-id="ebb38-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="ebb38-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="ebb38-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="ebb38-144">How to: Peek at the next message</span><span class="sxs-lookup"><span data-stu-id="ebb38-144">How to: Peek at the next message</span></span>
<span data-ttu-id="ebb38-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span><span class="sxs-lookup"><span data-stu-id="ebb38-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="ebb38-146">How to: Change the contents of a queued message</span><span class="sxs-lookup"><span data-stu-id="ebb38-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="ebb38-147">You can change the contents of a message in-place in the queue.</span><span class="sxs-lookup"><span data-stu-id="ebb38-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="ebb38-148">If the message represents a work task, you could use this feature to update the status of the work task.</span><span class="sxs-lookup"><span data-stu-id="ebb38-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="ebb38-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="ebb38-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="ebb38-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span><span class="sxs-lookup"><span data-stu-id="ebb38-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="ebb38-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span><span class="sxs-lookup"><span data-stu-id="ebb38-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="ebb38-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span><span class="sxs-lookup"><span data-stu-id="ebb38-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="ebb38-153">This protects against a message that triggers an application error each time it is processed.</span><span class="sxs-lookup"><span data-stu-id="ebb38-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="ebb38-154">How to: De-queue the next message</span><span class="sxs-lookup"><span data-stu-id="ebb38-154">How to: De-queue the next message</span></span>
<span data-ttu-id="ebb38-155">Your code de-queues a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="ebb38-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="ebb38-156">When you call **get_message**, you get the next message in a queue.</span><span class="sxs-lookup"><span data-stu-id="ebb38-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="ebb38-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="ebb38-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="ebb38-158">To finish removing the message from the queue, you must also call **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="ebb38-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="ebb38-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="ebb38-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="ebb38-160">Your code calls **delete_message** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="ebb38-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="ebb38-161">How to: Leverage additional options for de-queuing messages</span><span class="sxs-lookup"><span data-stu-id="ebb38-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="ebb38-162">There are two ways you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="ebb38-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="ebb38-163">First, you can get a batch of messages (up to 32).</span><span class="sxs-lookup"><span data-stu-id="ebb38-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="ebb38-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="ebb38-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="ebb38-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="ebb38-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="ebb38-166">Then it processes each message using a **for** loop.</span><span class="sxs-lookup"><span data-stu-id="ebb38-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="ebb38-167">It also sets the invisibility timeout to five minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="ebb38-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="ebb38-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span><span class="sxs-lookup"><span data-stu-id="ebb38-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="ebb38-169">How to: Get the queue length</span><span class="sxs-lookup"><span data-stu-id="ebb38-169">How to: Get the queue length</span></span>
<span data-ttu-id="ebb38-170">You can get an estimate of the number of messages in a queue.</span><span class="sxs-lookup"><span data-stu-id="ebb38-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="ebb38-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span><span class="sxs-lookup"><span data-stu-id="ebb38-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="ebb38-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span><span class="sxs-lookup"><span data-stu-id="ebb38-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="ebb38-173">How to: Delete a queue</span><span class="sxs-lookup"><span data-stu-id="ebb38-173">How to: Delete a queue</span></span>
<span data-ttu-id="ebb38-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span><span class="sxs-lookup"><span data-stu-id="ebb38-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="ebb38-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="ebb38-175">Next steps</span></span>
<span data-ttu-id="ebb38-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ebb38-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="ebb38-177">How to use Blob Storage from C++</span><span class="sxs-lookup"><span data-stu-id="ebb38-177">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="ebb38-178">How to use Table Storage from C++</span><span class="sxs-lookup"><span data-stu-id="ebb38-178">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="ebb38-179">List Azure Storage Resources in C++</span><span class="sxs-lookup"><span data-stu-id="ebb38-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="ebb38-180">Storage Client Library for C++ Reference</span><span class="sxs-lookup"><span data-stu-id="ebb38-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="ebb38-181">Azure Storage Documentation</span><span class="sxs-lookup"><span data-stu-id="ebb38-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)