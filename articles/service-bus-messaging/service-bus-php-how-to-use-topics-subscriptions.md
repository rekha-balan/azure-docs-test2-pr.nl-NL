---
title: How to use Service Bus topics with PHP | Microsoft Docs
description: Learn how to use Service Bus topics with PHP in Azure.
services: service-bus-messaging
documentationcenter: php
author: spelluru
manager: timlt
editor: ''
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/06/2017
ms.author: spelluru
ms.openlocfilehash: 9901b485b97ecde2de889796fc682db3ee30c544
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828581"
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="6bc88-103">How to use Service Bus topics and subscriptions with PHP</span><span class="sxs-lookup"><span data-stu-id="6bc88-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="6bc88-104">This article shows you how to use Service Bus topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="6bc88-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="6bc88-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6bc88-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="6bc88-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="6bc88-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="6bc88-107">Create a PHP application</span><span class="sxs-lookup"><span data-stu-id="6bc88-107">Create a PHP application</span></span>
<span data-ttu-id="6bc88-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span><span class="sxs-lookup"><span data-stu-id="6bc88-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="6bc88-109">You can use any development tools to create your application, or Notepad.</span><span class="sxs-lookup"><span data-stu-id="6bc88-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc88-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span><span class="sxs-lookup"><span data-stu-id="6bc88-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="6bc88-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span><span class="sxs-lookup"><span data-stu-id="6bc88-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="6bc88-112">Get the Azure client libraries</span><span class="sxs-lookup"><span data-stu-id="6bc88-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="6bc88-113">Configure your application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="6bc88-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="6bc88-114">To use the Service Bus APIs:</span><span class="sxs-lookup"><span data-stu-id="6bc88-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="6bc88-115">Reference the autoloader file using the [require_once][require-once] statement.</span><span class="sxs-lookup"><span data-stu-id="6bc88-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="6bc88-116">Reference any classes you might use.</span><span class="sxs-lookup"><span data-stu-id="6bc88-116">Reference any classes you might use.</span></span>

<span data-ttu-id="6bc88-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span><span class="sxs-lookup"><span data-stu-id="6bc88-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc88-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="6bc88-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="6bc88-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span><span class="sxs-lookup"><span data-stu-id="6bc88-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="6bc88-120">In the following examples, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span><span class="sxs-lookup"><span data-stu-id="6bc88-120">In the following examples, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="6bc88-121">Set up a Service Bus connection</span><span class="sxs-lookup"><span data-stu-id="6bc88-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="6bc88-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span><span class="sxs-lookup"><span data-stu-id="6bc88-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="6bc88-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="6bc88-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="6bc88-124">To create any Azure service client you must use the `ServicesBuilder` class.</span><span class="sxs-lookup"><span data-stu-id="6bc88-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="6bc88-125">You can:</span><span class="sxs-lookup"><span data-stu-id="6bc88-125">You can:</span></span>

