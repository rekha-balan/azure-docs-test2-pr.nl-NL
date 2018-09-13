---
title: Indexing a DocumentDB data source for Azure Search | Microsoft Docs
description: This article shows you how to create an Azure Search indexer with DocumentDB as a data source.
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: ''
ms.service: documentdb
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 04/11/2017
ms.author: eugenesh
ms.openlocfilehash: 5f657ed128103d4bf1304dfc5fae8d86ef950d87
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671272"
---
# <a name="connecting-documentdb-with-azure-search-using-indexers"></a><span data-ttu-id="4ba85-103">Connecting DocumentDB with Azure Search using indexers</span><span class="sxs-lookup"><span data-stu-id="4ba85-103">Connecting DocumentDB with Azure Search using indexers</span></span>

<span data-ttu-id="4ba85-104">If you want to implement a great search experience over your DocumentDB data, you can use an Azure Search indexer to pull data into an Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="4ba85-104">If you want to implement a great search experience over your DocumentDB data, you can use an Azure Search indexer to pull data into an Azure Search index.</span></span> <span data-ttu-id="4ba85-105">In this article, we show you how to integrate Azure DocumentDB with Azure Search without having to write any code to maintain indexing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4ba85-105">In this article, we show you how to integrate Azure DocumentDB with Azure Search without having to write any code to maintain indexing infrastructure.</span></span>

<span data-ttu-id="4ba85-106">To set up a DocumentDB indexer, you must have an [Azure Search service](search-create-service-portal.md), and create an index, datasource, and finally the indexer.</span><span class="sxs-lookup"><span data-stu-id="4ba85-106">To set up a DocumentDB indexer, you must have an [Azure Search service](search-create-service-portal.md), and create an index, datasource, and finally the indexer.</span></span> <span data-ttu-id="4ba85-107">You can create these objects using the [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), or [REST API](/rest/api/searchservice/) for all non-.NET languages.</span><span class="sxs-lookup"><span data-stu-id="4ba85-107">You can create these objects using the [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), or [REST API](/rest/api/searchservice/) for all non-.NET languages.</span></span> 

<span data-ttu-id="4ba85-108">If you opt for the portal, the [Import data wizard](search-import-data-portal.md) guides you through the creation of all these resources.</span><span class="sxs-lookup"><span data-stu-id="4ba85-108">If you opt for the portal, the [Import data wizard](search-import-data-portal.md) guides you through the creation of all these resources.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba85-109">You can launch the **Import data** wizard from the DocumentDB dashboard to simplify indexing for that data source.</span><span class="sxs-lookup"><span data-stu-id="4ba85-109">You can launch the **Import data** wizard from the DocumentDB dashboard to simplify indexing for that data source.</span></span> <span data-ttu-id="4ba85-110">In left-navigation, go to **Collections** > **Add Azure Search** to get started.</span><span class="sxs-lookup"><span data-stu-id="4ba85-110">In left-navigation, go to **Collections** > **Add Azure Search** to get started.</span></span>

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a><span data-ttu-id="4ba85-111">Azure Search indexer concepts</span><span class="sxs-lookup"><span data-stu-id="4ba85-111">Azure Search indexer concepts</span></span>
<span data-ttu-id="4ba85-112">Azure Search supports the creation and management of data sources (including DocumentDB) and indexers that operate against those data sources.</span><span class="sxs-lookup"><span data-stu-id="4ba85-112">Azure Search supports the creation and management of data sources (including DocumentDB) and indexers that operate against those data sources.</span></span>

<span data-ttu-id="4ba85-113">A **data source** specifies the data to index, credentials, and policies for identifying changes in the data (such as modified or deleted documents inside your collection).</span><span class="sxs-lookup"><span data-stu-id="4ba85-113">A **data source** specifies the data to index, credentials, and policies for identifying changes in the data (such as modified or deleted documents inside your collection).</span></span> <span data-ttu-id="4ba85-114">The data source is defined as an independent resource so that it can be used by multiple indexers.</span><span class="sxs-lookup"><span data-stu-id="4ba85-114">The data source is defined as an independent resource so that it can be used by multiple indexers.</span></span>

