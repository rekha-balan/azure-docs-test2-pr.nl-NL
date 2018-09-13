---
title: Write applications that use Azure Service Bus queues | Microsoft Docs
description: How to write a simple queue-based application that uses Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: sethm
ms.openlocfilehash: 6d30b8a0130a03ed93be94c3d0913f032adfb895
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556752"
---
# <a name="create-applications-that-use-service-bus-queues"></a><span data-ttu-id="c4e43-103">Create applications that use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="c4e43-103">Create applications that use Service Bus queues</span></span>
<span data-ttu-id="c4e43-104">This topic describes Service Bus queues and shows how to write a simple queue-based application that uses Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c4e43-104">This topic describes Service Bus queues and shows how to write a simple queue-based application that uses Service Bus.</span></span>

<span data-ttu-id="c4e43-105">Consider a scenario from the world of retail in which sales data from individual Point-of-Sale (POS) terminals must be routed to an inventory management system that uses the data to determine when stock has to be replenished.</span><span class="sxs-lookup"><span data-stu-id="c4e43-105">Consider a scenario from the world of retail in which sales data from individual Point-of-Sale (POS) terminals must be routed to an inventory management system that uses the data to determine when stock has to be replenished.</span></span> <span data-ttu-id="c4e43-106">This solution uses Service Bus messaging for the communication between the terminals and the inventory management system, as illustrated in the following figure:</span><span class="sxs-lookup"><span data-stu-id="c4e43-106">This solution uses Service Bus messaging for the communication between the terminals and the inventory management system, as illustrated in the following figure:</span></span>

![Service Bus queues image 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-queues/IC657161.gif)

<span data-ttu-id="c4e43-108">Each POS terminal reports its sales data by sending messages to the **DataCollectionQueue**.</span><span class="sxs-lookup"><span data-stu-id="c4e43-108">Each POS terminal reports its sales data by sending messages to the **DataCollectionQueue**.</span></span> <span data-ttu-id="c4e43-109">These messages remain in this queue until they are retrieved by the inventory management system.</span><span class="sxs-lookup"><span data-stu-id="c4e43-109">These messages remain in this queue until they are retrieved by the inventory management system.</span></span> <span data-ttu-id="c4e43-110">This pattern is often termed *asynchronous messaging*, because the POS terminal does not have to wait for a reply from the inventory management system to continue processing.</span><span class="sxs-lookup"><span data-stu-id="c4e43-110">This pattern is often termed *asynchronous messaging*, because the POS terminal does not have to wait for a reply from the inventory management system to continue processing.</span></span>

## <a name="why-queuing"></a><span data-ttu-id="c4e43-111">Why queuing?</span><span class="sxs-lookup"><span data-stu-id="c4e43-111">Why queuing?</span></span>
<span data-ttu-id="c4e43-112">Before we look at the code that is required to set up this application, consider the advantages of using a queue in this scenario instead of having the POS terminals talk directly (synchronously) to the inventory management system.</span><span class="sxs-lookup"><span data-stu-id="c4e43-112">Before we look at the code that is required to set up this application, consider the advantages of using a queue in this scenario instead of having the POS terminals talk directly (synchronously) to the inventory management system.</span></span>

### <a name="temporal-decoupling"></a><span data-ttu-id="c4e43-113">Temporal decoupling</span><span class="sxs-lookup"><span data-stu-id="c4e43-113">Temporal decoupling</span></span>
<span data-ttu-id="c4e43-114">With the asynchronous messaging pattern, producers and consumers do not have to be online at the same time.</span><span class="sxs-lookup"><span data-stu-id="c4e43-114">With the asynchronous messaging pattern, producers and consumers do not have to be online at the same time.</span></span> <span data-ttu-id="c4e43-115">The messaging infrastructure reliably stores messages until the consuming party is ready to receive them.</span><span class="sxs-lookup"><span data-stu-id="c4e43-115">The messaging infrastructure reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="c4e43-116">This means the components of the distributed application can be disconnected, either voluntarily; for example, for maintenance, or due to a component crash, without affecting the whole system.</span><span class="sxs-lookup"><span data-stu-id="c4e43-116">This means the components of the distributed application can be disconnected, either voluntarily; for example, for maintenance, or due to a component crash, without affecting the whole system.</span></span> <span data-ttu-id="c4e43-117">Furthermore, the consuming application may only have to be online during certain times of the day.</span><span class="sxs-lookup"><span data-stu-id="c4e43-117">Furthermore, the consuming application may only have to be online during certain times of the day.</span></span> <span data-ttu-id="c4e43-118">For example, in this retail scenario, the inventory management system may only have to come online after the end of the business day.</span><span class="sxs-lookup"><span data-stu-id="c4e43-118">For example, in this retail scenario, the inventory management system may only have to come online after the end of the business day.</span></span>

