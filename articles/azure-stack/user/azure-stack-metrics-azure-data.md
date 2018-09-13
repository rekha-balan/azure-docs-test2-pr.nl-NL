---
title: Azure Monitor on Azure Stack | Microsoft Docs
description: Learn about Azure Monitor on Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: mabrigg
ms.openlocfilehash: b0cf2d7856a78bbe2aa531c6e872168e8e33b06a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868545"
---
# <a name="azure-monitor-on-azure-stack"></a><span data-ttu-id="692d8-103">Azure Monitor on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="692d8-103">Azure Monitor on Azure Stack</span></span>

<span data-ttu-id="692d8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="692d8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="692d8-105">This article provides an overview of the Azure Monitor service in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="692d8-105">This article provides an overview of the Azure Monitor service in Azure Stack.</span></span> <span data-ttu-id="692d8-106">It discusses the operation of Azure Monitor and additional information on how to use Azure Monitor on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="692d8-106">It discusses the operation of Azure Monitor and additional information on how to use Azure Monitor on Azure Stack.</span></span> 

<span data-ttu-id="692d8-107">For an introduction, overview, and how to get started with Azure Monitor, see the global Azure article [Get started with Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).</span><span class="sxs-lookup"><span data-stu-id="692d8-107">For an introduction, overview, and how to get started with Azure Monitor, see the global Azure article [Get started with Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).</span></span>

![Azure Stack Monitor blade](./media/azure-stack-metrics-azure-data/azs-monitor.png)

