---
title: Export using Stream Analytics from Azure Application Insights | Microsoft Docs
description: Stream Analytics can continuously transform, filter and route the data you export from Application Insights.
services: application-insights
documentationcenter: ''
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: awills
ms.openlocfilehash: d3606d74317f16d5ee8910c6b21679c56b6b9f55
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550359"
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="82c76-103">Use Stream Analytics to process exported data from Application Insights</span><span class="sxs-lookup"><span data-stu-id="82c76-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="82c76-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="82c76-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="82c76-105">Stream Analytics can pull data from a variety of sources.</span><span class="sxs-lookup"><span data-stu-id="82c76-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="82c76-106">It can transform and filter the data, and then route it to a variety of sinks.</span><span class="sxs-lookup"><span data-stu-id="82c76-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="82c76-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span><span class="sxs-lookup"><span data-stu-id="82c76-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="82c76-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="82c76-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="82c76-109">The path illustrated here is just an example to illustrate how to process exported data.</span><span class="sxs-lookup"><span data-stu-id="82c76-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Block diagram for export through SA to PBI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="82c76-111">Create storage in Azure</span><span class="sxs-lookup"><span data-stu-id="82c76-111">Create storage in Azure</span></span>
<span data-ttu-id="82c76-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span><span class="sxs-lookup"><span data-stu-id="82c76-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="82c76-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82c76-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![In Azure portal, choose New, Data, Storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="82c76-115">Create a container</span><span class="sxs-lookup"><span data-stu-id="82c76-115">Create a container</span></span>
   
    ![In the new storage, select Containers, click the Containers tile, and then Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="82c76-117">Copy the storage access key</span><span class="sxs-lookup"><span data-stu-id="82c76-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="82c76-118">You'll need it soon to set up the input to the stream analytics service.</span><span class="sxs-lookup"><span data-stu-id="82c76-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![In the storage, open Settings, Keys, and take a copy of the Primary Access Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="82c76-120">Start continuous export to Azure storage</span><span class="sxs-lookup"><span data-stu-id="82c76-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="82c76-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span><span class="sxs-lookup"><span data-stu-id="82c76-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="82c76-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span><span class="sxs-lookup"><span data-stu-id="82c76-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Choose Browse, Application Insights, your application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="82c76-124">Create a continuous export.</span><span class="sxs-lookup"><span data-stu-id="82c76-124">Create a continuous export.</span></span>
   
    ![Choose Settings, Continuous Export, Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="82c76-126">Select the storage account you created earlier:</span><span class="sxs-lookup"><span data-stu-id="82c76-126">Select the storage account you created earlier:</span></span>

    ![Set the export destination](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="82c76-128">Set the event types you want to see:</span><span class="sxs-lookup"><span data-stu-id="82c76-128">Set the event types you want to see:</span></span>

    ![Choose event types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="82c76-130">Let some data accumulate.</span><span class="sxs-lookup"><span data-stu-id="82c76-130">Let some data accumulate.</span></span> <span data-ttu-id="82c76-131">Sit back and let people use your application for a while.</span><span class="sxs-lookup"><span data-stu-id="82c76-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="82c76-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="82c76-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="82c76-133">And also, the data will export to your storage.</span><span class="sxs-lookup"><span data-stu-id="82c76-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="82c76-134">Inspect the exported data.</span><span class="sxs-lookup"><span data-stu-id="82c76-134">Inspect the exported data.</span></span> <span data-ttu-id="82c76-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span><span class="sxs-lookup"><span data-stu-id="82c76-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="82c76-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span><span class="sxs-lookup"><span data-stu-id="82c76-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="82c76-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="82c76-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="82c76-138">The events are written to blob files in JSON format.</span><span class="sxs-lookup"><span data-stu-id="82c76-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="82c76-139">Each file may contain one or more events.</span><span class="sxs-lookup"><span data-stu-id="82c76-139">Each file may contain one or more events.</span></span> <span data-ttu-id="82c76-140">So we'd like to read the event data and filter out the fields we want.</span><span class="sxs-lookup"><span data-stu-id="82c76-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="82c76-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span><span class="sxs-lookup"><span data-stu-id="82c76-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="82c76-142">Create an Azure Stream Analytics instance</span><span class="sxs-lookup"><span data-stu-id="82c76-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="82c76-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span><span class="sxs-lookup"><span data-stu-id="82c76-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/090.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="82c76-144">When the new job is created, expand its details:</span><span class="sxs-lookup"><span data-stu-id="82c76-144">When the new job is created, expand its details:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="82c76-145">Set blob location</span><span class="sxs-lookup"><span data-stu-id="82c76-145">Set blob location</span></span>
<span data-ttu-id="82c76-146">Set it to take input from your Continuous Export blob:</span><span class="sxs-lookup"><span data-stu-id="82c76-146">Set it to take input from your Continuous Export blob:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="82c76-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="82c76-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="82c76-148">Set this as the Storage Account Key.</span><span class="sxs-lookup"><span data-stu-id="82c76-148">Set this as the Storage Account Key.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="82c76-149">Set path prefix pattern</span><span class="sxs-lookup"><span data-stu-id="82c76-149">Set path prefix pattern</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="82c76-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span><span class="sxs-lookup"><span data-stu-id="82c76-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="82c76-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span><span class="sxs-lookup"><span data-stu-id="82c76-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="82c76-152">You need to set it to correspond to how Continuous Export stores the data.</span><span class="sxs-lookup"><span data-stu-id="82c76-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="82c76-153">Set it like this:</span><span class="sxs-lookup"><span data-stu-id="82c76-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="82c76-154">In this example:</span><span class="sxs-lookup"><span data-stu-id="82c76-154">In this example:</span></span>

* <span data-ttu-id="82c76-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span><span class="sxs-lookup"><span data-stu-id="82c76-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="82c76-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span><span class="sxs-lookup"><span data-stu-id="82c76-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="82c76-157">`PageViews` is the type of data you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="82c76-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="82c76-158">The available types depend on the filter you set in Continuous Export.</span><span class="sxs-lookup"><span data-stu-id="82c76-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="82c76-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="82c76-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="82c76-160">`/{date}/{time}` is a pattern written literally.</span><span class="sxs-lookup"><span data-stu-id="82c76-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="82c76-161">Inspect the storage to make sure you get the path right.</span><span class="sxs-lookup"><span data-stu-id="82c76-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="82c76-162">Finish initial setup</span><span class="sxs-lookup"><span data-stu-id="82c76-162">Finish initial setup</span></span>
<span data-ttu-id="82c76-163">Confirm the serialization format:</span><span class="sxs-lookup"><span data-stu-id="82c76-163">Confirm the serialization format:</span></span>

![Confirm and close wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="82c76-165">Close the wizard and wait for the setup to complete.</span><span class="sxs-lookup"><span data-stu-id="82c76-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="82c76-166">Use the Sample command to download some data.</span><span class="sxs-lookup"><span data-stu-id="82c76-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="82c76-167">Keep it as a test sample to debug your query.</span><span class="sxs-lookup"><span data-stu-id="82c76-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="82c76-168">Set the output</span><span class="sxs-lookup"><span data-stu-id="82c76-168">Set the output</span></span>
<span data-ttu-id="82c76-169">Now select your job and set the output.</span><span class="sxs-lookup"><span data-stu-id="82c76-169">Now select your job and set the output.</span></span>

![Select the new channel, click Outputs, Add, Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="82c76-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span><span class="sxs-lookup"><span data-stu-id="82c76-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="82c76-172">Then invent a name for the output, and for the target Power BI dataset and table.</span><span class="sxs-lookup"><span data-stu-id="82c76-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Invent three names](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="82c76-174">Set the query</span><span class="sxs-lookup"><span data-stu-id="82c76-174">Set the query</span></span>
<span data-ttu-id="82c76-175">The query governs the translation from input to output.</span><span class="sxs-lookup"><span data-stu-id="82c76-175">The query governs the translation from input to output.</span></span>

![Select the job and click Query.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="82c76-178">Use the Test function to check that you get the right output.</span><span class="sxs-lookup"><span data-stu-id="82c76-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="82c76-179">Give it the sample data that you took from the inputs page.</span><span class="sxs-lookup"><span data-stu-id="82c76-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="82c76-180">Query to display counts of events</span><span class="sxs-lookup"><span data-stu-id="82c76-180">Query to display counts of events</span></span>
<span data-ttu-id="82c76-181">Paste this query:</span><span class="sxs-lookup"><span data-stu-id="82c76-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="82c76-182">export-input is the alias we gave to the stream input</span><span class="sxs-lookup"><span data-stu-id="82c76-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="82c76-183">pbi-output is the output alias we defined</span><span class="sxs-lookup"><span data-stu-id="82c76-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="82c76-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span><span class="sxs-lookup"><span data-stu-id="82c76-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="82c76-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span><span class="sxs-lookup"><span data-stu-id="82c76-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="82c76-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span><span class="sxs-lookup"><span data-stu-id="82c76-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="82c76-187">Query to display metric values</span><span class="sxs-lookup"><span data-stu-id="82c76-187">Query to display metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="82c76-188">This query drills into the metrics telemetry to get the event time and the metric value.</span><span class="sxs-lookup"><span data-stu-id="82c76-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="82c76-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span><span class="sxs-lookup"><span data-stu-id="82c76-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="82c76-190">"myMetric" is the name of the metric in this case.</span><span class="sxs-lookup"><span data-stu-id="82c76-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="82c76-191">Query to include values of dimension properties</span><span class="sxs-lookup"><span data-stu-id="82c76-191">Query to include values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="82c76-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span><span class="sxs-lookup"><span data-stu-id="82c76-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="82c76-193">Run the job</span><span class="sxs-lookup"><span data-stu-id="82c76-193">Run the job</span></span>
<span data-ttu-id="82c76-194">You can select a date in the past to start the job from.</span><span class="sxs-lookup"><span data-stu-id="82c76-194">You can select a date in the past to start the job from.</span></span> 

![Select the job and click Query.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="82c76-197">Wait until the job is Running.</span><span class="sxs-lookup"><span data-stu-id="82c76-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="82c76-198">See results in Power BI</span><span class="sxs-lookup"><span data-stu-id="82c76-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="82c76-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="82c76-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="82c76-200">The path illustrated here is just an example to illustrate how to process exported data.</span><span class="sxs-lookup"><span data-stu-id="82c76-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="82c76-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="82c76-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![In Power BI, select your dataset and fields.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="82c76-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="82c76-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![In Power BI, select your dataset and fields.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="82c76-205">No data?</span><span class="sxs-lookup"><span data-stu-id="82c76-205">No data?</span></span>
* <span data-ttu-id="82c76-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span><span class="sxs-lookup"><span data-stu-id="82c76-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="82c76-207">Video</span><span class="sxs-lookup"><span data-stu-id="82c76-207">Video</span></span>
<span data-ttu-id="82c76-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="82c76-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="82c76-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="82c76-209">Next steps</span></span>
* [<span data-ttu-id="82c76-210">Continuous export</span><span class="sxs-lookup"><span data-stu-id="82c76-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="82c76-211">Detailed data model reference for the property types and values.</span><span class="sxs-lookup"><span data-stu-id="82c76-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="82c76-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="82c76-212">Application Insights</span></span>](app-insights-overview.md)