### <a name="load-leveling"></a><span data-ttu-id="c4e43-119">Load leveling</span><span class="sxs-lookup"><span data-stu-id="c4e43-119">Load leveling</span></span>
<span data-ttu-id="c4e43-120">In many applications system load varies over time, whereas the processing time required for each unit of work is typically constant.</span><span class="sxs-lookup"><span data-stu-id="c4e43-120">In many applications system load varies over time, whereas the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="c4e43-121">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only has to be provisioned to service an average load rather than a peak load.</span><span class="sxs-lookup"><span data-stu-id="c4e43-121">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only has to be provisioned to service an average load rather than a peak load.</span></span> <span data-ttu-id="c4e43-122">The depth of the queue will grow and contract as the incoming load varies.</span><span class="sxs-lookup"><span data-stu-id="c4e43-122">The depth of the queue will grow and contract as the incoming load varies.</span></span> <span data-ttu-id="c4e43-123">This directly saves money with regard to the amount of infrastructure required to service the application load.</span><span class="sxs-lookup"><span data-stu-id="c4e43-123">This directly saves money with regard to the amount of infrastructure required to service the application load.</span></span>

![Service Bus queues image 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a><span data-ttu-id="c4e43-125">Load balancing</span><span class="sxs-lookup"><span data-stu-id="c4e43-125">Load balancing</span></span>
<span data-ttu-id="c4e43-126">As the load increases, more worker processes can be added to read from the worker queue.</span><span class="sxs-lookup"><span data-stu-id="c4e43-126">As the load increases, more worker processes can be added to read from the worker queue.</span></span> <span data-ttu-id="c4e43-127">Each message is processed by only one of the worker processes.</span><span class="sxs-lookup"><span data-stu-id="c4e43-127">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="c4e43-128">Furthermore, this pull-based load balancing allows for optimum usage of the worker computers even if the worker computers differ with regard to processing power, as they will pull messages at their own maximum rate.</span><span class="sxs-lookup"><span data-stu-id="c4e43-128">Furthermore, this pull-based load balancing allows for optimum usage of the worker computers even if the worker computers differ with regard to processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="c4e43-129">This pattern is often termed the competing consumer pattern.</span><span class="sxs-lookup"><span data-stu-id="c4e43-129">This pattern is often termed the competing consumer pattern.</span></span>

![Service Bus queues image 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a><span data-ttu-id="c4e43-131">Loose coupling</span><span class="sxs-lookup"><span data-stu-id="c4e43-131">Loose coupling</span></span>
<span data-ttu-id="c4e43-132">Using message queuing to intermediate between message producers and consumers provides an intrinsic loose coupling between the components.</span><span class="sxs-lookup"><span data-stu-id="c4e43-132">Using message queuing to intermediate between message producers and consumers provides an intrinsic loose coupling between the components.</span></span> <span data-ttu-id="c4e43-133">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on the producer.</span><span class="sxs-lookup"><span data-stu-id="c4e43-133">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on the producer.</span></span> <span data-ttu-id="c4e43-134">Furthermore, the messaging topology can evolve without affecting the existing endpoints.</span><span class="sxs-lookup"><span data-stu-id="c4e43-134">Furthermore, the messaging topology can evolve without affecting the existing endpoints.</span></span> <span data-ttu-id="c4e43-135">We’ll discuss this more when we talk about publish/subscribe.</span><span class="sxs-lookup"><span data-stu-id="c4e43-135">We’ll discuss this more when we talk about publish/subscribe.</span></span>

## <a name="show-me-the-code"></a><span data-ttu-id="c4e43-136">Show me the code</span><span class="sxs-lookup"><span data-stu-id="c4e43-136">Show me the code</span></span>
<span data-ttu-id="c4e43-137">The following section shows how to use Service Bus to build this application.</span><span class="sxs-lookup"><span data-stu-id="c4e43-137">The following section shows how to use Service Bus to build this application.</span></span>

### <a name="sign-up-for-an-azure-account"></a><span data-ttu-id="c4e43-138">Sign up for an Azure account</span><span class="sxs-lookup"><span data-stu-id="c4e43-138">Sign up for an Azure account</span></span>
<span data-ttu-id="c4e43-139">You’ll need an Azure account in order to start working with Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c4e43-139">You’ll need an Azure account in order to start working with Service Bus.</span></span> <span data-ttu-id="c4e43-140">If you do not already have one, you can sign up for a free account [here](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="c4e43-140">If you do not already have one, you can sign up for a free account [here](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="create-a-namespace"></a><span data-ttu-id="c4e43-141">Create a namespace</span><span class="sxs-lookup"><span data-stu-id="c4e43-141">Create a namespace</span></span>
<span data-ttu-id="c4e43-142">Once you have a subscription, you can [create a service namespace](service-bus-create-namespace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4e43-142">Once you have a subscription, you can [create a service namespace](service-bus-create-namespace-portal.md).</span></span> <span data-ttu-id="c4e43-143">Each namespace acts as a scoping container for a set of Service Bus entities.</span><span class="sxs-lookup"><span data-stu-id="c4e43-143">Each namespace acts as a scoping container for a set of Service Bus entities.</span></span> <span data-ttu-id="c4e43-144">Give your new namespace a unique name across all Service Bus accounts.</span><span class="sxs-lookup"><span data-stu-id="c4e43-144">Give your new namespace a unique name across all Service Bus accounts.</span></span> 

### <a name="install-the-nuget-package"></a><span data-ttu-id="c4e43-145">Install the NuGet package</span><span class="sxs-lookup"><span data-stu-id="c4e43-145">Install the NuGet package</span></span>
<span data-ttu-id="c4e43-146">To use the Service Bus namespace, an application must reference the Service Bus assembly, specifically Microsoft.ServiceBus.dll.</span><span class="sxs-lookup"><span data-stu-id="c4e43-146">To use the Service Bus namespace, an application must reference the Service Bus assembly, specifically Microsoft.ServiceBus.dll.</span></span> <span data-ttu-id="c4e43-147">You can find this assembly as part of the Microsoft Azure SDK, and the download is available at the [Azure SDK download page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c4e43-147">You can find this assembly as part of the Microsoft Azure SDK, and the download is available at the [Azure SDK download page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c4e43-148">However, the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span><span class="sxs-lookup"><span data-stu-id="c4e43-148">However, the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span>

### <a name="create-the-queue"></a><span data-ttu-id="c4e43-149">Create the queue</span><span class="sxs-lookup"><span data-stu-id="c4e43-149">Create the queue</span></span>
<span data-ttu-id="c4e43-150">Management operations for Service Bus messaging entities (queues and publish/subscribe topics) are performed via the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class.</span><span class="sxs-lookup"><span data-stu-id="c4e43-150">Management operations for Service Bus messaging entities (queues and publish/subscribe topics) are performed via the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class.</span></span> <span data-ttu-id="c4e43-151">Service Bus uses a [Shared Access Signature (SAS)](service-bus-sas.md) based security model.</span><span class="sxs-lookup"><span data-stu-id="c4e43-151">Service Bus uses a [Shared Access Signature (SAS)](service-bus-sas.md) based security model.</span></span> <span data-ttu-id="c4e43-152">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods returning some well-known token providers.</span><span class="sxs-lookup"><span data-stu-id="c4e43-152">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods returning some well-known token providers.</span></span> <span data-ttu-id="c4e43-153">We’ll use a [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to hold the SAS credentials.</span><span class="sxs-lookup"><span data-stu-id="c4e43-153">We’ll use a [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to hold the SAS credentials.</span></span> <span data-ttu-id="c4e43-154">The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instance is then constructed with the base address of the Service Bus namespace and the token provider.</span><span class="sxs-lookup"><span data-stu-id="c4e43-154">The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instance is then constructed with the base address of the Service Bus namespace and the token provider.</span></span>

<span data-ttu-id="c4e43-155">The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class provides methods to create, enumerate and delete messaging entities.</span><span class="sxs-lookup"><span data-stu-id="c4e43-155">The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class provides methods to create, enumerate and delete messaging entities.</span></span> <span data-ttu-id="c4e43-156">The code that is shown here shows how the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instance is created and used to create the **DataCollectionQueue** queue.</span><span class="sxs-lookup"><span data-stu-id="c4e43-156">The code that is shown here shows how the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instance is created and used to create the **DataCollectionQueue** queue.</span></span>

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

<span data-ttu-id="c4e43-157">Note that there are overloads of the [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method that enable properties of the queue to be tuned.</span><span class="sxs-lookup"><span data-stu-id="c4e43-157">Note that there are overloads of the [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method that enable properties of the queue to be tuned.</span></span> <span data-ttu-id="c4e43-158">For example, you can set the default time-to-live (TTL) value for messages sent to the queue.</span><span class="sxs-lookup"><span data-stu-id="c4e43-158">For example, you can set the default time-to-live (TTL) value for messages sent to the queue.</span></span>

### <a name="send-messages-to-the-queue"></a><span data-ttu-id="c4e43-159">Send messages to the queue</span><span class="sxs-lookup"><span data-stu-id="c4e43-159">Send messages to the queue</span></span>
<span data-ttu-id="c4e43-160">For run-time operations on Service Bus entities; for example, sending and receiving messages, an application must first create a [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) object.</span><span class="sxs-lookup"><span data-stu-id="c4e43-160">For run-time operations on Service Bus entities; for example, sending and receiving messages, an application must first create a [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) object.</span></span> <span data-ttu-id="c4e43-161">Similar to the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class, the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance is created from the base address of the service namespace and the token provider.</span><span class="sxs-lookup"><span data-stu-id="c4e43-161">Similar to the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class, the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance is created from the base address of the service namespace and the token provider.</span></span>

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

<span data-ttu-id="c4e43-162">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) class.</span><span class="sxs-lookup"><span data-stu-id="c4e43-162">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) class.</span></span> <span data-ttu-id="c4e43-163">This class consists of a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold application properties, and a body of arbitrary application data.</span><span class="sxs-lookup"><span data-stu-id="c4e43-163">This class consists of a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold application properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="c4e43-164">An application can set the body by passing in any serializable object (the following example passes in a **SalesData** object that represents the sales data from the POS terminal), which will use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) to serialize the object.</span><span class="sxs-lookup"><span data-stu-id="c4e43-164">An application can set the body by passing in any serializable object (the following example passes in a **SalesData** object that represents the sales data from the POS terminal), which will use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) to serialize the object.</span></span> <span data-ttu-id="c4e43-165">Alternatively, a [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) object can be provided.</span><span class="sxs-lookup"><span data-stu-id="c4e43-165">Alternatively, a [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) object can be provided.</span></span>

<span data-ttu-id="c4e43-166">The easiest way to send messages to a given queue, in our case the **DataCollectionQueue**, is to use [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) to create a [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance.</span><span class="sxs-lookup"><span data-stu-id="c4e43-166">The easiest way to send messages to a given queue, in our case the **DataCollectionQueue**, is to use [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) to create a [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance.</span></span>

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-the-queue"></a><span data-ttu-id="c4e43-167">Receiving messages from the queue</span><span class="sxs-lookup"><span data-stu-id="c4e43-167">Receiving messages from the queue</span></span>
<span data-ttu-id="c4e43-168">To receive messages from the queue, you can use a [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) object which you create directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) using [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_).</span><span class="sxs-lookup"><span data-stu-id="c4e43-168">To receive messages from the queue, you can use a [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) object which you create directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) using [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_).</span></span> <span data-ttu-id="c4e43-169">Message receivers can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="c4e43-169">Message receivers can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span> <span data-ttu-id="c4e43-170">The [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) is set when the message receiver is created, as a parameter to the [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) call.</span><span class="sxs-lookup"><span data-stu-id="c4e43-170">The [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) is set when the message receiver is created, as a parameter to the [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) call.</span></span>

<span data-ttu-id="c4e43-171">When using the **ReceiveAndDelete** mode, the receive is a single-shot operation; that is, when Service Bus receives the request, it marks the message as being consumed and returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="c4e43-171">When using the **ReceiveAndDelete** mode, the receive is a single-shot operation; that is, when Service Bus receives the request, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="c4e43-172">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which the application can tolerate not processing a message if a failure were to occur.</span><span class="sxs-lookup"><span data-stu-id="c4e43-172">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which the application can tolerate not processing a message if a failure were to occur.</span></span> <span data-ttu-id="c4e43-173">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="c4e43-173">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="c4e43-174">Since Service Bus marked the message as being consumed, when the application restarts and starts consuming messages again, it will have missed the message that was consumed before the crash.</span><span class="sxs-lookup"><span data-stu-id="c4e43-174">Since Service Bus marked the message as being consumed, when the application restarts and starts consuming messages again, it will have missed the message that was consumed before the crash.</span></span>

<span data-ttu-id="c4e43-175">In **PeekLock** mode, the receive becomes a two-stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="c4e43-175">In **PeekLock** mode, the receive becomes a two-stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="c4e43-176">When Service Bus receives the request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="c4e43-176">When Service Bus receives the request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="c4e43-177">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span><span class="sxs-lookup"><span data-stu-id="c4e43-177">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span></span> <span data-ttu-id="c4e43-178">When Service Bus sees the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) call, it marks the message as being consumed.</span><span class="sxs-lookup"><span data-stu-id="c4e43-178">When Service Bus sees the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) call, it marks the message as being consumed.</span></span>

<span data-ttu-id="c4e43-179">Two other outcomes are possible.</span><span class="sxs-lookup"><span data-stu-id="c4e43-179">Two other outcomes are possible.</span></span> <span data-ttu-id="c4e43-180">First, if the application is unable to process the message for some reason, it can call [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) on the received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span><span class="sxs-lookup"><span data-stu-id="c4e43-180">First, if the application is unable to process the message for some reason, it can call [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) on the received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span></span> <span data-ttu-id="c4e43-181">This causes Service Bus to unlock the message and make it available to be received again, either by the same consumer or by another completing consumer.</span><span class="sxs-lookup"><span data-stu-id="c4e43-181">This causes Service Bus to unlock the message and make it available to be received again, either by the same consumer or by another completing consumer.</span></span> <span data-ttu-id="c4e43-182">Second, there is a time-out associated with the lock and if the application cannot process the message before the lock time-out expires (for example, if the application crashes), then Service Bus will unlock the message and make it available to be received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span><span class="sxs-lookup"><span data-stu-id="c4e43-182">Second, there is a time-out associated with the lock and if the application cannot process the message before the lock time-out expires (for example, if the application crashes), then Service Bus will unlock the message and make it available to be received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span></span>

<span data-ttu-id="c4e43-183">Note that if the application crashes after it processes the message but before the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) request was issued, the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="c4e43-183">Note that if the application crashes after it processes the message but before the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) request was issued, the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="c4e43-184">This is often termed \*At Least Once \* processing.</span><span class="sxs-lookup"><span data-stu-id="c4e43-184">This is often termed \*At Least Once \* processing.</span></span> <span data-ttu-id="c4e43-185">This means that each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="c4e43-185">This means that each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="c4e43-186">If the scenario cannot tolerate duplicate processing, then additional logic is required in the application to detect duplicates.</span><span class="sxs-lookup"><span data-stu-id="c4e43-186">If the scenario cannot tolerate duplicate processing, then additional logic is required in the application to detect duplicates.</span></span> <span data-ttu-id="c4e43-187">This can be achieved based on the [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) property of the message.</span><span class="sxs-lookup"><span data-stu-id="c4e43-187">This can be achieved based on the [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) property of the message.</span></span> <span data-ttu-id="c4e43-188">The value of this property remains constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="c4e43-188">The value of this property remains constant across delivery attempts.</span></span> <span data-ttu-id="c4e43-189">This is termed *Exactly Once* processing.</span><span class="sxs-lookup"><span data-stu-id="c4e43-189">This is termed *Exactly Once* processing.</span></span>

