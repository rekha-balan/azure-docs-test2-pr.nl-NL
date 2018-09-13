---
title: Use Powershell to set alerts in Application Insights | Microsoft Docs
description: Automate configuration of Application Insights to get emails about metric changes.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: awills
ms.openlocfilehash: f479ae38e446c3404592901c416990ab6e39126b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553436"
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="56c2b-103">Use PowerShell to set alerts in Application Insights</span><span class="sxs-lookup"><span data-stu-id="56c2b-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="56c2b-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56c2b-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="56c2b-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="56c2b-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="56c2b-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="56c2b-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="56c2b-107">One-time setup</span><span class="sxs-lookup"><span data-stu-id="56c2b-107">One-time setup</span></span>
<span data-ttu-id="56c2b-108">If you haven't used PowerShell with your Azure subscription before:</span><span class="sxs-lookup"><span data-stu-id="56c2b-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="56c2b-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span><span class="sxs-lookup"><span data-stu-id="56c2b-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="56c2b-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="56c2b-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="56c2b-111">Use it to install Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="56c2b-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="56c2b-112">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="56c2b-112">Connect to Azure</span></span>
<span data-ttu-id="56c2b-113">Start Azure PowerShell and [connect to your subscription](/powershell/azureps-cmdlets-docs):</span><span class="sxs-lookup"><span data-stu-id="56c2b-113">Start Azure PowerShell and [connect to your subscription](/powershell/azureps-cmdlets-docs):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="56c2b-114">Get alerts</span><span class="sxs-lookup"><span data-stu-id="56c2b-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="56c2b-115">Add alert</span><span class="sxs-lookup"><span data-stu-id="56c2b-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="56c2b-116">Example 1</span><span class="sxs-lookup"><span data-stu-id="56c2b-116">Example 1</span></span>
<span data-ttu-id="56c2b-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span><span class="sxs-lookup"><span data-stu-id="56c2b-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="56c2b-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="56c2b-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="56c2b-119">I am the owner of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="56c2b-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="56c2b-120">The GUID is the subscription ID (not the instrumentation key of the application).</span><span class="sxs-lookup"><span data-stu-id="56c2b-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="56c2b-121">Example 2</span><span class="sxs-lookup"><span data-stu-id="56c2b-121">Example 2</span></span>
<span data-ttu-id="56c2b-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span><span class="sxs-lookup"><span data-stu-id="56c2b-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="56c2b-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span><span class="sxs-lookup"><span data-stu-id="56c2b-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="56c2b-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span><span class="sxs-lookup"><span data-stu-id="56c2b-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="56c2b-125">Metric names</span><span class="sxs-lookup"><span data-stu-id="56c2b-125">Metric names</span></span>
| <span data-ttu-id="56c2b-126">Metric name</span><span class="sxs-lookup"><span data-stu-id="56c2b-126">Metric name</span></span> | <span data-ttu-id="56c2b-127">Screen name</span><span class="sxs-lookup"><span data-stu-id="56c2b-127">Screen name</span></span> | <span data-ttu-id="56c2b-128">Description</span><span class="sxs-lookup"><span data-stu-id="56c2b-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="56c2b-129">Browser exceptions</span><span class="sxs-lookup"><span data-stu-id="56c2b-129">Browser exceptions</span></span> |<span data-ttu-id="56c2b-130">Count of uncaught exceptions thrown in the browser.</span><span class="sxs-lookup"><span data-stu-id="56c2b-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="56c2b-131">Server exceptions</span><span class="sxs-lookup"><span data-stu-id="56c2b-131">Server exceptions</span></span> |<span data-ttu-id="56c2b-132">Count of unhandled exceptions thrown by the app</span><span class="sxs-lookup"><span data-stu-id="56c2b-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="56c2b-133">Client processing time</span><span class="sxs-lookup"><span data-stu-id="56c2b-133">Client processing time</span></span> |<span data-ttu-id="56c2b-134">Time between receiving the last byte of a document until the DOM is loaded.</span><span class="sxs-lookup"><span data-stu-id="56c2b-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="56c2b-135">Async requests may still be processing.</span><span class="sxs-lookup"><span data-stu-id="56c2b-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="56c2b-136">Page load network connect time</span><span class="sxs-lookup"><span data-stu-id="56c2b-136">Page load network connect time</span></span> |<span data-ttu-id="56c2b-137">Time the browser takes to connect to the network.</span><span class="sxs-lookup"><span data-stu-id="56c2b-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="56c2b-138">Can be 0 if cached.</span><span class="sxs-lookup"><span data-stu-id="56c2b-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="56c2b-139">Receiving response time</span><span class="sxs-lookup"><span data-stu-id="56c2b-139">Receiving response time</span></span> |<span data-ttu-id="56c2b-140">Time between browser sending request to starting to receive response.</span><span class="sxs-lookup"><span data-stu-id="56c2b-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="56c2b-141">Send request time</span><span class="sxs-lookup"><span data-stu-id="56c2b-141">Send request time</span></span> |<span data-ttu-id="56c2b-142">Time taken by browser to send request.</span><span class="sxs-lookup"><span data-stu-id="56c2b-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="56c2b-143">Browser page load time</span><span class="sxs-lookup"><span data-stu-id="56c2b-143">Browser page load time</span></span> |<span data-ttu-id="56c2b-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span><span class="sxs-lookup"><span data-stu-id="56c2b-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="56c2b-145">Available memory</span><span class="sxs-lookup"><span data-stu-id="56c2b-145">Available memory</span></span> |<span data-ttu-id="56c2b-146">Physical memory immediately available for a process or for system use.</span><span class="sxs-lookup"><span data-stu-id="56c2b-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="56c2b-147">Process IO Rate</span><span class="sxs-lookup"><span data-stu-id="56c2b-147">Process IO Rate</span></span> |<span data-ttu-id="56c2b-148">Total bytes per second read and written to files, network and devices.</span><span class="sxs-lookup"><span data-stu-id="56c2b-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="56c2b-149">exception rate</span><span class="sxs-lookup"><span data-stu-id="56c2b-149">exception rate</span></span> |<span data-ttu-id="56c2b-150">Exceptions thrown per second.</span><span class="sxs-lookup"><span data-stu-id="56c2b-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="56c2b-151">Process CPU</span><span class="sxs-lookup"><span data-stu-id="56c2b-151">Process CPU</span></span> |<span data-ttu-id="56c2b-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span><span class="sxs-lookup"><span data-stu-id="56c2b-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="56c2b-153">Processor time</span><span class="sxs-lookup"><span data-stu-id="56c2b-153">Processor time</span></span> |<span data-ttu-id="56c2b-154">The percentage of time that the processor spends in non-Idle threads.</span><span class="sxs-lookup"><span data-stu-id="56c2b-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="56c2b-155">Process private bytes</span><span class="sxs-lookup"><span data-stu-id="56c2b-155">Process private bytes</span></span> |<span data-ttu-id="56c2b-156">Memory exclusively assigned to the monitored application's processes.</span><span class="sxs-lookup"><span data-stu-id="56c2b-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="56c2b-157">ASP.NET request execution time</span><span class="sxs-lookup"><span data-stu-id="56c2b-157">ASP.NET request execution time</span></span> |<span data-ttu-id="56c2b-158">Execution time of the most recent request.</span><span class="sxs-lookup"><span data-stu-id="56c2b-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="56c2b-159">ASP.NET requests in execution queue</span><span class="sxs-lookup"><span data-stu-id="56c2b-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="56c2b-160">Length of the application request queue.</span><span class="sxs-lookup"><span data-stu-id="56c2b-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="56c2b-161">ASP.NET request rate</span><span class="sxs-lookup"><span data-stu-id="56c2b-161">ASP.NET request rate</span></span> |<span data-ttu-id="56c2b-162">Rate of all requests to the application per second from ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="56c2b-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="56c2b-163">Dependency failures</span><span class="sxs-lookup"><span data-stu-id="56c2b-163">Dependency failures</span></span> |<span data-ttu-id="56c2b-164">Count of failed calls made by the server application to external resources.</span><span class="sxs-lookup"><span data-stu-id="56c2b-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="56c2b-165">Server response time</span><span class="sxs-lookup"><span data-stu-id="56c2b-165">Server response time</span></span> |<span data-ttu-id="56c2b-166">Time between receiving an HTTP request and finishing sending the response.</span><span class="sxs-lookup"><span data-stu-id="56c2b-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="56c2b-167">Request rate</span><span class="sxs-lookup"><span data-stu-id="56c2b-167">Request rate</span></span> |<span data-ttu-id="56c2b-168">Rate of all requests to the application per second.</span><span class="sxs-lookup"><span data-stu-id="56c2b-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="56c2b-169">Failed requests</span><span class="sxs-lookup"><span data-stu-id="56c2b-169">Failed requests</span></span> |<span data-ttu-id="56c2b-170">Count of HTTP requests that resulted in a response code >= 400</span><span class="sxs-lookup"><span data-stu-id="56c2b-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="56c2b-171">Page views</span><span class="sxs-lookup"><span data-stu-id="56c2b-171">Page views</span></span> |<span data-ttu-id="56c2b-172">Count of client user requests for a web page.</span><span class="sxs-lookup"><span data-stu-id="56c2b-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="56c2b-173">Synthetic traffic is filtered out.</span><span class="sxs-lookup"><span data-stu-id="56c2b-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="56c2b-174">{your custom metric name}</span><span class="sxs-lookup"><span data-stu-id="56c2b-174">{your custom metric name}</span></span> |<span data-ttu-id="56c2b-175">{Your metric name}</span><span class="sxs-lookup"><span data-stu-id="56c2b-175">{Your metric name}</span></span> |<span data-ttu-id="56c2b-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="56c2b-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="56c2b-177">The metrics are sent by different telemetry modules:</span><span class="sxs-lookup"><span data-stu-id="56c2b-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="56c2b-178">Metric group</span><span class="sxs-lookup"><span data-stu-id="56c2b-178">Metric group</span></span> | <span data-ttu-id="56c2b-179">Collector module</span><span class="sxs-lookup"><span data-stu-id="56c2b-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="56c2b-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="56c2b-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="56c2b-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="56c2b-181">clientPerformance,</span></span><br/><span data-ttu-id="56c2b-182">view</span><span class="sxs-lookup"><span data-stu-id="56c2b-182">view</span></span> |[<span data-ttu-id="56c2b-183">Browser JavaScript</span><span class="sxs-lookup"><span data-stu-id="56c2b-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="56c2b-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="56c2b-184">performanceCounter</span></span> |[<span data-ttu-id="56c2b-185">Performance</span><span class="sxs-lookup"><span data-stu-id="56c2b-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="56c2b-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="56c2b-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="56c2b-187">Dependency</span><span class="sxs-lookup"><span data-stu-id="56c2b-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="56c2b-188">request,</span><span class="sxs-lookup"><span data-stu-id="56c2b-188">request,</span></span><br/><span data-ttu-id="56c2b-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="56c2b-189">requestFailed</span></span> |[<span data-ttu-id="56c2b-190">Server request</span><span class="sxs-lookup"><span data-stu-id="56c2b-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="56c2b-191">Webhooks</span><span class="sxs-lookup"><span data-stu-id="56c2b-191">Webhooks</span></span>
<span data-ttu-id="56c2b-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="56c2b-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="56c2b-193">Azure will call a web address of your choice when an alert is raised.</span><span class="sxs-lookup"><span data-stu-id="56c2b-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="56c2b-194">See also</span><span class="sxs-lookup"><span data-stu-id="56c2b-194">See also</span></span>
* [<span data-ttu-id="56c2b-195">Script to configure Application Insights</span><span class="sxs-lookup"><span data-stu-id="56c2b-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="56c2b-196">Create Application Insights and web test resources from templates</span><span class="sxs-lookup"><span data-stu-id="56c2b-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="56c2b-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span><span class="sxs-lookup"><span data-stu-id="56c2b-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="56c2b-198">Automate your response to an alert</span><span class="sxs-lookup"><span data-stu-id="56c2b-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
