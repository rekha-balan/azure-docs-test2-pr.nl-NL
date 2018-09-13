---
title: How to use Service Bus queues with PHP | Microsoft Docs
description: Learn how to use Service Bus queues in Azure. Code samples written in PHP.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 01/18/2017
ms.author: sethm
ms.openlocfilehash: c5db806969a6e018596c1ff0a0861423df19b61c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562722"
---
# <a name="how-to-use-service-bus-queues"></a><span data-ttu-id="dbd2a-104">How to use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="dbd2a-104">How to use Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="dbd2a-105">This guide shows you how to use Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="dbd2a-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="dbd2a-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="dbd2a-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="dbd2a-108">Create a PHP application</span><span class="sxs-lookup"><span data-stu-id="dbd2a-108">Create a PHP application</span></span>
<span data-ttu-id="dbd2a-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="dbd2a-110">You can use any development tools to create your application, or Notepad.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="dbd2a-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="dbd2a-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="dbd2a-113">Get the Azure client libraries</span><span class="sxs-lookup"><span data-stu-id="dbd2a-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="dbd2a-114">Configure your application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="dbd2a-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="dbd2a-115">To use the Service Bus queue APIs, do the following:</span><span class="sxs-lookup"><span data-stu-id="dbd2a-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="dbd2a-116">Reference the autoloader file using the [require_once][require_once] statement.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="dbd2a-117">Reference any classes you might use.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-117">Reference any classes you might use.</span></span>

<span data-ttu-id="dbd2a-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="dbd2a-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="dbd2a-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="dbd2a-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="dbd2a-122">Set up a Service Bus connection</span><span class="sxs-lookup"><span data-stu-id="dbd2a-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="dbd2a-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span><span class="sxs-lookup"><span data-stu-id="dbd2a-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedSecretIssuer=[Default Issuer];SharedSecretValue=[Default Key]
```

<span data-ttu-id="dbd2a-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="dbd2a-125">To create any Azure service client you must use the `ServicesBuilder` class.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="dbd2a-126">You can:</span><span class="sxs-lookup"><span data-stu-id="dbd2a-126">You can:</span></span>

* <span data-ttu-id="dbd2a-127">Pass the connection string directly to it.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="dbd2a-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span><span class="sxs-lookup"><span data-stu-id="dbd2a-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="dbd2a-129">By default it comes with support for one external source - environmental variables</span><span class="sxs-lookup"><span data-stu-id="dbd2a-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="dbd2a-130">You can add new sources by extending the `ConnectionStringSource` class</span><span class="sxs-lookup"><span data-stu-id="dbd2a-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="dbd2a-131">For the examples outlined here, the connection string will be passed directly.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-131">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedSecretIssuer=[Default Issuer];SharedSecretValue=[Default Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="dbd2a-132">How to: create a queue</span><span class="sxs-lookup"><span data-stu-id="dbd2a-132">How to: create a queue</span></span>
<span data-ttu-id="dbd2a-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="dbd2a-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="dbd2a-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span><span class="sxs-lookup"><span data-stu-id="dbd2a-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // http://msdn.microsoft.com/library/windowsazure/dd179357
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="dbd2a-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="how-to-send-messages-to-a-queue"></a><span data-ttu-id="dbd2a-137">How to: send messages to a queue</span><span class="sxs-lookup"><span data-stu-id="dbd2a-137">How to: send messages to a queue</span></span>
<span data-ttu-id="dbd2a-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="dbd2a-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // http://msdn.microsoft.com/library/windowsazure/hh780775
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="dbd2a-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="dbd2a-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="dbd2a-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="dbd2a-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="dbd2a-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="dbd2a-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="dbd2a-145">This upper limit on queue size is 5 GB.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-queue"></a><span data-ttu-id="dbd2a-146">How to receive messages from a queue</span><span class="sxs-lookup"><span data-stu-id="dbd2a-146">How to receive messages from a queue</span></span>
<span data-ttu-id="dbd2a-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="dbd2a-148">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="dbd2a-148">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="dbd2a-149">**PeekLock** is the default.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="dbd2a-150">When using [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-150">When using [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="dbd2a-151">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-151">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="dbd2a-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="dbd2a-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="dbd2a-154">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-154">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="dbd2a-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="dbd2a-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="dbd2a-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="dbd2a-158">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span><span class="sxs-lookup"><span data-stu-id="dbd2a-158">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/windowsazure/hh780735
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="dbd2a-159">How to: handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="dbd2a-159">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="dbd2a-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="dbd2a-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span><span class="sxs-lookup"><span data-stu-id="dbd2a-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="dbd2a-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="dbd2a-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="dbd2a-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="dbd2a-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="dbd2a-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="dbd2a-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbd2a-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbd2a-168">Next steps</span></span>
<span data-ttu-id="dbd2a-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span><span class="sxs-lookup"><span data-stu-id="dbd2a-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="dbd2a-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="dbd2a-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


