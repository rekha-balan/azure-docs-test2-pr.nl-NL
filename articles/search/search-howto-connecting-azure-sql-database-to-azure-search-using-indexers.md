---
title: Connecting Azure SQL Database to Azure Search Using Indexers | Microsoft Docs
description: Learn how to pull data from Azure SQL Database to an Azure Search index using indexers.
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/15/2017
ms.author: eugenesh
ms.openlocfilehash: 51c9d9afb6c2ed460abd4c47a6afbc404b97a85e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550130"
---
# <a name="connecting-azure-sql-database-to-azure-search-using-indexers"></a><span data-ttu-id="920db-103">Connecting Azure SQL Database to Azure Search using indexers</span><span class="sxs-lookup"><span data-stu-id="920db-103">Connecting Azure SQL Database to Azure Search using indexers</span></span>
<span data-ttu-id="920db-104">Azure Search service is a hosted cloud search service that makes it easy to provide a great search experience.</span><span class="sxs-lookup"><span data-stu-id="920db-104">Azure Search service is a hosted cloud search service that makes it easy to provide a great search experience.</span></span> <span data-ttu-id="920db-105">Before you can search, you need to populate an Azure Search index with your data.</span><span class="sxs-lookup"><span data-stu-id="920db-105">Before you can search, you need to populate an Azure Search index with your data.</span></span> <span data-ttu-id="920db-106">If the data lives in an Azure SQL database, the new **Azure Search indexer for Azure SQL Database** (or **Azure SQL indexer** for short) can automate the indexing process.</span><span class="sxs-lookup"><span data-stu-id="920db-106">If the data lives in an Azure SQL database, the new **Azure Search indexer for Azure SQL Database** (or **Azure SQL indexer** for short) can automate the indexing process.</span></span> <span data-ttu-id="920db-107">This means you have less code to write and less infrastructure to care about.</span><span class="sxs-lookup"><span data-stu-id="920db-107">This means you have less code to write and less infrastructure to care about.</span></span>

