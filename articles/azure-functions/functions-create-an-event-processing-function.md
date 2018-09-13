---
title: Create an event processing function | Microsoft Docs
description: Use Azure Functions create a C# function that runs based on an event timer.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: 84bd0373-65e2-4022-bcca-2b9cd9e696f5
ms.service: functions
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: a8a0d0864c1c57db60b1e7a418cae334ae72105e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563760"
---
# <a name="create-an-event-processing-azure-function"></a><span data-ttu-id="a335b-103">Create an event processing Azure Function</span><span class="sxs-lookup"><span data-stu-id="a335b-103">Create an event processing Azure Function</span></span>
<span data-ttu-id="a335b-104">Azure Functions is an event-driven, compute-on-demand experience that enables you to create scheduled or triggered units of code implemented in a variety of programming languages.</span><span class="sxs-lookup"><span data-stu-id="a335b-104">Azure Functions is an event-driven, compute-on-demand experience that enables you to create scheduled or triggered units of code implemented in a variety of programming languages.</span></span> <span data-ttu-id="a335b-105">To learn more about Azure Functions, see the [Azure Functions Overview](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a335b-105">To learn more about Azure Functions, see the [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="a335b-106">This topic shows you how to create a new function in C# that executes based on an event timer to add messages to a storage queue.</span><span class="sxs-lookup"><span data-stu-id="a335b-106">This topic shows you how to create a new function in C# that executes based on an event timer to add messages to a storage queue.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a335b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a335b-107">Prerequisites</span></span>
<span data-ttu-id="a335b-108">A function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="a335b-108">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="a335b-109">If you don't already have an Azure account, check out the [Try Functions](https://functions.azure.com/try) experience or  [create a free Azure acccount](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a335b-109">If you don't already have an Azure account, check out the [Try Functions](https://functions.azure.com/try) experience or  [create a free Azure acccount](https://azure.microsoft.com/free/).</span></span> 

## <a name="create-a-timer-triggered-function-from-the-template"></a><span data-ttu-id="a335b-110">Create a timer-triggered function from the template</span><span class="sxs-lookup"><span data-stu-id="a335b-110">Create a timer-triggered function from the template</span></span>
<span data-ttu-id="a335b-111">A function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="a335b-111">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="a335b-112">Before you can create a function, you need to have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="a335b-112">Before you can create a function, you need to have an active Azure account.</span></span> <span data-ttu-id="a335b-113">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a335b-113">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span> 

1. <span data-ttu-id="a335b-114">Go to the [Azure Functions portal](https://functions.azure.com/signin) and sign-in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a335b-114">Go to the [Azure Functions portal](https://functions.azure.com/signin) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="a335b-115">If you have an existing function app to use, select it from **Your function apps** then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="a335b-115">If you have an existing function app to use, select it from **Your function apps** then click **Open**.</span></span> <span data-ttu-id="a335b-116">To create a new function app, type a unique **Name** for your new function app or accept the generated one, select your preferred **Region**, then click **Create + get started**.</span><span class="sxs-lookup"><span data-stu-id="a335b-116">To create a new function app, type a unique **Name** for your new function app or accept the generated one, select your preferred **Region**, then click **Create + get started**.</span></span> 
3. <span data-ttu-id="a335b-117">In your function app, click **+ New Function** > **TimerTrigger - C#** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="a335b-117">In your function app, click **+ New Function** > **TimerTrigger - C#** > **Create**.</span></span> <span data-ttu-id="a335b-118">This creates a function with a default name that is run on the default schedule of once every minute.</span><span class="sxs-lookup"><span data-stu-id="a335b-118">This creates a function with a default name that is run on the default schedule of once every minute.</span></span> 
   
    ![Create a new timer-triggered function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-event-processing-function/functions-create-new-timer-trigger.png)
4. <span data-ttu-id="a335b-120">In your new function, click the **Integrate** tab > **New Output** > **Azure Storage Queue** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="a335b-120">In your new function, click the **Integrate** tab > **New Output** > **Azure Storage Queue** > **Select**.</span></span>
   
    ![Create a new timer-triggered function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-event-processing-function/functions-create-storage-queue-output-binding.png)
5. <span data-ttu-id="a335b-122">In  **Azure Storage Queue output**, select an existing **Storage account connection**, or create a new one, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a335b-122">In  **Azure Storage Queue output**, select an existing **Storage account connection**, or create a new one, then click **Save**.</span></span> 
   
    ![Create a new timer-triggered function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-event-processing-function/functions-create-storage-queue-output-binding-2.png)
6. <span data-ttu-id="a335b-124">Back in the **Develop** tab, replace the existing C# script in the **Code** window with the following code:</span><span class="sxs-lookup"><span data-stu-id="a335b-124">Back in the **Develop** tab, replace the existing C# script in the **Code** window with the following code:</span></span>
    ```cs   
    using System;

    public static void Run(TimerInfo myTimer, out string outputQueueItem, TraceWriter log)
    {
        // Add a new scheduled message to the queue.
        outputQueueItem = $"Ping message added to the queue at: {DateTime.Now}.";

        // Also write the message to the logs.
        log.Info(outputQueueItem);
    }
    ```
   
    <span data-ttu-id="a335b-125">This code adds a new message to the queue with the current date and time when the function is executed.</span><span class="sxs-lookup"><span data-stu-id="a335b-125">This code adds a new message to the queue with the current date and time when the function is executed.</span></span>
7. <span data-ttu-id="a335b-126">Click **Save** and watch the **Logs** windows for the next function execution.</span><span class="sxs-lookup"><span data-stu-id="a335b-126">Click **Save** and watch the **Logs** windows for the next function execution.</span></span>
8. <span data-ttu-id="a335b-127">(Optional) Navigate to the storage account and verify that messages are being added to the queue.</span><span class="sxs-lookup"><span data-stu-id="a335b-127">(Optional) Navigate to the storage account and verify that messages are being added to the queue.</span></span>
9. <span data-ttu-id="a335b-128">Go back to the **Integrate** tab and change the schedule field to `0 0 * * * *`.</span><span class="sxs-lookup"><span data-stu-id="a335b-128">Go back to the **Integrate** tab and change the schedule field to `0 0 * * * *`.</span></span> <span data-ttu-id="a335b-129">The function now runs once every hour.</span><span class="sxs-lookup"><span data-stu-id="a335b-129">The function now runs once every hour.</span></span> 

<span data-ttu-id="a335b-130">This is a very simplified example of both a timer trigger and a storage queue output binding.</span><span class="sxs-lookup"><span data-stu-id="a335b-130">This is a very simplified example of both a timer trigger and a storage queue output binding.</span></span> <span data-ttu-id="a335b-131">For more information, see both the [Azure Functions timer trigger](functions-bindings-timer.md) and the [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md) topics.</span><span class="sxs-lookup"><span data-stu-id="a335b-131">For more information, see both the [Azure Functions timer trigger](functions-bindings-timer.md) and the [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md) topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a335b-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="a335b-132">Next steps</span></span>
<span data-ttu-id="a335b-133">See these topics for more information about Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a335b-133">See these topics for more information about Azure Functions.</span></span>

* [<span data-ttu-id="a335b-134">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="a335b-134">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="a335b-135">Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="a335b-135">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="a335b-136">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a335b-136">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="a335b-137">Describes various tools and techniques for testing your functions.</span><span class="sxs-lookup"><span data-stu-id="a335b-137">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="a335b-138">How to scale Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a335b-138">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="a335b-139">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span><span class="sxs-lookup"><span data-stu-id="a335b-139">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span>  

[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]




