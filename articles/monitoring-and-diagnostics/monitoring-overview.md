---
title: Azure Monitor Overview | Microsoft Docs
description: Azure Monitor collects stats for use in alerts, webhooks, autoscale, and automation. Article also list other Microsoft monitoring options.
author: rboucher
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: robb
ms.openlocfilehash: eb4db32bf3b9d3202538d39314ad1aab1155f713
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660758"
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="71ce9-104">Overview of Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="71ce9-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="71ce9-105">This article provides a conceptual overview of monitoring Azure resources.</span><span class="sxs-lookup"><span data-stu-id="71ce9-105">This article provides a conceptual overview of monitoring Azure resources.</span></span> <span data-ttu-id="71ce9-106">It provides pointers to information on specific types of resources.</span><span class="sxs-lookup"><span data-stu-id="71ce9-106">It provides pointers to information on specific types of resources.</span></span>  <span data-ttu-id="71ce9-107">For high-level information on monitoring your application from non-Azure point of view, see [Monitoring and diagnostics guidance](../best-practices-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="71ce9-107">For high-level information on monitoring your application from non-Azure point of view, see [Monitoring and diagnostics guidance](../best-practices-monitoring.md).</span></span>

<span data-ttu-id="71ce9-108">A video walkthrough of Azure Monitor is available at</span><span class="sxs-lookup"><span data-stu-id="71ce9-108">A video walkthrough of Azure Monitor is available at</span></span>  
<span data-ttu-id="71ce9-109">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="71ce9-109">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="71ce9-110">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234).</span><span class="sxs-lookup"><span data-stu-id="71ce9-110">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234).</span></span>  

<span data-ttu-id="71ce9-111">Cloud applications are complex with many moving parts.</span><span class="sxs-lookup"><span data-stu-id="71ce9-111">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="71ce9-112">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span><span class="sxs-lookup"><span data-stu-id="71ce9-112">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="71ce9-113">It also helps you to stave off potential problems or troubleshoot past ones.</span><span class="sxs-lookup"><span data-stu-id="71ce9-113">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="71ce9-114">In addition, you can use monitoring data to gain deep insights about your application.</span><span class="sxs-lookup"><span data-stu-id="71ce9-114">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="71ce9-115">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span><span class="sxs-lookup"><span data-stu-id="71ce9-115">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="71ce9-116">The following diagram shows a conceptual view of Azure monitoring, including the type of logs you can collect and what you can do with that data.</span><span class="sxs-lookup"><span data-stu-id="71ce9-116">The following diagram shows a conceptual view of Azure monitoring, including the type of logs you can collect and what you can do with that data.</span></span>   

![Model for monitoring and diagnostics for non-compute resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview/Monitoring_Azure_Resources-compute_v4.png)

<br/>

![Model for monitoring and diagnostics for compute resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview/Monitoring_Azure_Resources-non-compute_v4.png)


## <a name="monitoring-sources"></a><span data-ttu-id="71ce9-119">Monitoring Sources</span><span class="sxs-lookup"><span data-stu-id="71ce9-119">Monitoring Sources</span></span>
### <a name="activity-logs"></a><span data-ttu-id="71ce9-120">Activity Logs</span><span class="sxs-lookup"><span data-stu-id="71ce9-120">Activity Logs</span></span>
<span data-ttu-id="71ce9-121">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71ce9-121">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> <span data-ttu-id="71ce9-122">The log contains information such as times when resources are created or destroyed.</span><span class="sxs-lookup"><span data-stu-id="71ce9-122">The log contains information such as times when resources are created or destroyed.</span></span>  

### <a name="host-vm"></a><span data-ttu-id="71ce9-123">Host VM</span><span class="sxs-lookup"><span data-stu-id="71ce9-123">Host VM</span></span>
<span data-ttu-id="71ce9-124">**Compute Only**</span><span class="sxs-lookup"><span data-stu-id="71ce9-124">**Compute Only**</span></span>

