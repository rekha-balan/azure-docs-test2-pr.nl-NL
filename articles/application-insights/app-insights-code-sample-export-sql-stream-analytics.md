---
title: Export to SQL from Azure Application Insights | Microsoft Docs
description: Continuously export Application Insights data to SQL using Stream Analytics.
services: application-insights
documentationcenter: ''
author: noamben
manager: douge
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: awills
ms.openlocfilehash: f7a7af57d5686d07854ce6cea3ecc583a9061dcc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564594"
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="bed60-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bed60-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="bed60-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="bed60-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="bed60-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span><span class="sxs-lookup"><span data-stu-id="bed60-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="bed60-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span><span class="sxs-lookup"><span data-stu-id="bed60-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="bed60-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bed60-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="bed60-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span><span class="sxs-lookup"><span data-stu-id="bed60-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="bed60-109">We'll start with the assumption that you already have the app you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="bed60-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="bed60-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span><span class="sxs-lookup"><span data-stu-id="bed60-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="bed60-111">Add Application Insights to your application</span><span class="sxs-lookup"><span data-stu-id="bed60-111">Add Application Insights to your application</span></span>
<span data-ttu-id="bed60-112">To get started:</span><span class="sxs-lookup"><span data-stu-id="bed60-112">To get started:</span></span>

