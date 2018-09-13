---
title: How to disable functions in Azure Functions
description: Learn how to disable and enable functions in Azure Functions 1.x and 2.x.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.topic: conceptual
ms.date: 07/24/2018
ms.author: glenga
ms.openlocfilehash: ab9cf429a0af69db116fe910ab90b83d404afbb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856304"
---
# <a name="how-to-disable-functions-in-azure-functions"></a><span data-ttu-id="36339-103">How to disable functions in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="36339-103">How to disable functions in Azure Functions</span></span>

<span data-ttu-id="36339-104">This article explains how to disable a function in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="36339-104">This article explains how to disable a function in Azure Functions.</span></span> <span data-ttu-id="36339-105">To *disable* a function means to make the runtime ignore the automatic trigger that is defined for the function.</span><span class="sxs-lookup"><span data-stu-id="36339-105">To *disable* a function means to make the runtime ignore the automatic trigger that is defined for the function.</span></span> <span data-ttu-id="36339-106">The way you do that depends on the runtime version and the programming language:</span><span class="sxs-lookup"><span data-stu-id="36339-106">The way you do that depends on the runtime version and the programming language:</span></span>

* <span data-ttu-id="36339-107">Functions 1.x</span><span class="sxs-lookup"><span data-stu-id="36339-107">Functions 1.x</span></span>
  * <span data-ttu-id="36339-108">Scripting languages</span><span class="sxs-lookup"><span data-stu-id="36339-108">Scripting languages</span></span>
  * <span data-ttu-id="36339-109">C# class libraries</span><span class="sxs-lookup"><span data-stu-id="36339-109">C# class libraries</span></span>
* <span data-ttu-id="36339-110">Functions 2.x</span><span class="sxs-lookup"><span data-stu-id="36339-110">Functions 2.x</span></span>
  * <span data-ttu-id="36339-111">One way for all languages</span><span class="sxs-lookup"><span data-stu-id="36339-111">One way for all languages</span></span>
  * <span data-ttu-id="36339-112">Optional way for C# class libraries</span><span class="sxs-lookup"><span data-stu-id="36339-112">Optional way for C# class libraries</span></span>

## <a name="functions-1x---scripting-languages"></a><span data-ttu-id="36339-113">Functions 1.x - scripting languages</span><span class="sxs-lookup"><span data-stu-id="36339-113">Functions 1.x - scripting languages</span></span>

<span data-ttu-id="36339-114">For scripting languages such as C# script and JavaScript, you use the `disabled` property of the *function.json* file to tell the runtime not to trigger a function.</span><span class="sxs-lookup"><span data-stu-id="36339-114">For scripting languages such as C# script and JavaScript, you use the `disabled` property of the *function.json* file to tell the runtime not to trigger a function.</span></span> <span data-ttu-id="36339-115">This property can be set to `true` or to the name of an app setting:</span><span class="sxs-lookup"><span data-stu-id="36339-115">This property can be set to `true` or to the name of an app setting:</span></span>

```json
{
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionAppSetting"
        }
    ],
    "disabled": true
}
```
<span data-ttu-id="36339-116">or</span><span class="sxs-lookup"><span data-stu-id="36339-116">or</span></span> 

```json
    "bindings": [
        ...
    ],
    "disabled": "IS_DISABLED"
```

<span data-ttu-id="36339-117">In the second example, the function is disabled when there is an app setting that is named IS_DISABLED and is set to `true` or 1.</span><span class="sxs-lookup"><span data-stu-id="36339-117">In the second example, the function is disabled when there is an app setting that is named IS_DISABLED and is set to `true` or 1.</span></span>

<span data-ttu-id="36339-118">You can edit the file in the Azure portal or use the **Function State** switch on the function's **Manage** tab. The portal switch works by changing the *function.json* file.</span><span class="sxs-lookup"><span data-stu-id="36339-118">You can edit the file in the Azure portal or use the **Function State** switch on the function's **Manage** tab. The portal switch works by changing the *function.json* file.</span></span>

![Function state switch](media/disable-function/function-state-switch.png)

## <a name="functions-1x---c-class-libraries"></a><span data-ttu-id="36339-120">Functions 1.x - C# class libraries</span><span class="sxs-lookup"><span data-stu-id="36339-120">Functions 1.x - C# class libraries</span></span>

<span data-ttu-id="36339-121">In a Functions 1.x class library, you use a `Disable` attribute to prevent a function from being triggered.</span><span class="sxs-lookup"><span data-stu-id="36339-121">In a Functions 1.x class library, you use a `Disable` attribute to prevent a function from being triggered.</span></span> <span data-ttu-id="36339-122">You can use the attribute without a constructor parameter, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="36339-122">You can use the attribute without a constructor parameter, as shown in the following example:</span></span>

```csharp
public static class QueueFunctions
{
    [Disable]
    [FunctionName("QueueTrigger")]
    public static void QueueTrigger(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}
```

