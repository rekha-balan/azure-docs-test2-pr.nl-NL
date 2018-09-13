---
title: How to use Azure Service Bus topics with Java | Microsoft Docs
description: Learn how to use Service Bus topics and subscriptions in Azure. Code samples are written for Java applications.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 03/23/2017
ms.author: sethm
ms.openlocfilehash: 5fd912d7213938334c7784d1c20ebd9f5c3d878f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564018"
---
# <a name="how-to-use-service-bus-topics-and-subscriptions"></a><span data-ttu-id="5a887-104">How to use Service Bus topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="5a887-104">How to use Service Bus topics and subscriptions</span></span>
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="5a887-105">This guide describes how to use Service Bus topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5a887-105">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="5a887-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="5a887-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="5a887-107">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="5a887-107">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="5a887-108">What are Service Bus topics and subscriptions?</span><span class="sxs-lookup"><span data-stu-id="5a887-108">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="5a887-109">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span><span class="sxs-lookup"><span data-stu-id="5a887-109">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="5a887-110">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span><span class="sxs-lookup"><span data-stu-id="5a887-110">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="5a887-112">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span><span class="sxs-lookup"><span data-stu-id="5a887-112">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="5a887-113">It is possible to register multiple subscriptions to a topic.</span><span class="sxs-lookup"><span data-stu-id="5a887-113">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="5a887-114">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span><span class="sxs-lookup"><span data-stu-id="5a887-114">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="5a887-115">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span><span class="sxs-lookup"><span data-stu-id="5a887-115">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="5a887-116">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5a887-116">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="5a887-117">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span><span class="sxs-lookup"><span data-stu-id="5a887-117">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="5a887-118">Create a service namespace</span><span class="sxs-lookup"><span data-stu-id="5a887-118">Create a service namespace</span></span>
<span data-ttu-id="5a887-119">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span><span class="sxs-lookup"><span data-stu-id="5a887-119">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="5a887-120">To create a namespace:</span><span class="sxs-lookup"><span data-stu-id="5a887-120">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="5a887-121">Configure your application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="5a887-121">Configure your application to use Service Bus</span></span>
<span data-ttu-id="5a887-122">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span><span class="sxs-lookup"><span data-stu-id="5a887-122">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="5a887-123">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span><span class="sxs-lookup"><span data-stu-id="5a887-123">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="5a887-124">You can then add the **Microsoft Azure Libraries for Java** to your project:</span><span class="sxs-lookup"><span data-stu-id="5a887-124">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="5a887-125">Add the following `import` statements to the top of the Java file:</span><span class="sxs-lookup"><span data-stu-id="5a887-125">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="5a887-126">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span><span class="sxs-lookup"><span data-stu-id="5a887-126">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="5a887-127">Create a topic</span><span class="sxs-lookup"><span data-stu-id="5a887-127">Create a topic</span></span>
<span data-ttu-id="5a887-128">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span><span class="sxs-lookup"><span data-stu-id="5a887-128">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="5a887-129">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span><span class="sxs-lookup"><span data-stu-id="5a887-129">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="5a887-130">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span><span class="sxs-lookup"><span data-stu-id="5a887-130">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="5a887-131">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="5a887-131">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="5a887-132">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span><span class="sxs-lookup"><span data-stu-id="5a887-132">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="5a887-133">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span><span class="sxs-lookup"><span data-stu-id="5a887-133">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="5a887-134">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span><span class="sxs-lookup"><span data-stu-id="5a887-134">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="5a887-135">Create subscriptions</span><span class="sxs-lookup"><span data-stu-id="5a887-135">Create subscriptions</span></span>
<span data-ttu-id="5a887-136">Subscriptions to topics are also created with the **ServiceBusService** class.</span><span class="sxs-lookup"><span data-stu-id="5a887-136">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="5a887-137">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="5a887-137">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="5a887-138">Create a subscription with the default (MatchAll) filter</span><span class="sxs-lookup"><span data-stu-id="5a887-138">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="5a887-139">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span><span class="sxs-lookup"><span data-stu-id="5a887-139">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="5a887-140">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="5a887-140">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="5a887-141">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="5a887-141">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="5a887-142">Create subscriptions with filters</span><span class="sxs-lookup"><span data-stu-id="5a887-142">Create subscriptions with filters</span></span>
<span data-ttu-id="5a887-143">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span><span class="sxs-lookup"><span data-stu-id="5a887-143">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="5a887-144">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span><span class="sxs-lookup"><span data-stu-id="5a887-144">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="5a887-145">SQL filters operate on the properties of the messages that are published to the topic.</span><span class="sxs-lookup"><span data-stu-id="5a887-145">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="5a887-146">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span><span class="sxs-lookup"><span data-stu-id="5a887-146">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="5a887-147">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span><span class="sxs-lookup"><span data-stu-id="5a887-147">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="5a887-148">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span><span class="sxs-lookup"><span data-stu-id="5a887-148">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="5a887-149">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span><span class="sxs-lookup"><span data-stu-id="5a887-149">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="5a887-150">Send messages to a topic</span><span class="sxs-lookup"><span data-stu-id="5a887-150">Send messages to a topic</span></span>
<span data-ttu-id="5a887-151">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="5a887-151">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a887-152">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span><span class="sxs-lookup"><span data-stu-id="5a887-152">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="5a887-153">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span><span class="sxs-lookup"><span data-stu-id="5a887-153">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5a887-154">[BrokeredMessage][BrokeredMessage]\* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span><span class="sxs-lookup"><span data-stu-id="5a887-154">[BrokeredMessage][BrokeredMessage]\* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="5a887-155">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span><span class="sxs-lookup"><span data-stu-id="5a887-155">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="5a887-156">Alternatively, a **java.io.InputStream** can be provided.</span><span class="sxs-lookup"><span data-stu-id="5a887-156">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="5a887-157">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span><span class="sxs-lookup"><span data-stu-id="5a887-157">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="5a887-158">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span><span class="sxs-lookup"><span data-stu-id="5a887-158">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="5a887-159">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5a887-159">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5a887-160">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="5a887-160">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5a887-161">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span><span class="sxs-lookup"><span data-stu-id="5a887-161">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="5a887-162">This topic size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="5a887-162">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="5a887-163">How to receive messages from a subscription</span><span class="sxs-lookup"><span data-stu-id="5a887-163">How to receive messages from a subscription</span></span>
<span data-ttu-id="5a887-164">To receive messages from a subscription, use a **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="5a887-164">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a887-165">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="5a887-165">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="5a887-166">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="5a887-166">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="5a887-167">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="5a887-167">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="5a887-168">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="5a887-168">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="5a887-169">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="5a887-169">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="5a887-170">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="5a887-170">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5a887-171">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="5a887-171">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="5a887-172">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span><span class="sxs-lookup"><span data-stu-id="5a887-172">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="5a887-173">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span><span class="sxs-lookup"><span data-stu-id="5a887-173">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="5a887-174">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span><span class="sxs-lookup"><span data-stu-id="5a887-174">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="5a887-175">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span><span class="sxs-lookup"><span data-stu-id="5a887-175">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5a887-176">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="5a887-176">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="5a887-177">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="5a887-177">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5a887-178">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span><span class="sxs-lookup"><span data-stu-id="5a887-178">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="5a887-179">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="5a887-179">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5a887-180">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="5a887-180">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="5a887-181">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="5a887-181">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="5a887-182">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="5a887-182">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="5a887-183">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="5a887-183">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="5a887-184">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="5a887-184">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="5a887-185">Delete topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="5a887-185">Delete topics and subscriptions</span></span>
<span data-ttu-id="5a887-186">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="5a887-186">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a887-187">Deleting a topic will also delete any subscriptions that are registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="5a887-187">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="5a887-188">Subscriptions can also be deleted independently.</span><span class="sxs-lookup"><span data-stu-id="5a887-188">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="5a887-189">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5a887-189">Next Steps</span></span>
<span data-ttu-id="5a887-190">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span><span class="sxs-lookup"><span data-stu-id="5a887-190">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png





