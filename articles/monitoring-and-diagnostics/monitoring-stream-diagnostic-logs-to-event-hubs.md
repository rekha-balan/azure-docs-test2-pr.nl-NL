---
title: Stream Azure Diagnostic Logs to Event Hubs | Microsoft Docs
description: Learn how to stream Azure Diagnostic Logs to Event Hubs.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 9d7c98b3131be5fd88351c44732a6b7b498d593a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555765"
---
# <a name="stream-azure-diagnostic-logs-to-event-hubs"></a><span data-ttu-id="cd516-103">Stream Azure Diagnostic Logs to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd516-103">Stream Azure Diagnostic Logs to Event Hubs</span></span>
<span data-ttu-id="cd516-104">**[Azure Diagnostic Logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule Id in a Diagnostic Setting via the Azure PowerShell Cmdlets or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cd516-104">**[Azure Diagnostic Logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule Id in a Diagnostic Setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="cd516-105">What you can do with Diagnostics Logs and Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd516-105">What you can do with Diagnostics Logs and Event Hubs</span></span>
<span data-ttu-id="cd516-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span><span class="sxs-lookup"><span data-stu-id="cd516-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="cd516-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Diagnostic Logs into third party SIEMs and log analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="cd516-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Diagnostic Logs into third party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="cd516-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data into near real-time insights on your Azure services.</span><span class="sxs-lookup"><span data-stu-id="cd516-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="cd516-109">[This documentation article gives a great overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="cd516-109">[This documentation article gives a great overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="cd516-110">Here’s a few tips for getting set up with Diagnostic Logs:</span><span class="sxs-lookup"><span data-stu-id="cd516-110">Here’s a few tips for getting set up with Diagnostic Logs:</span></span>
  
  * <span data-ttu-id="cd516-111">The Event Hubs for a category of Diagnostic Logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the Event Hubs in the Service Bus namespace with the name that starts with “insights-”</span><span class="sxs-lookup"><span data-stu-id="cd516-111">The Event Hubs for a category of Diagnostic Logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the Event Hubs in the Service Bus namespace with the name that starts with “insights-”</span></span>
  * <span data-ttu-id="cd516-112">Here’s a sample Stream Analytics query you can use to simply parse all the log data in to a PowerBI table:</span><span class="sxs-lookup"><span data-stu-id="cd516-112">Here’s a sample Stream Analytics query you can use to simply parse all the log data in to a PowerBI table:</span></span>

```
SELECT
records.ArrayValue.[Properties you want to track]
INTO
[OutputSourceName – the PowerBI source]
FROM
[InputSourceName] AS e
CROSS APPLY GetArrayElements(e.records) AS records
```

* <span data-ttu-id="cd516-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="cd516-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="cd516-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="cd516-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="cd516-115">Enable streaming of Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="cd516-115">Enable streaming of Diagnostic Logs</span></span>
<span data-ttu-id="cd516-116">You can enable streaming of Diagnostic Logs programmatically, via the portal, or using the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd516-116">You can enable streaming of Diagnostic Logs programmatically, via the portal, or using the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="cd516-117">Either way, you pick a Service Bus Namespace and an Event Hubs is created in the namespace for each log category you enable.</span><span class="sxs-lookup"><span data-stu-id="cd516-117">Either way, you pick a Service Bus Namespace and an Event Hubs is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="cd516-118">A Diagnostic **Log Category** is a type of log that a resource may collect.</span><span class="sxs-lookup"><span data-stu-id="cd516-118">A Diagnostic **Log Category** is a type of log that a resource may collect.</span></span> <span data-ttu-id="cd516-119">You can select which log categories you’d like to collect for a particular resource in the Azure Portal under the Diagnostics blade.</span><span class="sxs-lookup"><span data-stu-id="cd516-119">You can select which log categories you’d like to collect for a particular resource in the Azure Portal under the Diagnostics blade.</span></span>

![Log categories in the Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-stream-diagnostic-logs-to-event-hubs/log-categories.png)

> [!WARNING]
> <span data-ttu-id="cd516-121">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="cd516-121">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="cd516-122">The service bus or event hub namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="cd516-122">The service bus or event hub namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="cd516-123">Via PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="cd516-123">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="cd516-124">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span><span class="sxs-lookup"><span data-stu-id="cd516-124">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```
Set-AzureRmDiagnosticSetting -ResourceId [your resource Id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
```

<span data-ttu-id="cd516-125">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{service bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="cd516-125">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{service bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="cd516-126">Via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cd516-126">Via Azure CLI</span></span>
<span data-ttu-id="cd516-127">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span><span class="sxs-lookup"><span data-stu-id="cd516-127">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="cd516-128">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd516-128">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="cd516-129">Via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cd516-129">Via Azure Portal</span></span>
<span data-ttu-id="cd516-130">To enable streaming via the Azure Portal, navigate to the diagnostics settings of a resource and select ‘Export to Event Hub.’</span><span class="sxs-lookup"><span data-stu-id="cd516-130">To enable streaming via the Azure Portal, navigate to the diagnostics settings of a resource and select ‘Export to Event Hub.’</span></span>

![Export to Event Hubs in the Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-stream-diagnostic-logs-to-event-hubs/portal-export.png)

<span data-ttu-id="cd516-132">To configure it, select an existing Service Bus Namespace.</span><span class="sxs-lookup"><span data-stu-id="cd516-132">To configure it, select an existing Service Bus Namespace.</span></span> <span data-ttu-id="cd516-133">The namespace selected will be where the Event Hubs is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span><span class="sxs-lookup"><span data-stu-id="cd516-133">The namespace selected will be where the Event Hubs is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="cd516-134">Today, streaming to an Event Hubs requires Manage, Send, and Listen permissions.</span><span class="sxs-lookup"><span data-stu-id="cd516-134">Today, streaming to an Event Hubs requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="cd516-135">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span><span class="sxs-lookup"><span data-stu-id="cd516-135">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="cd516-136">To update one of these Diagnostic Settings, the client must have the ListKey permission on the Service Bus Authorization Rule.</span><span class="sxs-lookup"><span data-stu-id="cd516-136">To update one of these Diagnostic Settings, the client must have the ListKey permission on the Service Bus Authorization Rule.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="cd516-137">How do I consume the log data from Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="cd516-137">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="cd516-138">Here is sample output data from the Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="cd516-138">Here is sample output data from the Event Hubs:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="cd516-139">Element Name</span><span class="sxs-lookup"><span data-stu-id="cd516-139">Element Name</span></span> | <span data-ttu-id="cd516-140">Description</span><span class="sxs-lookup"><span data-stu-id="cd516-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd516-141">records</span><span class="sxs-lookup"><span data-stu-id="cd516-141">records</span></span> |<span data-ttu-id="cd516-142">An array of all log events in this payload.</span><span class="sxs-lookup"><span data-stu-id="cd516-142">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="cd516-143">time</span><span class="sxs-lookup"><span data-stu-id="cd516-143">time</span></span> |<span data-ttu-id="cd516-144">Time at which the event occurred.</span><span class="sxs-lookup"><span data-stu-id="cd516-144">Time at which the event occurred.</span></span> |
| <span data-ttu-id="cd516-145">category</span><span class="sxs-lookup"><span data-stu-id="cd516-145">category</span></span> |<span data-ttu-id="cd516-146">Log category for this event.</span><span class="sxs-lookup"><span data-stu-id="cd516-146">Log category for this event.</span></span> |
| <span data-ttu-id="cd516-147">resourceId</span><span class="sxs-lookup"><span data-stu-id="cd516-147">resourceId</span></span> |<span data-ttu-id="cd516-148">Resource ID of the resource that generated this event.</span><span class="sxs-lookup"><span data-stu-id="cd516-148">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="cd516-149">operationName</span><span class="sxs-lookup"><span data-stu-id="cd516-149">operationName</span></span> |<span data-ttu-id="cd516-150">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="cd516-150">Name of the operation.</span></span> |
| <span data-ttu-id="cd516-151">level</span><span class="sxs-lookup"><span data-stu-id="cd516-151">level</span></span> |<span data-ttu-id="cd516-152">Optional.</span><span class="sxs-lookup"><span data-stu-id="cd516-152">Optional.</span></span> <span data-ttu-id="cd516-153">Indicates the log event level.</span><span class="sxs-lookup"><span data-stu-id="cd516-153">Indicates the log event level.</span></span> |
| <span data-ttu-id="cd516-154">properties</span><span class="sxs-lookup"><span data-stu-id="cd516-154">properties</span></span> |<span data-ttu-id="cd516-155">Properties of the event.</span><span class="sxs-lookup"><span data-stu-id="cd516-155">Properties of the event.</span></span> |

<span data-ttu-id="cd516-156">You can view a list of all resource providers that support streaming to Event Hub [here](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="cd516-156">You can view a list of all resource providers that support streaming to Event Hub [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="cd516-157">Stream data from Compute resources</span><span class="sxs-lookup"><span data-stu-id="cd516-157">Stream data from Compute resources</span></span>
<span data-ttu-id="cd516-158">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnositcs agent.</span><span class="sxs-lookup"><span data-stu-id="cd516-158">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnositcs agent.</span></span> <span data-ttu-id="cd516-159">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span><span class="sxs-lookup"><span data-stu-id="cd516-159">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd516-160">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cd516-160">Next Steps</span></span>
* [<span data-ttu-id="cd516-161">Read more about Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="cd516-161">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="cd516-162">Get started with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd516-162">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)



