---
title: host.json reference for Azure Functions
description: Reference documentation for the Azure Functions host.json file.
services: functions
author: ggailey777
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 02/12/2018
ms.author: glenga
ms.openlocfilehash: 11bf136897b5d5b8140fc7ff1bb259c657a71921
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856527"
---
# <a name="hostjson-reference-for-azure-functions"></a><span data-ttu-id="4ac2a-103">host.json reference for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4ac2a-103">host.json reference for Azure Functions</span></span>

<span data-ttu-id="4ac2a-104">The *host.json* metadata file contains global configuration options that affect all functions for a function app.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-104">The *host.json* metadata file contains global configuration options that affect all functions for a function app.</span></span> <span data-ttu-id="4ac2a-105">This article lists the settings that are available.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-105">This article lists the settings that are available.</span></span> <span data-ttu-id="4ac2a-106">The JSON schema is at http://json.schemastore.org/host.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-106">The JSON schema is at http://json.schemastore.org/host.</span></span>

<span data-ttu-id="4ac2a-107">There are other global configuration options in [app settings](functions-app-settings.md) and in the [local.settings.json](functions-run-local.md#local-settings-file) file.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-107">There are other global configuration options in [app settings](functions-app-settings.md) and in the [local.settings.json](functions-run-local.md#local-settings-file) file.</span></span>

## <a name="sample-hostjson-file"></a><span data-ttu-id="4ac2a-108">Sample host.json file</span><span class="sxs-lookup"><span data-stu-id="4ac2a-108">Sample host.json file</span></span>

<span data-ttu-id="4ac2a-109">The following sample *host.json* file has all possible options specified.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-109">The following sample *host.json* file has all possible options specified.</span></span>

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    },
    "applicationInsights": {
        "sampling": {
          "isEnabled": true,
          "maxTelemetryItemsPerSecond" : 5
        }
    },
    "eventHub": {
      "maxBatchSize": 64,
      "prefetchCount": 256,
      "batchCheckpointFrequency": 1
    },
    "functions": [ "QueueProcessor", "GitHubWebHook" ],
    "functionTimeout": "00:05:00",
    "healthMonitor": {
        "enabled": true,
        "healthCheckInterval": "00:00:10",
        "healthCheckWindow": "00:02:00",
        "healthCheckThreshold": 6,
        "counterThreshold": 0.80
    },
    "http": {
        "routePrefix": "api",
        "maxOutstandingRequests": 20,
        "maxConcurrentRequests": 10,
        "dynamicThrottlesEnabled": false
    },
    "id": "9f4ea53c5136457d883d685e57164f08",
    "logger": {
        "categoryFilter": {
            "defaultLevel": "Information",
            "categoryLevels": {
                "Host": "Error",
                "Function": "Error",
                "Host.Aggregator": "Information"
            }
        }
    },
    "queues": {
      "maxPollingInterval": 2000,
      "visibilityTimeout" : "00:00:30",
      "batchSize": 16,
      "maxDequeueCount": 5,
      "newBatchThreshold": 8
    },
    "serviceBus": {
      "maxConcurrentCalls": 16,
      "prefetchCount": 100,
      "autoRenewTimeout": "00:05:00"
    },
    "singleton": {
      "lockPeriod": "00:00:15",
      "listenerLockPeriod": "00:01:00",
      "listenerLockRecoveryPollingInterval": "00:01:00",
      "lockAcquisitionTimeout": "00:01:00",
      "lockAcquisitionPollingInterval": "00:00:03"
    },
    "tracing": {
      "consoleLevel": "verbose",
      "fileLoggingMode": "debugOnly"
    },
    "watchDirectories": [ "Shared" ],
}
```

<span data-ttu-id="4ac2a-110">The following sections of this article explain each top-level property.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-110">The following sections of this article explain each top-level property.</span></span> <span data-ttu-id="4ac2a-111">All are optional unless otherwise indicated.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-111">All are optional unless otherwise indicated.</span></span>

## <a name="aggregator"></a><span data-ttu-id="4ac2a-112">aggregator</span><span class="sxs-lookup"><span data-stu-id="4ac2a-112">aggregator</span></span>

<span data-ttu-id="4ac2a-113">Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](functions-monitoring.md#configure-the-aggregator).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-113">Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](functions-monitoring.md#configure-the-aggregator).</span></span> 

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    }
}
```

