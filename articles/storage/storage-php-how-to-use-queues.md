---
title: How to use Queue storage from PHP | Microsoft Docs
description: Learn how to use the Azure Queue storage service to create and delete queues, and insert, get, and delete messages. Samples are written in PHP.
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549463"
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="a3510-104">How to use Queue storage from PHP</span><span class="sxs-lookup"><span data-stu-id="a3510-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="a3510-105">Overview</span><span class="sxs-lookup"><span data-stu-id="a3510-105">Overview</span></span>
<span data-ttu-id="a3510-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span><span class="sxs-lookup"><span data-stu-id="a3510-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="a3510-107">The samples are written via classes from the Windows SDK for PHP.</span><span class="sxs-lookup"><span data-stu-id="a3510-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="a3510-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span><span class="sxs-lookup"><span data-stu-id="a3510-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="a3510-109">Create a PHP application</span><span class="sxs-lookup"><span data-stu-id="a3510-109">Create a PHP application</span></span>
<span data-ttu-id="a3510-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span><span class="sxs-lookup"><span data-stu-id="a3510-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="a3510-111">You can use any development tools to create your application, including Notepad.</span><span class="sxs-lookup"><span data-stu-id="a3510-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="a3510-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span><span class="sxs-lookup"><span data-stu-id="a3510-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="a3510-113">Get the Azure Client Libraries</span><span class="sxs-lookup"><span data-stu-id="a3510-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="a3510-114">Configure your application to access Queue storage</span><span class="sxs-lookup"><span data-stu-id="a3510-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="a3510-115">To use the APIs for Azure Queue storage, you need to:</span><span class="sxs-lookup"><span data-stu-id="a3510-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="a3510-116">Reference the autoloader file by using the [require_once] statement.</span><span class="sxs-lookup"><span data-stu-id="a3510-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="a3510-117">Reference any classes that you might use.</span><span class="sxs-lookup"><span data-stu-id="a3510-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="a3510-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span><span class="sxs-lookup"><span data-stu-id="a3510-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="a3510-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="a3510-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="a3510-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span><span class="sxs-lookup"><span data-stu-id="a3510-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="a3510-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span><span class="sxs-lookup"><span data-stu-id="a3510-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="a3510-122">Set up an Azure storage connection</span><span class="sxs-lookup"><span data-stu-id="a3510-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="a3510-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span><span class="sxs-lookup"><span data-stu-id="a3510-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="a3510-124">The format for the queue service connection string is as follows.</span><span class="sxs-lookup"><span data-stu-id="a3510-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="a3510-125">For accessing a live service:</span><span class="sxs-lookup"><span data-stu-id="a3510-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="a3510-126">For accessing the emulator storage:</span><span class="sxs-lookup"><span data-stu-id="a3510-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="a3510-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span><span class="sxs-lookup"><span data-stu-id="a3510-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="a3510-128">You can use either of the following techniques:</span><span class="sxs-lookup"><span data-stu-id="a3510-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="a3510-129">Pass the connection string directly to it.</span><span class="sxs-lookup"><span data-stu-id="a3510-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="a3510-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span><span class="sxs-lookup"><span data-stu-id="a3510-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="a3510-131">By default, it comes with support for one external source—environmental variables.</span><span class="sxs-lookup"><span data-stu-id="a3510-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="a3510-132">You can add new sources by extending the **ConnectionStringSource** class.</span><span class="sxs-lookup"><span data-stu-id="a3510-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="a3510-133">For the examples outlined here, the connection string will be passed directly.</span><span class="sxs-lookup"><span data-stu-id="a3510-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="a3510-134">Create a queue</span><span class="sxs-lookup"><span data-stu-id="a3510-134">Create a queue</span></span>
<span data-ttu-id="a3510-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span><span class="sxs-lookup"><span data-stu-id="a3510-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="a3510-136">When creating a queue, you can set options on the queue, but doing so is not required.</span><span class="sxs-lookup"><span data-stu-id="a3510-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="a3510-137">(The example below shows how to set metadata on a queue.)</span><span class="sxs-lookup"><span data-stu-id="a3510-137">(The example below shows how to set metadata on a queue.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="a3510-138">You should not rely on case sensitivity for metadata keys.</span><span class="sxs-lookup"><span data-stu-id="a3510-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="a3510-139">All keys are read from the service in lowercase.</span><span class="sxs-lookup"><span data-stu-id="a3510-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="a3510-140">Add a message to a queue</span><span class="sxs-lookup"><span data-stu-id="a3510-140">Add a message to a queue</span></span>
<span data-ttu-id="a3510-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span><span class="sxs-lookup"><span data-stu-id="a3510-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="a3510-142">The method takes the queue name, the message text, and message options (which are optional).</span><span class="sxs-lookup"><span data-stu-id="a3510-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="a3510-143">Peek at the next message</span><span class="sxs-lookup"><span data-stu-id="a3510-143">Peek at the next message</span></span>
<span data-ttu-id="a3510-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="a3510-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="a3510-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span><span class="sxs-lookup"><span data-stu-id="a3510-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="a3510-146">De-queue the next message</span><span class="sxs-lookup"><span data-stu-id="a3510-146">De-queue the next message</span></span>
<span data-ttu-id="a3510-147">Your code removes a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="a3510-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="a3510-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span><span class="sxs-lookup"><span data-stu-id="a3510-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="a3510-149">By default, this message will stay invisible for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="a3510-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="a3510-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="a3510-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="a3510-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="a3510-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="a3510-152">Your code calls **deleteMessage** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="a3510-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="a3510-153">Change the contents of a queued message</span><span class="sxs-lookup"><span data-stu-id="a3510-153">Change the contents of a queued message</span></span>
<span data-ttu-id="a3510-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="a3510-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="a3510-155">If the message represents a work task, you could use this feature to update the status of the work task.</span><span class="sxs-lookup"><span data-stu-id="a3510-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="a3510-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="a3510-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="a3510-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span><span class="sxs-lookup"><span data-stu-id="a3510-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="a3510-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span><span class="sxs-lookup"><span data-stu-id="a3510-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="a3510-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span><span class="sxs-lookup"><span data-stu-id="a3510-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="a3510-160">This protects against a message that triggers an application error each time it is processed.</span><span class="sxs-lookup"><span data-stu-id="a3510-160">This protects against a message that triggers an application error each time it is processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="a3510-161">Additional options for de-queuing messages</span><span class="sxs-lookup"><span data-stu-id="a3510-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="a3510-162">There are two ways that you can customize message retrieval from a queue.</span><span class="sxs-lookup"><span data-stu-id="a3510-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="a3510-163">First, you can get a batch of messages (up to 32).</span><span class="sxs-lookup"><span data-stu-id="a3510-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="a3510-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span><span class="sxs-lookup"><span data-stu-id="a3510-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="a3510-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span><span class="sxs-lookup"><span data-stu-id="a3510-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="a3510-166">Then it processes each message by using a **for** loop.</span><span class="sxs-lookup"><span data-stu-id="a3510-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="a3510-167">It also sets the invisibility timeout to five minutes for each message.</span><span class="sxs-lookup"><span data-stu-id="a3510-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a><span data-ttu-id="a3510-168">Get queue length</span><span class="sxs-lookup"><span data-stu-id="a3510-168">Get queue length</span></span>
<span data-ttu-id="a3510-169">You can get an estimate of the number of messages in a queue.</span><span class="sxs-lookup"><span data-stu-id="a3510-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="a3510-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span><span class="sxs-lookup"><span data-stu-id="a3510-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="a3510-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span><span class="sxs-lookup"><span data-stu-id="a3510-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="a3510-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span><span class="sxs-lookup"><span data-stu-id="a3510-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a><span data-ttu-id="a3510-173">Delete a queue</span><span class="sxs-lookup"><span data-stu-id="a3510-173">Delete a queue</span></span>
<span data-ttu-id="a3510-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span><span class="sxs-lookup"><span data-stu-id="a3510-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="a3510-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3510-175">Next steps</span></span>
<span data-ttu-id="a3510-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span><span class="sxs-lookup"><span data-stu-id="a3510-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="a3510-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="a3510-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="a3510-178">For more information, see also the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a3510-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

