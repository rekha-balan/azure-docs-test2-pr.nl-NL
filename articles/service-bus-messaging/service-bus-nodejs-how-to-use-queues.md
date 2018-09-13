---
title: How to use Service Bus queues in Node.js | Microsoft Docs
description: Learn how to use Service Bus queues in Azure from a Node.js app.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/11/2017
ms.author: sethm
ms.openlocfilehash: 0fdf872b5b0b054a67a32992a5b495647be3fb67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553905"
---
# <a name="how-to-use-service-bus-queues"></a><span data-ttu-id="93ce8-103">How to use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="93ce8-103">How to use Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="93ce8-104">This article describes how to use Service Bus queues in Node.js.</span><span class="sxs-lookup"><span data-stu-id="93ce8-104">This article describes how to use Service Bus queues in Node.js.</span></span> <span data-ttu-id="93ce8-105">The samples are written in JavaScript and use the Node.js Azure module.</span><span class="sxs-lookup"><span data-stu-id="93ce8-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="93ce8-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="93ce8-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="93ce8-107">For more information on queues, see the [Next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="93ce8-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="93ce8-108">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="93ce8-108">Create a Node.js application</span></span>
<span data-ttu-id="93ce8-109">Create a blank Node.js application.</span><span class="sxs-lookup"><span data-stu-id="93ce8-109">Create a blank Node.js application.</span></span> <span data-ttu-id="93ce8-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93ce8-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="93ce8-111">Configure your application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="93ce8-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="93ce8-112">To use Azure Service Bus, download and use the Node.js Azure package.</span><span class="sxs-lookup"><span data-stu-id="93ce8-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="93ce8-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span><span class="sxs-lookup"><span data-stu-id="93ce8-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="93ce8-114">Use Node Package Manager (NPM) to obtain the package</span><span class="sxs-lookup"><span data-stu-id="93ce8-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="93ce8-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span><span class="sxs-lookup"><span data-stu-id="93ce8-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="93ce8-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="93ce8-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. <span data-ttu-id="93ce8-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="93ce8-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="93ce8-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="93ce8-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="93ce8-119">Import the module</span><span class="sxs-lookup"><span data-stu-id="93ce8-119">Import the module</span></span>
<span data-ttu-id="93ce8-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span><span class="sxs-lookup"><span data-stu-id="93ce8-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="93ce8-121">Set up an Azure Service Bus connection</span><span class="sxs-lookup"><span data-stu-id="93ce8-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="93ce8-122">The Azure module reads the environment variables AZURE\_SERVICEBUS\_NAMESPACE and AZURE\_SERVICEBUS\_ACCESS\_KEY to obtain information required to connect to Service Bus.</span><span class="sxs-lookup"><span data-stu-id="93ce8-122">The Azure module reads the environment variables AZURE\_SERVICEBUS\_NAMESPACE and AZURE\_SERVICEBUS\_ACCESS\_KEY to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="93ce8-123">If these environment variables are not set, you must specify the account information when calling **createServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="93ce8-123">If these environment variables are not set, you must specify the account information when calling **createServiceBusService**.</span></span>

