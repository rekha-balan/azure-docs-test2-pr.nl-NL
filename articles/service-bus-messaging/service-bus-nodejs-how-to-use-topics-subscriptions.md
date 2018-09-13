---
title: How to use Azure Service Bus topics and subscriptions with Node.js | Microsoft Docs
description: Learn how to use Service Bus topics and subscriptions in Azure from a Node.js app.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/12/2017
ms.author: sethm
ms.openlocfilehash: 24375a7c56cdad59363803ef3aae724977961b44
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553239"
---
# <a name="how-to-use-service-bus-topics-and-subscriptions"></a><span data-ttu-id="fa3d7-103">How to Use Service Bus topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="fa3d7-103">How to Use Service Bus topics and subscriptions</span></span>
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="fa3d7-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="fa3d7-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="fa3d7-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="fa3d7-107">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="fa3d7-107">Create a Node.js application</span></span>
<span data-ttu-id="fa3d7-108">Create a blank Node.js application.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-108">Create a blank Node.js application.</span></span> <span data-ttu-id="fa3d7-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="fa3d7-110">Configure your application to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="fa3d7-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="fa3d7-111">To use Service Bus, download the Node.js Azure package.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="fa3d7-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="fa3d7-113">Use Node Package Manager (NPM) to obtain the package</span><span class="sxs-lookup"><span data-stu-id="fa3d7-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="fa3d7-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="fa3d7-115">Type **npm install azure** in the command window, which should result in the following output:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. <span data-ttu-id="fa3d7-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="fa3d7-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="fa3d7-118">Import the module</span><span class="sxs-lookup"><span data-stu-id="fa3d7-118">Import the module</span></span>
<span data-ttu-id="fa3d7-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="fa3d7-120">Set up a Service Bus connection</span><span class="sxs-lookup"><span data-stu-id="fa3d7-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="fa3d7-121">The Azure module reads the environment variables AZURE\_SERVICEBUS\_NAMESPACE and AZURE\_SERVICEBUS\_ACCESS\_KEY for information required to connect to Service Bus.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-121">The Azure module reads the environment variables AZURE\_SERVICEBUS\_NAMESPACE and AZURE\_SERVICEBUS\_ACCESS\_KEY for information required to connect to Service Bus.</span></span> <span data-ttu-id="fa3d7-122">If these environment variables are not set, you must specify the account information when calling **createServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-122">If these environment variables are not set, you must specify the account information when calling **createServiceBusService**.</span></span>

