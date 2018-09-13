---
title: Use Azure Service Bus topics with .NET | Microsoft Docs
description: Learn how to use Service Bus topics and subscriptions with .NET in Azure. Code samples are written for .NET applications.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 31d0bc29-6524-4b1b-9c7f-aa15d5a9d3b4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: sethm
ms.openlocfilehash: 232a98e09bc673e7c7b22c50c539ab1db82c9b19
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549577"
---
# <a name="how-to-use-service-bus-topics-and-subscriptions"></a><span data-ttu-id="70f9f-104">How to use Service Bus topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="70f9f-104">How to use Service Bus topics and subscriptions</span></span>
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="70f9f-105">This article describes how to use Service Bus topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="70f9f-105">This article describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="70f9f-106">The samples are written in C# and use the .NET APIs.</span><span class="sxs-lookup"><span data-stu-id="70f9f-106">The samples are written in C# and use the .NET APIs.</span></span> <span data-ttu-id="70f9f-107">The scenarios covered include creating topics and subscriptions, creating subscription filters, sending messages to a topic, receiving messages from a subscription, and deleting topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="70f9f-107">The scenarios covered include creating topics and subscriptions, creating subscription filters, sending messages to a topic, receiving messages from a subscription, and deleting topics and subscriptions.</span></span> <span data-ttu-id="70f9f-108">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="70f9f-108">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="configure-the-application-to-use-service-bus"></a><span data-ttu-id="70f9f-109">Configure the application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="70f9f-109">Configure the application to use Service Bus</span></span>
<span data-ttu-id="70f9f-110">When you create an application that uses Service Bus, you must add a reference to the Service Bus assembly and include the corresponding namespaces.</span><span class="sxs-lookup"><span data-stu-id="70f9f-110">When you create an application that uses Service Bus, you must add a reference to the Service Bus assembly and include the corresponding namespaces.</span></span> <span data-ttu-id="70f9f-111">The easiest way to do this is to download the appropriate [NuGet](https://www.nuget.org) package.</span><span class="sxs-lookup"><span data-stu-id="70f9f-111">The easiest way to do this is to download the appropriate [NuGet](https://www.nuget.org) package.</span></span>

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="70f9f-112">Get the Service Bus NuGet package</span><span class="sxs-lookup"><span data-stu-id="70f9f-112">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="70f9f-113">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to configure your application with all the necessary Service Bus dependencies.</span><span class="sxs-lookup"><span data-stu-id="70f9f-113">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to configure your application with all the necessary Service Bus dependencies.</span></span> <span data-ttu-id="70f9f-114">To install the Service Bus NuGet package in your project, do the following:</span><span class="sxs-lookup"><span data-stu-id="70f9f-114">To install the Service Bus NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="70f9f-115">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="70f9f-115">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="70f9f-116">Click **Browse**, search for "Azure Service Bus" and then select the **Microsoft Azure Service Bus** item.</span><span class="sxs-lookup"><span data-stu-id="70f9f-116">Click **Browse**, search for "Azure Service Bus" and then select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="70f9f-117">Click **Install** to complete the installation, then close the dialog box:</span><span class="sxs-lookup"><span data-stu-id="70f9f-117">Click **Install** to complete the installation, then close the dialog box:</span></span>
   
   ![][7]

<span data-ttu-id="70f9f-118">You are now ready to write code for Service Bus.</span><span class="sxs-lookup"><span data-stu-id="70f9f-118">You are now ready to write code for Service Bus.</span></span>

## <a name="create-a-service-bus-connection-string"></a><span data-ttu-id="70f9f-119">Create a Service Bus connection string</span><span class="sxs-lookup"><span data-stu-id="70f9f-119">Create a Service Bus connection string</span></span>
<span data-ttu-id="70f9f-120">Service Bus uses a connection string to store endpoints and credentials.</span><span class="sxs-lookup"><span data-stu-id="70f9f-120">Service Bus uses a connection string to store endpoints and credentials.</span></span> <span data-ttu-id="70f9f-121">You can put your connection string in a configuration file, rather than hard-coding it:</span><span class="sxs-lookup"><span data-stu-id="70f9f-121">You can put your connection string in a configuration file, rather than hard-coding it:</span></span>

* <span data-ttu-id="70f9f-122">When using Azure services, it is recommended that you store your connection string using the Azure service configuration system (.csdef and .cscfg files).</span><span class="sxs-lookup"><span data-stu-id="70f9f-122">When using Azure services, it is recommended that you store your connection string using the Azure service configuration system (.csdef and .cscfg files).</span></span>
* <span data-ttu-id="70f9f-123">When using Azure websites or Azure Virtual Machines, it is recommended that you store your connection string using the .NET configuration system (for example, the Web.config file).</span><span class="sxs-lookup"><span data-stu-id="70f9f-123">When using Azure websites or Azure Virtual Machines, it is recommended that you store your connection string using the .NET configuration system (for example, the Web.config file).</span></span>

<span data-ttu-id="70f9f-124">In both cases, you can retrieve your connection string using the `CloudConfigurationManager.GetSetting` method, as shown later in this article.</span><span class="sxs-lookup"><span data-stu-id="70f9f-124">In both cases, you can retrieve your connection string using the `CloudConfigurationManager.GetSetting` method, as shown later in this article.</span></span>

### <a name="configure-your-connection-string"></a><span data-ttu-id="70f9f-125">Configure your connection string</span><span class="sxs-lookup"><span data-stu-id="70f9f-125">Configure your connection string</span></span>
<span data-ttu-id="70f9f-126">The service configuration mechanism enables you to dynamically change configuration settings from the [Azure portal][Azure portal] without redeploying your application.</span><span class="sxs-lookup"><span data-stu-id="70f9f-126">The service configuration mechanism enables you to dynamically change configuration settings from the [Azure portal][Azure portal] without redeploying your application.</span></span> <span data-ttu-id="70f9f-127">For example, add a `Setting` label to your service definition (**.csdef**) file, as shown in the next example.</span><span class="sxs-lookup"><span data-stu-id="70f9f-127">For example, add a `Setting` label to your service definition (**.csdef**) file, as shown in the next example.</span></span>

```xml
<ServiceDefinition name="Azure1">
...
    <WebRole name="MyRole" vmsize="Small">
        <ConfigurationSettings>
            <Setting name="Microsoft.ServiceBus.ConnectionString" />
        </ConfigurationSettings>
    </WebRole>
...
</ServiceDefinition>
```

<span data-ttu-id="70f9f-128">You then specify values in the service configuration (.cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="70f9f-128">You then specify values in the service configuration (.cscfg) file.</span></span>

```xml
<ServiceConfiguration serviceName="Azure1">
...
    <Role name="MyRole">
        <ConfigurationSettings>
            <Setting name="Microsoft.ServiceBus.ConnectionString"
                     value="Endpoint=sb://yourServiceNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey" />
        </ConfigurationSettings>
    </Role>
...
</ServiceConfiguration>
```

<span data-ttu-id="70f9f-129">Use the Shared Access Signature (SAS) key name and key values retrieved from the portal as described previously.</span><span class="sxs-lookup"><span data-stu-id="70f9f-129">Use the Shared Access Signature (SAS) key name and key values retrieved from the portal as described previously.</span></span>

### <a name="configure-your-connection-string-when-using-azure-websites-or-azure-virtual-machines"></a><span data-ttu-id="70f9f-130">Configure your connection string when using Azure websites or Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="70f9f-130">Configure your connection string when using Azure websites or Azure Virtual Machines</span></span>
<span data-ttu-id="70f9f-131">When using websites or Virtual Machines, it is recommended that you use the .NET configuration system (for example, Web.config).</span><span class="sxs-lookup"><span data-stu-id="70f9f-131">When using websites or Virtual Machines, it is recommended that you use the .NET configuration system (for example, Web.config).</span></span> <span data-ttu-id="70f9f-132">You store the connection string using the `<appSettings>` element.</span><span class="sxs-lookup"><span data-stu-id="70f9f-132">You store the connection string using the `<appSettings>` element.</span></span>

```xml
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://yourServiceNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey" />
    </appSettings>
</configuration>
```

<span data-ttu-id="70f9f-133">Use the SAS name and key values that you retrieved from the [Azure portal][Azure portal], as described previously.</span><span class="sxs-lookup"><span data-stu-id="70f9f-133">Use the SAS name and key values that you retrieved from the [Azure portal][Azure portal], as described previously.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="70f9f-134">Create a topic</span><span class="sxs-lookup"><span data-stu-id="70f9f-134">Create a topic</span></span>
<span data-ttu-id="70f9f-135">You can perform management operations for Service Bus topics and subscriptions using the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class.</span><span class="sxs-lookup"><span data-stu-id="70f9f-135">You can perform management operations for Service Bus topics and subscriptions using the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class.</span></span> <span data-ttu-id="70f9f-136">This class provides methods to create, enumerate, and delete topics.</span><span class="sxs-lookup"><span data-stu-id="70f9f-136">This class provides methods to create, enumerate, and delete topics.</span></span>

<span data-ttu-id="70f9f-137">The following example constructs a `NamespaceManager` object using the Azure `CloudConfigurationManager` class with a connection string consisting of the base address of a Service Bus namespace and the appropriate SAS credentials with permissions to manage it.</span><span class="sxs-lookup"><span data-stu-id="70f9f-137">The following example constructs a `NamespaceManager` object using the Azure `CloudConfigurationManager` class with a connection string consisting of the base address of a Service Bus namespace and the appropriate SAS credentials with permissions to manage it.</span></span> <span data-ttu-id="70f9f-138">This connection string is of the following form:</span><span class="sxs-lookup"><span data-stu-id="70f9f-138">This connection string is of the following form:</span></span>

```xml
Endpoint=sb://<yourNamespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<yourKey>
```

<span data-ttu-id="70f9f-139">Use the following example, given the configuration settings in the previous section.</span><span class="sxs-lookup"><span data-stu-id="70f9f-139">Use the following example, given the configuration settings in the previous section.</span></span>

```csharp
// Create the topic if it does not exist already.
string connectionString =
    CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

var namespaceManager =
    NamespaceManager.CreateFromConnectionString(connectionString);

if (!namespaceManager.TopicExists("TestTopic"))
{
    namespaceManager.CreateTopic("TestTopic");
}
```

<span data-ttu-id="70f9f-140">There are overloads of the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager) method that enable you to set properties of the topic; for example, to set the default time-to-live (TTL) value to be applied to messages sent to the topic.</span><span class="sxs-lookup"><span data-stu-id="70f9f-140">There are overloads of the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager) method that enable you to set properties of the topic; for example, to set the default time-to-live (TTL) value to be applied to messages sent to the topic.</span></span> <span data-ttu-id="70f9f-141">These settings are applied by using the [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription) class.</span><span class="sxs-lookup"><span data-stu-id="70f9f-141">These settings are applied by using the [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription) class.</span></span> <span data-ttu-id="70f9f-142">The following example shows how to create a topic named **TestTopic** with a maximum size of 5 GB and a default message TTL of 1 minute.</span><span class="sxs-lookup"><span data-stu-id="70f9f-142">The following example shows how to create a topic named **TestTopic** with a maximum size of 5 GB and a default message TTL of 1 minute.</span></span>