* <span data-ttu-id="6bc88-126">Pass the connection string directly to it.</span><span class="sxs-lookup"><span data-stu-id="6bc88-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="6bc88-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span><span class="sxs-lookup"><span data-stu-id="6bc88-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="6bc88-128">By default it comes with support for one external source - environmental variables.</span><span class="sxs-lookup"><span data-stu-id="6bc88-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="6bc88-129">You can add new sources by extending the `ConnectionStringSource` class.</span><span class="sxs-lookup"><span data-stu-id="6bc88-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="6bc88-130">For the examples outlined here, the connection string is passed directly.</span><span class="sxs-lookup"><span data-stu-id="6bc88-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="6bc88-131">Create a topic</span><span class="sxs-lookup"><span data-stu-id="6bc88-131">Create a topic</span></span>
<span data-ttu-id="6bc88-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span><span class="sxs-lookup"><span data-stu-id="6bc88-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="6bc88-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span><span class="sxs-lookup"><span data-stu-id="6bc88-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="6bc88-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span><span class="sxs-lookup"><span data-stu-id="6bc88-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="6bc88-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span><span class="sxs-lookup"><span data-stu-id="6bc88-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="6bc88-136">Create a subscription</span><span class="sxs-lookup"><span data-stu-id="6bc88-136">Create a subscription</span></span>
<span data-ttu-id="6bc88-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span><span class="sxs-lookup"><span data-stu-id="6bc88-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="6bc88-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="6bc88-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="6bc88-139">Create a subscription with the default (MatchAll) filter</span><span class="sxs-lookup"><span data-stu-id="6bc88-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="6bc88-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span><span class="sxs-lookup"><span data-stu-id="6bc88-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="6bc88-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="6bc88-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="6bc88-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="6bc88-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="6bc88-143">Create subscriptions with filters</span><span class="sxs-lookup"><span data-stu-id="6bc88-143">Create subscriptions with filters</span></span>
<span data-ttu-id="6bc88-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span><span class="sxs-lookup"><span data-stu-id="6bc88-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="6bc88-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span><span class="sxs-lookup"><span data-stu-id="6bc88-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="6bc88-146">SQL filters operate on the properties of the messages that are published to the topic.</span><span class="sxs-lookup"><span data-stu-id="6bc88-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="6bc88-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="6bc88-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="6bc88-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span><span class="sxs-lookup"><span data-stu-id="6bc88-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="6bc88-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span><span class="sxs-lookup"><span data-stu-id="6bc88-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="6bc88-150">To receive only messages matching your filter, you must remove the default rule.</span><span class="sxs-lookup"><span data-stu-id="6bc88-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="6bc88-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span><span class="sxs-lookup"><span data-stu-id="6bc88-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="6bc88-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span><span class="sxs-lookup"><span data-stu-id="6bc88-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="6bc88-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span><span class="sxs-lookup"><span data-stu-id="6bc88-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="6bc88-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="6bc88-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="6bc88-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span><span class="sxs-lookup"><span data-stu-id="6bc88-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="6bc88-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span><span class="sxs-lookup"><span data-stu-id="6bc88-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="6bc88-157">Send messages to a topic</span><span class="sxs-lookup"><span data-stu-id="6bc88-157">Send messages to a topic</span></span>
<span data-ttu-id="6bc88-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span><span class="sxs-lookup"><span data-stu-id="6bc88-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="6bc88-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span><span class="sxs-lookup"><span data-stu-id="6bc88-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="6bc88-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span><span class="sxs-lookup"><span data-stu-id="6bc88-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="6bc88-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span><span class="sxs-lookup"><span data-stu-id="6bc88-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="6bc88-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span><span class="sxs-lookup"><span data-stu-id="6bc88-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="6bc88-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span><span class="sxs-lookup"><span data-stu-id="6bc88-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="6bc88-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span><span class="sxs-lookup"><span data-stu-id="6bc88-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="6bc88-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="6bc88-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="6bc88-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6bc88-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="6bc88-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span><span class="sxs-lookup"><span data-stu-id="6bc88-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="6bc88-168">This upper limit on topic size is 5 GB.</span><span class="sxs-lookup"><span data-stu-id="6bc88-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="6bc88-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="6bc88-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="6bc88-170">Receive messages from a subscription</span><span class="sxs-lookup"><span data-stu-id="6bc88-170">Receive messages from a subscription</span></span>
<span data-ttu-id="6bc88-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span><span class="sxs-lookup"><span data-stu-id="6bc88-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="6bc88-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="6bc88-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="6bc88-173">**PeekLock** is the default.</span><span class="sxs-lookup"><span data-stu-id="6bc88-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="6bc88-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="6bc88-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="6bc88-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) \* mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="6bc88-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) \* mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="6bc88-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="6bc88-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="6bc88-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="6bc88-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="6bc88-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="6bc88-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="6bc88-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="6bc88-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="6bc88-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="6bc88-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="6bc88-181">When Service Bus sees the `deleteMessage` call, it marks the message as being consumed and remove it from the queue.</span><span class="sxs-lookup"><span data-stu-id="6bc88-181">When Service Bus sees the `deleteMessage` call, it marks the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="6bc88-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span><span class="sxs-lookup"><span data-stu-id="6bc88-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="6bc88-183">How to: handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="6bc88-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="6bc88-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="6bc88-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="6bc88-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span><span class="sxs-lookup"><span data-stu-id="6bc88-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="6bc88-186">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="6bc88-186">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="6bc88-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and make it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="6bc88-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="6bc88-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message is redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="6bc88-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="6bc88-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="6bc88-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="6bc88-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="6bc88-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="6bc88-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="6bc88-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="6bc88-192">Delete topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="6bc88-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="6bc88-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span><span class="sxs-lookup"><span data-stu-id="6bc88-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="6bc88-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="6bc88-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="6bc88-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span><span class="sxs-lookup"><span data-stu-id="6bc88-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="6bc88-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span><span class="sxs-lookup"><span data-stu-id="6bc88-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="6bc88-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="6bc88-197">Next steps</span></span>
<span data-ttu-id="6bc88-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span><span class="sxs-lookup"><span data-stu-id="6bc88-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
