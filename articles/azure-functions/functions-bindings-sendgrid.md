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
# <a name="azure-functions-sendgrid-bindings"></a>Azure Functions SendGrid bindings

This article explains how to send email by using [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) bindings in Azure Functions. Azure Functions supports an output binding for SendGrid.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a>Packages - Functions 1.x

The SendGrid bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid) NuGet package, version 2.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.SendGrid/) GitHub repository.

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="packages---functions-2x"></a>Packages - Functions 2.x

The SendGrid bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid) NuGet package, version 3.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/) GitHub repository.

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="example"></a>Example

See the language-specific example:

* [C#](#c-example)
* [C# script (.csx)](#c-script-example)
* [JavaScript](#javascript-example)

### <a name="c-example"></a>C# example

The following example shows a [C# function](functions-dotnet-class-library.md) that uses a Service Bus queue trigger and a SendGrid output binding.

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

You can omit setting the attribute's `ApiKey` property if you have your API key in an app setting named "AzureWebJobsSendGridApiKey".

### <a name="c-script-example"></a>C# script example

The following example shows a SendGrid output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding.

Here's the binding data in the *function.json* file:

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

The [configuration](#configuration) section explains these properties.

Here's the C# script code:

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

### <a name="javascript-example"></a>JavaScript example

The following example shows a SendGrid output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding.

Here's the binding data in the *function.json* file:

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

The [configuration](#configuration) section explains these properties.

Here's the JavaScript code:

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

## <a name="attributes"></a>Attributes

In [C# class libraries](functions-dotnet-class-library.md), use the [SendGrid](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs) attribute.

For information about attribute properties that you can configure, see [Configuration](#configuration). Here's a `SendGrid` attribute example in a method signature:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid(ApiKey = "CustomSendGridKeyAppSettingName")] out SendGridMessage message)
{
    ...
}
```

For a complete example, see [C# example](#c-example).

## <a name="configuration"></a>Configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `SendGrid` attribute.

|function.json property | Attribute property |Description|
|---------|---------|----------------------|
|**type**|| Required - must be set to `sendGrid`.|
|**direction**|| Required - must be set to `out`.|
|**name**|| Required - the variable name used in function code for the request or request body. This value is ```$return``` when there is only one return value. |
|**apiKey**|**ApiKey**| The name of an app setting that contains your API key. If not set, the default app setting name is "AzureWebJobsSendGridApiKey".|
|**to**|**To**| the recipient's email address. |
|**from**|**From**| the sender's email address. |
|**subject**|**Subject**| the subject of the email. |
|**text**|**Text**| the email content. |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Learn more about Azure functions triggers and bindings](functions-triggers-bindings.md)
