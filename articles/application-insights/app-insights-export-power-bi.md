---
title: Export to Power BI from Application Insights | Microsoft Docs
description: Analytics queries can be displayed in Power BI.
services: application-insights
documentationcenter: ''
author: noamben
manager: douge
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: awills
ms.openlocfilehash: bb1528d0295e60255b87c24f11c4d6228658a8a2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549853"
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="da783-103">Feed Power BI from Application Insights</span><span class="sxs-lookup"><span data-stu-id="da783-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="da783-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span><span class="sxs-lookup"><span data-stu-id="da783-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="da783-105">Rich dashboards are available on every device.</span><span class="sxs-lookup"><span data-stu-id="da783-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="da783-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da783-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="da783-107">There are three recommended methods of exporting Application Insights data to Power BI.</span><span class="sxs-lookup"><span data-stu-id="da783-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="da783-108">You can use them separately or together.</span><span class="sxs-lookup"><span data-stu-id="da783-108">You can use them separately or together.</span></span>

* <span data-ttu-id="da783-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span><span class="sxs-lookup"><span data-stu-id="da783-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="da783-110">The set of charts is predefined, but you can add your own queries from any other sources.</span><span class="sxs-lookup"><span data-stu-id="da783-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="da783-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span><span class="sxs-lookup"><span data-stu-id="da783-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="da783-112">You can place this query on a dashboard along with any other data.</span><span class="sxs-lookup"><span data-stu-id="da783-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="da783-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span><span class="sxs-lookup"><span data-stu-id="da783-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="da783-114">It is useful if you want to keep your data for long periods.</span><span class="sxs-lookup"><span data-stu-id="da783-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="da783-115">Otherwise, the other methods are recommended.</span><span class="sxs-lookup"><span data-stu-id="da783-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="da783-116">Power BI adapter</span><span class="sxs-lookup"><span data-stu-id="da783-116">Power BI adapter</span></span>
<span data-ttu-id="da783-117">This method creates a complete dashboard of telemetry for you.</span><span class="sxs-lookup"><span data-stu-id="da783-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="da783-118">The initial data set is predefined, but you can add more data to it.</span><span class="sxs-lookup"><span data-stu-id="da783-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="da783-119">Get the adapter</span><span class="sxs-lookup"><span data-stu-id="da783-119">Get the adapter</span></span>
1. <span data-ttu-id="da783-120">Sign in to [Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="da783-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="da783-121">Open **Get Data**, **Services**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="da783-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Get from Application Insights data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="da783-123">Provide the details of your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="da783-123">Provide the details of your Application Insights resource.</span></span>
   
    ![Get from Application Insights data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="da783-125">Wait a minute or two for the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="da783-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Power BI adapter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/010.png)

<span data-ttu-id="da783-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="da783-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="da783-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span><span class="sxs-lookup"><span data-stu-id="da783-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="da783-129">After the initial import, the dashboard and the reports continue to update daily.</span><span class="sxs-lookup"><span data-stu-id="da783-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="da783-130">You can control the refresh schedule on the dataset.</span><span class="sxs-lookup"><span data-stu-id="da783-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="da783-131">Export Analytics queries</span><span class="sxs-lookup"><span data-stu-id="da783-131">Export Analytics queries</span></span>
<span data-ttu-id="da783-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span><span class="sxs-lookup"><span data-stu-id="da783-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="da783-133">(You can add to the dashboard created by the adapter.)</span><span class="sxs-lookup"><span data-stu-id="da783-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="da783-134">One time: install Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="da783-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="da783-135">To import your Application Insights query, you use the desktop version of Power BI.</span><span class="sxs-lookup"><span data-stu-id="da783-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="da783-136">But then you can publish it to the web or to your Power BI cloud workspace.</span><span class="sxs-lookup"><span data-stu-id="da783-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="da783-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="da783-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="da783-138">Export an Analytics query</span><span class="sxs-lookup"><span data-stu-id="da783-138">Export an Analytics query</span></span>
1. <span data-ttu-id="da783-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="da783-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="da783-140">Test and refine the query until you're happy with the results.</span><span class="sxs-lookup"><span data-stu-id="da783-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="da783-141">**Make sure that the query runs correctly in Analytics before you export it.**</span><span class="sxs-lookup"><span data-stu-id="da783-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="da783-142">On the **Export** menu, choose **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="da783-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="da783-143">Save the text file.</span><span class="sxs-lookup"><span data-stu-id="da783-143">Save the text file.</span></span>
   
    ![Export Power BI query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="da783-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="da783-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="da783-146">Paste the exported M Language script into the Advanced Query Editor.</span><span class="sxs-lookup"><span data-stu-id="da783-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![Advanced query editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="da783-148">You might have to provide credentials to allow Power BI to access Azure.</span><span class="sxs-lookup"><span data-stu-id="da783-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="da783-149">Use 'organizational account' to sign in with your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="da783-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![Supply Azure credentials to enable Power BI to run your Application Insights query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="da783-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="da783-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="da783-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span><span class="sxs-lookup"><span data-stu-id="da783-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="da783-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span><span class="sxs-lookup"><span data-stu-id="da783-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Select visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="da783-155">Publish your report to your Power BI cloud workspace.</span><span class="sxs-lookup"><span data-stu-id="da783-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="da783-156">From there, you can embed a synchronized version into other web pages.</span><span class="sxs-lookup"><span data-stu-id="da783-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Select visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="da783-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span><span class="sxs-lookup"><span data-stu-id="da783-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="about-sampling"></a><span data-ttu-id="da783-159">About sampling</span><span class="sxs-lookup"><span data-stu-id="da783-159">About sampling</span></span>
<span data-ttu-id="da783-160">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span><span class="sxs-lookup"><span data-stu-id="da783-160">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="da783-161">The same is true if you have manually set sampling either in the SDK or on ingestion.</span><span class="sxs-lookup"><span data-stu-id="da783-161">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="da783-162">Learn more about sampling.</span><span class="sxs-lookup"><span data-stu-id="da783-162">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <a name="next-steps"></a><span data-ttu-id="da783-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="da783-163">Next steps</span></span>
* [<span data-ttu-id="da783-164">Power BI - Learn</span><span class="sxs-lookup"><span data-stu-id="da783-164">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="da783-165">Analytics tutorial</span><span class="sxs-lookup"><span data-stu-id="da783-165">Analytics tutorial</span></span>](app-insights-analytics-tour.md)









