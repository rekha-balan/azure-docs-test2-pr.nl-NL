---
title: Overview of metrics in Microsoft Azure | Microsoft Docs
description: Overview of metrics and their use in Microsoft Azure
author: kamathashwin
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: ashwink
ms.openlocfilehash: 9e8c0a06c5cd1d8cd9020950412a2baf2ef74d62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564736"
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="80f5c-103">Overview of metrics in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="80f5c-103">Overview of metrics in Microsoft Azure</span></span>
<span data-ttu-id="80f5c-104">This article describes what metrics are in Microsoft Azure, their benefits, and how to start using them.</span><span class="sxs-lookup"><span data-stu-id="80f5c-104">This article describes what metrics are in Microsoft Azure, their benefits, and how to start using them.</span></span>  

## <a name="what-are-metrics"></a><span data-ttu-id="80f5c-105">What are metrics?</span><span class="sxs-lookup"><span data-stu-id="80f5c-105">What are metrics?</span></span>
<span data-ttu-id="80f5c-106">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span><span class="sxs-lookup"><span data-stu-id="80f5c-106">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span></span> <span data-ttu-id="80f5c-107">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span><span class="sxs-lookup"><span data-stu-id="80f5c-107">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="80f5c-108">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="80f5c-108">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span></span>

## <a name="what-can-you-do-with-metrics"></a><span data-ttu-id="80f5c-109">What can you do with metrics?</span><span class="sxs-lookup"><span data-stu-id="80f5c-109">What can you do with metrics?</span></span>
<span data-ttu-id="80f5c-110">Metrics are a valuable source of telemetry and enable you to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="80f5c-110">Metrics are a valuable source of telemetry and enable you to do the following tasks:</span></span>

* <span data-ttu-id="80f5c-111">**Track the performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart to a dashboard.</span><span class="sxs-lookup"><span data-stu-id="80f5c-111">**Track the performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart to a dashboard.</span></span>
* <span data-ttu-id="80f5c-112">**Get notified of an issue** that impacts the performance of your resource when a metric crosses a certain threshold.</span><span class="sxs-lookup"><span data-stu-id="80f5c-112">**Get notified of an issue** that impacts the performance of your resource when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="80f5c-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span><span class="sxs-lookup"><span data-stu-id="80f5c-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="80f5c-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span><span class="sxs-lookup"><span data-stu-id="80f5c-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span></span>
* <span data-ttu-id="80f5c-115">**Archive** the performance or health history of your resource **for compliance or auditing** purposes.</span><span class="sxs-lookup"><span data-stu-id="80f5c-115">**Archive** the performance or health history of your resource **for compliance or auditing** purposes.</span></span>

## <a name="what-are-the-characteristics-of-metrics"></a><span data-ttu-id="80f5c-116">What are the characteristics of metrics?</span><span class="sxs-lookup"><span data-stu-id="80f5c-116">What are the characteristics of metrics?</span></span>
<span data-ttu-id="80f5c-117">Metrics have the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="80f5c-117">Metrics have the following characteristics:</span></span>

* <span data-ttu-id="80f5c-118">All metrics have **one-minute frequency**.</span><span class="sxs-lookup"><span data-stu-id="80f5c-118">All metrics have **one-minute frequency**.</span></span> <span data-ttu-id="80f5c-119">You receive a metric value every minute from your resource, giving you near real-time visibility into the state and health of your resource.</span><span class="sxs-lookup"><span data-stu-id="80f5c-119">You receive a metric value every minute from your resource, giving you near real-time visibility into the state and health of your resource.</span></span>
* <span data-ttu-id="80f5c-120">Metrics are **available immediately**.</span><span class="sxs-lookup"><span data-stu-id="80f5c-120">Metrics are **available immediately**.</span></span> <span data-ttu-id="80f5c-121">You don't need to opt in or set up additional diagnostics.</span><span class="sxs-lookup"><span data-stu-id="80f5c-121">You don't need to opt in or set up additional diagnostics.</span></span>
* <span data-ttu-id="80f5c-122">You can access **30 days of history** for each metric.</span><span class="sxs-lookup"><span data-stu-id="80f5c-122">You can access **30 days of history** for each metric.</span></span> <span data-ttu-id="80f5c-123">You can quickly look at the recent and monthly trends in the performance or health of your resource.</span><span class="sxs-lookup"><span data-stu-id="80f5c-123">You can quickly look at the recent and monthly trends in the performance or health of your resource.</span></span>

