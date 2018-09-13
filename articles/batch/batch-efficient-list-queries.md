---
title: Design efficient list queries - Azure Batch | Microsoft Docs
description: Increase performance by filtering your queries when requesting information on Batch resources like pools, jobs, tasks, and compute nodes.
services: batch
documentationcenter: .net
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 06/26/2018
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6bc31e8541797930583e41fb6efbb6473cd4b894
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808768"
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="30278-103">Create queries to list Batch resources efficiently</span><span class="sxs-lookup"><span data-stu-id="30278-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="30278-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, compute nodes, and other resources with the [Batch .NET][api_net] library.</span><span class="sxs-lookup"><span data-stu-id="30278-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, compute nodes, and other resources with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="30278-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="30278-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="30278-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span><span class="sxs-lookup"><span data-stu-id="30278-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="30278-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span><span class="sxs-lookup"><span data-stu-id="30278-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="30278-108">This article explains how to execute such queries in the most efficient way.</span><span class="sxs-lookup"><span data-stu-id="30278-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="30278-109">The Batch service provides special API support for the common scenarios of counting tasks in a job, and counting compute nodes in Batch pool.</span><span class="sxs-lookup"><span data-stu-id="30278-109">The Batch service provides special API support for the common scenarios of counting tasks in a job, and counting compute nodes in Batch pool.</span></span> <span data-ttu-id="30278-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] and [List Pool Node Counts][rest_get_node_counts] operations.</span><span class="sxs-lookup"><span data-stu-id="30278-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] and [List Pool Node Counts][rest_get_node_counts] operations.</span></span> <span data-ttu-id="30278-111">These operations are more efficient than a list query, but return more limited information.</span><span class="sxs-lookup"><span data-stu-id="30278-111">These operations are more efficient than a list query, but return more limited information.</span></span> <span data-ttu-id="30278-112">See [Count tasks and compute nodes by state](batch-get-resource-counts.md).</span><span class="sxs-lookup"><span data-stu-id="30278-112">See [Count tasks and compute nodes by state](batch-get-resource-counts.md).</span></span> 


## <a name="meet-the-detaillevel"></a><span data-ttu-id="30278-113">Meet the DetailLevel</span><span class="sxs-lookup"><span data-stu-id="30278-113">Meet the DetailLevel</span></span>
<span data-ttu-id="30278-114">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span><span class="sxs-lookup"><span data-stu-id="30278-114">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="30278-115">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span><span class="sxs-lookup"><span data-stu-id="30278-115">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="30278-116">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span><span class="sxs-lookup"><span data-stu-id="30278-116">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="30278-117">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span><span class="sxs-lookup"><span data-stu-id="30278-117">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="30278-118">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span><span class="sxs-lookup"><span data-stu-id="30278-118">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="30278-119">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span><span class="sxs-lookup"><span data-stu-id="30278-119">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="30278-120">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span><span class="sxs-lookup"><span data-stu-id="30278-120">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="30278-121">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span><span class="sxs-lookup"><span data-stu-id="30278-121">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="30278-122">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="30278-122">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30278-123">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span><span class="sxs-lookup"><span data-stu-id="30278-123">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="30278-124">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span><span class="sxs-lookup"><span data-stu-id="30278-124">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="30278-125">Filter, select, and expand</span><span class="sxs-lookup"><span data-stu-id="30278-125">Filter, select, and expand</span></span>
<span data-ttu-id="30278-126">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span><span class="sxs-lookup"><span data-stu-id="30278-126">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="30278-127">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span><span class="sxs-lookup"><span data-stu-id="30278-127">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="30278-128">Filter</span><span class="sxs-lookup"><span data-stu-id="30278-128">Filter</span></span>
<span data-ttu-id="30278-129">The filter string is an expression that reduces the number of items that are returned.</span><span class="sxs-lookup"><span data-stu-id="30278-129">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="30278-130">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span><span class="sxs-lookup"><span data-stu-id="30278-130">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="30278-131">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span><span class="sxs-lookup"><span data-stu-id="30278-131">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="30278-132">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span><span class="sxs-lookup"><span data-stu-id="30278-132">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="30278-133">Multiple expressions can be combined by using the logical operators `and` and `or`.</span><span class="sxs-lookup"><span data-stu-id="30278-133">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="30278-134">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="30278-134">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="30278-135">Select</span><span class="sxs-lookup"><span data-stu-id="30278-135">Select</span></span>
<span data-ttu-id="30278-136">The select string limits the property values that are returned for each item.</span><span class="sxs-lookup"><span data-stu-id="30278-136">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="30278-137">You specify a list of property names, and only those property values are returned for the items in the query results.</span><span class="sxs-lookup"><span data-stu-id="30278-137">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="30278-138">The select string consists of a comma-separated list of property names.</span><span class="sxs-lookup"><span data-stu-id="30278-138">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="30278-139">You can specify any of the properties for the entity type you are querying.</span><span class="sxs-lookup"><span data-stu-id="30278-139">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="30278-140">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="30278-140">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="30278-141">Expand</span><span class="sxs-lookup"><span data-stu-id="30278-141">Expand</span></span>
<span data-ttu-id="30278-142">The expand string reduces the number of API calls that are required to obtain certain information.</span><span class="sxs-lookup"><span data-stu-id="30278-142">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="30278-143">When you use an expand string, more information about each item can be obtained with a single API call.</span><span class="sxs-lookup"><span data-stu-id="30278-143">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="30278-144">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span><span class="sxs-lookup"><span data-stu-id="30278-144">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="30278-145">Less API calls means better performance.</span><span class="sxs-lookup"><span data-stu-id="30278-145">Less API calls means better performance.</span></span>