|<span data-ttu-id="4ac2a-114">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-114">Property</span></span> |<span data-ttu-id="4ac2a-115">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-115">Default</span></span>  | <span data-ttu-id="4ac2a-116">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-116">Description</span></span> |
|---------|---------|---------| 
|<span data-ttu-id="4ac2a-117">batchSize</span><span class="sxs-lookup"><span data-stu-id="4ac2a-117">batchSize</span></span>|<span data-ttu-id="4ac2a-118">1000</span><span class="sxs-lookup"><span data-stu-id="4ac2a-118">1000</span></span>|<span data-ttu-id="4ac2a-119">Maximum number of requests to aggregate.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-119">Maximum number of requests to aggregate.</span></span>| 
|<span data-ttu-id="4ac2a-120">flushTimeout</span><span class="sxs-lookup"><span data-stu-id="4ac2a-120">flushTimeout</span></span>|<span data-ttu-id="4ac2a-121">00:00:30</span><span class="sxs-lookup"><span data-stu-id="4ac2a-121">00:00:30</span></span>|<span data-ttu-id="4ac2a-122">Maximum time period to aggregate.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-122">Maximum time period to aggregate.</span></span>| 

<span data-ttu-id="4ac2a-123">Function invocations are aggregated when the first of the two limits are reached.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-123">Function invocations are aggregated when the first of the two limits are reached.</span></span>

## <a name="applicationinsights"></a><span data-ttu-id="4ac2a-124">applicationInsights</span><span class="sxs-lookup"><span data-stu-id="4ac2a-124">applicationInsights</span></span>

