---
title: Monitor DocumentDB requests and storage | Microsoft Docs
description: Learn how to monitor your DocumentDB account for performance metrics, such as requests and server errors, and usage metrics, such as storage consumption.
services: documentdb
documentationcenter: ''
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: mimig
ms.openlocfilehash: 65a5ce65e0c05ebc92d9aeb0a8d12a18c7025f7a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555172"
---
# <a name="monitor-documentdb-requests-usage-and-storage"></a><span data-ttu-id="1e16a-103">Monitor DocumentDB requests, usage, and storage</span><span class="sxs-lookup"><span data-stu-id="1e16a-103">Monitor DocumentDB requests, usage, and storage</span></span>
<span data-ttu-id="1e16a-104">You can monitor your Azure DocumentDB accounts in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e16a-104">You can monitor your Azure DocumentDB accounts in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1e16a-105">For each DocumentDB account, both performance metrics, such as requests and server errors, and usage metrics, such as storage consumption, are available.</span><span class="sxs-lookup"><span data-stu-id="1e16a-105">For each DocumentDB account, both performance metrics, such as requests and server errors, and usage metrics, such as storage consumption, are available.</span></span>

<span data-ttu-id="1e16a-106">Metrics can be reviewed on the Account blade, the new Metrics blade, or in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="1e16a-106">Metrics can be reviewed on the Account blade, the new Metrics blade, or in Azure Monitor.</span></span>

## <a name="view-performance-metrics-on-the-metrics-blade"></a><span data-ttu-id="1e16a-107">View performance metrics on the Metrics blade</span><span class="sxs-lookup"><span data-stu-id="1e16a-107">View performance metrics on the Metrics blade</span></span>
1. <span data-ttu-id="1e16a-108">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **NoSQL (DocumentDB)**, and then click the name of the DocumentDB account for which you would like to view performance metrics.</span><span class="sxs-lookup"><span data-stu-id="1e16a-108">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **NoSQL (DocumentDB)**, and then click the name of the DocumentDB account for which you would like to view performance metrics.</span></span>
2. <span data-ttu-id="1e16a-109">In the resource menu, under **Monitoring**, click **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-109">In the resource menu, under **Monitoring**, click **Metrics**.</span></span>

<span data-ttu-id="1e16a-110">The Metrics blade opens, and you can select the collection to review.</span><span class="sxs-lookup"><span data-stu-id="1e16a-110">The Metrics blade opens, and you can select the collection to review.</span></span> <span data-ttu-id="1e16a-111">You can review Availability, Requests, Throughput, and Storage metrics and compare them to the DocumentDB SLAs.</span><span class="sxs-lookup"><span data-stu-id="1e16a-111">You can review Availability, Requests, Throughput, and Storage metrics and compare them to the DocumentDB SLAs.</span></span>

