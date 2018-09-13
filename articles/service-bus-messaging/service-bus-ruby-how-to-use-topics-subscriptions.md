---
title: How to use Service Bus topics (Ruby) | Microsoft Docs
description: Learn how to use Service Bus topics and subscriptions in Azure. Code samples are written for Ruby applications.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 01/11/2017
ms.author: sethm
ms.openlocfilehash: c083d8ac0d16de40de4a2a9908cdcf2e02ed3d6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555202"
---
# <a name="how-to-use-service-bus-topicssubscriptions"></a><span data-ttu-id="f52ea-104">How to Use Service Bus Topics/Subscriptions</span><span class="sxs-lookup"><span data-stu-id="f52ea-104">How to Use Service Bus Topics/Subscriptions</span></span>
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="f52ea-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span><span class="sxs-lookup"><span data-stu-id="f52ea-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="f52ea-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="f52ea-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="f52ea-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="f52ea-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="f52ea-108">Create a Ruby application</span><span class="sxs-lookup"><span data-stu-id="f52ea-108">Create a Ruby application</span></span>
<span data-ttu-id="f52ea-109">For instructions, see [Create a Ruby Application on Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="f52ea-109">For instructions, see [Create a Ruby Application on Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="f52ea-110">Configure Your application to Use Service Bus</span><span class="sxs-lookup"><span data-stu-id="f52ea-110">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="f52ea-111">To use Service Bus, download and use the Ruby Azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="f52ea-111">To use Service Bus, download and use the Ruby Azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="f52ea-112">Use RubyGems to obtain the package</span><span class="sxs-lookup"><span data-stu-id="f52ea-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="f52ea-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="f52ea-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="f52ea-114">Type "gem install azure" in the command window to install the gem and dependencies.</span><span class="sxs-lookup"><span data-stu-id="f52ea-114">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="f52ea-115">Import the package</span><span class="sxs-lookup"><span data-stu-id="f52ea-115">Import the package</span></span>
<span data-ttu-id="f52ea-116">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span><span class="sxs-lookup"><span data-stu-id="f52ea-116">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="f52ea-117">Set up a Service Bus connection</span><span class="sxs-lookup"><span data-stu-id="f52ea-117">Set up a Service Bus connection</span></span>
<span data-ttu-id="f52ea-118">The Azure module reads the environment variables **AZURE\_SERVICEBUS\_NAMESPACE** and **AZURE\_SERVICEBUS\_ACCESS\_KEY** for information required to connect to your namespace.</span><span class="sxs-lookup"><span data-stu-id="f52ea-118">The Azure module reads the environment variables **AZURE\_SERVICEBUS\_NAMESPACE** and **AZURE\_SERVICEBUS\_ACCESS\_KEY** for information required to connect to your namespace.</span></span> <span data-ttu-id="f52ea-119">If these environment variables are not set, you must specify the namespace information before using **Azure::ServiceBusService** with the following code:</span><span class="sxs-lookup"><span data-stu-id="f52ea-119">If these environment variables are not set, you must specify the namespace information before using **Azure::ServiceBusService** with the following code:</span></span>

```ruby
Azure.config.sb_namespace = "<your azure service bus namespace>"
Azure.config.sb_access_key = "<your azure service bus access key>"
```

<span data-ttu-id="f52ea-120">Set the namespace value to the value you created rather than the entire URL.</span><span class="sxs-lookup"><span data-stu-id="f52ea-120">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="f52ea-121">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="f52ea-121">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="f52ea-122">Create a topic</span><span class="sxs-lookup"><span data-stu-id="f52ea-122">Create a topic</span></span>
<span data-ttu-id="f52ea-123">The **Azure::ServiceBusService** object enables you to work with topics.</span><span class="sxs-lookup"><span data-stu-id="f52ea-123">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="f52ea-124">The following code creates an **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-124">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="f52ea-125">To create a topic, use the **create\_topic()** method.</span><span class="sxs-lookup"><span data-stu-id="f52ea-125">To create a topic, use the **create\_topic()** method.</span></span> <span data-ttu-id="f52ea-126">The following example creates a topic or prints out the errors if there are any.</span><span class="sxs-lookup"><span data-stu-id="f52ea-126">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBusService.new
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="f52ea-127">You can also pass a **Azure::ServiceBus::Topic** object with additional options, which allow you to override default topic settings such as message time to live or maximum queue size.</span><span class="sxs-lookup"><span data-stu-id="f52ea-127">You can also pass a **Azure::ServiceBus::Topic** object with additional options, which allow you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="f52ea-128">The following example shows setting the maximum queue size to 5GB and time to live to 1 minute:</span><span class="sxs-lookup"><span data-stu-id="f52ea-128">The following example shows setting the maximum queue size to 5GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="f52ea-129">Create subscriptions</span><span class="sxs-lookup"><span data-stu-id="f52ea-129">Create subscriptions</span></span>
<span data-ttu-id="f52ea-130">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-130">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="f52ea-131">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="f52ea-131">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="f52ea-132">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span><span class="sxs-lookup"><span data-stu-id="f52ea-132">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="f52ea-133">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span><span class="sxs-lookup"><span data-stu-id="f52ea-133">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="f52ea-134">Create a subscription with the default (MatchAll) filter</span><span class="sxs-lookup"><span data-stu-id="f52ea-134">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="f52ea-135">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span><span class="sxs-lookup"><span data-stu-id="f52ea-135">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="f52ea-136">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="f52ea-136">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="f52ea-137">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="f52ea-137">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="f52ea-138">Create subscriptions with filters</span><span class="sxs-lookup"><span data-stu-id="f52ea-138">Create subscriptions with filters</span></span>
<span data-ttu-id="f52ea-139">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span><span class="sxs-lookup"><span data-stu-id="f52ea-139">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="f52ea-140">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span><span class="sxs-lookup"><span data-stu-id="f52ea-140">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="f52ea-141">SQL filters operate on the properties of the messages that are published to the topic.</span><span class="sxs-lookup"><span data-stu-id="f52ea-141">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="f52ea-142">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression](http://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx) syntax.</span><span class="sxs-lookup"><span data-stu-id="f52ea-142">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression](http://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx) syntax.</span></span>

<span data-ttu-id="f52ea-143">You can add filters to a subscription by using the **create\_rule()** method of the **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-143">You can add filters to a subscription by using the **create\_rule()** method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="f52ea-144">This method enables you to add new filters to an existing subscription.</span><span class="sxs-lookup"><span data-stu-id="f52ea-144">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="f52ea-145">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span><span class="sxs-lookup"><span data-stu-id="f52ea-145">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="f52ea-146">You can remove the default rule by using the **delete\_rule()** method on the **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-146">You can remove the default rule by using the **delete\_rule()** method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="f52ea-147">The following example creates a subscription named "high-messages" with a **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom **message\_number** property greater than 3:</span><span class="sxs-lookup"><span data-stu-id="f52ea-147">The following example creates a subscription named "high-messages" with a **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom **message\_number** property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="f52ea-148">Similarly, the following example creates a subscription named "low-messages" with a **Azure::ServiceBus::SqlFilter** that only selects messages that have a **message_number** property less than or equal to 3:</span><span class="sxs-lookup"><span data-stu-id="f52ea-148">Similarly, the following example creates a subscription named "low-messages" with a **Azure::ServiceBus::SqlFilter** that only selects messages that have a **message_number** property less than or equal to 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="f52ea-149">When a message is now sent to "test-topic", it is always be delivered to receivers subscribed to the "all-messages" topic subscription, and selectively delivered to receivers subscribed to the "high-messages" and "low-messages" topic subscriptions (depending upon the message content).</span><span class="sxs-lookup"><span data-stu-id="f52ea-149">When a message is now sent to "test-topic", it is always be delivered to receivers subscribed to the "all-messages" topic subscription, and selectively delivered to receivers subscribed to the "high-messages" and "low-messages" topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="f52ea-150">Send messages to a topic</span><span class="sxs-lookup"><span data-stu-id="f52ea-150">Send messages to a topic</span></span>
<span data-ttu-id="f52ea-151">To send a message to a Service Bus topic, your application must use the **send\_topic\_message()** method on the **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-151">To send a message to a Service Bus topic, your application must use the **send\_topic\_message()** method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="f52ea-152">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span><span class="sxs-lookup"><span data-stu-id="f52ea-152">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="f52ea-153">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as **label** and **time\_to\_live**), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span><span class="sxs-lookup"><span data-stu-id="f52ea-153">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as **label** and **time\_to\_live**), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="f52ea-154">An application can set the body of the message by passing a string value to the **send\_topic\_message()** method and any required standard properties will be populated by default values.</span><span class="sxs-lookup"><span data-stu-id="f52ea-154">An application can set the body of the message by passing a string value to the **send\_topic\_message()** method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="f52ea-155">The following example demonstrates how to send five test messages to "test-topic".</span><span class="sxs-lookup"><span data-stu-id="f52ea-155">The following example demonstrates how to send five test messages to "test-topic".</span></span> <span data-ttu-id="f52ea-156">Note that the **message_number** custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span><span class="sxs-lookup"><span data-stu-id="f52ea-156">Note that the **message_number** custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="f52ea-157">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="f52ea-157">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="f52ea-158">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="f52ea-158">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="f52ea-159">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span><span class="sxs-lookup"><span data-stu-id="f52ea-159">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="f52ea-160">This topic size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="f52ea-160">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="f52ea-161">Receive messages from a subscription</span><span class="sxs-lookup"><span data-stu-id="f52ea-161">Receive messages from a subscription</span></span>
<span data-ttu-id="f52ea-162">Messages are received from a subscription using the **receive\_subscription\_message()** method on the **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-162">Messages are received from a subscription using the **receive\_subscription\_message()** method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="f52ea-163">By default, messages are read(peak) and locked without deleting it from the subscription.</span><span class="sxs-lookup"><span data-stu-id="f52ea-163">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="f52ea-164">You can read and delete the message from the subscription by setting the **peek\_lock** option to **false**.</span><span class="sxs-lookup"><span data-stu-id="f52ea-164">You can read and delete the message from the subscription by setting the **peek\_lock** option to **false**.</span></span>

<span data-ttu-id="f52ea-165">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="f52ea-165">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="f52ea-166">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="f52ea-166">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="f52ea-167">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **delete\_subscription\_message()** method and providing the message to be deleted as a parameter.</span><span class="sxs-lookup"><span data-stu-id="f52ea-167">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **delete\_subscription\_message()** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="f52ea-168">The **delete\_subscription\_message()** method will mark the message as being consumed and remove it from the subscription.</span><span class="sxs-lookup"><span data-stu-id="f52ea-168">The **delete\_subscription\_message()** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="f52ea-169">If the **:peek\_lock** parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="f52ea-169">If the **:peek\_lock** parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="f52ea-170">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="f52ea-170">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="f52ea-171">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="f52ea-171">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="f52ea-172">The following example demonstrates how messages can be received and processed using **receive\_subscription\_message()**.</span><span class="sxs-lookup"><span data-stu-id="f52ea-172">The following example demonstrates how messages can be received and processed using **receive\_subscription\_message()**.</span></span> <span data-ttu-id="f52ea-173">The example first receives and deletes a message from the "low-messages" subscription by using **:peek\_lock** set to **false**, then it receives another message from the "high-messages" and then deletes the message using **delete\_subscription\_message()**:</span><span class="sxs-lookup"><span data-stu-id="f52ea-173">The example first receives and deletes a message from the "low-messages" subscription by using **:peek\_lock** set to **false**, then it receives another message from the "high-messages" and then deletes the message using **delete\_subscription\_message()**:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="f52ea-174">Handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="f52ea-174">Handle application crashes and unreadable messages</span></span>
<span data-ttu-id="f52ea-175">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="f52ea-175">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="f52ea-176">If a receiver application is unable to process the message for some reason, then it can call the **unlock\_subscription\_message()** method on the **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="f52ea-176">If a receiver application is unable to process the message for some reason, then it can call the **unlock\_subscription\_message()** method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="f52ea-177">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="f52ea-177">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="f52ea-178">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="f52ea-178">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="f52ea-179">In the event that the application crashes after processing the message but before the **delete\_subscription\_message()** method is called, then the message is redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="f52ea-179">In the event that the application crashes after processing the message but before the **delete\_subscription\_message()** method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="f52ea-180">This is often called **At Least Once Processing**; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="f52ea-180">This is often called **At Least Once Processing**; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="f52ea-181">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="f52ea-181">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="f52ea-182">This logic is often achieved using the **message\_id** property of the message, which will remain constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="f52ea-182">This logic is often achieved using the **message\_id** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="f52ea-183">Delete topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="f52ea-183">Delete topics and subscriptions</span></span>
<span data-ttu-id="f52ea-184">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span><span class="sxs-lookup"><span data-stu-id="f52ea-184">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="f52ea-185">The example below demonstrates how to delete the topic named "test-topic".</span><span class="sxs-lookup"><span data-stu-id="f52ea-185">The example below demonstrates how to delete the topic named "test-topic".</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="f52ea-186">Deleting a topic also deletes any subscriptions that are registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="f52ea-186">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="f52ea-187">Subscriptions can also be deleted independently.</span><span class="sxs-lookup"><span data-stu-id="f52ea-187">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="f52ea-188">The following code demonstrates how to delete the subscription named "high-messages" from the "test-topic" topic:</span><span class="sxs-lookup"><span data-stu-id="f52ea-188">The following code demonstrates how to delete the subscription named "high-messages" from the "test-topic" topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="f52ea-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="f52ea-189">Next steps</span></span>
<span data-ttu-id="f52ea-190">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="f52ea-190">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="f52ea-191">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="f52ea-191">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="f52ea-192">API reference for [SqlFilter](http://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sqlfilter.aspx).</span><span class="sxs-lookup"><span data-stu-id="f52ea-192">API reference for [SqlFilter](http://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sqlfilter.aspx).</span></span>
* <span data-ttu-id="f52ea-193">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f52ea-193">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