```csharp
// Configure Topic Settings.
TopicDescription td = new TopicDescription("TestTopic");
td.MaxSizeInMegabytes = 5120;
td.DefaultMessageTimeToLive = new TimeSpan(0, 1, 0);

// Create a new Topic with custom settings.
string connectionString =
    CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

var namespaceManager =
    NamespaceManager.CreateFromConnectionString(connectionString);

if (!namespaceManager.TopicExists("TestTopic"))
{
    namespaceManager.CreateTopic(td);
}
```

> [!NOTE]
> <span data-ttu-id="70f9f-143">You can use the [TopicExists](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_TopicExists_System_String_) method on [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) objects to check whether a topic with a specified name already exists within a namespace.</span><span class="sxs-lookup"><span data-stu-id="70f9f-143">You can use the [TopicExists](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_TopicExists_System_String_) method on [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) objects to check whether a topic with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="70f9f-144">Create a subscription</span><span class="sxs-lookup"><span data-stu-id="70f9f-144">Create a subscription</span></span>
<span data-ttu-id="70f9f-145">You can also create topic subscriptions using the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class.</span><span class="sxs-lookup"><span data-stu-id="70f9f-145">You can also create topic subscriptions using the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class.</span></span> <span data-ttu-id="70f9f-146">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="70f9f-146">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70f9f-147">In order for messages to be received by a subscription, you must create that subscription before sending any messages to the topic.</span><span class="sxs-lookup"><span data-stu-id="70f9f-147">In order for messages to be received by a subscription, you must create that subscription before sending any messages to the topic.</span></span> <span data-ttu-id="70f9f-148">If there are no subscriptions to a topic, the topic discards those messages.</span><span class="sxs-lookup"><span data-stu-id="70f9f-148">If there are no subscriptions to a topic, the topic discards those messages.</span></span>
> 
> 

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="70f9f-149">Create a subscription with the default (MatchAll) filter</span><span class="sxs-lookup"><span data-stu-id="70f9f-149">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="70f9f-150">If no filter is specified when a new subscription is created, the **MatchAll** filter is the default filter that is used.</span><span class="sxs-lookup"><span data-stu-id="70f9f-150">If no filter is specified when a new subscription is created, the **MatchAll** filter is the default filter that is used.</span></span> <span data-ttu-id="70f9f-151">When you use the **MatchAll** filter, all messages published to the topic are placed in the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="70f9f-151">When you use the **MatchAll** filter, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="70f9f-152">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="70f9f-152">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```csharp
string connectionString =
    CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

var namespaceManager =
    NamespaceManager.CreateFromConnectionString(connectionString);

if (!namespaceManager.SubscriptionExists("TestTopic", "AllMessages"))
{
    namespaceManager.CreateSubscription("TestTopic", "AllMessages");
}
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="70f9f-153">Create subscriptions with filters</span><span class="sxs-lookup"><span data-stu-id="70f9f-153">Create subscriptions with filters</span></span>
<span data-ttu-id="70f9f-154">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span><span class="sxs-lookup"><span data-stu-id="70f9f-154">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

<span data-ttu-id="70f9f-155">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter] class, which implements a subset of SQL92.</span><span class="sxs-lookup"><span data-stu-id="70f9f-155">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter] class, which implements a subset of SQL92.</span></span> <span data-ttu-id="70f9f-156">SQL filters operate on the properties of the messages that are published to the topic.</span><span class="sxs-lookup"><span data-stu-id="70f9f-156">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="70f9f-157">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span><span class="sxs-lookup"><span data-stu-id="70f9f-157">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="70f9f-158">The following example creates a subscription named **HighMessages** with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3.</span><span class="sxs-lookup"><span data-stu-id="70f9f-158">The following example creates a subscription named **HighMessages** with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3.</span></span>

```csharp
// Create a "HighMessages" filtered subscription.
SqlFilter highMessagesFilter =
   new SqlFilter("MessageId > 3");

