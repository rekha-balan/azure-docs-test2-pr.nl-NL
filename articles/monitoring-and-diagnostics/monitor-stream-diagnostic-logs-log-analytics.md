---
title: Stream Azure Diagnostic Logs to Log Analytics
description: Learn how to stream Azure diagnostic logs to a Log Analytics workspace.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 04/04/2018
ms.author: johnkem
ms.component: logs
ms.openlocfilehash: d8966edb6061ed07f5aecb9682fca081ed589040
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871335"
---
# <a name="stream-azure-diagnostic-logs-to-log-analytics"></a><span data-ttu-id="c99d1-103">Stream Azure Diagnostic Logs to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c99d1-103">Stream Azure Diagnostic Logs to Log Analytics</span></span>

<span data-ttu-id="c99d1-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to Azure Log Analytics using the portal, PowerShell cmdlets or Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c99d1-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to Azure Log Analytics using the portal, PowerShell cmdlets or Azure CLI 2.0.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-in-log-analytics"></a><span data-ttu-id="c99d1-105">What you can do with diagnostics logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c99d1-105">What you can do with diagnostics logs in Log Analytics</span></span>

<span data-ttu-id="c99d1-106">Azure Log Analytics is a flexible log search and analytics tool that enables you to gain insight into the raw log data generated from Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c99d1-106">Azure Log Analytics is a flexible log search and analytics tool that enables you to gain insight into the raw log data generated from Azure resources.</span></span> <span data-ttu-id="c99d1-107">Some capabilities include:</span><span class="sxs-lookup"><span data-stu-id="c99d1-107">Some capabilities include:</span></span>

* <span data-ttu-id="c99d1-108">**Log search** - Write advanced queries over your log data, correlate logs from various sources, and even generate charts that can be pinned to your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="c99d1-108">**Log search** - Write advanced queries over your log data, correlate logs from various sources, and even generate charts that can be pinned to your Azure dashboard.</span></span>
* <span data-ttu-id="c99d1-109">**Alerting** - Detect when one or more events match a particular query and become notified with an email or webhook call.</span><span class="sxs-lookup"><span data-stu-id="c99d1-109">**Alerting** - Detect when one or more events match a particular query and become notified with an email or webhook call.</span></span>
* <span data-ttu-id="c99d1-110">**Solutions** - Use pre-built views and dashboards that give you immediate insight into your log data.</span><span class="sxs-lookup"><span data-stu-id="c99d1-110">**Solutions** - Use pre-built views and dashboards that give you immediate insight into your log data.</span></span>
* <span data-ttu-id="c99d1-111">**Advanced analytics** - Apply machine learning and pattern matching algorithms to identify possible issues revealed by your logs.</span><span class="sxs-lookup"><span data-stu-id="c99d1-111">**Advanced analytics** - Apply machine learning and pattern matching algorithms to identify possible issues revealed by your logs.</span></span>

## <a name="enable-streaming-of-diagnostic-logs-to-log-analytics"></a><span data-ttu-id="c99d1-112">Enable streaming of diagnostic logs to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c99d1-112">Enable streaming of diagnostic logs to Log Analytics</span></span>

<span data-ttu-id="c99d1-113">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/en-us/rest/api/monitor/diagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="c99d1-113">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/en-us/rest/api/monitor/diagnosticsettings).</span></span> <span data-ttu-id="c99d1-114">Either way, you create a diagnostic setting in which you specify a Log Analytics workspace and the log categories and metrics you want to send in to that workspace.</span><span class="sxs-lookup"><span data-stu-id="c99d1-114">Either way, you create a diagnostic setting in which you specify a Log Analytics workspace and the log categories and metrics you want to send in to that workspace.</span></span> <span data-ttu-id="c99d1-115">A diagnostic **log category** is a type of log that a resource may provide.</span><span class="sxs-lookup"><span data-stu-id="c99d1-115">A diagnostic **log category** is a type of log that a resource may provide.</span></span>

<span data-ttu-id="c99d1-116">The Log Analytics workspace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c99d1-116">The Log Analytics workspace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

> [!NOTE]
> <span data-ttu-id="c99d1-117">Sending multi-dimensional metrics via diagnostic settings is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="c99d1-117">Sending multi-dimensional metrics via diagnostic settings is not currently supported.</span></span> <span data-ttu-id="c99d1-118">Metrics with dimensions are exported as flattened single dimensional metrics, aggregated across dimension values.</span><span class="sxs-lookup"><span data-stu-id="c99d1-118">Metrics with dimensions are exported as flattened single dimensional metrics, aggregated across dimension values.</span></span>
>
> <span data-ttu-id="c99d1-119">*For example*: The 'Incoming Messages' metric on an Event Hub can be explored and charted on a per queue level.</span><span class="sxs-lookup"><span data-stu-id="c99d1-119">*For example*: The 'Incoming Messages' metric on an Event Hub can be explored and charted on a per queue level.</span></span> <span data-ttu-id="c99d1-120">However, when exported via diagnostic settings the metric will be represented as all incoming messages across all queues in the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="c99d1-120">However, when exported via diagnostic settings the metric will be represented as all incoming messages across all queues in the Event Hub.</span></span>
>
>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="c99d1-121">Stream diagnostic logs using the portal</span><span class="sxs-lookup"><span data-stu-id="c99d1-121">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="c99d1-122">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span><span class="sxs-lookup"><span data-stu-id="c99d1-122">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Monitoring section of Azure Monitor](media/monitoring-stream-diagnostic-logs-to-log-analytics/diagnostic-settings-blade.png)

