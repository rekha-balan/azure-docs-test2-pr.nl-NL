---
title: Export to SQL from Azure Application Insights | Microsoft Docs
description: Continuously export Application Insights data to SQL using Stream Analytics.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 03/06/2015
ms.author: mbullwin
ms.openlocfilehash: 7d4bf0c5beeba22569e0000b28b007fb5b0ff68f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779212"
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="a3f9f-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3f9f-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="a3f9f-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="a3f9f-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="a3f9f-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="a3f9f-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="a3f9f-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="a3f9f-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span><span class="sxs-lookup"><span data-stu-id="a3f9f-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="a3f9f-109">We'll start with the assumption that you already have the app you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="a3f9f-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="a3f9f-111">Add Application Insights to your application</span><span class="sxs-lookup"><span data-stu-id="a3f9f-111">Add Application Insights to your application</span></span>
<span data-ttu-id="a3f9f-112">To get started:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-112">To get started:</span></span>

1. <span data-ttu-id="a3f9f-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a3f9f-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="a3f9f-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span><span class="sxs-lookup"><span data-stu-id="a3f9f-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="a3f9f-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="a3f9f-116">Create storage in Azure</span><span class="sxs-lookup"><span data-stu-id="a3f9f-116">Create storage in Azure</span></span>
<span data-ttu-id="a3f9f-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="a3f9f-118">Create a storage account in your subscription in the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="a3f9f-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![In Azure portal, choose New, Data, Storage.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="a3f9f-122">Create a container</span><span class="sxs-lookup"><span data-stu-id="a3f9f-122">Create a container</span></span>
   
    ![In the new storage, select Containers, click the Containers tile, and then Add](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="a3f9f-124">Copy the storage access key</span><span class="sxs-lookup"><span data-stu-id="a3f9f-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="a3f9f-125">You'll need it soon to set up the input to the stream analytics service.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![In the storage, open Settings, Keys, and take a copy of the Primary Access Key](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="a3f9f-127">Start continuous export to Azure storage</span><span class="sxs-lookup"><span data-stu-id="a3f9f-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="a3f9f-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Choose Browse, Application Insights, your application](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="a3f9f-130">Create a continuous export.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-130">Create a continuous export.</span></span>
   
    ![Choose Settings, Continuous Export, Add](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="a3f9f-132">Select the storage account you created earlier:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-132">Select the storage account you created earlier:</span></span>

    ![Set the export destination](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="a3f9f-134">Set the event types you want to see:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-134">Set the event types you want to see:</span></span>

    ![Choose event types](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="a3f9f-136">Let some data accumulate.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-136">Let some data accumulate.</span></span> <span data-ttu-id="a3f9f-137">Sit back and let people use your application for a while.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="a3f9f-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="a3f9f-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="a3f9f-139">And also, the data will export to your storage.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="a3f9f-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="a3f9f-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="a3f9f-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span><span class="sxs-lookup"><span data-stu-id="a3f9f-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![In Visual Studio, open Server Browser, Azure, Storage](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="a3f9f-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="a3f9f-145">The events are written to blob files in JSON format.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="a3f9f-146">Each file may contain one or more events.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-146">Each file may contain one or more events.</span></span> <span data-ttu-id="a3f9f-147">So we'd like to read the event data and filter out the fields we want.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="a3f9f-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="a3f9f-149">That will make it easy to run lots of interesting queries.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="a3f9f-150">Create an Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3f9f-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="a3f9f-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![New, Data, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="a3f9f-153">Make sure that the database server allows access to Azure services:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-153">Make sure that the database server allows access to Azure services:</span></span>

![Browse, Servers, your server, Settings, Firewall, Allow Access to Azure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="a3f9f-155">Create a table in Azure SQL DB</span><span class="sxs-lookup"><span data-stu-id="a3f9f-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="a3f9f-156">Connect to the database created in the previous section with your preferred management tool.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="a3f9f-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="a3f9f-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="a3f9f-158">Create a new query, and execute the following T-SQL:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-158">Create a new query, and execute the following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="a3f9f-159">In this sample, we are using data from page views.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="a3f9f-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a3f9f-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="a3f9f-161">Create an Azure Stream Analytics instance</span><span class="sxs-lookup"><span data-stu-id="a3f9f-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="a3f9f-162">From the [Azure portal](https://portal.azure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-162">From the [Azure portal](https://portal.azure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/SA001.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/SA002.png)

<span data-ttu-id="a3f9f-163">When the new job is created, select **Go to resource**.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-163">When the new job is created, select **Go to resource**.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/SA003.png)

#### <a name="add-a-new-input"></a><span data-ttu-id="a3f9f-164">Add a new input</span><span class="sxs-lookup"><span data-stu-id="a3f9f-164">Add a new input</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/SA004.png)

<span data-ttu-id="a3f9f-165">Set it to take input from your Continuous Export blob:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/SA005.png)

<span data-ttu-id="a3f9f-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="a3f9f-167">Set this as the Storage Account Key.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-167">Set this as the Storage Account Key.</span></span>

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="a3f9f-168">Set path prefix pattern</span><span class="sxs-lookup"><span data-stu-id="a3f9f-168">Set path prefix pattern</span></span>

<span data-ttu-id="a3f9f-169">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span><span class="sxs-lookup"><span data-stu-id="a3f9f-169">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="a3f9f-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="a3f9f-171">You need to set it to correspond to how Continuous Export stores the data.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="a3f9f-172">Set it like this:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="a3f9f-173">In this example:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-173">In this example:</span></span>

* <span data-ttu-id="a3f9f-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="a3f9f-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="a3f9f-176">`PageViews` is the type of data we want to analyze.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="a3f9f-177">The available types depend on the filter you set in Continuous Export.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="a3f9f-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a3f9f-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="a3f9f-179">`/{date}/{time}` is a pattern written literally.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="a3f9f-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

> [!TIP]
> <span data-ttu-id="a3f9f-181">Use the Sample function to check that you have set the input path correctly.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-181">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="a3f9f-182">If it fails: Check that there is data in the storage for the sample time range you chose.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-182">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="a3f9f-183">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-183">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 
## <a name="set-query"></a><span data-ttu-id="a3f9f-184">Set query</span><span class="sxs-lookup"><span data-stu-id="a3f9f-184">Set query</span></span>
<span data-ttu-id="a3f9f-185">Open the query section:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-185">Open the query section:</span></span>

<span data-ttu-id="a3f9f-186">Replace the default query with:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-186">Replace the default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="a3f9f-187">Notice that the first few properties are specific to page view data.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-187">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="a3f9f-188">Exports of other telemetry types will have different properties.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-188">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="a3f9f-189">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="a3f9f-189">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="a3f9f-190">Set up output to database</span><span class="sxs-lookup"><span data-stu-id="a3f9f-190">Set up output to database</span></span>
<span data-ttu-id="a3f9f-191">Select SQL as the output.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-191">Select SQL as the output.</span></span>

![In stream analytics, select Outputs](./media/app-insights-code-sample-export-sql-stream-analytics/SA006.png)

<span data-ttu-id="a3f9f-193">Specify the SQL database.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-193">Specify the SQL database.</span></span>

![Fill in the details of your database](./media/app-insights-code-sample-export-sql-stream-analytics/SA007.png)

<span data-ttu-id="a3f9f-195">Close the wizard and wait for a notification that the output has been set up.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-195">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="a3f9f-196">Start processing</span><span class="sxs-lookup"><span data-stu-id="a3f9f-196">Start processing</span></span>
<span data-ttu-id="a3f9f-197">Start the job from the action bar:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-197">Start the job from the action bar:</span></span>

![In stream analytics, click  Start](./media/app-insights-code-sample-export-sql-stream-analytics/SA008.png)

<span data-ttu-id="a3f9f-199">You can choose whether to start processing the data starting from now, or to start with earlier data.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-199">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="a3f9f-200">The latter is useful if you have had Continuous Export already running for a while.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-200">The latter is useful if you have had Continuous Export already running for a while.</span></span>

<span data-ttu-id="a3f9f-201">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-201">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="a3f9f-202">For example, use a query like this:</span><span class="sxs-lookup"><span data-stu-id="a3f9f-202">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="a3f9f-203">Related articles</span><span class="sxs-lookup"><span data-stu-id="a3f9f-203">Related articles</span></span>
* [<span data-ttu-id="a3f9f-204">Export to PowerBI using Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3f9f-204">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="a3f9f-205">Detailed data model reference for the property types and values.</span><span class="sxs-lookup"><span data-stu-id="a3f9f-205">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="a3f9f-206">Continuous Export in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a3f9f-206">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="a3f9f-207">Application Insights</span><span class="sxs-lookup"><span data-stu-id="a3f9f-207">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