namespaceManager.CreateSubscription("TestTopic",
   "HighMessages",
   highMessagesFilter);
```

<span data-ttu-id="70f9f-159">Similarly, the following example creates a subscription named **LowMessages** with a [SqlFilter][SqlFilter] that only selects messages that have a **MessageNumber** property less than or equal to 3.</span><span class="sxs-lookup"><span data-stu-id="70f9f-159">Similarly, the following example creates a subscription named **LowMessages** with a [SqlFilter][SqlFilter] that only selects messages that have a **MessageNumber** property less than or equal to 3.</span></span>

```csharp
// Create a "LowMessages" filtered subscription.
SqlFilter lowMessagesFilter =
   new SqlFilter("MessageId <= 3");

namespaceManager.CreateSubscription("TestTopic",
   "LowMessages",
   lowMessagesFilter);
```

<span data-ttu-id="70f9f-160">Now when a message is sent to `TestTopic`, it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span><span class="sxs-lookup"><span data-stu-id="70f9f-160">Now when a message is sent to `TestTopic`, it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="70f9f-161">Send messages to a topic</span><span class="sxs-lookup"><span data-stu-id="70f9f-161">Send messages to a topic</span></span>
<span data-ttu-id="70f9f-162">To send a message to a Service Bus topic, your application creates a [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient) object using the connection string.</span><span class="sxs-lookup"><span data-stu-id="70f9f-162">To send a message to a Service Bus topic, your application creates a [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient) object using the connection string.</span></span>

<span data-ttu-id="70f9f-163">The following code demonstrates how to create a [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient) object for the **TestTopic** topic created earlier using the [CreateFromConnectionString](/dotnet/api/microsoft.servicebus.messaging.topicclient#Microsoft_ServiceBus_Messaging_TopicClient_CreateFromConnectionString_System_String_System_String_) API.</span><span class="sxs-lookup"><span data-stu-id="70f9f-163">The following code demonstrates how to create a [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient) object for the **TestTopic** topic created earlier using the [CreateFromConnectionString](/dotnet/api/microsoft.servicebus.messaging.topicclient#Microsoft_ServiceBus_Messaging_TopicClient_CreateFromConnectionString_System_String_System_String_) API.</span></span>

```csharp
string connectionString =
    CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

