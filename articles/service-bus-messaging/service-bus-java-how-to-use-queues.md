---
title: How to use Azure Service Bus queues with Java | Microsoft Docs
description: Learn how to use Service Bus queues in Azure. Code samples written in Java.
services: service-bus-messaging
documentationcenter: java
author: spelluru
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: e4099c8228e9434276242a3c49ebcb4fc2e995b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819382"
---
# <a name="how-to-use-service-bus-queues-with-java"></a><span data-ttu-id="1549c-104">How to use Service Bus queues with Java</span><span class="sxs-lookup"><span data-stu-id="1549c-104">How to use Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="1549c-105">This article describes how to use Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="1549c-105">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="1549c-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="1549c-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="1549c-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span><span class="sxs-lookup"><span data-stu-id="1549c-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="1549c-108">Configure your application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="1549c-108">Configure your application to use Service Bus</span></span>
<span data-ttu-id="1549c-109">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span><span class="sxs-lookup"><span data-stu-id="1549c-109">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="1549c-110">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span><span class="sxs-lookup"><span data-stu-id="1549c-110">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="1549c-111">You can then add the **Microsoft Azure Libraries for Java** to your project:</span><span class="sxs-lookup"><span data-stu-id="1549c-111">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="1549c-112">Add the following `import` statements to the top of the Java file:</span><span class="sxs-lookup"><span data-stu-id="1549c-112">Add the following `import` statements to the top of the Java file:</span></span>

```java
// Include the following imports to use Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="1549c-113">Create a queue</span><span class="sxs-lookup"><span data-stu-id="1549c-113">Create a queue</span></span>
<span data-ttu-id="1549c-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span><span class="sxs-lookup"><span data-stu-id="1549c-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="1549c-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span><span class="sxs-lookup"><span data-stu-id="1549c-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="1549c-116">The **ServiceBusService** class provides methods to create, enumerate, and delete queues.</span><span class="sxs-lookup"><span data-stu-id="1549c-116">The **ServiceBusService** class provides methods to create, enumerate, and delete queues.</span></span> <span data-ttu-id="1549c-117">The example below shows how a **ServiceBusService** object can be used to create a queue named `TestQueue`, with a namespace named `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="1549c-117">The example below shows how a **ServiceBusService** object can be used to create a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="1549c-118">There are methods on `QueueInfo` that allow properties of the queue to be tuned (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the queue).</span><span class="sxs-lookup"><span data-stu-id="1549c-118">There are methods on `QueueInfo` that allow properties of the queue to be tuned (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the queue).</span></span> <span data-ttu-id="1549c-119">The following example shows how to create a queue named `TestQueue` with a maximum size of 5GB:</span><span class="sxs-lookup"><span data-stu-id="1549c-119">The following example shows how to create a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="1549c-120">Note that you can use the `listQueues` method on **ServiceBusContract** objects to check if a queue with a specified name already exists within a service namespace.</span><span class="sxs-lookup"><span data-stu-id="1549c-120">Note that you can use the `listQueues` method on **ServiceBusContract** objects to check if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="1549c-121">Send messages to a queue</span><span class="sxs-lookup"><span data-stu-id="1549c-121">Send messages to a queue</span></span>
<span data-ttu-id="1549c-122">To send a message to a Service Bus queue, your application obtains a **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="1549c-122">To send a message to a Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="1549c-123">The following code shows how to send a message for the `TestQueue` queue previously created in the `HowToSample` namespace:</span><span class="sxs-lookup"><span data-stu-id="1549c-123">The following code shows how to send a message for the `TestQueue` queue previously created in the `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="1549c-124">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span><span class="sxs-lookup"><span data-stu-id="1549c-124">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="1549c-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span><span class="sxs-lookup"><span data-stu-id="1549c-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="1549c-126">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate serializer will then be used to serialize the object.</span><span class="sxs-lookup"><span data-stu-id="1549c-126">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate serializer will then be used to serialize the object.</span></span> <span data-ttu-id="1549c-127">Alternatively, you can provide a **java.IO.InputStream** object.</span><span class="sxs-lookup"><span data-stu-id="1549c-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="1549c-128">The following example demonstrates how to send five test messages to the `TestQueue` **MessageSender** we obtained in the previous code snippet:</span><span class="sxs-lookup"><span data-stu-id="1549c-128">The following example demonstrates how to send five test messages to the `TestQueue` **MessageSender** we obtained in the previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for the body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message to the queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="1549c-129">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1549c-129">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1549c-130">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1549c-130">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1549c-131">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span><span class="sxs-lookup"><span data-stu-id="1549c-131">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="1549c-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="1549c-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="1549c-133">Receive messages from a queue</span><span class="sxs-lookup"><span data-stu-id="1549c-133">Receive messages from a queue</span></span>
<span data-ttu-id="1549c-134">The primary way to receive messages from a queue is to use a **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="1549c-134">The primary way to receive messages from a queue is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="1549c-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="1549c-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="1549c-136">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="1549c-136">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="1549c-137">**ReceiveAndDelete** mode (which is the default mode) is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="1549c-137">**ReceiveAndDelete** mode (which is the default mode) is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1549c-138">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="1549c-138">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span>
<span data-ttu-id="1549c-139">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="1549c-139">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1549c-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="1549c-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1549c-141">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="1549c-141">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1549c-142">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span><span class="sxs-lookup"><span data-stu-id="1549c-142">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="1549c-143">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the queue.</span><span class="sxs-lookup"><span data-stu-id="1549c-143">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="1549c-144">The following example demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span><span class="sxs-lookup"><span data-stu-id="1549c-144">The following example demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="1549c-145">The example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="1549c-145">The example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the queue message.
            System.out.print("From queue: ");
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
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1549c-146">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="1549c-146">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="1549c-147">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="1549c-147">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1549c-148">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span><span class="sxs-lookup"><span data-stu-id="1549c-148">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="1549c-149">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="1549c-149">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1549c-150">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="1549c-150">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="1549c-151">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message is redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="1549c-151">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="1549c-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="1549c-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1549c-153">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="1549c-153">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="1549c-154">This is often achieved using the **getMessageId** method of the message, which remains constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="1549c-154">This is often achieved using the **getMessageId** method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1549c-155">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1549c-155">Next Steps</span></span>
<span data-ttu-id="1549c-156">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span><span class="sxs-lookup"><span data-stu-id="1549c-156">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="1549c-157">For more information, see the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="1549c-157">For more information, see the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