<span data-ttu-id="36339-123">The attribute without a constructor parameter requires that you recompile and redeploy the project to change the function's disabled state.</span><span class="sxs-lookup"><span data-stu-id="36339-123">The attribute without a constructor parameter requires that you recompile and redeploy the project to change the function's disabled state.</span></span> <span data-ttu-id="36339-124">A more flexible way to use the attribute is to include a constructor parameter that refers to a Boolean app setting, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="36339-124">A more flexible way to use the attribute is to include a constructor parameter that refers to a Boolean app setting, as shown in the following example:</span></span>

```csharp
public static class QueueFunctions
{
    [Disable("MY_TIMER_DISABLED")]
    [FunctionName("QueueTrigger")]
    public static void QueueTrigger(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}
```

<span data-ttu-id="36339-125">This method lets you enable and disable the function by changing the app setting, without recompiling or redeploying.</span><span class="sxs-lookup"><span data-stu-id="36339-125">This method lets you enable and disable the function by changing the app setting, without recompiling or redeploying.</span></span> <span data-ttu-id="36339-126">Changing an app setting causes the function app to restart, so the disabled state change is recognized immediately.</span><span class="sxs-lookup"><span data-stu-id="36339-126">Changing an app setting causes the function app to restart, so the disabled state change is recognized immediately.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36339-127">The `Disabled` attribute is the only way to disable a class library function.</span><span class="sxs-lookup"><span data-stu-id="36339-127">The `Disabled` attribute is the only way to disable a class library function.</span></span> <span data-ttu-id="36339-128">The generated *function.json* file for a class library function is not meant to be edited directly.</span><span class="sxs-lookup"><span data-stu-id="36339-128">The generated *function.json* file for a class library function is not meant to be edited directly.</span></span> <span data-ttu-id="36339-129">If you edit that file, whatever you do to the `disabled` property will have no effect.</span><span class="sxs-lookup"><span data-stu-id="36339-129">If you edit that file, whatever you do to the `disabled` property will have no effect.</span></span>
>
> <span data-ttu-id="36339-130">The same goes for the **Function state** switch on the **Manage** tab, since it works by changing the *function.json* file.</span><span class="sxs-lookup"><span data-stu-id="36339-130">The same goes for the **Function state** switch on the **Manage** tab, since it works by changing the *function.json* file.</span></span>
>
> <span data-ttu-id="36339-131">Also, note that the portal may indicate the function is disabled when it isn't.</span><span class="sxs-lookup"><span data-stu-id="36339-131">Also, note that the portal may indicate the function is disabled when it isn't.</span></span>



## <a name="functions-2x---all-languages"></a><span data-ttu-id="36339-132">Functions 2.x - all languages</span><span class="sxs-lookup"><span data-stu-id="36339-132">Functions 2.x - all languages</span></span>

<span data-ttu-id="36339-133">In Functions 2.x you disable a function by using an app setting.</span><span class="sxs-lookup"><span data-stu-id="36339-133">In Functions 2.x you disable a function by using an app setting.</span></span> <span data-ttu-id="36339-134">For example, to disable a function named `QueueTrigger`, you create an app setting named `AzureWebJobs.QueueTrigger.Disabled`, and set it to `true`.</span><span class="sxs-lookup"><span data-stu-id="36339-134">For example, to disable a function named `QueueTrigger`, you create an app setting named `AzureWebJobs.QueueTrigger.Disabled`, and set it to `true`.</span></span> <span data-ttu-id="36339-135">To enable the function, set the app setting to `false`.</span><span class="sxs-lookup"><span data-stu-id="36339-135">To enable the function, set the app setting to `false`.</span></span> <span data-ttu-id="36339-136">You can also use the **Function State** switch on the function's **Manage** tab. The switch works by creating and deleting the `AzureWebJobs.<functionname>.Disabled` app setting.</span><span class="sxs-lookup"><span data-stu-id="36339-136">You can also use the **Function State** switch on the function's **Manage** tab. The switch works by creating and deleting the `AzureWebJobs.<functionname>.Disabled` app setting.</span></span>

![Function state switch](media/disable-function/function-state-switch.png)

## <a name="functions-2x---c-class-libraries"></a><span data-ttu-id="36339-138">Functions 2.x - C# class libraries</span><span class="sxs-lookup"><span data-stu-id="36339-138">Functions 2.x - C# class libraries</span></span>

<span data-ttu-id="36339-139">In a Functions 2.x class library, we recommend that you use the method that works for all languages.</span><span class="sxs-lookup"><span data-stu-id="36339-139">In a Functions 2.x class library, we recommend that you use the method that works for all languages.</span></span> <span data-ttu-id="36339-140">But if you prefer, you can [use the Disable attribute as in Functions 1.x](#functions-1x---c-class-libraries).</span><span class="sxs-lookup"><span data-stu-id="36339-140">But if you prefer, you can [use the Disable attribute as in Functions 1.x](#functions-1x---c-class-libraries).</span></span>

## <a name="next-steps"></a><span data-ttu-id="36339-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="36339-141">Next steps</span></span>

<span data-ttu-id="36339-142">This article is about disabling automatic triggers.</span><span class="sxs-lookup"><span data-stu-id="36339-142">This article is about disabling automatic triggers.</span></span> <span data-ttu-id="36339-143">For more information about triggers, see [Triggers and bindings](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="36339-143">For more information about triggers, see [Triggers and bindings](functions-triggers-bindings.md).</span></span>
