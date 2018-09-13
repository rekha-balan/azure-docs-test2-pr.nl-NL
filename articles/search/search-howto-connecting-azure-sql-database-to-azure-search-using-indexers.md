---
title: Connecting Azure SQL Database to Azure Search Using Indexers | Microsoft Docs
description: Learn how to pull data from Azure SQL Database to an Azure Search index using indexers.
author: chaosrealm
manager: jlembicz
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: eugenesh
ms.openlocfilehash: 5897740a1b5a183738c08b4dfde571be652aff3e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773701"
---
# <a name="connecting-azure-sql-database-to-azure-search-using-indexers"></a><span data-ttu-id="84db8-103">Connecting Azure SQL Database to Azure Search using indexers</span><span class="sxs-lookup"><span data-stu-id="84db8-103">Connecting Azure SQL Database to Azure Search using indexers</span></span>

<span data-ttu-id="84db8-104">Before you can query an [Azure Search index](search-what-is-an-index.md), you must populate it with your data.</span><span class="sxs-lookup"><span data-stu-id="84db8-104">Before you can query an [Azure Search index](search-what-is-an-index.md), you must populate it with your data.</span></span> <span data-ttu-id="84db8-105">If the data lives in an Azure SQL database, an **Azure Search indexer for Azure SQL Database** (or **Azure SQL indexer** for short) can automate the indexing process, which means less code to write and less infrastructure to care about.</span><span class="sxs-lookup"><span data-stu-id="84db8-105">If the data lives in an Azure SQL database, an **Azure Search indexer for Azure SQL Database** (or **Azure SQL indexer** for short) can automate the indexing process, which means less code to write and less infrastructure to care about.</span></span>

<span data-ttu-id="84db8-106">This article covers the mechanics of using [indexers](search-indexer-overview.md), but also describes features only available with Azure SQL databases (for example, integrated change tracking).</span><span class="sxs-lookup"><span data-stu-id="84db8-106">This article covers the mechanics of using [indexers](search-indexer-overview.md), but also describes features only available with Azure SQL databases (for example, integrated change tracking).</span></span> 

