---
title: How to use Azure Service Bus topics with Python | Microsoft Docs
description: Learn how to use Azure Service Bus topics and subscriptions from Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 01/12/2017
ms.author: sethm
ms.openlocfilehash: 69f8807d509c31ae4aadeb16731fc481039a7e20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554157"
---
# <a name="how-to-use-service-bus-topics-and-subscriptions"></a><span data-ttu-id="1d1f7-103">How to use Service Bus topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="1d1f7-103">How to use Service Bus topics and subscriptions</span></span>
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="1d1f7-104">This article describes how to use Service Bus topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-104">This article describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="1d1f7-105">The samples are written in Python and use the [Python Azure package][Python Azure package].</span><span class="sxs-lookup"><span data-stu-id="1d1f7-105">The samples are written in Python and use the [Python Azure package][Python Azure package].</span></span> <span data-ttu-id="1d1f7-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="1d1f7-107">For more information about topics and subscriptions, see the [Next Steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-107">For more information about topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="1d1f7-108">If you need to install Python or the [Python Azure package][Python Azure package], please see the [Python Installation Guide](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="1d1f7-108">If you need to install Python or the [Python Azure package][Python Azure package], please see the [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="1d1f7-109">Create a topic</span><span class="sxs-lookup"><span data-stu-id="1d1f7-109">Create a topic</span></span>
<span data-ttu-id="1d1f7-110">The **ServiceBusService** object enables you to work with topics.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-110">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="1d1f7-111">Add the following near the top of any Python file in which you wish to programmatically access Service Bus:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-111">Add the following near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="1d1f7-112">The following code creates a **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-112">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="1d1f7-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="1d1f7-114">You can obtain the values for the SAS key name and value from the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="1d1f7-114">You can obtain the values for the SAS key name and value from the [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="1d1f7-115">**create\_topic** also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-115">**create\_topic** also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="1d1f7-116">The following example sets the maximum topic size to 5 GB, and a time to live (TTL) value of 1 minute:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-116">The following example sets the maximum topic size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="1d1f7-117">Create subscriptions</span><span class="sxs-lookup"><span data-stu-id="1d1f7-117">Create subscriptions</span></span>
<span data-ttu-id="1d1f7-118">Subscriptions to topics are also created with the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-118">Subscriptions to topics are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="1d1f7-119">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-119">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="1d1f7-120">Subscriptions are persistent and will continue to exist until either they, or the topic to which they are subscribed, are deleted.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-120">Subscriptions are persistent and will continue to exist until either they, or the topic to which they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="1d1f7-121">Create a subscription with the default (MatchAll) filter</span><span class="sxs-lookup"><span data-stu-id="1d1f7-121">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="1d1f7-122">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-122">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="1d1f7-123">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-123">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="1d1f7-124">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-124">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="1d1f7-125">Create subscriptions with filters</span><span class="sxs-lookup"><span data-stu-id="1d1f7-125">Create subscriptions with filters</span></span>
<span data-ttu-id="1d1f7-126">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific topic subscription.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-126">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="1d1f7-127">The most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-127">The most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="1d1f7-128">SQL filters operate on the properties of the messages that are published to the topic.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-128">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="1d1f7-129">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-129">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="1d1f7-130">You can add filters to a subscription by using the **create\_rule** method of the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-130">You can add filters to a subscription by using the **create\_rule** method of the **ServiceBusService** object.</span></span> <span data-ttu-id="1d1f7-131">This method allows you to add new filters to an existing subscription.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-131">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1d1f7-132">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-132">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="1d1f7-133">You can remove the default rule by using the **delete\_rule** method of the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-133">You can remove the default rule by using the **delete\_rule** method of the **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="1d1f7-134">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom **messagenumber** property greater than 3:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-134">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom **messagenumber** property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="1d1f7-135">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a **messagenumber** property less than or equal to 3:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-135">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a **messagenumber** property less than or equal to 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="1d1f7-136">Now, when a message is sent to `mytopic` it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span><span class="sxs-lookup"><span data-stu-id="1d1f7-136">Now, when a message is sent to `mytopic` it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="1d1f7-137">Send messages to a topic</span><span class="sxs-lookup"><span data-stu-id="1d1f7-137">Send messages to a topic</span></span>
<span data-ttu-id="1d1f7-138">To send a message to a Service Bus topic, your application must use the **send\_topic\_message** method of the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-138">To send a message to a Service Bus topic, your application must use the **send\_topic\_message** method of the **ServiceBusService** object.</span></span>

<span data-ttu-id="1d1f7-139">The following example demonstrates how to send five test messages to `mytopic`.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-139">The following example demonstrates how to send five test messages to `mytopic`.</span></span> <span data-ttu-id="1d1f7-140">Note that the **messagenumber** property value of each message varies on the iteration of the loop (this determines which subscriptions receive it):</span><span class="sxs-lookup"><span data-stu-id="1d1f7-140">Note that the **messagenumber** property value of each message varies on the iteration of the loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="1d1f7-141">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1d1f7-141">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1d1f7-142">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-142">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1d1f7-143">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-143">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="1d1f7-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="1d1f7-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="1d1f7-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="1d1f7-146">Receive messages from a subscription</span><span class="sxs-lookup"><span data-stu-id="1d1f7-146">Receive messages from a subscription</span></span>
<span data-ttu-id="1d1f7-147">Messages are received from a subscription using the **receive\_subscription\_message** method on the **ServiceBusService** object:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-147">Messages are received from a subscription using the **receive\_subscription\_message** method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="1d1f7-148">Messages are deleted from the subscription as they are read when the parameter **peek\_lock** is set to **False**.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-148">Messages are deleted from the subscription as they are read when the parameter **peek\_lock** is set to **False**.</span></span> <span data-ttu-id="1d1f7-149">You can read (peek) and lock the message without deleting it from the queue by setting the parameter **peek\_lock** to **True**.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-149">You can read (peek) and lock the message without deleting it from the queue by setting the parameter **peek\_lock** to **True**.</span></span>

<span data-ttu-id="1d1f7-150">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-150">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1d1f7-151">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-151">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="1d1f7-152">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-152">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1d1f7-153">If the **peek\_lock** parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-153">If the **peek\_lock** parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1d1f7-154">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-154">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1d1f7-155">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **delete** method on the **Message** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-155">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **delete** method on the **Message** object.</span></span> <span data-ttu-id="1d1f7-156">The **delete** method marks the message as being consumed and removes it from the subscription.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-156">The **delete** method marks the message as being consumed and removes it from the subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1d1f7-157">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="1d1f7-157">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="1d1f7-158">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-158">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1d1f7-159">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-159">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="1d1f7-160">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-160">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1d1f7-161">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-161">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="1d1f7-162">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-162">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="1d1f7-163">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-163">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1d1f7-164">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-164">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="1d1f7-165">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-165">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="1d1f7-166">Delete topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="1d1f7-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="1d1f7-167">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-167">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="1d1f7-168">The following example shows how to delete the topic named `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-168">The following example shows how to delete the topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="1d1f7-169">Deleting a topic also deletes any subscriptions that are registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-169">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="1d1f7-170">Subscriptions can also be deleted independently.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="1d1f7-171">The following code shows how to delete a subscription named `HighMessages` from the `mytopic` topic:</span><span class="sxs-lookup"><span data-stu-id="1d1f7-171">The following code shows how to delete a subscription named `HighMessages` from the `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="1d1f7-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d1f7-172">Next steps</span></span>
<span data-ttu-id="1d1f7-173">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="1d1f7-173">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="1d1f7-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="1d1f7-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="1d1f7-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="1d1f7-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[Service Bus quotas]: service-bus-quotas.md 
