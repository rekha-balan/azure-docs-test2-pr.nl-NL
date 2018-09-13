---
title: Azure Functions SendGrid bindings
description: Azure Functions SendGrid bindings reference.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 11/29/2017
ms.author: glenga
ms.openlocfilehash: 212f8b0dacf5fa56e48df99fb10b11da54df57ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783814"
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="1ad87-103">Azure Functions SendGrid bindings</span><span class="sxs-lookup"><span data-stu-id="1ad87-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="1ad87-104">This article explains how to send email by using [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1ad87-104">This article explains how to send email by using [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) bindings in Azure Functions.</span></span> <span data-ttu-id="1ad87-105">Azure Functions supports an output binding for SendGrid.</span><span class="sxs-lookup"><span data-stu-id="1ad87-105">Azure Functions supports an output binding for SendGrid.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a><span data-ttu-id="1ad87-106">Packages - Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="1ad87-106">Packages - Functions 1.x</span></span>

<span data-ttu-id="1ad87-107">The SendGrid bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid) NuGet package, version 2.x.</span><span class="sxs-lookup"><span data-stu-id="1ad87-107">The SendGrid bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid) NuGet package, version 2.x.</span></span> <span data-ttu-id="1ad87-108">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.SendGrid/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="1ad87-108">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.SendGrid/) GitHub repository.</span></span>

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="packages---functions-2x"></a><span data-ttu-id="1ad87-109">Packages - Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="1ad87-109">Packages - Functions 2.x</span></span>

<span data-ttu-id="1ad87-110">The SendGrid bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid) NuGet package, version 3.x.</span><span class="sxs-lookup"><span data-stu-id="1ad87-110">The SendGrid bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid) NuGet package, version 3.x.</span></span> <span data-ttu-id="1ad87-111">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="1ad87-111">Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/) GitHub repository.</span></span>

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="example"></a><span data-ttu-id="1ad87-112">Example</span><span class="sxs-lookup"><span data-stu-id="1ad87-112">Example</span></span>

<span data-ttu-id="1ad87-113">See the language-specific example:</span><span class="sxs-lookup"><span data-stu-id="1ad87-113">See the language-specific example:</span></span>