<span data-ttu-id="4ac2a-125">Controls the [sampling feature in Application Insights](functions-monitoring.md#configure-sampling).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-125">Controls the [sampling feature in Application Insights](functions-monitoring.md#configure-sampling).</span></span>

```json
{
    "applicationInsights": {
        "sampling": {
          "isEnabled": true,
          "maxTelemetryItemsPerSecond" : 5
        }
    }
}
```

|<span data-ttu-id="4ac2a-126">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-126">Property</span></span>  |<span data-ttu-id="4ac2a-127">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-127">Default</span></span> | <span data-ttu-id="4ac2a-128">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-128">Description</span></span> |
|---------|---------|---------| 
|<span data-ttu-id="4ac2a-129">isEnabled</span><span class="sxs-lookup"><span data-stu-id="4ac2a-129">isEnabled</span></span>|<span data-ttu-id="4ac2a-130">true</span><span class="sxs-lookup"><span data-stu-id="4ac2a-130">true</span></span>|<span data-ttu-id="4ac2a-131">Enables or disables sampling.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-131">Enables or disables sampling.</span></span>| 
|<span data-ttu-id="4ac2a-132">maxTelemetryItemsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4ac2a-132">maxTelemetryItemsPerSecond</span></span>|<span data-ttu-id="4ac2a-133">5</span><span class="sxs-lookup"><span data-stu-id="4ac2a-133">5</span></span>|<span data-ttu-id="4ac2a-134">The threshold at which sampling begins.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-134">The threshold at which sampling begins.</span></span>| 

## <a name="durabletask"></a><span data-ttu-id="4ac2a-135">durableTask</span><span class="sxs-lookup"><span data-stu-id="4ac2a-135">durableTask</span></span>

<span data-ttu-id="4ac2a-136">Configuration settings for [Durable Functions](durable-functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-136">Configuration settings for [Durable Functions](durable-functions-overview.md).</span></span>

```json
{
  "durableTask": {
    "HubName": "MyTaskHub",
    "ControlQueueBatchSize": 32,
    "PartitionCount": 4,
    "ControlQueueVisibilityTimeout": "00:05:00",
    "WorkItemQueueVisibilityTimeout": "00:05:00",
    "MaxConcurrentActivityFunctions": 10,
    "MaxConcurrentOrchestratorFunctions": 10,
    "AzureStorageConnectionStringName": "AzureWebJobsStorage",
    "TraceInputsAndOutputs": false,
    "LogReplayEvents": false,
    "EventGridTopicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
    "EventGridKeySettingName":  "EventGridKey",
    "EventGridPublishRetryCount": 3,
    "EventGridPublishRetryInterval": "00:00:30"
  }
}
```

<span data-ttu-id="4ac2a-137">Task hub names must start with a letter and consist of only letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-137">Task hub names must start with a letter and consist of only letters and numbers.</span></span> <span data-ttu-id="4ac2a-138">If not specified, the default task hub name for a function app is **DurableFunctionsHub**.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-138">If not specified, the default task hub name for a function app is **DurableFunctionsHub**.</span></span> <span data-ttu-id="4ac2a-139">For  more information, see [Task hubs](durable-functions-task-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-139">For  more information, see [Task hubs](durable-functions-task-hubs.md).</span></span>

|<span data-ttu-id="4ac2a-140">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-140">Property</span></span>  |<span data-ttu-id="4ac2a-141">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-141">Default</span></span> | <span data-ttu-id="4ac2a-142">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-142">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="4ac2a-143">HubName</span><span class="sxs-lookup"><span data-stu-id="4ac2a-143">HubName</span></span>|<span data-ttu-id="4ac2a-144">DurableFunctionsHub</span><span class="sxs-lookup"><span data-stu-id="4ac2a-144">DurableFunctionsHub</span></span>|<span data-ttu-id="4ac2a-145">Alternate [task hub](durable-functions-task-hubs.md) names can be used to isolate multiple Durable Functions applications from each other, even if they are using the same storage backend.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-145">Alternate [task hub](durable-functions-task-hubs.md) names can be used to isolate multiple Durable Functions applications from each other, even if they are using the same storage backend.</span></span>|
|<span data-ttu-id="4ac2a-146">ControlQueueBatchSize</span><span class="sxs-lookup"><span data-stu-id="4ac2a-146">ControlQueueBatchSize</span></span>|<span data-ttu-id="4ac2a-147">32</span><span class="sxs-lookup"><span data-stu-id="4ac2a-147">32</span></span>|<span data-ttu-id="4ac2a-148">The number of messages to pull from the control queue at a time.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-148">The number of messages to pull from the control queue at a time.</span></span>|
|<span data-ttu-id="4ac2a-149">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="4ac2a-149">PartitionCount</span></span> |<span data-ttu-id="4ac2a-150">4</span><span class="sxs-lookup"><span data-stu-id="4ac2a-150">4</span></span>|<span data-ttu-id="4ac2a-151">The partition count for the control queue.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-151">The partition count for the control queue.</span></span> <span data-ttu-id="4ac2a-152">May be a positive integer between 1 and 16.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-152">May be a positive integer between 1 and 16.</span></span>|
|<span data-ttu-id="4ac2a-153">ControlQueueVisibilityTimeout</span><span class="sxs-lookup"><span data-stu-id="4ac2a-153">ControlQueueVisibilityTimeout</span></span> |<span data-ttu-id="4ac2a-154">5 minutes</span><span class="sxs-lookup"><span data-stu-id="4ac2a-154">5 minutes</span></span>|<span data-ttu-id="4ac2a-155">The visibility timeout of dequeued control queue messages.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-155">The visibility timeout of dequeued control queue messages.</span></span>|
|<span data-ttu-id="4ac2a-156">WorkItemQueueVisibilityTimeout</span><span class="sxs-lookup"><span data-stu-id="4ac2a-156">WorkItemQueueVisibilityTimeout</span></span> |<span data-ttu-id="4ac2a-157">5 minutes</span><span class="sxs-lookup"><span data-stu-id="4ac2a-157">5 minutes</span></span>|<span data-ttu-id="4ac2a-158">The visibility timeout of dequeued work item  queue messages.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-158">The visibility timeout of dequeued work item  queue messages.</span></span>|
|<span data-ttu-id="4ac2a-159">MaxConcurrentActivityFunctions</span><span class="sxs-lookup"><span data-stu-id="4ac2a-159">MaxConcurrentActivityFunctions</span></span> |<span data-ttu-id="4ac2a-160">10X the number of processors on the current machine</span><span class="sxs-lookup"><span data-stu-id="4ac2a-160">10X the number of processors on the current machine</span></span>|<span data-ttu-id="4ac2a-161">The maximum number of activity functions that can be processed concurrently on a single host instance.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-161">The maximum number of activity functions that can be processed concurrently on a single host instance.</span></span>|
|<span data-ttu-id="4ac2a-162">MaxConcurrentOrchestratorFunctions</span><span class="sxs-lookup"><span data-stu-id="4ac2a-162">MaxConcurrentOrchestratorFunctions</span></span> |<span data-ttu-id="4ac2a-163">10X the number of processors on the current machine</span><span class="sxs-lookup"><span data-stu-id="4ac2a-163">10X the number of processors on the current machine</span></span>|<span data-ttu-id="4ac2a-164">The maximum number of activity functions that can be processed concurrently on a single host instance.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-164">The maximum number of activity functions that can be processed concurrently on a single host instance.</span></span>|
|<span data-ttu-id="4ac2a-165">AzureStorageConnectionStringName</span><span class="sxs-lookup"><span data-stu-id="4ac2a-165">AzureStorageConnectionStringName</span></span> |<span data-ttu-id="4ac2a-166">AzureWebJobsStorage</span><span class="sxs-lookup"><span data-stu-id="4ac2a-166">AzureWebJobsStorage</span></span>|<span data-ttu-id="4ac2a-167">The name of the app setting that has the Azure Storage connection string used to manage the underlying Azure Storage resources.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-167">The name of the app setting that has the Azure Storage connection string used to manage the underlying Azure Storage resources.</span></span>|
|<span data-ttu-id="4ac2a-168">TraceInputsAndOutputs</span><span class="sxs-lookup"><span data-stu-id="4ac2a-168">TraceInputsAndOutputs</span></span> |<span data-ttu-id="4ac2a-169">false</span><span class="sxs-lookup"><span data-stu-id="4ac2a-169">false</span></span>|<span data-ttu-id="4ac2a-170">A value indicating whether to trace the inputs and outputs of function calls.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-170">A value indicating whether to trace the inputs and outputs of function calls.</span></span> <span data-ttu-id="4ac2a-171">The default behavior when tracing function execution events is to include the number of bytes in the serialized inputs and outputs for function calls.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-171">The default behavior when tracing function execution events is to include the number of bytes in the serialized inputs and outputs for function calls.</span></span> <span data-ttu-id="4ac2a-172">This provides minimal information about what the inputs and outputs look like without bloating the logs or inadvertently exposing sensitive information to the logs.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-172">This provides minimal information about what the inputs and outputs look like without bloating the logs or inadvertently exposing sensitive information to the logs.</span></span> <span data-ttu-id="4ac2a-173">Setting this property to true causes the default function logging to log the entire contents of function inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-173">Setting this property to true causes the default function logging to log the entire contents of function inputs and outputs.</span></span>|
|<span data-ttu-id="4ac2a-174">LogReplayEvents</span><span class="sxs-lookup"><span data-stu-id="4ac2a-174">LogReplayEvents</span></span>|<span data-ttu-id="4ac2a-175">false</span><span class="sxs-lookup"><span data-stu-id="4ac2a-175">false</span></span>|<span data-ttu-id="4ac2a-176">A value indicating whether to write orchestration replay events to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-176">A value indicating whether to write orchestration replay events to Application Insights.</span></span>|
|<span data-ttu-id="4ac2a-177">EventGridTopicEndpoint</span><span class="sxs-lookup"><span data-stu-id="4ac2a-177">EventGridTopicEndpoint</span></span> ||<span data-ttu-id="4ac2a-178">The URL of an Azure Event Grid custom topic endpoint.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-178">The URL of an Azure Event Grid custom topic endpoint.</span></span> <span data-ttu-id="4ac2a-179">When this property is set, orchestration life cycle notification events are published to this endpoint.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-179">When this property is set, orchestration life cycle notification events are published to this endpoint.</span></span> <span data-ttu-id="4ac2a-180">This property supports App Settings resolution.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-180">This property supports App Settings resolution.</span></span>|
|<span data-ttu-id="4ac2a-181">EventGridKeySettingName</span><span class="sxs-lookup"><span data-stu-id="4ac2a-181">EventGridKeySettingName</span></span> ||<span data-ttu-id="4ac2a-182">The name of the app setting containing the key used for authenticating with the Azure Event Grid custom topic at `EventGridTopicEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-182">The name of the app setting containing the key used for authenticating with the Azure Event Grid custom topic at `EventGridTopicEndpoint`.</span></span>|
|<span data-ttu-id="4ac2a-183">EventGridPublishRetryCount</span><span class="sxs-lookup"><span data-stu-id="4ac2a-183">EventGridPublishRetryCount</span></span>|<span data-ttu-id="4ac2a-184">0</span><span class="sxs-lookup"><span data-stu-id="4ac2a-184">0</span></span>|<span data-ttu-id="4ac2a-185">The number of times to retry if publishing to the Event Grid Topic fails.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-185">The number of times to retry if publishing to the Event Grid Topic fails.</span></span>|
|<span data-ttu-id="4ac2a-186">EventGridPublishRetryInterval</span><span class="sxs-lookup"><span data-stu-id="4ac2a-186">EventGridPublishRetryInterval</span></span>|<span data-ttu-id="4ac2a-187">5 minutes</span><span class="sxs-lookup"><span data-stu-id="4ac2a-187">5 minutes</span></span>|<span data-ttu-id="4ac2a-188">The Event Grid publish retry interval in the *hh:mm:ss* format.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-188">The Event Grid publish retry interval in the *hh:mm:ss* format.</span></span>|

<span data-ttu-id="4ac2a-189">Many of these are for optimizing performance.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-189">Many of these are for optimizing performance.</span></span> <span data-ttu-id="4ac2a-190">For more information, see [Performance and scale](durable-functions-perf-and-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-190">For more information, see [Performance and scale](durable-functions-perf-and-scale.md).</span></span>

## <a name="eventhub"></a><span data-ttu-id="4ac2a-191">eventHub</span><span class="sxs-lookup"><span data-stu-id="4ac2a-191">eventHub</span></span>

<span data-ttu-id="4ac2a-192">Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-192">Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs.md).</span></span>

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-event-hubs.md)]

## <a name="functions"></a><span data-ttu-id="4ac2a-193">functions</span><span class="sxs-lookup"><span data-stu-id="4ac2a-193">functions</span></span>

<span data-ttu-id="4ac2a-194">A list of functions that the job host will run.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-194">A list of functions that the job host will run.</span></span> <span data-ttu-id="4ac2a-195">An empty array means run all functions.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-195">An empty array means run all functions.</span></span> <span data-ttu-id="4ac2a-196">Intended for use only when [running locally](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-196">Intended for use only when [running locally](functions-run-local.md).</span></span> <span data-ttu-id="4ac2a-197">In function apps, use the *function.json* `disabled` property rather than this property in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-197">In function apps, use the *function.json* `disabled` property rather than this property in *host.json*.</span></span>

```json
{
    "functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```

## <a name="functiontimeout"></a><span data-ttu-id="4ac2a-198">functionTimeout</span><span class="sxs-lookup"><span data-stu-id="4ac2a-198">functionTimeout</span></span>

<span data-ttu-id="4ac2a-199">Indicates the timeout duration for all functions.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-199">Indicates the timeout duration for all functions.</span></span> <span data-ttu-id="4ac2a-200">In Consumption plans, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-200">In Consumption plans, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes.</span></span> <span data-ttu-id="4ac2a-201">In App Service plans, there is no limit and the default value is null, which indicates no timeout.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-201">In App Service plans, there is no limit and the default value is null, which indicates no timeout.</span></span>

```json
{
    "functionTimeout": "00:05:00"
}
```

## <a name="healthmonitor"></a><span data-ttu-id="4ac2a-202">healthMonitor</span><span class="sxs-lookup"><span data-stu-id="4ac2a-202">healthMonitor</span></span>

<span data-ttu-id="4ac2a-203">Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-203">Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).</span></span>

```
{
    "healthMonitor": {
        "enabled": true,
        "healthCheckInterval": "00:00:10",
        "healthCheckWindow": "00:02:00",
        "healthCheckThreshold": 6,
        "counterThreshold": 0.80
    }
}
```

|<span data-ttu-id="4ac2a-204">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-204">Property</span></span>  |<span data-ttu-id="4ac2a-205">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-205">Default</span></span> | <span data-ttu-id="4ac2a-206">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-206">Description</span></span> |
|---------|---------|---------| 
|<span data-ttu-id="4ac2a-207">enabled</span><span class="sxs-lookup"><span data-stu-id="4ac2a-207">enabled</span></span>|<span data-ttu-id="4ac2a-208">true</span><span class="sxs-lookup"><span data-stu-id="4ac2a-208">true</span></span>|<span data-ttu-id="4ac2a-209">Whether the feature is enabled.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-209">Whether the feature is enabled.</span></span> | 
|<span data-ttu-id="4ac2a-210">healthCheckInterval</span><span class="sxs-lookup"><span data-stu-id="4ac2a-210">healthCheckInterval</span></span>|<span data-ttu-id="4ac2a-211">10 seconds</span><span class="sxs-lookup"><span data-stu-id="4ac2a-211">10 seconds</span></span>|<span data-ttu-id="4ac2a-212">The time interval between the periodic background health checks.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-212">The time interval between the periodic background health checks.</span></span> | 
|<span data-ttu-id="4ac2a-213">healthCheckWindow</span><span class="sxs-lookup"><span data-stu-id="4ac2a-213">healthCheckWindow</span></span>|<span data-ttu-id="4ac2a-214">2 minutes</span><span class="sxs-lookup"><span data-stu-id="4ac2a-214">2 minutes</span></span>|<span data-ttu-id="4ac2a-215">A sliding time window used in conjunction with the `healthCheckThreshold` setting.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-215">A sliding time window used in conjunction with the `healthCheckThreshold` setting.</span></span>| 
|<span data-ttu-id="4ac2a-216">healthCheckThreshold</span><span class="sxs-lookup"><span data-stu-id="4ac2a-216">healthCheckThreshold</span></span>|<span data-ttu-id="4ac2a-217">6</span><span class="sxs-lookup"><span data-stu-id="4ac2a-217">6</span></span>|<span data-ttu-id="4ac2a-218">Maximum number of times the health check can fail before a host recycle is initiated.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-218">Maximum number of times the health check can fail before a host recycle is initiated.</span></span>| 
|<span data-ttu-id="4ac2a-219">counterThreshold</span><span class="sxs-lookup"><span data-stu-id="4ac2a-219">counterThreshold</span></span>|<span data-ttu-id="4ac2a-220">0.80</span><span class="sxs-lookup"><span data-stu-id="4ac2a-220">0.80</span></span>|<span data-ttu-id="4ac2a-221">The threshold at which a performance counter will be considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-221">The threshold at which a performance counter will be considered unhealthy.</span></span>| 

## <a name="http"></a><span data-ttu-id="4ac2a-222">http</span><span class="sxs-lookup"><span data-stu-id="4ac2a-222">http</span></span>

<span data-ttu-id="4ac2a-223">Configuration settings for [http triggers and bindings](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-223">Configuration settings for [http triggers and bindings](functions-bindings-http-webhook.md).</span></span>

[!INCLUDE [functions-host-json-http](../../includes/functions-host-json-http.md)]

## <a name="id"></a><span data-ttu-id="4ac2a-224">id</span><span class="sxs-lookup"><span data-stu-id="4ac2a-224">id</span></span>

<span data-ttu-id="4ac2a-225">The unique ID for a job host.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-225">The unique ID for a job host.</span></span> <span data-ttu-id="4ac2a-226">Can be a lower case GUID with dashes removed.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-226">Can be a lower case GUID with dashes removed.</span></span> <span data-ttu-id="4ac2a-227">Required when running locally.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-227">Required when running locally.</span></span> <span data-ttu-id="4ac2a-228">When running in Azure Functions, an ID is generated automatically if `id` is omitted.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-228">When running in Azure Functions, an ID is generated automatically if `id` is omitted.</span></span>

<span data-ttu-id="4ac2a-229">If you share a Storage account across multiple function apps, make sure that each function app has a different `id`.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-229">If you share a Storage account across multiple function apps, make sure that each function app has a different `id`.</span></span> <span data-ttu-id="4ac2a-230">You can omit the `id` property or manually set each function app's `id` to a different value.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-230">You can omit the `id` property or manually set each function app's `id` to a different value.</span></span> <span data-ttu-id="4ac2a-231">The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-231">The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances.</span></span> <span data-ttu-id="4ac2a-232">If two function apps share the same `id` and each uses a timer trigger, only one timer will run.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-232">If two function apps share the same `id` and each uses a timer trigger, only one timer will run.</span></span>


```json
{
    "id": "9f4ea53c5136457d883d685e57164f08"
}
```

## <a name="logger"></a><span data-ttu-id="4ac2a-233">logger</span><span class="sxs-lookup"><span data-stu-id="4ac2a-233">logger</span></span>

<span data-ttu-id="4ac2a-234">Controls filtering for logs written by an [ILogger object](functions-monitoring.md#write-logs-in-c-functions) or by [context.log](functions-monitoring.md#write-logs-in-javascript-functions).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-234">Controls filtering for logs written by an [ILogger object](functions-monitoring.md#write-logs-in-c-functions) or by [context.log](functions-monitoring.md#write-logs-in-javascript-functions).</span></span>

```json
{
    "logger": {
        "categoryFilter": {
            "defaultLevel": "Information",
            "categoryLevels": {
                "Host": "Error",
                "Function": "Error",
                "Host.Aggregator": "Information"
            }
        }
    }
}
```

|<span data-ttu-id="4ac2a-235">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-235">Property</span></span>  |<span data-ttu-id="4ac2a-236">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-236">Default</span></span> | <span data-ttu-id="4ac2a-237">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-237">Description</span></span> |
|---------|---------|---------| 
|<span data-ttu-id="4ac2a-238">categoryFilter</span><span class="sxs-lookup"><span data-stu-id="4ac2a-238">categoryFilter</span></span>|<span data-ttu-id="4ac2a-239">n/a</span><span class="sxs-lookup"><span data-stu-id="4ac2a-239">n/a</span></span>|<span data-ttu-id="4ac2a-240">Specifies filtering by category</span><span class="sxs-lookup"><span data-stu-id="4ac2a-240">Specifies filtering by category</span></span>| 
|<span data-ttu-id="4ac2a-241">defaultLevel</span><span class="sxs-lookup"><span data-stu-id="4ac2a-241">defaultLevel</span></span>|<span data-ttu-id="4ac2a-242">Information</span><span class="sxs-lookup"><span data-stu-id="4ac2a-242">Information</span></span>|<span data-ttu-id="4ac2a-243">For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-243">For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights.</span></span>| 
|<span data-ttu-id="4ac2a-244">categoryLevels</span><span class="sxs-lookup"><span data-stu-id="4ac2a-244">categoryLevels</span></span>|<span data-ttu-id="4ac2a-245">n/a</span><span class="sxs-lookup"><span data-stu-id="4ac2a-245">n/a</span></span>|<span data-ttu-id="4ac2a-246">An array of categories that specifies the minimum log level to send to Application Insights for each category.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-246">An array of categories that specifies the minimum log level to send to Application Insights for each category.</span></span> <span data-ttu-id="4ac2a-247">The category specified here controls all categories that begin with the same value, and longer values take precedence.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-247">The category specified here controls all categories that begin with the same value, and longer values take precedence.</span></span> <span data-ttu-id="4ac2a-248">In the preceding sample *host.json* file, all categories that begin with "Host.Aggregator" log at `Information` level.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-248">In the preceding sample *host.json* file, all categories that begin with "Host.Aggregator" log at `Information` level.</span></span> <span data-ttu-id="4ac2a-249">All other categories that begin with "Host", such as "Host.Executor", log at `Error` level.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-249">All other categories that begin with "Host", such as "Host.Executor", log at `Error` level.</span></span>| 

## <a name="queues"></a><span data-ttu-id="4ac2a-250">queues</span><span class="sxs-lookup"><span data-stu-id="4ac2a-250">queues</span></span>

<span data-ttu-id="4ac2a-251">Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-251">Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue.md).</span></span>

[!INCLUDE [functions-host-json-queues](../../includes/functions-host-json-queues.md)]

## <a name="servicebus"></a><span data-ttu-id="4ac2a-252">serviceBus</span><span class="sxs-lookup"><span data-stu-id="4ac2a-252">serviceBus</span></span>

<span data-ttu-id="4ac2a-253">Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-253">Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus.md).</span></span>

[!INCLUDE [functions-host-json-service-bus](../../includes/functions-host-json-service-bus.md)]

## <a name="singleton"></a><span data-ttu-id="4ac2a-254">singleton</span><span class="sxs-lookup"><span data-stu-id="4ac2a-254">singleton</span></span>

<span data-ttu-id="4ac2a-255">Configuration settings for Singleton lock behavior.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-255">Configuration settings for Singleton lock behavior.</span></span> <span data-ttu-id="4ac2a-256">For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-256">For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).</span></span>

```json
{
    "singleton": {
      "lockPeriod": "00:00:15",
      "listenerLockPeriod": "00:01:00",
      "listenerLockRecoveryPollingInterval": "00:01:00",
      "lockAcquisitionTimeout": "00:01:00",
      "lockAcquisitionPollingInterval": "00:00:03"
    }
}
```

|<span data-ttu-id="4ac2a-257">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-257">Property</span></span>  |<span data-ttu-id="4ac2a-258">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-258">Default</span></span> | <span data-ttu-id="4ac2a-259">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-259">Description</span></span> |
|---------|---------|---------| 
|<span data-ttu-id="4ac2a-260">lockPeriod</span><span class="sxs-lookup"><span data-stu-id="4ac2a-260">lockPeriod</span></span>|<span data-ttu-id="4ac2a-261">00:00:15</span><span class="sxs-lookup"><span data-stu-id="4ac2a-261">00:00:15</span></span>|<span data-ttu-id="4ac2a-262">The period that function level locks are taken for.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-262">The period that function level locks are taken for.</span></span> <span data-ttu-id="4ac2a-263">The locks auto-renew.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-263">The locks auto-renew.</span></span>| 
|<span data-ttu-id="4ac2a-264">listenerLockPeriod</span><span class="sxs-lookup"><span data-stu-id="4ac2a-264">listenerLockPeriod</span></span>|<span data-ttu-id="4ac2a-265">00:01:00</span><span class="sxs-lookup"><span data-stu-id="4ac2a-265">00:01:00</span></span>|<span data-ttu-id="4ac2a-266">The period that listener locks are taken for.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-266">The period that listener locks are taken for.</span></span>| 
|<span data-ttu-id="4ac2a-267">listenerLockRecoveryPollingInterval</span><span class="sxs-lookup"><span data-stu-id="4ac2a-267">listenerLockRecoveryPollingInterval</span></span>|<span data-ttu-id="4ac2a-268">00:01:00</span><span class="sxs-lookup"><span data-stu-id="4ac2a-268">00:01:00</span></span>|<span data-ttu-id="4ac2a-269">The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-269">The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup.</span></span>| 
|<span data-ttu-id="4ac2a-270">lockAcquisitionTimeout</span><span class="sxs-lookup"><span data-stu-id="4ac2a-270">lockAcquisitionTimeout</span></span>|<span data-ttu-id="4ac2a-271">00:01:00</span><span class="sxs-lookup"><span data-stu-id="4ac2a-271">00:01:00</span></span>|<span data-ttu-id="4ac2a-272">The maximum amount of time the runtime will try to acquire a lock.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-272">The maximum amount of time the runtime will try to acquire a lock.</span></span>| 
|<span data-ttu-id="4ac2a-273">lockAcquisitionPollingInterval</span><span class="sxs-lookup"><span data-stu-id="4ac2a-273">lockAcquisitionPollingInterval</span></span>|<span data-ttu-id="4ac2a-274">n/a</span><span class="sxs-lookup"><span data-stu-id="4ac2a-274">n/a</span></span>|<span data-ttu-id="4ac2a-275">The interval between lock acquisition attempts.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-275">The interval between lock acquisition attempts.</span></span>| 

## <a name="tracing"></a><span data-ttu-id="4ac2a-276">tracing</span><span class="sxs-lookup"><span data-stu-id="4ac2a-276">tracing</span></span>

<span data-ttu-id="4ac2a-277">Configuration settings for logs that you create by using a `TraceWriter` object.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-277">Configuration settings for logs that you create by using a `TraceWriter` object.</span></span> <span data-ttu-id="4ac2a-278">See [C# Logging](functions-reference-csharp.md#logging) and [Node.js Logging](functions-reference-node.md#writing-trace-output-to-the-console).</span><span class="sxs-lookup"><span data-stu-id="4ac2a-278">See [C# Logging](functions-reference-csharp.md#logging) and [Node.js Logging](functions-reference-node.md#writing-trace-output-to-the-console).</span></span> 

```json
{
    "tracing": {
      "consoleLevel": "verbose",
      "fileLoggingMode": "debugOnly"
    }
}
```

|<span data-ttu-id="4ac2a-279">Property</span><span class="sxs-lookup"><span data-stu-id="4ac2a-279">Property</span></span>  |<span data-ttu-id="4ac2a-280">Default</span><span class="sxs-lookup"><span data-stu-id="4ac2a-280">Default</span></span> | <span data-ttu-id="4ac2a-281">Description</span><span class="sxs-lookup"><span data-stu-id="4ac2a-281">Description</span></span> |
|---------|---------|---------| 
|<span data-ttu-id="4ac2a-282">consoleLevel</span><span class="sxs-lookup"><span data-stu-id="4ac2a-282">consoleLevel</span></span>|<span data-ttu-id="4ac2a-283">info</span><span class="sxs-lookup"><span data-stu-id="4ac2a-283">info</span></span>|<span data-ttu-id="4ac2a-284">The tracing level for console logging.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-284">The tracing level for console logging.</span></span> <span data-ttu-id="4ac2a-285">Options are: `off`, `error`, `warning`, `info`, and `verbose`.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-285">Options are: `off`, `error`, `warning`, `info`, and `verbose`.</span></span>|
|<span data-ttu-id="4ac2a-286">fileLoggingMode</span><span class="sxs-lookup"><span data-stu-id="4ac2a-286">fileLoggingMode</span></span>|<span data-ttu-id="4ac2a-287">debugOnly</span><span class="sxs-lookup"><span data-stu-id="4ac2a-287">debugOnly</span></span>|<span data-ttu-id="4ac2a-288">The tracing level for file logging.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-288">The tracing level for file logging.</span></span> <span data-ttu-id="4ac2a-289">Options are `never`, `always`, `debugOnly`.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-289">Options are `never`, `always`, `debugOnly`.</span></span>| 

## <a name="watchdirectories"></a><span data-ttu-id="4ac2a-290">watchDirectories</span><span class="sxs-lookup"><span data-stu-id="4ac2a-290">watchDirectories</span></span>

<span data-ttu-id="4ac2a-291">A set of [shared code directories](functions-reference-csharp.md#watched-directories) that should be monitored for changes.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-291">A set of [shared code directories](functions-reference-csharp.md#watched-directories) that should be monitored for changes.</span></span>  <span data-ttu-id="4ac2a-292">Ensures that when code in these directories is changed, the changes are picked up by your functions.</span><span class="sxs-lookup"><span data-stu-id="4ac2a-292">Ensures that when code in these directories is changed, the changes are picked up by your functions.</span></span>

```json
{
    "watchDirectories": [ "Shared" ]
}
```

## <a name="next-steps"></a><span data-ttu-id="4ac2a-293">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ac2a-293">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ac2a-294">Learn how to update the host.json file</span><span class="sxs-lookup"><span data-stu-id="4ac2a-294">Learn how to update the host.json file</span></span>](functions-reference.md#fileupdate)

> [!div class="nextstepaction"]
> [<span data-ttu-id="4ac2a-295">See global settings in environment variables</span><span class="sxs-lookup"><span data-stu-id="4ac2a-295">See global settings in environment variables</span></span>](functions-app-settings.md)