<span data-ttu-id="4ba85-115">An **indexer** describes how the data flows from your data source into a target search index.</span><span class="sxs-lookup"><span data-stu-id="4ba85-115">An **indexer** describes how the data flows from your data source into a target search index.</span></span> <span data-ttu-id="4ba85-116">An indexer can be used to:</span><span class="sxs-lookup"><span data-stu-id="4ba85-116">An indexer can be used to:</span></span>

* <span data-ttu-id="4ba85-117">Perform a one-time copy of the data to populate an index.</span><span class="sxs-lookup"><span data-stu-id="4ba85-117">Perform a one-time copy of the data to populate an index.</span></span>
* <span data-ttu-id="4ba85-118">Sync an index with changes in the data source on a schedule.</span><span class="sxs-lookup"><span data-stu-id="4ba85-118">Sync an index with changes in the data source on a schedule.</span></span> <span data-ttu-id="4ba85-119">The schedule is part of the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="4ba85-119">The schedule is part of the indexer definition.</span></span>
* <span data-ttu-id="4ba85-120">Invoke on-demand updates to an index as needed.</span><span class="sxs-lookup"><span data-stu-id="4ba85-120">Invoke on-demand updates to an index as needed.</span></span>

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a><span data-ttu-id="4ba85-121">Step 1: Create a data source</span><span class="sxs-lookup"><span data-stu-id="4ba85-121">Step 1: Create a data source</span></span>
<span data-ttu-id="4ba85-122">To create a data source, do a POST:</span><span class="sxs-lookup"><span data-stu-id="4ba85-122">To create a data source, do a POST:</span></span>

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

<span data-ttu-id="4ba85-123">The body of the request contains the data source definition, which should include the following fields:</span><span class="sxs-lookup"><span data-stu-id="4ba85-123">The body of the request contains the data source definition, which should include the following fields:</span></span>

* <span data-ttu-id="4ba85-124">**name**: Choose any name to represent your DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="4ba85-124">**name**: Choose any name to represent your DocumentDB database.</span></span>
* <span data-ttu-id="4ba85-125">**type**: Must be `documentdb`.</span><span class="sxs-lookup"><span data-stu-id="4ba85-125">**type**: Must be `documentdb`.</span></span>
* <span data-ttu-id="4ba85-126">**credentials**:</span><span class="sxs-lookup"><span data-stu-id="4ba85-126">**credentials**:</span></span>
  
  * <span data-ttu-id="4ba85-127">**connectionString**: Required.</span><span class="sxs-lookup"><span data-stu-id="4ba85-127">**connectionString**: Required.</span></span> <span data-ttu-id="4ba85-128">Specify the connection info to your Azure DocumentDB database in the following format: `AccountEndpoint=<DocumentDB endpoint url>;AccountKey=<DocumentDB auth key>;Database=<DocumentDB database id>`</span><span class="sxs-lookup"><span data-stu-id="4ba85-128">Specify the connection info to your Azure DocumentDB database in the following format: `AccountEndpoint=<DocumentDB endpoint url>;AccountKey=<DocumentDB auth key>;Database=<DocumentDB database id>`</span></span>
* <span data-ttu-id="4ba85-129">**container**:</span><span class="sxs-lookup"><span data-stu-id="4ba85-129">**container**:</span></span>
  
  * <span data-ttu-id="4ba85-130">**name**: Required.</span><span class="sxs-lookup"><span data-stu-id="4ba85-130">**name**: Required.</span></span> <span data-ttu-id="4ba85-131">Specify the id of the DocumentDB collection to be indexed.</span><span class="sxs-lookup"><span data-stu-id="4ba85-131">Specify the id of the DocumentDB collection to be indexed.</span></span>
  * <span data-ttu-id="4ba85-132">**query**: Optional.</span><span class="sxs-lookup"><span data-stu-id="4ba85-132">**query**: Optional.</span></span> <span data-ttu-id="4ba85-133">You can specify a query to flatten an arbitrary JSON document into a flat schema that Azure Search can index.</span><span class="sxs-lookup"><span data-stu-id="4ba85-133">You can specify a query to flatten an arbitrary JSON document into a flat schema that Azure Search can index.</span></span>
