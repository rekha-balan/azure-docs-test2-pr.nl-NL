---
title: Azure Functions timer trigger | Microsoft Docs
description: Understand how to use timer triggers in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: chrande; glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 146884833e968767c14d7e4f924762a592e427e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551326"
---
# <a name="schedule-code-execution-with-azure-functions"></a><span data-ttu-id="9fe43-104">Schedule code execution with Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9fe43-104">Schedule code execution with Azure Functions</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="9fe43-105">This article explains how to configure and code timer triggers in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="9fe43-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="9fe43-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span><span class="sxs-lookup"><span data-stu-id="9fe43-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="9fe43-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span><span class="sxs-lookup"><span data-stu-id="9fe43-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="9fe43-108">Timer trigger</span><span class="sxs-lookup"><span data-stu-id="9fe43-108">Timer trigger</span></span>
<span data-ttu-id="9fe43-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="9fe43-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="9fe43-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span><span class="sxs-lookup"><span data-stu-id="9fe43-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="9fe43-111">Many of the cron expressions you find online omit the `{second}` field.</span><span class="sxs-lookup"><span data-stu-id="9fe43-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="9fe43-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span><span class="sxs-lookup"><span data-stu-id="9fe43-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="9fe43-113">For specific examples, see [Schedule examples](#examples) below.</span><span class="sxs-lookup"><span data-stu-id="9fe43-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="9fe43-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="9fe43-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="9fe43-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="9fe43-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="9fe43-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fe43-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="9fe43-117">For example, *Eastern Standard Time* is UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="9fe43-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="9fe43-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span><span class="sxs-lookup"><span data-stu-id="9fe43-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="9fe43-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span><span class="sxs-lookup"><span data-stu-id="9fe43-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="9fe43-120">Then the following CRON expression could be used for 10:00 AM EST:</span><span class="sxs-lookup"><span data-stu-id="9fe43-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="9fe43-121">Schedule examples</span><span class="sxs-lookup"><span data-stu-id="9fe43-121">Schedule examples</span></span>
<span data-ttu-id="9fe43-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span><span class="sxs-lookup"><span data-stu-id="9fe43-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="9fe43-123">To trigger once every five minutes:</span><span class="sxs-lookup"><span data-stu-id="9fe43-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="9fe43-124">To trigger once at the top of every hour:</span><span class="sxs-lookup"><span data-stu-id="9fe43-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="9fe43-125">To trigger once every two hours:</span><span class="sxs-lookup"><span data-stu-id="9fe43-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="9fe43-126">To trigger once every hour from 9 AM to 5 PM:</span><span class="sxs-lookup"><span data-stu-id="9fe43-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="9fe43-127">To trigger At 9:30 AM every day:</span><span class="sxs-lookup"><span data-stu-id="9fe43-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="9fe43-128">To trigger At 9:30 AM every weekday:</span><span class="sxs-lookup"><span data-stu-id="9fe43-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="9fe43-129">Trigger usage</span><span class="sxs-lookup"><span data-stu-id="9fe43-129">Trigger usage</span></span>
<span data-ttu-id="9fe43-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span><span class="sxs-lookup"><span data-stu-id="9fe43-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="9fe43-131">The following JSON is an example representation of the timer object.</span><span class="sxs-lookup"><span data-stu-id="9fe43-131">The following JSON is an example representation of the timer object.</span></span> 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="9fe43-132">Trigger sample</span><span class="sxs-lookup"><span data-stu-id="9fe43-132">Trigger sample</span></span>
<span data-ttu-id="9fe43-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span><span class="sxs-lookup"><span data-stu-id="9fe43-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="9fe43-134">See the language-specific sample that reads the timer object to see whether it's running late.</span><span class="sxs-lookup"><span data-stu-id="9fe43-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="9fe43-135">C#</span><span class="sxs-lookup"><span data-stu-id="9fe43-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="9fe43-136">F#</span><span class="sxs-lookup"><span data-stu-id="9fe43-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="9fe43-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="9fe43-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="9fe43-138">Trigger sample in C#</span><span class="sxs-lookup"><span data-stu-id="9fe43-138">Trigger sample in C#</span></span> #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="9fe43-139">Trigger sample in F#</span><span class="sxs-lookup"><span data-stu-id="9fe43-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="9fe43-140">Trigger sample in Node.js</span><span class="sxs-lookup"><span data-stu-id="9fe43-140">Trigger sample in Node.js</span></span>
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="9fe43-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="9fe43-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