<span data-ttu-id="71ce9-125">Some compute resources like Cloud Services, Virtual Machines, and Service Fabric have a dedicated Host VM they interact with.</span><span class="sxs-lookup"><span data-stu-id="71ce9-125">Some compute resources like Cloud Services, Virtual Machines, and Service Fabric have a dedicated Host VM they interact with.</span></span> <span data-ttu-id="71ce9-126">The Host VM is the equivalent of Root VM in the Hyper-V hypervisor model.</span><span class="sxs-lookup"><span data-stu-id="71ce9-126">The Host VM is the equivalent of Root VM in the Hyper-V hypervisor model.</span></span> <span data-ttu-id="71ce9-127">In this case, you can collect metrics on just the Host VM in addition to the Guest OS.</span><span class="sxs-lookup"><span data-stu-id="71ce9-127">In this case, you can collect metrics on just the Host VM in addition to the Guest OS.</span></span>  

<span data-ttu-id="71ce9-128">For other Azure services, there is not necessarily a 1:1 mapping between your resource and a particular Host VM so host VM metrics are not available.</span><span class="sxs-lookup"><span data-stu-id="71ce9-128">For other Azure services, there is not necessarily a 1:1 mapping between your resource and a particular Host VM so host VM metrics are not available.</span></span>

### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="71ce9-129">Resource - Metrics and Diagnostics Logs</span><span class="sxs-lookup"><span data-stu-id="71ce9-129">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="71ce9-130">Collectable metrics vary based on the resource type.</span><span class="sxs-lookup"><span data-stu-id="71ce9-130">Collectable metrics vary based on the resource type.</span></span> <span data-ttu-id="71ce9-131">For example, Virtual Machines provides statistics on the Disk IO and Percent CPU.</span><span class="sxs-lookup"><span data-stu-id="71ce9-131">For example, Virtual Machines provides statistics on the Disk IO and Percent CPU.</span></span> <span data-ttu-id="71ce9-132">But those stats don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span><span class="sxs-lookup"><span data-stu-id="71ce9-132">But those stats don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span>

<span data-ttu-id="71ce9-133">For compute resources you can obtain metrics on the Guest OS and diagnostics modules like Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="71ce9-133">For compute resources you can obtain metrics on the Guest OS and diagnostics modules like Azure Diagnostics.</span></span> <span data-ttu-id="71ce9-134">Azure Diagnostics helps gather and route diagnostic data to other locations, including Azure storage.</span><span class="sxs-lookup"><span data-stu-id="71ce9-134">Azure Diagnostics helps gather and route diagnostic data to other locations, including Azure storage.</span></span>