<span data-ttu-id="80f5c-124">You can also:</span><span class="sxs-lookup"><span data-stu-id="80f5c-124">You can also:</span></span>

* <span data-ttu-id="80f5c-125">Configure a metric **alert rule that sends a notification or takes automated action** when the metric crosses the threshold that you have set.</span><span class="sxs-lookup"><span data-stu-id="80f5c-125">Configure a metric **alert rule that sends a notification or takes automated action** when the metric crosses the threshold that you have set.</span></span> <span data-ttu-id="80f5c-126">Autoscale is a special automated action that enables you to scale out your resource to meet incoming requests or loads on your website or computing resources.</span><span class="sxs-lookup"><span data-stu-id="80f5c-126">Autoscale is a special automated action that enables you to scale out your resource to meet incoming requests or loads on your website or computing resources.</span></span> <span data-ttu-id="80f5c-127">You can configure an Autoscale setting rule to scale in or out based on a metric crossing a threshold.</span><span class="sxs-lookup"><span data-stu-id="80f5c-127">You can configure an Autoscale setting rule to scale in or out based on a metric crossing a threshold.</span></span>

* <span data-ttu-id="80f5c-128">**Route** all metrics Application Insights or Log Analytics (OMS) to enable instant analytics, search, and custom alerting on metrics data from your resources.</span><span class="sxs-lookup"><span data-stu-id="80f5c-128">**Route** all metrics Application Insights or Log Analytics (OMS) to enable instant analytics, search, and custom alerting on metrics data from your resources.</span></span> <span data-ttu-id="80f5c-129">You can also stream metrics to an Event Hub, enabling you to then route them to Azure Stream Analytics or to custom apps for near-real time analysis.</span><span class="sxs-lookup"><span data-stu-id="80f5c-129">You can also stream metrics to an Event Hub, enabling you to then route them to Azure Stream Analytics or to custom apps for near-real time analysis.</span></span> <span data-ttu-id="80f5c-130">You set up Event Hub streaming using diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="80f5c-130">You set up Event Hub streaming using diagnostic settings.</span></span>

* <span data-ttu-id="80f5c-131">**Archive metrics to storage** for longer retention or use them for offline reporting.</span><span class="sxs-lookup"><span data-stu-id="80f5c-131">**Archive metrics to storage** for longer retention or use them for offline reporting.</span></span> <span data-ttu-id="80f5c-132">You can route your metrics to Azure Blob storage when you configure diagnostic settings for your resource.</span><span class="sxs-lookup"><span data-stu-id="80f5c-132">You can route your metrics to Azure Blob storage when you configure diagnostic settings for your resource.</span></span>

* <span data-ttu-id="80f5c-133">Easily discover, access, and **view all metrics** via the Azure portal when you select a resource and plot the metrics on a chart.</span><span class="sxs-lookup"><span data-stu-id="80f5c-133">Easily discover, access, and **view all metrics** via the Azure portal when you select a resource and plot the metrics on a chart.</span></span>

* <span data-ttu-id="80f5c-134">**Consume** the metrics via the new Azure Monitor REST APIs.</span><span class="sxs-lookup"><span data-stu-id="80f5c-134">**Consume** the metrics via the new Azure Monitor REST APIs.</span></span>

