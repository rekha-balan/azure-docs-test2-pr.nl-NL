---
title: Understanding Stream Analytics Job Monitoring | Microsoft Docs
description: Understanding Stream Analytics Job Monitoring
keywords: query monitor
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e6bfb57671cd513a0a33c6cd0c60f8de9c98cf21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553022"
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="be329-104">Understand Stream Analytics job monitoring and how to monitor queries</span><span class="sxs-lookup"><span data-stu-id="be329-104">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="be329-105">Introduction: The monitor page</span><span class="sxs-lookup"><span data-stu-id="be329-105">Introduction: The monitor page</span></span>
<span data-ttu-id="be329-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span><span class="sxs-lookup"><span data-stu-id="be329-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="be329-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span><span class="sxs-lookup"><span data-stu-id="be329-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![Monitoring link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="be329-109">The window will appear as shown:</span><span class="sxs-lookup"><span data-stu-id="be329-109">The window will appear as shown:</span></span>

![Monitoring job Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="be329-111">Metrics available for Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="be329-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="be329-112">Metric</span><span class="sxs-lookup"><span data-stu-id="be329-112">Metric</span></span>                 | <span data-ttu-id="be329-113">Definition</span><span class="sxs-lookup"><span data-stu-id="be329-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="be329-114">SU % Utilization</span><span class="sxs-lookup"><span data-stu-id="be329-114">SU % Utilization</span></span>       | <span data-ttu-id="be329-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span><span class="sxs-lookup"><span data-stu-id="be329-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="be329-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span><span class="sxs-lookup"><span data-stu-id="be329-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="be329-117">Input Events</span><span class="sxs-lookup"><span data-stu-id="be329-117">Input Events</span></span>           | <span data-ttu-id="be329-118">Amount of data received by the Stream Analytics job, in number of events.</span><span class="sxs-lookup"><span data-stu-id="be329-118">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="be329-119">This can be used to validate that events are being sent to the input source.</span><span class="sxs-lookup"><span data-stu-id="be329-119">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="be329-120">Output Events</span><span class="sxs-lookup"><span data-stu-id="be329-120">Output Events</span></span>          | <span data-ttu-id="be329-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span><span class="sxs-lookup"><span data-stu-id="be329-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="be329-122">Out-of-Order Events</span><span class="sxs-lookup"><span data-stu-id="be329-122">Out-of-Order Events</span></span>    | <span data-ttu-id="be329-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span><span class="sxs-lookup"><span data-stu-id="be329-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="be329-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span><span class="sxs-lookup"><span data-stu-id="be329-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="be329-125">Data Conversion Errors</span><span class="sxs-lookup"><span data-stu-id="be329-125">Data Conversion Errors</span></span> | <span data-ttu-id="be329-126">Number of data conversion errors incurred by a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="be329-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="be329-127">Runtime Errors</span><span class="sxs-lookup"><span data-stu-id="be329-127">Runtime Errors</span></span>         | <span data-ttu-id="be329-128">The total number of errors that happen during execution of a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="be329-128">The total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="be329-129">Late Input Events</span><span class="sxs-lookup"><span data-stu-id="be329-129">Late Input Events</span></span>      | <span data-ttu-id="be329-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span><span class="sxs-lookup"><span data-stu-id="be329-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="be329-131">Function Requests</span><span class="sxs-lookup"><span data-stu-id="be329-131">Function Requests</span></span>      | <span data-ttu-id="be329-132">Number of calls to the Azure Machine Learning function (if present).</span><span class="sxs-lookup"><span data-stu-id="be329-132">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="be329-133">Failed Function Requests</span><span class="sxs-lookup"><span data-stu-id="be329-133">Failed Function Requests</span></span> | <span data-ttu-id="be329-134">Number of failed Azure Machine Learning function calls (if present).</span><span class="sxs-lookup"><span data-stu-id="be329-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="be329-135">Function Events</span><span class="sxs-lookup"><span data-stu-id="be329-135">Function Events</span></span>        | <span data-ttu-id="be329-136">Number of events sent to the Azure Machine Learning function (if present).</span><span class="sxs-lookup"><span data-stu-id="be329-136">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="be329-137">Input Event Bytes</span><span class="sxs-lookup"><span data-stu-id="be329-137">Input Event Bytes</span></span>      | <span data-ttu-id="be329-138">Amount of data received by the Stream Analytics job, in bytes.</span><span class="sxs-lookup"><span data-stu-id="be329-138">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="be329-139">This can be used to validate that events are being sent to the input source.</span><span class="sxs-lookup"><span data-stu-id="be329-139">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="be329-140">Customizing Monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="be329-140">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="be329-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span><span class="sxs-lookup"><span data-stu-id="be329-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="be329-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="be329-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Query Monitor Time graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="be329-144">Get help</span><span class="sxs-lookup"><span data-stu-id="be329-144">Get help</span></span>
<span data-ttu-id="be329-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="be329-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="be329-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="be329-146">Next steps</span></span>
* [<span data-ttu-id="be329-147">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="be329-147">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="be329-148">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="be329-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="be329-149">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="be329-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="be329-150">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="be329-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="be329-151">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="be329-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)




