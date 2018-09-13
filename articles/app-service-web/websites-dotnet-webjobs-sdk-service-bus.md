---
title: How to use Azure Service Bus with the WebJobs SDK
description: Learn how to use Azure Service Bus queues and topics with the WebJobs SDK.
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562941"
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="43778-103">How to use Azure Service Bus with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="43778-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="43778-104">Overview</span><span class="sxs-lookup"><span data-stu-id="43778-104">Overview</span></span>
<span data-ttu-id="43778-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span><span class="sxs-lookup"><span data-stu-id="43778-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="43778-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="43778-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="43778-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="43778-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="43778-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span><span class="sxs-lookup"><span data-stu-id="43778-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="43778-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="43778-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <a id="prerequisites"></a> <span data-ttu-id="43778-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43778-110">Prerequisites</span></span>
<span data-ttu-id="43778-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span><span class="sxs-lookup"><span data-stu-id="43778-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="43778-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span><span class="sxs-lookup"><span data-stu-id="43778-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="43778-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="43778-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="43778-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="43778-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="43778-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="43778-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <a id="trigger"></a> <span data-ttu-id="43778-116">How to trigger a function when a Service Bus queue message is received</span><span class="sxs-lookup"><span data-stu-id="43778-116">How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="43778-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span><span class="sxs-lookup"><span data-stu-id="43778-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="43778-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span><span class="sxs-lookup"><span data-stu-id="43778-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="43778-119">How ServiceBusTrigger works</span><span class="sxs-lookup"><span data-stu-id="43778-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="43778-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span><span class="sxs-lookup"><span data-stu-id="43778-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="43778-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span><span class="sxs-lookup"><span data-stu-id="43778-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="43778-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="43778-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="43778-123">String queue message</span><span class="sxs-lookup"><span data-stu-id="43778-123">String queue message</span></span>
<span data-ttu-id="43778-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span><span class="sxs-lookup"><span data-stu-id="43778-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="43778-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span><span class="sxs-lookup"><span data-stu-id="43778-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="43778-126">POCO queue message</span><span class="sxs-lookup"><span data-stu-id="43778-126">POCO queue message</span></span>
<span data-ttu-id="43778-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span><span class="sxs-lookup"><span data-stu-id="43778-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="43778-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span><span class="sxs-lookup"><span data-stu-id="43778-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="43778-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="43778-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="43778-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="43778-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="43778-131">Types ServiceBusTrigger works with</span><span class="sxs-lookup"><span data-stu-id="43778-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="43778-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span><span class="sxs-lookup"><span data-stu-id="43778-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <a id="create"></a> <span data-ttu-id="43778-133">How to create Service Bus queue messages</span><span class="sxs-lookup"><span data-stu-id="43778-133">How to create Service Bus queue messages</span></span>
<span data-ttu-id="43778-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span><span class="sxs-lookup"><span data-stu-id="43778-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="43778-135">Create a single queue message in a non-async function</span><span class="sxs-lookup"><span data-stu-id="43778-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="43778-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="43778-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="43778-137">The output parameter for creating a single queue message can be any of the following types:</span><span class="sxs-lookup"><span data-stu-id="43778-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="43778-138">A serializable POCO type that you define.</span><span class="sxs-lookup"><span data-stu-id="43778-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="43778-139">Automatically serialized as JSON.</span><span class="sxs-lookup"><span data-stu-id="43778-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="43778-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span><span class="sxs-lookup"><span data-stu-id="43778-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="43778-141">For the other types, if the parameter is null no queue message is created.</span><span class="sxs-lookup"><span data-stu-id="43778-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="43778-142">Create multiple queue messages or in async functions</span><span class="sxs-lookup"><span data-stu-id="43778-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="43778-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span><span class="sxs-lookup"><span data-stu-id="43778-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="43778-144">Each queue message is created immediately when the `Add` method is called.</span><span class="sxs-lookup"><span data-stu-id="43778-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <a id="topics"></a><span data-ttu-id="43778-145">How to work with Service Bus topics</span><span class="sxs-lookup"><span data-stu-id="43778-145">How to work with Service Bus topics</span></span>
<span data-ttu-id="43778-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span><span class="sxs-lookup"><span data-stu-id="43778-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="43778-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span><span class="sxs-lookup"><span data-stu-id="43778-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="43778-148">Features added in release 1.1</span><span class="sxs-lookup"><span data-stu-id="43778-148">Features added in release 1.1</span></span>
<span data-ttu-id="43778-149">The following features were added in release 1.1:</span><span class="sxs-lookup"><span data-stu-id="43778-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="43778-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="43778-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="43778-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="43778-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="43778-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span><span class="sxs-lookup"><span data-stu-id="43778-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="43778-153">Message processing concurrency is supported by default.</span><span class="sxs-lookup"><span data-stu-id="43778-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="43778-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="43778-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="43778-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span><span class="sxs-lookup"><span data-stu-id="43778-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="43778-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span><span class="sxs-lookup"><span data-stu-id="43778-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <a id="queues"></a><span data-ttu-id="43778-157">Related topics covered by the storage queues how-to article</span><span class="sxs-lookup"><span data-stu-id="43778-157">Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="43778-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="43778-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="43778-159">Topics covered in that article include the following:</span><span class="sxs-lookup"><span data-stu-id="43778-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="43778-160">Async functions</span><span class="sxs-lookup"><span data-stu-id="43778-160">Async functions</span></span>
* <span data-ttu-id="43778-161">Multiple instances</span><span class="sxs-lookup"><span data-stu-id="43778-161">Multiple instances</span></span>
* <span data-ttu-id="43778-162">Graceful shutdown</span><span class="sxs-lookup"><span data-stu-id="43778-162">Graceful shutdown</span></span>
* <span data-ttu-id="43778-163">Use WebJobs SDK attributes in the body of a function</span><span class="sxs-lookup"><span data-stu-id="43778-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="43778-164">Set the SDK connection strings in code</span><span class="sxs-lookup"><span data-stu-id="43778-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="43778-165">Set values for WebJobs SDK constructor parameters in code</span><span class="sxs-lookup"><span data-stu-id="43778-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="43778-166">Trigger a function manually</span><span class="sxs-lookup"><span data-stu-id="43778-166">Trigger a function manually</span></span>
* <span data-ttu-id="43778-167">Write logs</span><span class="sxs-lookup"><span data-stu-id="43778-167">Write logs</span></span>

## <a id="nextsteps"></a> <span data-ttu-id="43778-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="43778-168">Next steps</span></span>
<span data-ttu-id="43778-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="43778-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="43778-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="43778-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