<span data-ttu-id="93ce8-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="93ce8-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="93ce8-125">For an example of setting the environment variables in the [Azure classic portal][Azure classic portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="93ce8-125">For an example of setting the environment variables in the [Azure classic portal][Azure classic portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="93ce8-126">Create a queue</span><span class="sxs-lookup"><span data-stu-id="93ce8-126">Create a queue</span></span>
<span data-ttu-id="93ce8-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="93ce8-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="93ce8-128">The following code creates a **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="93ce8-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="93ce8-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span><span class="sxs-lookup"><span data-stu-id="93ce8-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="93ce8-130">By calling **createQueueIfNotExists** on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span><span class="sxs-lookup"><span data-stu-id="93ce8-130">By calling **createQueueIfNotExists** on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="93ce8-131">The following code uses **createQueueIfNotExists** to create or connect to the queue named `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="93ce8-131">The following code uses **createQueueIfNotExists** to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="93ce8-132">**createServiceBusService** also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span><span class="sxs-lookup"><span data-stu-id="93ce8-132">**createServiceBusService** also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="93ce8-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span><span class="sxs-lookup"><span data-stu-id="93ce8-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="93ce8-134">Filters</span><span class="sxs-lookup"><span data-stu-id="93ce8-134">Filters</span></span>
<span data-ttu-id="93ce8-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="93ce8-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="93ce8-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span><span class="sxs-lookup"><span data-stu-id="93ce8-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="93ce8-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span><span class="sxs-lookup"><span data-stu-id="93ce8-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="93ce8-138">In this callback, and after processing the **returnObject** (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span><span class="sxs-lookup"><span data-stu-id="93ce8-138">In this callback, and after processing the **returnObject** (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="93ce8-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="93ce8-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="93ce8-140">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="93ce8-140">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="93ce8-141">Send messages to a queue</span><span class="sxs-lookup"><span data-stu-id="93ce8-141">Send messages to a queue</span></span>
<span data-ttu-id="93ce8-142">To send a message to a Service Bus queue, your application calls the **sendQueueMessage** method on the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="93ce8-142">To send a message to a Service Bus queue, your application calls the **sendQueueMessage** method on the **ServiceBusService** object.</span></span> <span data-ttu-id="93ce8-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span><span class="sxs-lookup"><span data-stu-id="93ce8-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="93ce8-144">An application can set the body of the message by passing a string as the message.</span><span class="sxs-lookup"><span data-stu-id="93ce8-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="93ce8-145">Any required standard properties are populated with default values.</span><span class="sxs-lookup"><span data-stu-id="93ce8-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="93ce8-146">The following example demonstrates how to send a test message to the queue named `myqueue` using **sendQueueMessage**:</span><span class="sxs-lookup"><span data-stu-id="93ce8-146">The following example demonstrates how to send a test message to the queue named `myqueue` using **sendQueueMessage**:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="93ce8-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="93ce8-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="93ce8-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="93ce8-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="93ce8-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span><span class="sxs-lookup"><span data-stu-id="93ce8-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="93ce8-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="93ce8-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="93ce8-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="93ce8-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="93ce8-152">Receive messages from a queue</span><span class="sxs-lookup"><span data-stu-id="93ce8-152">Receive messages from a queue</span></span>
<span data-ttu-id="93ce8-153">Messages are received from a queue using the **receiveQueueMessage** method on the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="93ce8-153">Messages are received from a queue using the **receiveQueueMessage** method on the **ServiceBusService** object.</span></span> <span data-ttu-id="93ce8-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter **isPeekLock** to **true**.</span><span class="sxs-lookup"><span data-stu-id="93ce8-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter **isPeekLock** to **true**.</span></span>

<span data-ttu-id="93ce8-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="93ce8-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="93ce8-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="93ce8-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="93ce8-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="93ce8-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="93ce8-158">If the **isPeekLock** parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="93ce8-158">If the **isPeekLock** parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="93ce8-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="93ce8-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="93ce8-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span><span class="sxs-lookup"><span data-stu-id="93ce8-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="93ce8-161">The **deleteMessage** method will mark the message as being consumed and remove it from the queue.</span><span class="sxs-lookup"><span data-stu-id="93ce8-161">The **deleteMessage** method will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="93ce8-162">The following example demonstrates how to receive and process messages using **receiveQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="93ce8-162">The following example demonstrates how to receive and process messages using **receiveQueueMessage**.</span></span> <span data-ttu-id="93ce8-163">The example first receives and deletes a message, and then receives a message using **isPeekLock** set to **true**, then deletes the message using **deleteMessage**:</span><span class="sxs-lookup"><span data-stu-id="93ce8-163">The example first receives and deletes a message, and then receives a message using **isPeekLock** set to **true**, then deletes the message using **deleteMessage**:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="93ce8-164">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="93ce8-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="93ce8-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="93ce8-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="93ce8-166">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="93ce8-166">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the **ServiceBusService** object.</span></span> <span data-ttu-id="93ce8-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="93ce8-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="93ce8-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="93ce8-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="93ce8-169">In the event that the application crashes after processing the message but before the **deleteMessage** method is called, then the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="93ce8-169">In the event that the application crashes after processing the message but before the **deleteMessage** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="93ce8-170">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="93ce8-170">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="93ce8-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="93ce8-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="93ce8-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="93ce8-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93ce8-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="93ce8-173">Next steps</span></span>
<span data-ttu-id="93ce8-174">To learn more about queues, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="93ce8-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="93ce8-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="93ce8-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="93ce8-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="93ce8-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="93ce8-177">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="93ce8-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure classic portal]: http://manage.windowsazure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../storage/storage-nodejs-use-table-storage-cloud-service-app.md
[Node.js Web Application with Storage]: ../storage/storage-nodejs-how-to-use-table-storage.md
[Service Bus quotas]: service-bus-quotas.md
