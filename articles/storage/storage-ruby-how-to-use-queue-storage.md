---
title: How to use Queue storage from Ruby | Microsoft Docs
description: Learn how to use the Azure Queue service to create and delete queues, and insert, get, and delete messages. Samples written in Ruby.
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: b978b65bb3b717362697a41510c5b2b4d057cf1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556326"
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="c5d34-104">How to use Queue storage from Ruby</span><span class="sxs-lookup"><span data-stu-id="c5d34-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c5d34-105">Overview</span><span class="sxs-lookup"><span data-stu-id="c5d34-105">Overview</span></span>
<span data-ttu-id="c5d34-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span><span class="sxs-lookup"><span data-stu-id="c5d34-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="c5d34-107">The samples are written using the Ruby Azure API.</span><span class="sxs-lookup"><span data-stu-id="c5d34-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="c5d34-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="c5d34-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="c5d34-109">Create a Ruby Application</span><span class="sxs-lookup"><span data-stu-id="c5d34-109">Create a Ruby Application</span></span>
<span data-ttu-id="c5d34-110">Create a Ruby application.</span><span class="sxs-lookup"><span data-stu-id="c5d34-110">Create a Ruby application.</span></span> <span data-ttu-id="c5d34-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="c5d34-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="c5d34-112">Configure Your Application to Access Storage</span><span class="sxs-lookup"><span data-stu-id="c5d34-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="c5d34-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="c5d34-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="c5d34-114">Use RubyGems to obtain the package</span><span class="sxs-lookup"><span data-stu-id="c5d34-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="c5d34-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="c5d34-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="c5d34-116">Type "gem install azure" in the command window to install the gem and dependencies.</span><span class="sxs-lookup"><span data-stu-id="c5d34-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="c5d34-117">Import the package</span><span class="sxs-lookup"><span data-stu-id="c5d34-117">Import the package</span></span>
<span data-ttu-id="c5d34-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span><span class="sxs-lookup"><span data-stu-id="c5d34-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="c5d34-119">Setup an Azure Storage Connection</span><span class="sxs-lookup"><span data-stu-id="c5d34-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="c5d34-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="c5d34-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="c5d34-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span><span class="sxs-lookup"><span data-stu-id="c5d34-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="c5d34-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="c5d34-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="c5d34-123">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5d34-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c5d34-124">Navigate to the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="c5d34-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="c5d34-125">In the Settings blade on the right, click **Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="c5d34-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="c5d34-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span><span class="sxs-lookup"><span data-stu-id="c5d34-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="c5d34-127">You can use either of these.</span><span class="sxs-lookup"><span data-stu-id="c5d34-127">You can use either of these.</span></span> 
5. <span data-ttu-id="c5d34-128">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="c5d34-128">Click the copy icon to copy the key to the clipboard.</span></span> 

<span data-ttu-id="c5d34-129">To obtain these values from a classic storage account in the classic Azure portal:</span><span class="sxs-lookup"><span data-stu-id="c5d34-129">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="c5d34-130">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c5d34-130">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c5d34-131">Navigate to the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="c5d34-131">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="c5d34-132">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span><span class="sxs-lookup"><span data-stu-id="c5d34-132">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="c5d34-133">In the pop up dialog, you'll see the storage account name, primary access key and secondary access key.</span><span class="sxs-lookup"><span data-stu-id="c5d34-133">In the pop up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="c5d34-134">For access key, you can use either the primary one or the secondary one.</span><span class="sxs-lookup"><span data-stu-id="c5d34-134">For access key, you can use either the primary one or the secondary one.</span></span> 
5. <span data-ttu-id="c5d34-135">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="c5d34-135">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c5d34-136">How To: Create a Queue</span><span class="sxs-lookup"><span data-stu-id="c5d34-136">How To: Create a Queue</span></span>
<span data-ttu-id="c5d34-137">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span><span class="sxs-lookup"><span data-stu-id="c5d34-137">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="c5d34-138">Use the **create_queue()** method to create a queue with the specified name.</span><span class="sxs-lookup"><span data-stu-id="c5d34-138">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c5d34-139">How To: Insert a Message into a Queue</span><span class="sxs-lookup"><span data-stu-id="c5d34-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="c5d34-140">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-140">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="c5d34-141">How To: Peek at the Next Message</span><span class="sxs-lookup"><span data-stu-id="c5d34-141">How To: Peek at the Next Message</span></span>
<span data-ttu-id="c5d34-142">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span><span class="sxs-lookup"><span data-stu-id="c5d34-142">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="c5d34-143">By default, **peek\_messages()** peeks at a single message.</span><span class="sxs-lookup"><span data-stu-id="c5d34-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="c5d34-144">You can also specify how many messages you want to peek.</span><span class="sxs-lookup"><span data-stu-id="c5d34-144">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="c5d34-145">How To: Dequeue the Next Message</span><span class="sxs-lookup"><span data-stu-id="c5d34-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="c5d34-146">You can remove a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="c5d34-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="c5d34-147">When you call **list\_messages()**, you get the next message in a queue by default.</span><span class="sxs-lookup"><span data-stu-id="c5d34-147">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="c5d34-148">You can also specify how many messages you want to get.</span><span class="sxs-lookup"><span data-stu-id="c5d34-148">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="c5d34-149">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-149">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="c5d34-150">You pass in the visibility timeout in seconds as a parameter.</span><span class="sxs-lookup"><span data-stu-id="c5d34-150">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="c5d34-151">To finish removing the message from the queue, you must also call **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="c5d34-151">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="c5d34-152">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="c5d34-152">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c5d34-153">Your code calls **delete\_message()** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="c5d34-153">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="c5d34-154">How To: Change the Contents of a Queued Message</span><span class="sxs-lookup"><span data-stu-id="c5d34-154">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="c5d34-155">You can change the contents of a message in-place in the queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-155">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="c5d34-156">The code below uses the **update_message()** method to update a message.</span><span class="sxs-lookup"><span data-stu-id="c5d34-156">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="c5d34-157">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-157">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="c5d34-158">How To: Additional Options for Dequeuing Messages</span><span class="sxs-lookup"><span data-stu-id="c5d34-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="c5d34-159">There are two ways you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="c5d34-160">You can get a batch of message.</span><span class="sxs-lookup"><span data-stu-id="c5d34-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="c5d34-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="c5d34-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="c5d34-162">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="c5d34-162">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="c5d34-163">Then it prints and deletes each message.</span><span class="sxs-lookup"><span data-stu-id="c5d34-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="c5d34-164">It also sets the invisibility timeout to five minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="c5d34-164">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="c5d34-165">How To: Get the Queue Length</span><span class="sxs-lookup"><span data-stu-id="c5d34-165">How To: Get the Queue Length</span></span>
<span data-ttu-id="c5d34-166">You can get an estimation of the number of messages in the queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-166">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="c5d34-167">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span><span class="sxs-lookup"><span data-stu-id="c5d34-167">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c5d34-168">How To: Delete a Queue</span><span class="sxs-lookup"><span data-stu-id="c5d34-168">How To: Delete a Queue</span></span>
<span data-ttu-id="c5d34-169">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span><span class="sxs-lookup"><span data-stu-id="c5d34-169">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="c5d34-170">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c5d34-170">Next Steps</span></span>
<span data-ttu-id="c5d34-171">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span><span class="sxs-lookup"><span data-stu-id="c5d34-171">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="c5d34-172">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="c5d34-172">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="c5d34-173">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="c5d34-173">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="c5d34-174">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="c5d34-174">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>