## <a name="view-performance-metrics-by-using-azure-monitoring"></a><span data-ttu-id="1e16a-112">View performance metrics by using Azure Monitoring</span><span class="sxs-lookup"><span data-stu-id="1e16a-112">View performance metrics by using Azure Monitoring</span></span>
1. <span data-ttu-id="1e16a-113">In the [Azure portal](https://portal.azure.com/), click **Monitor** on the Jumpbar.</span><span class="sxs-lookup"><span data-stu-id="1e16a-113">In the [Azure portal](https://portal.azure.com/), click **Monitor** on the Jumpbar.</span></span>
2. <span data-ttu-id="1e16a-114">In the resource menu, click **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-114">In the resource menu, click **Metrics**.</span></span>
3. <span data-ttu-id="1e16a-115">In the **Monitor - Metrics** window, in the **esource group** drop-down menu, select the resource group associated with the DocumentDB account that you'd like to monitor.</span><span class="sxs-lookup"><span data-stu-id="1e16a-115">In the **Monitor - Metrics** window, in the **esource group** drop-down menu, select the resource group associated with the DocumentDB account that you'd like to monitor.</span></span> 
4. <span data-ttu-id="1e16a-116">In the **Resource** drop-down menu, select the database account to monitor.</span><span class="sxs-lookup"><span data-stu-id="1e16a-116">In the **Resource** drop-down menu, select the database account to monitor.</span></span>
5. <span data-ttu-id="1e16a-117">In the list of **Available metrics**, select the metrics to display.</span><span class="sxs-lookup"><span data-stu-id="1e16a-117">In the list of **Available metrics**, select the metrics to display.</span></span> <span data-ttu-id="1e16a-118">Use the CTRL button to multi-select.</span><span class="sxs-lookup"><span data-stu-id="1e16a-118">Use the CTRL button to multi-select.</span></span> 

    <span data-ttu-id="1e16a-119">Your metrics are displayed on in the **Plot** window.</span><span class="sxs-lookup"><span data-stu-id="1e16a-119">Your metrics are displayed on in the **Plot** window.</span></span> 

## <a name="view-performance-metrics-on-the-account-blade"></a><span data-ttu-id="1e16a-120">View performance metrics on the account blade</span><span class="sxs-lookup"><span data-stu-id="1e16a-120">View performance metrics on the account blade</span></span>
1. <span data-ttu-id="1e16a-121">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **NoSQL (DocumentDB)**, and then click the name of the DocumentDB account for which you would like to view performance metrics.</span><span class="sxs-lookup"><span data-stu-id="1e16a-121">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **NoSQL (DocumentDB)**, and then click the name of the DocumentDB account for which you would like to view performance metrics.</span></span>
2. <span data-ttu-id="1e16a-122">The **Monitoring** lens displays the following tiles by default:</span><span class="sxs-lookup"><span data-stu-id="1e16a-122">The **Monitoring** lens displays the following tiles by default:</span></span>
   
   * <span data-ttu-id="1e16a-123">Total requests for the current day.</span><span class="sxs-lookup"><span data-stu-id="1e16a-123">Total requests for the current day.</span></span>
   * <span data-ttu-id="1e16a-124">Storage used.</span><span class="sxs-lookup"><span data-stu-id="1e16a-124">Storage used.</span></span>
   
   <span data-ttu-id="1e16a-125">If your table displays **No data available** and you believe there is data in your database, see the [Troubleshooting](#troubleshooting) section.</span><span class="sxs-lookup"><span data-stu-id="1e16a-125">If your table displays **No data available** and you believe there is data in your database, see the [Troubleshooting](#troubleshooting) section.</span></span>
   
   ![Screen shot of the Monitoring lens which shows the requests and the storage usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/documentdb-total-requests-and-usage.png)
3. <span data-ttu-id="1e16a-127">Clicking on the **Requests** or **Usage Quota** tile opens a detailed **Metric** blade.</span><span class="sxs-lookup"><span data-stu-id="1e16a-127">Clicking on the **Requests** or **Usage Quota** tile opens a detailed **Metric** blade.</span></span>
4. <span data-ttu-id="1e16a-128">The **Metric** blade shows you details about the metrics you have selected.</span><span class="sxs-lookup"><span data-stu-id="1e16a-128">The **Metric** blade shows you details about the metrics you have selected.</span></span>  <span data-ttu-id="1e16a-129">At the top of the blade is a graph of requests charted hourly, and below that is table that shows aggregation values for throttled and total requests.</span><span class="sxs-lookup"><span data-stu-id="1e16a-129">At the top of the blade is a graph of requests charted hourly, and below that is table that shows aggregation values for throttled and total requests.</span></span>  <span data-ttu-id="1e16a-130">The metric blade also shows the list of alerts which have been defined, filtered to the metrics that appear on the current metric blade (this way, if you have a number of alerts, you'll only see the relevant ones presented here).</span><span class="sxs-lookup"><span data-stu-id="1e16a-130">The metric blade also shows the list of alerts which have been defined, filtered to the metrics that appear on the current metric blade (this way, if you have a number of alerts, you'll only see the relevant ones presented here).</span></span>   
   
   ![Screenshot of the Metric blade which includes throttled requests](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-the-portal"></a><span data-ttu-id="1e16a-132">Customize performance metric views in the portal</span><span class="sxs-lookup"><span data-stu-id="1e16a-132">Customize performance metric views in the portal</span></span>
1. <span data-ttu-id="1e16a-133">To customize the metrics that display in a particular chart, click the chart to open it in the **Metric** blade, and then click **Edit chart**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-133">To customize the metrics that display in a particular chart, click the chart to open it in the **Metric** blade, and then click **Edit chart**.</span></span>  
   <span data-ttu-id="1e16a-134">![Screen shot of the Metric blade controls, with Edit chart highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb3.png)</span><span class="sxs-lookup"><span data-stu-id="1e16a-134">![Screen shot of the Metric blade controls, with Edit chart highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb3.png)</span></span>
2. <span data-ttu-id="1e16a-135">On the **Edit Chart** blade, there are options to modify the metrics that display in the chart, as well as their time range.</span><span class="sxs-lookup"><span data-stu-id="1e16a-135">On the **Edit Chart** blade, there are options to modify the metrics that display in the chart, as well as their time range.</span></span>  
   <span data-ttu-id="1e16a-136">![Screen shot of the Edit Chart blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb4.png)</span><span class="sxs-lookup"><span data-stu-id="1e16a-136">![Screen shot of the Edit Chart blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb4.png)</span></span>
3. <span data-ttu-id="1e16a-137">To change the metrics displayed in the part, simply select or clear the available performance metrics, and then click **OK** at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="1e16a-137">To change the metrics displayed in the part, simply select or clear the available performance metrics, and then click **OK** at the bottom of the blade.</span></span>  
4. <span data-ttu-id="1e16a-138">To change the time range, choose a different range (for example, **Custom**), and then click **OK** at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="1e16a-138">To change the time range, choose a different range (for example, **Custom**), and then click **OK** at the bottom of the blade.</span></span>  
   
   ![Screen shot of the Time Range part of the Edit Chart blade showing how to enter a custom time range](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-the-portal"></a><span data-ttu-id="1e16a-140">Create side-by-side charts in the portal</span><span class="sxs-lookup"><span data-stu-id="1e16a-140">Create side-by-side charts in the portal</span></span>
<span data-ttu-id="1e16a-141">The Azure Portal allows you to create side-by-side metric charts.</span><span class="sxs-lookup"><span data-stu-id="1e16a-141">The Azure Portal allows you to create side-by-side metric charts.</span></span>  

1. <span data-ttu-id="1e16a-142">First, right-click on the chart you want to copy and select **Customize**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-142">First, right-click on the chart you want to copy and select **Customize**.</span></span>
   
   ![Screen shot of the Total Requests chart with the Customize option highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb6.png)
2. <span data-ttu-id="1e16a-144">Click **Clone** on the menu to copy the part and then click **Done customizing**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-144">Click **Clone** on the menu to copy the part and then click **Done customizing**.</span></span>
   
   ![Screen shot of the Total Requests chart with the Clone and Done customizing options highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb7.png)  

<span data-ttu-id="1e16a-146">You may now treat this part as any other metric part, customizing the metrics and time range displayed in the part.</span><span class="sxs-lookup"><span data-stu-id="1e16a-146">You may now treat this part as any other metric part, customizing the metrics and time range displayed in the part.</span></span>  <span data-ttu-id="1e16a-147">By doing this, you can see two different metrics chart side-by-side at the same time.</span><span class="sxs-lookup"><span data-stu-id="1e16a-147">By doing this, you can see two different metrics chart side-by-side at the same time.</span></span>  
    ![Screen shot of the Total Requests chart and the new Total Requests past hour chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-the-portal"></a><span data-ttu-id="1e16a-149">Set up alerts in the portal</span><span class="sxs-lookup"><span data-stu-id="1e16a-149">Set up alerts in the portal</span></span>
1. <span data-ttu-id="1e16a-150">In the [Azure portal](https://portal.azure.com/), click **More Services**, click **DocumentDB (NoSQL)**, and then click the name of the DocumentDB account for which you would like to setup performance metric alerts.</span><span class="sxs-lookup"><span data-stu-id="1e16a-150">In the [Azure portal](https://portal.azure.com/), click **More Services**, click **DocumentDB (NoSQL)**, and then click the name of the DocumentDB account for which you would like to setup performance metric alerts.</span></span>
2. <span data-ttu-id="1e16a-151">In the resource menu, click **Alert Rules** to open the Alert rules blade.</span><span class="sxs-lookup"><span data-stu-id="1e16a-151">In the resource menu, click **Alert Rules** to open the Alert rules blade.</span></span>  
   <span data-ttu-id="1e16a-152">![Screen shot of the Alert rules part selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb10.5.png)</span><span class="sxs-lookup"><span data-stu-id="1e16a-152">![Screen shot of the Alert rules part selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb10.5.png)</span></span>
3. <span data-ttu-id="1e16a-153">In the **Alert rules** blade, click **Add alert**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-153">In the **Alert rules** blade, click **Add alert**.</span></span>  
   <span data-ttu-id="1e16a-154">![Screenshot of the Alert Rules blade, with the Add Alert button highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb11.png)</span><span class="sxs-lookup"><span data-stu-id="1e16a-154">![Screenshot of the Alert Rules blade, with the Add Alert button highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb11.png)</span></span>
4. <span data-ttu-id="1e16a-155">In the **Add an alert rule** blade, specify:</span><span class="sxs-lookup"><span data-stu-id="1e16a-155">In the **Add an alert rule** blade, specify:</span></span>
   
   * <span data-ttu-id="1e16a-156">The name of the alert rule you are setting up.</span><span class="sxs-lookup"><span data-stu-id="1e16a-156">The name of the alert rule you are setting up.</span></span>
   * <span data-ttu-id="1e16a-157">A description of the new alert rule.</span><span class="sxs-lookup"><span data-stu-id="1e16a-157">A description of the new alert rule.</span></span>
   * <span data-ttu-id="1e16a-158">The metric for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="1e16a-158">The metric for the alert rule.</span></span>
   * <span data-ttu-id="1e16a-159">The condition, threshold, and period that determine when the alert activates.</span><span class="sxs-lookup"><span data-stu-id="1e16a-159">The condition, threshold, and period that determine when the alert activates.</span></span> <span data-ttu-id="1e16a-160">For example, a server error count greater than 5 over the last 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="1e16a-160">For example, a server error count greater than 5 over the last 15 minutes.</span></span>
   * <span data-ttu-id="1e16a-161">Whether the service administrator and coadministrators are emailed when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="1e16a-161">Whether the service administrator and coadministrators are emailed when the alert fires.</span></span>
   * <span data-ttu-id="1e16a-162">Additional email addresses for alert notifications.</span><span class="sxs-lookup"><span data-stu-id="1e16a-162">Additional email addresses for alert notifications.</span></span>  
     ![Screen shot of the Add an alert rule blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb12.png)

## <a name="monitor-documentdb-programatically"></a><span data-ttu-id="1e16a-164">Monitor DocumentDB programatically</span><span class="sxs-lookup"><span data-stu-id="1e16a-164">Monitor DocumentDB programatically</span></span>
<span data-ttu-id="1e16a-165">The account level metrics available in the portal, such as account storage usage and total requests, are not available via the DocumentDB APIs.</span><span class="sxs-lookup"><span data-stu-id="1e16a-165">The account level metrics available in the portal, such as account storage usage and total requests, are not available via the DocumentDB APIs.</span></span> <span data-ttu-id="1e16a-166">However, you can retrieve usage data at the collection level by using the DocumentDB APIs.</span><span class="sxs-lookup"><span data-stu-id="1e16a-166">However, you can retrieve usage data at the collection level by using the DocumentDB APIs.</span></span> <span data-ttu-id="1e16a-167">To retrieve collection level data, do the following:</span><span class="sxs-lookup"><span data-stu-id="1e16a-167">To retrieve collection level data, do the following:</span></span>

* <span data-ttu-id="1e16a-168">To use the REST API, [perform a GET on the collection](https://msdn.microsoft.com/library/mt489073.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e16a-168">To use the REST API, [perform a GET on the collection](https://msdn.microsoft.com/library/mt489073.aspx).</span></span> <span data-ttu-id="1e16a-169">The quota and usage information for the collection is returned in the x-ms-resource-quota and x-ms-resource-usage headers in the response.</span><span class="sxs-lookup"><span data-stu-id="1e16a-169">The quota and usage information for the collection is returned in the x-ms-resource-quota and x-ms-resource-usage headers in the response.</span></span>
* <span data-ttu-id="1e16a-170">To use the .NET SDK, use the [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) method, which returns a [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) that contains a number of usage properties such as **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, and more.</span><span class="sxs-lookup"><span data-stu-id="1e16a-170">To use the .NET SDK, use the [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) method, which returns a [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) that contains a number of usage properties such as **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, and more.</span></span>

<span data-ttu-id="1e16a-171">To access additional metrics, use the [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights).</span><span class="sxs-lookup"><span data-stu-id="1e16a-171">To access additional metrics, use the [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights).</span></span> <span data-ttu-id="1e16a-172">Available metric definitions can be retrieved by calling:</span><span class="sxs-lookup"><span data-stu-id="1e16a-172">Available metric definitions can be retrieved by calling:</span></span>

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

<span data-ttu-id="1e16a-173">Queries to retrieve individual metrics use the following format:</span><span class="sxs-lookup"><span data-stu-id="1e16a-173">Queries to retrieve individual metrics use the following format:</span></span>

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

<span data-ttu-id="1e16a-174">For more information, see [Retrieving Resource Metrics via the Azure Monitor REST API](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/).</span><span class="sxs-lookup"><span data-stu-id="1e16a-174">For more information, see [Retrieving Resource Metrics via the Azure Monitor REST API](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/).</span></span> <span data-ttu-id="1e16a-175">Note that "Azure Inights" was renamed "Azure Monitor".</span><span class="sxs-lookup"><span data-stu-id="1e16a-175">Note that "Azure Inights" was renamed "Azure Monitor".</span></span>  <span data-ttu-id="1e16a-176">This blog entry refers to the older name.</span><span class="sxs-lookup"><span data-stu-id="1e16a-176">This blog entry refers to the older name.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1e16a-177">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="1e16a-177">Troubleshooting</span></span>
<span data-ttu-id="1e16a-178">If your monitoring tiles display the **No data available** message, and you recently made requests or added data to the database, you can edit the tile to reflect the recent usage.</span><span class="sxs-lookup"><span data-stu-id="1e16a-178">If your monitoring tiles display the **No data available** message, and you recently made requests or added data to the database, you can edit the tile to reflect the recent usage.</span></span>

### <a name="edit-a-tile-to-refresh-current-data"></a><span data-ttu-id="1e16a-179">Edit a tile to refresh current data</span><span class="sxs-lookup"><span data-stu-id="1e16a-179">Edit a tile to refresh current data</span></span>
1. <span data-ttu-id="1e16a-180">To customize the metrics that display in a particular part, click the chart to open the **Metric** blade, and then click **Edit Chart**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-180">To customize the metrics that display in a particular part, click the chart to open the **Metric** blade, and then click **Edit Chart**.</span></span>  
   <span data-ttu-id="1e16a-181">![Screen shot of the Metric blade controls, with Edit chart highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb3.png)</span><span class="sxs-lookup"><span data-stu-id="1e16a-181">![Screen shot of the Metric blade controls, with Edit chart highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/madocdb3.png)</span></span>
2. <span data-ttu-id="1e16a-182">On the **Edit Chart** blade, in the **Time Range** section, click **past hour**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e16a-182">On the **Edit Chart** blade, in the **Time Range** section, click **past hour**, and then click **OK**.</span></span>  
   <span data-ttu-id="1e16a-183">![Screen shot of the Edit Chart blade with past hour selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/documentdb-no-available-data-past-hour.png)</span><span class="sxs-lookup"><span data-stu-id="1e16a-183">![Screen shot of the Edit Chart blade with past hour selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/documentdb-no-available-data-past-hour.png)</span></span>
3. <span data-ttu-id="1e16a-184">Your tile should now refresh showing your current data and usage.</span><span class="sxs-lookup"><span data-stu-id="1e16a-184">Your tile should now refresh showing your current data and usage.</span></span>  
   ![Screen shot of the updated Total requests past hour tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a><span data-ttu-id="1e16a-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e16a-186">Next steps</span></span>
<span data-ttu-id="1e16a-187">To learn more about DocumentDB capacity planning, see the [DocumentDB capacity planner calculator](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="1e16a-187">To learn more about DocumentDB capacity planning, see the [DocumentDB capacity planner calculator](https://www.documentdb.com/capacityplanner).</span></span>