1. <span data-ttu-id="bed60-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="bed60-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="bed60-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span><span class="sxs-lookup"><span data-stu-id="bed60-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="bed60-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="bed60-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="bed60-116">Create storage in Azure</span><span class="sxs-lookup"><span data-stu-id="bed60-116">Create storage in Azure</span></span>
<span data-ttu-id="bed60-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span><span class="sxs-lookup"><span data-stu-id="bed60-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="bed60-118">Create a storage account in your subscription in the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="bed60-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![In Azure portal, choose New, Data, Storage.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="bed60-122">Create a container</span><span class="sxs-lookup"><span data-stu-id="bed60-122">Create a container</span></span>
   
    ![In the new storage, select Containers, click the Containers tile, and then Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="bed60-124">Copy the storage access key</span><span class="sxs-lookup"><span data-stu-id="bed60-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="bed60-125">You'll need it soon to set up the input to the stream analytics service.</span><span class="sxs-lookup"><span data-stu-id="bed60-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![In the storage, open Settings, Keys, and take a copy of the Primary Access Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="bed60-127">Start continuous export to Azure storage</span><span class="sxs-lookup"><span data-stu-id="bed60-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="bed60-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span><span class="sxs-lookup"><span data-stu-id="bed60-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Choose Browse, Application Insights, your application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="bed60-130">Create a continuous export.</span><span class="sxs-lookup"><span data-stu-id="bed60-130">Create a continuous export.</span></span>
   
    ![Choose Settings, Continuous Export, Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="bed60-132">Select the storage account you created earlier:</span><span class="sxs-lookup"><span data-stu-id="bed60-132">Select the storage account you created earlier:</span></span>

    ![Set the export destination](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="bed60-134">Set the event types you want to see:</span><span class="sxs-lookup"><span data-stu-id="bed60-134">Set the event types you want to see:</span></span>

    ![Choose event types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="bed60-136">Let some data accumulate.</span><span class="sxs-lookup"><span data-stu-id="bed60-136">Let some data accumulate.</span></span> <span data-ttu-id="bed60-137">Sit back and let people use your application for a while.</span><span class="sxs-lookup"><span data-stu-id="bed60-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="bed60-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="bed60-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="bed60-139">And also, the data will export to your storage.</span><span class="sxs-lookup"><span data-stu-id="bed60-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="bed60-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bed60-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="bed60-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span><span class="sxs-lookup"><span data-stu-id="bed60-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="bed60-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span><span class="sxs-lookup"><span data-stu-id="bed60-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![In Visual Studio, open Server Browser, Azure, Storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="bed60-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="bed60-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="bed60-145">The events are written to blob files in JSON format.</span><span class="sxs-lookup"><span data-stu-id="bed60-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="bed60-146">Each file may contain one or more events.</span><span class="sxs-lookup"><span data-stu-id="bed60-146">Each file may contain one or more events.</span></span> <span data-ttu-id="bed60-147">So we'd like to read the event data and filter out the fields we want.</span><span class="sxs-lookup"><span data-stu-id="bed60-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="bed60-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="bed60-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="bed60-149">That will make it easy to run lots of interesting queries.</span><span class="sxs-lookup"><span data-stu-id="bed60-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="bed60-150">Create an Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="bed60-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="bed60-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span><span class="sxs-lookup"><span data-stu-id="bed60-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![New, Data, SQL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="bed60-153">Make sure that the database server allows access to Azure services:</span><span class="sxs-lookup"><span data-stu-id="bed60-153">Make sure that the database server allows access to Azure services:</span></span>

![Browse, Servers, your server, Settings, Firewall, Allow Access to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="bed60-155">Create a table in Azure SQL DB</span><span class="sxs-lookup"><span data-stu-id="bed60-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="bed60-156">Connect to the database created in the previous section with your preferred management tool.</span><span class="sxs-lookup"><span data-stu-id="bed60-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="bed60-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="bed60-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="bed60-158">Create a new query, and execute the following T-SQL:</span><span class="sxs-lookup"><span data-stu-id="bed60-158">Create a new query, and execute the following T-SQL:</span></span>

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

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="bed60-159">In this sample, we are using data from page views.</span><span class="sxs-lookup"><span data-stu-id="bed60-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="bed60-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="bed60-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="bed60-161">Create an Azure Stream Analytics instance</span><span class="sxs-lookup"><span data-stu-id="bed60-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="bed60-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span><span class="sxs-lookup"><span data-stu-id="bed60-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="bed60-163">When the new job is created, expand its details:</span><span class="sxs-lookup"><span data-stu-id="bed60-163">When the new job is created, expand its details:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="bed60-164">Set blob location</span><span class="sxs-lookup"><span data-stu-id="bed60-164">Set blob location</span></span>
<span data-ttu-id="bed60-165">Set it to take input from your Continuous Export blob:</span><span class="sxs-lookup"><span data-stu-id="bed60-165">Set it to take input from your Continuous Export blob:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="bed60-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="bed60-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="bed60-167">Set this as the Storage Account Key.</span><span class="sxs-lookup"><span data-stu-id="bed60-167">Set this as the Storage Account Key.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="bed60-168">Set path prefix pattern</span><span class="sxs-lookup"><span data-stu-id="bed60-168">Set path prefix pattern</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="bed60-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span><span class="sxs-lookup"><span data-stu-id="bed60-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="bed60-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span><span class="sxs-lookup"><span data-stu-id="bed60-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="bed60-171">You need to set it to correspond to how Continuous Export stores the data.</span><span class="sxs-lookup"><span data-stu-id="bed60-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="bed60-172">Set it like this:</span><span class="sxs-lookup"><span data-stu-id="bed60-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="bed60-173">In this example:</span><span class="sxs-lookup"><span data-stu-id="bed60-173">In this example:</span></span>

* <span data-ttu-id="bed60-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span><span class="sxs-lookup"><span data-stu-id="bed60-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="bed60-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span><span class="sxs-lookup"><span data-stu-id="bed60-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="bed60-176">`PageViews` is the type of data we want to analyze.</span><span class="sxs-lookup"><span data-stu-id="bed60-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="bed60-177">The available types depend on the filter you set in Continuous Export.</span><span class="sxs-lookup"><span data-stu-id="bed60-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="bed60-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="bed60-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="bed60-179">`/{date}/{time}` is a pattern written literally.</span><span class="sxs-lookup"><span data-stu-id="bed60-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="bed60-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span><span class="sxs-lookup"><span data-stu-id="bed60-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="bed60-181">Finish initial setup</span><span class="sxs-lookup"><span data-stu-id="bed60-181">Finish initial setup</span></span>
<span data-ttu-id="bed60-182">Confirm the serialization format:</span><span class="sxs-lookup"><span data-stu-id="bed60-182">Confirm the serialization format:</span></span>

![Confirm and close wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="bed60-184">Close the wizard and wait for the setup to complete.</span><span class="sxs-lookup"><span data-stu-id="bed60-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="bed60-185">Use the Sample function to check that you have set the input path correctly.</span><span class="sxs-lookup"><span data-stu-id="bed60-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="bed60-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span><span class="sxs-lookup"><span data-stu-id="bed60-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="bed60-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span><span class="sxs-lookup"><span data-stu-id="bed60-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="bed60-188">Set query</span><span class="sxs-lookup"><span data-stu-id="bed60-188">Set query</span></span>
<span data-ttu-id="bed60-189">Open the query section:</span><span class="sxs-lookup"><span data-stu-id="bed60-189">Open the query section:</span></span>

![In stream analytics, select Query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="bed60-191">Replace the default query with:</span><span class="sxs-lookup"><span data-stu-id="bed60-191">Replace the default query with:</span></span>

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

<span data-ttu-id="bed60-192">Notice that the first few properties are specific to page view data.</span><span class="sxs-lookup"><span data-stu-id="bed60-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="bed60-193">Exports of other telemetry types will have different properties.</span><span class="sxs-lookup"><span data-stu-id="bed60-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="bed60-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="bed60-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="bed60-195">Set up output to database</span><span class="sxs-lookup"><span data-stu-id="bed60-195">Set up output to database</span></span>
<span data-ttu-id="bed60-196">Select SQL as the output.</span><span class="sxs-lookup"><span data-stu-id="bed60-196">Select SQL as the output.</span></span>

![In stream analytics, select Outputs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="bed60-198">Specify the SQL database.</span><span class="sxs-lookup"><span data-stu-id="bed60-198">Specify the SQL database.</span></span>

![Fill in the details of your database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="bed60-200">Close the wizard and wait for a notification that the output has been set up.</span><span class="sxs-lookup"><span data-stu-id="bed60-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="bed60-201">Start processing</span><span class="sxs-lookup"><span data-stu-id="bed60-201">Start processing</span></span>
<span data-ttu-id="bed60-202">Start the job from the action bar:</span><span class="sxs-lookup"><span data-stu-id="bed60-202">Start the job from the action bar:</span></span>

![In stream analytics, click  Start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="bed60-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span><span class="sxs-lookup"><span data-stu-id="bed60-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="bed60-205">The latter is useful if you have had Continuous Export already running for a while.</span><span class="sxs-lookup"><span data-stu-id="bed60-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![In stream analytics, click  Start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="bed60-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span><span class="sxs-lookup"><span data-stu-id="bed60-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="bed60-208">For example, use a query like this:</span><span class="sxs-lookup"><span data-stu-id="bed60-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="bed60-209">Related articles</span><span class="sxs-lookup"><span data-stu-id="bed60-209">Related articles</span></span>
* [<span data-ttu-id="bed60-210">Export to PowerBI using Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bed60-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="bed60-211">Detailed data model reference for the property types and values.</span><span class="sxs-lookup"><span data-stu-id="bed60-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="bed60-212">Continuous Export in Application Insights</span><span class="sxs-lookup"><span data-stu-id="bed60-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="bed60-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="bed60-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

