2. <span data-ttu-id="c99d1-124">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span><span class="sxs-lookup"><span data-stu-id="c99d1-124">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="c99d1-125">If no settings exist on the resource you have selected, you are prompted to create a setting.</span><span class="sxs-lookup"><span data-stu-id="c99d1-125">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="c99d1-126">Click "Turn on diagnostics."</span><span class="sxs-lookup"><span data-stu-id="c99d1-126">Click "Turn on diagnostics."</span></span>

   ![Add diagnostic setting - no existing settings](media/monitoring-stream-diagnostic-logs-to-log-analytics/diagnostic-settings-none.png)

   <span data-ttu-id="c99d1-128">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span><span class="sxs-lookup"><span data-stu-id="c99d1-128">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="c99d1-129">Click "Add diagnostic setting."</span><span class="sxs-lookup"><span data-stu-id="c99d1-129">Click "Add diagnostic setting."</span></span>

   ![Add diagnostic setting - existing settings](media/monitoring-stream-diagnostic-logs-to-log-analytics/diagnostic-settings-multiple.png)

3. <span data-ttu-id="c99d1-131">Give your setting a name and check the box for **Send to Log Analytics**, then select a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="c99d1-131">Give your setting a name and check the box for **Send to Log Analytics**, then select a Log Analytics workspace.</span></span>

   ![Add diagnostic setting - existing settings](media/monitoring-stream-diagnostic-logs-to-log-analytics/diagnostic-settings-configure.png)

4. <span data-ttu-id="c99d1-133">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c99d1-133">Click **Save**.</span></span>

<span data-ttu-id="c99d1-134">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that workspace as soon as new event data is generated.</span><span class="sxs-lookup"><span data-stu-id="c99d1-134">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that workspace as soon as new event data is generated.</span></span> <span data-ttu-id="c99d1-135">Note that there may be up to fifteen minutes between when an event is emitted and when it appears in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c99d1-135">Note that there may be up to fifteen minutes between when an event is emitted and when it appears in Log Analytics.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="c99d1-136">Via PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="c99d1-136">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="c99d1-137">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span><span class="sxs-lookup"><span data-stu-id="c99d1-137">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -WorkspaceID [resource ID of the Log Analytics workspace] -Categories [list of log categories] -Enabled $true
```

<span data-ttu-id="c99d1-138">Note that the workspaceID property takes the full Azure resource ID of the workspace, not the workspace ID/key shown in the Log Analytics portal.</span><span class="sxs-lookup"><span data-stu-id="c99d1-138">Note that the workspaceID property takes the full Azure resource ID of the workspace, not the workspace ID/key shown in the Log Analytics portal.</span></span>

### <a name="via-azure-cli-20"></a><span data-ttu-id="c99d1-139">Via Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c99d1-139">Via Azure CLI 2.0</span></span>

<span data-ttu-id="c99d1-140">To enable streaming via the [Azure CLI 2.0](insights-cli-samples.md), you can use the [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings#az-monitor-diagnostic-settings-create) command.</span><span class="sxs-lookup"><span data-stu-id="c99d1-140">To enable streaming via the [Azure CLI 2.0](insights-cli-samples.md), you can use the [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings#az-monitor-diagnostic-settings-create) command.</span></span>

```azurecli
az monitor diagnostic-settings create --name <diagnostic name> \
    --workspace <log analytics name or object ID> \
    --resource <target resource object ID> \
    --resource-group <log analytics workspace resource group> \
    --logs '[
    {
        "category": <category name>,
        "enabled": true
    }
    ]'
```

<span data-ttu-id="c99d1-141">You can add additional categories to the diagnostic log by adding dictionaries to the JSON array passed as the `--logs` parameter.</span><span class="sxs-lookup"><span data-stu-id="c99d1-141">You can add additional categories to the diagnostic log by adding dictionaries to the JSON array passed as the `--logs` parameter.</span></span>

<span data-ttu-id="c99d1-142">The `--resource-group` argument is only required if `--workspace` is not an object ID.</span><span class="sxs-lookup"><span data-stu-id="c99d1-142">The `--resource-group` argument is only required if `--workspace` is not an object ID.</span></span>

## <a name="how-do-i-query-the-data-in-log-analytics"></a><span data-ttu-id="c99d1-143">How do I query the data in Log Analytics?</span><span class="sxs-lookup"><span data-stu-id="c99d1-143">How do I query the data in Log Analytics?</span></span>

<span data-ttu-id="c99d1-144">In the Log Search blade in the portal or Advanced Analytics experience as part of Log Analytics, you can query diagnostic logs as part of the Log Management solution under the AzureDiagnostics table.</span><span class="sxs-lookup"><span data-stu-id="c99d1-144">In the Log Search blade in the portal or Advanced Analytics experience as part of Log Analytics, you can query diagnostic logs as part of the Log Management solution under the AzureDiagnostics table.</span></span> <span data-ttu-id="c99d1-145">There are also [several solutions for Azure resources](../log-analytics/log-analytics-add-solutions.md) you can install to get immediate insight into the log data you are sending into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c99d1-145">There are also [several solutions for Azure resources](../log-analytics/log-analytics-add-solutions.md) you can install to get immediate insight into the log data you are sending into Log Analytics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c99d1-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="c99d1-146">Next steps</span></span>

* [<span data-ttu-id="c99d1-147">Read more about Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="c99d1-147">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
