---
title: Best Practices for Azure Functions | Microsoft Docs
description: Learn best practices and patterns for Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: ''
tags: ''
keywords: azure functions, patterns, best practice, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53dcaea155471d47eb61317c52d38524c05e4600
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551143"
---
# <a name="tips-for-improving-the-performance-and-reliability-of-azure-functions"></a>Tips for improving the performance and reliability of Azure Functions

##<a name="overview"></a>Overview

This article provides a collection of best practices for you to consider when implementing function apps. Keep in mind that your function app is an app in Azure App Service. So App Service best practices also apply.


## <a name="avoid-large-long-running-functions"></a>Avoid large long running functions

Large, long-running functions can cause unexpected timeout issues. A function can be large because of many Node.js dependencies. Importing these dependencies can cause increased load times resulting in unexpected timeouts. Node.js dependencies could be explicitly loaded by multiple `require()` statements in your code. Dependencies could also be implicit, based on a single module loaded by your code that has its own internal dependencies.  

Whenever possible, refactor large functions into smaller function sets that work together and return fast responses. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit. You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function. This approach allows you to defer the actual work and return an immediate response. It is common for webhooks to require an immediate response.


## <a name="cross-function-communication"></a>Cross function communication.

When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.  The main reason is storage queues are cheaper and much easier to provision. 

Individual messages in a storage queue are limited in size to 64 KB. If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.

Service Bus topics are useful if you require message filtering before processing.

Event hubs are useful to support high volume communications.



## <a name="write-functions-to-be-stateless"></a>Write functions to be stateless 

Functions should be stateless and idempotent if possible. Associate any required state information with your data. For example, an order being processed would likely have an associated `state` member. A function could process an order based on that state while the function itself remains stateless. 

Idempotent functions are especially recommended with timer triggers. For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results. The function can exit when there is no work for a particular day. Also if a previous run failed to complete, the next run should pick up where it left off.


## <a name="write-defensive-functions"></a>Write defensive functions.

Assume your function could encounter an exception at any time. Design your functions with the ability to continue from a previous fail point during the next execution. Consider a scenario that requires the following actions:

1. Query for 10,000 rows in a db.
2. Create a queue message for each of those rows to process further down the line.
 
Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time. You need to design your functions to be prepared for it.

How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing? Track items in a set that you’ve completed. Otherwise, you might insert them again next time. This can have a serious impact on your work flow. 

If a queue item was already processed, allow your function to be a no-op.

Take advantage of defensive measures already provided for components you use in the Azure Functions platform. For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a>Don't mix test and production code in the same function app.

Functions within a function app share resources. For example, memory is shared. If you're using a function app in production, don't add test-related functions and resources to it. It can cause unexpected overhead during production code execution.

Be careful what you load in your production function apps. Memory is averaged across each function in the app.

If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder. Reference the assembly with a statement similar to the following example: 

    #r "..\Shared\MyAssembly.dll". 

Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.

Don't use verbose logging in production code. It has a negative performance impact.



## <a name="use-async-code-but-avoid-taskresult"></a>Use async code but avoid Task.Result

Asynchronous programming is a recommended best practice. However, always avoid referencing the `Task.Result` property. This approach essentially does a busy-wait on a lock of another thread. Holding a lock creates the potential for deadlocks.




## <a name="next-steps"></a>Next steps
For more information, see the following resources:

* [Azure Functions developer reference](functions-reference.md)
* [Azure Functions C# developer reference](functions-reference-csharp.md)
* [Azure Functions F# developer reference](functions-reference-fsharp.md)
* [Azure Functions NodeJS developer reference](functions-reference-node.md)
* [Patterns and Practices HTTP Performance Optimizations](https://github.com/mspnp/performance-optimization/blob/master/ImproperInstantiation/docs/ImproperInstantiation.md)

