---
title: Azure Monitor Overview
description: Azure Monitor collects stats for use in alerts, webhooks, autoscale, and automation. Article also list other Microsoft monitoring options.
author: rboucher
services: azure-monitor
ms.service: azure-monitor
ms.topic: overview
ms.date: 03/28/2018
ms.author: robb
ms.custom: mvc
ms.component: ''
ms.openlocfilehash: a96991c424b4709002d46b6b7abe1e884c3605dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966967"
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="07f54-104">Overview of Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="07f54-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="07f54-105">This article provides an overview of the Azure Monitor service in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="07f54-105">This article provides an overview of the Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="07f54-106">It discusses what Azure Monitor does and provides pointers to additional information on how to use Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="07f54-106">It discusses what Azure Monitor does and provides pointers to additional information on how to use Azure Monitor.</span></span>  <span data-ttu-id="07f54-107">If you prefer a video introduction, see Next steps links at the bottom of this article.</span><span class="sxs-lookup"><span data-stu-id="07f54-107">If you prefer a video introduction, see Next steps links at the bottom of this article.</span></span> 

## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="07f54-108">Azure Monitor and Microsoft's other monitoring products</span><span class="sxs-lookup"><span data-stu-id="07f54-108">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="07f54-109">Azure Monitor provides base-level infrastructure metrics and logs for most services in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="07f54-109">Azure Monitor provides base-level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="07f54-110">Azure services that do not yet put their data into Azure Monitor will put it there in the future.</span><span class="sxs-lookup"><span data-stu-id="07f54-110">Azure services that do not yet put their data into Azure Monitor will put it there in the future.</span></span>

<span data-ttu-id="07f54-111">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span><span class="sxs-lookup"><span data-stu-id="07f54-111">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="07f54-112">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07f54-112">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="portal-overview-page"></a><span data-ttu-id="07f54-113">Portal overview page</span><span class="sxs-lookup"><span data-stu-id="07f54-113">Portal overview page</span></span>

<span data-ttu-id="07f54-114">Azure Monitor has a landing page that helps users:</span><span class="sxs-lookup"><span data-stu-id="07f54-114">Azure Monitor has a landing page that helps users:</span></span> 
- <span data-ttu-id="07f54-115">Understand the monitoring capabilities offered by Azure.</span><span class="sxs-lookup"><span data-stu-id="07f54-115">Understand the monitoring capabilities offered by Azure.</span></span>
- <span data-ttu-id="07f54-116">Discover, configure, and on-board Azure’s platform and premium monitoring capabilities.</span><span class="sxs-lookup"><span data-stu-id="07f54-116">Discover, configure, and on-board Azure’s platform and premium monitoring capabilities.</span></span>

<span data-ttu-id="07f54-117">The page is a starting point for navigation, including on-boarding.</span><span class="sxs-lookup"><span data-stu-id="07f54-117">The page is a starting point for navigation, including on-boarding.</span></span> <span data-ttu-id="07f54-118">It shows curated notable issues from different services and allows the user to navigate to them in context.</span><span class="sxs-lookup"><span data-stu-id="07f54-118">It shows curated notable issues from different services and allows the user to navigate to them in context.</span></span>
 
![Model for monitoring and diagnostics for non-compute resources](./media/monitoring-overview-azure-monitor/monitor-overview-ux2.png)

<span data-ttu-id="07f54-120">When you open the page, you can select among the subscriptions you have read access to.</span><span class="sxs-lookup"><span data-stu-id="07f54-120">When you open the page, you can select among the subscriptions you have read access to.</span></span> <span data-ttu-id="07f54-121">For a selected subscription, you can see:</span><span class="sxs-lookup"><span data-stu-id="07f54-121">For a selected subscription, you can see:</span></span>

