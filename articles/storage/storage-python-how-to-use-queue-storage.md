---
title: How to use Queue storage from Python | Microsoft Docs
description: Learn how to use the Azure Queue service from Python to create and delete queues, and insert, get, and delete messages.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 1ad3ba6853edda93034b84996823262cb017c71a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553204"
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="c9b89-103">How to use Queue storage from Python</span><span class="sxs-lookup"><span data-stu-id="c9b89-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c9b89-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c9b89-104">Overview</span></span>
<span data-ttu-id="c9b89-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span><span class="sxs-lookup"><span data-stu-id="c9b89-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="c9b89-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span><span class="sxs-lookup"><span data-stu-id="c9b89-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="c9b89-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="c9b89-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="c9b89-108">For more information on queues, refer to the [Next Steps] section.</span><span class="sxs-lookup"><span data-stu-id="c9b89-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c9b89-109">How To: Create a Queue</span><span class="sxs-lookup"><span data-stu-id="c9b89-109">How To: Create a Queue</span></span>
<span data-ttu-id="c9b89-110">The **QueueService** object lets you work with queues.</span><span class="sxs-lookup"><span data-stu-id="c9b89-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="c9b89-111">The following code creates a **QueueService** object.</span><span class="sxs-lookup"><span data-stu-id="c9b89-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="c9b89-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="c9b89-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="c9b89-113">The following code creates a **QueueService** object using the storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="c9b89-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="c9b89-114">Replace 'myaccount' and 'mykey' with your account name and key.</span><span class="sxs-lookup"><span data-stu-id="c9b89-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c9b89-115">How To: Insert a Message into a Queue</span><span class="sxs-lookup"><span data-stu-id="c9b89-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="c9b89-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span><span class="sxs-lookup"><span data-stu-id="c9b89-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="c9b89-117">How To: Peek at the Next Message</span><span class="sxs-lookup"><span data-stu-id="c9b89-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="c9b89-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span><span class="sxs-lookup"><span data-stu-id="c9b89-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="c9b89-119">By default, **peek\_messages** peeks at a single message.</span><span class="sxs-lookup"><span data-stu-id="c9b89-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="c9b89-120">How To: Dequeue Messages</span><span class="sxs-lookup"><span data-stu-id="c9b89-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="c9b89-121">Your code removes a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="c9b89-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="c9b89-122">When you call **get\_messages**, you get the next message in a queue by default.</span><span class="sxs-lookup"><span data-stu-id="c9b89-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="c9b89-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="c9b89-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="c9b89-124">By default, this message stays invisible for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="c9b89-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="c9b89-125">To finish removing the message from the queue, you must also call **delete\_message**.</span><span class="sxs-lookup"><span data-stu-id="c9b89-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="c9b89-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="c9b89-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c9b89-127">Your code calls **delete\_message** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="c9b89-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="c9b89-128">There are two ways you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="c9b89-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="c9b89-129">First, you can get a batch of messages (up to 32).</span><span class="sxs-lookup"><span data-stu-id="c9b89-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="c9b89-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="c9b89-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="c9b89-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="c9b89-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="c9b89-132">Then it processes each message using a for loop.</span><span class="sxs-lookup"><span data-stu-id="c9b89-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="c9b89-133">It also sets the invisibility timeout to five minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="c9b89-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="c9b89-134">How To: Change the Contents of a Queued Message</span><span class="sxs-lookup"><span data-stu-id="c9b89-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="c9b89-135">You can change the contents of a message in-place in the queue.</span><span class="sxs-lookup"><span data-stu-id="c9b89-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="c9b89-136">If the message represents a work task, you could use this feature to update the status of the work task.</span><span class="sxs-lookup"><span data-stu-id="c9b89-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="c9b89-137">The code below uses the **update\_message** method to update a message.</span><span class="sxs-lookup"><span data-stu-id="c9b89-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="c9b89-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span><span class="sxs-lookup"><span data-stu-id="c9b89-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="c9b89-139">How To: Get the Queue Length</span><span class="sxs-lookup"><span data-stu-id="c9b89-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="c9b89-140">You can get an estimate of the number of messages in a queue.</span><span class="sxs-lookup"><span data-stu-id="c9b89-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="c9b89-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="c9b89-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="c9b89-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span><span class="sxs-lookup"><span data-stu-id="c9b89-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c9b89-143">How To: Delete a Queue</span><span class="sxs-lookup"><span data-stu-id="c9b89-143">How To: Delete a Queue</span></span>
<span data-ttu-id="c9b89-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span><span class="sxs-lookup"><span data-stu-id="c9b89-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="c9b89-145">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c9b89-145">Next Steps</span></span>
<span data-ttu-id="c9b89-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="c9b89-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="c9b89-147">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="c9b89-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="c9b89-148">Azure Storage Services REST API</span><span class="sxs-lookup"><span data-stu-id="c9b89-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="c9b89-149">[Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="c9b89-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="c9b89-150">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="c9b89-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python