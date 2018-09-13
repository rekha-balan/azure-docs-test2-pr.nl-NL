---
title: Durable Functions publishing to Azure Event Grid (preview)
description: Learn how to configure automatic Azure Event Grid publishing for Durable Functions.
services: functions
author: ggailey777
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: glenga
ms.openlocfilehash: dff0aace6c46340f07ff6fb4fd7f92ee93b7fa8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858125"
---
# <a name="durable-functions-publishing-to-azure-event-grid-preview"></a><span data-ttu-id="0aa61-103">Durable Functions publishing to Azure Event Grid (preview)</span><span class="sxs-lookup"><span data-stu-id="0aa61-103">Durable Functions publishing to Azure Event Grid (preview)</span></span>

<span data-ttu-id="0aa61-104">This article shows how to set up Azure Durable Functions to publish orchestration lifecycle events (such as created, completed, and failed) to a custom [Azure Event Grid Topic](https://docs.microsoft.com/azure/event-grid/overview).</span><span class="sxs-lookup"><span data-stu-id="0aa61-104">This article shows how to set up Azure Durable Functions to publish orchestration lifecycle events (such as created, completed, and failed) to a custom [Azure Event Grid Topic](https://docs.microsoft.com/azure/event-grid/overview).</span></span> 

<span data-ttu-id="0aa61-105">Following are some scenarios where this feature is useful:</span><span class="sxs-lookup"><span data-stu-id="0aa61-105">Following are some scenarios where this feature is useful:</span></span>

* <span data-ttu-id="0aa61-106">**DevOps scenarios like blue/green deployments**: You might want to know if any tasks are running before implementing the  [side-by-side deployment strategy](https://docs.microsoft.com/azure/azure-functions/durable-functions-versioning#side-by-side-deployments).</span><span class="sxs-lookup"><span data-stu-id="0aa61-106">**DevOps scenarios like blue/green deployments**: You might want to know if any tasks are running before implementing the  [side-by-side deployment strategy](https://docs.microsoft.com/azure/azure-functions/durable-functions-versioning#side-by-side-deployments).</span></span>

* <span data-ttu-id="0aa61-107">**Advanced monitoring and diagnostics support**: You can keep track of orchestration status information in an external store optimized for queries, such as SQL database or CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="0aa61-107">**Advanced monitoring and diagnostics support**: You can keep track of orchestration status information in an external store optimized for queries, such as SQL database or CosmosDB.</span></span>

* <span data-ttu-id="0aa61-108">**Long-running background activity**: If you use Durable Functions for a long-running background activity, this feature helps you to know the current status.</span><span class="sxs-lookup"><span data-stu-id="0aa61-108">**Long-running background activity**: If you use Durable Functions for a long-running background activity, this feature helps you to know the current status.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aa61-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0aa61-109">Prerequisites</span></span>

* <span data-ttu-id="0aa61-110">Install [Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask) 1.3.0-rc or later in your Durable Functions project.</span><span class="sxs-lookup"><span data-stu-id="0aa61-110">Install [Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask) 1.3.0-rc or later in your Durable Functions project.</span></span>
* <span data-ttu-id="0aa61-111">Install [Azure Storage Emulator](https://docs.microsoft.com/azure/storage/common/storage-use-emulator).</span><span class="sxs-lookup"><span data-stu-id="0aa61-111">Install [Azure Storage Emulator](https://docs.microsoft.com/azure/storage/common/storage-use-emulator).</span></span>
* <span data-ttu-id="0aa61-112">Install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest) or use [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)</span><span class="sxs-lookup"><span data-stu-id="0aa61-112">Install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest) or use [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)</span></span>

## <a name="create-a-custom-event-grid-topic"></a><span data-ttu-id="0aa61-113">Create a custom Event Grid topic</span><span class="sxs-lookup"><span data-stu-id="0aa61-113">Create a custom Event Grid topic</span></span>

<span data-ttu-id="0aa61-114">Create an Event Grid topic for sending events from Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="0aa61-114">Create an Event Grid topic for sending events from Durable Functions.</span></span> <span data-ttu-id="0aa61-115">The following instructions show how to create a topic by using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0aa61-115">The following instructions show how to create a topic by using Azure CLI.</span></span> <span data-ttu-id="0aa61-116">For information about how to do it by using PowerShell or the Azure portal, refer to the following articles:</span><span class="sxs-lookup"><span data-stu-id="0aa61-116">For information about how to do it by using PowerShell or the Azure portal, refer to the following articles:</span></span>

* [<span data-ttu-id="0aa61-117">EventGrid Quickstarts: Create custom event - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0aa61-117">EventGrid Quickstarts: Create custom event - PowerShell</span></span>](https://docs.microsoft.com/azure/event-grid/custom-event-quickstart-powershell)
* [<span data-ttu-id="0aa61-118">EventGrid Quickstarts: Create custom event - Azure portal</span><span class="sxs-lookup"><span data-stu-id="0aa61-118">EventGrid Quickstarts: Create custom event - Azure portal</span></span>](https://docs.microsoft.com/azure/event-grid/custom-event-quickstart-portal)

### <a name="create-a-resource-group"></a><span data-ttu-id="0aa61-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="0aa61-119">Create a resource group</span></span>

<span data-ttu-id="0aa61-120">Create a resource group with the `az group create` command.</span><span class="sxs-lookup"><span data-stu-id="0aa61-120">Create a resource group with the `az group create` command.</span></span> <span data-ttu-id="0aa61-121">Currently, Event Grid doesn't support all regions.</span><span class="sxs-lookup"><span data-stu-id="0aa61-121">Currently, Event Grid doesn't support all regions.</span></span> <span data-ttu-id="0aa61-122">For information about which regions are supported, see the [Event Grid overview](https://docs.microsoft.com/azure/event-grid/overview).</span><span class="sxs-lookup"><span data-stu-id="0aa61-122">For information about which regions are supported, see the [Event Grid overview](https://docs.microsoft.com/azure/event-grid/overview).</span></span> 

```bash
az group create --name eventResourceGroup --location westus2
```

### <a name="create-a-custom-topic"></a><span data-ttu-id="0aa61-123">Create a custom topic</span><span class="sxs-lookup"><span data-stu-id="0aa61-123">Create a custom topic</span></span>

<span data-ttu-id="0aa61-124">An Event Grid topic provides a user-defined endpoint that you post your event to.</span><span class="sxs-lookup"><span data-stu-id="0aa61-124">An Event Grid topic provides a user-defined endpoint that you post your event to.</span></span> <span data-ttu-id="0aa61-125">Replace `<topic_name>` with a unique name for your topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="0aa61-126">The topic name must be unique because it becomes a DNS entry.</span><span class="sxs-lookup"><span data-stu-id="0aa61-126">The topic name must be unique because it becomes a DNS entry.</span></span>

```bash
az eventgrid topic create --name <topic_name> -l westus2 -g eventResourceGroup 
```

## <a name="get-the-endpoint-and-key"></a><span data-ttu-id="0aa61-127">Get the endpoint and key</span><span class="sxs-lookup"><span data-stu-id="0aa61-127">Get the endpoint and key</span></span>

<span data-ttu-id="0aa61-128">Get the endpoint of the topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-128">Get the endpoint of the topic.</span></span> <span data-ttu-id="0aa61-129">Replace `<topic_name>` with the name you chose.</span><span class="sxs-lookup"><span data-stu-id="0aa61-129">Replace `<topic_name>` with the name you chose.</span></span>

```bash
az eventgrid topic show --name <topic_name> -g eventResourceGroup --query "endpoint" --output tsv
```

<span data-ttu-id="0aa61-130">Get the topic key.</span><span class="sxs-lookup"><span data-stu-id="0aa61-130">Get the topic key.</span></span> <span data-ttu-id="0aa61-131">Replace `<topic_name>` with the name you chose.</span><span class="sxs-lookup"><span data-stu-id="0aa61-131">Replace `<topic_name>` with the name you chose.</span></span>

```bash
az eventgrid topic key list --name <topic_name> -g eventResourceGroup --query "key1" --output tsv
```

<span data-ttu-id="0aa61-132">Now you can send events to the topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-132">Now you can send events to the topic.</span></span>

## <a name="configure-azure-event-grid-publishing"></a><span data-ttu-id="0aa61-133">Configure Azure Event Grid publishing</span><span class="sxs-lookup"><span data-stu-id="0aa61-133">Configure Azure Event Grid publishing</span></span>

<span data-ttu-id="0aa61-134">In your Durable Functions project, find the `host.json` file.</span><span class="sxs-lookup"><span data-stu-id="0aa61-134">In your Durable Functions project, find the `host.json` file.</span></span>

<span data-ttu-id="0aa61-135">Add `EventGridTopicEndpoint` and `EventGridKeySettingName` in a `durableTask` property.</span><span class="sxs-lookup"><span data-stu-id="0aa61-135">Add `EventGridTopicEndpoint` and `EventGridKeySettingName` in a `durableTask` property.</span></span>

```json
{
    "durableTask": {
        "EventGridTopicEndpoint": "https://<topic_name>.westus2-1.eventgrid.azure.net/api/events",
        "EventGridKeySettingName": "EventGridKey"
    }
}
```

<span data-ttu-id="0aa61-136">The possible Azure Event Grid configuration properties are as follows:</span><span class="sxs-lookup"><span data-stu-id="0aa61-136">The possible Azure Event Grid configuration properties are as follows:</span></span>

* <span data-ttu-id="0aa61-137">**EventGridTopicEndpoint** - The endpoint of the Event Grid Topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-137">**EventGridTopicEndpoint** - The endpoint of the Event Grid Topic.</span></span> <span data-ttu-id="0aa61-138">The *%AppSettingName%* syntax can be used to resolve this value from application settings or environment variables.</span><span class="sxs-lookup"><span data-stu-id="0aa61-138">The *%AppSettingName%* syntax can be used to resolve this value from application settings or environment variables.</span></span>
* <span data-ttu-id="0aa61-139">**EventGridKeySettingName** - The key of the application setting on your Azure Function.</span><span class="sxs-lookup"><span data-stu-id="0aa61-139">**EventGridKeySettingName** - The key of the application setting on your Azure Function.</span></span> <span data-ttu-id="0aa61-140">Durable Functions will get the Event Grid Topic key from the value.</span><span class="sxs-lookup"><span data-stu-id="0aa61-140">Durable Functions will get the Event Grid Topic key from the value.</span></span>
* <span data-ttu-id="0aa61-141">**EventGridPublishRetryCount** - [Optional] The number of times to retry if publishing to the Event Grid topic fails.</span><span class="sxs-lookup"><span data-stu-id="0aa61-141">**EventGridPublishRetryCount** - [Optional] The number of times to retry if publishing to the Event Grid topic fails.</span></span>
* <span data-ttu-id="0aa61-142">**EventGridPublishRetryInterval** - [Optional] The Event Grid publish retry interval in the *hh:mm:ss* format.</span><span class="sxs-lookup"><span data-stu-id="0aa61-142">**EventGridPublishRetryInterval** - [Optional] The Event Grid publish retry interval in the *hh:mm:ss* format.</span></span> <span data-ttu-id="0aa61-143">If not specified, the default retry interval is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="0aa61-143">If not specified, the default retry interval is 5 minutes.</span></span>

<span data-ttu-id="0aa61-144">Once you configure the `host.json` file, Your Durable Functions project starts to send lifecycle events to the Event Grid topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-144">Once you configure the `host.json` file, Your Durable Functions project starts to send lifecycle events to the Event Grid topic.</span></span> <span data-ttu-id="0aa61-145">This works when you run in the Function App and when you run locally.</span><span class="sxs-lookup"><span data-stu-id="0aa61-145">This works when you run in the Function App and when you run locally.</span></span>

<span data-ttu-id="0aa61-146">Set the app setting for the topic key in the Function App and `local.setting.json`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-146">Set the app setting for the topic key in the Function App and `local.setting.json`.</span></span> <span data-ttu-id="0aa61-147">The following JSON is a sample of the `local.settings.json` for local debugging.</span><span class="sxs-lookup"><span data-stu-id="0aa61-147">The following JSON is a sample of the `local.settings.json` for local debugging.</span></span> <span data-ttu-id="0aa61-148">Replace `<topic_key>` with the topic key.</span><span class="sxs-lookup"><span data-stu-id="0aa61-148">Replace `<topic_key>` with the topic key.</span></span>  

```json
{
    "IsEncrypted": false,
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
        "EventGridKey": "<topic_key>"
    }
}
```

<span data-ttu-id="0aa61-149">Make sure that [Storage Emulator](https://docs.microsoft.com/azure/storage/common/storage-use-emulator) is working.</span><span class="sxs-lookup"><span data-stu-id="0aa61-149">Make sure that [Storage Emulator](https://docs.microsoft.com/azure/storage/common/storage-use-emulator) is working.</span></span> <span data-ttu-id="0aa61-150">It's a good idea to run the `AzureStorageEmulator.exe clear all` command before executing.</span><span class="sxs-lookup"><span data-stu-id="0aa61-150">It's a good idea to run the `AzureStorageEmulator.exe clear all` command before executing.</span></span>

## <a name="create-functions-that-listen-for-events"></a><span data-ttu-id="0aa61-151">Create functions that listen for events</span><span class="sxs-lookup"><span data-stu-id="0aa61-151">Create functions that listen for events</span></span>

<span data-ttu-id="0aa61-152">Create a Function App.</span><span class="sxs-lookup"><span data-stu-id="0aa61-152">Create a Function App.</span></span> <span data-ttu-id="0aa61-153">It's best to locate it in the same region as the Event Grid Topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-153">It's best to locate it in the same region as the Event Grid Topic.</span></span>

### <a name="create-an-event-grid-trigger-function"></a><span data-ttu-id="0aa61-154">Create an Event Grid trigger function</span><span class="sxs-lookup"><span data-stu-id="0aa61-154">Create an Event Grid trigger function</span></span>

<span data-ttu-id="0aa61-155">Create a function to receive the lifecycle events.</span><span class="sxs-lookup"><span data-stu-id="0aa61-155">Create a function to receive the lifecycle events.</span></span> <span data-ttu-id="0aa61-156">Select **Custom Function**.</span><span class="sxs-lookup"><span data-stu-id="0aa61-156">Select **Custom Function**.</span></span> 

![Select a Create a custom function.](media/durable-functions-event-publishing/functions-portal.png)

<span data-ttu-id="0aa61-158">Choose Event Grid Trigger, and select `C#`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-158">Choose Event Grid Trigger, and select `C#`.</span></span>

![Select the Event Grid Trigger.](media/durable-functions-event-publishing/eventgrid-trigger.png)

<span data-ttu-id="0aa61-160">Enter the name of the function, and then select `Create`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-160">Enter the name of the function, and then select `Create`.</span></span>

![Create the Event Grid Trigger.](media/durable-functions-event-publishing/eventgrid-trigger-creation.png)

<span data-ttu-id="0aa61-162">A function with the following code is created:</span><span class="sxs-lookup"><span data-stu-id="0aa61-162">A function with the following code is created:</span></span> 

```csharp
#r "Newtonsoft.Json"
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
public static void Run(JObject eventGridEvent, TraceWriter log)
{
    log.Info(eventGridEvent.ToString(Formatting.Indented));
}
```

<span data-ttu-id="0aa61-163">Select `Add Event Grid Subscription`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-163">Select `Add Event Grid Subscription`.</span></span> <span data-ttu-id="0aa61-164">This operation adds an Event Grid subscription for the Event Grid topic that you created.</span><span class="sxs-lookup"><span data-stu-id="0aa61-164">This operation adds an Event Grid subscription for the Event Grid topic that you created.</span></span> <span data-ttu-id="0aa61-165">For more information, see [Concepts in Azure Event Grid](https://docs.microsoft.com/azure/event-grid/concepts)</span><span class="sxs-lookup"><span data-stu-id="0aa61-165">For more information, see [Concepts in Azure Event Grid](https://docs.microsoft.com/azure/event-grid/concepts)</span></span>

![Select the Event Grid Trigger link.](media/durable-functions-event-publishing/eventgrid-trigger-link.png)

<span data-ttu-id="0aa61-167">Select `Event Grid Topics` for **Topic Type**.</span><span class="sxs-lookup"><span data-stu-id="0aa61-167">Select `Event Grid Topics` for **Topic Type**.</span></span> <span data-ttu-id="0aa61-168">Select the resource group that you created for the Event Grid topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-168">Select the resource group that you created for the Event Grid topic.</span></span> <span data-ttu-id="0aa61-169">Then select the instance of the Event Grid topic.</span><span class="sxs-lookup"><span data-stu-id="0aa61-169">Then select the instance of the Event Grid topic.</span></span> <span data-ttu-id="0aa61-170">Press `Create`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-170">Press `Create`.</span></span>

![Create an Event Grid subscription.](media/durable-functions-event-publishing/eventsubscription.png)

<span data-ttu-id="0aa61-172">Now you're ready to receive lifecycle events.</span><span class="sxs-lookup"><span data-stu-id="0aa61-172">Now you're ready to receive lifecycle events.</span></span> 

## <a name="create-durable-functions-to-send-the-events"></a><span data-ttu-id="0aa61-173">Create Durable Functions to send the events.</span><span class="sxs-lookup"><span data-stu-id="0aa61-173">Create Durable Functions to send the events.</span></span>

<span data-ttu-id="0aa61-174">In your Durable Functions project, start debugging on your local machine.</span><span class="sxs-lookup"><span data-stu-id="0aa61-174">In your Durable Functions project, start debugging on your local machine.</span></span>  <span data-ttu-id="0aa61-175">The following code is the same as the template code for the Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="0aa61-175">The following code is the same as the template code for the Durable Functions.</span></span> <span data-ttu-id="0aa61-176">You already configured `host.json` and `local.settings.json` on your local machine.</span><span class="sxs-lookup"><span data-stu-id="0aa61-176">You already configured `host.json` and `local.settings.json` on your local machine.</span></span> 

```csharp
using System.Collections.Generic;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;

namespace LifeCycleEventSpike
{
    public static class Sample
    {
    {
        [FunctionName("Sample")]
        public static async Task<List<string>> RunOrchestrator(
            [OrchestrationTrigger] DurableOrchestrationContext context)
        {
            var outputs = new List<string>();

            // Replace "hello" with the name of your Durable Activity Function.
            outputs.Add(await context.CallActivityAsync<string>("Sample_Hello", "Tokyo"));
            outputs.Add(await context.CallActivityAsync<string>("Sample_Hello", "Seattle"));
            outputs.Add(await context.CallActivityAsync<string>("Sample_Hello", "London"));

            // returns ["Hello Tokyo!", "Hello Seattle!", "Hello London!"]
            return outputs;
        }

        [FunctionName("Sample_Hello")]
        public static string SayHello([ActivityTrigger] string name, TraceWriter log)
        {
            log.Info($"Saying hello to {name}.");
            return $"Hello {name}!";
        }

        [FunctionName("Sample_HttpStart")]
        public static async Task<HttpResponseMessage> HttpStart(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")]HttpRequestMessage req,
            [OrchestrationClient]DurableOrchestrationClient starter,
            TraceWriter log)
        {
            // Function input comes from the request content.
            string instanceId = await starter.StartNewAsync("Sample", null);
            log.Info($"Started orchestration with ID = '{instanceId}'.");
            return starter.CreateCheckStatusResponse(req, instanceId);
        }
    }
}
```

<span data-ttu-id="0aa61-177">If you call the `Sample_HttpStart` with Postman or your browser, Durable Function starts to send lifecycle events.</span><span class="sxs-lookup"><span data-stu-id="0aa61-177">If you call the `Sample_HttpStart` with Postman or your browser, Durable Function starts to send lifecycle events.</span></span> <span data-ttu-id="0aa61-178">The endpoint is usually `http://localhost:7071/api/Sample_HttpStart` for local debugging.</span><span class="sxs-lookup"><span data-stu-id="0aa61-178">The endpoint is usually `http://localhost:7071/api/Sample_HttpStart` for local debugging.</span></span>

<span data-ttu-id="0aa61-179">See the logs from the function that you created in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0aa61-179">See the logs from the function that you created in the Azure portal.</span></span>

```
2018-04-20T09:28:21.041 [Info] Function started (Id=3301c3ef-625f-40ce-ad4c-9ba2916b162d)
2018-04-20T09:28:21.104 [Info] {
    "id": "054fe385-c017-4ce3-b38a-052ac970c39d",    
    "subject": "durable/orchestrator/Running",
    "data": {
        "hubName": "DurableFunctionsHub",
        "functionName": "Sample",
        "instanceId": "055d045b1c8a415b94f7671d8df693a6",
        "reason": "",
        "runtimeStatus": "Running"
    },
    "eventType": "orchestratorEvent",
    "eventTime": "2018-04-20T09:28:19.6492068Z",
    "dataVersion": "1.0",
    "metadataVersion": "1",
    "topic": "/subscriptions/<your_subscription_id>/resourceGroups/eventResourceGroup/providers/Microsoft.EventGrid/topics/durableTopic"
}

2018-04-20T09:28:21.104 [Info] Function completed (Success, Id=3301c3ef-625f-40ce-ad4c-9ba2916b162d, Duration=65ms)
2018-04-20T09:28:37.098 [Info] Function started (Id=36fadea5-198b-4345-bb8e-2837febb89a2)
2018-04-20T09:28:37.098 [Info] {
    "id": "8cf17246-fa9c-4dad-b32a-5a868104f17b",
    "subject": "durable/orchestrator/Completed",
    "data": {
        "hubName": "DurableFunctionsHub",
        "functionName": "Sample",
        "instanceId": "055d045b1c8a415b94f7671d8df693a6",
        "reason": "",
        "runtimeStatus": "Completed"
    },
    "eventType": "orchestratorEvent",
    "eventTime": "2018-04-20T09:28:36.5061317Z",
    "dataVersion": "1.0",
    "metadataVersion": "1",
    "topic": "/subscriptions/<your_subscription_id>/resourceGroups/eventResourceGroup/providers/Microsoft.EventGrid/topics/durableTopic"
}
2018-04-20T09:28:37.098 [Info] Function completed (Success, Id=36fadea5-198b-4345-bb8e-2837febb89a2, Duration=0ms)
```

## <a name="event-schema"></a><span data-ttu-id="0aa61-180">Event Schema</span><span class="sxs-lookup"><span data-stu-id="0aa61-180">Event Schema</span></span>

<span data-ttu-id="0aa61-181">The following list explains the lifecycle events schema:</span><span class="sxs-lookup"><span data-stu-id="0aa61-181">The following list explains the lifecycle events schema:</span></span>

* <span data-ttu-id="0aa61-182">**id**: Unique identifier for the Event Grid event.</span><span class="sxs-lookup"><span data-stu-id="0aa61-182">**id**: Unique identifier for the Event Grid event.</span></span>
* <span data-ttu-id="0aa61-183">**subject**: Path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="0aa61-183">**subject**: Path to the event subject.</span></span> <span data-ttu-id="0aa61-184">`durable/orchestrator/{orchestrationRuntimeStatus}`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-184">`durable/orchestrator/{orchestrationRuntimeStatus}`.</span></span> <span data-ttu-id="0aa61-185">`{orchestrationRuntimeStatus}` will be `Running`, `Completed`, `Failed`, and `Terminated`.</span><span class="sxs-lookup"><span data-stu-id="0aa61-185">`{orchestrationRuntimeStatus}` will be `Running`, `Completed`, `Failed`, and `Terminated`.</span></span>  
* <span data-ttu-id="0aa61-186">**data**: Durable Functions Specific Parameters.</span><span class="sxs-lookup"><span data-stu-id="0aa61-186">**data**: Durable Functions Specific Parameters.</span></span>
    * <span data-ttu-id="0aa61-187">**hubName**: [TaskHub](https://docs.microsoft.com/azure/azure-functions/durable-functions-task-hubs) name.</span><span class="sxs-lookup"><span data-stu-id="0aa61-187">**hubName**: [TaskHub](https://docs.microsoft.com/azure/azure-functions/durable-functions-task-hubs) name.</span></span>
    * <span data-ttu-id="0aa61-188">**functionName**: Orchestrator function name.</span><span class="sxs-lookup"><span data-stu-id="0aa61-188">**functionName**: Orchestrator function name.</span></span>
    * <span data-ttu-id="0aa61-189">**instanceId**: Durable Functions instanceId.</span><span class="sxs-lookup"><span data-stu-id="0aa61-189">**instanceId**: Durable Functions instanceId.</span></span>
    * <span data-ttu-id="0aa61-190">**reason**: Additional data associated with the tracking event.</span><span class="sxs-lookup"><span data-stu-id="0aa61-190">**reason**: Additional data associated with the tracking event.</span></span> <span data-ttu-id="0aa61-191">For more information, see [Diagnostics in Durable Functions (Azure Functions)](https://docs.microsoft.com/azure/azure-functions/durable-functions-diagnostics)</span><span class="sxs-lookup"><span data-stu-id="0aa61-191">For more information, see [Diagnostics in Durable Functions (Azure Functions)](https://docs.microsoft.com/azure/azure-functions/durable-functions-diagnostics)</span></span>
    * <span data-ttu-id="0aa61-192">**runtimeStatus**: Orchestration Runtime Status.</span><span class="sxs-lookup"><span data-stu-id="0aa61-192">**runtimeStatus**: Orchestration Runtime Status.</span></span> <span data-ttu-id="0aa61-193">Running, Completed, Failed, Canceled.</span><span class="sxs-lookup"><span data-stu-id="0aa61-193">Running, Completed, Failed, Canceled.</span></span> 
* <span data-ttu-id="0aa61-194">**eventType**: "orchestratorEvent"</span><span class="sxs-lookup"><span data-stu-id="0aa61-194">**eventType**: "orchestratorEvent"</span></span>
* <span data-ttu-id="0aa61-195">**eventTime**: Event time (UTC).</span><span class="sxs-lookup"><span data-stu-id="0aa61-195">**eventTime**: Event time (UTC).</span></span>
* <span data-ttu-id="0aa61-196">**dataVersion**: Version of the lifecycle event schema.</span><span class="sxs-lookup"><span data-stu-id="0aa61-196">**dataVersion**: Version of the lifecycle event schema.</span></span>
* <span data-ttu-id="0aa61-197">**metadataVersion**:  Version of the metadata.</span><span class="sxs-lookup"><span data-stu-id="0aa61-197">**metadataVersion**:  Version of the metadata.</span></span>
* <span data-ttu-id="0aa61-198">**topic**: EventGrid Topic resource.</span><span class="sxs-lookup"><span data-stu-id="0aa61-198">**topic**: EventGrid Topic resource.</span></span>

## <a name="how-to-test-locally"></a><span data-ttu-id="0aa61-199">How to test locally</span><span class="sxs-lookup"><span data-stu-id="0aa61-199">How to test locally</span></span>

<span data-ttu-id="0aa61-200">To test locally, use [ngrok](functions-bindings-event-grid.md#local-testing-with-ngrok).</span><span class="sxs-lookup"><span data-stu-id="0aa61-200">To test locally, use [ngrok](functions-bindings-event-grid.md#local-testing-with-ngrok).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aa61-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="0aa61-201">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0aa61-202">Learn instance management in Durable Functions</span><span class="sxs-lookup"><span data-stu-id="0aa61-202">Learn instance management in Durable Functions</span></span>](durable-functions-instance-management.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="0aa61-203">Learn versioning in Durable Functions</span><span class="sxs-lookup"><span data-stu-id="0aa61-203">Learn versioning in Durable Functions</span></span>](durable-functions-versioning.md)