<span data-ttu-id="71ce9-135">A list of currently collectable metrics is available at [supported metrics](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="71ce9-135">A list of currently collectable metrics is available at [supported metrics](monitoring-supported-metrics.md).</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="71ce9-136">Application - Diagnostics Logs, Application Logs, and Metrics</span><span class="sxs-lookup"><span data-stu-id="71ce9-136">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="71ce9-137">**Compute Only**</span><span class="sxs-lookup"><span data-stu-id="71ce9-137">**Compute Only**</span></span>

<span data-ttu-id="71ce9-138">Applications can run on top of the Guest OS in the compute model.</span><span class="sxs-lookup"><span data-stu-id="71ce9-138">Applications can run on top of the Guest OS in the compute model.</span></span> <span data-ttu-id="71ce9-139">They emit their own set of logs and metrics.</span><span class="sxs-lookup"><span data-stu-id="71ce9-139">They emit their own set of logs and metrics.</span></span>

<span data-ttu-id="71ce9-140">Types of metrics include</span><span class="sxs-lookup"><span data-stu-id="71ce9-140">Types of metrics include</span></span>

* <span data-ttu-id="71ce9-141">Performance counters</span><span class="sxs-lookup"><span data-stu-id="71ce9-141">Performance counters</span></span>
* <span data-ttu-id="71ce9-142">Application Logs</span><span class="sxs-lookup"><span data-stu-id="71ce9-142">Application Logs</span></span>
* <span data-ttu-id="71ce9-143">Windows Event Logs</span><span class="sxs-lookup"><span data-stu-id="71ce9-143">Windows Event Logs</span></span>
* <span data-ttu-id="71ce9-144">.NET Event Source</span><span class="sxs-lookup"><span data-stu-id="71ce9-144">.NET Event Source</span></span>
* <span data-ttu-id="71ce9-145">IIS Logs</span><span class="sxs-lookup"><span data-stu-id="71ce9-145">IIS Logs</span></span>
* <span data-ttu-id="71ce9-146">Manifest based ETW</span><span class="sxs-lookup"><span data-stu-id="71ce9-146">Manifest based ETW</span></span>
* <span data-ttu-id="71ce9-147">Crash Dumps</span><span class="sxs-lookup"><span data-stu-id="71ce9-147">Crash Dumps</span></span>
* <span data-ttu-id="71ce9-148">Customer Error Logs</span><span class="sxs-lookup"><span data-stu-id="71ce9-148">Customer Error Logs</span></span>

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="71ce9-149">Uses for Monitoring Data</span><span class="sxs-lookup"><span data-stu-id="71ce9-149">Uses for Monitoring Data</span></span>
### <a name="visualize"></a><span data-ttu-id="71ce9-150">Visualize</span><span class="sxs-lookup"><span data-stu-id="71ce9-150">Visualize</span></span>
<span data-ttu-id="71ce9-151">Visualizing your monitoring data in graphics and charts helps you find trends far more quickly than looking through the data itself.</span><span class="sxs-lookup"><span data-stu-id="71ce9-151">Visualizing your monitoring data in graphics and charts helps you find trends far more quickly than looking through the data itself.</span></span>  

<span data-ttu-id="71ce9-152">A few visualization methods include:</span><span class="sxs-lookup"><span data-stu-id="71ce9-152">A few visualization methods include:</span></span>

* <span data-ttu-id="71ce9-153">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="71ce9-153">Use the Azure portal</span></span>
* <span data-ttu-id="71ce9-154">Route data to Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="71ce9-154">Route data to Azure Application Insights</span></span>
* <span data-ttu-id="71ce9-155">Route data to Microsoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="71ce9-155">Route data to Microsoft PowerBI</span></span>
* <span data-ttu-id="71ce9-156">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span><span class="sxs-lookup"><span data-stu-id="71ce9-156">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span></span>

### <a name="archive"></a><span data-ttu-id="71ce9-157">Archive</span><span class="sxs-lookup"><span data-stu-id="71ce9-157">Archive</span></span>
<span data-ttu-id="71ce9-158">Monitoring data is typically written to Azure storage and kept there until you delete it.</span><span class="sxs-lookup"><span data-stu-id="71ce9-158">Monitoring data is typically written to Azure storage and kept there until you delete it.</span></span>

<span data-ttu-id="71ce9-159">A few ways to use this data:</span><span class="sxs-lookup"><span data-stu-id="71ce9-159">A few ways to use this data:</span></span>

* <span data-ttu-id="71ce9-160">Once written, you can have other tools within or outside of Azure read it and process it.</span><span class="sxs-lookup"><span data-stu-id="71ce9-160">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
* <span data-ttu-id="71ce9-161">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="71ce9-161">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span></span>  
* <a name="you-leave-the-data-in-azure-storage-indefinitely-though-you-have-to-pay-for-azure-storage-based-on-the-amount-of-data-you-keep"></a><span data-ttu-id="71ce9-162">You leave the data in Azure storage indefinitely, though you have to pay for Azure storage based on the amount of data you keep.</span><span class="sxs-lookup"><span data-stu-id="71ce9-162">You leave the data in Azure storage indefinitely, though you have to pay for Azure storage based on the amount of data you keep.</span></span>
  -

### <a name="query"></a><span data-ttu-id="71ce9-163">Query</span><span class="sxs-lookup"><span data-stu-id="71ce9-163">Query</span></span>
<span data-ttu-id="71ce9-164">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span><span class="sxs-lookup"><span data-stu-id="71ce9-164">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span></span>

<span data-ttu-id="71ce9-165">Examples include:</span><span class="sxs-lookup"><span data-stu-id="71ce9-165">Examples include:</span></span>

* <span data-ttu-id="71ce9-166">Getting data for a custom monitoring application you have written</span><span class="sxs-lookup"><span data-stu-id="71ce9-166">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="71ce9-167">Creating custom queries and sending that data to a third-party application.</span><span class="sxs-lookup"><span data-stu-id="71ce9-167">Creating custom queries and sending that data to a third-party application.</span></span>

### <a name="route"></a><span data-ttu-id="71ce9-168">Route</span><span class="sxs-lookup"><span data-stu-id="71ce9-168">Route</span></span>
<span data-ttu-id="71ce9-169">You can stream monitoring data to other locations in real time.</span><span class="sxs-lookup"><span data-stu-id="71ce9-169">You can stream monitoring data to other locations in real time.</span></span>

<span data-ttu-id="71ce9-170">Examples include:</span><span class="sxs-lookup"><span data-stu-id="71ce9-170">Examples include:</span></span>

* <span data-ttu-id="71ce9-171">Send to Application Insights so you can use the visualization tools there.</span><span class="sxs-lookup"><span data-stu-id="71ce9-171">Send to Application Insights so you can use the visualization tools there.</span></span>
* <span data-ttu-id="71ce9-172">Send to Event Hubs so you can route to third-party tools to perform real-time analysis.</span><span class="sxs-lookup"><span data-stu-id="71ce9-172">Send to Event Hubs so you can route to third-party tools to perform real-time analysis.</span></span>

### <a name="automate"></a><span data-ttu-id="71ce9-173">Automate</span><span class="sxs-lookup"><span data-stu-id="71ce9-173">Automate</span></span>
<span data-ttu-id="71ce9-174">You can use monitoring data to trigger alerts or even whole processes.</span><span class="sxs-lookup"><span data-stu-id="71ce9-174">You can use monitoring data to trigger alerts or even whole processes.</span></span>
<span data-ttu-id="71ce9-175">Examples include:</span><span class="sxs-lookup"><span data-stu-id="71ce9-175">Examples include:</span></span>

* <span data-ttu-id="71ce9-176">Use data to autoscale compute instances up or down based on application load.</span><span class="sxs-lookup"><span data-stu-id="71ce9-176">Use data to autoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="71ce9-177">Send emails when a metric crosses a predetermined threshold.</span><span class="sxs-lookup"><span data-stu-id="71ce9-177">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="71ce9-178">Call a web URL (webhook) to execute an action in a system outside of Azure</span><span class="sxs-lookup"><span data-stu-id="71ce9-178">Call a web URL (webhook) to execute an action in a system outside of Azure</span></span>
* <span data-ttu-id="71ce9-179">Start a runbook in Azure automation to perform any variety of tasks</span><span class="sxs-lookup"><span data-stu-id="71ce9-179">Start a runbook in Azure automation to perform any variety of tasks</span></span>

## <a name="methods-of-use"></a><span data-ttu-id="71ce9-180">Methods of Use</span><span class="sxs-lookup"><span data-stu-id="71ce9-180">Methods of Use</span></span>
<span data-ttu-id="71ce9-181">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span><span class="sxs-lookup"><span data-stu-id="71ce9-181">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span></span> <span data-ttu-id="71ce9-182">Not all methods are available for all actions or data types.</span><span class="sxs-lookup"><span data-stu-id="71ce9-182">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="71ce9-183">Azure portal</span><span class="sxs-lookup"><span data-stu-id="71ce9-183">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="71ce9-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71ce9-184">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="71ce9-185">Cross-platform Command Line Interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="71ce9-185">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="71ce9-186">REST API</span><span class="sxs-lookup"><span data-stu-id="71ce9-186">REST API</span></span>](https://msdn.microsoft.com/library/dn931943.aspx)
* [<span data-ttu-id="71ce9-187">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="71ce9-187">.NET SDK</span></span>](https://msdn.microsoft.com/library/dn802153.aspx)

## <a name="azures-monitoring-offerings"></a><span data-ttu-id="71ce9-188">Azure’s Monitoring Offerings</span><span class="sxs-lookup"><span data-stu-id="71ce9-188">Azure’s Monitoring Offerings</span></span>
<span data-ttu-id="71ce9-189">Azure has offerings available for monitoring your services from bare-metal infrastructure to application telemetry.</span><span class="sxs-lookup"><span data-stu-id="71ce9-189">Azure has offerings available for monitoring your services from bare-metal infrastructure to application telemetry.</span></span> <span data-ttu-id="71ce9-190">The best monitoring strategy combines use of all three to gain comprehensive, detailed insight into the health of your services.</span><span class="sxs-lookup"><span data-stu-id="71ce9-190">The best monitoring strategy combines use of all three to gain comprehensive, detailed insight into the health of your services.</span></span>

* <span data-ttu-id="71ce9-191">[Azure Monitor](http://aka.ms/azmondocs) – Offers visualization, query, routing, alerting, autoscale, and automation on data both from the Azure infrastructure (Activity Log) and each individual Azure resource (Diagnostic Logs).</span><span class="sxs-lookup"><span data-stu-id="71ce9-191">[Azure Monitor](http://aka.ms/azmondocs) – Offers visualization, query, routing, alerting, autoscale, and automation on data both from the Azure infrastructure (Activity Log) and each individual Azure resource (Diagnostic Logs).</span></span> <span data-ttu-id="71ce9-192">This article is part of the Azure Monitor documentation.</span><span class="sxs-lookup"><span data-stu-id="71ce9-192">This article is part of the Azure Monitor documentation.</span></span> <span data-ttu-id="71ce9-193">The Azure Monitor name was released September 25 at Ignite 2016.</span><span class="sxs-lookup"><span data-stu-id="71ce9-193">The Azure Monitor name was released September 25 at Ignite 2016.</span></span>  <span data-ttu-id="71ce9-194">The previous name was "Azure Insights."</span><span class="sxs-lookup"><span data-stu-id="71ce9-194">The previous name was "Azure Insights."</span></span>  
* <span data-ttu-id="71ce9-195">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) – Provides rich detection and diagnostics for issues at the application layer of your service, well-integrated on top of data from Azure Monitoring.</span><span class="sxs-lookup"><span data-stu-id="71ce9-195">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) – Provides rich detection and diagnostics for issues at the application layer of your service, well-integrated on top of data from Azure Monitoring.</span></span> <span data-ttu-id="71ce9-196">It's the default diagnostics platform for App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="71ce9-196">It's the default diagnostics platform for App Service Web Apps.</span></span>  <span data-ttu-id="71ce9-197">You can route data from other services to it.</span><span class="sxs-lookup"><span data-stu-id="71ce9-197">You can route data from other services to it.</span></span>  
* <span data-ttu-id="71ce9-198">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) part of [Operations Management Suite](https://www.microsoft.com/oms/) – Provides a holistic IT management solution for both on-premises and third-party cloud-based infrastructure (such as AWS) in addition to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="71ce9-198">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) part of [Operations Management Suite](https://www.microsoft.com/oms/) – Provides a holistic IT management solution for both on-premises and third-party cloud-based infrastructure (such as AWS) in addition to Azure resources.</span></span>  <span data-ttu-id="71ce9-199">Data from Azure Monitor can be routed directly to Log Analytics so you can see metrics and logs for your entire environment in one place.</span><span class="sxs-lookup"><span data-stu-id="71ce9-199">Data from Azure Monitor can be routed directly to Log Analytics so you can see metrics and logs for your entire environment in one place.</span></span>     

## <a name="next-steps"></a><span data-ttu-id="71ce9-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="71ce9-200">Next steps</span></span>
<span data-ttu-id="71ce9-201">Learn more about</span><span class="sxs-lookup"><span data-stu-id="71ce9-201">Learn more about</span></span>

* [<span data-ttu-id="71ce9-202">Azure Monitor in a video from Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="71ce9-202">Azure Monitor in a video from Ignite 2016</span></span>](https://myignite.microsoft.com/videos/4977)
* [<span data-ttu-id="71ce9-203">Getting Started with Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="71ce9-203">Getting Started with Azure Monitor</span></span>](monitoring-get-started.md)
* <span data-ttu-id="71ce9-204">[Azure Diagnostics](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, or Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="71ce9-204">[Azure Diagnostics](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, or Service Fabric application.</span></span>
* <span data-ttu-id="71ce9-205">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span><span class="sxs-lookup"><span data-stu-id="71ce9-205">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span></span>
* <span data-ttu-id="71ce9-206">[Troubleshooting Azure Storage](../storage/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span><span class="sxs-lookup"><span data-stu-id="71ce9-206">[Troubleshooting Azure Storage](../storage/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
* <span data-ttu-id="71ce9-207">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and the [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="71ce9-207">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and the [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>