TopicClient Client =
    TopicClient.CreateFromConnectionString(connectionString, "TestTopic");

Client.Send(new BrokeredMessage());
```

<span data-ttu-id="70f9f-164">Messages sent to Service Bus topics are instances of the [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) class.</span><span class="sxs-lookup"><span data-stu-id="70f9f-164">Messages sent to Service Bus topics are instances of the [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) class.</span></span> <span data-ttu-id="70f9f-165">**BrokeredMessage** objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span><span class="sxs-lookup"><span data-stu-id="70f9f-165">**BrokeredMessage** objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="70f9f-166">An application can set the body of the message by passing any serializable object to the constructor of the **BrokeredMessage** object, and the appropriate **DataContractSerializer** is then used to serialize the object.</span><span class="sxs-lookup"><span data-stu-id="70f9f-166">An application can set the body of the message by passing any serializable object to the constructor of the **BrokeredMessage** object, and the appropriate **DataContractSerializer** is then used to serialize the object.</span></span> <span data-ttu-id="70f9f-167">Alternatively, a **System.IO.Stream** object can be provided.</span><span class="sxs-lookup"><span data-stu-id="70f9f-167">Alternatively, a **System.IO.Stream** object can be provided.</span></span>

<span data-ttu-id="70f9f-168">The following example demonstrates how to send five test messages to the **TestTopic** [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient) object obtained in the previous code example.</span><span class="sxs-lookup"><span data-stu-id="70f9f-168">The following example demonstrates how to send five test messages to the **TestTopic** [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient) object obtained in the previous code example.</span></span> <span data-ttu-id="70f9f-169">Note that the [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) property value of each message varies depending on the iteration of the loop (this determines which subscriptions receive it).</span><span class="sxs-lookup"><span data-stu-id="70f9f-169">Note that the [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) property value of each message varies depending on the iteration of the loop (this determines which subscriptions receive it).</span></span>

```csharp
for (int i=0; i<5; i++)
{
  // Create message, passing a string message for the body.
  BrokeredMessage message = new BrokeredMessage("Test message " + i);

  // Set additional custom app-specific property.
  message.Properties["MessageId"] = i;

  // Send message to the topic.
  Client.Send(message);
}
```

<span data-ttu-id="70f9f-170">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="70f9f-170">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="70f9f-171">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="70f9f-171">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="70f9f-172">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span><span class="sxs-lookup"><span data-stu-id="70f9f-172">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="70f9f-173">This topic size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="70f9f-173">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="70f9f-174">If partitioning is enabled, the upper limit is higher.</span><span class="sxs-lookup"><span data-stu-id="70f9f-174">If partitioning is enabled, the upper limit is higher.</span></span> <span data-ttu-id="70f9f-175">For more information, see [Partitioned messaging entities](service-bus-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="70f9f-175">For more information, see [Partitioned messaging entities](service-bus-partitioning.md).</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="70f9f-176">How to receive messages from a subscription</span><span class="sxs-lookup"><span data-stu-id="70f9f-176">How to receive messages from a subscription</span></span>
<span data-ttu-id="70f9f-177">The recommended way to receive messages from a subscription is to use a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object.</span><span class="sxs-lookup"><span data-stu-id="70f9f-177">The recommended way to receive messages from a subscription is to use a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object.</span></span> <span data-ttu-id="70f9f-178">**SubscriptionClient** objects can work in two different modes: [*ReceiveAndDelete* and *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="70f9f-178">**SubscriptionClient** objects can work in two different modes: [*ReceiveAndDelete* and *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="70f9f-179">**PeekLock** is the default.</span><span class="sxs-lookup"><span data-stu-id="70f9f-179">**PeekLock** is the default.</span></span>

<span data-ttu-id="70f9f-180">When using the **ReceiveAndDelete** mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="70f9f-180">When using the **ReceiveAndDelete** mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="70f9f-181">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="70f9f-181">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="70f9f-182">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="70f9f-182">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="70f9f-183">Because Service Bus has marked the message as consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="70f9f-183">Because Service Bus has marked the message as consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="70f9f-184">In **PeekLock** mode (the default mode), the receive process becomes a two-stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="70f9f-184">In **PeekLock** mode (the default mode), the receive process becomes a two-stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="70f9f-185">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="70f9f-185">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="70f9f-186">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span><span class="sxs-lookup"><span data-stu-id="70f9f-186">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span></span> <span data-ttu-id="70f9f-187">When Service Bus sees the **Complete** call, it marks the message as being consumed and removes it from the subscription.</span><span class="sxs-lookup"><span data-stu-id="70f9f-187">When Service Bus sees the **Complete** call, it marks the message as being consumed and removes it from the subscription.</span></span>

<span data-ttu-id="70f9f-188">The following example demonstrates how messages can be received and processed using the default **PeekLock** mode.</span><span class="sxs-lookup"><span data-stu-id="70f9f-188">The following example demonstrates how messages can be received and processed using the default **PeekLock** mode.</span></span> <span data-ttu-id="70f9f-189">To specify a different [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) value, you can use another overload for [CreateFromConnectionString](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_CreateFromConnectionString_System_String_System_String_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_).</span><span class="sxs-lookup"><span data-stu-id="70f9f-189">To specify a different [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) value, you can use another overload for [CreateFromConnectionString](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_CreateFromConnectionString_System_String_System_String_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_).</span></span> <span data-ttu-id="70f9f-190">This example uses the [OnMessage](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback to process messages as they arrive into the **HighMessages** subscription.</span><span class="sxs-lookup"><span data-stu-id="70f9f-190">This example uses the [OnMessage](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback to process messages as they arrive into the **HighMessages** subscription.</span></span>

```csharp
string connectionString =
    CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