<span data-ttu-id="692d8-109">Azure Monitor is the platform service that provides a single source for monitoring Azure resources.</span><span class="sxs-lookup"><span data-stu-id="692d8-109">Azure Monitor is the platform service that provides a single source for monitoring Azure resources.</span></span> <span data-ttu-id="692d8-110">With Azure Monitor, you can visualize, query, route, archive, and otherwise take action on the metrics and logs coming from resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="692d8-110">With Azure Monitor, you can visualize, query, route, archive, and otherwise take action on the metrics and logs coming from resources in Azure.</span></span> <span data-ttu-id="692d8-111">You can work with this data by using the Azure Stack admin portal, Monitor PowerShell Cmdlets, Cross-Platform CLI, or Azure Monitor REST APIs.</span><span class="sxs-lookup"><span data-stu-id="692d8-111">You can work with this data by using the Azure Stack admin portal, Monitor PowerShell Cmdlets, Cross-Platform CLI, or Azure Monitor REST APIs.</span></span> <span data-ttu-id="692d8-112">For the specific connectivity supported by Azure Stack, see [How to consume monitoring data from Azure Stack](azure-stack-metrics-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="692d8-112">For the specific connectivity supported by Azure Stack, see [How to consume monitoring data from Azure Stack](azure-stack-metrics-monitor.md)</span></span>

> [!Note]  
<span data-ttu-id="692d8-113">Metrics and diagnostic logs are not available for the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="692d8-113">Metrics and diagnostic logs are not available for the Azure Stack Development Kit.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="692d8-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="692d8-114">Prerequisites</span></span>

<span data-ttu-id="692d8-115">Register the **Microsoft.insights** resource provider on your subscription's offer resource providers settings.</span><span class="sxs-lookup"><span data-stu-id="692d8-115">Register the **Microsoft.insights** resource provider on your subscription's offer resource providers settings.</span></span> <span data-ttu-id="692d8-116">You can verify that the resource provider is available in your offer associated with your subscription:</span><span class="sxs-lookup"><span data-stu-id="692d8-116">You can verify that the resource provider is available in your offer associated with your subscription:</span></span>

1. <span data-ttu-id="692d8-117">Open the Azure Stack admin portal.</span><span class="sxs-lookup"><span data-stu-id="692d8-117">Open the Azure Stack admin portal.</span></span>
2. <span data-ttu-id="692d8-118">Select **Offers**.</span><span class="sxs-lookup"><span data-stu-id="692d8-118">Select **Offers**.</span></span>
3. <span data-ttu-id="692d8-119">Select the offer associated with the subscription.</span><span class="sxs-lookup"><span data-stu-id="692d8-119">Select the offer associated with the subscription.</span></span>
4. <span data-ttu-id="692d8-120">Select **Resource providers** under **Settings.**</span><span class="sxs-lookup"><span data-stu-id="692d8-120">Select **Resource providers** under **Settings.**</span></span> 
5. <span data-ttu-id="692d8-121">Find **Microsoft.Insights** in the list and verify that the status is **Registered.**.</span><span class="sxs-lookup"><span data-stu-id="692d8-121">Find **Microsoft.Insights** in the list and verify that the status is **Registered.**.</span></span>

## <a name="overview"></a><span data-ttu-id="692d8-122">Overview</span><span class="sxs-lookup"><span data-stu-id="692d8-122">Overview</span></span>

<span data-ttu-id="692d8-123">Like Azure Monitor on Azure, Azure Monitor on Azure Stack provides base-level infrastructure metrics and logs for most services.</span><span class="sxs-lookup"><span data-stu-id="692d8-123">Like Azure Monitor on Azure, Azure Monitor on Azure Stack provides base-level infrastructure metrics and logs for most services.</span></span>

## <a name="azure-monitor-sources-compute-subset"></a><span data-ttu-id="692d8-124">Azure monitor sources: compute subset</span><span class="sxs-lookup"><span data-stu-id="692d8-124">Azure monitor sources: compute subset</span></span>

![Azure monitor sources -compute subset](media//azure-stack-metrics-azure-data/azs-monitor-computersubset.png)

<span data-ttu-id="692d8-126">The **Microsoft.Compute** resource provider in Azure Stack includes:</span><span class="sxs-lookup"><span data-stu-id="692d8-126">The **Microsoft.Compute** resource provider in Azure Stack includes:</span></span>
 - <span data-ttu-id="692d8-127">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="692d8-127">Virtual Machines</span></span> 
 - <span data-ttu-id="692d8-128">Virtual Machines scale sets</span><span class="sxs-lookup"><span data-stu-id="692d8-128">Virtual Machines scale sets</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="692d8-129">Application - Diagnostics logs, Application logs, and Metrics</span><span class="sxs-lookup"><span data-stu-id="692d8-129">Application - Diagnostics logs, Application logs, and Metrics</span></span>

<span data-ttu-id="692d8-130">Applications can run in the OS of a VM running with the **Microsoft.Compute** resource provider.</span><span class="sxs-lookup"><span data-stu-id="692d8-130">Applications can run in the OS of a VM running with the **Microsoft.Compute** resource provider.</span></span> <span data-ttu-id="692d8-131">These applications and VMs emit their own set of logs and metrics.</span><span class="sxs-lookup"><span data-stu-id="692d8-131">These applications and VMs emit their own set of logs and metrics.</span></span> <span data-ttu-id="692d8-132">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span><span class="sxs-lookup"><span data-stu-id="692d8-132">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> 

<span data-ttu-id="692d8-133">The types of measures include:</span><span class="sxs-lookup"><span data-stu-id="692d8-133">The types of measures include:</span></span>
 - <span data-ttu-id="692d8-134">Performance counters</span><span class="sxs-lookup"><span data-stu-id="692d8-134">Performance counters</span></span>
 - <span data-ttu-id="692d8-135">Application logs</span><span class="sxs-lookup"><span data-stu-id="692d8-135">Application logs</span></span>
 - <span data-ttu-id="692d8-136">Windows event logs</span><span class="sxs-lookup"><span data-stu-id="692d8-136">Windows event logs</span></span>
 - <span data-ttu-id="692d8-137">.NET event source</span><span class="sxs-lookup"><span data-stu-id="692d8-137">.NET event source</span></span>
 - <span data-ttu-id="692d8-138">IIS logs</span><span class="sxs-lookup"><span data-stu-id="692d8-138">IIS logs</span></span>
 - <span data-ttu-id="692d8-139">Manifest-based ETW</span><span class="sxs-lookup"><span data-stu-id="692d8-139">Manifest-based ETW</span></span>
 - <span data-ttu-id="692d8-140">Crash dumps</span><span class="sxs-lookup"><span data-stu-id="692d8-140">Crash dumps</span></span>
 - <span data-ttu-id="692d8-141">Customer error logs</span><span class="sxs-lookup"><span data-stu-id="692d8-141">Customer error logs</span></span>

> [!Note]  
> <span data-ttu-id="692d8-142">Linux Diagnostics extension on Azure Stack are not supported.</span><span class="sxs-lookup"><span data-stu-id="692d8-142">Linux Diagnostics extension on Azure Stack are not supported.</span></span>

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="692d8-143">Host and Guest VM metrics</span><span class="sxs-lookup"><span data-stu-id="692d8-143">Host and Guest VM metrics</span></span>

<span data-ttu-id="692d8-144">The previously listed compute resources have a dedicated host VM and guest OS.</span><span class="sxs-lookup"><span data-stu-id="692d8-144">The previously listed compute resources have a dedicated host VM and guest OS.</span></span> <span data-ttu-id="692d8-145">The host VM and guest OS are the equivalent of root VM and guest VM in Hyper-V hypervisor.</span><span class="sxs-lookup"><span data-stu-id="692d8-145">The host VM and guest OS are the equivalent of root VM and guest VM in Hyper-V hypervisor.</span></span> <span data-ttu-id="692d8-146">You can collect metrics for both the host VM and the guest OS.</span><span class="sxs-lookup"><span data-stu-id="692d8-146">You can collect metrics for both the host VM and the guest OS.</span></span> <span data-ttu-id="692d8-147">In addition, you can collect diagnostics logs for the guest OS.</span><span class="sxs-lookup"><span data-stu-id="692d8-147">In addition, you can collect diagnostics logs for the guest OS.</span></span> <span data-ttu-id="692d8-148">A list of collectible metrics for Host and Guest VM metrics on Azure Stack are available at [Supported metrics with Azure Monitor on Azure Stack](azure-stack-metrics-supported.md).</span><span class="sxs-lookup"><span data-stu-id="692d8-148">A list of collectible metrics for Host and Guest VM metrics on Azure Stack are available at [Supported metrics with Azure Monitor on Azure Stack](azure-stack-metrics-supported.md).</span></span> 

### <a name="activity-log"></a><span data-ttu-id="692d8-149">Activity log</span><span class="sxs-lookup"><span data-stu-id="692d8-149">Activity log</span></span>

<span data-ttu-id="692d8-150">You can search the activity logs for information about your compute resources as seen by the Azure Stack infrastructure.</span><span class="sxs-lookup"><span data-stu-id="692d8-150">You can search the activity logs for information about your compute resources as seen by the Azure Stack infrastructure.</span></span> <span data-ttu-id="692d8-151">The log contains information such as times when resources are created or destroyed.</span><span class="sxs-lookup"><span data-stu-id="692d8-151">The log contains information such as times when resources are created or destroyed.</span></span> <span data-ttu-id="692d8-152">The activity logs on Azure Stack is consistent with Azure.</span><span class="sxs-lookup"><span data-stu-id="692d8-152">The activity logs on Azure Stack is consistent with Azure.</span></span> <span data-ttu-id="692d8-153">For more information, see the description of [Activity log overview on Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</span><span class="sxs-lookup"><span data-stu-id="692d8-153">For more information, see the description of [Activity log overview on Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</span></span> 


## <a name="azure-monitor-sources-everything-else"></a><span data-ttu-id="692d8-154">Azure monitor sources: everything else</span><span class="sxs-lookup"><span data-stu-id="692d8-154">Azure monitor sources: everything else</span></span>

![Azure monitor sources - everything else](media//azure-stack-metrics-azure-data/azs-monitor-othersubset.png)

### <a name="resources---metrics-and-diagnostics-logs"></a><span data-ttu-id="692d8-156">Resources - Metrics and Diagnostics logs</span><span class="sxs-lookup"><span data-stu-id="692d8-156">Resources - Metrics and Diagnostics logs</span></span>

<span data-ttu-id="692d8-157">Collectible metrics and diagnostics logs vary based on the resource type.</span><span class="sxs-lookup"><span data-stu-id="692d8-157">Collectible metrics and diagnostics logs vary based on the resource type.</span></span> <span data-ttu-id="692d8-158">A list of collectible metrics for each resource on Azure Stack is available at supported metrics.</span><span class="sxs-lookup"><span data-stu-id="692d8-158">A list of collectible metrics for each resource on Azure Stack is available at supported metrics.</span></span> <span data-ttu-id="692d8-159">For more information, see [Supported metrics with Azure Monitor on Azure Stack](azure-stack-metrics-supported.md).</span><span class="sxs-lookup"><span data-stu-id="692d8-159">For more information, see [Supported metrics with Azure Monitor on Azure Stack](azure-stack-metrics-supported.md).</span></span>

### <a name="activity-log"></a><span data-ttu-id="692d8-160">Activity log</span><span class="sxs-lookup"><span data-stu-id="692d8-160">Activity log</span></span>

<span data-ttu-id="692d8-161">The activity log is the same for compute resources.</span><span class="sxs-lookup"><span data-stu-id="692d8-161">The activity log is the same for compute resources.</span></span> 

### <a name="uses-for-monitoring-data"></a><span data-ttu-id="692d8-162">Uses for monitoring data</span><span class="sxs-lookup"><span data-stu-id="692d8-162">Uses for monitoring data</span></span>

<span data-ttu-id="692d8-163">**Store and Archive**</span><span class="sxs-lookup"><span data-stu-id="692d8-163">**Store and Archive**</span></span>  

<span data-ttu-id="692d8-164">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span><span class="sxs-lookup"><span data-stu-id="692d8-164">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
 - <span data-ttu-id="692d8-165">Metrics are stored for 90 days.</span><span class="sxs-lookup"><span data-stu-id="692d8-165">Metrics are stored for 90 days.</span></span> 
 - <span data-ttu-id="692d8-166">Activity log entries are stored for 90 days.</span><span class="sxs-lookup"><span data-stu-id="692d8-166">Activity log entries are stored for 90 days.</span></span> 
 - <span data-ttu-id="692d8-167">Diagnostics logs are not stored.</span><span class="sxs-lookup"><span data-stu-id="692d8-167">Diagnostics logs are not stored.</span></span>
 - <span data-ttu-id="692d8-168">Archive the data to a storage account for longer retention.</span><span class="sxs-lookup"><span data-stu-id="692d8-168">Archive the data to a storage account for longer retention.</span></span>

<span data-ttu-id="692d8-169">**Query**</span><span class="sxs-lookup"><span data-stu-id="692d8-169">**Query**</span></span>  

<span data-ttu-id="692d8-170">You can use the Azure Monitor REST API, cross-platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage.</span><span class="sxs-lookup"><span data-stu-id="692d8-170">You can use the Azure Monitor REST API, cross-platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage.</span></span> 

<span data-ttu-id="692d8-171">**Visualization**</span><span class="sxs-lookup"><span data-stu-id="692d8-171">**Visualization**</span></span>

<span data-ttu-id="692d8-172">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span><span class="sxs-lookup"><span data-stu-id="692d8-172">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span></span> 

<span data-ttu-id="692d8-173">A few visualization methods include:</span><span class="sxs-lookup"><span data-stu-id="692d8-173">A few visualization methods include:</span></span>
 - <span data-ttu-id="692d8-174">Use the Azure Stack user and admin portal</span><span class="sxs-lookup"><span data-stu-id="692d8-174">Use the Azure Stack user and admin portal</span></span>
 - <span data-ttu-id="692d8-175">Route data to Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="692d8-175">Route data to Microsoft Power BI</span></span>
 - <span data-ttu-id="692d8-176">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span><span class="sxs-lookup"><span data-stu-id="692d8-176">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span></span>

## <a name="methods-of-accessing-azure-monitor-on-azure-stack"></a><span data-ttu-id="692d8-177">Methods of accessing Azure monitor on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="692d8-177">Methods of accessing Azure monitor on Azure Stack</span></span>

<span data-ttu-id="692d8-178">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span><span class="sxs-lookup"><span data-stu-id="692d8-178">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span></span> <span data-ttu-id="692d8-179">Not all methods are available for all actions or data types.</span><span class="sxs-lookup"><span data-stu-id="692d8-179">Not all methods are available for all actions or data types.</span></span>

 - [<span data-ttu-id="692d8-180">Azure Stack Portal</span><span class="sxs-lookup"><span data-stu-id="692d8-180">Azure Stack Portal</span></span>](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-use-portal)
 - [<span data-ttu-id="692d8-181">PowerShell</span><span class="sxs-lookup"><span data-stu-id="692d8-181">PowerShell</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples)
 - [<span data-ttu-id="692d8-182">Cross-platform Command Line Interface(CLI)</span><span class="sxs-lookup"><span data-stu-id="692d8-182">Cross-platform Command Line Interface(CLI)</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples)
 - [<span data-ttu-id="692d8-183">REST API</span><span class="sxs-lookup"><span data-stu-id="692d8-183">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor)
 - [<span data-ttu-id="692d8-184">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="692d8-184">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="692d8-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="692d8-185">Next steps</span></span>

<span data-ttu-id="692d8-186">Learn more about the options of the monitoring data consumption on Azure Stack in the article [Consume monitoring data from Azure Stack](azure-stack-metrics-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="692d8-186">Learn more about the options of the monitoring data consumption on Azure Stack in the article [Consume monitoring data from Azure Stack](azure-stack-metrics-monitor.md).</span></span>
