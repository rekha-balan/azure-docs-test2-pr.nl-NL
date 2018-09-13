---
title: Sub-orchestrations for Durable Functions - Azure
description: How to call orchestrations from orchestrations in the Durable Functions extension for Azure Functions.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 59e8eb41b7e9fe3d57196f6844d1a768c3ef598b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969374"
---
# <a name="sub-orchestrations-in-durable-functions-azure-functions"></a><span data-ttu-id="02e12-103">Sub-orchestrations in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="02e12-103">Sub-orchestrations in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="02e12-104">In addition to calling activity functions, orchestrator functions can  call other orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="02e12-104">In addition to calling activity functions, orchestrator functions can  call other orchestrator functions.</span></span> <span data-ttu-id="02e12-105">For example, you can build a larger orchestration out of a library of orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="02e12-105">For example, you can build a larger orchestration out of a library of orchestrator functions.</span></span> <span data-ttu-id="02e12-106">Or you can run multiple instances of an orchestrator function in parallel.</span><span class="sxs-lookup"><span data-stu-id="02e12-106">Or you can run multiple instances of an orchestrator function in parallel.</span></span>

<span data-ttu-id="02e12-107">An orchestrator function can call another orchestrator function by calling the [CallSubOrchestratorAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallSubOrchestratorAsync_) or the [CallSubOrchestratorWithRetryAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallSubOrchestratorWithRetryAsync_) method.</span><span class="sxs-lookup"><span data-stu-id="02e12-107">An orchestrator function can call another orchestrator function by calling the [CallSubOrchestratorAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallSubOrchestratorAsync_) or the [CallSubOrchestratorWithRetryAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallSubOrchestratorWithRetryAsync_) method.</span></span> <span data-ttu-id="02e12-108">The [Error Handling & Compensation](durable-functions-error-handling.md#automatic-retry-on-failure) article has more information on automatic retry.</span><span class="sxs-lookup"><span data-stu-id="02e12-108">The [Error Handling & Compensation](durable-functions-error-handling.md#automatic-retry-on-failure) article has more information on automatic retry.</span></span>

<span data-ttu-id="02e12-109">Sub-orchestrator functions behave just like activity functions from the caller's perspective.</span><span class="sxs-lookup"><span data-stu-id="02e12-109">Sub-orchestrator functions behave just like activity functions from the caller's perspective.</span></span> <span data-ttu-id="02e12-110">They can return a value, throw an exception, and can be awaited by the parent orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="02e12-110">They can return a value, throw an exception, and can be awaited by the parent orchestrator function.</span></span>

> [!NOTE]
> <span data-ttu-id="02e12-111">The `CallSubOrchestratorAsync` and `CallSubOrchestratorWithRetryAsync` methods are not yet available in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="02e12-111">The `CallSubOrchestratorAsync` and `CallSubOrchestratorWithRetryAsync` methods are not yet available in JavaScript.</span></span>

## <a name="example"></a><span data-ttu-id="02e12-112">Example</span><span class="sxs-lookup"><span data-stu-id="02e12-112">Example</span></span>

<span data-ttu-id="02e12-113">The following example illustrates an IoT ("Internet of Things") scenario where there are multiple devices that need to be provisioned.</span><span class="sxs-lookup"><span data-stu-id="02e12-113">The following example illustrates an IoT ("Internet of Things") scenario where there are multiple devices that need to be provisioned.</span></span> <span data-ttu-id="02e12-114">There is a particular orchestration that needs to happen for each of the devices, which might look something like the following:</span><span class="sxs-lookup"><span data-stu-id="02e12-114">There is a particular orchestration that needs to happen for each of the devices, which might look something like the following:</span></span>

```csharp
public static async Task DeviceProvisioningOrchestration(
    [OrchestrationTrigger] DurableOrchestrationContext ctx)
{
    string deviceId = ctx.GetInput<string>();

    // Step 1: Create an installation package in blob storage and return a SAS URL.
    Uri sasUrl = await ctx.CallActivityAsync<Uri>("CreateInstallationPackage", deviceId);

    // Step 2: Notify the device that the installation package is ready.
    await ctx.CallActivityAsync("SendPackageUrlToDevice", Tuple.Create(deviceId, sasUrl));

    // Step 3: Wait for the device to acknowledge that it has downloaded the new package.
    await ctx.WaitForExternalEvent<bool>("DownloadCompletedAck");

    // Step 4: ...
}
```

<span data-ttu-id="02e12-115">This orchestrator function can be used as-is for one-off device provisioning or it can be part of a larger orchestration.</span><span class="sxs-lookup"><span data-stu-id="02e12-115">This orchestrator function can be used as-is for one-off device provisioning or it can be part of a larger orchestration.</span></span> <span data-ttu-id="02e12-116">In the latter case, the parent orchestrator function can schedule instances of `DeviceProvisioningOrchestration` using the `CallSubOrchestratorAsync` API.</span><span class="sxs-lookup"><span data-stu-id="02e12-116">In the latter case, the parent orchestrator function can schedule instances of `DeviceProvisioningOrchestration` using the `CallSubOrchestratorAsync` API.</span></span>

<span data-ttu-id="02e12-117">Here is an example that shows how to run multiple orchestrator functions in parallel.</span><span class="sxs-lookup"><span data-stu-id="02e12-117">Here is an example that shows how to run multiple orchestrator functions in parallel.</span></span>

```csharp
[FunctionName("ProvisionNewDevices")]
public static async Task ProvisionNewDevices(
    [OrchestrationTrigger] DurableOrchestrationContext ctx)
{
    string[] deviceIds = await ctx.CallActivityAsync<string[]>("GetNewDeviceIds");

    // Run multiple device provisioning flows in parallel
    var provisioningTasks = new List<Task>();
    foreach (string deviceId in deviceIds)
    {
        Task provisionTask = ctx.CallSubOrchestratorAsync("DeviceProvisioningOrchestration", deviceId);
        provisioningTasks.Add(provisionTask);
    }

    await Task.WhenAll(provisioningTasks);

    // ...
}
```

## <a name="next-steps"></a><span data-ttu-id="02e12-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="02e12-118">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="02e12-119">Learn what task hubs are and how to configure them</span><span class="sxs-lookup"><span data-stu-id="02e12-119">Learn what task hubs are and how to configure them</span></span>](durable-functions-task-hubs.md)
