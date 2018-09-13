---
title: Monitoring Azure Functions | Microsoft Docs
description: Learn how to monitor your Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: e4cb740b9187f4de4ee8b523e23a63064a4ec87c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555510"
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="a582c-104">Monitoring Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a582c-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="a582c-105">Overview</span><span class="sxs-lookup"><span data-stu-id="a582c-105">Overview</span></span> 


<span data-ttu-id="a582c-106">The **Monitor** tab for each function allows you to review each execution of a function.</span><span class="sxs-lookup"><span data-stu-id="a582c-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Azure Functions monitor tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="a582c-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span><span class="sxs-lookup"><span data-stu-id="a582c-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="a582c-109">This is useful debugging and performance tuning your functions.</span><span class="sxs-lookup"><span data-stu-id="a582c-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="a582c-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span><span class="sxs-lookup"><span data-stu-id="a582c-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="a582c-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span><span class="sxs-lookup"><span data-stu-id="a582c-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="a582c-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span><span class="sxs-lookup"><span data-stu-id="a582c-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="a582c-113">The following screen-shot shows an example:</span><span class="sxs-lookup"><span data-stu-id="a582c-113">The following screen-shot shows an example:</span></span>
> 
> ![Monitoring on the main resource blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="a582c-115">Real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="a582c-115">Real-time monitoring</span></span>

<span data-ttu-id="a582c-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span><span class="sxs-lookup"><span data-stu-id="a582c-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Live event stream option for the monitor tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="a582c-118">The live event stream will be graphed in a new browser tab as shown below.</span><span class="sxs-lookup"><span data-stu-id="a582c-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Live event stream example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="a582c-120">There is a known issue that may cause your data to fail to be populated.</span><span class="sxs-lookup"><span data-stu-id="a582c-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="a582c-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span><span class="sxs-lookup"><span data-stu-id="a582c-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="a582c-122">The live event stream will graph the following statistics for your function:</span><span class="sxs-lookup"><span data-stu-id="a582c-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="a582c-123">Executions started per second</span><span class="sxs-lookup"><span data-stu-id="a582c-123">Executions started per second</span></span>
* <span data-ttu-id="a582c-124">Executions completed per second</span><span class="sxs-lookup"><span data-stu-id="a582c-124">Executions completed per second</span></span>
* <span data-ttu-id="a582c-125">Executions failed per second</span><span class="sxs-lookup"><span data-stu-id="a582c-125">Executions failed per second</span></span>
* <span data-ttu-id="a582c-126">Average execution time in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="a582c-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="a582c-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span><span class="sxs-lookup"><span data-stu-id="a582c-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="a582c-128">Monitoring log files from a command line</span><span class="sxs-lookup"><span data-stu-id="a582c-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="a582c-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a582c-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="a582c-130">Monitoring function app log files with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a582c-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="a582c-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="a582c-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="a582c-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a582c-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="a582c-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span><span class="sxs-lookup"><span data-stu-id="a582c-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="a582c-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span><span class="sxs-lookup"><span data-stu-id="a582c-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="a582c-135">The following command will stream the log files of your function app to the command line:</span><span class="sxs-lookup"><span data-stu-id="a582c-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="a582c-136">Monitoring function app log files with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a582c-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="a582c-137">To get started, [install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a582c-137">To get started, [install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="a582c-138">Add your Azure account by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a582c-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="a582c-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span><span class="sxs-lookup"><span data-stu-id="a582c-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="a582c-140">If you need to set the active subscription to the one containing your function app, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a582c-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="a582c-141">Stream the logs to your PowerShell session with the following command:</span><span class="sxs-lookup"><span data-stu-id="a582c-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="a582c-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="a582c-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a582c-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="a582c-143">Next steps</span></span>
<span data-ttu-id="a582c-144">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="a582c-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="a582c-145">Testing a function</span><span class="sxs-lookup"><span data-stu-id="a582c-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="a582c-146">Scale a function</span><span class="sxs-lookup"><span data-stu-id="a582c-146">Scale a function</span></span>](functions-scale.md)





