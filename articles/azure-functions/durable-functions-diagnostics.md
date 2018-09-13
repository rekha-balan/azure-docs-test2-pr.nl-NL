---
title: Diagnostics in Durable Functions - Azure
description: Learn how to diagnose problems with the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/30/2018
ms.author: azfuncdf
ms.openlocfilehash: e1211241ec3a2b32647260d1a5c7dc561019cfdf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866892"
---
# <a name="diagnostics-in-durable-functions-azure-functions"></a><span data-ttu-id="56e52-103">Diagnostics in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="56e52-103">Diagnostics in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="56e52-104">There are several options for diagnosing issues with [Durable Functions](durable-functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56e52-104">There are several options for diagnosing issues with [Durable Functions](durable-functions-overview.md).</span></span> <span data-ttu-id="56e52-105">Some of these options are the same for regular functions and some of them are unique to Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="56e52-105">Some of these options are the same for regular functions and some of them are unique to Durable Functions.</span></span>

## <a name="application-insights"></a><span data-ttu-id="56e52-106">Application Insights</span><span class="sxs-lookup"><span data-stu-id="56e52-106">Application Insights</span></span>

<span data-ttu-id="56e52-107">[Application Insights](../application-insights/app-insights-overview.md) is the recommended way to do diagnostics and monitoring in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="56e52-107">[Application Insights](../application-insights/app-insights-overview.md) is the recommended way to do diagnostics and monitoring in Azure Functions.</span></span> <span data-ttu-id="56e52-108">The same applies to Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="56e52-108">The same applies to Durable Functions.</span></span> <span data-ttu-id="56e52-109">For an overview of how to leverage Application Insights in your function app, see [Monitor Azure Functions](functions-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="56e52-109">For an overview of how to leverage Application Insights in your function app, see [Monitor Azure Functions](functions-monitoring.md).</span></span>

<span data-ttu-id="56e52-110">The Azure Functions Durable Extension also emits *tracking events* that allow you to trace the end-to-end execution of an orchestration.</span><span class="sxs-lookup"><span data-stu-id="56e52-110">The Azure Functions Durable Extension also emits *tracking events* that allow you to trace the end-to-end execution of an orchestration.</span></span> <span data-ttu-id="56e52-111">These can be found and queried using the [Application Insights Analytics](../application-insights/app-insights-analytics.md) tool in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56e52-111">These can be found and queried using the [Application Insights Analytics](../application-insights/app-insights-analytics.md) tool in the Azure portal.</span></span>

### <a name="tracking-data"></a><span data-ttu-id="56e52-112">Tracking data</span><span class="sxs-lookup"><span data-stu-id="56e52-112">Tracking data</span></span>

<span data-ttu-id="56e52-113">Each lifecycle event of an orchestration instance causes a tracking event to be written to the **traces** collection in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="56e52-113">Each lifecycle event of an orchestration instance causes a tracking event to be written to the **traces** collection in Application Insights.</span></span> <span data-ttu-id="56e52-114">This event contains a **customDimensions** payload with several fields.</span><span class="sxs-lookup"><span data-stu-id="56e52-114">This event contains a **customDimensions** payload with several fields.</span></span>  <span data-ttu-id="56e52-115">Field names are all prepended with `prop__`.</span><span class="sxs-lookup"><span data-stu-id="56e52-115">Field names are all prepended with `prop__`.</span></span>

* <span data-ttu-id="56e52-116">**hubName**: The name of the task hub in which your orchestrations are running.</span><span class="sxs-lookup"><span data-stu-id="56e52-116">**hubName**: The name of the task hub in which your orchestrations are running.</span></span>
* <span data-ttu-id="56e52-117">**appName**: The name of the function app.</span><span class="sxs-lookup"><span data-stu-id="56e52-117">**appName**: The name of the function app.</span></span> <span data-ttu-id="56e52-118">This is useful when you have multiple function apps sharing the same Application Insights instance.</span><span class="sxs-lookup"><span data-stu-id="56e52-118">This is useful when you have multiple function apps sharing the same Application Insights instance.</span></span>
* <span data-ttu-id="56e52-119">**slotName**: The [deployment slot](https://blogs.msdn.microsoft.com/appserviceteam/2017/06/13/deployment-slots-preview-for-azure-functions/) in which the current function app is running.</span><span class="sxs-lookup"><span data-stu-id="56e52-119">**slotName**: The [deployment slot](https://blogs.msdn.microsoft.com/appserviceteam/2017/06/13/deployment-slots-preview-for-azure-functions/) in which the current function app is running.</span></span> <span data-ttu-id="56e52-120">This is useful when you leverage deployment slots to version your orchestrations.</span><span class="sxs-lookup"><span data-stu-id="56e52-120">This is useful when you leverage deployment slots to version your orchestrations.</span></span>
* <span data-ttu-id="56e52-121">**functionName**: The name of the orchestrator or activity function.</span><span class="sxs-lookup"><span data-stu-id="56e52-121">**functionName**: The name of the orchestrator or activity function.</span></span>
* <span data-ttu-id="56e52-122">**functionType**: The type of the function, such as **Orchestrator** or **Activity**.</span><span class="sxs-lookup"><span data-stu-id="56e52-122">**functionType**: The type of the function, such as **Orchestrator** or **Activity**.</span></span>
* <span data-ttu-id="56e52-123">**instanceId**: The unique ID of the orchestration instance.</span><span class="sxs-lookup"><span data-stu-id="56e52-123">**instanceId**: The unique ID of the orchestration instance.</span></span>
* <span data-ttu-id="56e52-124">**state**: The lifecycle execution state of the instance.</span><span class="sxs-lookup"><span data-stu-id="56e52-124">**state**: The lifecycle execution state of the instance.</span></span> <span data-ttu-id="56e52-125">Valid values include:</span><span class="sxs-lookup"><span data-stu-id="56e52-125">Valid values include:</span></span>
    * <span data-ttu-id="56e52-126">**Scheduled**: The function was scheduled for execution but hasn't started running yet.</span><span class="sxs-lookup"><span data-stu-id="56e52-126">**Scheduled**: The function was scheduled for execution but hasn't started running yet.</span></span>
    * <span data-ttu-id="56e52-127">**Started**: The function has started running but has not yet awaited or completed.</span><span class="sxs-lookup"><span data-stu-id="56e52-127">**Started**: The function has started running but has not yet awaited or completed.</span></span>
    * <span data-ttu-id="56e52-128">**Awaited**: The orchestrator has scheduled some work and is waiting for it to complete.</span><span class="sxs-lookup"><span data-stu-id="56e52-128">**Awaited**: The orchestrator has scheduled some work and is waiting for it to complete.</span></span>
    * <span data-ttu-id="56e52-129">**Listening**: The orchestrator is listening for an external event notification.</span><span class="sxs-lookup"><span data-stu-id="56e52-129">**Listening**: The orchestrator is listening for an external event notification.</span></span>
    * <span data-ttu-id="56e52-130">**Completed**: The function has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="56e52-130">**Completed**: The function has completed successfully.</span></span>
    * <span data-ttu-id="56e52-131">**Failed**: The function failed with an error.</span><span class="sxs-lookup"><span data-stu-id="56e52-131">**Failed**: The function failed with an error.</span></span>
* <span data-ttu-id="56e52-132">**reason**: Additional data associated with the tracking event.</span><span class="sxs-lookup"><span data-stu-id="56e52-132">**reason**: Additional data associated with the tracking event.</span></span> <span data-ttu-id="56e52-133">For example, if an instance is waiting for an external event notification, this field indicates the name of the event it is waiting for.</span><span class="sxs-lookup"><span data-stu-id="56e52-133">For example, if an instance is waiting for an external event notification, this field indicates the name of the event it is waiting for.</span></span> <span data-ttu-id="56e52-134">If a function has failed, this will contain the error details.</span><span class="sxs-lookup"><span data-stu-id="56e52-134">If a function has failed, this will contain the error details.</span></span>
* <span data-ttu-id="56e52-135">**isReplay**: Boolean value indicating whether the tracking event is for replayed execution.</span><span class="sxs-lookup"><span data-stu-id="56e52-135">**isReplay**: Boolean value indicating whether the tracking event is for replayed execution.</span></span>
* <span data-ttu-id="56e52-136">**extensionVersion**: The version of the Durable Task extension.</span><span class="sxs-lookup"><span data-stu-id="56e52-136">**extensionVersion**: The version of the Durable Task extension.</span></span> <span data-ttu-id="56e52-137">This is especially important data when reporting possible bugs in the extension.</span><span class="sxs-lookup"><span data-stu-id="56e52-137">This is especially important data when reporting possible bugs in the extension.</span></span> <span data-ttu-id="56e52-138">Long-running instances may report multiple versions if an update occurs while it is running.</span><span class="sxs-lookup"><span data-stu-id="56e52-138">Long-running instances may report multiple versions if an update occurs while it is running.</span></span> 
* <span data-ttu-id="56e52-139">**sequenceNumber**: Execution sequence number for an event.</span><span class="sxs-lookup"><span data-stu-id="56e52-139">**sequenceNumber**: Execution sequence number for an event.</span></span> <span data-ttu-id="56e52-140">Combined with the timestamp helps to order the events by execution time.</span><span class="sxs-lookup"><span data-stu-id="56e52-140">Combined with the timestamp helps to order the events by execution time.</span></span> <span data-ttu-id="56e52-141">*Note that this number will be reset to zero if the host restarts while the instance is running, so it's important to always sort by timestamp first, then sequenceNumber.*</span><span class="sxs-lookup"><span data-stu-id="56e52-141">*Note that this number will be reset to zero if the host restarts while the instance is running, so it's important to always sort by timestamp first, then sequenceNumber.*</span></span>

<span data-ttu-id="56e52-142">The verbosity of tracking data emitted to Application Insights can be configured in the `logger` section of the `host.json` file.</span><span class="sxs-lookup"><span data-stu-id="56e52-142">The verbosity of tracking data emitted to Application Insights can be configured in the `logger` section of the `host.json` file.</span></span>

```json
{
    "logger": {
        "categoryFilter": {
            "categoryLevels": {
                "Host.Triggers.DurableTask": "Information"
            }
        }
    }
}
```

<span data-ttu-id="56e52-143">By default, all non-replay tracking events are emitted.</span><span class="sxs-lookup"><span data-stu-id="56e52-143">By default, all non-replay tracking events are emitted.</span></span> <span data-ttu-id="56e52-144">The volume of data can be reduced by setting `Host.Triggers.DurableTask` to `"Warning"` or `"Error"` in which case tracking events will only be emitted for exceptional situations.</span><span class="sxs-lookup"><span data-stu-id="56e52-144">The volume of data can be reduced by setting `Host.Triggers.DurableTask` to `"Warning"` or `"Error"` in which case tracking events will only be emitted for exceptional situations.</span></span>

<span data-ttu-id="56e52-145">To enable emitting the verbose orchestration replay events, the `LogReplayEvents` can be set to `true` in the `host.json` file under `durableTask` as shown:</span><span class="sxs-lookup"><span data-stu-id="56e52-145">To enable emitting the verbose orchestration replay events, the `LogReplayEvents` can be set to `true` in the `host.json` file under `durableTask` as shown:</span></span>

```json
{
    "durableTask": {
        "logReplayEvents": true
    }
}
```

> [!NOTE]
> <span data-ttu-id="56e52-146">By default, Application Insights telemetry is sampled by the Azure Functions runtime to avoid emitting data too frequently.</span><span class="sxs-lookup"><span data-stu-id="56e52-146">By default, Application Insights telemetry is sampled by the Azure Functions runtime to avoid emitting data too frequently.</span></span> <span data-ttu-id="56e52-147">This can cause tracking information to be lost when many lifecycle events occur in a short period of time.</span><span class="sxs-lookup"><span data-stu-id="56e52-147">This can cause tracking information to be lost when many lifecycle events occur in a short period of time.</span></span> <span data-ttu-id="56e52-148">The [Azure Functions Monitoring article](functions-monitoring.md#configure-sampling) explains how to configure this behavior.</span><span class="sxs-lookup"><span data-stu-id="56e52-148">The [Azure Functions Monitoring article](functions-monitoring.md#configure-sampling) explains how to configure this behavior.</span></span>

### <a name="single-instance-query"></a><span data-ttu-id="56e52-149">Single instance query</span><span class="sxs-lookup"><span data-stu-id="56e52-149">Single instance query</span></span>

<span data-ttu-id="56e52-150">The following query shows historical tracking data for a single instance of the [Hello Sequence](durable-functions-sequence.md) function orchestration.</span><span class="sxs-lookup"><span data-stu-id="56e52-150">The following query shows historical tracking data for a single instance of the [Hello Sequence](durable-functions-sequence.md) function orchestration.</span></span> <span data-ttu-id="56e52-151">It's written using the [Application Insights Query Language (AIQL)](https://docs.loganalytics.io/docs/Language-Reference).</span><span class="sxs-lookup"><span data-stu-id="56e52-151">It's written using the [Application Insights Query Language (AIQL)](https://docs.loganalytics.io/docs/Language-Reference).</span></span> <span data-ttu-id="56e52-152">It filters out replay execution so that only the *logical* execution path is shown.</span><span class="sxs-lookup"><span data-stu-id="56e52-152">It filters out replay execution so that only the *logical* execution path is shown.</span></span> <span data-ttu-id="56e52-153">Events can be ordered by sorting by `timestamp` and `sequenceNumber` as shown in the query below:</span><span class="sxs-lookup"><span data-stu-id="56e52-153">Events can be ordered by sorting by `timestamp` and `sequenceNumber` as shown in the query below:</span></span> 

```AIQL
let targetInstanceId = "ddd1aaa685034059b545eb004b15d4eb";
let start = datetime(2018-03-25T09:20:00);
traces
| where timestamp > start and timestamp < start + 30m
| where customDimensions.Category == "Host.Triggers.DurableTask"
| extend functionName = customDimensions["prop__functionName"]
| extend instanceId = customDimensions["prop__instanceId"]
| extend state = customDimensions["prop__state"]
| extend isReplay = tobool(tolower(customDimensions["prop__isReplay"]))
| extend sequenceNumber = tolong(customDimensions["prop__sequenceNumber"]) 
| where isReplay != true
| where instanceId == targetInstanceId
| sort by timestamp asc, sequenceNumber asc
| project timestamp, functionName, state, instanceId, sequenceNumber, appName = cloud_RoleName
```

<span data-ttu-id="56e52-154">The result is a list of tracking events that shows the execution path of the orchestration, including any activity functions ordered by the execution time in ascending order.</span><span class="sxs-lookup"><span data-stu-id="56e52-154">The result is a list of tracking events that shows the execution path of the orchestration, including any activity functions ordered by the execution time in ascending order.</span></span>

![Application Insights query](media/durable-functions-diagnostics/app-insights-single-instance-ordered-query.png)


### <a name="instance-summary-query"></a><span data-ttu-id="56e52-156">Instance summary query</span><span class="sxs-lookup"><span data-stu-id="56e52-156">Instance summary query</span></span>

<span data-ttu-id="56e52-157">The following query displays the status of all orchestration instances that were run in a specified time range.</span><span class="sxs-lookup"><span data-stu-id="56e52-157">The following query displays the status of all orchestration instances that were run in a specified time range.</span></span>

```AIQL
let start = datetime(2017-09-30T04:30:00);
traces
| where timestamp > start and timestamp < start + 1h
| where customDimensions.Category == "Host.Triggers.DurableTask"
| extend functionName = tostring(customDimensions["prop__functionName"])
| extend instanceId = tostring(customDimensions["prop__instanceId"])
| extend state = tostring(customDimensions["prop__state"])
| extend isReplay = tobool(tolower(customDimensions["prop__isReplay"]))
| extend output = tostring(customDimensions["prop__output"])
| where isReplay != true
| summarize arg_max(timestamp, *) by instanceId
| project timestamp, instanceId, functionName, state, output, appName = cloud_RoleName
| order by timestamp asc
```
<span data-ttu-id="56e52-158">The result is a list of instance IDs and their current runtime status.</span><span class="sxs-lookup"><span data-stu-id="56e52-158">The result is a list of instance IDs and their current runtime status.</span></span>

![Application Insights query](media/durable-functions-diagnostics/app-insights-single-summary-query.png)

## <a name="logging"></a><span data-ttu-id="56e52-160">Logging</span><span class="sxs-lookup"><span data-stu-id="56e52-160">Logging</span></span>

<span data-ttu-id="56e52-161">It's important to keep the orchestrator replay behavior in mind when writing logs directly from an orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="56e52-161">It's important to keep the orchestrator replay behavior in mind when writing logs directly from an orchestrator function.</span></span> <span data-ttu-id="56e52-162">For example, consider the following orchestrator function:</span><span class="sxs-lookup"><span data-stu-id="56e52-162">For example, consider the following orchestrator function:</span></span>

#### <a name="c"></a><span data-ttu-id="56e52-163">C#</span><span class="sxs-lookup"><span data-stu-id="56e52-163">C#</span></span>

```cs
public static async Task Run(
    DurableOrchestrationContext ctx,
    TraceWriter log)
{
    log.Info("Calling F1.");
    await ctx.CallActivityAsync("F1");
    log.Info("Calling F2.");
    await ctx.CallActivityAsync("F2");
    log.Info("Calling F3");
    await ctx.CallActivityAsync("F3");
    log.Info("Done!");
}
```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="56e52-164">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="56e52-164">JavaScript (Functions v2 only)</span></span>

```javascript
const df = require("durable-functions");

module.exports = df(function*(context){
    context.log("Calling F1.");
    yield context.df.callActivityAsync("F1");
    context.log("Calling F2.");
    yield context.df.callActivityAsync("F2");
    context.log("Calling F3.");
    yield context.df.callActivityAsync("F3");
    context.log("Done!");
});
```

<span data-ttu-id="56e52-165">The resulting log data is going to look something like the following:</span><span class="sxs-lookup"><span data-stu-id="56e52-165">The resulting log data is going to look something like the following:</span></span>

```txt
Calling F1.
Calling F1.
Calling F2.
Calling F1.
Calling F2.
Calling F3.
Calling F1.
Calling F2.
Calling F3.
Done!
```

> [!NOTE]
> <span data-ttu-id="56e52-166">Remember that while the logs claim to be calling F1, F2, and F3, those functions are only *actually* called the first time they are encountered.</span><span class="sxs-lookup"><span data-stu-id="56e52-166">Remember that while the logs claim to be calling F1, F2, and F3, those functions are only *actually* called the first time they are encountered.</span></span> <span data-ttu-id="56e52-167">Subsequent calls that happen during replay are skipped and the outputs are replayed to the orchestrator logic.</span><span class="sxs-lookup"><span data-stu-id="56e52-167">Subsequent calls that happen during replay are skipped and the outputs are replayed to the orchestrator logic.</span></span>

<span data-ttu-id="56e52-168">If you want to only log on non-replay execution, you can write a conditional expression to log only if `IsReplaying` is `false`.</span><span class="sxs-lookup"><span data-stu-id="56e52-168">If you want to only log on non-replay execution, you can write a conditional expression to log only if `IsReplaying` is `false`.</span></span> <span data-ttu-id="56e52-169">Consider the example above, but this time with replay checks.</span><span class="sxs-lookup"><span data-stu-id="56e52-169">Consider the example above, but this time with replay checks.</span></span>

```cs
public static async Task Run(
    DurableOrchestrationContext ctx,
    TraceWriter log)
{
    if (!ctx.IsReplaying) log.Info("Calling F1.");
    await ctx.CallActivityAsync("F1");
    if (!ctx.IsReplaying) log.Info("Calling F2.");
    await ctx.CallActivityAsync("F2");
    if (!ctx.IsReplaying) log.Info("Calling F3");
    await ctx.CallActivityAsync("F3");
    log.Info("Done!");
}
```
<span data-ttu-id="56e52-170">With this change, the log output is as follows:</span><span class="sxs-lookup"><span data-stu-id="56e52-170">With this change, the log output is as follows:</span></span>

```txt
Calling F1.
Calling F2.
Calling F3.
Done!
```

> [!NOTE]
> <span data-ttu-id="56e52-171">The `IsReplaying` property is not yet available in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="56e52-171">The `IsReplaying` property is not yet available in JavaScript.</span></span>

## <a name="custom-status"></a><span data-ttu-id="56e52-172">Custom Status</span><span class="sxs-lookup"><span data-stu-id="56e52-172">Custom Status</span></span>

<span data-ttu-id="56e52-173">Custom orchestration status lets you set a custom status value for your orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="56e52-173">Custom orchestration status lets you set a custom status value for your orchestrator function.</span></span> <span data-ttu-id="56e52-174">This status is provided via the HTTP status query API or the `DurableOrchestrationClient.GetStatusAsync` API.</span><span class="sxs-lookup"><span data-stu-id="56e52-174">This status is provided via the HTTP status query API or the `DurableOrchestrationClient.GetStatusAsync` API.</span></span> <span data-ttu-id="56e52-175">The custom orchestration status enables richer monitoring for orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="56e52-175">The custom orchestration status enables richer monitoring for orchestrator functions.</span></span> <span data-ttu-id="56e52-176">For example, the orchestrator function code can include `DurableOrchestrationContext.SetCustomStatus` calls to update the progress for a long-running operation.</span><span class="sxs-lookup"><span data-stu-id="56e52-176">For example, the orchestrator function code can include `DurableOrchestrationContext.SetCustomStatus` calls to update the progress for a long-running operation.</span></span> <span data-ttu-id="56e52-177">A client, such as a web page or other external system, could then periodically query the HTTP status query APIs for richer progress information.</span><span class="sxs-lookup"><span data-stu-id="56e52-177">A client, such as a web page or other external system, could then periodically query the HTTP status query APIs for richer progress information.</span></span> <span data-ttu-id="56e52-178">A sample using `DurableOrchestrationContext.SetCustomStatus` is provided below:</span><span class="sxs-lookup"><span data-stu-id="56e52-178">A sample using `DurableOrchestrationContext.SetCustomStatus` is provided below:</span></span>

```csharp
public static async Task SetStatusTest([OrchestrationTrigger] DurableOrchestrationContext ctx)
{
    // ...do work...

    // update the status of the orchestration with some arbitrary data
    var customStatus = new { completionPercentage = 90.0, status = "Updating database records" };
    ctx.SetCustomStatus(customStatus);

    // ...do more work...
}
```

<span data-ttu-id="56e52-179">While the orchestration is running, external clients can fetch this custom status:</span><span class="sxs-lookup"><span data-stu-id="56e52-179">While the orchestration is running, external clients can fetch this custom status:</span></span>

```http
GET /admin/extensions/DurableTaskExtension/instances/instance123

```

<span data-ttu-id="56e52-180">Clients will get the following response:</span><span class="sxs-lookup"><span data-stu-id="56e52-180">Clients will get the following response:</span></span> 

```http
{
  "runtimeStatus": "Running",
  "input": null,
  "customStatus": { "completionPercentage": 90.0, "status": "Updating database records" },
  "output": null,
  "createdTime": "2017-10-06T18:30:24Z",
  "lastUpdatedTime": "2017-10-06T19:40:30Z"
}
```

> [!WARNING]
>  <span data-ttu-id="56e52-181">The custom status payload is limited to 16 KB of UTF-16 JSON text because it needs to be able to fit in an Azure Table Storage column.</span><span class="sxs-lookup"><span data-stu-id="56e52-181">The custom status payload is limited to 16 KB of UTF-16 JSON text because it needs to be able to fit in an Azure Table Storage column.</span></span> <span data-ttu-id="56e52-182">You can use external storage if you need larger payload.</span><span class="sxs-lookup"><span data-stu-id="56e52-182">You can use external storage if you need larger payload.</span></span>

## <a name="debugging"></a><span data-ttu-id="56e52-183">Debugging</span><span class="sxs-lookup"><span data-stu-id="56e52-183">Debugging</span></span>

<span data-ttu-id="56e52-184">Azure Functions supports debugging function code directly, and that same support carries forward to Durable Functions, whether running in Azure or locally.</span><span class="sxs-lookup"><span data-stu-id="56e52-184">Azure Functions supports debugging function code directly, and that same support carries forward to Durable Functions, whether running in Azure or locally.</span></span> <span data-ttu-id="56e52-185">However, there are a few behaviors to be aware of when debugging:</span><span class="sxs-lookup"><span data-stu-id="56e52-185">However, there are a few behaviors to be aware of when debugging:</span></span>

* <span data-ttu-id="56e52-186">**Replay**: Orchestrator functions regularly replay when new inputs are received.</span><span class="sxs-lookup"><span data-stu-id="56e52-186">**Replay**: Orchestrator functions regularly replay when new inputs are received.</span></span> <span data-ttu-id="56e52-187">This means a single *logical* execution of an orchestrator function can result in hitting the same breakpoint multiple times, especially if it is set early in the function code.</span><span class="sxs-lookup"><span data-stu-id="56e52-187">This means a single *logical* execution of an orchestrator function can result in hitting the same breakpoint multiple times, especially if it is set early in the function code.</span></span>
* <span data-ttu-id="56e52-188">**Await**: Whenever an `await` is encountered, it yields control back to the Durable Task Framework dispatcher.</span><span class="sxs-lookup"><span data-stu-id="56e52-188">**Await**: Whenever an `await` is encountered, it yields control back to the Durable Task Framework dispatcher.</span></span> <span data-ttu-id="56e52-189">If this is the first time a particular `await` has been encountered, the associated task is *never* resumed.</span><span class="sxs-lookup"><span data-stu-id="56e52-189">If this is the first time a particular `await` has been encountered, the associated task is *never* resumed.</span></span> <span data-ttu-id="56e52-190">Because the task never resumes, stepping *over* the await (F10 in Visual Studio) is not actually possible.</span><span class="sxs-lookup"><span data-stu-id="56e52-190">Because the task never resumes, stepping *over* the await (F10 in Visual Studio) is not actually possible.</span></span> <span data-ttu-id="56e52-191">Stepping over only works when a task is being replayed.</span><span class="sxs-lookup"><span data-stu-id="56e52-191">Stepping over only works when a task is being replayed.</span></span>
* <span data-ttu-id="56e52-192">**Messaging timeouts**: Durable Functions internally uses queue messages to drive execution of both orchestrator functions and activity functions.</span><span class="sxs-lookup"><span data-stu-id="56e52-192">**Messaging timeouts**: Durable Functions internally uses queue messages to drive execution of both orchestrator functions and activity functions.</span></span> <span data-ttu-id="56e52-193">In a multi-VM environment, breaking into the debugging for extended periods of time could cause another VM to pick up the message, resulting in duplicate execution.</span><span class="sxs-lookup"><span data-stu-id="56e52-193">In a multi-VM environment, breaking into the debugging for extended periods of time could cause another VM to pick up the message, resulting in duplicate execution.</span></span> <span data-ttu-id="56e52-194">This behavior exists for regular queue-trigger functions as well, but is important to point out in this context since the queues are an implementation detail.</span><span class="sxs-lookup"><span data-stu-id="56e52-194">This behavior exists for regular queue-trigger functions as well, but is important to point out in this context since the queues are an implementation detail.</span></span>

> [!TIP]
> <span data-ttu-id="56e52-195">When setting breakpoints, if you want to only break on non-replay execution, you can set a conditional breakpoint that breaks only if `IsReplaying` is `false`.</span><span class="sxs-lookup"><span data-stu-id="56e52-195">When setting breakpoints, if you want to only break on non-replay execution, you can set a conditional breakpoint that breaks only if `IsReplaying` is `false`.</span></span>

## <a name="storage"></a><span data-ttu-id="56e52-196">Storage</span><span class="sxs-lookup"><span data-stu-id="56e52-196">Storage</span></span>

<span data-ttu-id="56e52-197">By default, Durable Functions stores state in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="56e52-197">By default, Durable Functions stores state in Azure Storage.</span></span> <span data-ttu-id="56e52-198">This means you can inspect the state of your orchestrations using tools such as [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span><span class="sxs-lookup"><span data-stu-id="56e52-198">This means you can inspect the state of your orchestrations using tools such as [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span></span>

![Azure Storage Explorer screen shot](media/durable-functions-diagnostics/storage-explorer.png)

<span data-ttu-id="56e52-200">This is useful for debugging because you see exactly what state an orchestration may be in.</span><span class="sxs-lookup"><span data-stu-id="56e52-200">This is useful for debugging because you see exactly what state an orchestration may be in.</span></span> <span data-ttu-id="56e52-201">Messages in the queues can also be examined to learn what work is pending (or stuck in some cases).</span><span class="sxs-lookup"><span data-stu-id="56e52-201">Messages in the queues can also be examined to learn what work is pending (or stuck in some cases).</span></span>

> [!WARNING]
> <span data-ttu-id="56e52-202">While it's convenient to see execution history in table storage, avoid taking any dependency on this table.</span><span class="sxs-lookup"><span data-stu-id="56e52-202">While it's convenient to see execution history in table storage, avoid taking any dependency on this table.</span></span> <span data-ttu-id="56e52-203">It may change as the Durable Functions extension evolves.</span><span class="sxs-lookup"><span data-stu-id="56e52-203">It may change as the Durable Functions extension evolves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56e52-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="56e52-204">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56e52-205">Learn how to use durable timers</span><span class="sxs-lookup"><span data-stu-id="56e52-205">Learn how to use durable timers</span></span>](durable-functions-timers.md)
