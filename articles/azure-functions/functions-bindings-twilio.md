---
title: Azure Functions Twilio binding
description: Understand how to use Twilio bindings with Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
ms.date: 07/09/2018
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6fc563c4d75551d441880a915dea0e1871deae46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773948"
---
# <a name="twilio-binding-for-azure-functions"></a><span data-ttu-id="4a290-104">Twilio binding for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4a290-104">Twilio binding for Azure Functions</span></span>

<span data-ttu-id="4a290-105">This article explains how to send text messages by using [Twilio](https://www.twilio.com/) bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4a290-105">This article explains how to send text messages by using [Twilio](https://www.twilio.com/) bindings in Azure Functions.</span></span> <span data-ttu-id="4a290-106">Azure Functions supports output bindings for Twilio.</span><span class="sxs-lookup"><span data-stu-id="4a290-106">Azure Functions supports output bindings for Twilio.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="4a290-107">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="4a290-107">Packages - Functions 1.x</span></span>

<span data-ttu-id="4a290-108">The Twilio bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Twilio](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio) NuGet package, version 1.x.</span><span class="sxs-lookup"><span data-stu-id="4a290-108">The Twilio bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Twilio](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio) NuGet package, version 1.x.</span></span> <span data-ttu-id="4a290-109">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.Twilio/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="4a290-109">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.Twilio/) GitHub repository.</span></span>

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="4a290-110">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="4a290-110">Packages - Functions 2.x</span></span>

