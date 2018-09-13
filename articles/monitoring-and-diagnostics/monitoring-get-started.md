---
title: Get started with Azure Monitor | Microsoft Docs
description: Get started using Azure Monitor to gain insight into the operation of your resources and take action based off of data.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: e1c93a20026e5f6e4b6df6a87d7d0c158fdad302
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556532"
---
# <a name="get-started-with-azure-monitor"></a><span data-ttu-id="245de-103">Get started with Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="245de-103">Get started with Azure Monitor</span></span>
<span data-ttu-id="245de-104">Azure Monitor is the platform service that provides a single source for monitoring Azure resources.</span><span class="sxs-lookup"><span data-stu-id="245de-104">Azure Monitor is the platform service that provides a single source for monitoring Azure resources.</span></span> <span data-ttu-id="245de-105">With Azure Monitor, you can visualize, query, route, archive, and take action on the metrics and logs coming from resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="245de-105">With Azure Monitor, you can visualize, query, route, archive, and take action on the metrics and logs coming from resources in Azure.</span></span> <span data-ttu-id="245de-106">You can work with this data using the Monitor portal blade, [Monitor PowerShell Cmdlets](insights-powershell-samples.md), [Cross-Platform CLI](insights-cli-samples.md), or [Azure Monitor REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="245de-106">You can work with this data using the Monitor portal blade, [Monitor PowerShell Cmdlets](insights-powershell-samples.md), [Cross-Platform CLI](insights-cli-samples.md), or [Azure Monitor REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span> <span data-ttu-id="245de-107">In this article, we walk through a few of the key components of Azure Monitor, using the portal for demonstration.</span><span class="sxs-lookup"><span data-stu-id="245de-107">In this article, we walk through a few of the key components of Azure Monitor, using the portal for demonstration.</span></span>

1. <span data-ttu-id="245de-108">In the portal, navigate to **More services** and find the **Monitor** option.</span><span class="sxs-lookup"><span data-stu-id="245de-108">In the portal, navigate to **More services** and find the **Monitor** option.</span></span> <span data-ttu-id="245de-109">Click the star icon to add this option to your favorites list so that it is always easily accessible from the left-hand navigation bar.</span><span class="sxs-lookup"><span data-stu-id="245de-109">Click the star icon to add this option to your favorites list so that it is always easily accessible from the left-hand navigation bar.</span></span>
   
    ![Monitor in the services list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-more-services.png)
2. <span data-ttu-id="245de-111">Click the **Monitor** option to open up the **Monitor** blade.</span><span class="sxs-lookup"><span data-stu-id="245de-111">Click the **Monitor** option to open up the **Monitor** blade.</span></span> <span data-ttu-id="245de-112">This blade brings together all your monitoring settings and data into one consolidated view.</span><span class="sxs-lookup"><span data-stu-id="245de-112">This blade brings together all your monitoring settings and data into one consolidated view.</span></span> <span data-ttu-id="245de-113">It first opens to the **Activity log** section.</span><span class="sxs-lookup"><span data-stu-id="245de-113">It first opens to the **Activity log** section.</span></span>
   
    ![Monitor blade navigation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-blade-nav.png)
   
    <span data-ttu-id="245de-115">Azure Monitor has three basic categories of monitoring data: The **activity log**, **metrics**, and **diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="245de-115">Azure Monitor has three basic categories of monitoring data: The **activity log**, **metrics**, and **diagnostic logs**.</span></span>
3. <span data-ttu-id="245de-116">Click **Activity log** to ensure that the activity log section is displayed.</span><span class="sxs-lookup"><span data-stu-id="245de-116">Click **Activity log** to ensure that the activity log section is displayed.</span></span>
   
    ![Activity Log blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-act-log-blade.png)
   
    <span data-ttu-id="245de-118">The [**activity log**](monitoring-overview-activity-logs.md) describes all operations performed on resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="245de-118">The [**activity log**](monitoring-overview-activity-logs.md) describes all operations performed on resources in your subscription.</span></span> <span data-ttu-id="245de-119">Using the Activity Log, you can determine the ‘what, who, and when’ for any create, update, or delete operations on resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="245de-119">Using the Activity Log, you can determine the ‘what, who, and when’ for any create, update, or delete operations on resources in your subscription.</span></span> <span data-ttu-id="245de-120">For example, the Activity Log tells you when a web app was stopped and who stopped it.</span><span class="sxs-lookup"><span data-stu-id="245de-120">For example, the Activity Log tells you when a web app was stopped and who stopped it.</span></span> <span data-ttu-id="245de-121">Activity Log events are stored in the platform and available to query for 90 days.</span><span class="sxs-lookup"><span data-stu-id="245de-121">Activity Log events are stored in the platform and available to query for 90 days.</span></span>
   
    <span data-ttu-id="245de-122">You can create and save queries for common filters, then pin the most important queries to a portal dashboard so you'll always know if events that meet your criteria have occurred.</span><span class="sxs-lookup"><span data-stu-id="245de-122">You can create and save queries for common filters, then pin the most important queries to a portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>
4. <span data-ttu-id="245de-123">Filter the view to a particular resource group over the last week, then click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="245de-123">Filter the view to a particular resource group over the last week, then click the **Save** button.</span></span>
   
    ![Save activity log query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-act-log-save.png)
5. <span data-ttu-id="245de-125">Now, click the **Pin** button.</span><span class="sxs-lookup"><span data-stu-id="245de-125">Now, click the **Pin** button.</span></span>
   
    ![Click pin for activity log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-act-log-pin.png)
   
    <span data-ttu-id="245de-127">Most of the views in this walkthrough can be pinned to a dashboard.</span><span class="sxs-lookup"><span data-stu-id="245de-127">Most of the views in this walkthrough can be pinned to a dashboard.</span></span> <span data-ttu-id="245de-128">This helps you create a single source of information for operational data on your services.</span><span class="sxs-lookup"><span data-stu-id="245de-128">This helps you create a single source of information for operational data on your services.</span></span> 
6. <span data-ttu-id="245de-129">Return to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="245de-129">Return to your dashboard.</span></span> <span data-ttu-id="245de-130">You can now see that the query (and number of results) is displayed in your dashboard.</span><span class="sxs-lookup"><span data-stu-id="245de-130">You can now see that the query (and number of results) is displayed in your dashboard.</span></span> <span data-ttu-id="245de-131">This is useful if you want to quickly see any high-profile actions that have occurred recently in your subscription, eg.</span><span class="sxs-lookup"><span data-stu-id="245de-131">This is useful if you want to quickly see any high-profile actions that have occurred recently in your subscription, eg.</span></span> <span data-ttu-id="245de-132">a new role was assigned or a VM was deleted.</span><span class="sxs-lookup"><span data-stu-id="245de-132">a new role was assigned or a VM was deleted.</span></span>
   
    ![Activity log pinned to dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-act-log-db.png)
7. <span data-ttu-id="245de-134">Return to the **Monitor** tile and click the **Metrics** section.</span><span class="sxs-lookup"><span data-stu-id="245de-134">Return to the **Monitor** tile and click the **Metrics** section.</span></span> <span data-ttu-id="245de-135">You first need to select a resource by filtering and selecting using the drop down options at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="245de-135">You first need to select a resource by filtering and selecting using the drop down options at the top of the blade.</span></span>
   
    ![Filter resource for metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-met-filter.png)
   
    <span data-ttu-id="245de-137">All Azure resources emit [**metrics**](monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="245de-137">All Azure resources emit [**metrics**](monitoring-overview-metrics.md).</span></span> <span data-ttu-id="245de-138">This view brings together all metrics in a single pane of glass so you can easily understand how your resources are performing.</span><span class="sxs-lookup"><span data-stu-id="245de-138">This view brings together all metrics in a single pane of glass so you can easily understand how your resources are performing.</span></span>
8. <span data-ttu-id="245de-139">Once you have selected a resource, all available metrics appear on the left side of the blade.</span><span class="sxs-lookup"><span data-stu-id="245de-139">Once you have selected a resource, all available metrics appear on the left side of the blade.</span></span> <span data-ttu-id="245de-140">You can chart multiple metrics at once by selecting metrics and modify the graph type and time range.</span><span class="sxs-lookup"><span data-stu-id="245de-140">You can chart multiple metrics at once by selecting metrics and modify the graph type and time range.</span></span> <span data-ttu-id="245de-141">You can also view all metric alerts set on this resource.</span><span class="sxs-lookup"><span data-stu-id="245de-141">You can also view all metric alerts set on this resource.</span></span>
   
    ![Metric blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > <span data-ttu-id="245de-143">Some metrics are only available by enabling [Application Insights](../application-insights/app-insights-overview.md) and/or Windows or Linux Azure Diagnostics on your resource.</span><span class="sxs-lookup"><span data-stu-id="245de-143">Some metrics are only available by enabling [Application Insights](../application-insights/app-insights-overview.md) and/or Windows or Linux Azure Diagnostics on your resource.</span></span>
   > 
   > 
9. <span data-ttu-id="245de-144">When you are happy with your chart, you can use the **Pin** button to pin it to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="245de-144">When you are happy with your chart, you can use the **Pin** button to pin it to your dashboard.</span></span>
10. <span data-ttu-id="245de-145">Return to the **Monitor** blade and click **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="245de-145">Return to the **Monitor** blade and click **Diagnostic logs**.</span></span>
    
    ![Diagnostic logs blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    <span data-ttu-id="245de-147">[**Diagnostic logs**](monitoring-overview-of-diagnostic-logs.md) are logs emitted *by* a resource that provide data about the operation of that particular resource.</span><span class="sxs-lookup"><span data-stu-id="245de-147">[**Diagnostic logs**](monitoring-overview-of-diagnostic-logs.md) are logs emitted *by* a resource that provide data about the operation of that particular resource.</span></span> <span data-ttu-id="245de-148">For example, Network Security Group Rule Counters and Logic App Workflow Logs are both types of diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="245de-148">For example, Network Security Group Rule Counters and Logic App Workflow Logs are both types of diagnostic logs.</span></span> <span data-ttu-id="245de-149">These logs can be stored in a storage account, streamed to an Event Hub, and/or sent to [Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="245de-149">These logs can be stored in a storage account, streamed to an Event Hub, and/or sent to [Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="245de-150">Log Analytics is Microsoft's operational intelligence product for advanced searching and alerting.</span><span class="sxs-lookup"><span data-stu-id="245de-150">Log Analytics is Microsoft's operational intelligence product for advanced searching and alerting.</span></span>
    
    <span data-ttu-id="245de-151">In the portal you can view and filter a list of all resources in your subscription to identify if they have diagnostic logs enabled.</span><span class="sxs-lookup"><span data-stu-id="245de-151">In the portal you can view and filter a list of all resources in your subscription to identify if they have diagnostic logs enabled.</span></span>
11. <span data-ttu-id="245de-152">Click a resource in the diagnostic logs blade.</span><span class="sxs-lookup"><span data-stu-id="245de-152">Click a resource in the diagnostic logs blade.</span></span> <span data-ttu-id="245de-153">If diagnostic logs are being stored in a storage account, you will see a list of hourly logs that you can directly download.</span><span class="sxs-lookup"><span data-stu-id="245de-153">If diagnostic logs are being stored in a storage account, you will see a list of hourly logs that you can directly download.</span></span>
    
    ![Diagnostic logs for one resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    <span data-ttu-id="245de-155">You can also click **Diagnostic Settings**, which allows you to set up or modify your settings for archival to a storage account, streaming to Event Hubs, or sending to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="245de-155">You can also click **Diagnostic Settings**, which allows you to set up or modify your settings for archival to a storage account, streaming to Event Hubs, or sending to a Log Analytics workspace.</span></span>
    
    ![Enable diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    <span data-ttu-id="245de-157">If you have set up diagnostic logs to Log Analytics, you can then search them in the **Log search** section of the portal.</span><span class="sxs-lookup"><span data-stu-id="245de-157">If you have set up diagnostic logs to Log Analytics, you can then search them in the **Log search** section of the portal.</span></span>
12. <span data-ttu-id="245de-158">Navigate to the **Alerts** section of the Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="245de-158">Navigate to the **Alerts** section of the Monitor blade.</span></span>
    
    ![alerts blade for public](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-alerts-nopp.png)
    
    <span data-ttu-id="245de-160">Here you can manage all [**alerts**](monitoring-overview-alerts.md) on your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="245de-160">Here you can manage all [**alerts**](monitoring-overview-alerts.md) on your Azure resources.</span></span> <span data-ttu-id="245de-161">This includes alerts on metrics, activity log events, Application Insights web tests (Locations), and Application Insights proactive diagnostics.</span><span class="sxs-lookup"><span data-stu-id="245de-161">This includes alerts on metrics, activity log events, Application Insights web tests (Locations), and Application Insights proactive diagnostics.</span></span> <span data-ttu-id="245de-162">Alerts can trigger an email to be sent or an HTTP POST to a webhook URL.</span><span class="sxs-lookup"><span data-stu-id="245de-162">Alerts can trigger an email to be sent or an HTTP POST to a webhook URL.</span></span>
13. <span data-ttu-id="245de-163">Click **Add metric alert** to create an alert.</span><span class="sxs-lookup"><span data-stu-id="245de-163">Click **Add metric alert** to create an alert.</span></span>
    
    ![add metric alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-alerts-add.png)
    
    <span data-ttu-id="245de-165">You can then pin an alert to your dashboard to easily see its state at any time.</span><span class="sxs-lookup"><span data-stu-id="245de-165">You can then pin an alert to your dashboard to easily see its state at any time.</span></span>
14. <span data-ttu-id="245de-166">The Monitor section also includes links to [Application Insights](../application-insights/app-insights-overview.md) applications and [Log Analytics](../log-analytics/log-analytics-overview.md) management solutions.</span><span class="sxs-lookup"><span data-stu-id="245de-166">The Monitor section also includes links to [Application Insights](../application-insights/app-insights-overview.md) applications and [Log Analytics](../log-analytics/log-analytics-overview.md) management solutions.</span></span> <span data-ttu-id="245de-167">These other Microsoft products have deep integration with Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="245de-167">These other Microsoft products have deep integration with Azure Monitor.</span></span>
15. <span data-ttu-id="245de-168">If you are not using Application Insights or Log Analytics, chances are that Azure Monitor has a partnership with your current monitoring, logging, and alerting products.</span><span class="sxs-lookup"><span data-stu-id="245de-168">If you are not using Application Insights or Log Analytics, chances are that Azure Monitor has a partnership with your current monitoring, logging, and alerting products.</span></span> <span data-ttu-id="245de-169">See our [partners page](monitoring-partners.md) for a full list and instructions for how to integrate.</span><span class="sxs-lookup"><span data-stu-id="245de-169">See our [partners page](monitoring-partners.md) for a full list and instructions for how to integrate.</span></span>

<span data-ttu-id="245de-170">By following these steps and pinning all relevant tiles to a dashboard, you can create comprehensive views of your application and infrastructure like this one:</span><span class="sxs-lookup"><span data-stu-id="245de-170">By following these steps and pinning all relevant tiles to a dashboard, you can create comprehensive views of your application and infrastructure like this one:</span></span>

![Azure Monitor dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a><span data-ttu-id="245de-172">Next Steps</span><span class="sxs-lookup"><span data-stu-id="245de-172">Next Steps</span></span>
* <span data-ttu-id="245de-173">Read the [Overview of Azure Monitor](monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="245de-173">Read the [Overview of Azure Monitor](monitoring-overview.md)</span></span>















