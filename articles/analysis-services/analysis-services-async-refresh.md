---
title: Asynchronous refresh for Azure Analysis Services models | Microsoft Docs
description: Learn how to code asynchronous refresh by using REST API.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 883d03b9ffebf85815da7ae62546f75b3d72442f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858126"
---
# <a name="asynchronous-refresh-with-the-rest-api"></a><span data-ttu-id="77792-103">Asynchronous refresh with the REST API</span><span class="sxs-lookup"><span data-stu-id="77792-103">Asynchronous refresh with the REST API</span></span>
<span data-ttu-id="77792-104">By using any programming language that supports REST calls, you can  perform asynchronous data-refresh operations on your Azure Analysis Services tabular models.</span><span class="sxs-lookup"><span data-stu-id="77792-104">By using any programming language that supports REST calls, you can  perform asynchronous data-refresh operations on your Azure Analysis Services tabular models.</span></span> <span data-ttu-id="77792-105">This includes synchronization of read-only replicas for query scale-out.</span><span class="sxs-lookup"><span data-stu-id="77792-105">This includes synchronization of read-only replicas for query scale-out.</span></span> 

<span data-ttu-id="77792-106">Data-refresh operations can take some time depending on a number of factors including data volume, level of optimization using partitions, etc. These operations have traditionally been invoked with existing methods such as using [TOM](https://docs.microsoft.com/sql/analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo) (Tabular Object Model), [PowerShell](https://docs.microsoft.com/sql/analysis-services/powershell/analysis-services-powershell-reference) cmdlets, or [TMSL](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) (Tabular Model Scripting Language).</span><span class="sxs-lookup"><span data-stu-id="77792-106">Data-refresh operations can take some time depending on a number of factors including data volume, level of optimization using partitions, etc. These operations have traditionally been invoked with existing methods such as using [TOM](https://docs.microsoft.com/sql/analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo) (Tabular Object Model), [PowerShell](https://docs.microsoft.com/sql/analysis-services/powershell/analysis-services-powershell-reference) cmdlets, or [TMSL](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) (Tabular Model Scripting Language).</span></span> <span data-ttu-id="77792-107">However, these methods can require often unreliable, long-running HTTP connections.</span><span class="sxs-lookup"><span data-stu-id="77792-107">However, these methods can require often unreliable, long-running HTTP connections.</span></span>

<span data-ttu-id="77792-108">The REST API for Azure Analysis Services enables data-refresh operations to be carried out asynchronously.</span><span class="sxs-lookup"><span data-stu-id="77792-108">The REST API for Azure Analysis Services enables data-refresh operations to be carried out asynchronously.</span></span> <span data-ttu-id="77792-109">By using the REST API, long-running HTTP connections from client applications aren't necessary.</span><span class="sxs-lookup"><span data-stu-id="77792-109">By using the REST API, long-running HTTP connections from client applications aren't necessary.</span></span> <span data-ttu-id="77792-110">There are also other built-in features for reliability, such as auto retries and batched commits.</span><span class="sxs-lookup"><span data-stu-id="77792-110">There are also other built-in features for reliability, such as auto retries and batched commits.</span></span>

## <a name="base-url"></a><span data-ttu-id="77792-111">Base URL</span><span class="sxs-lookup"><span data-stu-id="77792-111">Base URL</span></span>

<span data-ttu-id="77792-112">The base URL follows this format:</span><span class="sxs-lookup"><span data-stu-id="77792-112">The base URL follows this format:</span></span>

```
https://<rollout>.asazure.windows.net/servers/<serverName>/models/<resource>/
```

<span data-ttu-id="77792-113">For example, consider a model named AdventureWorks on a server named myserver, located in the West US Azure region.</span><span class="sxs-lookup"><span data-stu-id="77792-113">For example, consider a model named AdventureWorks on a server named myserver, located in the West US Azure region.</span></span> <span data-ttu-id="77792-114">The server name is:</span><span class="sxs-lookup"><span data-stu-id="77792-114">The server name is:</span></span>

```
asazure://westus.asazure.windows.net/myserver 
```

<span data-ttu-id="77792-115">The base URL for this server name is:</span><span class="sxs-lookup"><span data-stu-id="77792-115">The base URL for this server name is:</span></span>

```
https://westus.asazure.windows.net/servers/myserver/models/AdventureWorks/ 
```

<span data-ttu-id="77792-116">By using the base URL, resources and operations can be appended based on the following parameters:</span><span class="sxs-lookup"><span data-stu-id="77792-116">By using the base URL, resources and operations can be appended based on the following parameters:</span></span> 

![Async refresh](./media/analysis-services-async-refresh/aas-async-refresh-flow.png)

- <span data-ttu-id="77792-118">Anything that ends in **s** is a collection.</span><span class="sxs-lookup"><span data-stu-id="77792-118">Anything that ends in **s** is a collection.</span></span>
- <span data-ttu-id="77792-119">Anything that ends with **()** is a function.</span><span class="sxs-lookup"><span data-stu-id="77792-119">Anything that ends with **()** is a function.</span></span>
- <span data-ttu-id="77792-120">Anything else is a resource/object.</span><span class="sxs-lookup"><span data-stu-id="77792-120">Anything else is a resource/object.</span></span>

<span data-ttu-id="77792-121">For example, you can use the POST verb on the Refreshes collection to perform a refresh operation:</span><span class="sxs-lookup"><span data-stu-id="77792-121">For example, you can use the POST verb on the Refreshes collection to perform a refresh operation:</span></span>

```
https://westus.asazure.windows.net/servers/myserver/models/AdventureWorks/refreshes
```

## <a name="authentication"></a><span data-ttu-id="77792-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="77792-122">Authentication</span></span>

<span data-ttu-id="77792-123">All calls must be authenticated with a valid Azure Active Directory (OAuth 2) token in the Authorization header and must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="77792-123">All calls must be authenticated with a valid Azure Active Directory (OAuth 2) token in the Authorization header and must meet the following requirements:</span></span>

- <span data-ttu-id="77792-124">The token must be either a user token or an application service principal.</span><span class="sxs-lookup"><span data-stu-id="77792-124">The token must be either a user token or an application service principal.</span></span>
- <span data-ttu-id="77792-125">The token must have the correct audience set to `https://*.asazure.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="77792-125">The token must have the correct audience set to `https://*.asazure.windows.net`.</span></span>
- <span data-ttu-id="77792-126">The user or application must have sufficient permissions on the server or model to make the requested call.</span><span class="sxs-lookup"><span data-stu-id="77792-126">The user or application must have sufficient permissions on the server or model to make the requested call.</span></span> <span data-ttu-id="77792-127">The permission level is determined by roles within the model or the admin group on the server.</span><span class="sxs-lookup"><span data-stu-id="77792-127">The permission level is determined by roles within the model or the admin group on the server.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="77792-128">Currently, **server admin** role permissions are necessary.</span><span class="sxs-lookup"><span data-stu-id="77792-128">Currently, **server admin** role permissions are necessary.</span></span>

## <a name="post-refreshes"></a><span data-ttu-id="77792-129">POST /refreshes</span><span class="sxs-lookup"><span data-stu-id="77792-129">POST /refreshes</span></span>

<span data-ttu-id="77792-130">To perform a refresh operation, use the POST verb on the /refreshes collection to add a new refresh item to the collection.</span><span class="sxs-lookup"><span data-stu-id="77792-130">To perform a refresh operation, use the POST verb on the /refreshes collection to add a new refresh item to the collection.</span></span> <span data-ttu-id="77792-131">The Location header in the response includes the refresh ID.</span><span class="sxs-lookup"><span data-stu-id="77792-131">The Location header in the response includes the refresh ID.</span></span> <span data-ttu-id="77792-132">The client application can disconnect and check the status later if required because it is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="77792-132">The client application can disconnect and check the status later if required because it is asynchronous.</span></span>

<span data-ttu-id="77792-133">Only one refresh operation is accepted at a time for a model.</span><span class="sxs-lookup"><span data-stu-id="77792-133">Only one refresh operation is accepted at a time for a model.</span></span> <span data-ttu-id="77792-134">If there's a current running refresh operation and another is submitted, the 409 Conflict HTTP status code is returned.</span><span class="sxs-lookup"><span data-stu-id="77792-134">If there's a current running refresh operation and another is submitted, the 409 Conflict HTTP status code is returned.</span></span>

<span data-ttu-id="77792-135">The body may resemble the following:</span><span class="sxs-lookup"><span data-stu-id="77792-135">The body may resemble the following:</span></span>

```
{
    "Type": "Full",
    "CommitMode": "transactional",
    "MaxParallelism": 2,
    "RetryCount": 2,
    "Objects": [
        {
            "table": "DimCustomer",
            "partition": "DimCustomer"
        },
        {
            "table": "DimDate"
        }
    ]
}
```

### <a name="parameters"></a><span data-ttu-id="77792-136">Parameters</span><span class="sxs-lookup"><span data-stu-id="77792-136">Parameters</span></span>
<span data-ttu-id="77792-137">Specifying parameters is not required.</span><span class="sxs-lookup"><span data-stu-id="77792-137">Specifying parameters is not required.</span></span> <span data-ttu-id="77792-138">The default is applied.</span><span class="sxs-lookup"><span data-stu-id="77792-138">The default is applied.</span></span>

|<span data-ttu-id="77792-139">Name</span><span class="sxs-lookup"><span data-stu-id="77792-139">Name</span></span>  |<span data-ttu-id="77792-140">Type</span><span class="sxs-lookup"><span data-stu-id="77792-140">Type</span></span>  |<span data-ttu-id="77792-141">Description</span><span class="sxs-lookup"><span data-stu-id="77792-141">Description</span></span>  |<span data-ttu-id="77792-142">Default</span><span class="sxs-lookup"><span data-stu-id="77792-142">Default</span></span>  |
|---------|---------|---------|---------|
|<span data-ttu-id="77792-143">Type</span><span class="sxs-lookup"><span data-stu-id="77792-143">Type</span></span>     |  <span data-ttu-id="77792-144">Enum</span><span class="sxs-lookup"><span data-stu-id="77792-144">Enum</span></span>       |  <span data-ttu-id="77792-145">The type of processing to perform.</span><span class="sxs-lookup"><span data-stu-id="77792-145">The type of processing to perform.</span></span> <span data-ttu-id="77792-146">The types are aligned with the TMSL [refresh command](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl) types: full, clearValues, calculate, dataOnly, automatic, and defragment.</span><span class="sxs-lookup"><span data-stu-id="77792-146">The types are aligned with the TMSL [refresh command](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl) types: full, clearValues, calculate, dataOnly, automatic, and defragment.</span></span> <span data-ttu-id="77792-147">Add type is not supported.</span><span class="sxs-lookup"><span data-stu-id="77792-147">Add type is not supported.</span></span>      |   <span data-ttu-id="77792-148">automatic</span><span class="sxs-lookup"><span data-stu-id="77792-148">automatic</span></span>      |
|<span data-ttu-id="77792-149">CommitMode</span><span class="sxs-lookup"><span data-stu-id="77792-149">CommitMode</span></span>     |  <span data-ttu-id="77792-150">Enum</span><span class="sxs-lookup"><span data-stu-id="77792-150">Enum</span></span>       |  <span data-ttu-id="77792-151">Determines if objects will be committed in batches or only when complete.</span><span class="sxs-lookup"><span data-stu-id="77792-151">Determines if objects will be committed in batches or only when complete.</span></span> <span data-ttu-id="77792-152">Modes include: default, transactional, partialBatch.</span><span class="sxs-lookup"><span data-stu-id="77792-152">Modes include: default, transactional, partialBatch.</span></span>  |  <span data-ttu-id="77792-153">transactional</span><span class="sxs-lookup"><span data-stu-id="77792-153">transactional</span></span>       |
|<span data-ttu-id="77792-154">MaxParallelism</span><span class="sxs-lookup"><span data-stu-id="77792-154">MaxParallelism</span></span>     |   <span data-ttu-id="77792-155">Int</span><span class="sxs-lookup"><span data-stu-id="77792-155">Int</span></span>      |  <span data-ttu-id="77792-156">This value determines the maximum number of threads on which to run processing commands in parallel.</span><span class="sxs-lookup"><span data-stu-id="77792-156">This value determines the maximum number of threads on which to run processing commands in parallel.</span></span> <span data-ttu-id="77792-157">This value aligned with the MaxParallelism property that can be set in the TMSL [Sequence command](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl) or using other methods.</span><span class="sxs-lookup"><span data-stu-id="77792-157">This value aligned with the MaxParallelism property that can be set in the TMSL [Sequence command](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl) or using other methods.</span></span>       | <span data-ttu-id="77792-158">10</span><span class="sxs-lookup"><span data-stu-id="77792-158">10</span></span>        |
|<span data-ttu-id="77792-159">RetryCount</span><span class="sxs-lookup"><span data-stu-id="77792-159">RetryCount</span></span>    |    <span data-ttu-id="77792-160">Int</span><span class="sxs-lookup"><span data-stu-id="77792-160">Int</span></span>     |   <span data-ttu-id="77792-161">Indicates the number of times the operation will retry before failing.</span><span class="sxs-lookup"><span data-stu-id="77792-161">Indicates the number of times the operation will retry before failing.</span></span>      |     <span data-ttu-id="77792-162">0</span><span class="sxs-lookup"><span data-stu-id="77792-162">0</span></span>    |
|<span data-ttu-id="77792-163">Objects</span><span class="sxs-lookup"><span data-stu-id="77792-163">Objects</span></span>     |   <span data-ttu-id="77792-164">Array</span><span class="sxs-lookup"><span data-stu-id="77792-164">Array</span></span>      |   <span data-ttu-id="77792-165">An array of objects to be processed.</span><span class="sxs-lookup"><span data-stu-id="77792-165">An array of objects to be processed.</span></span> <span data-ttu-id="77792-166">Each object includes: "table" when processing the entire table or "table" and "partition" when processing a partition.</span><span class="sxs-lookup"><span data-stu-id="77792-166">Each object includes: "table" when processing the entire table or "table" and "partition" when processing a partition.</span></span> <span data-ttu-id="77792-167">If no objects are specified, the whole model is refreshed.</span><span class="sxs-lookup"><span data-stu-id="77792-167">If no objects are specified, the whole model is refreshed.</span></span> |   <span data-ttu-id="77792-168">Process the entire model</span><span class="sxs-lookup"><span data-stu-id="77792-168">Process the entire model</span></span>      |

<span data-ttu-id="77792-169">CommitMode is equal to partialBatch.</span><span class="sxs-lookup"><span data-stu-id="77792-169">CommitMode is equal to partialBatch.</span></span> <span data-ttu-id="77792-170">It's used when doing an initial load of large datasets that could take hours.</span><span class="sxs-lookup"><span data-stu-id="77792-170">It's used when doing an initial load of large datasets that could take hours.</span></span> <span data-ttu-id="77792-171">If the refresh operation fails after successfully committing one or more batches, the successfully committed batches will remain committed (it will not roll back successfully committed batches).</span><span class="sxs-lookup"><span data-stu-id="77792-171">If the refresh operation fails after successfully committing one or more batches, the successfully committed batches will remain committed (it will not roll back successfully committed batches).</span></span>

> [!NOTE]
> <span data-ttu-id="77792-172">At time of writing, the batch size is the MaxParallelism value, but this value could change.</span><span class="sxs-lookup"><span data-stu-id="77792-172">At time of writing, the batch size is the MaxParallelism value, but this value could change.</span></span>

## <a name="get-refreshesrefreshid"></a><span data-ttu-id="77792-173">GET /refreshes/\<refreshId></span><span class="sxs-lookup"><span data-stu-id="77792-173">GET /refreshes/\<refreshId></span></span>

<span data-ttu-id="77792-174">To check the status of a refresh operation, use the GET verb on the refresh ID.</span><span class="sxs-lookup"><span data-stu-id="77792-174">To check the status of a refresh operation, use the GET verb on the refresh ID.</span></span> <span data-ttu-id="77792-175">Here's an example of the response body.</span><span class="sxs-lookup"><span data-stu-id="77792-175">Here's an example of the response body.</span></span> <span data-ttu-id="77792-176">If the operation is in progress, **inProgress** is returned in status.</span><span class="sxs-lookup"><span data-stu-id="77792-176">If the operation is in progress, **inProgress** is returned in status.</span></span>

```
{
    "startTime": "2017-12-07T02:06:57.1838734Z",
    "endTime": "2017-12-07T02:07:00.4929675Z",
    "type": "full",
    "status": "succeeded",
    "currentRefreshType": "full",
    "objects": [
        {
            "table": "DimCustomer",
            "partition": "DimCustomer",
            "status": "succeeded"
        },
        {
            "table": "DimDate",
            "partition": "DimDate",
            "status": "succeeded"
        }
    ]
}
```

## <a name="get-refreshes"></a><span data-ttu-id="77792-177">GET /refreshes</span><span class="sxs-lookup"><span data-stu-id="77792-177">GET /refreshes</span></span>

<span data-ttu-id="77792-178">To get a list of historical refresh operations for a model, use the GET verb on the /refreshes collection.</span><span class="sxs-lookup"><span data-stu-id="77792-178">To get a list of historical refresh operations for a model, use the GET verb on the /refreshes collection.</span></span> <span data-ttu-id="77792-179">Here's an example of the response body.</span><span class="sxs-lookup"><span data-stu-id="77792-179">Here's an example of the response body.</span></span> 

> [!NOTE]
> <span data-ttu-id="77792-180">At time of writing, the last 30 days of refresh operations are stored and returned, but this number could change.</span><span class="sxs-lookup"><span data-stu-id="77792-180">At time of writing, the last 30 days of refresh operations are stored and returned, but this number could change.</span></span>

```
[
    {
        "refreshId": "1344a272-7893-4afa-a4b3-3fb87222fdac",
        "startTime": "2017-12-09T01:58:04.76",
        "endTime": "2017-12-09T01:58:12.607",
        "status": "succeeded"
    },
    {
        "refreshId": "474fc5a0-3d69-4c5d-adb4-8a846fa5580b",
        "startTime": "2017-12-07T02:05:48.32",
        "endTime": "2017-12-07T02:05:54.913",
        "status": "succeeded"
    }
]
```

## <a name="delete-refreshesrefreshid"></a><span data-ttu-id="77792-181">DELETE /refreshes/\<refreshId></span><span class="sxs-lookup"><span data-stu-id="77792-181">DELETE /refreshes/\<refreshId></span></span>

<span data-ttu-id="77792-182">To cancel an in-progress refresh operation, use the DELETE verb on the refresh ID.</span><span class="sxs-lookup"><span data-stu-id="77792-182">To cancel an in-progress refresh operation, use the DELETE verb on the refresh ID.</span></span>

## <a name="post-sync"></a><span data-ttu-id="77792-183">POST /sync</span><span class="sxs-lookup"><span data-stu-id="77792-183">POST /sync</span></span>

<span data-ttu-id="77792-184">Having performed refresh operations, it may be necessary to synchronize the new data with replicas for query scale-out. To perform a synchronize operation for a model, use the POST verb on the /sync function.</span><span class="sxs-lookup"><span data-stu-id="77792-184">Having performed refresh operations, it may be necessary to synchronize the new data with replicas for query scale-out. To perform a synchronize operation for a model, use the POST verb on the /sync function.</span></span> <span data-ttu-id="77792-185">The Location header in the response includes the sync operation ID.</span><span class="sxs-lookup"><span data-stu-id="77792-185">The Location header in the response includes the sync operation ID.</span></span>

## <a name="get-sync-status"></a><span data-ttu-id="77792-186">GET /sync status</span><span class="sxs-lookup"><span data-stu-id="77792-186">GET /sync status</span></span>

<span data-ttu-id="77792-187">To check the status of a sync operation, use the GET verb passing the operation ID as a parameter.</span><span class="sxs-lookup"><span data-stu-id="77792-187">To check the status of a sync operation, use the GET verb passing the operation ID as a parameter.</span></span> <span data-ttu-id="77792-188">Here's an example of the response body:</span><span class="sxs-lookup"><span data-stu-id="77792-188">Here's an example of the response body:</span></span>

```
{
    "operationId": "cd5e16c6-6d4e-4347-86a0-762bdf5b4875",
    "database": "AdventureWorks2",
    "UpdatedAt": "2017-12-09T02:44:26.18",
    "StartedAt": "2017-12-09T02:44:20.743",
    "syncstate": 2,
    "details": null
}
```

<span data-ttu-id="77792-189">Values for `syncstate`:</span><span class="sxs-lookup"><span data-stu-id="77792-189">Values for `syncstate`:</span></span>

- <span data-ttu-id="77792-190">0: Replicating.</span><span class="sxs-lookup"><span data-stu-id="77792-190">0: Replicating.</span></span> <span data-ttu-id="77792-191">Database files are being replicated to a target folder.</span><span class="sxs-lookup"><span data-stu-id="77792-191">Database files are being replicated to a target folder.</span></span>
- <span data-ttu-id="77792-192">1: Rehydrating.</span><span class="sxs-lookup"><span data-stu-id="77792-192">1: Rehydrating.</span></span> <span data-ttu-id="77792-193">The database is being rehydrated on read-only server instance(s).</span><span class="sxs-lookup"><span data-stu-id="77792-193">The database is being rehydrated on read-only server instance(s).</span></span>
- <span data-ttu-id="77792-194">2: Completed.</span><span class="sxs-lookup"><span data-stu-id="77792-194">2: Completed.</span></span> <span data-ttu-id="77792-195">The sync operation completed successfully.</span><span class="sxs-lookup"><span data-stu-id="77792-195">The sync operation completed successfully.</span></span>
- <span data-ttu-id="77792-196">3: Failed.</span><span class="sxs-lookup"><span data-stu-id="77792-196">3: Failed.</span></span> <span data-ttu-id="77792-197">The sync operation failed.</span><span class="sxs-lookup"><span data-stu-id="77792-197">The sync operation failed.</span></span>
- <span data-ttu-id="77792-198">4: Finalizing.</span><span class="sxs-lookup"><span data-stu-id="77792-198">4: Finalizing.</span></span> <span data-ttu-id="77792-199">The sync operation has completed but is performing cleanup steps.</span><span class="sxs-lookup"><span data-stu-id="77792-199">The sync operation has completed but is performing cleanup steps.</span></span>

## <a name="code-sample"></a><span data-ttu-id="77792-200">Code sample</span><span class="sxs-lookup"><span data-stu-id="77792-200">Code sample</span></span>

<span data-ttu-id="77792-201">Here's a C# code sample to get you started, [RestApiSample on GitHub](https://github.com/Microsoft/Analysis-Services/tree/master/RestApiSample).</span><span class="sxs-lookup"><span data-stu-id="77792-201">Here's a C# code sample to get you started, [RestApiSample on GitHub](https://github.com/Microsoft/Analysis-Services/tree/master/RestApiSample).</span></span>

### <a name="to-use-the-code-sample"></a><span data-ttu-id="77792-202">To use the code sample</span><span class="sxs-lookup"><span data-stu-id="77792-202">To use the code sample</span></span>

1.  <span data-ttu-id="77792-203">Clone or download the repo.</span><span class="sxs-lookup"><span data-stu-id="77792-203">Clone or download the repo.</span></span> <span data-ttu-id="77792-204">Open the RestApiSample solution.</span><span class="sxs-lookup"><span data-stu-id="77792-204">Open the RestApiSample solution.</span></span>
2.  <span data-ttu-id="77792-205">Find the line **client.BaseAddress = …**</span><span class="sxs-lookup"><span data-stu-id="77792-205">Find the line **client.BaseAddress = …**</span></span> <span data-ttu-id="77792-206">and provide your [base URL](#base-url).</span><span class="sxs-lookup"><span data-stu-id="77792-206">and provide your [base URL](#base-url).</span></span>

<span data-ttu-id="77792-207">The code sample can use interactive login, username/password, or [service principal](#service-principal).</span><span class="sxs-lookup"><span data-stu-id="77792-207">The code sample can use interactive login, username/password, or [service principal](#service-principal).</span></span>

#### <a name="interactive-login-or-usernamepassword"></a><span data-ttu-id="77792-208">Interactive login or username/password</span><span class="sxs-lookup"><span data-stu-id="77792-208">Interactive login or username/password</span></span>

<span data-ttu-id="77792-209">This form of authentication requires an Azure application be created with the necessary API permissions assigned.</span><span class="sxs-lookup"><span data-stu-id="77792-209">This form of authentication requires an Azure application be created with the necessary API permissions assigned.</span></span> 

1.  <span data-ttu-id="77792-210">In Azure portal, click **Create a resource** > **Azure Active Directory** > **App registrations** > **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="77792-210">In Azure portal, click **Create a resource** > **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

    ![New Application registration](./media/analysis-services-async-refresh/aas-async-app-reg.png)


2.  <span data-ttu-id="77792-212">In **Create**, type a name, select **Native** application type.</span><span class="sxs-lookup"><span data-stu-id="77792-212">In **Create**, type a name, select **Native** application type.</span></span> <span data-ttu-id="77792-213">For **Redirect URI**, enter **urn:ietf:wg:oauth:2.0:oob**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="77792-213">For **Redirect URI**, enter **urn:ietf:wg:oauth:2.0:oob**, and then click **Create**.</span></span>

    ![Settings](./media/analysis-services-async-refresh/aas-async-app-reg-name.png)

3.  <span data-ttu-id="77792-215">Select your app and then copy and save the **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="77792-215">Select your app and then copy and save the **Application ID**.</span></span>

    ![Copy application ID](./media/analysis-services-async-refresh/aas-async-app-id.png)

4.  <span data-ttu-id="77792-217">In **Settings**, click **Required permissions** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="77792-217">In **Settings**, click **Required permissions** > **Add**.</span></span>

    ![Add API access](./media/analysis-services-async-refresh/aas-async-add.png)

5.  <span data-ttu-id="77792-219">In **Select an API**, type **Azure Analysis Services** into the search box, and then select it.</span><span class="sxs-lookup"><span data-stu-id="77792-219">In **Select an API**, type **Azure Analysis Services** into the search box, and then select it.</span></span>

    ![Select API](./media/analysis-services-async-refresh/aas-async-select-api.png)

6.  <span data-ttu-id="77792-221">Select **Read and Write all Models**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="77792-221">Select **Read and Write all Models**, and then click **Select**.</span></span> <span data-ttu-id="77792-222">When both are selected, click **Done** to add the permissions.</span><span class="sxs-lookup"><span data-stu-id="77792-222">When both are selected, click **Done** to add the permissions.</span></span> <span data-ttu-id="77792-223">It may take a few minutes to propagate.</span><span class="sxs-lookup"><span data-stu-id="77792-223">It may take a few minutes to propagate.</span></span>

    ![Select Read and Write all models](./media/analysis-services-async-refresh/aas-async-select-read.png)

7.  <span data-ttu-id="77792-225">In the code sample, find the **UpdateToken()** method.</span><span class="sxs-lookup"><span data-stu-id="77792-225">In the code sample, find the **UpdateToken()** method.</span></span> <span data-ttu-id="77792-226">Observe the contents of this method.</span><span class="sxs-lookup"><span data-stu-id="77792-226">Observe the contents of this method.</span></span>
8.  <span data-ttu-id="77792-227">Find **string clientID = …**, and then enter the **Application ID** you copied from step 3.</span><span class="sxs-lookup"><span data-stu-id="77792-227">Find **string clientID = …**, and then enter the **Application ID** you copied from step 3.</span></span>
9.  <span data-ttu-id="77792-228">Run the sample.</span><span class="sxs-lookup"><span data-stu-id="77792-228">Run the sample.</span></span>

#### <a name="service-principal"></a><span data-ttu-id="77792-229">Service principal</span><span class="sxs-lookup"><span data-stu-id="77792-229">Service principal</span></span>

<span data-ttu-id="77792-230">See [Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) and [Add a service principal to the server administrator role](analysis-services-addservprinc-admins.md) for more info on how to set up a service principal and assign the necessary permissions in Azure AS.</span><span class="sxs-lookup"><span data-stu-id="77792-230">See [Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) and [Add a service principal to the server administrator role](analysis-services-addservprinc-admins.md) for more info on how to set up a service principal and assign the necessary permissions in Azure AS.</span></span> <span data-ttu-id="77792-231">Once you've completed the steps, complete the following additional steps:</span><span class="sxs-lookup"><span data-stu-id="77792-231">Once you've completed the steps, complete the following additional steps:</span></span>

1.  <span data-ttu-id="77792-232">In the code sample, find **string authority = …**, replace **common** with your organization’s tenant ID.</span><span class="sxs-lookup"><span data-stu-id="77792-232">In the code sample, find **string authority = …**, replace **common** with your organization’s tenant ID.</span></span>
2.  <span data-ttu-id="77792-233">Comment/uncomment so the ClientCredential class is used to instantiate the cred object.</span><span class="sxs-lookup"><span data-stu-id="77792-233">Comment/uncomment so the ClientCredential class is used to instantiate the cred object.</span></span> <span data-ttu-id="77792-234">Ensure the \<App ID> and \<App Key> values are accessed in a secure way or use certificate-based authentication for service principals.</span><span class="sxs-lookup"><span data-stu-id="77792-234">Ensure the \<App ID> and \<App Key> values are accessed in a secure way or use certificate-based authentication for service principals.</span></span>
3.  <span data-ttu-id="77792-235">Run the sample.</span><span class="sxs-lookup"><span data-stu-id="77792-235">Run the sample.</span></span>


## <a name="see-also"></a><span data-ttu-id="77792-236">See also</span><span class="sxs-lookup"><span data-stu-id="77792-236">See also</span></span>

<span data-ttu-id="77792-237">[Samples](analysis-services-samples.md) </span><span class="sxs-lookup"><span data-stu-id="77792-237">[Samples](analysis-services-samples.md) </span></span>  
[<span data-ttu-id="77792-238">REST API</span><span class="sxs-lookup"><span data-stu-id="77792-238">REST API</span></span>](https://docs.microsoft.com/rest/api/analysisservices/servers)   


