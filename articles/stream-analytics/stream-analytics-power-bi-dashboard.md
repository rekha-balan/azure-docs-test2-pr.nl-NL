---
title: Power BI dashboard on Azure Stream Analytics | Microsoft Docs
description: Use a real-time streaming Power BI dashboard to gather business intelligence and analyze high-volume data from a Stream Analytics job.
keywords: analytics dashboard, real-time dashboard
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b6c256d21cc0a65363d65f922f407095209af3e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549247"
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="05c53-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span><span class="sxs-lookup"><span data-stu-id="05c53-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="05c53-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="05c53-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, Microsoft Power BI.</span></span> <span data-ttu-id="05c53-106">Learn how to use Azure Stream Analytics to analyze high-volume, streaming data and get insight from a real-time Power BI analytics dashboard.</span><span class="sxs-lookup"><span data-stu-id="05c53-106">Learn how to use Azure Stream Analytics to analyze high-volume, streaming data and get insight from a real-time Power BI analytics dashboard.</span></span>

<span data-ttu-id="05c53-107">Use [Microsoft Power BI](https://powerbi.com/) to build a live dashboard quickly.</span><span class="sxs-lookup"><span data-stu-id="05c53-107">Use [Microsoft Power BI](https://powerbi.com/) to build a live dashboard quickly.</span></span> <span data-ttu-id="05c53-108">[Watch a video that illustrates this scenario](https://www.youtube.com/watch?v=SGUpT-a99MA).</span><span class="sxs-lookup"><span data-stu-id="05c53-108">[Watch a video that illustrates this scenario](https://www.youtube.com/watch?v=SGUpT-a99MA).</span></span>

<span data-ttu-id="05c53-109">In this article, you learn how create your own custom business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="05c53-109">In this article, you learn how create your own custom business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="05c53-110">You also learn how to utilize a real-time dashboard.</span><span class="sxs-lookup"><span data-stu-id="05c53-110">You also learn how to utilize a real-time dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05c53-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05c53-111">Prerequisites</span></span>
* <span data-ttu-id="05c53-112">Microsoft Azure Account.</span><span class="sxs-lookup"><span data-stu-id="05c53-112">Microsoft Azure Account.</span></span>
* <span data-ttu-id="05c53-113">Work or school account for Power BI.</span><span class="sxs-lookup"><span data-stu-id="05c53-113">Work or school account for Power BI.</span></span>
* <span data-ttu-id="05c53-114">Completion of the [Real-time fraud detection](stream-analytics-real-time-fraud-detection.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="05c53-114">Completion of the [Real-time fraud detection](stream-analytics-real-time-fraud-detection.md) scenario.</span></span> <span data-ttu-id="05c53-115">The article you're reading now builds on the workflow that's described in [Real-time fraud detection](stream-analytics-real-time-fraud-detection.md) and adds a Power BI streaming dataset output.</span><span class="sxs-lookup"><span data-stu-id="05c53-115">The article you're reading now builds on the workflow that's described in [Real-time fraud detection](stream-analytics-real-time-fraud-detection.md) and adds a Power BI streaming dataset output.</span></span>

## <a name="add-power-bi-output"></a><span data-ttu-id="05c53-116">Add Power BI output</span><span class="sxs-lookup"><span data-stu-id="05c53-116">Add Power BI output</span></span>
<span data-ttu-id="05c53-117">Now that an input exists for the job, an output to Power BI can be defined.</span><span class="sxs-lookup"><span data-stu-id="05c53-117">Now that an input exists for the job, an output to Power BI can be defined.</span></span>

1. <span data-ttu-id="05c53-118">Select the **Outputs** box in the middle of the job dashboard.</span><span class="sxs-lookup"><span data-stu-id="05c53-118">Select the **Outputs** box in the middle of the job dashboard.</span></span> <span data-ttu-id="05c53-119">Then select **+ Add** to create your output.</span><span class="sxs-lookup"><span data-stu-id="05c53-119">Then select **+ Add** to create your output.</span></span>

    ![Add output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/create-pbi-output.png)

2. <span data-ttu-id="05c53-121">Provide the **Output Alias**.</span><span class="sxs-lookup"><span data-stu-id="05c53-121">Provide the **Output Alias**.</span></span> <span data-ttu-id="05c53-122">You can use any output alias that is easy for you to refer to.</span><span class="sxs-lookup"><span data-stu-id="05c53-122">You can use any output alias that is easy for you to refer to.</span></span> <span data-ttu-id="05c53-123">This output alias is helpful if you decide to have multiple outputs for your job.</span><span class="sxs-lookup"><span data-stu-id="05c53-123">This output alias is helpful if you decide to have multiple outputs for your job.</span></span> <span data-ttu-id="05c53-124">In this case, you refer to this output in your query.</span><span class="sxs-lookup"><span data-stu-id="05c53-124">In this case, you refer to this output in your query.</span></span> <span data-ttu-id="05c53-125">For example, let’s use the output alias value "StreamAnalyticsRealTimeFraudPBI."</span><span class="sxs-lookup"><span data-stu-id="05c53-125">For example, let’s use the output alias value "StreamAnalyticsRealTimeFraudPBI."</span></span>

3. <span data-ttu-id="05c53-126">Select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="05c53-126">Select **Authorize**.</span></span>

    ![Add authorization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/pbi-authorize.png)

4. <span data-ttu-id="05c53-128">A window opens where you can provide your Azure credentials (for a work or school account).</span><span class="sxs-lookup"><span data-stu-id="05c53-128">A window opens where you can provide your Azure credentials (for a work or school account).</span></span> <span data-ttu-id="05c53-129">It also provides your Azure job with access to your Power BI area.</span><span class="sxs-lookup"><span data-stu-id="05c53-129">It also provides your Azure job with access to your Power BI area.</span></span>

    ![Authorize fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/authorize-area.png)

5. <span data-ttu-id="05c53-131">The authorization disappears after you've provided the necessary information.</span><span class="sxs-lookup"><span data-stu-id="05c53-131">The authorization disappears after you've provided the necessary information.</span></span> <span data-ttu-id="05c53-132">The **New output** area has fields for the **Dataset Name** and **Table Name**.</span><span class="sxs-lookup"><span data-stu-id="05c53-132">The **New output** area has fields for the **Dataset Name** and **Table Name**.</span></span>

    ![PBI workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/pbi-workspace.png)

6. <span data-ttu-id="05c53-134">Define them as follows:</span><span class="sxs-lookup"><span data-stu-id="05c53-134">Define them as follows:</span></span>
    * <span data-ttu-id="05c53-135">**Group Workspace**: Select a workspace in your Power BI tenant under which to create the dataset.</span><span class="sxs-lookup"><span data-stu-id="05c53-135">**Group Workspace**: Select a workspace in your Power BI tenant under which to create the dataset.</span></span>
    * <span data-ttu-id="05c53-136">**Dataset Name**:  Provide a dataset name that you want your Power BI output to have.</span><span class="sxs-lookup"><span data-stu-id="05c53-136">**Dataset Name**:  Provide a dataset name that you want your Power BI output to have.</span></span> <span data-ttu-id="05c53-137">For example, let’s use "StreamAnalyticsRealTimeFraudPBI."</span><span class="sxs-lookup"><span data-stu-id="05c53-137">For example, let’s use "StreamAnalyticsRealTimeFraudPBI."</span></span>
    * <span data-ttu-id="05c53-138">**Table Name**: Provide a table name under the dataset of your Power BI output.</span><span class="sxs-lookup"><span data-stu-id="05c53-138">**Table Name**: Provide a table name under the dataset of your Power BI output.</span></span> <span data-ttu-id="05c53-139">For example, let's use "StreamAnalyticsRealTimeFraudPBI."</span><span class="sxs-lookup"><span data-stu-id="05c53-139">For example, let's use "StreamAnalyticsRealTimeFraudPBI."</span></span> <span data-ttu-id="05c53-140">Currently, Power BI output from Stream Analytics jobs can only have one table in a dataset.</span><span class="sxs-lookup"><span data-stu-id="05c53-140">Currently, Power BI output from Stream Analytics jobs can only have one table in a dataset.</span></span>

7. <span data-ttu-id="05c53-141">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="05c53-141">Select **Create**.</span></span> <span data-ttu-id="05c53-142">Now your output configuration is complete.</span><span class="sxs-lookup"><span data-stu-id="05c53-142">Now your output configuration is complete.</span></span>

> [!WARNING]
> <span data-ttu-id="05c53-143">If Power BI already has a dataset and table that has the same name as the one in this Stream Analytics job, the existing data is overwritten.</span><span class="sxs-lookup"><span data-stu-id="05c53-143">If Power BI already has a dataset and table that has the same name as the one in this Stream Analytics job, the existing data is overwritten.</span></span>
> <span data-ttu-id="05c53-144">Also, we recommend that you do not explicitly create this dataset and table in your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="05c53-144">Also, we recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="05c53-145">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span><span class="sxs-lookup"><span data-stu-id="05c53-145">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="05c53-146">If your job query doesn’t return any results, the dataset and table isn't created.</span><span class="sxs-lookup"><span data-stu-id="05c53-146">If your job query doesn’t return any results, the dataset and table isn't created.</span></span>
>
>

<span data-ttu-id="05c53-147">The dataset is created with the following settings:</span><span class="sxs-lookup"><span data-stu-id="05c53-147">The dataset is created with the following settings:</span></span>
* <span data-ttu-id="05c53-148">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span><span class="sxs-lookup"><span data-stu-id="05c53-148">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="05c53-149">**defaultMode: pushStreaming**: Supports both streaming tiles and traditional report-based visuals (aka push).</span><span class="sxs-lookup"><span data-stu-id="05c53-149">**defaultMode: pushStreaming**: Supports both streaming tiles and traditional report-based visuals (aka push).</span></span>

<span data-ttu-id="05c53-150">Currently, you can't create datasets with other flags.</span><span class="sxs-lookup"><span data-stu-id="05c53-150">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="05c53-151">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span><span class="sxs-lookup"><span data-stu-id="05c53-151">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-query"></a><span data-ttu-id="05c53-152">Write query</span><span class="sxs-lookup"><span data-stu-id="05c53-152">Write query</span></span>
<span data-ttu-id="05c53-153">Go to the **Query** tab of your job.</span><span class="sxs-lookup"><span data-stu-id="05c53-153">Go to the **Query** tab of your job.</span></span> <span data-ttu-id="05c53-154">Write your query, the output of which you want in Power BI.</span><span class="sxs-lookup"><span data-stu-id="05c53-154">Write your query, the output of which you want in Power BI.</span></span> <span data-ttu-id="05c53-155">For example, it could be similar to the following SQL query to catch SIM fraud in the telecommunications industry:</span><span class="sxs-lookup"><span data-stu-id="05c53-155">For example, it could be similar to the following SQL query to catch SIM fraud in the telecommunications industry:</span></span>


```
/* Our criteria for fraud:
 Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

 SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
 INTO "StreamAnalyticsRealTimeFraudPBI"
 FROM "StreamAnalyticsRealTimeFraudInput" CS1 TIMESTAMP BY CallRecTime
 JOIN "StreamAnalyticsRealTimeFraudInput" CS2 TIMESTAMP BY CallRecTime

/* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
 ON CS1.CallingIMSI = CS2.CallingIMSI

/* ...and date between CS1 and CS2 is between one and five seconds */
 AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

/* Where the switch location is different */
 WHERE CS1.SwitchNum != CS2.SwitchNum
 GROUP BY TumblingWindow(Duration(second, 1))
```

## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="05c53-156">Create the dashboard in Power BI</span><span class="sxs-lookup"><span data-stu-id="05c53-156">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="05c53-157">Go to [Powerbi.com](https://powerbi.com), and then sign in with your work or school account.</span><span class="sxs-lookup"><span data-stu-id="05c53-157">Go to [Powerbi.com](https://powerbi.com), and then sign in with your work or school account.</span></span> <span data-ttu-id="05c53-158">If the Stream Analytics job query outputs results, you see that your dataset is already created, as shown in the following illustration:</span><span class="sxs-lookup"><span data-stu-id="05c53-158">If the Stream Analytics job query outputs results, you see that your dataset is already created, as shown in the following illustration:</span></span>

    ![Streaming dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="05c53-160">Select **Add tile**, and then select your custom streaming data.</span><span class="sxs-lookup"><span data-stu-id="05c53-160">Select **Add tile**, and then select your custom streaming data.</span></span>

    ![Custom streaming dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

3. <span data-ttu-id="05c53-162">Select your dataset from the list.</span><span class="sxs-lookup"><span data-stu-id="05c53-162">Select your dataset from the list.</span></span>

    ![Your streaming dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

4. <span data-ttu-id="05c53-164">Create a visualization card.</span><span class="sxs-lookup"><span data-stu-id="05c53-164">Create a visualization card.</span></span> <span data-ttu-id="05c53-165">Then select the **fraudulentcalls** field.</span><span class="sxs-lookup"><span data-stu-id="05c53-165">Then select the **fraudulentcalls** field.</span></span>

    ![Add fraud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/add-fraud.png)

    <span data-ttu-id="05c53-167">Now we have a fraud counter!</span><span class="sxs-lookup"><span data-stu-id="05c53-167">Now we have a fraud counter!</span></span>

    ![Fraud counter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/fraud-counter.png)

5. <span data-ttu-id="05c53-169">Walk through the exercise of adding a tile again.</span><span class="sxs-lookup"><span data-stu-id="05c53-169">Walk through the exercise of adding a tile again.</span></span> <span data-ttu-id="05c53-170">This time, however, select the line chart.</span><span class="sxs-lookup"><span data-stu-id="05c53-170">This time, however, select the line chart.</span></span> <span data-ttu-id="05c53-171">Add **fraudulentcalls** as the value and **windowend** as the axis.</span><span class="sxs-lookup"><span data-stu-id="05c53-171">Add **fraudulentcalls** as the value and **windowend** as the axis.</span></span> <span data-ttu-id="05c53-172">We selected the last 10 minutes, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="05c53-172">We selected the last 10 minutes, as shown in the following screenshot:</span></span>

![Fraud calls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/fraud-calls.png)


<span data-ttu-id="05c53-174">This tutorial demonstrates how to create only one kind of chart for a dataset.</span><span class="sxs-lookup"><span data-stu-id="05c53-174">This tutorial demonstrates how to create only one kind of chart for a dataset.</span></span> <span data-ttu-id="05c53-175">Power BI can help you create other customer business intelligence tools for your organization.</span><span class="sxs-lookup"><span data-stu-id="05c53-175">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="05c53-176">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span><span class="sxs-lookup"><span data-stu-id="05c53-176">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>

<span data-ttu-id="05c53-177">For more information about configuring a Power BI output and utilizing Power BI groups, review the [Power BI section](stream-analytics-define-outputs.md#power-bi) of [Understanding Stream Analytics outputs](stream-analytics-define-outputs.md "Understanding Stream Analytics outputs").</span><span class="sxs-lookup"><span data-stu-id="05c53-177">For more information about configuring a Power BI output and utilizing Power BI groups, review the [Power BI section](stream-analytics-define-outputs.md#power-bi) of [Understanding Stream Analytics outputs](stream-analytics-define-outputs.md "Understanding Stream Analytics outputs").</span></span> <span data-ttu-id="05c53-178">[Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/) is another helpful resource.</span><span class="sxs-lookup"><span data-stu-id="05c53-178">[Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/) is another helpful resource.</span></span>

## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="05c53-179">Learn about limitations and best practices</span><span class="sxs-lookup"><span data-stu-id="05c53-179">Learn about limitations and best practices</span></span>
<span data-ttu-id="05c53-180">Power BI employs both concurrency and throughput constraints as described [on this page about Power BI](https://powerbi.microsoft.com/pricing "Power BI Pricing").</span><span class="sxs-lookup"><span data-stu-id="05c53-180">Power BI employs both concurrency and throughput constraints as described [on this page about Power BI](https://powerbi.microsoft.com/pricing "Power BI Pricing").</span></span>

<span data-ttu-id="05c53-181">Currently, Power BI can be called roughly once per second.</span><span class="sxs-lookup"><span data-stu-id="05c53-181">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="05c53-182">Streaming visuals support packets of 15 KB.</span><span class="sxs-lookup"><span data-stu-id="05c53-182">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="05c53-183">Beyond that, streaming visuals fail (but push continues to work).</span><span class="sxs-lookup"><span data-stu-id="05c53-183">Beyond that, streaming visuals fail (but push continues to work).</span></span>

<span data-ttu-id="05c53-184">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span><span class="sxs-lookup"><span data-stu-id="05c53-184">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span>
<span data-ttu-id="05c53-185">We recommend using Tumbling Window or Hopping Window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span><span class="sxs-lookup"><span data-stu-id="05c53-185">We recommend using Tumbling Window or Hopping Window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="05c53-186">You can use the following equation to compute the value to give your window in seconds:</span><span class="sxs-lookup"><span data-stu-id="05c53-186">You can use the following equation to compute the value to give your window in seconds:</span></span>

![Equation1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="05c53-188">For example:</span><span class="sxs-lookup"><span data-stu-id="05c53-188">For example:</span></span>
- <span data-ttu-id="05c53-189">You have 1,000 devices sending data at one-second intervals.</span><span class="sxs-lookup"><span data-stu-id="05c53-189">You have 1,000 devices sending data at one-second intervals.</span></span>
- <span data-ttu-id="05c53-190">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span><span class="sxs-lookup"><span data-stu-id="05c53-190">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
- <span data-ttu-id="05c53-191">You want to publish the amount of average data per device to Power BI.</span><span class="sxs-lookup"><span data-stu-id="05c53-191">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="05c53-192">As a result, the equation becomes:</span><span class="sxs-lookup"><span data-stu-id="05c53-192">As a result, the equation becomes:</span></span>

![Equation2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="05c53-194">This means we can change the original query to the following:</span><span class="sxs-lookup"><span data-stu-id="05c53-194">This means we can change the original query to the following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO
        OutPBI
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="05c53-195">Renew authorization</span><span class="sxs-lookup"><span data-stu-id="05c53-195">Renew authorization</span></span>
<span data-ttu-id="05c53-196">If the password has changed since your job was created or last authenticated, you need to re-authenticate your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="05c53-196">If the password has changed since your job was created or last authenticated, you need to re-authenticate your Power BI account.</span></span> <span data-ttu-id="05c53-197">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span><span class="sxs-lookup"><span data-stu-id="05c53-197">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="05c53-198">If you don't renew, you could see symptoms such as a lack of job output or an "Authenticate user error" in the operation logs.</span><span class="sxs-lookup"><span data-stu-id="05c53-198">If you don't renew, you could see symptoms such as a lack of job output or an "Authenticate user error" in the operation logs.</span></span>

<span data-ttu-id="05c53-199">Similarly, if a job attempts to start after the token has expired, an error occurs and the job starts to fail.</span><span class="sxs-lookup"><span data-stu-id="05c53-199">Similarly, if a job attempts to start after the token has expired, an error occurs and the job starts to fail.</span></span> <span data-ttu-id="05c53-200">To resolve this issue, stop the job that's running and go to your Power BI output.</span><span class="sxs-lookup"><span data-stu-id="05c53-200">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="05c53-201">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span><span class="sxs-lookup"><span data-stu-id="05c53-201">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="05c53-202">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span><span class="sxs-lookup"><span data-stu-id="05c53-202">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="05c53-203">Get help</span><span class="sxs-lookup"><span data-stu-id="05c53-203">Get help</span></span>
<span data-ttu-id="05c53-204">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="05c53-204">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05c53-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="05c53-205">Next steps</span></span>
* [<span data-ttu-id="05c53-206">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="05c53-206">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="05c53-207">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="05c53-207">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="05c53-208">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="05c53-208">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="05c53-209">Azure Stream Analytics query language reference</span><span class="sxs-lookup"><span data-stu-id="05c53-209">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="05c53-210">Azure Stream Analytics Management REST API reference</span><span class="sxs-lookup"><span data-stu-id="05c53-210">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)