* <span data-ttu-id="4ba85-134">**dataChangeDetectionPolicy**: Recommended.</span><span class="sxs-lookup"><span data-stu-id="4ba85-134">**dataChangeDetectionPolicy**: Recommended.</span></span> <span data-ttu-id="4ba85-135">See [Indexing Changed Documents](#DataChangeDetectionPolicy) section.</span><span class="sxs-lookup"><span data-stu-id="4ba85-135">See [Indexing Changed Documents](#DataChangeDetectionPolicy) section.</span></span>
* <span data-ttu-id="4ba85-136">**dataDeletionDetectionPolicy**: Optional.</span><span class="sxs-lookup"><span data-stu-id="4ba85-136">**dataDeletionDetectionPolicy**: Optional.</span></span> <span data-ttu-id="4ba85-137">See [Indexing Deleted Documents](#DataDeletionDetectionPolicy) section.</span><span class="sxs-lookup"><span data-stu-id="4ba85-137">See [Indexing Deleted Documents](#DataDeletionDetectionPolicy) section.</span></span>

### <a name="using-queries-to-shape-indexed-data"></a><span data-ttu-id="4ba85-138">Using queries to shape indexed data</span><span class="sxs-lookup"><span data-stu-id="4ba85-138">Using queries to shape indexed data</span></span>
<span data-ttu-id="4ba85-139">You can specify a DocumentDB query to flatten nested properties or arrays, project JSON properties, and filter the data to be indexed.</span><span class="sxs-lookup"><span data-stu-id="4ba85-139">You can specify a DocumentDB query to flatten nested properties or arrays, project JSON properties, and filter the data to be indexed.</span></span> 

<span data-ttu-id="4ba85-140">Example document:</span><span class="sxs-lookup"><span data-stu-id="4ba85-140">Example document:</span></span>

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

<span data-ttu-id="4ba85-141">Filter query:</span><span class="sxs-lookup"><span data-stu-id="4ba85-141">Filter query:</span></span>

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark

<span data-ttu-id="4ba85-142">Flattening query:</span><span class="sxs-lookup"><span data-stu-id="4ba85-142">Flattening query:</span></span>

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark
    
    
<span data-ttu-id="4ba85-143">Projection query:</span><span class="sxs-lookup"><span data-stu-id="4ba85-143">Projection query:</span></span>

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark


<span data-ttu-id="4ba85-144">Array flattening query:</span><span class="sxs-lookup"><span data-stu-id="4ba85-144">Array flattening query:</span></span>

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a><span data-ttu-id="4ba85-145">Step 2: Create an index</span><span class="sxs-lookup"><span data-stu-id="4ba85-145">Step 2: Create an index</span></span>
<span data-ttu-id="4ba85-146">Create a target Azure Search index if you don’t have one already.</span><span class="sxs-lookup"><span data-stu-id="4ba85-146">Create a target Azure Search index if you don’t have one already.</span></span> <span data-ttu-id="4ba85-147">You can create an index using the [Azure portal UI](search-create-index-portal.md), the [Create Index REST API](/rest/api/searchservice/create-index) or [Index class](/dotnet/api/microsoft.azure.search.models.index).</span><span class="sxs-lookup"><span data-stu-id="4ba85-147">You can create an index using the [Azure portal UI](search-create-index-portal.md), the [Create Index REST API](/rest/api/searchservice/create-index) or [Index class](/dotnet/api/microsoft.azure.search.models.index).</span></span>

<span data-ttu-id="4ba85-148">The following example creates an index with an id and description field:</span><span class="sxs-lookup"><span data-stu-id="4ba85-148">The following example creates an index with an id and description field:</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

<span data-ttu-id="4ba85-149">Ensure that the schema of your target index is compatible with the schema of the source JSON documents or the output of your custom query projection.</span><span class="sxs-lookup"><span data-stu-id="4ba85-149">Ensure that the schema of your target index is compatible with the schema of the source JSON documents or the output of your custom query projection.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba85-150">For partitioned collections, the default document key is DocumentDB's `_rid` property, which gets renamed to `rid` in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="4ba85-150">For partitioned collections, the default document key is DocumentDB's `_rid` property, which gets renamed to `rid` in Azure Search.</span></span> <span data-ttu-id="4ba85-151">Also, DocumentDB's `_rid` values contain characters that are invalid in Azure Search keys.</span><span class="sxs-lookup"><span data-stu-id="4ba85-151">Also, DocumentDB's `_rid` values contain characters that are invalid in Azure Search keys.</span></span> <span data-ttu-id="4ba85-152">For this reason, the `_rid` values are Base64 encoded.</span><span class="sxs-lookup"><span data-stu-id="4ba85-152">For this reason, the `_rid` values are Base64 encoded.</span></span>
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a><span data-ttu-id="4ba85-153">Mapping between JSON Data Types and Azure Search Data Types</span><span class="sxs-lookup"><span data-stu-id="4ba85-153">Mapping between JSON Data Types and Azure Search Data Types</span></span>
| <span data-ttu-id="4ba85-154">JSON DATA TYPE</span><span class="sxs-lookup"><span data-stu-id="4ba85-154">JSON DATA TYPE</span></span> | <span data-ttu-id="4ba85-155">COMPATIBLE TARGET INDEX FIELD TYPES</span><span class="sxs-lookup"><span data-stu-id="4ba85-155">COMPATIBLE TARGET INDEX FIELD TYPES</span></span> |
| --- | --- |
| <span data-ttu-id="4ba85-156">Bool</span><span class="sxs-lookup"><span data-stu-id="4ba85-156">Bool</span></span> |<span data-ttu-id="4ba85-157">Edm.Boolean, Edm.String</span><span class="sxs-lookup"><span data-stu-id="4ba85-157">Edm.Boolean, Edm.String</span></span> |
| <span data-ttu-id="4ba85-158">Numbers that look like integers</span><span class="sxs-lookup"><span data-stu-id="4ba85-158">Numbers that look like integers</span></span> |<span data-ttu-id="4ba85-159">Edm.Int32, Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="4ba85-159">Edm.Int32, Edm.Int64, Edm.String</span></span> |
| <span data-ttu-id="4ba85-160">Numbers that look like floating-points</span><span class="sxs-lookup"><span data-stu-id="4ba85-160">Numbers that look like floating-points</span></span> |<span data-ttu-id="4ba85-161">Edm.Double, Edm.String</span><span class="sxs-lookup"><span data-stu-id="4ba85-161">Edm.Double, Edm.String</span></span> |
| <span data-ttu-id="4ba85-162">String</span><span class="sxs-lookup"><span data-stu-id="4ba85-162">String</span></span> |<span data-ttu-id="4ba85-163">Edm.String</span><span class="sxs-lookup"><span data-stu-id="4ba85-163">Edm.String</span></span> |
| <span data-ttu-id="4ba85-164">Arrays of primitive types, for example ["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="4ba85-164">Arrays of primitive types, for example ["a", "b", "c"]</span></span> |<span data-ttu-id="4ba85-165">Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="4ba85-165">Collection(Edm.String)</span></span> |
| <span data-ttu-id="4ba85-166">Strings that look like dates</span><span class="sxs-lookup"><span data-stu-id="4ba85-166">Strings that look like dates</span></span> |<span data-ttu-id="4ba85-167">Edm.DateTimeOffset, Edm.String</span><span class="sxs-lookup"><span data-stu-id="4ba85-167">Edm.DateTimeOffset, Edm.String</span></span> |
| <span data-ttu-id="4ba85-168">GeoJSON objects, for example { "type": "Point", "coordinates": [long, lat] }</span><span class="sxs-lookup"><span data-stu-id="4ba85-168">GeoJSON objects, for example { "type": "Point", "coordinates": [long, lat] }</span></span> |<span data-ttu-id="4ba85-169">Edm.GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="4ba85-169">Edm.GeographyPoint</span></span> |
| <span data-ttu-id="4ba85-170">Other JSON objects</span><span class="sxs-lookup"><span data-stu-id="4ba85-170">Other JSON objects</span></span> |<span data-ttu-id="4ba85-171">N/A</span><span class="sxs-lookup"><span data-stu-id="4ba85-171">N/A</span></span> |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a><span data-ttu-id="4ba85-172">Step 3: Create an indexer</span><span class="sxs-lookup"><span data-stu-id="4ba85-172">Step 3: Create an indexer</span></span>

<span data-ttu-id="4ba85-173">Once the index and data source have been created, you're ready to create the indexer:</span><span class="sxs-lookup"><span data-stu-id="4ba85-173">Once the index and data source have been created, you're ready to create the indexer:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

<span data-ttu-id="4ba85-174">This indexer runs every two hours (schedule interval is set to "PT2H").</span><span class="sxs-lookup"><span data-stu-id="4ba85-174">This indexer runs every two hours (schedule interval is set to "PT2H").</span></span> <span data-ttu-id="4ba85-175">To run an indexer every 30 minutes, set the interval to "PT30M".</span><span class="sxs-lookup"><span data-stu-id="4ba85-175">To run an indexer every 30 minutes, set the interval to "PT30M".</span></span> <span data-ttu-id="4ba85-176">The shortest supported interval is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="4ba85-176">The shortest supported interval is 5 minutes.</span></span> <span data-ttu-id="4ba85-177">The schedule is optional - if omitted, an indexer runs only once when it's created.</span><span class="sxs-lookup"><span data-stu-id="4ba85-177">The schedule is optional - if omitted, an indexer runs only once when it's created.</span></span> <span data-ttu-id="4ba85-178">However, you can run an indexer on-demand at any time.</span><span class="sxs-lookup"><span data-stu-id="4ba85-178">However, you can run an indexer on-demand at any time.</span></span>   

<span data-ttu-id="4ba85-179">For more details on the Create Indexer API, check out [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span><span class="sxs-lookup"><span data-stu-id="4ba85-179">For more details on the Create Indexer API, check out [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span></span>

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a><span data-ttu-id="4ba85-180">Running indexer on-demand</span><span class="sxs-lookup"><span data-stu-id="4ba85-180">Running indexer on-demand</span></span>
<span data-ttu-id="4ba85-181">In addition to running periodically on a schedule, an indexer can also be invoked on demand:</span><span class="sxs-lookup"><span data-stu-id="4ba85-181">In addition to running periodically on a schedule, an indexer can also be invoked on demand:</span></span>

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> <span data-ttu-id="4ba85-182">When Run API returns successfully, the indexer invocation has been scheduled, but the actual processing happens asynchronously.</span><span class="sxs-lookup"><span data-stu-id="4ba85-182">When Run API returns successfully, the indexer invocation has been scheduled, but the actual processing happens asynchronously.</span></span> 

<span data-ttu-id="4ba85-183">You can monitor the indexer status in the portal or using the Get Indexer Status API, which we describe next.</span><span class="sxs-lookup"><span data-stu-id="4ba85-183">You can monitor the indexer status in the portal or using the Get Indexer Status API, which we describe next.</span></span> 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a><span data-ttu-id="4ba85-184">Getting indexer status</span><span class="sxs-lookup"><span data-stu-id="4ba85-184">Getting indexer status</span></span>
<span data-ttu-id="4ba85-185">You can retrieve the status and execution history of an indexer:</span><span class="sxs-lookup"><span data-stu-id="4ba85-185">You can retrieve the status and execution history of an indexer:</span></span>

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

<span data-ttu-id="4ba85-186">The response contains overall indexer status, the last (or in-progress) indexer invocation, and the history of recent indexer invocations.</span><span class="sxs-lookup"><span data-stu-id="4ba85-186">The response contains overall indexer status, the last (or in-progress) indexer invocation, and the history of recent indexer invocations.</span></span>

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

<span data-ttu-id="4ba85-187">Execution history contains up to the 50 most recent completed executions, which are sorted in reverse chronological order (so the latest execution comes first in the response).</span><span class="sxs-lookup"><span data-stu-id="4ba85-187">Execution history contains up to the 50 most recent completed executions, which are sorted in reverse chronological order (so the latest execution comes first in the response).</span></span>

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a><span data-ttu-id="4ba85-188">Indexing changed documents</span><span class="sxs-lookup"><span data-stu-id="4ba85-188">Indexing changed documents</span></span>
<span data-ttu-id="4ba85-189">The purpose of a data change detection policy is to efficiently identify changed data items.</span><span class="sxs-lookup"><span data-stu-id="4ba85-189">The purpose of a data change detection policy is to efficiently identify changed data items.</span></span> <span data-ttu-id="4ba85-190">Currently, the only supported policy is the `High Water Mark` policy using the `_ts` (timestamp) property provided by DocumentDB, which is specified as follows:</span><span class="sxs-lookup"><span data-stu-id="4ba85-190">Currently, the only supported policy is the `High Water Mark` policy using the `_ts` (timestamp) property provided by DocumentDB, which is specified as follows:</span></span>

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

<span data-ttu-id="4ba85-191">Using this policy is highly recommended to ensure good indexer performance.</span><span class="sxs-lookup"><span data-stu-id="4ba85-191">Using this policy is highly recommended to ensure good indexer performance.</span></span> 

<span data-ttu-id="4ba85-192">If you are using a custom query, make sure that the `_ts` property is projected by the query.</span><span class="sxs-lookup"><span data-stu-id="4ba85-192">If you are using a custom query, make sure that the `_ts` property is projected by the query.</span></span> 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a><span data-ttu-id="4ba85-193">Indexing deleted documents</span><span class="sxs-lookup"><span data-stu-id="4ba85-193">Indexing deleted documents</span></span>
<span data-ttu-id="4ba85-194">When rows are deleted from the collection, you normally want to delete those rows from the search index as well.</span><span class="sxs-lookup"><span data-stu-id="4ba85-194">When rows are deleted from the collection, you normally want to delete those rows from the search index as well.</span></span> <span data-ttu-id="4ba85-195">The purpose of a data deletion detection policy is to efficiently identify deleted data items.</span><span class="sxs-lookup"><span data-stu-id="4ba85-195">The purpose of a data deletion detection policy is to efficiently identify deleted data items.</span></span> <span data-ttu-id="4ba85-196">Currently, the only supported policy is the `Soft Delete` policy (deletion is marked with a flag of some sort), which is specified as follows:</span><span class="sxs-lookup"><span data-stu-id="4ba85-196">Currently, the only supported policy is the `Soft Delete` policy (deletion is marked with a flag of some sort), which is specified as follows:</span></span>

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "the property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "the value that identifies a document as deleted"
    }

<span data-ttu-id="4ba85-197">If you are using a custom query, make sure that the property referenced by `softDeleteColumnName` is projected by the query.</span><span class="sxs-lookup"><span data-stu-id="4ba85-197">If you are using a custom query, make sure that the property referenced by `softDeleteColumnName` is projected by the query.</span></span>

<span data-ttu-id="4ba85-198">The following example creates a data source with a soft-deletion policy:</span><span class="sxs-lookup"><span data-stu-id="4ba85-198">The following example creates a data source with a soft-deletion policy:</span></span>

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a><span data-ttu-id="4ba85-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ba85-199">Next steps</span></span>
<span data-ttu-id="4ba85-200">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4ba85-200">Congratulations!</span></span> <span data-ttu-id="4ba85-201">You have learned how to integrate Azure DocumentDB with Azure Search using the indexer for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4ba85-201">You have learned how to integrate Azure DocumentDB with Azure Search using the indexer for DocumentDB.</span></span>

* <span data-ttu-id="4ba85-202">To learn how more about Azure DocumentDB, see the [DocumentDB service page](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="4ba85-202">To learn how more about Azure DocumentDB, see the [DocumentDB service page](https://azure.microsoft.com/services/documentdb/).</span></span>
* <span data-ttu-id="4ba85-203">To learn how more about Azure Search, see the [Search service page](https://azure.microsoft.com/services/search/).</span><span class="sxs-lookup"><span data-stu-id="4ba85-203">To learn how more about Azure Search, see the [Search service page](https://azure.microsoft.com/services/search/).</span></span>