- <span data-ttu-id="07f54-122">**Triggered alerts and alert sources** - This table shows summary counts, alert sources, and how many times alerts fired for the selected time duration.</span><span class="sxs-lookup"><span data-stu-id="07f54-122">**Triggered alerts and alert sources** - This table shows summary counts, alert sources, and how many times alerts fired for the selected time duration.</span></span> <span data-ttu-id="07f54-123">It applies to both older and newer alerts.</span><span class="sxs-lookup"><span data-stu-id="07f54-123">It applies to both older and newer alerts.</span></span> <span data-ttu-id="07f54-124">Read more about the [newer Azure Alerts](monitoring-overview-unified-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="07f54-124">Read more about the [newer Azure Alerts](monitoring-overview-unified-alerts.md).</span></span> 
- <span data-ttu-id="07f54-125">**Activity Log Errors** - If any of your Azure resources log events with error-level severity, you can view a high-level count and click through to the activity log page to investigate each event.</span><span class="sxs-lookup"><span data-stu-id="07f54-125">**Activity Log Errors** - If any of your Azure resources log events with error-level severity, you can view a high-level count and click through to the activity log page to investigate each event.</span></span>
- <span data-ttu-id="07f54-126">**Azure Service Health** - You can see a count of Service Health service issues, planned maintenance events, and health advisories.</span><span class="sxs-lookup"><span data-stu-id="07f54-126">**Azure Service Health** - You can see a count of Service Health service issues, planned maintenance events, and health advisories.</span></span> <span data-ttu-id="07f54-127">Azure Service Health provides personalized information when problems in the Azure infrastructure impact your services.</span><span class="sxs-lookup"><span data-stu-id="07f54-127">Azure Service Health provides personalized information when problems in the Azure infrastructure impact your services.</span></span>  <span data-ttu-id="07f54-128">See [Azure Service Health](../service-health/service-health-overview.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="07f54-128">See [Azure Service Health](../service-health/service-health-overview.md) for more information.</span></span>  
- <span data-ttu-id="07f54-129">**Application Insights** - See KPIs for each AppInsights resource in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="07f54-129">**Application Insights** - See KPIs for each AppInsights resource in the current subscription.</span></span> <span data-ttu-id="07f54-130">The KPIs are optimized for server-side application monitoring across ASP.NET web apps, Java, Node, and General application types.</span><span class="sxs-lookup"><span data-stu-id="07f54-130">The KPIs are optimized for server-side application monitoring across ASP.NET web apps, Java, Node, and General application types.</span></span> <span data-ttu-id="07f54-131">The KPIs include metrics for request rate, response duration, failure rate, and availability %.</span><span class="sxs-lookup"><span data-stu-id="07f54-131">The KPIs include metrics for request rate, response duration, failure rate, and availability %.</span></span> 

<span data-ttu-id="07f54-132">If you have not on-boarded to Log Analytics or Application Insights, or if you have not configured any Azure Alerts in the current subscription, the page provides links to begin your on-boarding process.</span><span class="sxs-lookup"><span data-stu-id="07f54-132">If you have not on-boarded to Log Analytics or Application Insights, or if you have not configured any Azure Alerts in the current subscription, the page provides links to begin your on-boarding process.</span></span>



## <a name="azure-monitor-sources---compute-subset"></a><span data-ttu-id="07f54-133">Azure Monitor Sources - Compute subset</span><span class="sxs-lookup"><span data-stu-id="07f54-133">Azure Monitor Sources - Compute subset</span></span>

![Model for monitoring and diagnostics for non-compute resources](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)


<span data-ttu-id="07f54-135">The Compute services here include</span><span class="sxs-lookup"><span data-stu-id="07f54-135">The Compute services here include</span></span> 
- <span data-ttu-id="07f54-136">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="07f54-136">Cloud Services</span></span> 
- <span data-ttu-id="07f54-137">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07f54-137">Virtual Machines</span></span> 
- <span data-ttu-id="07f54-138">Virtual Machine scale sets</span><span class="sxs-lookup"><span data-stu-id="07f54-138">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="07f54-139">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07f54-139">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="07f54-140">Application - Diagnostics Logs, Application Logs, and Metrics</span><span class="sxs-lookup"><span data-stu-id="07f54-140">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="07f54-141">Applications can run on top of the Guest OS in the compute model.</span><span class="sxs-lookup"><span data-stu-id="07f54-141">Applications can run on top of the Guest OS in the compute model.</span></span> <span data-ttu-id="07f54-142">They emit their own set of logs and metrics.</span><span class="sxs-lookup"><span data-stu-id="07f54-142">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="07f54-143">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span><span class="sxs-lookup"><span data-stu-id="07f54-143">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="07f54-144">The types include</span><span class="sxs-lookup"><span data-stu-id="07f54-144">The types include</span></span>

* <span data-ttu-id="07f54-145">Performance counters</span><span class="sxs-lookup"><span data-stu-id="07f54-145">Performance counters</span></span>
* <span data-ttu-id="07f54-146">Application Logs</span><span class="sxs-lookup"><span data-stu-id="07f54-146">Application Logs</span></span>
* <span data-ttu-id="07f54-147">Windows Event Logs</span><span class="sxs-lookup"><span data-stu-id="07f54-147">Windows Event Logs</span></span>
* <span data-ttu-id="07f54-148">.NET Event Source</span><span class="sxs-lookup"><span data-stu-id="07f54-148">.NET Event Source</span></span>
* <span data-ttu-id="07f54-149">IIS Logs</span><span class="sxs-lookup"><span data-stu-id="07f54-149">IIS Logs</span></span>
* <span data-ttu-id="07f54-150">Manifest based ETW</span><span class="sxs-lookup"><span data-stu-id="07f54-150">Manifest based ETW</span></span>
* <span data-ttu-id="07f54-151">Crash Dumps</span><span class="sxs-lookup"><span data-stu-id="07f54-151">Crash Dumps</span></span>
* <span data-ttu-id="07f54-152">Customer Error Logs</span><span class="sxs-lookup"><span data-stu-id="07f54-152">Customer Error Logs</span></span>

<span data-ttu-id="07f54-153">Without the diagnostics extension, only a few metrics like CPU usage are available.</span><span class="sxs-lookup"><span data-stu-id="07f54-153">Without the diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="07f54-154">Host and Guest VM metrics</span><span class="sxs-lookup"><span data-stu-id="07f54-154">Host and Guest VM metrics</span></span>
<span data-ttu-id="07f54-155">The previously listed compute resources have a dedicated host VM and guest OS they interact with.</span><span class="sxs-lookup"><span data-stu-id="07f54-155">The previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="07f54-156">The host VM and guest OS are the equivalent of root VM and guest VM in the Hyper-V hypervisor model.</span><span class="sxs-lookup"><span data-stu-id="07f54-156">The host VM and guest OS are the equivalent of root VM and guest VM in the Hyper-V hypervisor model.</span></span> <span data-ttu-id="07f54-157">You can collect metrics on both.</span><span class="sxs-lookup"><span data-stu-id="07f54-157">You can collect metrics on both.</span></span> <span data-ttu-id="07f54-158">You can also collect diagnostics logs on the guest OS.</span><span class="sxs-lookup"><span data-stu-id="07f54-158">You can also collect diagnostics logs on the guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="07f54-159">Activity Log</span><span class="sxs-lookup"><span data-stu-id="07f54-159">Activity Log</span></span>
<span data-ttu-id="07f54-160">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="07f54-160">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> <span data-ttu-id="07f54-161">The log contains information such as times when resources are created or destroyed.</span><span class="sxs-lookup"><span data-stu-id="07f54-161">The log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="07f54-162">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="07f54-162">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="azure-monitor-sources---everything-else"></a><span data-ttu-id="07f54-163">Azure Monitor Sources - everything else</span><span class="sxs-lookup"><span data-stu-id="07f54-163">Azure Monitor Sources - everything else</span></span>

![Model for monitoring and diagnostics for compute resources](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="07f54-165">Resource - Metrics and Diagnostics Logs</span><span class="sxs-lookup"><span data-stu-id="07f54-165">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="07f54-166">Collectable metrics and diagnostics logs vary based on the resource type.</span><span class="sxs-lookup"><span data-stu-id="07f54-166">Collectable metrics and diagnostics logs vary based on the resource type.</span></span> <span data-ttu-id="07f54-167">For example, Web Apps provides statistics on the Disk IO and Percent CPU.</span><span class="sxs-lookup"><span data-stu-id="07f54-167">For example, Web Apps provides statistics on the Disk IO and Percent CPU.</span></span> <span data-ttu-id="07f54-168">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span><span class="sxs-lookup"><span data-stu-id="07f54-168">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="07f54-169">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="07f54-169">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="07f54-170">Host and Guest VM metrics</span><span class="sxs-lookup"><span data-stu-id="07f54-170">Host and Guest VM metrics</span></span>
<span data-ttu-id="07f54-171">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span><span class="sxs-lookup"><span data-stu-id="07f54-171">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="07f54-172">Activity Log</span><span class="sxs-lookup"><span data-stu-id="07f54-172">Activity Log</span></span>
<span data-ttu-id="07f54-173">The activity log is the same as for compute resources.</span><span class="sxs-lookup"><span data-stu-id="07f54-173">The activity log is the same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="07f54-174">Uses for Monitoring Data</span><span class="sxs-lookup"><span data-stu-id="07f54-174">Uses for Monitoring Data</span></span>
<span data-ttu-id="07f54-175">Once you collect your data, you can do the following with it in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="07f54-175">Once you collect your data, you can do the following with it in Azure Monitor.</span></span>

### <a name="route"></a><span data-ttu-id="07f54-176">Route</span><span class="sxs-lookup"><span data-stu-id="07f54-176">Route</span></span>
<span data-ttu-id="07f54-177">You can stream monitoring data to other locations.</span><span class="sxs-lookup"><span data-stu-id="07f54-177">You can stream monitoring data to other locations.</span></span> 

<span data-ttu-id="07f54-178">Examples include:</span><span class="sxs-lookup"><span data-stu-id="07f54-178">Examples include:</span></span>

- <span data-ttu-id="07f54-179">Send to Application Insights so you can use its richer visualization and analysis tools.</span><span class="sxs-lookup"><span data-stu-id="07f54-179">Send to Application Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="07f54-180">Send to Event Hubs so you can route to third-party tools.</span><span class="sxs-lookup"><span data-stu-id="07f54-180">Send to Event Hubs so you can route to third-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="07f54-181">Store and Archive</span><span class="sxs-lookup"><span data-stu-id="07f54-181">Store and Archive</span></span>
<span data-ttu-id="07f54-182">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span><span class="sxs-lookup"><span data-stu-id="07f54-182">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="07f54-183">Metrics are stored for 90 days.</span><span class="sxs-lookup"><span data-stu-id="07f54-183">Metrics are stored for 90 days.</span></span> 
- <span data-ttu-id="07f54-184">Activity log entries are stored for 90 days.</span><span class="sxs-lookup"><span data-stu-id="07f54-184">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="07f54-185">Diagnostics logs are not stored at all.</span><span class="sxs-lookup"><span data-stu-id="07f54-185">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="07f54-186">If you want to store data longer than the time periods listed above, you can use an Azure storage.</span><span class="sxs-lookup"><span data-stu-id="07f54-186">If you want to store data longer than the time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="07f54-187">Monitoring data is kept in your storage account based on a retention policy you set.</span><span class="sxs-lookup"><span data-stu-id="07f54-187">Monitoring data is kept in your storage account based on a retention policy you set.</span></span> <span data-ttu-id="07f54-188">You do have to pay for the space the data takes up in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="07f54-188">You do have to pay for the space the data takes up in Azure storage.</span></span> 

<span data-ttu-id="07f54-189">A few ways to use this data:</span><span class="sxs-lookup"><span data-stu-id="07f54-189">A few ways to use this data:</span></span>

- <span data-ttu-id="07f54-190">Once written, you can have other tools within or outside of Azure read it and process it.</span><span class="sxs-lookup"><span data-stu-id="07f54-190">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="07f54-191">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="07f54-191">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span></span>  
- <span data-ttu-id="07f54-192">You leave the data in Azure storage indefinitely for archive purposes.</span><span class="sxs-lookup"><span data-stu-id="07f54-192">You leave the data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="07f54-193">Query</span><span class="sxs-lookup"><span data-stu-id="07f54-193">Query</span></span>
<span data-ttu-id="07f54-194">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span><span class="sxs-lookup"><span data-stu-id="07f54-194">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span></span>

<span data-ttu-id="07f54-195">Examples include:</span><span class="sxs-lookup"><span data-stu-id="07f54-195">Examples include:</span></span>

* <span data-ttu-id="07f54-196">Getting data for a custom monitoring application you have written</span><span class="sxs-lookup"><span data-stu-id="07f54-196">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="07f54-197">Creating custom queries and sending that data to a third-party application.</span><span class="sxs-lookup"><span data-stu-id="07f54-197">Creating custom queries and sending that data to a third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="07f54-198">Visualize</span><span class="sxs-lookup"><span data-stu-id="07f54-198">Visualize</span></span>
<span data-ttu-id="07f54-199">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span><span class="sxs-lookup"><span data-stu-id="07f54-199">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span></span>  

<span data-ttu-id="07f54-200">A few visualization methods include:</span><span class="sxs-lookup"><span data-stu-id="07f54-200">A few visualization methods include:</span></span>

* <span data-ttu-id="07f54-201">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="07f54-201">Use the Azure portal</span></span>
* <span data-ttu-id="07f54-202">Route data to Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="07f54-202">Route data to Azure Application Insights</span></span>
* <span data-ttu-id="07f54-203">Route data to Microsoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="07f54-203">Route data to Microsoft PowerBI</span></span>
* <span data-ttu-id="07f54-204">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span><span class="sxs-lookup"><span data-stu-id="07f54-204">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="07f54-205">Automate</span><span class="sxs-lookup"><span data-stu-id="07f54-205">Automate</span></span>
> [!NOTE]
> <span data-ttu-id="07f54-206">As part of the ongoing evolution of alerts on Microsoft Azure, now a unified experience for alerting is available.</span><span class="sxs-lookup"><span data-stu-id="07f54-206">As part of the ongoing evolution of alerts on Microsoft Azure, now a unified experience for alerting is available.</span></span> <span data-ttu-id="07f54-207">More details on [new Azure alerts](monitoring-overview-unified-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="07f54-207">More details on [new Azure alerts](monitoring-overview-unified-alerts.md)</span></span>

<span data-ttu-id="07f54-208">In the Azure alerts, you can use monitoring data to trigger alerts or even whole processes.</span><span class="sxs-lookup"><span data-stu-id="07f54-208">In the Azure alerts, you can use monitoring data to trigger alerts or even whole processes.</span></span> <span data-ttu-id="07f54-209">Examples include:</span><span class="sxs-lookup"><span data-stu-id="07f54-209">Examples include:</span></span>

* <span data-ttu-id="07f54-210">Use data to autoscale compute instances up or down based on application load.</span><span class="sxs-lookup"><span data-stu-id="07f54-210">Use data to autoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="07f54-211">Send emails based on metric or log conditions.</span><span class="sxs-lookup"><span data-stu-id="07f54-211">Send emails based on metric or log conditions.</span></span> 
* <span data-ttu-id="07f54-212">Call a web URL (webhook) to execute an action in a system outside of Azure</span><span class="sxs-lookup"><span data-stu-id="07f54-212">Call a web URL (webhook) to execute an action in a system outside of Azure</span></span>
* <span data-ttu-id="07f54-213">Start a runbook in Azure automation to perform any variety of tasks</span><span class="sxs-lookup"><span data-stu-id="07f54-213">Start a runbook in Azure automation to perform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="07f54-214">Methods of accessing Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="07f54-214">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="07f54-215">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span><span class="sxs-lookup"><span data-stu-id="07f54-215">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span></span> <span data-ttu-id="07f54-216">Not all methods are available for all actions or data types.</span><span class="sxs-lookup"><span data-stu-id="07f54-216">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="07f54-217">Azure portal</span><span class="sxs-lookup"><span data-stu-id="07f54-217">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="07f54-218">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07f54-218">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="07f54-219">Cross-platform Command Line Interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="07f54-219">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="07f54-220">REST API</span><span class="sxs-lookup"><span data-stu-id="07f54-220">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="07f54-221">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="07f54-221">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="07f54-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="07f54-222">Next steps</span></span>
<span data-ttu-id="07f54-223">Learn more about</span><span class="sxs-lookup"><span data-stu-id="07f54-223">Learn more about</span></span>
- <span data-ttu-id="07f54-224">A video walkthrough of just Azure Monitor is available at</span><span class="sxs-lookup"><span data-stu-id="07f54-224">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="07f54-225">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="07f54-225">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> 
- <span data-ttu-id="07f54-226">A video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977).</span><span class="sxs-lookup"><span data-stu-id="07f54-226">A video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977).</span></span>
- <span data-ttu-id="07f54-227">Run through the Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="07f54-227">Run through the Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="07f54-228">Set up the [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="07f54-228">Set up the [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="07f54-229">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span><span class="sxs-lookup"><span data-stu-id="07f54-229">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="07f54-230">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span><span class="sxs-lookup"><span data-stu-id="07f54-230">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- [<span data-ttu-id="07f54-231">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="07f54-231">Log Analytics</span></span>](https://azure.microsoft.com/documentation/services/log-analytics/)
