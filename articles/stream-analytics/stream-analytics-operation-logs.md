---
title: Debug using operation and service logs in Stream Analytics | Microsoft Docs
description: How-to use Stream Analytics operation logs
keywords: service logs
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3b9b1943aa084204d55e9b24fe02adc89b31435f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662043"
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="e59e7-104">Debug Stream Analytics jobs using service and operation logs</span><span class="sxs-lookup"><span data-stu-id="e59e7-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="e59e7-105">All Azure services supply operational logging messages to users to record details related to management operations.</span><span class="sxs-lookup"><span data-stu-id="e59e7-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="e59e7-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span><span class="sxs-lookup"><span data-stu-id="e59e7-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="e59e7-107">Find operation logs in the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="e59e7-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="e59e7-108">Operation Logs can be accessed in two ways:</span><span class="sxs-lookup"><span data-stu-id="e59e7-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="e59e7-109">Dashboard of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="e59e7-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="e59e7-110">Management Services in the Azure Classic portal</span><span class="sxs-lookup"><span data-stu-id="e59e7-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="e59e7-111">Dashboard of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="e59e7-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="e59e7-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span><span class="sxs-lookup"><span data-stu-id="e59e7-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Select Management Services logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="e59e7-114">Management Services</span><span class="sxs-lookup"><span data-stu-id="e59e7-114">Management Services</span></span>
<span data-ttu-id="e59e7-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span><span class="sxs-lookup"><span data-stu-id="e59e7-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="e59e7-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e59e7-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e59e7-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span><span class="sxs-lookup"><span data-stu-id="e59e7-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Select Stream Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="e59e7-119">Find audit logs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e59e7-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="e59e7-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="e59e7-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure portal Select Stream Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="e59e7-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="e59e7-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="e59e7-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span><span class="sxs-lookup"><span data-stu-id="e59e7-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Azure portal Select Stream Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="e59e7-125">Get log details</span><span class="sxs-lookup"><span data-stu-id="e59e7-125">Get log details</span></span>
<span data-ttu-id="e59e7-126">You can filter by Time Range and Status to view the logs for your job.</span><span class="sxs-lookup"><span data-stu-id="e59e7-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="e59e7-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span><span class="sxs-lookup"><span data-stu-id="e59e7-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Select Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="e59e7-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span><span class="sxs-lookup"><span data-stu-id="e59e7-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Azure portal Select Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="e59e7-131">From there, you can open the **Detail** blade by clicking on the event.</span><span class="sxs-lookup"><span data-stu-id="e59e7-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Azure portal Select Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="e59e7-133">Debug a failed job</span><span class="sxs-lookup"><span data-stu-id="e59e7-133">Debug a failed job</span></span>
<span data-ttu-id="e59e7-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span><span class="sxs-lookup"><span data-stu-id="e59e7-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="e59e7-135">This gives a result of all logs with failures.</span><span class="sxs-lookup"><span data-stu-id="e59e7-135">This gives a result of all logs with failures.</span></span> 

  ![Debugging a failed job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="e59e7-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span><span class="sxs-lookup"><span data-stu-id="e59e7-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Azure portal debug](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="e59e7-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span><span class="sxs-lookup"><span data-stu-id="e59e7-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="e59e7-140">Some error messages also provide information about how to mitigate the issue.</span><span class="sxs-lookup"><span data-stu-id="e59e7-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Operation Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="e59e7-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span><span class="sxs-lookup"><span data-stu-id="e59e7-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="e59e7-143">Get help</span><span class="sxs-lookup"><span data-stu-id="e59e7-143">Get help</span></span>
<span data-ttu-id="e59e7-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="e59e7-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e59e7-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="e59e7-145">Next steps</span></span>
* [<span data-ttu-id="e59e7-146">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e59e7-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e59e7-147">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e59e7-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="e59e7-148">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="e59e7-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e59e7-149">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="e59e7-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e59e7-150">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="e59e7-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)











