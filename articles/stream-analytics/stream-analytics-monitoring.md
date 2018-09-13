---
title: Understand job monitoring in Azure Stream Analytics
description: This article describes how to monitor jobs in Azure Stream Analytics
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 03/28/2017
ms.openlocfilehash: 4b048705c80b7776ab0ab6823e27659a01eedeb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44788884"
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="bb833-103">Understand Stream Analytics job monitoring and how to monitor queries</span><span class="sxs-lookup"><span data-stu-id="bb833-103">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="bb833-104">Introduction: The monitor page</span><span class="sxs-lookup"><span data-stu-id="bb833-104">Introduction: The monitor page</span></span>
<span data-ttu-id="bb833-105">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span><span class="sxs-lookup"><span data-stu-id="bb833-105">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="bb833-106">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span><span class="sxs-lookup"><span data-stu-id="bb833-106">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![Monitoring link](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="bb833-108">The window will appear as shown:</span><span class="sxs-lookup"><span data-stu-id="bb833-108">The window will appear as shown:</span></span>

![Monitoring job Dashboard](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="bb833-110">Metrics available for Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb833-110">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="bb833-111">Metric</span><span class="sxs-lookup"><span data-stu-id="bb833-111">Metric</span></span>                 | <span data-ttu-id="bb833-112">Definition</span><span class="sxs-lookup"><span data-stu-id="bb833-112">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="bb833-113">SU % Utilization</span><span class="sxs-lookup"><span data-stu-id="bb833-113">SU % Utilization</span></span>       | <span data-ttu-id="bb833-114">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span><span class="sxs-lookup"><span data-stu-id="bb833-114">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="bb833-115">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span><span class="sxs-lookup"><span data-stu-id="bb833-115">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="bb833-116">Input Events</span><span class="sxs-lookup"><span data-stu-id="bb833-116">Input Events</span></span>           | <span data-ttu-id="bb833-117">Amount of data received by the Stream Analytics job, in number of events.</span><span class="sxs-lookup"><span data-stu-id="bb833-117">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="bb833-118">This can be used to validate that events are being sent to the input source.</span><span class="sxs-lookup"><span data-stu-id="bb833-118">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="bb833-119">Output Events</span><span class="sxs-lookup"><span data-stu-id="bb833-119">Output Events</span></span>          | <span data-ttu-id="bb833-120">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span><span class="sxs-lookup"><span data-stu-id="bb833-120">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="bb833-121">Out-of-Order Events</span><span class="sxs-lookup"><span data-stu-id="bb833-121">Out-of-Order Events</span></span>    | <span data-ttu-id="bb833-122">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span><span class="sxs-lookup"><span data-stu-id="bb833-122">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="bb833-123">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span><span class="sxs-lookup"><span data-stu-id="bb833-123">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="bb833-124">Data Conversion Errors</span><span class="sxs-lookup"><span data-stu-id="bb833-124">Data Conversion Errors</span></span> | <span data-ttu-id="bb833-125">Number of data conversion errors incurred by a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="bb833-125">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="bb833-126">Runtime Errors</span><span class="sxs-lookup"><span data-stu-id="bb833-126">Runtime Errors</span></span>         | <span data-ttu-id="bb833-127">Total number of errors related to query processing (excluding errors found while ingesting events or outputing results)</span><span class="sxs-lookup"><span data-stu-id="bb833-127">Total number of errors related to query processing (excluding errors found while ingesting events or outputing results)</span></span> |
| <span data-ttu-id="bb833-128">Late Input Events</span><span class="sxs-lookup"><span data-stu-id="bb833-128">Late Input Events</span></span>      | <span data-ttu-id="bb833-129">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span><span class="sxs-lookup"><span data-stu-id="bb833-129">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="bb833-130">Function Requests</span><span class="sxs-lookup"><span data-stu-id="bb833-130">Function Requests</span></span>      | <span data-ttu-id="bb833-131">Number of calls to the Azure Machine Learning function (if present).</span><span class="sxs-lookup"><span data-stu-id="bb833-131">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="bb833-132">Failed Function Requests</span><span class="sxs-lookup"><span data-stu-id="bb833-132">Failed Function Requests</span></span> | <span data-ttu-id="bb833-133">Number of failed Azure Machine Learning function calls (if present).</span><span class="sxs-lookup"><span data-stu-id="bb833-133">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="bb833-134">Function Events</span><span class="sxs-lookup"><span data-stu-id="bb833-134">Function Events</span></span>        | <span data-ttu-id="bb833-135">Number of events sent to the Azure Machine Learning function (if present).</span><span class="sxs-lookup"><span data-stu-id="bb833-135">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="bb833-136">Input Event Bytes</span><span class="sxs-lookup"><span data-stu-id="bb833-136">Input Event Bytes</span></span>      | <span data-ttu-id="bb833-137">Amount of data received by the Stream Analytics job, in bytes.</span><span class="sxs-lookup"><span data-stu-id="bb833-137">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="bb833-138">This can be used to validate that events are being sent to the input source.</span><span class="sxs-lookup"><span data-stu-id="bb833-138">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="bb833-139">Customizing Monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb833-139">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="bb833-140">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span><span class="sxs-lookup"><span data-stu-id="bb833-140">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="bb833-141">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="bb833-141">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Query Monitor Time graph](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="latest-output"></a><span data-ttu-id="bb833-143">Latest output</span><span class="sxs-lookup"><span data-stu-id="bb833-143">Latest output</span></span>
<span data-ttu-id="bb833-144">Another interesting data point to monitor your job is the time of the last output, shown in the Overview page.</span><span class="sxs-lookup"><span data-stu-id="bb833-144">Another interesting data point to monitor your job is the time of the last output, shown in the Overview page.</span></span>
<span data-ttu-id="bb833-145">This time is the application time (i.e. the time using the timestamp from the event data) of the latest output of your job.</span><span class="sxs-lookup"><span data-stu-id="bb833-145">This time is the application time (i.e. the time using the timestamp from the event data) of the latest output of your job.</span></span>

## <a name="get-help"></a><span data-ttu-id="bb833-146">Get help</span><span class="sxs-lookup"><span data-stu-id="bb833-146">Get help</span></span>
<span data-ttu-id="bb833-147">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="bb833-147">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb833-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb833-148">Next steps</span></span>
* [<span data-ttu-id="bb833-149">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb833-149">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bb833-150">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bb833-150">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bb833-151">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="bb833-151">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bb833-152">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="bb833-152">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bb833-153">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="bb833-153">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