<span data-ttu-id="fa3d7-123">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="fa3d7-123">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="fa3d7-124">For an example of setting the environment variables in the [Azure classic portal][Azure classic portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="fa3d7-124">For an example of setting the environment variables in the [Azure classic portal][Azure classic portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="fa3d7-125">Create a topic</span><span class="sxs-lookup"><span data-stu-id="fa3d7-125">Create a topic</span></span>
<span data-ttu-id="fa3d7-126">The **ServiceBusService** object enables you to work with topics.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="fa3d7-127">The following code creates a **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="fa3d7-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="fa3d7-129">By calling **createTopicIfNotExists** on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-129">By calling **createTopicIfNotExists** on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="fa3d7-130">The following code uses **createTopicIfNotExists** to create or connect to the topic named 'MyTopic':</span><span class="sxs-lookup"><span data-stu-id="fa3d7-130">The following code uses **createTopicIfNotExists** to create or connect to the topic named 'MyTopic':</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="fa3d7-131">**createServiceBusService** also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-131">**createServiceBusService** also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="fa3d7-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="fa3d7-133">Filters</span><span class="sxs-lookup"><span data-stu-id="fa3d7-133">Filters</span></span>
<span data-ttu-id="fa3d7-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="fa3d7-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="fa3d7-136">After performing preprocessing on the request options, the method calls `next` passing a callback with the following signature:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-136">After performing preprocessing on the request options, the method calls `next` passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="fa3d7-137">In this callback, and after processing the **returnObject** (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke **finalCallback** otherwise to end up the service invocation.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-137">In this callback, and after processing the **returnObject** (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke **finalCallback** otherwise to end up the service invocation.</span></span>

<span data-ttu-id="fa3d7-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="fa3d7-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="fa3d7-140">Create subscriptions</span><span class="sxs-lookup"><span data-stu-id="fa3d7-140">Create subscriptions</span></span>
<span data-ttu-id="fa3d7-141">Topic subscriptions are also created with the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="fa3d7-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="fa3d7-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="fa3d7-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the **getSubscription** method.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the **getSubscription** method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="fa3d7-145">Create a subscription with the default (MatchAll) filter</span><span class="sxs-lookup"><span data-stu-id="fa3d7-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="fa3d7-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="fa3d7-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="fa3d7-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="fa3d7-149">Create subscriptions with filters</span><span class="sxs-lookup"><span data-stu-id="fa3d7-149">Create subscriptions with filters</span></span>
<span data-ttu-id="fa3d7-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="fa3d7-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="fa3d7-152">SQL filters operate on the properties of the messages that are published to the topic.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="fa3d7-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="fa3d7-154">Filters can be added to a subscription by using the **createRule** method of the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-154">Filters can be added to a subscription by using the **createRule** method of the **ServiceBusService** object.</span></span> <span data-ttu-id="fa3d7-155">This method allows you to add new filters to an existing subscription.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fa3d7-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="fa3d7-157">You can remove the default rule by using the **deleteRule** method of the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-157">You can remove the default rule by using the **deleteRule** method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="fa3d7-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom **messagenumber** property greater than 3:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom **messagenumber** property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="fa3d7-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a **messagenumber** property less than or equal to 3:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a **messagenumber** property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="fa3d7-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span><span class="sxs-lookup"><span data-stu-id="fa3d7-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="fa3d7-161">How to send messages to a topic</span><span class="sxs-lookup"><span data-stu-id="fa3d7-161">How to send messages to a topic</span></span>
<span data-ttu-id="fa3d7-162">To send a message to a Service Bus topic, your application must use the **sendTopicMessage** method of the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-162">To send a message to a Service Bus topic, your application must use the **sendTopicMessage** method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="fa3d7-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="fa3d7-164">**BrokeredMessage** objects have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-164">**BrokeredMessage** objects have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="fa3d7-165">An application can set the body of the message by passing a string value to the **sendTopicMessage** and any required standard properties will be populated by default values.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-165">An application can set the body of the message by passing a string value to the **sendTopicMessage** and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="fa3d7-166">The following example demonstrates how to send five test messages to 'MyTopic'.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-166">The following example demonstrates how to send five test messages to 'MyTopic'.</span></span> <span data-ttu-id="fa3d7-167">Note that the **messagenumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span><span class="sxs-lookup"><span data-stu-id="fa3d7-167">Note that the **messagenumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="fa3d7-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="fa3d7-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="fa3d7-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="fa3d7-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="fa3d7-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="fa3d7-172">Receive messages from a subscription</span><span class="sxs-lookup"><span data-stu-id="fa3d7-172">Receive messages from a subscription</span></span>
<span data-ttu-id="fa3d7-173">Messages are received from a subscription using the **receiveSubscriptionMessage** method on the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-173">Messages are received from a subscription using the **receiveSubscriptionMessage** method on the **ServiceBusService** object.</span></span> <span data-ttu-id="fa3d7-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter **isPeekLock** to **true**.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter **isPeekLock** to **true**.</span></span>

<span data-ttu-id="fa3d7-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="fa3d7-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="fa3d7-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="fa3d7-178">If the **isPeekLock** parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-178">If the **isPeekLock** parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="fa3d7-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="fa3d7-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="fa3d7-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="fa3d7-182">The following example demonstrates how messages can be received and processed using **receiveSubscriptionMessage**.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-182">The following example demonstrates how messages can be received and processed using **receiveSubscriptionMessage**.</span></span> <span data-ttu-id="fa3d7-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using **isPeekLock** set to true.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using **isPeekLock** set to true.</span></span> <span data-ttu-id="fa3d7-184">It then deletes the message using **deleteMessage**:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-184">It then deletes the message using **deleteMessage**:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="fa3d7-185">How to handle application crashes and unreadable messages</span><span class="sxs-lookup"><span data-stu-id="fa3d7-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="fa3d7-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="fa3d7-187">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-187">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the **ServiceBusService** object.</span></span> <span data-ttu-id="fa3d7-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="fa3d7-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="fa3d7-190">In the event that the application crashes after processing the message but before the **deleteMessage** method is called, then the message will be redelivered to the application when it restarts.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-190">In the event that the application crashes after processing the message but before the **deleteMessage** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="fa3d7-191">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-191">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="fa3d7-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="fa3d7-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="fa3d7-194">Delete topics and subscriptions</span><span class="sxs-lookup"><span data-stu-id="fa3d7-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="fa3d7-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure classic portal][Azure classic portal] or programmatically.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure classic portal][Azure classic portal] or programmatically.</span></span>
<span data-ttu-id="fa3d7-196">The following example demonstrates how to delete the topic named `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="fa3d7-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="fa3d7-198">Subscriptions can also be deleted independently.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="fa3d7-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span><span class="sxs-lookup"><span data-stu-id="fa3d7-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="fa3d7-200">Next Steps</span><span class="sxs-lookup"><span data-stu-id="fa3d7-200">Next Steps</span></span>
<span data-ttu-id="fa3d7-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="fa3d7-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="fa3d7-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="fa3d7-203">API reference for [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="fa3d7-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="fa3d7-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa3d7-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure classic portal]: https://manage.windowsazure.com
[SqlFilter.SqlExpression]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Create and deploy a Node.js application to an Azure Web Site]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]: ../storage/storage-nodejs-use-table-storage-cloud-service-app.md
