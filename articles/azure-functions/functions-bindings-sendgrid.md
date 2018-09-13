---
title: Azure Functions SendGrid bindings | Microsoft Docs
description: Azure Functions SendGrid bindings reference
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 0cd7e7c55e77863c142800cdc11d6ea144c38293
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550844"
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="998e3-103">Azure Functions SendGrid bindings</span><span class="sxs-lookup"><span data-stu-id="998e3-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="998e3-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="998e3-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="998e3-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span><span class="sxs-lookup"><span data-stu-id="998e3-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="998e3-106">This article is reference information for Azure Functions developers.</span><span class="sxs-lookup"><span data-stu-id="998e3-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="998e3-107">If you're new to Azure Functions, start with the following resources:</span><span class="sxs-lookup"><span data-stu-id="998e3-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="998e3-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="998e3-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="998e3-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span><span class="sxs-lookup"><span data-stu-id="998e3-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="998e3-110">function.json for SendGrid bindings</span><span class="sxs-lookup"><span data-stu-id="998e3-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="998e3-111">Azure Functions provides an output binding for SendGrid.</span><span class="sxs-lookup"><span data-stu-id="998e3-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="998e3-112">The SendGrid output binding enables you to create and send email programmatically.</span><span class="sxs-lookup"><span data-stu-id="998e3-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="998e3-113">The SendGrid binding supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="998e3-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="998e3-114">`name` : Required - the variable name used in function code for the request or request body.</span><span class="sxs-lookup"><span data-stu-id="998e3-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="998e3-115">This value is ```$return``` when there is only one return value.</span><span class="sxs-lookup"><span data-stu-id="998e3-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="998e3-116">`type` : Required - must be set to "sendGrid."</span><span class="sxs-lookup"><span data-stu-id="998e3-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="998e3-117">`direction` : Required - must be set to "out."</span><span class="sxs-lookup"><span data-stu-id="998e3-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="998e3-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span><span class="sxs-lookup"><span data-stu-id="998e3-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="998e3-119">`to` : the recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="998e3-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="998e3-120">`from` : the sender's email address.</span><span class="sxs-lookup"><span data-stu-id="998e3-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="998e3-121">`subject` : the subject of the email.</span><span class="sxs-lookup"><span data-stu-id="998e3-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="998e3-122">`text` : the email content.</span><span class="sxs-lookup"><span data-stu-id="998e3-122">`text` : the email content.</span></span>

<span data-ttu-id="998e3-123">Example of **function.json**:</span><span class="sxs-lookup"><span data-stu-id="998e3-123">Example of **function.json**:</span></span>

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

> [!NOTE]
> <span data-ttu-id="998e3-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span><span class="sxs-lookup"><span data-stu-id="998e3-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="998e3-125">This action safeguards your sensitive information.</span><span class="sxs-lookup"><span data-stu-id="998e3-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="998e3-126">C# example of the SendGrid output binding</span><span class="sxs-lookup"><span data-stu-id="998e3-126">C# example of the SendGrid output binding</span></span>

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="998e3-127">Node example of the SendGrid output binding</span><span class="sxs-lookup"><span data-stu-id="998e3-127">Node example of the SendGrid output binding</span></span>

```javascript
module.exports = function (context, input) {    
    var message = {
        to: "recipient@contoso.com",
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a><span data-ttu-id="998e3-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="998e3-128">Next steps</span></span>
<span data-ttu-id="998e3-129">For information about other bindings and triggers for Azure Functions, see</span><span class="sxs-lookup"><span data-stu-id="998e3-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="998e3-130">Azure Functions triggers and bindings developer reference</span><span class="sxs-lookup"><span data-stu-id="998e3-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="998e3-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="998e3-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="998e3-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="998e3-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>