SubscriptionClient Client =
    SubscriptionClient.CreateFromConnectionString
            (connectionString, "TestTopic", "HighMessages");

// Configure the callback options.
OnMessageOptions options = new OnMessageOptions();
options.AutoComplete = false;
options.AutoRenewTimeout = TimeSpan.FromMinutes(1);

Client.OnMessage((message) =>
{
    try
    {
        // Process message from subscription.
        Console.WriteLine("\n**High Messages**");
        Console.WriteLine("Body: " + message.GetBody<string>());
        Console.WriteLine("MessageID: " + message.MessageId);
        Console.WriteLine("Message Number: " +
            message.Properties["MessageNumber"]);

        // Remove message from subscription.
        message.Complete();
    }
    catch (Exception)
    {
        // Indicates a problem, unlock message in subscription.
        message.Abandon();
    }
}, options);
```

<span data-ttu-id="70f9f-191">This example configures the [OnMessage](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback using an [OnMessageOptions](/dotnet/api/microsoft.servicebus.messaging.onmessageoptions) object.</span><span class="sxs-lookup"><span data-stu-id="70f9f-191">This example configures the [OnMessage](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback using an [OnMessageOptions](/dotnet/api/microsoft.servicebus.messaging.onmessageoptions) object.</span></span> <span data-ttu-id="70f9f-192">[AutoComplete](/dotnet/api/microsoft.servicebus.messaging.onmessageoptions#Microsoft_ServiceBus_Messaging_OnMessageOptions_AutoComplete) is set to **false** to enable manual control of when to call [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span><span class="sxs-lookup"><span data-stu-id="70f9f-192">[AutoComplete](/dotnet/api/microsoft.servicebus.messaging.onmessageoptions#Microsoft_ServiceBus_Messaging_OnMessageOptions_AutoComplete) is set to **false** to enable manual control of when to call [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span></span> <span data-ttu-id="70f9f-193">[AutoRenewTimeout](/dotnet/api/microsoft.servicebus.messaging.onmessageoptions#Microsoft_ServiceBus_Messaging_OnMessageOptions_AutoRenewTimeout) is set to 1 minute, which causes the client to wait for up to one minute before terminating the auto-renewal feature and the client makes a new call to check for messages.</span><span class="sxs-lookup"><span data-stu-id="70f9f-193">[AutoRenewTimeout](/dotnet/api/microsoft.servicebus.messaging.onmessageoptions#Microsoft_ServiceBus_Messaging_OnMessageOptions_AutoRenewTimeout) is set to 1 minute, which causes the client to wait for up to one minute before terminating the auto-renewal feature and the client makes a new call to check for messages.</span></span> <span data-ttu-id="70f9f-194">This property value reduces the number of times the client makes chargeable calls that do not retrieve messages.</span><span class="sxs-lookup"><span data-stu-id="70f9f-194">This property value reduces the number of times the client makes chargeable calls that do not retrieve messages.</span></span>

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="70f9f-195">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="70f9f-195">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="70f9f-196">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="70f9f-196">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="70f9f-197">If a receiving application is unable to process the message for some reason, then it can call the [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon_System_Collections_Generic_IDictionary_System_String_System_Object__) method on the received message (instead of the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) method).</span><span class="sxs-lookup"><span data-stu-id="70f9f-197">If a receiving application is unable to process the message for some reason, then it can call the [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon_System_Collections_Generic_IDictionary_System_String_System_Object__) method on the received message (instead of the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) method).</span></span> <span data-ttu-id="70f9f-198">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="70f9f-198">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="70f9f-199">There is also a time-out associated with a message locked within the subscription, and if the application fails to process the message before the lock time-out expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="70f9f-199">There is also a time-out associated with a message locked within the subscription, and if the application fails to process the message before the lock time-out expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="70f9f-200">In the event that the application crashes after processing the message but before the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) request is issued, the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="70f9f-200">In the event that the application crashes after processing the message but before the [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) request is issued, the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="70f9f-201">This is often called *At Least Once processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="70f9f-201">This is often called *At Least Once processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="70f9f-202">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="70f9f-202">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="70f9f-203">This is often achieved using the [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) property of the message, which remains constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="70f9f-203">This is often achieved using the [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) property of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="70f9f-204">Delete topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="70f9f-204">Delete topics and subscriptions</span></span>
<span data-ttu-id="70f9f-205">The following example demonstrates how to delete the topic **TestTopic** from the **HowToSample** service namespace.</span><span class="sxs-lookup"><span data-stu-id="70f9f-205">The following example demonstrates how to delete the topic **TestTopic** from the **HowToSample** service namespace.</span></span>

```csharp
// Delete Topic.
namespaceManager.DeleteTopic("TestTopic");
```

<span data-ttu-id="70f9f-206">Deleting a topic also deletes any subscriptions that are registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="70f9f-206">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="70f9f-207">Subscriptions can also be deleted independently.</span><span class="sxs-lookup"><span data-stu-id="70f9f-207">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="70f9f-208">The following code demonstrates how to delete a subscription named **HighMessages** from the **TestTopic** topic.</span><span class="sxs-lookup"><span data-stu-id="70f9f-208">The following code demonstrates how to delete a subscription named **HighMessages** from the **TestTopic** topic.</span></span>

```csharp
namespaceManager.DeleteSubscription("TestTopic", "HighMessages");
```

## <a name="next-steps"></a><span data-ttu-id="70f9f-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="70f9f-209">Next steps</span></span>
<span data-ttu-id="70f9f-210">Now that you've learned the basics of Service Bus topics and subscriptions, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="70f9f-210">Now that you've learned the basics of Service Bus topics and subscriptions, follow these links to learn more.</span></span>

* <span data-ttu-id="70f9f-211">[Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="70f9f-211">[Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="70f9f-212">[Topic filters sample][Topic filters sample]</span><span class="sxs-lookup"><span data-stu-id="70f9f-212">[Topic filters sample][Topic filters sample]</span></span>
* <span data-ttu-id="70f9f-213">API reference for [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="70f9f-213">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="70f9f-214">Build a working application that sends and receives messages to and from a Service Bus queue: [Service Bus brokered messaging .NET tutorial][Service Bus brokered messaging .NET tutorial].</span><span class="sxs-lookup"><span data-stu-id="70f9f-214">Build a working application that sends and receives messages to and from a Service Bus queue: [Service Bus brokered messaging .NET tutorial][Service Bus brokered messaging .NET tutorial].</span></span>
* <span data-ttu-id="70f9f-215">Service Bus samples: Download from [Azure samples][Azure samples] or see the [overview](service-bus-samples.md).</span><span class="sxs-lookup"><span data-stu-id="70f9f-215">Service Bus samples: Download from [Azure samples][Azure samples] or see the [overview](service-bus-samples.md).</span></span>

[Azure portal]: https://portal.azure.com

[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-how-to-use-topics-subscriptions/getting-started-multi-tier-13.png

[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Topic filters sample]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[Service Bus brokered messaging .NET tutorial]: service-bus-brokered-tutorial-dotnet.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2

