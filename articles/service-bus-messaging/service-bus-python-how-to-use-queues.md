---
title: How to use Azure Service Bus queues with Python | Microsoft Docs
description: Learn how to use Azure Service Bus queues from Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 01/11/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: 775959d93105ca9fb28ce72e4ee4adf6b956e815
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549331"
---
# <a name="how-to-use-service-bus-queues"></a><span data-ttu-id="09551-103">How to use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="09551-103">How to use Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="09551-104">This article describes how to use Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="09551-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="09551-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="09551-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="09551-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="09551-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="09551-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="09551-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="09551-108">Create a queue</span><span class="sxs-lookup"><span data-stu-id="09551-108">Create a queue</span></span>
<span data-ttu-id="09551-109">The **ServiceBusService** object enables you to work with queues.</span><span class="sxs-lookup"><span data-stu-id="09551-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="09551-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span><span class="sxs-lookup"><span data-stu-id="09551-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="09551-111">The following code creates a **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="09551-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="09551-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span><span class="sxs-lookup"><span data-stu-id="09551-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="09551-113">The values for the SAS key name and value can be found in the [Azure classic portal][Azure classic portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span><span class="sxs-lookup"><span data-stu-id="09551-113">The values for the SAS key name and value can be found in the [Azure classic portal][Azure classic portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="09551-114">**create_queue** also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span><span class="sxs-lookup"><span data-stu-id="09551-114">**create_queue** also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="09551-115">The following example sets the maximum queue size to 5GB, and the TTL value to 1 minute:</span><span class="sxs-lookup"><span data-stu-id="09551-115">The following example sets the maximum queue size to 5GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="09551-116">Send messages to a queue</span><span class="sxs-lookup"><span data-stu-id="09551-116">Send messages to a queue</span></span>
<span data-ttu-id="09551-117">To send a message to a Service Bus queue, your application calls the **send\_queue\_message** method on the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="09551-117">To send a message to a Service Bus queue, your application calls the **send\_queue\_message** method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="09551-118">The following example demonstrates how to send a test message to the queue named *taskqueue using* **send\_queue\_message**:</span><span class="sxs-lookup"><span data-stu-id="09551-118">The following example demonstrates how to send a test message to the queue named *taskqueue using* **send\_queue\_message**:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="09551-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="09551-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="09551-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="09551-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="09551-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span><span class="sxs-lookup"><span data-stu-id="09551-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="09551-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="09551-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="09551-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="09551-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="09551-124">Receive messages from a queue</span><span class="sxs-lookup"><span data-stu-id="09551-124">Receive messages from a queue</span></span>
<span data-ttu-id="09551-125">Messages are received from a queue using the **receive\_queue\_message** method on the **ServiceBusService** object:</span><span class="sxs-lookup"><span data-stu-id="09551-125">Messages are received from a queue using the **receive\_queue\_message** method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="09551-126">Messages are deleted from the queue as they are read when the parameter **peek\_lock** is set to **False**.</span><span class="sxs-lookup"><span data-stu-id="09551-126">Messages are deleted from the queue as they are read when the parameter **peek\_lock** is set to **False**.</span></span> <span data-ttu-id="09551-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter **peek\_lock** to **True**.</span><span class="sxs-lookup"><span data-stu-id="09551-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter **peek\_lock** to **True**.</span></span>

<span data-ttu-id="09551-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="09551-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="09551-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="09551-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="09551-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="09551-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="09551-131">If the **peek\_lock** parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="09551-131">If the **peek\_lock** parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="09551-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="09551-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="09551-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span><span class="sxs-lookup"><span data-stu-id="09551-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="09551-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span><span class="sxs-lookup"><span data-stu-id="09551-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="09551-135">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="09551-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="09551-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="09551-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="09551-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span><span class="sxs-lookup"><span data-stu-id="09551-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="09551-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="09551-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="09551-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="09551-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="09551-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="09551-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="09551-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="09551-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="09551-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="09551-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="09551-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="09551-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09551-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="09551-144">Next steps</span></span>
<span data-ttu-id="09551-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span><span class="sxs-lookup"><span data-stu-id="09551-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="09551-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="09551-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure classic portal]: https://manage.windowsazure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

