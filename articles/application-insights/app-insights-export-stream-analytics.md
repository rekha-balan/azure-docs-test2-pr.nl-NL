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
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a>Use Stream Analytics to process exported data from Application Insights
[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md). Stream Analytics can pull data from a variety of sources. It can transform and filter the data, and then route it to a variety of sinks.

In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.

> [!WARNING]
> There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md). The path illustrated here is just an example to illustrate how to process exported data.
> 
> 

![Block diagram for export through SA to PBI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Create storage in Azure
Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.

1. Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).
   
   ![In Azure portal, choose New, Data, Storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/030.png)
2. Create a container
   
    ![In the new storage, select Containers, click the Containers tile, and then Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/040.png)
3. Copy the storage access key
   
    You'll need it soon to set up the input to the stream analytics service.
   
    ![In the storage, open Settings, Keys, and take a copy of the Primary Access Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a>Start continuous export to Azure storage
[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.

1. In the Azure portal, browse to the Application Insights resource you created for your application.
   
    ![Choose Browse, Application Insights, your application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/050.png)
2. Create a continuous export.
   
    ![Choose Settings, Continuous Export, Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/060.png)

    Select the storage account you created earlier:

    ![Set the export destination](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/070.png)

    Set the event types you want to see:

    ![Choose event types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/080.png)

1. Let some data accumulate. Sit back and let people use your application for a while. Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md). 
   
    And also, the data will export to your storage. 
2. Inspect the exported data. In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage. (If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/04-data.png)
   
    Make a note of the common part of the path name, which is derived from the application name and instrumentation key. 

The events are written to blob files in JSON format. Each file may contain one or more events. So we'd like to read the event data and filter out the fields we want. There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Create an Azure Stream Analytics instance
From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/090.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/100.png)

When the new job is created, expand its details:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Set blob location
Set it to take input from your Continuous Export blob:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/120.png)

Now you'll need the Primary Access Key from your Storage Account, which you noted earlier. Set this as the Storage Account Key.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Set path prefix pattern
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/140.png)

**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**

The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage. You need to set it to correspond to how Continuous Export stores the data. Set it like this:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

In this example:

* `webapplication27` is the name of the Application Insights resource **all lower case**.
* `1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**. 
* `PageViews` is the type of data you want to analyze. The available types depend on the filter you set in Continuous Export. Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).
* `/{date}/{time}` is a pattern written literally.

> [!NOTE]
> Inspect the storage to make sure you get the path right.
> 
> 

### <a name="finish-initial-setup"></a>Finish initial setup
Confirm the serialization format:

![Confirm and close wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/150.png)

Close the wizard and wait for the setup to complete.

> [!TIP]
> Use the Sample command to download some data. Keep it as a test sample to debug your query.
> 
> 

## <a name="set-the-output"></a>Set the output
Now select your job and set the output.

![Select the new channel, click Outputs, Add, Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/160.png)

Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource. Then invent a name for the output, and for the target Power BI dataset and table.

![Invent three names](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a>Set the query
The query governs the translation from input to output.

![Select the job and click Query. Paste the sample below.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/180.png)

Use the Test function to check that you get the right output. Give it the sample data that you took from the inputs page. 

### <a name="query-to-display-counts-of-events"></a>Query to display counts of events
Paste this query:

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

* export-input is the alias we gave to the stream input
* pbi-output is the output alias we defined
* We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray. Then the Select picks the event name, together with a count of the number of instances with that name in the time period. The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.

### <a name="query-to-display-metric-values"></a>Query to display metric values
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

* This query drills into the metrics telemetry to get the event time and the metric value. The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows. "myMetric" is the name of the metric in this case. 

### <a name="query-to-include-values-of-dimension-properties"></a>Query to include values of dimension properties
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

* This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.

## <a name="run-the-job"></a>Run the job
You can select a date in the past to start the job from. 

![Select the job and click Query. Paste the sample below.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/190.png)

Wait until the job is Running.

## <a name="see-results-in-power-bi"></a>See results in Power BI
> [!WARNING]
> There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md). The path illustrated here is just an example to illustrate how to process exported data.
> 
> 

Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.

![In Power BI, select your dataset and fields.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/200.png)

Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).

![In Power BI, select your dataset and fields.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>No data?
* Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).

## <a name="video"></a>Video
Noam Ben Zeev shows how to process exported data using Stream Analytics.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Next steps
* [Continuous export](app-insights-export-telemetry.md)
* [Detailed data model reference for the property types and values.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)























