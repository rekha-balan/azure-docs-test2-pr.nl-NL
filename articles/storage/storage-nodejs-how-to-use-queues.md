---
title: How to use Queue storage from Node.js | Microsoft Docs
description: Learn how to use the Azure Queue service to create and delete queues, and insert, get, and delete messages. Samples written in Node.js.
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: e30297bd0cc65105c92d6428035d2e6c156448af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553243"
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="c95bb-104">How to use Queue storage from Node.js</span><span class="sxs-lookup"><span data-stu-id="c95bb-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="c95bb-105">Overview</span><span class="sxs-lookup"><span data-stu-id="c95bb-105">Overview</span></span>
<span data-ttu-id="c95bb-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span><span class="sxs-lookup"><span data-stu-id="c95bb-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="c95bb-107">The samples are written using the Node.js API.</span><span class="sxs-lookup"><span data-stu-id="c95bb-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="c95bb-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="c95bb-109">Create a Node.js Application</span><span class="sxs-lookup"><span data-stu-id="c95bb-109">Create a Node.js Application</span></span>
<span data-ttu-id="c95bb-110">Create a blank Node.js application.</span><span class="sxs-lookup"><span data-stu-id="c95bb-110">Create a blank Node.js application.</span></span> <span data-ttu-id="c95bb-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="c95bb-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="c95bb-112">Configure Your Application to Access Storage</span><span class="sxs-lookup"><span data-stu-id="c95bb-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="c95bb-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="c95bb-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="c95bb-114">Use Node Package Manager (NPM) to obtain the package</span><span class="sxs-lookup"><span data-stu-id="c95bb-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="c95bb-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span><span class="sxs-lookup"><span data-stu-id="c95bb-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="c95bb-116">Type **npm install azure-storage** in the command window.</span><span class="sxs-lookup"><span data-stu-id="c95bb-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="c95bb-117">Output from the command is similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="c95bb-117">Output from the command is similar to the following example.</span></span>
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. <span data-ttu-id="c95bb-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="c95bb-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="c95bb-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span><span class="sxs-lookup"><span data-stu-id="c95bb-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="c95bb-120">Import the package</span><span class="sxs-lookup"><span data-stu-id="c95bb-120">Import the package</span></span>
<span data-ttu-id="c95bb-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span><span class="sxs-lookup"><span data-stu-id="c95bb-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="c95bb-122">Setup an Azure Storage Connection</span><span class="sxs-lookup"><span data-stu-id="c95bb-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="c95bb-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="c95bb-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="c95bb-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="c95bb-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span><span class="sxs-lookup"><span data-stu-id="c95bb-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c95bb-126">How To: Create a Queue</span><span class="sxs-lookup"><span data-stu-id="c95bb-126">How To: Create a Queue</span></span>
<span data-ttu-id="c95bb-127">The following code creates a **QueueService** object, which enables you to work with queues.</span><span class="sxs-lookup"><span data-stu-id="c95bb-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="c95bb-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="c95bb-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="c95bb-129">If the queue is created, `result.created` is true.</span><span class="sxs-lookup"><span data-stu-id="c95bb-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="c95bb-130">If the queue exists, `result.created` is false.</span><span class="sxs-lookup"><span data-stu-id="c95bb-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="c95bb-131">Filters</span><span class="sxs-lookup"><span data-stu-id="c95bb-131">Filters</span></span>
<span data-ttu-id="c95bb-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="c95bb-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span><span class="sxs-lookup"><span data-stu-id="c95bb-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="c95bb-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span><span class="sxs-lookup"><span data-stu-id="c95bb-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="c95bb-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span><span class="sxs-lookup"><span data-stu-id="c95bb-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="c95bb-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="c95bb-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="c95bb-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c95bb-138">How To: Insert a Message into a Queue</span><span class="sxs-lookup"><span data-stu-id="c95bb-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="c95bb-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span><span class="sxs-lookup"><span data-stu-id="c95bb-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="c95bb-140">How To: Peek at the Next Message</span><span class="sxs-lookup"><span data-stu-id="c95bb-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="c95bb-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span><span class="sxs-lookup"><span data-stu-id="c95bb-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="c95bb-142">By default, **peekMessages** peeks at a single message.</span><span class="sxs-lookup"><span data-stu-id="c95bb-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="c95bb-143">The `result` contains the message.</span><span class="sxs-lookup"><span data-stu-id="c95bb-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="c95bb-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span><span class="sxs-lookup"><span data-stu-id="c95bb-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="c95bb-145">How To: Dequeue the Next Message</span><span class="sxs-lookup"><span data-stu-id="c95bb-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="c95bb-146">Processing a message is a two-stage process:</span><span class="sxs-lookup"><span data-stu-id="c95bb-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="c95bb-147">Dequeue the message.</span><span class="sxs-lookup"><span data-stu-id="c95bb-147">Dequeue the message.</span></span>
2. <span data-ttu-id="c95bb-148">Delete the message.</span><span class="sxs-lookup"><span data-stu-id="c95bb-148">Delete the message.</span></span>