<span data-ttu-id="84db8-107">In addition to Azure SQL databases, Azure Search provides indexers for [Azure Cosmos DB](search-howto-index-cosmosdb.md), [Azure Blob storage](search-howto-indexing-azure-blob-storage.md), and [Azure table storage](search-howto-indexing-azure-tables.md).</span><span class="sxs-lookup"><span data-stu-id="84db8-107">In addition to Azure SQL databases, Azure Search provides indexers for [Azure Cosmos DB](search-howto-index-cosmosdb.md), [Azure Blob storage](search-howto-indexing-azure-blob-storage.md), and [Azure table storage](search-howto-indexing-azure-tables.md).</span></span> <span data-ttu-id="84db8-108">To request support for other data sources, provide your feedback on the [Azure Search feedback forum](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="84db8-108">To request support for other data sources, provide your feedback on the [Azure Search feedback forum](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

## <a name="indexers-and-data-sources"></a><span data-ttu-id="84db8-109">Indexers and data sources</span><span class="sxs-lookup"><span data-stu-id="84db8-109">Indexers and data sources</span></span>

<span data-ttu-id="84db8-110">A **data source** specifies which data to index, credentials for data access, and policies that efficiently identify changes in the data (new, modified, or deleted rows).</span><span class="sxs-lookup"><span data-stu-id="84db8-110">A **data source** specifies which data to index, credentials for data access, and policies that efficiently identify changes in the data (new, modified, or deleted rows).</span></span> <span data-ttu-id="84db8-111">It's defined as an independent resource so that it can be used by multiple indexers.</span><span class="sxs-lookup"><span data-stu-id="84db8-111">It's defined as an independent resource so that it can be used by multiple indexers.</span></span>

<span data-ttu-id="84db8-112">An **indexer** is a resource that connects a single data source with a targeted search index.</span><span class="sxs-lookup"><span data-stu-id="84db8-112">An **indexer** is a resource that connects a single data source with a targeted search index.</span></span> <span data-ttu-id="84db8-113">An indexer is used in the following ways:</span><span class="sxs-lookup"><span data-stu-id="84db8-113">An indexer is used in the following ways:</span></span>

* <span data-ttu-id="84db8-114">Perform a one-time copy of the data to populate an index.</span><span class="sxs-lookup"><span data-stu-id="84db8-114">Perform a one-time copy of the data to populate an index.</span></span>
* <span data-ttu-id="84db8-115">Update an index with changes in the data source on a schedule.</span><span class="sxs-lookup"><span data-stu-id="84db8-115">Update an index with changes in the data source on a schedule.</span></span>
* <span data-ttu-id="84db8-116">Run on-demand to update an index as needed.</span><span class="sxs-lookup"><span data-stu-id="84db8-116">Run on-demand to update an index as needed.</span></span>

<span data-ttu-id="84db8-117">A single indexer can only consume one table or view, but you can create multiple indexers if you want to populate multiple search indexes.</span><span class="sxs-lookup"><span data-stu-id="84db8-117">A single indexer can only consume one table or view, but you can create multiple indexers if you want to populate multiple search indexes.</span></span> <span data-ttu-id="84db8-118">For more information on concepts, see [Indexer Operations: Typical workflow](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).</span><span class="sxs-lookup"><span data-stu-id="84db8-118">For more information on concepts, see [Indexer Operations: Typical workflow](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).</span></span>

<span data-ttu-id="84db8-119">You can set up and configure an Azure SQL indexer using:</span><span class="sxs-lookup"><span data-stu-id="84db8-119">You can set up and configure an Azure SQL indexer using:</span></span>

* <span data-ttu-id="84db8-120">Import Data wizard in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="84db8-120">Import Data wizard in the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="84db8-121">Azure Search [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="84db8-121">Azure Search [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)</span></span>
* <span data-ttu-id="84db8-122">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/indexer-operations)</span><span class="sxs-lookup"><span data-stu-id="84db8-122">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/indexer-operations)</span></span>

<span data-ttu-id="84db8-123">In this article, we'll use the REST API to create **indexers** and **data sources**.</span><span class="sxs-lookup"><span data-stu-id="84db8-123">In this article, we'll use the REST API to create **indexers** and **data sources**.</span></span>

## <a name="when-to-use-azure-sql-indexer"></a><span data-ttu-id="84db8-124">When to use Azure SQL Indexer</span><span class="sxs-lookup"><span data-stu-id="84db8-124">When to use Azure SQL Indexer</span></span>
<span data-ttu-id="84db8-125">Depending on several factors relating to your data, the use of Azure SQL indexer may or may not be appropriate.</span><span class="sxs-lookup"><span data-stu-id="84db8-125">Depending on several factors relating to your data, the use of Azure SQL indexer may or may not be appropriate.</span></span> <span data-ttu-id="84db8-126">If your data fits the following requirements, you can use Azure SQL indexer.</span><span class="sxs-lookup"><span data-stu-id="84db8-126">If your data fits the following requirements, you can use Azure SQL indexer.</span></span>

| <span data-ttu-id="84db8-127">Criteria</span><span class="sxs-lookup"><span data-stu-id="84db8-127">Criteria</span></span> | <span data-ttu-id="84db8-128">Details</span><span class="sxs-lookup"><span data-stu-id="84db8-128">Details</span></span> |
|----------|---------|
| <span data-ttu-id="84db8-129">Data originates from a single table or view</span><span class="sxs-lookup"><span data-stu-id="84db8-129">Data originates from a single table or view</span></span> | <span data-ttu-id="84db8-130">If the data is scattered across multiple tables, you can create a single view of the data.</span><span class="sxs-lookup"><span data-stu-id="84db8-130">If the data is scattered across multiple tables, you can create a single view of the data.</span></span> <span data-ttu-id="84db8-131">However, if you use a view, you won’t be able to use SQL Server integrated change detection to refresh an index with incremental changes.</span><span class="sxs-lookup"><span data-stu-id="84db8-131">However, if you use a view, you won’t be able to use SQL Server integrated change detection to refresh an index with incremental changes.</span></span> <span data-ttu-id="84db8-132">For more information, see [Capturing Changed and Deleted Rows](#CaptureChangedRows) below.</span><span class="sxs-lookup"><span data-stu-id="84db8-132">For more information, see [Capturing Changed and Deleted Rows](#CaptureChangedRows) below.</span></span> |
| <span data-ttu-id="84db8-133">Data types are compatible</span><span class="sxs-lookup"><span data-stu-id="84db8-133">Data types are compatible</span></span> | <span data-ttu-id="84db8-134">Most but not all the SQL types are supported in an Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="84db8-134">Most but not all the SQL types are supported in an Azure Search index.</span></span> <span data-ttu-id="84db8-135">For a list, see [Mapping data types](#TypeMapping).</span><span class="sxs-lookup"><span data-stu-id="84db8-135">For a list, see [Mapping data types](#TypeMapping).</span></span> |
| <span data-ttu-id="84db8-136">Real-time data synchronization is not required</span><span class="sxs-lookup"><span data-stu-id="84db8-136">Real-time data synchronization is not required</span></span> | <span data-ttu-id="84db8-137">An indexer can reindex your table at most every five minutes.</span><span class="sxs-lookup"><span data-stu-id="84db8-137">An indexer can reindex your table at most every five minutes.</span></span> <span data-ttu-id="84db8-138">If your data changes frequently, and the changes need to be reflected in the index within seconds or single minutes, we recommend using the [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) or [.NET SDK](search-import-data-dotnet.md) to push updated rows directly.</span><span class="sxs-lookup"><span data-stu-id="84db8-138">If your data changes frequently, and the changes need to be reflected in the index within seconds or single minutes, we recommend using the [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) or [.NET SDK](search-import-data-dotnet.md) to push updated rows directly.</span></span> |
| <span data-ttu-id="84db8-139">Incremental indexing is possible</span><span class="sxs-lookup"><span data-stu-id="84db8-139">Incremental indexing is possible</span></span> | <span data-ttu-id="84db8-140">If you have a large data set and plan to run the indexer on a schedule, Azure Search must be able to efficiently identify new, changed, or deleted rows.</span><span class="sxs-lookup"><span data-stu-id="84db8-140">If you have a large data set and plan to run the indexer on a schedule, Azure Search must be able to efficiently identify new, changed, or deleted rows.</span></span> <span data-ttu-id="84db8-141">Non-incremental indexing is only allowed if you're indexing on demand (not on schedule), or indexing fewer than 100,000 rows.</span><span class="sxs-lookup"><span data-stu-id="84db8-141">Non-incremental indexing is only allowed if you're indexing on demand (not on schedule), or indexing fewer than 100,000 rows.</span></span> <span data-ttu-id="84db8-142">For more information, see [Capturing Changed and Deleted Rows](#CaptureChangedRows) below.</span><span class="sxs-lookup"><span data-stu-id="84db8-142">For more information, see [Capturing Changed and Deleted Rows](#CaptureChangedRows) below.</span></span> |

> [!NOTE] 
> <span data-ttu-id="84db8-143">Azure Search supports SQL Server authentication only.</span><span class="sxs-lookup"><span data-stu-id="84db8-143">Azure Search supports SQL Server authentication only.</span></span> <span data-ttu-id="84db8-144">If you require support for Azure Active Directory Password authentication, please vote for this [UserVoice suggestion](https://feedback.azure.com/forums/263029-azure-search/suggestions/33595465-support-azure-active-directory-password-authentica).</span><span class="sxs-lookup"><span data-stu-id="84db8-144">If you require support for Azure Active Directory Password authentication, please vote for this [UserVoice suggestion](https://feedback.azure.com/forums/263029-azure-search/suggestions/33595465-support-azure-active-directory-password-authentica).</span></span>

## <a name="create-an-azure-sql-indexer"></a><span data-ttu-id="84db8-145">Create an Azure SQL Indexer</span><span class="sxs-lookup"><span data-stu-id="84db8-145">Create an Azure SQL Indexer</span></span>

1. <span data-ttu-id="84db8-146">Create the data source:</span><span class="sxs-lookup"><span data-stu-id="84db8-146">Create the data source:</span></span>

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2017-11-11
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of the table or view that you want to index" }
    }
   ```

   <span data-ttu-id="84db8-147">You can get the connection string from the [Azure portal](https://portal.azure.com); use the `ADO.NET connection string` option.</span><span class="sxs-lookup"><span data-stu-id="84db8-147">You can get the connection string from the [Azure portal](https://portal.azure.com); use the `ADO.NET connection string` option.</span></span>

2. <span data-ttu-id="84db8-148">Create the target Azure Search index if you don’t have one already.</span><span class="sxs-lookup"><span data-stu-id="84db8-148">Create the target Azure Search index if you don’t have one already.</span></span> <span data-ttu-id="84db8-149">You can create an index using the [portal](https://portal.azure.com) or the [Create Index API](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span><span class="sxs-lookup"><span data-stu-id="84db8-149">You can create an index using the [portal](https://portal.azure.com) or the [Create Index API](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span></span> <span data-ttu-id="84db8-150">Ensure that the schema of your target index is compatible with the schema of the source table - see [mapping between SQL and Azure search data types](#TypeMapping).</span><span class="sxs-lookup"><span data-stu-id="84db8-150">Ensure that the schema of your target index is compatible with the schema of the source table - see [mapping between SQL and Azure search data types](#TypeMapping).</span></span>

3. <span data-ttu-id="84db8-151">Create the indexer by giving it a name and referencing the data source and target index:</span><span class="sxs-lookup"><span data-stu-id="84db8-151">Create the indexer by giving it a name and referencing the data source and target index:</span></span>

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2017-11-11
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

<span data-ttu-id="84db8-152">An indexer created in this way doesn’t have a schedule.</span><span class="sxs-lookup"><span data-stu-id="84db8-152">An indexer created in this way doesn’t have a schedule.</span></span> <span data-ttu-id="84db8-153">It automatically runs once when it’s created.</span><span class="sxs-lookup"><span data-stu-id="84db8-153">It automatically runs once when it’s created.</span></span> <span data-ttu-id="84db8-154">You can run it again at any time using a **run indexer** request:</span><span class="sxs-lookup"><span data-stu-id="84db8-154">You can run it again at any time using a **run indexer** request:</span></span>

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2017-11-11
    api-key: admin-key

<span data-ttu-id="84db8-155">You can customize several aspects of indexer behavior, such as batch size and how many documents can be skipped before an indexer execution fails.</span><span class="sxs-lookup"><span data-stu-id="84db8-155">You can customize several aspects of indexer behavior, such as batch size and how many documents can be skipped before an indexer execution fails.</span></span> <span data-ttu-id="84db8-156">For more information, see [Create Indexer API](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).</span><span class="sxs-lookup"><span data-stu-id="84db8-156">For more information, see [Create Indexer API](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).</span></span>

<span data-ttu-id="84db8-157">You may need to allow Azure services to connect to your database.</span><span class="sxs-lookup"><span data-stu-id="84db8-157">You may need to allow Azure services to connect to your database.</span></span> <span data-ttu-id="84db8-158">See [Connecting From Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for instructions on how to do that.</span><span class="sxs-lookup"><span data-stu-id="84db8-158">See [Connecting From Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for instructions on how to do that.</span></span>

<span data-ttu-id="84db8-159">To monitor the indexer status and execution history (number of items indexed, failures, etc.), use an **indexer status** request:</span><span class="sxs-lookup"><span data-stu-id="84db8-159">To monitor the indexer status and execution history (number of items indexed, failures, etc.), use an **indexer status** request:</span></span>

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2017-11-11
    api-key: admin-key

<span data-ttu-id="84db8-160">The response should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="84db8-160">The response should look similar to the following:</span></span>

    {
        "\@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
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

<span data-ttu-id="84db8-161">Execution history contains up to 50 of the most recently completed executions, which are sorted in the reverse chronological order (so that the latest execution comes first in the response).</span><span class="sxs-lookup"><span data-stu-id="84db8-161">Execution history contains up to 50 of the most recently completed executions, which are sorted in the reverse chronological order (so that the latest execution comes first in the response).</span></span>
<span data-ttu-id="84db8-162">Additional information about the response can be found in [Get Indexer Status](http://go.microsoft.com/fwlink/p/?LinkId=528198)</span><span class="sxs-lookup"><span data-stu-id="84db8-162">Additional information about the response can be found in [Get Indexer Status](http://go.microsoft.com/fwlink/p/?LinkId=528198)</span></span>

## <a name="run-indexers-on-a-schedule"></a><span data-ttu-id="84db8-163">Run indexers on a schedule</span><span class="sxs-lookup"><span data-stu-id="84db8-163">Run indexers on a schedule</span></span>
<span data-ttu-id="84db8-164">You can also arrange the indexer to run periodically on a schedule.</span><span class="sxs-lookup"><span data-stu-id="84db8-164">You can also arrange the indexer to run periodically on a schedule.</span></span> <span data-ttu-id="84db8-165">To do this, add the **schedule** property when creating or updating the indexer.</span><span class="sxs-lookup"><span data-stu-id="84db8-165">To do this, add the **schedule** property when creating or updating the indexer.</span></span> <span data-ttu-id="84db8-166">The example below shows a PUT request to update the indexer:</span><span class="sxs-lookup"><span data-stu-id="84db8-166">The example below shows a PUT request to update the indexer:</span></span>

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2017-11-11
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

<span data-ttu-id="84db8-167">The **interval** parameter is required.</span><span class="sxs-lookup"><span data-stu-id="84db8-167">The **interval** parameter is required.</span></span> <span data-ttu-id="84db8-168">The interval refers to the time between the start of two consecutive indexer executions.</span><span class="sxs-lookup"><span data-stu-id="84db8-168">The interval refers to the time between the start of two consecutive indexer executions.</span></span> <span data-ttu-id="84db8-169">The smallest allowed interval is 5 minutes; the longest is one day.</span><span class="sxs-lookup"><span data-stu-id="84db8-169">The smallest allowed interval is 5 minutes; the longest is one day.</span></span> <span data-ttu-id="84db8-170">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span><span class="sxs-lookup"><span data-stu-id="84db8-170">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span></span> <span data-ttu-id="84db8-171">The pattern for this is: `P(nD)(T(nH)(nM))`.</span><span class="sxs-lookup"><span data-stu-id="84db8-171">The pattern for this is: `P(nD)(T(nH)(nM))`.</span></span> <span data-ttu-id="84db8-172">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span><span class="sxs-lookup"><span data-stu-id="84db8-172">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span></span>

<span data-ttu-id="84db8-173">The optional **startTime** indicates when the scheduled executions should commence.</span><span class="sxs-lookup"><span data-stu-id="84db8-173">The optional **startTime** indicates when the scheduled executions should commence.</span></span> <span data-ttu-id="84db8-174">If it is omitted, the current UTC time is used.</span><span class="sxs-lookup"><span data-stu-id="84db8-174">If it is omitted, the current UTC time is used.</span></span> <span data-ttu-id="84db8-175">This time can be in the past – in which case the first execution is scheduled as if the indexer has been running continuously since the startTime.</span><span class="sxs-lookup"><span data-stu-id="84db8-175">This time can be in the past – in which case the first execution is scheduled as if the indexer has been running continuously since the startTime.</span></span>  

<span data-ttu-id="84db8-176">Only one execution of an indexer can run at a time.</span><span class="sxs-lookup"><span data-stu-id="84db8-176">Only one execution of an indexer can run at a time.</span></span> <span data-ttu-id="84db8-177">If an indexer is running when its execution is scheduled, the execution is postponed until the next scheduled time.</span><span class="sxs-lookup"><span data-stu-id="84db8-177">If an indexer is running when its execution is scheduled, the execution is postponed until the next scheduled time.</span></span>

<span data-ttu-id="84db8-178">Let’s consider an example to make this more concrete.</span><span class="sxs-lookup"><span data-stu-id="84db8-178">Let’s consider an example to make this more concrete.</span></span> <span data-ttu-id="84db8-179">Suppose we the following hourly schedule configured:</span><span class="sxs-lookup"><span data-stu-id="84db8-179">Suppose we the following hourly schedule configured:</span></span>

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

<span data-ttu-id="84db8-180">Here’s what happens:</span><span class="sxs-lookup"><span data-stu-id="84db8-180">Here’s what happens:</span></span>

1. <span data-ttu-id="84db8-181">The first indexer execution starts at or around March 1, 2015 12:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="84db8-181">The first indexer execution starts at or around March 1, 2015 12:00 a.m.</span></span> <span data-ttu-id="84db8-182">UTC.</span><span class="sxs-lookup"><span data-stu-id="84db8-182">UTC.</span></span>
2. <span data-ttu-id="84db8-183">Assume this execution takes 20 minutes (or any time less than 1 hour).</span><span class="sxs-lookup"><span data-stu-id="84db8-183">Assume this execution takes 20 minutes (or any time less than 1 hour).</span></span>
3. <span data-ttu-id="84db8-184">The second execution starts at or around March 1, 2015 1:00 a.m.</span><span class="sxs-lookup"><span data-stu-id="84db8-184">The second execution starts at or around March 1, 2015 1:00 a.m.</span></span>
4. <span data-ttu-id="84db8-185">Now suppose that this execution takes more than an hour – for example, 70 minutes – so that it completes around 2:10 a.m.</span><span class="sxs-lookup"><span data-stu-id="84db8-185">Now suppose that this execution takes more than an hour – for example, 70 minutes – so that it completes around 2:10 a.m.</span></span>
5. <span data-ttu-id="84db8-186">It’s now 2:00 a.m., time for the third execution to start.</span><span class="sxs-lookup"><span data-stu-id="84db8-186">It’s now 2:00 a.m., time for the third execution to start.</span></span> <span data-ttu-id="84db8-187">However, because the second execution from 1 a.m.</span><span class="sxs-lookup"><span data-stu-id="84db8-187">However, because the second execution from 1 a.m.</span></span> <span data-ttu-id="84db8-188">is still running, the third execution is skipped.</span><span class="sxs-lookup"><span data-stu-id="84db8-188">is still running, the third execution is skipped.</span></span> <span data-ttu-id="84db8-189">The third execution starts at 3 a.m.</span><span class="sxs-lookup"><span data-stu-id="84db8-189">The third execution starts at 3 a.m.</span></span>

<span data-ttu-id="84db8-190">You can add, change, or delete a schedule for an existing indexer by using a **PUT indexer** request.</span><span class="sxs-lookup"><span data-stu-id="84db8-190">You can add, change, or delete a schedule for an existing indexer by using a **PUT indexer** request.</span></span>

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a><span data-ttu-id="84db8-191">Capture new, changed, and deleted rows</span><span class="sxs-lookup"><span data-stu-id="84db8-191">Capture new, changed, and deleted rows</span></span>

<span data-ttu-id="84db8-192">Azure Search uses **incremental indexing** to avoid having to reindex the entire table or view every time an indexer runs.</span><span class="sxs-lookup"><span data-stu-id="84db8-192">Azure Search uses **incremental indexing** to avoid having to reindex the entire table or view every time an indexer runs.</span></span> <span data-ttu-id="84db8-193">Azure Search provides two change detection policies to support incremental indexing.</span><span class="sxs-lookup"><span data-stu-id="84db8-193">Azure Search provides two change detection policies to support incremental indexing.</span></span> 

### <a name="sql-integrated-change-tracking-policy"></a><span data-ttu-id="84db8-194">SQL Integrated Change Tracking Policy</span><span class="sxs-lookup"><span data-stu-id="84db8-194">SQL Integrated Change Tracking Policy</span></span>
<span data-ttu-id="84db8-195">If your SQL database supports [change tracking](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), we recommend using **SQL Integrated Change Tracking Policy**.</span><span class="sxs-lookup"><span data-stu-id="84db8-195">If your SQL database supports [change tracking](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), we recommend using **SQL Integrated Change Tracking Policy**.</span></span> <span data-ttu-id="84db8-196">This is the most efficient policy.</span><span class="sxs-lookup"><span data-stu-id="84db8-196">This is the most efficient policy.</span></span> <span data-ttu-id="84db8-197">In addition, it allows Azure Search to identify deleted rows without you having to add an explicit "soft delete" column to your table.</span><span class="sxs-lookup"><span data-stu-id="84db8-197">In addition, it allows Azure Search to identify deleted rows without you having to add an explicit "soft delete" column to your table.</span></span>

#### <a name="requirements"></a><span data-ttu-id="84db8-198">Requirements</span><span class="sxs-lookup"><span data-stu-id="84db8-198">Requirements</span></span> 

+ <span data-ttu-id="84db8-199">Database version requirements:</span><span class="sxs-lookup"><span data-stu-id="84db8-199">Database version requirements:</span></span>
  * <span data-ttu-id="84db8-200">SQL Server 2012 SP3 and later, if you're using SQL Server on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="84db8-200">SQL Server 2012 SP3 and later, if you're using SQL Server on Azure VMs.</span></span>
  * <span data-ttu-id="84db8-201">Azure SQL Database V12, if you're using Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="84db8-201">Azure SQL Database V12, if you're using Azure SQL Database.</span></span>
+ <span data-ttu-id="84db8-202">Tables only (no views).</span><span class="sxs-lookup"><span data-stu-id="84db8-202">Tables only (no views).</span></span> 
+ <span data-ttu-id="84db8-203">On the database, [enable change tracking](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) for the table.</span><span class="sxs-lookup"><span data-stu-id="84db8-203">On the database, [enable change tracking](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) for the table.</span></span> 
+ <span data-ttu-id="84db8-204">No composite primary key (a primary key containing more than one column) on the table.</span><span class="sxs-lookup"><span data-stu-id="84db8-204">No composite primary key (a primary key containing more than one column) on the table.</span></span>  

#### <a name="usage"></a><span data-ttu-id="84db8-205">Usage</span><span class="sxs-lookup"><span data-stu-id="84db8-205">Usage</span></span>

<span data-ttu-id="84db8-206">To use this policy, create or update your data source like this:</span><span class="sxs-lookup"><span data-stu-id="84db8-206">To use this policy, create or update your data source like this:</span></span>

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

<span data-ttu-id="84db8-207">When using SQL integrated change tracking policy, do not specify a separate data deletion detection policy - this policy has built-in support for identifying deleted rows.</span><span class="sxs-lookup"><span data-stu-id="84db8-207">When using SQL integrated change tracking policy, do not specify a separate data deletion detection policy - this policy has built-in support for identifying deleted rows.</span></span> <span data-ttu-id="84db8-208">However, for the deletes to be detected "automagically", the document key in your search index must be the same as the primary key in the SQL table.</span><span class="sxs-lookup"><span data-stu-id="84db8-208">However, for the deletes to be detected "automagically", the document key in your search index must be the same as the primary key in the SQL table.</span></span> 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a><span data-ttu-id="84db8-209">High Water Mark Change Detection policy</span><span class="sxs-lookup"><span data-stu-id="84db8-209">High Water Mark Change Detection policy</span></span>

<span data-ttu-id="84db8-210">This change detection policy relies on a "high water mark" column capturing the version or time when a row was last updated.</span><span class="sxs-lookup"><span data-stu-id="84db8-210">This change detection policy relies on a "high water mark" column capturing the version or time when a row was last updated.</span></span> <span data-ttu-id="84db8-211">If you're using a view, you must use a high water mark policy.</span><span class="sxs-lookup"><span data-stu-id="84db8-211">If you're using a view, you must use a high water mark policy.</span></span> <span data-ttu-id="84db8-212">The high water mark column must meet the following requirements.</span><span class="sxs-lookup"><span data-stu-id="84db8-212">The high water mark column must meet the following requirements.</span></span>

#### <a name="requirements"></a><span data-ttu-id="84db8-213">Requirements</span><span class="sxs-lookup"><span data-stu-id="84db8-213">Requirements</span></span> 

* <span data-ttu-id="84db8-214">All inserts specify a value for the column.</span><span class="sxs-lookup"><span data-stu-id="84db8-214">All inserts specify a value for the column.</span></span>
* <span data-ttu-id="84db8-215">All updates to an item also change the value of the column.</span><span class="sxs-lookup"><span data-stu-id="84db8-215">All updates to an item also change the value of the column.</span></span>
* <span data-ttu-id="84db8-216">The value of this column increases with each insert or update.</span><span class="sxs-lookup"><span data-stu-id="84db8-216">The value of this column increases with each insert or update.</span></span>
* <span data-ttu-id="84db8-217">Queries with the following WHERE and ORDER BY clauses can be executed efficiently: `WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`</span><span class="sxs-lookup"><span data-stu-id="84db8-217">Queries with the following WHERE and ORDER BY clauses can be executed efficiently: `WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="84db8-218">We strongly recommend using the [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) data type for the high water mark column.</span><span class="sxs-lookup"><span data-stu-id="84db8-218">We strongly recommend using the [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) data type for the high water mark column.</span></span> <span data-ttu-id="84db8-219">If any other data type is used, change tracking is not guaranteed to capture all changes in the presence of transactions executing concurrently with an indexer query.</span><span class="sxs-lookup"><span data-stu-id="84db8-219">If any other data type is used, change tracking is not guaranteed to capture all changes in the presence of transactions executing concurrently with an indexer query.</span></span> <span data-ttu-id="84db8-220">When using **rowversion** in a configuration with read-only replicas, you must point the indexer at the primary replica.</span><span class="sxs-lookup"><span data-stu-id="84db8-220">When using **rowversion** in a configuration with read-only replicas, you must point the indexer at the primary replica.</span></span> <span data-ttu-id="84db8-221">Only a primary replica can be used for data sync scenarios.</span><span class="sxs-lookup"><span data-stu-id="84db8-221">Only a primary replica can be used for data sync scenarios.</span></span>

#### <a name="usage"></a><span data-ttu-id="84db8-222">Usage</span><span class="sxs-lookup"><span data-stu-id="84db8-222">Usage</span></span>

<span data-ttu-id="84db8-223">To use a high water mark policy, create or update your data source like this:</span><span class="sxs-lookup"><span data-stu-id="84db8-223">To use a high water mark policy, create or update your data source like this:</span></span>

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
> <span data-ttu-id="84db8-224">If the source table does not have an index on the high water mark column, queries used by the SQL indexer may time out. In particular, the `ORDER BY [High Water Mark Column]` clause requires an index to run efficiently when the table contains many rows.</span><span class="sxs-lookup"><span data-stu-id="84db8-224">If the source table does not have an index on the high water mark column, queries used by the SQL indexer may time out. In particular, the `ORDER BY [High Water Mark Column]` clause requires an index to run efficiently when the table contains many rows.</span></span>
>
>

<span data-ttu-id="84db8-225">If you encounter timeout errors, you can use the `queryTimeout` indexer configuration setting to set the query timeout to a value higher than the default 5-minute timeout.</span><span class="sxs-lookup"><span data-stu-id="84db8-225">If you encounter timeout errors, you can use the `queryTimeout` indexer configuration setting to set the query timeout to a value higher than the default 5-minute timeout.</span></span> <span data-ttu-id="84db8-226">For example, to set the timeout to 10 minutes, create or update the indexer with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="84db8-226">For example, to set the timeout to 10 minutes, create or update the indexer with the following configuration:</span></span>

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

<span data-ttu-id="84db8-227">You can also disable the `ORDER BY [High Water Mark Column]` clause.</span><span class="sxs-lookup"><span data-stu-id="84db8-227">You can also disable the `ORDER BY [High Water Mark Column]` clause.</span></span> <span data-ttu-id="84db8-228">However, this is not recommended because if the indexer execution is interrupted by an error, the indexer has to re-process all rows if it runs later - even if the indexer has already processed almost all the rows by the time it was interrupted.</span><span class="sxs-lookup"><span data-stu-id="84db8-228">However, this is not recommended because if the indexer execution is interrupted by an error, the indexer has to re-process all rows if it runs later - even if the indexer has already processed almost all the rows by the time it was interrupted.</span></span> <span data-ttu-id="84db8-229">To disable the `ORDER BY` clause, use the `disableOrderByHighWaterMarkColumn` setting in the indexer definition:</span><span class="sxs-lookup"><span data-stu-id="84db8-229">To disable the `ORDER BY` clause, use the `disableOrderByHighWaterMarkColumn` setting in the indexer definition:</span></span>  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a><span data-ttu-id="84db8-230">Soft Delete Column Deletion Detection policy</span><span class="sxs-lookup"><span data-stu-id="84db8-230">Soft Delete Column Deletion Detection policy</span></span>
<span data-ttu-id="84db8-231">When rows are deleted from the source table, you probably want to delete those rows from the search index as well.</span><span class="sxs-lookup"><span data-stu-id="84db8-231">When rows are deleted from the source table, you probably want to delete those rows from the search index as well.</span></span> <span data-ttu-id="84db8-232">If you use the SQL integrated change tracking policy, this is taken care of for you.</span><span class="sxs-lookup"><span data-stu-id="84db8-232">If you use the SQL integrated change tracking policy, this is taken care of for you.</span></span> <span data-ttu-id="84db8-233">However, the high water mark change tracking policy doesn’t help you with deleted rows.</span><span class="sxs-lookup"><span data-stu-id="84db8-233">However, the high water mark change tracking policy doesn’t help you with deleted rows.</span></span> <span data-ttu-id="84db8-234">What to do?</span><span class="sxs-lookup"><span data-stu-id="84db8-234">What to do?</span></span>

<span data-ttu-id="84db8-235">If the rows are physically removed from the table, Azure Search has no way to infer the presence of records that no longer exist.</span><span class="sxs-lookup"><span data-stu-id="84db8-235">If the rows are physically removed from the table, Azure Search has no way to infer the presence of records that no longer exist.</span></span>  <span data-ttu-id="84db8-236">However, you can use the “soft-delete” technique to logically delete rows without removing them from the table.</span><span class="sxs-lookup"><span data-stu-id="84db8-236">However, you can use the “soft-delete” technique to logically delete rows without removing them from the table.</span></span> <span data-ttu-id="84db8-237">Add a column to your table or view and mark rows as deleted using that column.</span><span class="sxs-lookup"><span data-stu-id="84db8-237">Add a column to your table or view and mark rows as deleted using that column.</span></span>

<span data-ttu-id="84db8-238">When using the soft-delete technique, you can specify the soft delete policy as follows when creating or updating the data source:</span><span class="sxs-lookup"><span data-stu-id="84db8-238">When using the soft-delete technique, you can specify the soft delete policy as follows when creating or updating the data source:</span></span>

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[the value that indicates that a row is deleted]"
        }
    }

<span data-ttu-id="84db8-239">The **softDeleteMarkerValue** must be a string – use the string representation of your actual value.</span><span class="sxs-lookup"><span data-stu-id="84db8-239">The **softDeleteMarkerValue** must be a string – use the string representation of your actual value.</span></span> <span data-ttu-id="84db8-240">For example, if you have an integer column where deleted rows are marked with the value 1, use `"1"`.</span><span class="sxs-lookup"><span data-stu-id="84db8-240">For example, if you have an integer column where deleted rows are marked with the value 1, use `"1"`.</span></span> <span data-ttu-id="84db8-241">If you have a BIT column where deleted rows are marked with the Boolean true value, use `"True"`.</span><span class="sxs-lookup"><span data-stu-id="84db8-241">If you have a BIT column where deleted rows are marked with the Boolean true value, use `"True"`.</span></span>

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a><span data-ttu-id="84db8-242">Mapping between SQL and Azure Search data types</span><span class="sxs-lookup"><span data-stu-id="84db8-242">Mapping between SQL and Azure Search data types</span></span>
| <span data-ttu-id="84db8-243">SQL data type</span><span class="sxs-lookup"><span data-stu-id="84db8-243">SQL data type</span></span> | <span data-ttu-id="84db8-244">Allowed target index field types</span><span class="sxs-lookup"><span data-stu-id="84db8-244">Allowed target index field types</span></span> | <span data-ttu-id="84db8-245">Notes</span><span class="sxs-lookup"><span data-stu-id="84db8-245">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84db8-246">bit</span><span class="sxs-lookup"><span data-stu-id="84db8-246">bit</span></span> |<span data-ttu-id="84db8-247">Edm.Boolean, Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-247">Edm.Boolean, Edm.String</span></span> | |
| <span data-ttu-id="84db8-248">int, smallint, tinyint</span><span class="sxs-lookup"><span data-stu-id="84db8-248">int, smallint, tinyint</span></span> |<span data-ttu-id="84db8-249">Edm.Int32, Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-249">Edm.Int32, Edm.Int64, Edm.String</span></span> | |
| <span data-ttu-id="84db8-250">bigint</span><span class="sxs-lookup"><span data-stu-id="84db8-250">bigint</span></span> |<span data-ttu-id="84db8-251">Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-251">Edm.Int64, Edm.String</span></span> | |
| <span data-ttu-id="84db8-252">real, float</span><span class="sxs-lookup"><span data-stu-id="84db8-252">real, float</span></span> |<span data-ttu-id="84db8-253">Edm.Double, Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-253">Edm.Double, Edm.String</span></span> | |
| <span data-ttu-id="84db8-254">smallmoney, money decimal numeric</span><span class="sxs-lookup"><span data-stu-id="84db8-254">smallmoney, money decimal numeric</span></span> |<span data-ttu-id="84db8-255">Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-255">Edm.String</span></span> |<span data-ttu-id="84db8-256">Azure Search does not support converting decimal types into Edm.Double because this would lose precision</span><span class="sxs-lookup"><span data-stu-id="84db8-256">Azure Search does not support converting decimal types into Edm.Double because this would lose precision</span></span> |
| <span data-ttu-id="84db8-257">char, nchar, varchar, nvarchar</span><span class="sxs-lookup"><span data-stu-id="84db8-257">char, nchar, varchar, nvarchar</span></span> |<span data-ttu-id="84db8-258">Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-258">Edm.String</span></span><br/><span data-ttu-id="84db8-259">Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="84db8-259">Collection(Edm.String)</span></span> |<span data-ttu-id="84db8-260">A SQL string can be used to populate a Collection(Edm.String) field if the string represents a JSON array of strings: `["red", "white", "blue"]`</span><span class="sxs-lookup"><span data-stu-id="84db8-260">A SQL string can be used to populate a Collection(Edm.String) field if the string represents a JSON array of strings: `["red", "white", "blue"]`</span></span> |
| <span data-ttu-id="84db8-261">smalldatetime, datetime, datetime2, date, datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="84db8-261">smalldatetime, datetime, datetime2, date, datetimeoffset</span></span> |<span data-ttu-id="84db8-262">Edm.DateTimeOffset, Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-262">Edm.DateTimeOffset, Edm.String</span></span> | |
| <span data-ttu-id="84db8-263">uniqueidentifer</span><span class="sxs-lookup"><span data-stu-id="84db8-263">uniqueidentifer</span></span> |<span data-ttu-id="84db8-264">Edm.String</span><span class="sxs-lookup"><span data-stu-id="84db8-264">Edm.String</span></span> | |
| <span data-ttu-id="84db8-265">geography</span><span class="sxs-lookup"><span data-stu-id="84db8-265">geography</span></span> |<span data-ttu-id="84db8-266">Edm.GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="84db8-266">Edm.GeographyPoint</span></span> |<span data-ttu-id="84db8-267">Only geography instances of type POINT with SRID 4326 (which is the default) are supported</span><span class="sxs-lookup"><span data-stu-id="84db8-267">Only geography instances of type POINT with SRID 4326 (which is the default) are supported</span></span> |
| <span data-ttu-id="84db8-268">rowversion</span><span class="sxs-lookup"><span data-stu-id="84db8-268">rowversion</span></span> |<span data-ttu-id="84db8-269">N/A</span><span class="sxs-lookup"><span data-stu-id="84db8-269">N/A</span></span> |<span data-ttu-id="84db8-270">Row-version columns cannot be stored in the search index, but they can be used for change tracking</span><span class="sxs-lookup"><span data-stu-id="84db8-270">Row-version columns cannot be stored in the search index, but they can be used for change tracking</span></span> |
| <span data-ttu-id="84db8-271">time, timespan, binary, varbinary, image, xml, geometry, CLR types</span><span class="sxs-lookup"><span data-stu-id="84db8-271">time, timespan, binary, varbinary, image, xml, geometry, CLR types</span></span> |<span data-ttu-id="84db8-272">N/A</span><span class="sxs-lookup"><span data-stu-id="84db8-272">N/A</span></span> |<span data-ttu-id="84db8-273">Not supported</span><span class="sxs-lookup"><span data-stu-id="84db8-273">Not supported</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="84db8-274">Configuration Settings</span><span class="sxs-lookup"><span data-stu-id="84db8-274">Configuration Settings</span></span>
<span data-ttu-id="84db8-275">SQL indexer exposes several configuration settings:</span><span class="sxs-lookup"><span data-stu-id="84db8-275">SQL indexer exposes several configuration settings:</span></span>

| <span data-ttu-id="84db8-276">Setting</span><span class="sxs-lookup"><span data-stu-id="84db8-276">Setting</span></span> | <span data-ttu-id="84db8-277">Data type</span><span class="sxs-lookup"><span data-stu-id="84db8-277">Data type</span></span> | <span data-ttu-id="84db8-278">Purpose</span><span class="sxs-lookup"><span data-stu-id="84db8-278">Purpose</span></span> | <span data-ttu-id="84db8-279">Default value</span><span class="sxs-lookup"><span data-stu-id="84db8-279">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="84db8-280">queryTimeout</span><span class="sxs-lookup"><span data-stu-id="84db8-280">queryTimeout</span></span> |<span data-ttu-id="84db8-281">string</span><span class="sxs-lookup"><span data-stu-id="84db8-281">string</span></span> |<span data-ttu-id="84db8-282">Sets the timeout for SQL query execution</span><span class="sxs-lookup"><span data-stu-id="84db8-282">Sets the timeout for SQL query execution</span></span> |<span data-ttu-id="84db8-283">5 minutes ("00:05:00")</span><span class="sxs-lookup"><span data-stu-id="84db8-283">5 minutes ("00:05:00")</span></span> |
| <span data-ttu-id="84db8-284">disableOrderByHighWaterMarkColumn</span><span class="sxs-lookup"><span data-stu-id="84db8-284">disableOrderByHighWaterMarkColumn</span></span> |<span data-ttu-id="84db8-285">bool</span><span class="sxs-lookup"><span data-stu-id="84db8-285">bool</span></span> |<span data-ttu-id="84db8-286">Causes the SQL query used by the high water mark policy to omit the ORDER BY clause.</span><span class="sxs-lookup"><span data-stu-id="84db8-286">Causes the SQL query used by the high water mark policy to omit the ORDER BY clause.</span></span> <span data-ttu-id="84db8-287">See [High Water Mark policy](#HighWaterMarkPolicy)</span><span class="sxs-lookup"><span data-stu-id="84db8-287">See [High Water Mark policy](#HighWaterMarkPolicy)</span></span> |<span data-ttu-id="84db8-288">false</span><span class="sxs-lookup"><span data-stu-id="84db8-288">false</span></span> |

<span data-ttu-id="84db8-289">These settings are used in the `parameters.configuration` object in the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="84db8-289">These settings are used in the `parameters.configuration` object in the indexer definition.</span></span> <span data-ttu-id="84db8-290">For example, to set the query timeout to 10 minutes, create or update the indexer with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="84db8-290">For example, to set the query timeout to 10 minutes, create or update the indexer with the following configuration:</span></span>

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a><span data-ttu-id="84db8-291">FAQ</span><span class="sxs-lookup"><span data-stu-id="84db8-291">FAQ</span></span>

<span data-ttu-id="84db8-292">**Q: Can I use Azure SQL indexer with SQL databases running on IaaS VMs in Azure?**</span><span class="sxs-lookup"><span data-stu-id="84db8-292">**Q: Can I use Azure SQL indexer with SQL databases running on IaaS VMs in Azure?**</span></span>

<span data-ttu-id="84db8-293">Yes.</span><span class="sxs-lookup"><span data-stu-id="84db8-293">Yes.</span></span> <span data-ttu-id="84db8-294">However, you need to allow your search service to connect to your database.</span><span class="sxs-lookup"><span data-stu-id="84db8-294">However, you need to allow your search service to connect to your database.</span></span> <span data-ttu-id="84db8-295">For more information, see [Configure a connection from an Azure Search indexer to SQL Server on an Azure VM](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).</span><span class="sxs-lookup"><span data-stu-id="84db8-295">For more information, see [Configure a connection from an Azure Search indexer to SQL Server on an Azure VM](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).</span></span>

<span data-ttu-id="84db8-296">**Q: Can I use Azure SQL indexer with SQL databases running on-premises?**</span><span class="sxs-lookup"><span data-stu-id="84db8-296">**Q: Can I use Azure SQL indexer with SQL databases running on-premises?**</span></span>

<span data-ttu-id="84db8-297">Not directly.</span><span class="sxs-lookup"><span data-stu-id="84db8-297">Not directly.</span></span> <span data-ttu-id="84db8-298">We do not recommend or support a direct connection, as doing so would require you to open your databases to Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="84db8-298">We do not recommend or support a direct connection, as doing so would require you to open your databases to Internet traffic.</span></span> <span data-ttu-id="84db8-299">Customers have succeeded with this scenario using bridge technologies like Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="84db8-299">Customers have succeeded with this scenario using bridge technologies like Azure Data Factory.</span></span> <span data-ttu-id="84db8-300">For more information, see [Push data to an Azure Search index using Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).</span><span class="sxs-lookup"><span data-stu-id="84db8-300">For more information, see [Push data to an Azure Search index using Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).</span></span>

<span data-ttu-id="84db8-301">**Q: Can I use Azure SQL indexer with databases other than SQL Server running in IaaS on Azure?**</span><span class="sxs-lookup"><span data-stu-id="84db8-301">**Q: Can I use Azure SQL indexer with databases other than SQL Server running in IaaS on Azure?**</span></span>

<span data-ttu-id="84db8-302">No.</span><span class="sxs-lookup"><span data-stu-id="84db8-302">No.</span></span> <span data-ttu-id="84db8-303">We don’t support this scenario, because we haven’t tested the indexer with any databases other than SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84db8-303">We don’t support this scenario, because we haven’t tested the indexer with any databases other than SQL Server.</span></span>  

<span data-ttu-id="84db8-304">**Q: Can I create multiple indexers running on a schedule?**</span><span class="sxs-lookup"><span data-stu-id="84db8-304">**Q: Can I create multiple indexers running on a schedule?**</span></span>

<span data-ttu-id="84db8-305">Yes.</span><span class="sxs-lookup"><span data-stu-id="84db8-305">Yes.</span></span> <span data-ttu-id="84db8-306">However, only one indexer can be running on one node at one time.</span><span class="sxs-lookup"><span data-stu-id="84db8-306">However, only one indexer can be running on one node at one time.</span></span> <span data-ttu-id="84db8-307">If you need multiple indexers running concurrently, consider scaling up your search service to more than one search unit.</span><span class="sxs-lookup"><span data-stu-id="84db8-307">If you need multiple indexers running concurrently, consider scaling up your search service to more than one search unit.</span></span>

<span data-ttu-id="84db8-308">**Q: Does running an indexer affect my query workload?**</span><span class="sxs-lookup"><span data-stu-id="84db8-308">**Q: Does running an indexer affect my query workload?**</span></span>

<span data-ttu-id="84db8-309">Yes.</span><span class="sxs-lookup"><span data-stu-id="84db8-309">Yes.</span></span> <span data-ttu-id="84db8-310">Indexer runs on one of the nodes in your search service, and that node’s resources are shared between indexing and serving query traffic and other API requests.</span><span class="sxs-lookup"><span data-stu-id="84db8-310">Indexer runs on one of the nodes in your search service, and that node’s resources are shared between indexing and serving query traffic and other API requests.</span></span> <span data-ttu-id="84db8-311">If you run intensive indexing and query workloads and encounter a high rate of 503 errors or increasing response times, consider [scaling up your search service](search-capacity-planning.md).</span><span class="sxs-lookup"><span data-stu-id="84db8-311">If you run intensive indexing and query workloads and encounter a high rate of 503 errors or increasing response times, consider [scaling up your search service](search-capacity-planning.md).</span></span>

<span data-ttu-id="84db8-312">**Q: Can I use a secondary replica in a [failover cluster](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) as a data source?**</span><span class="sxs-lookup"><span data-stu-id="84db8-312">**Q: Can I use a secondary replica in a [failover cluster](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) as a data source?**</span></span>

<span data-ttu-id="84db8-313">It depends.</span><span class="sxs-lookup"><span data-stu-id="84db8-313">It depends.</span></span> <span data-ttu-id="84db8-314">For full indexing of a table or view, you can use a secondary replica.</span><span class="sxs-lookup"><span data-stu-id="84db8-314">For full indexing of a table or view, you can use a secondary replica.</span></span> 

<span data-ttu-id="84db8-315">For incremental indexing, Azure Search supports two change detection policies: SQL integrated change tracking and High Water Mark.</span><span class="sxs-lookup"><span data-stu-id="84db8-315">For incremental indexing, Azure Search supports two change detection policies: SQL integrated change tracking and High Water Mark.</span></span>

<span data-ttu-id="84db8-316">On read-only replicas, SQL database does not support integrated change tracking.</span><span class="sxs-lookup"><span data-stu-id="84db8-316">On read-only replicas, SQL database does not support integrated change tracking.</span></span> <span data-ttu-id="84db8-317">Therefore, you must use High Water Mark policy.</span><span class="sxs-lookup"><span data-stu-id="84db8-317">Therefore, you must use High Water Mark policy.</span></span> 

<span data-ttu-id="84db8-318">Our standard recommendation is to use the rowversion data type for the high water mark column.</span><span class="sxs-lookup"><span data-stu-id="84db8-318">Our standard recommendation is to use the rowversion data type for the high water mark column.</span></span> <span data-ttu-id="84db8-319">However, using rowversion relies on SQL Database's `MIN_ACTIVE_ROWVERSION` function, which is not supported on read-only replicas.</span><span class="sxs-lookup"><span data-stu-id="84db8-319">However, using rowversion relies on SQL Database's `MIN_ACTIVE_ROWVERSION` function, which is not supported on read-only replicas.</span></span> <span data-ttu-id="84db8-320">Therefore, you must point the indexer to a primary replica if you are using rowversion.</span><span class="sxs-lookup"><span data-stu-id="84db8-320">Therefore, you must point the indexer to a primary replica if you are using rowversion.</span></span>

<span data-ttu-id="84db8-321">If you attempt to use rowversion on a read-only replica, you will see the following error:</span><span class="sxs-lookup"><span data-stu-id="84db8-321">If you attempt to use rowversion on a read-only replica, you will see the following error:</span></span> 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update the datasource and specify a connection to the primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

<span data-ttu-id="84db8-322">**Q: Can I use an alternative, non-rowversion column for high water mark change tracking?**</span><span class="sxs-lookup"><span data-stu-id="84db8-322">**Q: Can I use an alternative, non-rowversion column for high water mark change tracking?**</span></span>

<span data-ttu-id="84db8-323">It's not recommended.</span><span class="sxs-lookup"><span data-stu-id="84db8-323">It's not recommended.</span></span> <span data-ttu-id="84db8-324">Only **rowversion** allows for reliable data synchronization.</span><span class="sxs-lookup"><span data-stu-id="84db8-324">Only **rowversion** allows for reliable data synchronization.</span></span> <span data-ttu-id="84db8-325">However, depending on your application logic, it may be safe if:</span><span class="sxs-lookup"><span data-stu-id="84db8-325">However, depending on your application logic, it may be safe if:</span></span>

+ <span data-ttu-id="84db8-326">You can ensure that when the indexer runs, there are no outstanding transactions on the table that’s being indexed (for example, all table updates happen as a batch on a schedule, and the Azure Search indexer schedule is set to avoid overlapping with the table update schedule).</span><span class="sxs-lookup"><span data-stu-id="84db8-326">You can ensure that when the indexer runs, there are no outstanding transactions on the table that’s being indexed (for example, all table updates happen as a batch on a schedule, and the Azure Search indexer schedule is set to avoid overlapping with the table update schedule).</span></span>  

+ <span data-ttu-id="84db8-327">You periodically do a full reindex to pick up any missed rows.</span><span class="sxs-lookup"><span data-stu-id="84db8-327">You periodically do a full reindex to pick up any missed rows.</span></span> 