* [<span data-ttu-id="1ad87-114">C#</span><span class="sxs-lookup"><span data-stu-id="1ad87-114">C#</span></span>](#c-example)
* [<span data-ttu-id="1ad87-115">C# script (.csx)</span><span class="sxs-lookup"><span data-stu-id="1ad87-115">C# script (.csx)</span></span>](#c-script-example)
* [<span data-ttu-id="1ad87-116">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1ad87-116">JavaScript</span></span>](#javascript-example)

### <a name="c-example"></a><span data-ttu-id="1ad87-117">C# example</span><span class="sxs-lookup"><span data-stu-id="1ad87-117">C# example</span></span>

<span data-ttu-id="1ad87-118">The following example shows a [C# function](functions-dotnet-class-library.md) that uses a Service Bus queue trigger and a SendGrid output binding.</span><span class="sxs-lookup"><span data-stu-id="1ad87-118">The following example shows a [C# function](functions-dotnet-class-library.md) that uses a Service Bus queue trigger and a SendGrid output binding.</span></span>

```cs
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid(ApiKey = "CustomSendGridKeyAppSettingName")] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<span data-ttu-id="1ad87-119">You can omit setting the attribute's `ApiKey` property if you have your API key in an app setting named "AzureWebJobsSendGridApiKey".</span><span class="sxs-lookup"><span data-stu-id="1ad87-119">You can omit setting the attribute's `ApiKey` property if you have your API key in an app setting named "AzureWebJobsSendGridApiKey".</span></span>

### <a name="c-script-example"></a><span data-ttu-id="1ad87-120">C# script example</span><span class="sxs-lookup"><span data-stu-id="1ad87-120">C# script example</span></span>

<span data-ttu-id="1ad87-121">The following example shows a SendGrid output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1ad87-121">The following example shows a SendGrid output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.</span></span>

<span data-ttu-id="1ad87-122">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1ad87-122">Here's the binding data in the *function.json* file:</span></span>

```json 
{
    "bindings": [
        {
            "name": "message",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

<span data-ttu-id="1ad87-123">The [configuration](#configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1ad87-123">The [configuration](#configuration) section explains these properties.</span></span>

<span data-ttu-id="1ad87-124">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="1ad87-124">Here's the C# script code:</span></span>

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

### <a name="javascript-example"></a><span data-ttu-id="1ad87-125">JavaScript example</span><span class="sxs-lookup"><span data-stu-id="1ad87-125">JavaScript example</span></span>

<span data-ttu-id="1ad87-126">The following example shows a SendGrid output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span><span class="sxs-lookup"><span data-stu-id="1ad87-126">The following example shows a SendGrid output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.</span></span>

<span data-ttu-id="1ad87-127">Here's the binding data in the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="1ad87-127">Here's the binding data in the *function.json* file:</span></span>

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

<span data-ttu-id="1ad87-128">The [configuration](#configuration) section explains these properties.</span><span class="sxs-lookup"><span data-stu-id="1ad87-128">The [configuration](#configuration) section explains these properties.</span></span>

<span data-ttu-id="1ad87-129">Here's the JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="1ad87-129">Here's the JavaScript code:</span></span>

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: { email: "sender@contoso.com" },        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};
```

## <a name="attributes"></a><span data-ttu-id="1ad87-130">Attributes</span><span class="sxs-lookup"><span data-stu-id="1ad87-130">Attributes</span></span>

<span data-ttu-id="1ad87-131">In [C# class libraries](functions-dotnet-class-library.md), use the [SendGrid](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs) attribute.</span><span class="sxs-lookup"><span data-stu-id="1ad87-131">In [C# class libraries](functions-dotnet-class-library.md), use the [SendGrid](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs) attribute.</span></span>

<span data-ttu-id="1ad87-132">For information about attribute properties that you can configure, see [Configuration](#configuration).</span><span class="sxs-lookup"><span data-stu-id="1ad87-132">For information about attribute properties that you can configure, see [Configuration](#configuration).</span></span> <span data-ttu-id="1ad87-133">Here's a `SendGrid` attribute example in a method signature:</span><span class="sxs-lookup"><span data-stu-id="1ad87-133">Here's a `SendGrid` attribute example in a method signature:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid(ApiKey = "CustomSendGridKeyAppSettingName")] out SendGridMessage message)
{
    ...
}
```

<span data-ttu-id="1ad87-134">For a complete example, see [C# example](#c-example).</span><span class="sxs-lookup"><span data-stu-id="1ad87-134">For a complete example, see [C# example](#c-example).</span></span>

## <a name="configuration"></a><span data-ttu-id="1ad87-135">Configuration</span><span class="sxs-lookup"><span data-stu-id="1ad87-135">Configuration</span></span>

<span data-ttu-id="1ad87-136">The following table explains the binding configuration properties that you set in the *function.json* file and the `SendGrid` attribute.</span><span class="sxs-lookup"><span data-stu-id="1ad87-136">The following table explains the binding configuration properties that you set in the *function.json* file and the `SendGrid` attribute.</span></span>

|<span data-ttu-id="1ad87-137">function.json property</span><span class="sxs-lookup"><span data-stu-id="1ad87-137">function.json property</span></span> | <span data-ttu-id="1ad87-138">Attribute property</span><span class="sxs-lookup"><span data-stu-id="1ad87-138">Attribute property</span></span> |<span data-ttu-id="1ad87-139">Description</span><span class="sxs-lookup"><span data-stu-id="1ad87-139">Description</span></span>|
|---------|---------|----------------------|
|<span data-ttu-id="1ad87-140">**type**</span><span class="sxs-lookup"><span data-stu-id="1ad87-140">**type**</span></span>|| <span data-ttu-id="1ad87-141">Required - must be set to `sendGrid`.</span><span class="sxs-lookup"><span data-stu-id="1ad87-141">Required - must be set to `sendGrid`.</span></span>|
|<span data-ttu-id="1ad87-142">**direction**</span><span class="sxs-lookup"><span data-stu-id="1ad87-142">**direction**</span></span>|| <span data-ttu-id="1ad87-143">Required - must be set to `out`.</span><span class="sxs-lookup"><span data-stu-id="1ad87-143">Required - must be set to `out`.</span></span>|
|<span data-ttu-id="1ad87-144">**name**</span><span class="sxs-lookup"><span data-stu-id="1ad87-144">**name**</span></span>|| <span data-ttu-id="1ad87-145">Required - the variable name used in function code for the request or request body.</span><span class="sxs-lookup"><span data-stu-id="1ad87-145">Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="1ad87-146">This value is ```$return``` when there is only one return value.</span><span class="sxs-lookup"><span data-stu-id="1ad87-146">This value is ```$return``` when there is only one return value.</span></span> |
|<span data-ttu-id="1ad87-147">**apiKey**</span><span class="sxs-lookup"><span data-stu-id="1ad87-147">**apiKey**</span></span>|<span data-ttu-id="1ad87-148">**ApiKey**</span><span class="sxs-lookup"><span data-stu-id="1ad87-148">**ApiKey**</span></span>| <span data-ttu-id="1ad87-149">The name of an app setting that contains your API key.</span><span class="sxs-lookup"><span data-stu-id="1ad87-149">The name of an app setting that contains your API key.</span></span> <span data-ttu-id="1ad87-150">If not set, the default app setting name is "AzureWebJobsSendGridApiKey".</span><span class="sxs-lookup"><span data-stu-id="1ad87-150">If not set, the default app setting name is "AzureWebJobsSendGridApiKey".</span></span>|
|<span data-ttu-id="1ad87-151">**to**</span><span class="sxs-lookup"><span data-stu-id="1ad87-151">**to**</span></span>|<span data-ttu-id="1ad87-152">**To**</span><span class="sxs-lookup"><span data-stu-id="1ad87-152">**To**</span></span>| <span data-ttu-id="1ad87-153">the recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="1ad87-153">the recipient's email address.</span></span> |
|<span data-ttu-id="1ad87-154">**from**</span><span class="sxs-lookup"><span data-stu-id="1ad87-154">**from**</span></span>|<span data-ttu-id="1ad87-155">**From**</span><span class="sxs-lookup"><span data-stu-id="1ad87-155">**From**</span></span>| <span data-ttu-id="1ad87-156">the sender's email address.</span><span class="sxs-lookup"><span data-stu-id="1ad87-156">the sender's email address.</span></span> |
|<span data-ttu-id="1ad87-157">**subject**</span><span class="sxs-lookup"><span data-stu-id="1ad87-157">**subject**</span></span>|<span data-ttu-id="1ad87-158">**Subject**</span><span class="sxs-lookup"><span data-stu-id="1ad87-158">**Subject**</span></span>| <span data-ttu-id="1ad87-159">the subject of the email.</span><span class="sxs-lookup"><span data-stu-id="1ad87-159">the subject of the email.</span></span> |
|<span data-ttu-id="1ad87-160">**text**</span><span class="sxs-lookup"><span data-stu-id="1ad87-160">**text**</span></span>|<span data-ttu-id="1ad87-161">**Text**</span><span class="sxs-lookup"><span data-stu-id="1ad87-161">**Text**</span></span>| <span data-ttu-id="1ad87-162">the email content.</span><span class="sxs-lookup"><span data-stu-id="1ad87-162">the email content.</span></span> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="next-steps"></a><span data-ttu-id="1ad87-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ad87-163">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ad87-164">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="1ad87-164">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