<span data-ttu-id="920db-108">This article covers the mechanics of using indexers, but it also describes the features that are only available with Azure SQL databases (for example, integrated change tracking).</span><span class="sxs-lookup"><span data-stu-id="920db-108">This article covers the mechanics of using indexers, but it also describes the features that are only available with Azure SQL databases (for example, integrated change tracking).</span></span> <span data-ttu-id="920db-109">Azure Search also supports other data sources, such as Azure DocumentDB, blob storage, and table storage.</span><span class="sxs-lookup"><span data-stu-id="920db-109">Azure Search also supports other data sources, such as Azure DocumentDB, blob storage, and table storage.</span></span> <span data-ttu-id="920db-110">If you would like to see support for additional data sources, provide your feedback on the [Azure Search feedback forum](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="920db-110">If you would like to see support for additional data sources, provide your feedback on the [Azure Search feedback forum](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

## <a name="indexers-and-data-sources"></a><span data-ttu-id="920db-111">Indexers and data sources</span><span class="sxs-lookup"><span data-stu-id="920db-111">Indexers and data sources</span></span>
<span data-ttu-id="920db-112">You can set up and configure an Azure SQL indexer using:</span><span class="sxs-lookup"><span data-stu-id="920db-112">You can set up and configure an Azure SQL indexer using:</span></span>

* <span data-ttu-id="920db-113">Import Data wizard in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="920db-113">Import Data wizard in the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="920db-114">Azure Search [.NET SDK](https://msdn.microsoft.com/library/azure/dn951165.aspx)</span><span class="sxs-lookup"><span data-stu-id="920db-114">Azure Search [.NET SDK](https://msdn.microsoft.com/library/azure/dn951165.aspx)</span></span>
* <span data-ttu-id="920db-115">Azure Search [REST API](http://go.microsoft.com/fwlink/p/?LinkID=528173)</span><span class="sxs-lookup"><span data-stu-id="920db-115">Azure Search [REST API](http://go.microsoft.com/fwlink/p/?LinkID=528173)</span></span>

<span data-ttu-id="920db-116">In this article, we'll use the REST API to show you how to create and manage **indexers** and **data sources**.</span><span class="sxs-lookup"><span data-stu-id="920db-116">In this article, we'll use the REST API to show you how to create and manage **indexers** and **data sources**.</span></span>

<span data-ttu-id="920db-117">A **data source** specifies which data to index, credentials needed to access the data, and policies that efficiently identify changes in the data (new, modified, or deleted rows).</span><span class="sxs-lookup"><span data-stu-id="920db-117">A **data source** specifies which data to index, credentials needed to access the data, and policies that efficiently identify changes in the data (new, modified, or deleted rows).</span></span> <span data-ttu-id="920db-118">It's defined as an independent resource so that it can be used by multiple indexers.</span><span class="sxs-lookup"><span data-stu-id="920db-118">It's defined as an independent resource so that it can be used by multiple indexers.</span></span>

<span data-ttu-id="920db-119">An **indexer** is a resource that connects data sources with target search indexes.</span><span class="sxs-lookup"><span data-stu-id="920db-119">An **indexer** is a resource that connects data sources with target search indexes.</span></span> <span data-ttu-id="920db-120">An indexer is used in the following ways:</span><span class="sxs-lookup"><span data-stu-id="920db-120">An indexer is used in the following ways:</span></span>

* <span data-ttu-id="920db-121">Perform a one-time copy of the data to populate an index.</span><span class="sxs-lookup"><span data-stu-id="920db-121">Perform a one-time copy of the data to populate an index.</span></span>
* <span data-ttu-id="920db-122">Update an index with changes in the data source on a schedule.</span><span class="sxs-lookup"><span data-stu-id="920db-122">Update an index with changes in the data source on a schedule.</span></span>
* <span data-ttu-id="920db-123">Run on-demand to update an index as needed.</span><span class="sxs-lookup"><span data-stu-id="920db-123">Run on-demand to update an index as needed.</span></span>

## <a name="when-to-use-azure-sql-indexer"></a><span data-ttu-id="920db-124">When to Use Azure SQL Indexer</span><span class="sxs-lookup"><span data-stu-id="920db-124">When to Use Azure SQL Indexer</span></span>
<span data-ttu-id="920db-125">Depending on several factors relating to your data, the use of Azure SQL indexer may or may not be appropriate.</span><span class="sxs-lookup"><span data-stu-id="920db-125">Depending on several factors relating to your data, the use of Azure SQL indexer may or may not be appropriate.</span></span> <span data-ttu-id="920db-126">If your data fits the following requirements, you can use Azure SQL indexer:</span><span class="sxs-lookup"><span data-stu-id="920db-126">If your data fits the following requirements, you can use Azure SQL indexer:</span></span>

* <span data-ttu-id="920db-127">All the data comes from a single table or view</span><span class="sxs-lookup"><span data-stu-id="920db-127">All the data comes from a single table or view</span></span>
  * <span data-ttu-id="920db-128">If the data is scattered across multiple tables, you can create a view and use that view with the indexer.</span><span class="sxs-lookup"><span data-stu-id="920db-128">If the data is scattered across multiple tables, you can create a view and use that view with the indexer.</span></span> <span data-ttu-id="920db-129">However, if you use a view, you won’t be able to use SQL Server integrated change detection.</span><span class="sxs-lookup"><span data-stu-id="920db-129">However, if you use a view, you won’t be able to use SQL Server integrated change detection.</span></span> <span data-ttu-id="920db-130">For more information, see [this section](#CaptureChangedRows).</span><span class="sxs-lookup"><span data-stu-id="920db-130">For more information, see [this section](#CaptureChangedRows).</span></span>
* <span data-ttu-id="920db-131">The data types used in the data source are supported by the indexer.</span><span class="sxs-lookup"><span data-stu-id="920db-131">The data types used in the data source are supported by the indexer.</span></span> <span data-ttu-id="920db-132">Most but not all the SQL types are supported.</span><span class="sxs-lookup"><span data-stu-id="920db-132">Most but not all the SQL types are supported.</span></span> <span data-ttu-id="920db-133">For details, see [Mapping data types in Azure Search](http://go.microsoft.com/fwlink/p/?LinkID=528105).</span><span class="sxs-lookup"><span data-stu-id="920db-133">For details, see [Mapping data types in Azure Search](http://go.microsoft.com/fwlink/p/?LinkID=528105).</span></span>
* <span data-ttu-id="920db-134">You don’t need near real-time updates to the index when a row changes.</span><span class="sxs-lookup"><span data-stu-id="920db-134">You don’t need near real-time updates to the index when a row changes.</span></span>
  * <span data-ttu-id="920db-135">The indexer can re-index your table at most every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="920db-135">The indexer can re-index your table at most every 5 minutes.</span></span> <span data-ttu-id="920db-136">If your data changes frequently and the changes need to be reflected in the index within seconds or single minutes, we recommend using [Azure Search Index API](https://msdn.microsoft.com/library/azure/dn798930.aspx) directly.</span><span class="sxs-lookup"><span data-stu-id="920db-136">If your data changes frequently and the changes need to be reflected in the index within seconds or single minutes, we recommend using [Azure Search Index API](https://msdn.microsoft.com/library/azure/dn798930.aspx) directly.</span></span>
* <span data-ttu-id="920db-137">If you have a large data set and plan to run the indexer on a schedule, your schema allows us to efficiently identify changed (and deleted, if applicable) rows.</span><span class="sxs-lookup"><span data-stu-id="920db-137">If you have a large data set and plan to run the indexer on a schedule, your schema allows us to efficiently identify changed (and deleted, if applicable) rows.</span></span> <span data-ttu-id="920db-138">For more details, see "Capturing Changed and Deleted Rows" below.</span><span class="sxs-lookup"><span data-stu-id="920db-138">For more details, see "Capturing Changed and Deleted Rows" below.</span></span>
* <span data-ttu-id="920db-139">The size of the indexed fields in a row doesn’t exceed the maximum size of an Azure Search indexing request, which is 16 MB.</span><span class="sxs-lookup"><span data-stu-id="920db-139">The size of the indexed fields in a row doesn’t exceed the maximum size of an Azure Search indexing request, which is 16 MB.</span></span>

## <a name="create-and-use-an-azure-sql-indexer"></a><span data-ttu-id="920db-140">Create and Use an Azure SQL Indexer</span><span class="sxs-lookup"><span data-stu-id="920db-140">Create and Use an Azure SQL Indexer</span></span>
<span data-ttu-id="920db-141">First, create the data source:</span><span class="sxs-lookup"><span data-stu-id="920db-141">First, create the data source:</span></span>

    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of the table or view that you want to index" }
    }


<span data-ttu-id="920db-142">You can get the connection string from the [Azure Classic Portal](https://portal.azure.com); use the `ADO.NET connection string` option.</span><span class="sxs-lookup"><span data-stu-id="920db-142">You can get the connection string from the [Azure Classic Portal](https://portal.azure.com); use the `ADO.NET connection string` option.</span></span>

<span data-ttu-id="920db-143">Then, create the target Azure Search index if you don’t have one already.</span><span class="sxs-lookup"><span data-stu-id="920db-143">Then, create the target Azure Search index if you don’t have one already.</span></span> <span data-ttu-id="920db-144">You can create an index using the [portal UI](https://portal.azure.com) or the [Create Index API](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span><span class="sxs-lookup"><span data-stu-id="920db-144">You can create an index using the [portal UI](https://portal.azure.com) or the [Create Index API](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span></span> <span data-ttu-id="920db-145">Ensure that the schema of your target index is compatible with the schema of the source table - see [mapping between SQL and Azure search data types](#TypeMapping).</span><span class="sxs-lookup"><span data-stu-id="920db-145">Ensure that the schema of your target index is compatible with the schema of the source table - see [mapping between SQL and Azure search data types](#TypeMapping).</span></span>

<span data-ttu-id="920db-146">Finally, create the indexer by giving it a name and referencing the data source and target index:</span><span class="sxs-lookup"><span data-stu-id="920db-146">Finally, create the indexer by giving it a name and referencing the data source and target index:</span></span>

    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }

<span data-ttu-id="920db-147">An indexer created in this way doesn’t have a schedule.</span><span class="sxs-lookup"><span data-stu-id="920db-147">An indexer created in this way doesn’t have a schedule.</span></span> <span data-ttu-id="920db-148">It automatically runs once when it’s created.</span><span class="sxs-lookup"><span data-stu-id="920db-148">It automatically runs once when it’s created.</span></span> <span data-ttu-id="920db-149">You can run it again at any time using a **run indexer** request:</span><span class="sxs-lookup"><span data-stu-id="920db-149">You can run it again at any time using a **run indexer** request:</span></span>

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

<span data-ttu-id="920db-150">You can customize several aspects of indexer behavior, such as batch size and how many documents can be skipped before an indexer execution fails.</span><span class="sxs-lookup"><span data-stu-id="920db-150">You can customize several aspects of indexer behavior, such as batch size and how many documents can be skipped before an indexer execution fails.</span></span> <span data-ttu-id="920db-151">For more information, see [Create Indexer API](https://msdn.microsoft.com/library/azure/dn946899.aspx).</span><span class="sxs-lookup"><span data-stu-id="920db-151">For more information, see [Create Indexer API](https://msdn.microsoft.com/library/azure/dn946899.aspx).</span></span>

<span data-ttu-id="920db-152">You may need to allow Azure services to connect to your database.</span><span class="sxs-lookup"><span data-stu-id="920db-152">You may need to allow Azure services to connect to your database.</span></span> <span data-ttu-id="920db-153">See [Connecting From Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) for instructions on how to do that.</span><span class="sxs-lookup"><span data-stu-id="920db-153">See [Connecting From Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) for instructions on how to do that.</span></span>

<span data-ttu-id="920db-154">To monitor the indexer status and execution history (number of items indexed, failures, etc.), use an **indexer status** request:</span><span class="sxs-lookup"><span data-stu-id="920db-154">To monitor the indexer status and execution history (number of items indexed, failures, etc.), use an **indexer status** request:</span></span>

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

<span data-ttu-id="920db-155">The response should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="920db-155">The response should look similar to the following:</span></span>

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

<span data-ttu-id="920db-156">Execution history contains up to 50 of the most recently completed executions, which are sorted in the reverse chronological order (so that the latest execution comes first in the response).</span><span class="sxs-lookup"><span data-stu-id="920db-156">Execution history contains up to 50 of the most recently completed executions, which are sorted in the reverse chronological order (so that the latest execution comes first in the response).</span></span>
<span data-ttu-id="920db-157">Additional information about the response can be found in [Get Indexer Status](http://go.microsoft.com/fwlink/p/?LinkId=528198)</span><span class="sxs-lookup"><span data-stu-id="920db-157">Additional information about the response can be found in [Get Indexer Status](http://go.microsoft.com/fwlink/p/?LinkId=528198)</span></span>

## <a name="run-indexers-on-a-schedule"></a><span data-ttu-id="920db-158">Run indexers on a schedule</span><span class="sxs-lookup"><span data-stu-id="920db-158">Run indexers on a schedule</span></span>
<span data-ttu-id="920db-159">You can also arrange the indexer to run periodically on a schedule.</span><span class="sxs-lookup"><span data-stu-id="920db-159">You can also arrange the indexer to run periodically on a schedule.</span></span> <span data-ttu-id="920db-160">To do this, add the **schedule** property when creating or updating the indexer.</span><span class="sxs-lookup"><span data-stu-id="920db-160">To do this, add the **schedule** property when creating or updating the indexer.</span></span> <span data-ttu-id="920db-161">The example below shows a PUT request to update the indexer:</span><span class="sxs-lookup"><span data-stu-id="920db-161">The example below shows a PUT request to update the indexer:</span></span>

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

<span data-ttu-id="920db-162">The **interval** parameter is required.</span><span class="sxs-lookup"><span data-stu-id="920db-162">The **interval** parameter is required.</span></span> <span data-ttu-id="920db-163">The interval refers to the time between the start of two consecutive indexer executions.</span><span class="sxs-lookup"><span data-stu-id="920db-163">The interval refers to the time between the start of two consecutive indexer executions.</span></span> <span data-ttu-id="920db-164">The smallest allowed interval is 5 minutes; the longest is one day.</span><span class="sxs-lookup"><span data-stu-id="920db-164">The smallest allowed interval is 5 minutes; the longest is one day.</span></span> <span data-ttu-id="920db-165">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span><span class="sxs-lookup"><span data-stu-id="920db-165">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span></span> <span data-ttu-id="920db-166">The pattern for this is: `P(nD)(T(nH)(nM))`.</span><span class="sxs-lookup"><span data-stu-id="920db-166">The pattern for this is: `P(nD)(T(nH)(nM))`.</span></span> <span data-ttu-id="920db-167">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span><span class="sxs-lookup"><span data-stu-id="920db-167">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span></span>

<span data-ttu-id="920db-168">The optional **startTime** indicates when the scheduled executions should commence.</span><span class="sxs-lookup"><span data-stu-id="920db-168">The optional **startTime** indicates when the scheduled executions should commence.</span></span> <span data-ttu-id="920db-169">If it is omitted, the current UTC time is used.</span><span class="sxs-lookup"><span data-stu-id="920db-169">If it is omitted, the current UTC time is used.</span></span> <span data-ttu-id="920db-170">This time can be in the past – in which case the first execution is scheduled as if the indexer has been running continuously since the startTime.</span><span class="sxs-lookup"><span data-stu-id="920db-170">This time can be in the past – in which case the first execution is scheduled as if the indexer has been running continuously since the startTime.</span></span>  

<span data-ttu-id="920db-171">Only one execution of an indexer can run at a time.</span><span class="sxs-lookup"><span data-stu-id="920db-171">Only one execution of an indexer can run at a time.</span></span> <span data-ttu-id="920db-172">If an indexer is running when its execution is scheduled, the execution is postponed until the next scheduled time.</span><span class="sxs-lookup"><span data-stu-id="920db-172">If an indexer is running when its execution is scheduled, the execution is postponed until the next scheduled time.</span></span>

<span data-ttu-id="920db-173">Let’s consider an example to make this more concrete.</span><span class="sxs-lookup"><span data-stu-id="920db-173">Let’s consider an example to make this more concrete.</span></span> <span data-ttu-id="920db-174">Suppose we the following hourly schedule configured:</span><span class="sxs-lookup"><span data-stu-id="920db-174">Suppose we the following hourly schedule configured:</span></span>

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

<span data-ttu-id="920db-175">Here’s what happens:</span><span class="sxs-lookup"><span data-stu-id="920db-175">Here’s what happens:</span></span>

1. <span data-ttu-id="920db-176">The first indexer execution starts at or around March 1, 2015 12:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="920db-176">The first indexer execution starts at or around March 1, 2015 12:00 a.m.</span></span> <span data-ttu-id="920db-177">UTC.</span><span class="sxs-lookup"><span data-stu-id="920db-177">UTC.</span></span>
2. <span data-ttu-id="920db-178">Assume this execution takes 20 minutes (or any time less than 1 hour).</span><span class="sxs-lookup"><span data-stu-id="920db-178">Assume this execution takes 20 minutes (or any time less than 1 hour).</span></span>
3. <span data-ttu-id="920db-179">The second execution starts at or around March 1, 2015 1:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="920db-179">The second execution starts at or around March 1, 2015 1:00 a.m.</span></span>
4. <span data-ttu-id="920db-180">Now suppose that this execution takes more than an hour – for example, 70 minutes – so that it completes around 2:10 a.m.</span><span class="sxs-lookup"><span data-stu-id="920db-180">Now suppose that this execution takes more than an hour – for example, 70 minutes – so that it completes around 2:10 a.m.</span></span>
5. <span data-ttu-id="920db-181">It’s now 2:00 a.m., time for the third execution to start.</span><span class="sxs-lookup"><span data-stu-id="920db-181">It’s now 2:00 a.m., time for the third execution to start.</span></span> <span data-ttu-id="920db-182">However, because the second execution from 1 a.m.</span><span class="sxs-lookup"><span data-stu-id="920db-182">However, because the second execution from 1 a.m.</span></span> <span data-ttu-id="920db-183">is still running, the third execution is skipped.</span><span class="sxs-lookup"><span data-stu-id="920db-183">is still running, the third execution is skipped.</span></span> <span data-ttu-id="920db-184">The third execution starts at 3 a.m.</span><span class="sxs-lookup"><span data-stu-id="920db-184">The third execution starts at 3 a.m.</span></span>

<span data-ttu-id="920db-185">You can add, change, or delete a schedule for an existing indexer by using a **PUT indexer** request.</span><span class="sxs-lookup"><span data-stu-id="920db-185">You can add, change, or delete a schedule for an existing indexer by using a **PUT indexer** request.</span></span>

<a name="CaptureChangedRows"></a>

## <a name="capturing-new-changed-and-deleted-rows"></a><span data-ttu-id="920db-186">Capturing new, changed, and deleted rows</span><span class="sxs-lookup"><span data-stu-id="920db-186">Capturing new, changed, and deleted rows</span></span>
<span data-ttu-id="920db-187">If your table has many rows, you should use a data change detection policy.</span><span class="sxs-lookup"><span data-stu-id="920db-187">If your table has many rows, you should use a data change detection policy.</span></span> <span data-ttu-id="920db-188">Change detection enables an efficient retrieval of only the new or changed rows without having to re-index the entire table.</span><span class="sxs-lookup"><span data-stu-id="920db-188">Change detection enables an efficient retrieval of only the new or changed rows without having to re-index the entire table.</span></span>

### <a name="sql-integrated-change-tracking-policy"></a><span data-ttu-id="920db-189">SQL Integrated Change Tracking Policy</span><span class="sxs-lookup"><span data-stu-id="920db-189">SQL Integrated Change Tracking Policy</span></span>
<span data-ttu-id="920db-190">If your SQL database supports [change tracking](https://msdn.microsoft.com/library/bb933875.aspx), we recommend using **SQL Integrated Change Tracking Policy**.</span><span class="sxs-lookup"><span data-stu-id="920db-190">If your SQL database supports [change tracking](https://msdn.microsoft.com/library/bb933875.aspx), we recommend using **SQL Integrated Change Tracking Policy**.</span></span> <span data-ttu-id="920db-191">This is the most efficient policy.</span><span class="sxs-lookup"><span data-stu-id="920db-191">This is the most efficient policy.</span></span> <span data-ttu-id="920db-192">In addition, it allows Azure Search to identify deleted rows without you having to add an explicit "soft delete" column to your table.</span><span class="sxs-lookup"><span data-stu-id="920db-192">In addition, it allows Azure Search to identify deleted rows without you having to add an explicit "soft delete" column to your table.</span></span>

<span data-ttu-id="920db-193">Integrated change tracking is supported starting with the following SQL Server database versions:</span><span class="sxs-lookup"><span data-stu-id="920db-193">Integrated change tracking is supported starting with the following SQL Server database versions:</span></span>

* <span data-ttu-id="920db-194">SQL Server 2008 R2 and later, if you're using SQL Server on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="920db-194">SQL Server 2008 R2 and later, if you're using SQL Server on Azure VMs.</span></span>
* <span data-ttu-id="920db-195">Azure SQL Database V12, if you're using Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="920db-195">Azure SQL Database V12, if you're using Azure SQL Database.</span></span>

<span data-ttu-id="920db-196">When using SQL integrated change tracking policy, do not specify a separate data deletion detection policy - this policy has built-in support for identifying deleted rows.</span><span class="sxs-lookup"><span data-stu-id="920db-196">When using SQL integrated change tracking policy, do not specify a separate data deletion detection policy - this policy has built-in support for identifying deleted rows.</span></span>

<span data-ttu-id="920db-197">This policy can only be used with tables; it cannot be used with views.</span><span class="sxs-lookup"><span data-stu-id="920db-197">This policy can only be used with tables; it cannot be used with views.</span></span> <span data-ttu-id="920db-198">You need to enable change tracking for the table you're using before you can use this policy.</span><span class="sxs-lookup"><span data-stu-id="920db-198">You need to enable change tracking for the table you're using before you can use this policy.</span></span> <span data-ttu-id="920db-199">See [Enable and disable change tracking](https://msdn.microsoft.com/library/bb964713.aspx) for instructions.</span><span class="sxs-lookup"><span data-stu-id="920db-199">See [Enable and disable change tracking](https://msdn.microsoft.com/library/bb964713.aspx) for instructions.</span></span>

<span data-ttu-id="920db-200">To use this policy, create or update your data source like this:</span><span class="sxs-lookup"><span data-stu-id="920db-200">To use this policy, create or update your data source like this:</span></span>

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a><span data-ttu-id="920db-201">High Water Mark Change Detection policy</span><span class="sxs-lookup"><span data-stu-id="920db-201">High Water Mark Change Detection policy</span></span>
<span data-ttu-id="920db-202">While the SQL Integrated Change Tracking policy is recommended, it can only be used with tables, not views.</span><span class="sxs-lookup"><span data-stu-id="920db-202">While the SQL Integrated Change Tracking policy is recommended, it can only be used with tables, not views.</span></span> <span data-ttu-id="920db-203">If you're using a view, consider using the high water mark policy.</span><span class="sxs-lookup"><span data-stu-id="920db-203">If you're using a view, consider using the high water mark policy.</span></span> <span data-ttu-id="920db-204">This policy can be used if your table or view contains a column that meets the following criteria:</span><span class="sxs-lookup"><span data-stu-id="920db-204">This policy can be used if your table or view contains a column that meets the following criteria:</span></span>

* <span data-ttu-id="920db-205">All inserts specify a value for the column.</span><span class="sxs-lookup"><span data-stu-id="920db-205">All inserts specify a value for the column.</span></span>
* <span data-ttu-id="920db-206">All updates to an item also change the value of the column.</span><span class="sxs-lookup"><span data-stu-id="920db-206">All updates to an item also change the value of the column.</span></span>
* <span data-ttu-id="920db-207">The value of this column increases with each insert or update.</span><span class="sxs-lookup"><span data-stu-id="920db-207">The value of this column increases with each insert or update.</span></span>
* <span data-ttu-id="920db-208">Queries with the following WHERE and ORDER BY clauses can be executed efficiently: `WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`.</span><span class="sxs-lookup"><span data-stu-id="920db-208">Queries with the following WHERE and ORDER BY clauses can be executed efficiently: `WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="920db-209">We strongly recommend using a **rowversion** column for change tracking.</span><span class="sxs-lookup"><span data-stu-id="920db-209">We strongly recommend using a **rowversion** column for change tracking.</span></span> <span data-ttu-id="920db-210">If any other data type is used, change tracking is not guaranteed to capture all changes in the presence of transactions executing concurrently with an indexer query.</span><span class="sxs-lookup"><span data-stu-id="920db-210">If any other data type is used, change tracking is not guaranteed to capture all changes in the presence of transactions executing concurrently with an indexer query.</span></span>

<span data-ttu-id="920db-211">To use a high water mark policy, create or update your data source like this:</span><span class="sxs-lookup"><span data-stu-id="920db-211">To use a high water mark policy, create or update your data source like this:</span></span>

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> <span data-ttu-id="920db-212">If the source table does not have an index on the high water mark column, queries used by the SQL indexer may time out. In particular, the `ORDER BY [High Water Mark Column]` clause requires an index to run efficiently when the table contains many rows.</span><span class="sxs-lookup"><span data-stu-id="920db-212">If the source table does not have an index on the high water mark column, queries used by the SQL indexer may time out. In particular, the `ORDER BY [High Water Mark Column]` clause requires an index to run efficiently when the table contains many rows.</span></span>
>
>

<span data-ttu-id="920db-213">If you encounter timeout errors, you can use the `queryTimeout` indexer configuration setting to set the query timeout to a value higher than the default 5-minute timeout.</span><span class="sxs-lookup"><span data-stu-id="920db-213">If you encounter timeout errors, you can use the `queryTimeout` indexer configuration setting to set the query timeout to a value higher than the default 5-minute timeout.</span></span> <span data-ttu-id="920db-214">For example, to set the timeout to 10 minutes, create or update the indexer with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="920db-214">For example, to set the timeout to 10 minutes, create or update the indexer with the following configuration:</span></span>

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

<span data-ttu-id="920db-215">You can also disable the `ORDER BY [High Water Mark Column]` clause.</span><span class="sxs-lookup"><span data-stu-id="920db-215">You can also disable the `ORDER BY [High Water Mark Column]` clause.</span></span> <span data-ttu-id="920db-216">However, this is not recommended because if the indexer execution is interrupted by an error, the indexer has to re-process all rows if it runs later - even if the indexer has already processed almost all the rows by the time it was interrupted.</span><span class="sxs-lookup"><span data-stu-id="920db-216">However, this is not recommended because if the indexer execution is interrupted by an error, the indexer has to re-process all rows if it runs later - even if the indexer has already processed almost all the rows by the time it was interrupted.</span></span> <span data-ttu-id="920db-217">To disable the `ORDER BY` clause, use the `disableOrderByHighWaterMarkColumn` setting in the indexer definition:</span><span class="sxs-lookup"><span data-stu-id="920db-217">To disable the `ORDER BY` clause, use the `disableOrderByHighWaterMarkColumn` setting in the indexer definition:</span></span>  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a><span data-ttu-id="920db-218">Soft Delete Column Deletion Detection policy</span><span class="sxs-lookup"><span data-stu-id="920db-218">Soft Delete Column Deletion Detection policy</span></span>
<span data-ttu-id="920db-219">When rows are deleted from the source table, you probably want to delete those rows from the search index as well.</span><span class="sxs-lookup"><span data-stu-id="920db-219">When rows are deleted from the source table, you probably want to delete those rows from the search index as well.</span></span> <span data-ttu-id="920db-220">If you use the SQL integrated change tracking policy, this is taken care of for you.</span><span class="sxs-lookup"><span data-stu-id="920db-220">If you use the SQL integrated change tracking policy, this is taken care of for you.</span></span> <span data-ttu-id="920db-221">However, the high water mark change tracking policy doesn’t help you with deleted rows.</span><span class="sxs-lookup"><span data-stu-id="920db-221">However, the high water mark change tracking policy doesn’t help you with deleted rows.</span></span> <span data-ttu-id="920db-222">What to do?</span><span class="sxs-lookup"><span data-stu-id="920db-222">What to do?</span></span>

<span data-ttu-id="920db-223">If the rows are physically removed from the table, Azure Search has no way to infer the presence of records that no longer exist.</span><span class="sxs-lookup"><span data-stu-id="920db-223">If the rows are physically removed from the table, Azure Search has no way to infer the presence of records that no longer exist.</span></span>  <span data-ttu-id="920db-224">However, you can use the “soft-delete” technique to logically delete rows without removing them from the table.</span><span class="sxs-lookup"><span data-stu-id="920db-224">However, you can use the “soft-delete” technique to logically delete rows without removing them from the table.</span></span> <span data-ttu-id="920db-225">Add a column to your table or view and mark rows as deleted using that column.</span><span class="sxs-lookup"><span data-stu-id="920db-225">Add a column to your table or view and mark rows as deleted using that column.</span></span>

<span data-ttu-id="920db-226">When using the soft-delete technique, you can specify the soft delete policy as follows when creating or updating the data source:</span><span class="sxs-lookup"><span data-stu-id="920db-226">When using the soft-delete technique, you can specify the soft delete policy as follows when creating or updating the data source:</span></span>

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[the value that indicates that a row is deleted]"
        }
    }

<span data-ttu-id="920db-227">The **softDeleteMarkerValue** must be a string – use the string representation of your actual value.</span><span class="sxs-lookup"><span data-stu-id="920db-227">The **softDeleteMarkerValue** must be a string – use the string representation of your actual value.</span></span> <span data-ttu-id="920db-228">For example, if you have an integer column where deleted rows are marked with the value 1, use `"1"`.</span><span class="sxs-lookup"><span data-stu-id="920db-228">For example, if you have an integer column where deleted rows are marked with the value 1, use `"1"`.</span></span> <span data-ttu-id="920db-229">If you have a BIT column where deleted rows are marked with the Boolean true value, use `"True"`.</span><span class="sxs-lookup"><span data-stu-id="920db-229">If you have a BIT column where deleted rows are marked with the Boolean true value, use `"True"`.</span></span>

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a><span data-ttu-id="920db-230">Mapping between SQL Data Types and Azure Search data types</span><span class="sxs-lookup"><span data-stu-id="920db-230">Mapping between SQL Data Types and Azure Search data types</span></span>
| <span data-ttu-id="920db-231">SQL data type</span><span class="sxs-lookup"><span data-stu-id="920db-231">SQL data type</span></span> | <span data-ttu-id="920db-232">Allowed target index field types</span><span class="sxs-lookup"><span data-stu-id="920db-232">Allowed target index field types</span></span> | <span data-ttu-id="920db-233">Notes</span><span class="sxs-lookup"><span data-stu-id="920db-233">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="920db-234">bit</span><span class="sxs-lookup"><span data-stu-id="920db-234">bit</span></span> |<span data-ttu-id="920db-235">Edm.Boolean, Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-235">Edm.Boolean, Edm.String</span></span> | |
| <span data-ttu-id="920db-236">int, smallint, tinyint</span><span class="sxs-lookup"><span data-stu-id="920db-236">int, smallint, tinyint</span></span> |<span data-ttu-id="920db-237">Edm.Int32, Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-237">Edm.Int32, Edm.Int64, Edm.String</span></span> | |
| <span data-ttu-id="920db-238">bigint</span><span class="sxs-lookup"><span data-stu-id="920db-238">bigint</span></span> |<span data-ttu-id="920db-239">Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-239">Edm.Int64, Edm.String</span></span> | |
| <span data-ttu-id="920db-240">real, float</span><span class="sxs-lookup"><span data-stu-id="920db-240">real, float</span></span> |<span data-ttu-id="920db-241">Edm.Double, Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-241">Edm.Double, Edm.String</span></span> | |
| <span data-ttu-id="920db-242">smallmoney, money decimal numeric</span><span class="sxs-lookup"><span data-stu-id="920db-242">smallmoney, money decimal numeric</span></span> |<span data-ttu-id="920db-243">Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-243">Edm.String</span></span> |<span data-ttu-id="920db-244">Azure Search does not support converting decimal types into Edm.Double because this would lose precision</span><span class="sxs-lookup"><span data-stu-id="920db-244">Azure Search does not support converting decimal types into Edm.Double because this would lose precision</span></span> |
| <span data-ttu-id="920db-245">char, nchar, varchar, nvarchar</span><span class="sxs-lookup"><span data-stu-id="920db-245">char, nchar, varchar, nvarchar</span></span> |<span data-ttu-id="920db-246">Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-246">Edm.String</span></span><br/><span data-ttu-id="920db-247">Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="920db-247">Collection(Edm.String)</span></span> |<span data-ttu-id="920db-248">A SQL string can be used to populate a Collection(Edm.String) field if the string represents a JSON array of strings: `["red", "white", "blue"]`</span><span class="sxs-lookup"><span data-stu-id="920db-248">A SQL string can be used to populate a Collection(Edm.String) field if the string represents a JSON array of strings: `["red", "white", "blue"]`</span></span> |
| <span data-ttu-id="920db-249">smalldatetime, datetime, datetime2, date, datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="920db-249">smalldatetime, datetime, datetime2, date, datetimeoffset</span></span> |<span data-ttu-id="920db-250">Edm.DateTimeOffset, Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-250">Edm.DateTimeOffset, Edm.String</span></span> | |
| <span data-ttu-id="920db-251">uniqueidentifer</span><span class="sxs-lookup"><span data-stu-id="920db-251">uniqueidentifer</span></span> |<span data-ttu-id="920db-252">Edm.String</span><span class="sxs-lookup"><span data-stu-id="920db-252">Edm.String</span></span> | |
| <span data-ttu-id="920db-253">geography</span><span class="sxs-lookup"><span data-stu-id="920db-253">geography</span></span> |<span data-ttu-id="920db-254">Edm.GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="920db-254">Edm.GeographyPoint</span></span> |<span data-ttu-id="920db-255">Only geography instances of type POINT with SRID 4326 (which is the default) are supported</span><span class="sxs-lookup"><span data-stu-id="920db-255">Only geography instances of type POINT with SRID 4326 (which is the default) are supported</span></span> |
| <span data-ttu-id="920db-256">rowversion</span><span class="sxs-lookup"><span data-stu-id="920db-256">rowversion</span></span> |<span data-ttu-id="920db-257">N/A</span><span class="sxs-lookup"><span data-stu-id="920db-257">N/A</span></span> |<span data-ttu-id="920db-258">Row-version columns cannot be stored in the search index, but they can be used for change tracking</span><span class="sxs-lookup"><span data-stu-id="920db-258">Row-version columns cannot be stored in the search index, but they can be used for change tracking</span></span> |
| <span data-ttu-id="920db-259">time, timespan, binary, varbinary, image, xml, geometry, CLR types</span><span class="sxs-lookup"><span data-stu-id="920db-259">time, timespan, binary, varbinary, image, xml, geometry, CLR types</span></span> |<span data-ttu-id="920db-260">N/A</span><span class="sxs-lookup"><span data-stu-id="920db-260">N/A</span></span> |<span data-ttu-id="920db-261">Not supported</span><span class="sxs-lookup"><span data-stu-id="920db-261">Not supported</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="920db-262">Configuration Settings</span><span class="sxs-lookup"><span data-stu-id="920db-262">Configuration Settings</span></span>
<span data-ttu-id="920db-263">SQL indexer exposes several configuration settings:</span><span class="sxs-lookup"><span data-stu-id="920db-263">SQL indexer exposes several configuration settings:</span></span>

| <span data-ttu-id="920db-264">Setting</span><span class="sxs-lookup"><span data-stu-id="920db-264">Setting</span></span> | <span data-ttu-id="920db-265">Data type</span><span class="sxs-lookup"><span data-stu-id="920db-265">Data type</span></span> | <span data-ttu-id="920db-266">Purpose</span><span class="sxs-lookup"><span data-stu-id="920db-266">Purpose</span></span> | <span data-ttu-id="920db-267">Default value</span><span class="sxs-lookup"><span data-stu-id="920db-267">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="920db-268">queryTimeout</span><span class="sxs-lookup"><span data-stu-id="920db-268">queryTimeout</span></span> |<span data-ttu-id="920db-269">string</span><span class="sxs-lookup"><span data-stu-id="920db-269">string</span></span> |<span data-ttu-id="920db-270">Sets the timeout for SQL query execution</span><span class="sxs-lookup"><span data-stu-id="920db-270">Sets the timeout for SQL query execution</span></span> |<span data-ttu-id="920db-271">5 minutes ("00:05:00")</span><span class="sxs-lookup"><span data-stu-id="920db-271">5 minutes ("00:05:00")</span></span> |
| <span data-ttu-id="920db-272">disableOrderByHighWaterMarkColumn</span><span class="sxs-lookup"><span data-stu-id="920db-272">disableOrderByHighWaterMarkColumn</span></span> |<span data-ttu-id="920db-273">bool</span><span class="sxs-lookup"><span data-stu-id="920db-273">bool</span></span> |<span data-ttu-id="920db-274">Causes the SQL query used by the high water mark policy to omit the ORDER BY clause.</span><span class="sxs-lookup"><span data-stu-id="920db-274">Causes the SQL query used by the high water mark policy to omit the ORDER BY clause.</span></span> <span data-ttu-id="920db-275">See [High Water Mark policy](#HighWaterMarkPolicy)</span><span class="sxs-lookup"><span data-stu-id="920db-275">See [High Water Mark policy](#HighWaterMarkPolicy)</span></span> |<span data-ttu-id="920db-276">false</span><span class="sxs-lookup"><span data-stu-id="920db-276">false</span></span> |

<span data-ttu-id="920db-277">These settings are used in the `parameters.configuration` object in the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="920db-277">These settings are used in the `parameters.configuration` object in the indexer definition.</span></span> <span data-ttu-id="920db-278">For example, to set the query timeout to 10 minutes, create or update the indexer with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="920db-278">For example, to set the query timeout to 10 minutes, create or update the indexer with the following configuration:</span></span>

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="frequently-asked-questions"></a><span data-ttu-id="920db-279">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="920db-279">Frequently asked questions</span></span>
<span data-ttu-id="920db-280">**Q:** Can I use Azure SQL indexer with SQL databases running on IaaS VMs in Azure?</span><span class="sxs-lookup"><span data-stu-id="920db-280">**Q:** Can I use Azure SQL indexer with SQL databases running on IaaS VMs in Azure?</span></span>

<span data-ttu-id="920db-281">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="920db-281">A: Yes.</span></span> <span data-ttu-id="920db-282">However, you need to allow your search service to connect to your database.</span><span class="sxs-lookup"><span data-stu-id="920db-282">However, you need to allow your search service to connect to your database.</span></span> <span data-ttu-id="920db-283">For more information, see [Configure a connection from an Azure Search indexer to SQL Server on an Azure VM](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).</span><span class="sxs-lookup"><span data-stu-id="920db-283">For more information, see [Configure a connection from an Azure Search indexer to SQL Server on an Azure VM](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).</span></span>

<span data-ttu-id="920db-284">**Q:** Can I use Azure SQL indexer with SQL databases running on-premises?</span><span class="sxs-lookup"><span data-stu-id="920db-284">**Q:** Can I use Azure SQL indexer with SQL databases running on-premises?</span></span>

<span data-ttu-id="920db-285">A: We do not recommend or support this, as doing this would require you to open your databases to Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="920db-285">A: We do not recommend or support this, as doing this would require you to open your databases to Internet traffic.</span></span>

<span data-ttu-id="920db-286">**Q:** Can I use Azure SQL indexer with databases other than SQL Server running in IaaS on Azure?</span><span class="sxs-lookup"><span data-stu-id="920db-286">**Q:** Can I use Azure SQL indexer with databases other than SQL Server running in IaaS on Azure?</span></span>

<span data-ttu-id="920db-287">A: We don’t support this scenario, because we haven’t tested the indexer with any databases other than SQL Server.</span><span class="sxs-lookup"><span data-stu-id="920db-287">A: We don’t support this scenario, because we haven’t tested the indexer with any databases other than SQL Server.</span></span>  

<span data-ttu-id="920db-288">**Q:** Can I create multiple indexers running on a schedule?</span><span class="sxs-lookup"><span data-stu-id="920db-288">**Q:** Can I create multiple indexers running on a schedule?</span></span>

<span data-ttu-id="920db-289">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="920db-289">A: Yes.</span></span> <span data-ttu-id="920db-290">However, only one indexer can be running on one node at one time.</span><span class="sxs-lookup"><span data-stu-id="920db-290">However, only one indexer can be running on one node at one time.</span></span> <span data-ttu-id="920db-291">If you need multiple indexers running concurrently, consider scaling up your search service to more than one search unit.</span><span class="sxs-lookup"><span data-stu-id="920db-291">If you need multiple indexers running concurrently, consider scaling up your search service to more than one search unit.</span></span>

<span data-ttu-id="920db-292">**Q:** Does running an indexer affect my query workload?</span><span class="sxs-lookup"><span data-stu-id="920db-292">**Q:** Does running an indexer affect my query workload?</span></span>

<span data-ttu-id="920db-293">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="920db-293">A: Yes.</span></span> <span data-ttu-id="920db-294">Indexer runs on one of the nodes in your search service, and that node’s resources are shared between indexing and serving query traffic and other API requests.</span><span class="sxs-lookup"><span data-stu-id="920db-294">Indexer runs on one of the nodes in your search service, and that node’s resources are shared between indexing and serving query traffic and other API requests.</span></span> <span data-ttu-id="920db-295">If you run intensive indexing and query workloads and encounter a high rate of 503 errors or increasing response times, consider scaling up your search service.</span><span class="sxs-lookup"><span data-stu-id="920db-295">If you run intensive indexing and query workloads and encounter a high rate of 503 errors or increasing response times, consider scaling up your search service.</span></span>