<span data-ttu-id="c4e43-190">The code that is shown here receives and processes a message using the **PeekLock** mode, which is the default if no [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) value is explicitly provided.</span><span class="sxs-lookup"><span data-stu-id="c4e43-190">The code that is shown here receives and processes a message using the **PeekLock** mode, which is the default if no [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) value is explicitly provided.</span></span>

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

### <a name="use-the-queue-client"></a><span data-ttu-id="c4e43-191">Use the queue client</span><span class="sxs-lookup"><span data-stu-id="c4e43-191">Use the queue client</span></span>
<span data-ttu-id="c4e43-192">The examples earlier in this section created [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) and [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objects directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) to send and receive messages from the queue, respectively.</span><span class="sxs-lookup"><span data-stu-id="c4e43-192">The examples earlier in this section created [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) and [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objects directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) to send and receive messages from the queue, respectively.</span></span> <span data-ttu-id="c4e43-193">An alternative approach is to use a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object, which supports both send and receive operations in addition to more advanced features, such as sessions.</span><span class="sxs-lookup"><span data-stu-id="c4e43-193">An alternative approach is to use a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object, which supports both send and receive operations in addition to more advanced features, such as sessions.</span></span>

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a><span data-ttu-id="c4e43-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4e43-194">Next steps</span></span>
<span data-ttu-id="c4e43-195">Now that you've learned the basics of queues, see [Create applications that use Service Bus topics and subscriptions](service-bus-create-topics-subscriptions.md) to continue this discussion using the publish/subscribe capabilities of Service Bus topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c4e43-195">Now that you've learned the basics of queues, see [Create applications that use Service Bus topics and subscriptions](service-bus-create-topics-subscriptions.md) to continue this discussion using the publish/subscribe capabilities of Service Bus topics and subscriptions.</span></span>