* <span data-ttu-id="80f5c-135">**Query** metrics by using the PowerShell cmdlets or the Cross-Platform REST API.</span><span class="sxs-lookup"><span data-stu-id="80f5c-135">**Query** metrics by using the PowerShell cmdlets or the Cross-Platform REST API.</span></span>

  ![Routing of Metrics in Azure Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a><span data-ttu-id="80f5c-137">Access metrics via the portal</span><span class="sxs-lookup"><span data-stu-id="80f5c-137">Access metrics via the portal</span></span>
<span data-ttu-id="80f5c-138">Following is a quick walkthrough of how to create a metric chart by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="80f5c-138">Following is a quick walkthrough of how to create a metric chart by using the Azure portal.</span></span>

### <a name="to-view-metrics-after-creating-a-resource"></a><span data-ttu-id="80f5c-139">To view metrics after creating a resource</span><span class="sxs-lookup"><span data-stu-id="80f5c-139">To view metrics after creating a resource</span></span>
1. <span data-ttu-id="80f5c-140">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="80f5c-140">Open the Azure portal.</span></span>
2. <span data-ttu-id="80f5c-141">Create an Azure App Service website.</span><span class="sxs-lookup"><span data-stu-id="80f5c-141">Create an Azure App Service website.</span></span>
3. <span data-ttu-id="80f5c-142">After you create a website, go to the **Overview** blade of the website.</span><span class="sxs-lookup"><span data-stu-id="80f5c-142">After you create a website, go to the **Overview** blade of the website.</span></span>
4. <span data-ttu-id="80f5c-143">You can view new metrics as a **Monitoring** tile.</span><span class="sxs-lookup"><span data-stu-id="80f5c-143">You can view new metrics as a **Monitoring** tile.</span></span> <span data-ttu-id="80f5c-144">You can then edit the tile and select more metrics.</span><span class="sxs-lookup"><span data-stu-id="80f5c-144">You can then edit the tile and select more metrics.</span></span>

   ![Metrics on a resource in Azure Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a><span data-ttu-id="80f5c-146">To access all metrics in a single place</span><span class="sxs-lookup"><span data-stu-id="80f5c-146">To access all metrics in a single place</span></span>
1. <span data-ttu-id="80f5c-147">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="80f5c-147">Open the Azure portal.</span></span>
2. <span data-ttu-id="80f5c-148">Navigate to the new **Monitor** tab, and then and select the **Metrics** option underneath it.</span><span class="sxs-lookup"><span data-stu-id="80f5c-148">Navigate to the new **Monitor** tab, and then and select the **Metrics** option underneath it.</span></span>
3. <span data-ttu-id="80f5c-149">Select your subscription, resource group, and the name of the resource from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="80f5c-149">Select your subscription, resource group, and the name of the resource from the drop-down list.</span></span>
4. <span data-ttu-id="80f5c-150">View the available metrics list.</span><span class="sxs-lookup"><span data-stu-id="80f5c-150">View the available metrics list.</span></span> <span data-ttu-id="80f5c-151">Then select the metric you are interested in and plot it.</span><span class="sxs-lookup"><span data-stu-id="80f5c-151">Then select the metric you are interested in and plot it.</span></span>
5. <span data-ttu-id="80f5c-152">You can pin it to the dashboard by clicking the pin on the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="80f5c-152">You can pin it to the dashboard by clicking the pin on the upper-right corner.</span></span>

   ![Access all metrics in a single place in Azure Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> <span data-ttu-id="80f5c-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span><span class="sxs-lookup"><span data-stu-id="80f5c-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span></span> <span data-ttu-id="80f5c-155">These new host-level metrics are available for Windows and Linux instances.</span><span class="sxs-lookup"><span data-stu-id="80f5c-155">These new host-level metrics are available for Windows and Linux instances.</span></span> <span data-ttu-id="80f5c-156">These metrics are not to be confused with the Guest-OS-level metrics that you have access to when you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="80f5c-156">These metrics are not to be confused with the Guest-OS-level metrics that you have access to when you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span></span> <span data-ttu-id="80f5c-157">To learn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="80f5c-157">To learn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span></span>
>
>

## <a name="access-metrics-via-the-rest-api"></a><span data-ttu-id="80f5c-158">Access metrics via the REST API</span><span class="sxs-lookup"><span data-stu-id="80f5c-158">Access metrics via the REST API</span></span>
<span data-ttu-id="80f5c-159">Azure Metrics can be accessed via the Azure Monitor APIs.</span><span class="sxs-lookup"><span data-stu-id="80f5c-159">Azure Metrics can be accessed via the Azure Monitor APIs.</span></span> <span data-ttu-id="80f5c-160">There are two APIs that help you discover and access metrics:</span><span class="sxs-lookup"><span data-stu-id="80f5c-160">There are two APIs that help you discover and access metrics:</span></span>

* <span data-ttu-id="80f5c-161">Use the [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) to access the list of metrics that are available for a service.</span><span class="sxs-lookup"><span data-stu-id="80f5c-161">Use the [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) to access the list of metrics that are available for a service.</span></span>
* <span data-ttu-id="80f5c-162">Use the [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) to access the actual metrics data.</span><span class="sxs-lookup"><span data-stu-id="80f5c-162">Use the [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) to access the actual metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="80f5c-163">This article covers the metrics via the [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="80f5c-163">This article covers the metrics via the [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span></span> <span data-ttu-id="80f5c-164">The API version for the new metric definitions API is 2016-03-01 and the version for metrics API is 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="80f5c-164">The API version for the new metric definitions API is 2016-03-01 and the version for metrics API is 2016-09-01.</span></span> <span data-ttu-id="80f5c-165">The legacy metric definitions and metrics can be accessed with the API version 2014-04-01.</span><span class="sxs-lookup"><span data-stu-id="80f5c-165">The legacy metric definitions and metrics can be accessed with the API version 2014-04-01.</span></span>
>
>

<span data-ttu-id="80f5c-166">For a more detailed walkthrough using the Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="80f5c-166">For a more detailed walkthrough using the Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span></span>

## <a name="export-metrics"></a><span data-ttu-id="80f5c-167">Export metrics</span><span class="sxs-lookup"><span data-stu-id="80f5c-167">Export metrics</span></span>
<span data-ttu-id="80f5c-168">You can go to the **Diagnostics settings** blade under the **Monitor** tab and view the export options for metrics.</span><span class="sxs-lookup"><span data-stu-id="80f5c-168">You can go to the **Diagnostics settings** blade under the **Monitor** tab and view the export options for metrics.</span></span> <span data-ttu-id="80f5c-169">You can select metrics (and diagnostic logs) to be routed to Blob storage, to Azure Event Hubs, or to OMS for use-cases that were mentioned previously in this article.</span><span class="sxs-lookup"><span data-stu-id="80f5c-169">You can select metrics (and diagnostic logs) to be routed to Blob storage, to Azure Event Hubs, or to OMS for use-cases that were mentioned previously in this article.</span></span>

 ![Export options for metrics in Azure Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-metrics/MetricsOverview3.png)

<span data-ttu-id="80f5c-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="80f5c-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span>

## <a name="take-action-on-metrics"></a><span data-ttu-id="80f5c-172">Take action on metrics</span><span class="sxs-lookup"><span data-stu-id="80f5c-172">Take action on metrics</span></span>
<span data-ttu-id="80f5c-173">To receive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span><span class="sxs-lookup"><span data-stu-id="80f5c-173">To receive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span></span>

### <a name="configure-alert-rules"></a><span data-ttu-id="80f5c-174">Configure alert rules</span><span class="sxs-lookup"><span data-stu-id="80f5c-174">Configure alert rules</span></span>
<span data-ttu-id="80f5c-175">You can configure alert rules on metrics.</span><span class="sxs-lookup"><span data-stu-id="80f5c-175">You can configure alert rules on metrics.</span></span> <span data-ttu-id="80f5c-176">These alert rules can check if a metric has crossed a certain threshold.</span><span class="sxs-lookup"><span data-stu-id="80f5c-176">These alert rules can check if a metric has crossed a certain threshold.</span></span> <span data-ttu-id="80f5c-177">They can then notify you via email or fire a webhook that can be used to run any custom script.</span><span class="sxs-lookup"><span data-stu-id="80f5c-177">They can then notify you via email or fire a webhook that can be used to run any custom script.</span></span> <span data-ttu-id="80f5c-178">You can also use the webhook to configure third-party product integrations.</span><span class="sxs-lookup"><span data-stu-id="80f5c-178">You can also use the webhook to configure third-party product integrations.</span></span>

 ![Metrics and alert rules in Azure Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a><span data-ttu-id="80f5c-180">Autoscale your Azure resources</span><span class="sxs-lookup"><span data-stu-id="80f5c-180">Autoscale your Azure resources</span></span>
<span data-ttu-id="80f5c-181">Some Azure resources support the scaling out or in of multiple instances to handle your workloads.</span><span class="sxs-lookup"><span data-stu-id="80f5c-181">Some Azure resources support the scaling out or in of multiple instances to handle your workloads.</span></span> <span data-ttu-id="80f5c-182">Autoscale applies to App Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="80f5c-182">Autoscale applies to App Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span></span> <span data-ttu-id="80f5c-183">You can configure Autoscale rules to scale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span><span class="sxs-lookup"><span data-stu-id="80f5c-183">You can configure Autoscale rules to scale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span></span> <span data-ttu-id="80f5c-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="80f5c-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span></span>

 ![Metrics and Autoscale in Azure Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a><span data-ttu-id="80f5c-186">Learn about supported services and metrics</span><span class="sxs-lookup"><span data-stu-id="80f5c-186">Learn about supported services and metrics</span></span>
<span data-ttu-id="80f5c-187">Azure Monitor is a new metrics infrastructure.</span><span class="sxs-lookup"><span data-stu-id="80f5c-187">Azure Monitor is a new metrics infrastructure.</span></span> <span data-ttu-id="80f5c-188">It supports the following Azure services in the Azure portal and the new version of the Azure Monitor API:</span><span class="sxs-lookup"><span data-stu-id="80f5c-188">It supports the following Azure services in the Azure portal and the new version of the Azure Monitor API:</span></span>

* <span data-ttu-id="80f5c-189">VMs (Azure Resource Manager-based)</span><span class="sxs-lookup"><span data-stu-id="80f5c-189">VMs (Azure Resource Manager-based)</span></span>
* <span data-ttu-id="80f5c-190">Virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="80f5c-190">Virtual machine scale sets</span></span>
* <span data-ttu-id="80f5c-191">Batch</span><span class="sxs-lookup"><span data-stu-id="80f5c-191">Batch</span></span>
* <span data-ttu-id="80f5c-192">Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="80f5c-192">Event Hubs namespace</span></span>
* <span data-ttu-id="80f5c-193">Service Bus namespace (premium SKU only)</span><span class="sxs-lookup"><span data-stu-id="80f5c-193">Service Bus namespace (premium SKU only)</span></span>
* <span data-ttu-id="80f5c-194">SQL Database (version 12)</span><span class="sxs-lookup"><span data-stu-id="80f5c-194">SQL Database (version 12)</span></span>
* <span data-ttu-id="80f5c-195">Elastic SQL Pool</span><span class="sxs-lookup"><span data-stu-id="80f5c-195">Elastic SQL Pool</span></span>
* <span data-ttu-id="80f5c-196">Websites</span><span class="sxs-lookup"><span data-stu-id="80f5c-196">Websites</span></span>
* <span data-ttu-id="80f5c-197">Web server farms</span><span class="sxs-lookup"><span data-stu-id="80f5c-197">Web server farms</span></span>
* <span data-ttu-id="80f5c-198">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="80f5c-198">Logic Apps</span></span>
* <span data-ttu-id="80f5c-199">IoT hubs</span><span class="sxs-lookup"><span data-stu-id="80f5c-199">IoT hubs</span></span>
* <span data-ttu-id="80f5c-200">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="80f5c-200">Redis Cache</span></span>
* <span data-ttu-id="80f5c-201">Networking: Application gateways</span><span class="sxs-lookup"><span data-stu-id="80f5c-201">Networking: Application gateways</span></span>
* <span data-ttu-id="80f5c-202">Search</span><span class="sxs-lookup"><span data-stu-id="80f5c-202">Search</span></span>

<span data-ttu-id="80f5c-203">You can view a detailed list of all the supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="80f5c-203">You can view a detailed list of all the supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80f5c-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="80f5c-204">Next steps</span></span>
<span data-ttu-id="80f5c-205">Refer to the links throughout this article.</span><span class="sxs-lookup"><span data-stu-id="80f5c-205">Refer to the links throughout this article.</span></span> <span data-ttu-id="80f5c-206">Additionally, learn about:</span><span class="sxs-lookup"><span data-stu-id="80f5c-206">Additionally, learn about:</span></span>  

* [<span data-ttu-id="80f5c-207">Common metrics for autoscaling</span><span class="sxs-lookup"><span data-stu-id="80f5c-207">Common metrics for autoscaling</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="80f5c-208">How to create alert rules</span><span class="sxs-lookup"><span data-stu-id="80f5c-208">How to create alert rules</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="80f5c-209">Analyze logs from Azure storage with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="80f5c-209">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)