* <span data-ttu-id="30278-146">Similar to the select string, the expand string controls whether certain data is included in list query results.</span><span class="sxs-lookup"><span data-stu-id="30278-146">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="30278-147">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span><span class="sxs-lookup"><span data-stu-id="30278-147">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="30278-148">Currently, it only supports statistics information.</span><span class="sxs-lookup"><span data-stu-id="30278-148">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="30278-149">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span><span class="sxs-lookup"><span data-stu-id="30278-149">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="30278-150">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span><span class="sxs-lookup"><span data-stu-id="30278-150">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="30278-151">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span><span class="sxs-lookup"><span data-stu-id="30278-151">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="30278-152">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span><span class="sxs-lookup"><span data-stu-id="30278-152">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="30278-153">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="30278-153">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="30278-154">See the tables below for property mappings between the .NET and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="30278-154">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="30278-155">Rules for filter, select, and expand strings</span><span class="sxs-lookup"><span data-stu-id="30278-155">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="30278-156">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span><span class="sxs-lookup"><span data-stu-id="30278-156">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="30278-157">All property names are case-sensitive, but property values are case insensitive.</span><span class="sxs-lookup"><span data-stu-id="30278-157">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="30278-158">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="30278-158">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="30278-159">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="30278-159">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="30278-160">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="30278-160">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="30278-161">Boolean strings are either `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="30278-161">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="30278-162">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span><span class="sxs-lookup"><span data-stu-id="30278-162">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="30278-163">Efficient querying in Batch .NET</span><span class="sxs-lookup"><span data-stu-id="30278-163">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="30278-164">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span><span class="sxs-lookup"><span data-stu-id="30278-164">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="30278-165">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span><span class="sxs-lookup"><span data-stu-id="30278-165">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="30278-166">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="30278-166">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="30278-167">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span><span class="sxs-lookup"><span data-stu-id="30278-167">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="30278-168">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span><span class="sxs-lookup"><span data-stu-id="30278-168">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="30278-169">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span><span class="sxs-lookup"><span data-stu-id="30278-169">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="30278-170">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span><span class="sxs-lookup"><span data-stu-id="30278-170">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="30278-171">In this scenario, the Batch user has both test and production pools.</span><span class="sxs-lookup"><span data-stu-id="30278-171">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="30278-172">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span><span class="sxs-lookup"><span data-stu-id="30278-172">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="30278-173">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span><span class="sxs-lookup"><span data-stu-id="30278-173">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="30278-174">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span><span class="sxs-lookup"><span data-stu-id="30278-174">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="30278-175">Batch REST to .NET API mappings</span><span class="sxs-lookup"><span data-stu-id="30278-175">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="30278-176">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span><span class="sxs-lookup"><span data-stu-id="30278-176">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="30278-177">The tables below provide mappings between the .NET and REST API counterparts.</span><span class="sxs-lookup"><span data-stu-id="30278-177">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="30278-178">Mappings for filter strings</span><span class="sxs-lookup"><span data-stu-id="30278-178">Mappings for filter strings</span></span>
* <span data-ttu-id="30278-179">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span><span class="sxs-lookup"><span data-stu-id="30278-179">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="30278-180">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span><span class="sxs-lookup"><span data-stu-id="30278-180">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="30278-181">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span><span class="sxs-lookup"><span data-stu-id="30278-181">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="30278-182">.NET list methods</span><span class="sxs-lookup"><span data-stu-id="30278-182">.NET list methods</span></span> | <span data-ttu-id="30278-183">REST list requests</span><span class="sxs-lookup"><span data-stu-id="30278-183">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="30278-184">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="30278-184">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="30278-185">[List the certificates in an account][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="30278-185">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="30278-186">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="30278-186">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="30278-187">[List the files associated with a task][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="30278-187">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="30278-188">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="30278-188">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="30278-189">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="30278-189">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="30278-190">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="30278-190">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="30278-191">[List the jobs in an account][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="30278-191">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="30278-192">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="30278-192">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="30278-193">[List the files on a node][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="30278-193">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="30278-194">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="30278-194">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="30278-195">[List the tasks associated with a job][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="30278-195">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="30278-196">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="30278-196">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="30278-197">[List the job schedules in an account][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="30278-197">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="30278-198">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="30278-198">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="30278-199">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="30278-199">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="30278-200">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="30278-200">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="30278-201">[List the compute nodes in a pool][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="30278-201">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="30278-202">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="30278-202">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="30278-203">[List the pools in an account][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="30278-203">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="30278-204">Mappings for select strings</span><span class="sxs-lookup"><span data-stu-id="30278-204">Mappings for select strings</span></span>
* <span data-ttu-id="30278-205">**Batch .NET types**: Batch .NET API types.</span><span class="sxs-lookup"><span data-stu-id="30278-205">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="30278-206">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span><span class="sxs-lookup"><span data-stu-id="30278-206">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="30278-207">These property names are used when you construct *select* strings.</span><span class="sxs-lookup"><span data-stu-id="30278-207">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="30278-208">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span><span class="sxs-lookup"><span data-stu-id="30278-208">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="30278-209">Batch .NET types</span><span class="sxs-lookup"><span data-stu-id="30278-209">Batch .NET types</span></span> | <span data-ttu-id="30278-210">REST API entities</span><span class="sxs-lookup"><span data-stu-id="30278-210">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="30278-211">[Certificate][net_cert]</span><span class="sxs-lookup"><span data-stu-id="30278-211">[Certificate][net_cert]</span></span> |<span data-ttu-id="30278-212">[Get information about a certificate][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="30278-212">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="30278-213">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="30278-213">[CloudJob][net_job]</span></span> |<span data-ttu-id="30278-214">[Get information about a job][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="30278-214">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="30278-215">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="30278-215">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="30278-216">[Get information about a job schedule][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="30278-216">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="30278-217">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="30278-217">[ComputeNode][net_node]</span></span> |<span data-ttu-id="30278-218">[Get information about a node][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="30278-218">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="30278-219">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="30278-219">[CloudPool][net_pool]</span></span> |<span data-ttu-id="30278-220">[Get information about a pool][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="30278-220">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="30278-221">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="30278-221">[CloudTask][net_task]</span></span> |<span data-ttu-id="30278-222">[Get information about a task][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="30278-222">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="30278-223">Example: construct a filter string</span><span class="sxs-lookup"><span data-stu-id="30278-223">Example: construct a filter string</span></span>
<span data-ttu-id="30278-224">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span><span class="sxs-lookup"><span data-stu-id="30278-224">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="30278-225">You will find the filterable properties and their supported operators in the first multirow table on that page.</span><span class="sxs-lookup"><span data-stu-id="30278-225">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="30278-226">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span><span class="sxs-lookup"><span data-stu-id="30278-226">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="30278-227">Property</span><span class="sxs-lookup"><span data-stu-id="30278-227">Property</span></span> | <span data-ttu-id="30278-228">Operations allowed</span><span class="sxs-lookup"><span data-stu-id="30278-228">Operations allowed</span></span> | <span data-ttu-id="30278-229">Type</span><span class="sxs-lookup"><span data-stu-id="30278-229">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="30278-230">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span><span class="sxs-lookup"><span data-stu-id="30278-230">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="30278-231">Example: construct a select string</span><span class="sxs-lookup"><span data-stu-id="30278-231">Example: construct a select string</span></span>
<span data-ttu-id="30278-232">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span><span class="sxs-lookup"><span data-stu-id="30278-232">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="30278-233">You will find the selectable properties and their supported operators in the first multirow table on that page.</span><span class="sxs-lookup"><span data-stu-id="30278-233">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="30278-234">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="30278-234">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="30278-235">Property</span><span class="sxs-lookup"><span data-stu-id="30278-235">Property</span></span> | <span data-ttu-id="30278-236">Type</span><span class="sxs-lookup"><span data-stu-id="30278-236">Type</span></span> | <span data-ttu-id="30278-237">Notes</span><span class="sxs-lookup"><span data-stu-id="30278-237">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="30278-238">The select string for including only the ID and command line with each listed task would then be:</span><span class="sxs-lookup"><span data-stu-id="30278-238">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="30278-239">Code samples</span><span class="sxs-lookup"><span data-stu-id="30278-239">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="30278-240">Efficient list queries code sample</span><span class="sxs-lookup"><span data-stu-id="30278-240">Efficient list queries code sample</span></span>
<span data-ttu-id="30278-241">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span><span class="sxs-lookup"><span data-stu-id="30278-241">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="30278-242">This C# console application creates and adds a large number of tasks to a job.</span><span class="sxs-lookup"><span data-stu-id="30278-242">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="30278-243">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span><span class="sxs-lookup"><span data-stu-id="30278-243">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="30278-244">It produces output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="30278-244">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="30278-245">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span><span class="sxs-lookup"><span data-stu-id="30278-245">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="30278-246">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="30278-246">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="30278-247">BatchMetrics library and code sample</span><span class="sxs-lookup"><span data-stu-id="30278-247">BatchMetrics library and code sample</span></span>
<span data-ttu-id="30278-248">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="30278-248">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="30278-249">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span><span class="sxs-lookup"><span data-stu-id="30278-249">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="30278-250">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span><span class="sxs-lookup"><span data-stu-id="30278-250">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="30278-251">The sample application within the project demonstrates the following operations:</span><span class="sxs-lookup"><span data-stu-id="30278-251">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="30278-252">Selecting specific attributes in order to download only the properties you need</span><span class="sxs-lookup"><span data-stu-id="30278-252">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="30278-253">Filtering on state transition times in order to download only changes since the last query</span><span class="sxs-lookup"><span data-stu-id="30278-253">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="30278-254">For example, the following method appears in the BatchMetrics library.</span><span class="sxs-lookup"><span data-stu-id="30278-254">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="30278-255">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span><span class="sxs-lookup"><span data-stu-id="30278-255">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="30278-256">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span><span class="sxs-lookup"><span data-stu-id="30278-256">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="30278-257">Next steps</span><span class="sxs-lookup"><span data-stu-id="30278-257">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="30278-258">Parallel node tasks</span><span class="sxs-lookup"><span data-stu-id="30278-258">Parallel node tasks</span></span>
<span data-ttu-id="30278-259">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span><span class="sxs-lookup"><span data-stu-id="30278-259">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="30278-260">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span><span class="sxs-lookup"><span data-stu-id="30278-260">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="30278-261">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span><span class="sxs-lookup"><span data-stu-id="30278-261">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>


[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: /rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_node_counts]: /rest/api/batchservice/account/listpoolnodecounts