<span data-ttu-id="4a290-111">The Twilio bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Twilio](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="4a290-111">The Twilio bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.Twilio](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio) NuGet package, version 3.x.</span></span> <span data-ttu-id="4a290-112">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="4a290-112">Source code for the package is in the [azure-webjobs-sdk](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="example---functions-1x"></a><span data-ttu-id="4a290-113">Example - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="4a290-113">Example - Functions 1.x</span></span>

<span data-ttu-id="4a290-114">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="4a290-114">See the language-specific example:</span></span>

* [<span data-ttu-id="4a290-115">C#</span><span class="sxs-lookup"><span data-stu-id="4a290-115">C#</span></span>](#c-example)
* [<span data-ttu-id="4a290-116">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="4a290-116">C# script (.csx)</span></span>](#c-script-example)
* [<span data-ttu-id="4a290-117">JavaScript</span><span class="sxs-lookup"><span data-stu-id="4a290-117">JavaScript</span></span>](#javascript-example)

### <a name="c-example"></a><span data-ttu-id="4a290-118">C# example</span><span class="sxs-lookup"><span data-stu-id="4a290-118">C# example</span></span>

<span data-ttu-id="4a290-119">The following example shows a [C# function](functions-dotnet-class-library.md) that sends a text message when triggered by a queue message.</span><span class="sxs-lookup"><span data-stu-id="4a290-119">The following example shows a [C# function](functions-dotnet-class-library.md) that sends a text message when triggered by a queue message.</span></span>

```cs
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

<span data-ttu-id="4a290-120">This example uses the `TwilioSms` attribute with the method return value.</span><span class="sxs-lookup"><span data-stu-id="4a290-120">This example uses the `TwilioSms` attribute with the method return value.</span></span> <span data-ttu-id="4a290-121">An alternative is to use the attribute with an `out SMSMessage` parameter or an `ICollector<SMSMessage>` or `IAsyncCollector<SMSMessage>` parameter.</span><span class="sxs-lookup"><span data-stu-id="4a290-121">An alternative is to use the attribute with an `out SMSMessage` parameter or an `ICollector<SMSMessage>` or `IAsyncCollector<SMSMessage>` parameter.</span></span>

### <a name="c-script-example"></a><span data-ttu-id="4a290-122">C# script example</span><span class="sxs-lookup"><span data-stu-id="4a290-122">C# script example</span></span>

<span data-ttu-id="4a290-123">The following example shows a Twilio output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="4a290-123">The following example shows a Twilio output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="4a290-124">The function uses an `out` parameter to send a text message.</span><span class="sxs-lookup"><span data-stu-id="4a290-124">The function uses an `out` parameter to send a text message.</span></span>

<span data-ttu-id="4a290-125">Here's binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="4a290-125">Here's binding data in the *function.json* file:</span></span>

<span data-ttu-id="4a290-126">Example function.json:</span><span class="sxs-lookup"><span data-stu-id="4a290-126">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```

<span data-ttu-id="4a290-127">Here's C# script code:</span><span class="sxs-lookup"><span data-stu-id="4a290-127">Here's C# script code:</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

<span data-ttu-id="4a290-128">You can't use out parameters in asynchronous code.</span><span class="sxs-lookup"><span data-stu-id="4a290-128">You can't use out parameters in asynchronous code.</span></span> <span data-ttu-id="4a290-129">Here's an asynchronous C# script code example:</span><span class="sxs-lookup"><span data-stu-id="4a290-129">Here's an asynchronous C# script code example:</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

### <a name="javascript-example"></a><span data-ttu-id="4a290-130">JavaScript example</span><span class="sxs-lookup"><span data-stu-id="4a290-130">JavaScript example</span></span>

<span data-ttu-id="4a290-131">The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="4a290-131">The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span>

<span data-ttu-id="4a290-132">Here's binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="4a290-132">Here's binding data in the *function.json* file:</span></span>

<span data-ttu-id="4a290-133">Example function.json:</span><span class="sxs-lookup"><span data-stu-id="4a290-133">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```

<span data-ttu-id="4a290-134">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="4a290-134">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="example---functions-2x"></a><span data-ttu-id="4a290-135">Example - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="4a290-135">Example - Functions 2.x</span></span>

<span data-ttu-id="4a290-136">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="4a290-136">See the language-specific example:</span></span>

* [<span data-ttu-id="4a290-137">2.x C#</span><span class="sxs-lookup"><span data-stu-id="4a290-137">2.x C#</span></span>](#2x-c-example)
* [<span data-ttu-id="4a290-138">2.x C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="4a290-138">2.x C# script (.csx)</span></span>](#2x-c-script-example)
* [<span data-ttu-id="4a290-139">2.x JavaScript</span><span class="sxs-lookup"><span data-stu-id="4a290-139">2.x JavaScript</span></span>](#2x-javascript-example)

### <a name="2x-c-example"></a><span data-ttu-id="4a290-140">2.x C# example</span><span class="sxs-lookup"><span data-stu-id="4a290-140">2.x C# example</span></span>

<span data-ttu-id="4a290-141">The following example shows a [C# function](functions-dotnet-class-library.md) that sends a text message when triggered by a queue message.</span><span class="sxs-lookup"><span data-stu-id="4a290-141">The following example shows a [C# function](functions-dotnet-class-library.md) that sends a text message when triggered by a queue message.</span></span>

```cs
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static CreateMessageOptions Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new CreateMessageOptions(new PhoneNumber(order["mobileNumber"].ToString()))
    {
        Body = $"Hello {order["name"]}, thanks for your order!"
    };

    return message;
}
```

<span data-ttu-id="4a290-142">This example uses the `TwilioSms` attribute with the method return value.</span><span class="sxs-lookup"><span data-stu-id="4a290-142">This example uses the `TwilioSms` attribute with the method return value.</span></span> <span data-ttu-id="4a290-143">An alternative is to use the attribute with an `out CreateMessageOptions` parameter or an `ICollector<CreateMessageOptions>` or `IAsyncCollector<CreateMessageOptions>` parameter.</span><span class="sxs-lookup"><span data-stu-id="4a290-143">An alternative is to use the attribute with an `out CreateMessageOptions` parameter or an `ICollector<CreateMessageOptions>` or `IAsyncCollector<CreateMessageOptions>` parameter.</span></span>

### <a name="2x-c-script-example"></a><span data-ttu-id="4a290-144">2.x C# script example</span><span class="sxs-lookup"><span data-stu-id="4a290-144">2.x C# script example</span></span>

<span data-ttu-id="4a290-145">The following example shows a Twilio output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="4a290-145">The following example shows a Twilio output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span> <span data-ttu-id="4a290-146">The function uses an `out` parameter to send a text message.</span><span class="sxs-lookup"><span data-stu-id="4a290-146">The function uses an `out` parameter to send a text message.</span></span>

<span data-ttu-id="4a290-147">Here's binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="4a290-147">Here's binding data in the *function.json* file:</span></span>

<span data-ttu-id="4a290-148">Example function.json:</span><span class="sxs-lookup"><span data-stu-id="4a290-148">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```

<span data-ttu-id="4a290-149">Here's C# script code:</span><span class="sxs-lookup"><span data-stu-id="4a290-149">Here's C# script code:</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;

public static void Run(string myQueueItem, out CreateMessageOptions message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least
    // initialize the CreateMessageOptions variable.
    message = new CreateMessageOptions(new PhoneNumber("+1704XXXXXXX"));

    // A dynamic message can be set instead of the body in the output binding. In this example, we use
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

<span data-ttu-id="4a290-150">You can't use out parameters in asynchronous code.</span><span class="sxs-lookup"><span data-stu-id="4a290-150">You can't use out parameters in asynchronous code.</span></span> <span data-ttu-id="4a290-151">Here's an asynchronous C# script code example:</span><span class="sxs-lookup"><span data-stu-id="4a290-151">Here's an asynchronous C# script code example:</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;

public static async Task Run(string myQueueItem, IAsyncCollector<CreateMessageOptions> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least
    // initialize the CreateMessageOptions variable.
    CreateMessageOptions smsText = new CreateMessageOptions(new PhoneNumber("+1704XXXXXXX"));

    // A dynamic message can be set instead of the body in the output binding. In this example, we use
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

### <a name="2x-javascript-example"></a><span data-ttu-id="4a290-152">2.x JavaScript example</span><span class="sxs-lookup"><span data-stu-id="4a290-152">2.x JavaScript example</span></span>

<span data-ttu-id="4a290-153">The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="4a290-153">The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span>

<span data-ttu-id="4a290-154">Here's binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="4a290-154">Here's binding data in the *function.json* file:</span></span>

<span data-ttu-id="4a290-155">Example function.json:</span><span class="sxs-lookup"><span data-stu-id="4a290-155">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```

<span data-ttu-id="4a290-156">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="4a290-156">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="attributes"></a><span data-ttu-id="4a290-157">Attributes</span><span class="sxs-lookup"><span data-stu-id="4a290-157">Attributes</span></span>

<span data-ttu-id="4a290-158">In [C# class libraries](functions-dotnet-class-library.md), use the [TwilioSms](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="4a290-158">In [C# class libraries](functions-dotnet-class-library.md), use the [TwilioSms](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) attribute.</span></span>

<span data-ttu-id="4a290-159">For information about attribute properties that you can configure, see [Configuration](#configuration).</span><span class="sxs-lookup"><span data-stu-id="4a290-159">For information about attribute properties that you can configure, see [Configuration](#configuration).</span></span> <span data-ttu-id="4a290-160">Here's a `TwilioSms` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="4a290-160">Here's a `TwilioSms` attribute example in a method signature:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(
    AccountSidSetting = "TwilioAccountSid", 
    AuthTokenSetting = "TwilioAuthToken", 
    From = "+1425XXXXXXX" )]
public static SMSMessage Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order,
    TraceWriter log)
{
    ...
}
 ```

<span data-ttu-id="4a290-161">For a complete example, see [C# example](#c-example).</span><span class="sxs-lookup"><span data-stu-id="4a290-161">For a complete example, see [C# example](#c-example).</span></span>

## <a name="configuration"></a><span data-ttu-id="4a290-162">Configuration</span><span class="sxs-lookup"><span data-stu-id="4a290-162">Configuration</span></span>

<span data-ttu-id="4a290-163">The following table explains the binding configuration properties that you set in the *function.json* file and the `TwilioSms` attribute.</span><span class="sxs-lookup"><span data-stu-id="4a290-163">The following table explains the binding configuration properties that you set in the *function.json* file and the `TwilioSms` attribute.</span></span>

|<span data-ttu-id="4a290-164">function.json property</span><span class="sxs-lookup"><span data-stu-id="4a290-164">function.json property</span></span> | <span data-ttu-id="4a290-165">Attribute property</span><span class="sxs-lookup"><span data-stu-id="4a290-165">Attribute property</span></span> |<span data-ttu-id="4a290-166">Description</span><span class="sxs-lookup"><span data-stu-id="4a290-166">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="4a290-167">**type**</span><span class="sxs-lookup"><span data-stu-id="4a290-167">**type**</span></span>|| <span data-ttu-id="4a290-168">must be set to `twilioSms`.</span><span class="sxs-lookup"><span data-stu-id="4a290-168">must be set to `twilioSms`.</span></span>|
|<span data-ttu-id="4a290-169">**direction**</span><span class="sxs-lookup"><span data-stu-id="4a290-169">**direction**</span></span>|| <span data-ttu-id="4a290-170">must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="4a290-170">must be set to `out`.</span></span>|
|<span data-ttu-id="4a290-171">**name**</span><span class="sxs-lookup"><span data-stu-id="4a290-171">**name**</span></span>|| <span data-ttu-id="4a290-172">Variable name used in function code for the Twilio SMS text message.</span><span class="sxs-lookup"><span data-stu-id="4a290-172">Variable name used in function code for the Twilio SMS text message.</span></span> |
|<span data-ttu-id="4a290-173">**accountSid**</span><span class="sxs-lookup"><span data-stu-id="4a290-173">**accountSid**</span></span>|<span data-ttu-id="4a290-174">**AccountSid**</span><span class="sxs-lookup"><span data-stu-id="4a290-174">**AccountSid**</span></span>| <span data-ttu-id="4a290-175">This value must be set to the name of an app setting that holds your Twilio Account Sid.</span><span class="sxs-lookup"><span data-stu-id="4a290-175">This value must be set to the name of an app setting that holds your Twilio Account Sid.</span></span>|
|<span data-ttu-id="4a290-176">**authToken**</span><span class="sxs-lookup"><span data-stu-id="4a290-176">**authToken**</span></span>|<span data-ttu-id="4a290-177">**AuthToken**</span><span class="sxs-lookup"><span data-stu-id="4a290-177">**AuthToken**</span></span>| <span data-ttu-id="4a290-178">This value must be set to the name of an app setting that holds your Twilio authentication token.</span><span class="sxs-lookup"><span data-stu-id="4a290-178">This value must be set to the name of an app setting that holds your Twilio authentication token.</span></span>|
|<span data-ttu-id="4a290-179">**to**</span><span class="sxs-lookup"><span data-stu-id="4a290-179">**to**</span></span>|<span data-ttu-id="4a290-180">**To**</span><span class="sxs-lookup"><span data-stu-id="4a290-180">**To**</span></span>| <span data-ttu-id="4a290-181">This value is set to the phone number that the SMS text is sent to.</span><span class="sxs-lookup"><span data-stu-id="4a290-181">This value is set to the phone number that the SMS text is sent to.</span></span>|
|<span data-ttu-id="4a290-182">**from**</span><span class="sxs-lookup"><span data-stu-id="4a290-182">**from**</span></span>|<span data-ttu-id="4a290-183">**From**</span><span class="sxs-lookup"><span data-stu-id="4a290-183">**From**</span></span>| <span data-ttu-id="4a290-184">This value is set to the phone number that the SMS text is sent from.</span><span class="sxs-lookup"><span data-stu-id="4a290-184">This value is set to the phone number that the SMS text is sent from.</span></span>|
|<span data-ttu-id="4a290-185">**body**</span><span class="sxs-lookup"><span data-stu-id="4a290-185">**body**</span></span>|<span data-ttu-id="4a290-186">**Body**</span><span class="sxs-lookup"><span data-stu-id="4a290-186">**Body**</span></span>| <span data-ttu-id="4a290-187">This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span><span class="sxs-lookup"><span data-stu-id="4a290-187">This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="next-steps"></a><span data-ttu-id="4a290-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="4a290-188">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a290-189">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="4a290-189">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