<span data-ttu-id="c95bb-149">To dequeue a message, use **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="c95bb-150">This makes the messages invisible in the queue, so no other clients can process them.</span><span class="sxs-lookup"><span data-stu-id="c95bb-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="c95bb-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span><span class="sxs-lookup"><span data-stu-id="c95bb-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="c95bb-152">The following example gets a message, then deletes it:</span><span class="sxs-lookup"><span data-stu-id="c95bb-152">The following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="c95bb-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span><span class="sxs-lookup"><span data-stu-id="c95bb-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="c95bb-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="c95bb-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span><span class="sxs-lookup"><span data-stu-id="c95bb-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="c95bb-156">How To: Change the Contents of a Queued Message</span><span class="sxs-lookup"><span data-stu-id="c95bb-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="c95bb-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="c95bb-158">The following example updates the text of a message:</span><span class="sxs-lookup"><span data-stu-id="c95bb-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="c95bb-159">How To: Additional Options for Dequeuing Messages</span><span class="sxs-lookup"><span data-stu-id="c95bb-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="c95bb-160">There are two ways you can customize message retrieval from a queue:</span><span class="sxs-lookup"><span data-stu-id="c95bb-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="c95bb-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span><span class="sxs-lookup"><span data-stu-id="c95bb-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="c95bb-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span><span class="sxs-lookup"><span data-stu-id="c95bb-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="c95bb-163">The following example uses the **getMessages** method to get 15 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="c95bb-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="c95bb-164">Then it processes each message using a for loop.</span><span class="sxs-lookup"><span data-stu-id="c95bb-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="c95bb-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span><span class="sxs-lookup"><span data-stu-id="c95bb-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="c95bb-166">How To: Get the Queue Length</span><span class="sxs-lookup"><span data-stu-id="c95bb-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="c95bb-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span><span class="sxs-lookup"><span data-stu-id="c95bb-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="c95bb-168">How To: List Queues</span><span class="sxs-lookup"><span data-stu-id="c95bb-168">How To: List Queues</span></span>
<span data-ttu-id="c95bb-169">To retrieve a list of queues, use **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="c95bb-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="c95bb-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span><span class="sxs-lookup"><span data-stu-id="c95bb-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c95bb-172">How To: Delete a Queue</span><span class="sxs-lookup"><span data-stu-id="c95bb-172">How To: Delete a Queue</span></span>
<span data-ttu-id="c95bb-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span><span class="sxs-lookup"><span data-stu-id="c95bb-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="c95bb-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="c95bb-175">How to: Work with Shared Access Signatures</span><span class="sxs-lookup"><span data-stu-id="c95bb-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="c95bb-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span><span class="sxs-lookup"><span data-stu-id="c95bb-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="c95bb-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span><span class="sxs-lookup"><span data-stu-id="c95bb-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="c95bb-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span><span class="sxs-lookup"><span data-stu-id="c95bb-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="c95bb-179">For example, a mobile app.</span><span class="sxs-lookup"><span data-stu-id="c95bb-179">For example, a mobile app.</span></span> <span data-ttu-id="c95bb-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span><span class="sxs-lookup"><span data-stu-id="c95bb-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="c95bb-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span><span class="sxs-lookup"><span data-stu-id="c95bb-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="c95bb-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span><span class="sxs-lookup"><span data-stu-id="c95bb-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="c95bb-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span><span class="sxs-lookup"><span data-stu-id="c95bb-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="c95bb-184">The following example connects to the queue and creates a message.</span><span class="sxs-lookup"><span data-stu-id="c95bb-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="c95bb-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span><span class="sxs-lookup"><span data-stu-id="c95bb-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="c95bb-186">Access control lists</span><span class="sxs-lookup"><span data-stu-id="c95bb-186">Access control lists</span></span>
<span data-ttu-id="c95bb-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span><span class="sxs-lookup"><span data-stu-id="c95bb-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="c95bb-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span><span class="sxs-lookup"><span data-stu-id="c95bb-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="c95bb-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span><span class="sxs-lookup"><span data-stu-id="c95bb-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="c95bb-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span><span class="sxs-lookup"><span data-stu-id="c95bb-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="c95bb-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="c95bb-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="c95bb-192">This approach allows:</span><span class="sxs-lookup"><span data-stu-id="c95bb-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="c95bb-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span><span class="sxs-lookup"><span data-stu-id="c95bb-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="c95bb-194">The following example creates a new SAS for 'user2':</span><span class="sxs-lookup"><span data-stu-id="c95bb-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="c95bb-195">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c95bb-195">Next Steps</span></span>
<span data-ttu-id="c95bb-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span><span class="sxs-lookup"><span data-stu-id="c95bb-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="c95bb-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="c95bb-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="c95bb-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="c95bb-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
