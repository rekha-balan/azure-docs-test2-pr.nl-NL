---
title: Connecting DocumentDB with Azure Search using indexers | Microsoft Docs
description: This article shows you how to use to Azure Search indexer with DocumentDB as a data source.
services: documentdb
documentationcenter: ''
author: mimig1
manager: jhubbard
editor: ''
ms.assetid: fdef3d1d-b814-4161-bdb8-e47d29da596f
ms.service: documentdb
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: mimig
redirect_url: https://docs.microsoft.com/azure/search/search-howto-index-documentdb
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 995b93d60c476f931ce50267af7c46f21e17f8fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540658"
---
# <a name="connecting-documentdb-with-azure-search-using-indexers"></a><span data-ttu-id="03393-103">Connecting DocumentDB with Azure Search using indexers</span><span class="sxs-lookup"><span data-stu-id="03393-103">Connecting DocumentDB with Azure Search using indexers</span></span>
<span data-ttu-id="03393-104">If you're looking to implement great search experiences over your DocumentDB data, use Azure Search indexer for DocumentDB!</span><span class="sxs-lookup"><span data-stu-id="03393-104">If you're looking to implement great search experiences over your DocumentDB data, use Azure Search indexer for DocumentDB!</span></span> <span data-ttu-id="03393-105">In this article, we will show you how to integrate Azure DocumentDB with Azure Search without having to write any code to maintain indexing infrastructure!</span><span class="sxs-lookup"><span data-stu-id="03393-105">In this article, we will show you how to integrate Azure DocumentDB with Azure Search without having to write any code to maintain indexing infrastructure!</span></span>

<span data-ttu-id="03393-106">To set this up, you have to [setup an Azure Search account](../search/search-create-service-portal.md) (you don't need to upgrade to standard search), and then call the [Azure Search REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to create a DocumentDB **data source** and an **indexer** for that data source.</span><span class="sxs-lookup"><span data-stu-id="03393-106">To set this up, you have to [setup an Azure Search account](../search/search-create-service-portal.md) (you don't need to upgrade to standard search), and then call the [Azure Search REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to create a DocumentDB **data source** and an **indexer** for that data source.</span></span>

<span data-ttu-id="03393-107">In order send requests to interact with the REST APIs, you can use [Postman](https://www.getpostman.com/), [Fiddler](http://www.telerik.com/fiddler), or any tool of your preference.</span><span class="sxs-lookup"><span data-stu-id="03393-107">In order send requests to interact with the REST APIs, you can use [Postman](https://www.getpostman.com/), [Fiddler](http://www.telerik.com/fiddler), or any tool of your preference.</span></span>

## <a id="Concepts"></a><span data-ttu-id="03393-108">Azure Search indexer concepts</span><span class="sxs-lookup"><span data-stu-id="03393-108">Azure Search indexer concepts</span></span>
<span data-ttu-id="03393-109">Azure Search supports the creation and management of data sources (including DocumentDB) and indexers that operate against those data sources.</span><span class="sxs-lookup"><span data-stu-id="03393-109">Azure Search supports the creation and management of data sources (including DocumentDB) and indexers that operate against those data sources.</span></span>

<span data-ttu-id="03393-110">A **data source** specifies what data needs to be indexed, credentials to access the data, and policies to enable Azure Search to efficiently identify changes in the data (such as modified or deleted documents inside your collection).</span><span class="sxs-lookup"><span data-stu-id="03393-110">A **data source** specifies what data needs to be indexed, credentials to access the data, and policies to enable Azure Search to efficiently identify changes in the data (such as modified or deleted documents inside your collection).</span></span> <span data-ttu-id="03393-111">The data source is defined as an independent resource so that it can be used by multiple indexers.</span><span class="sxs-lookup"><span data-stu-id="03393-111">The data source is defined as an independent resource so that it can be used by multiple indexers.</span></span>

<span data-ttu-id="03393-112">An **indexer** describes how the data flows from your data source into a target search index.</span><span class="sxs-lookup"><span data-stu-id="03393-112">An **indexer** describes how the data flows from your data source into a target search index.</span></span> <span data-ttu-id="03393-113">You should plan on creating one indexer for every target index and data source combination.</span><span class="sxs-lookup"><span data-stu-id="03393-113">You should plan on creating one indexer for every target index and data source combination.</span></span> <span data-ttu-id="03393-114">While you can have multiple indexers writing into the same index, an indexer can only write into a single index.</span><span class="sxs-lookup"><span data-stu-id="03393-114">While you can have multiple indexers writing into the same index, an indexer can only write into a single index.</span></span> <span data-ttu-id="03393-115">An indexer is used to:</span><span class="sxs-lookup"><span data-stu-id="03393-115">An indexer is used to:</span></span>

* <span data-ttu-id="03393-116">Perform a one-time copy of the data to populate an index.</span><span class="sxs-lookup"><span data-stu-id="03393-116">Perform a one-time copy of the data to populate an index.</span></span>
* <span data-ttu-id="03393-117">Sync an index with changes in the data source on a schedule.</span><span class="sxs-lookup"><span data-stu-id="03393-117">Sync an index with changes in the data source on a schedule.</span></span> <span data-ttu-id="03393-118">The schedule is part of the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="03393-118">The schedule is part of the indexer definition.</span></span>
* <span data-ttu-id="03393-119">Invoke on-demand updates to an index as needed.</span><span class="sxs-lookup"><span data-stu-id="03393-119">Invoke on-demand updates to an index as needed.</span></span>

## <a id="CreateDataSource"></a><span data-ttu-id="03393-120">Step 1: Create a data source</span><span class="sxs-lookup"><span data-stu-id="03393-120">Step 1: Create a data source</span></span>
<span data-ttu-id="03393-121">Issue a HTTP POST request to create a new data source in your Azure Search service, including the following request headers.</span><span class="sxs-lookup"><span data-stu-id="03393-121">Issue a HTTP POST request to create a new data source in your Azure Search service, including the following request headers.</span></span>

    POST https://[Search service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [Search service admin key]

<span data-ttu-id="03393-122">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="03393-122">The `api-version` is required.</span></span> <span data-ttu-id="03393-123">Valid values include `2015-02-28` or a later version.</span><span class="sxs-lookup"><span data-stu-id="03393-123">Valid values include `2015-02-28` or a later version.</span></span> <span data-ttu-id="03393-124">Visit [API versions in Azure Search](../search/search-api-versions.md) to see all supported Search API versions.</span><span class="sxs-lookup"><span data-stu-id="03393-124">Visit [API versions in Azure Search](../search/search-api-versions.md) to see all supported Search API versions.</span></span>

<span data-ttu-id="03393-125">The body of the request contains the data source definition, which should include the following fields:</span><span class="sxs-lookup"><span data-stu-id="03393-125">The body of the request contains the data source definition, which should include the following fields:</span></span>

* <span data-ttu-id="03393-126">**name**: Choose any name to represent your DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="03393-126">**name**: Choose any name to represent your DocumentDB database.</span></span>
* <span data-ttu-id="03393-127">**type**: Use `documentdb`.</span><span class="sxs-lookup"><span data-stu-id="03393-127">**type**: Use `documentdb`.</span></span>
* <span data-ttu-id="03393-128">**credentials**:</span><span class="sxs-lookup"><span data-stu-id="03393-128">**credentials**:</span></span>
  
  * <span data-ttu-id="03393-129">**connectionString**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-129">**connectionString**: Required.</span></span> <span data-ttu-id="03393-130">Specify the connection info to your Azure DocumentDB database in the following format: `AccountEndpoint=<DocumentDB endpoint url>;AccountKey=<DocumentDB auth key>;Database=<DocumentDB database id>`</span><span class="sxs-lookup"><span data-stu-id="03393-130">Specify the connection info to your Azure DocumentDB database in the following format: `AccountEndpoint=<DocumentDB endpoint url>;AccountKey=<DocumentDB auth key>;Database=<DocumentDB database id>`</span></span>
* <span data-ttu-id="03393-131">**container**:</span><span class="sxs-lookup"><span data-stu-id="03393-131">**container**:</span></span>
  
  * <span data-ttu-id="03393-132">**name**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-132">**name**: Required.</span></span> <span data-ttu-id="03393-133">Specify the id of the DocumentDB collection to be indexed.</span><span class="sxs-lookup"><span data-stu-id="03393-133">Specify the id of the DocumentDB collection to be indexed.</span></span>
  * <span data-ttu-id="03393-134">**query**: Optional.</span><span class="sxs-lookup"><span data-stu-id="03393-134">**query**: Optional.</span></span> <span data-ttu-id="03393-135">You can specify a query to flatten an arbitrary JSON document into a flat schema that Azure Search can index.</span><span class="sxs-lookup"><span data-stu-id="03393-135">You can specify a query to flatten an arbitrary JSON document into a flat schema that Azure Search can index.</span></span>
* <span data-ttu-id="03393-136">**dataChangeDetectionPolicy**: Optional.</span><span class="sxs-lookup"><span data-stu-id="03393-136">**dataChangeDetectionPolicy**: Optional.</span></span> <span data-ttu-id="03393-137">See [Data Change Detection Policy](#DataChangeDetectionPolicy) below.</span><span class="sxs-lookup"><span data-stu-id="03393-137">See [Data Change Detection Policy](#DataChangeDetectionPolicy) below.</span></span>
* <span data-ttu-id="03393-138">**dataDeletionDetectionPolicy**: Optional.</span><span class="sxs-lookup"><span data-stu-id="03393-138">**dataDeletionDetectionPolicy**: Optional.</span></span> <span data-ttu-id="03393-139">See [Data Deletion Detection Policy](#DataDeletionDetectionPolicy) below.</span><span class="sxs-lookup"><span data-stu-id="03393-139">See [Data Deletion Detection Policy](#DataDeletionDetectionPolicy) below.</span></span>

<span data-ttu-id="03393-140">See below for an [example request body](#CreateDataSourceExample).</span><span class="sxs-lookup"><span data-stu-id="03393-140">See below for an [example request body](#CreateDataSourceExample).</span></span>

### <a id="DataChangeDetectionPolicy"></a><span data-ttu-id="03393-141">Capturing changed documents</span><span class="sxs-lookup"><span data-stu-id="03393-141">Capturing changed documents</span></span>
<span data-ttu-id="03393-142">The purpose of a data change detection policy is to efficiently identify changed data items.</span><span class="sxs-lookup"><span data-stu-id="03393-142">The purpose of a data change detection policy is to efficiently identify changed data items.</span></span> <span data-ttu-id="03393-143">Currently, the only supported policy is the `High Water Mark` policy using the `_ts` last-modified timestamp property provided by DocumentDB - which is specified as follows:</span><span class="sxs-lookup"><span data-stu-id="03393-143">Currently, the only supported policy is the `High Water Mark` policy using the `_ts` last-modified timestamp property provided by DocumentDB - which is specified as follows:</span></span>

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

<span data-ttu-id="03393-144">You will also need to add `_ts` in the projection and `WHERE` clause for your query.</span><span class="sxs-lookup"><span data-stu-id="03393-144">You will also need to add `_ts` in the projection and `WHERE` clause for your query.</span></span> <span data-ttu-id="03393-145">For example:</span><span class="sxs-lookup"><span data-stu-id="03393-145">For example:</span></span>

    SELECT s.id, s.Title, s.Abstract, s._ts FROM Sessions s WHERE s._ts >= @HighWaterMark

### <a id="DataDeletionDetectionPolicy"></a><span data-ttu-id="03393-146">Capturing deleted documents</span><span class="sxs-lookup"><span data-stu-id="03393-146">Capturing deleted documents</span></span>
<span data-ttu-id="03393-147">When rows are deleted from the source table, you should delete those rows from the search index as well.</span><span class="sxs-lookup"><span data-stu-id="03393-147">When rows are deleted from the source table, you should delete those rows from the search index as well.</span></span> <span data-ttu-id="03393-148">The purpose of a data deletion detection policy is to efficiently identify deleted data items.</span><span class="sxs-lookup"><span data-stu-id="03393-148">The purpose of a data deletion detection policy is to efficiently identify deleted data items.</span></span> <span data-ttu-id="03393-149">Currently, the only supported policy is the `Soft Delete` policy (deletion is marked with a flag of some sort), which is specified as follows:</span><span class="sxs-lookup"><span data-stu-id="03393-149">Currently, the only supported policy is the `Soft Delete` policy (deletion is marked with a flag of some sort), which is specified as follows:</span></span>

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "the property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "the value that identifies a document as deleted"
    }

> [!NOTE]
> <span data-ttu-id="03393-150">You will need to include the softDeleteColumnName property in your SELECT clause if you are using a custom projection.</span><span class="sxs-lookup"><span data-stu-id="03393-150">You will need to include the softDeleteColumnName property in your SELECT clause if you are using a custom projection.</span></span>
> 
> 

### <a id="LeveagingQueries"></a><span data-ttu-id="03393-151">Leveraging Queries</span><span class="sxs-lookup"><span data-stu-id="03393-151">Leveraging Queries</span></span>
<span data-ttu-id="03393-152">In addition to capturing changed and deleted documents, specifying a DocumentDB query can be used to flatten nested properties, unwind arrays, project json properties, and filter the data to be indexed.</span><span class="sxs-lookup"><span data-stu-id="03393-152">In addition to capturing changed and deleted documents, specifying a DocumentDB query can be used to flatten nested properties, unwind arrays, project json properties, and filter the data to be indexed.</span></span> <span data-ttu-id="03393-153">Manipulating the data to be indexed can improve performance of the Azure Search indexer.</span><span class="sxs-lookup"><span data-stu-id="03393-153">Manipulating the data to be indexed can improve performance of the Azure Search indexer.</span></span>

<span data-ttu-id="03393-154">Example Document:</span><span class="sxs-lookup"><span data-stu-id="03393-154">Example Document:</span></span>

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }


<span data-ttu-id="03393-155">Flatten query:</span><span class="sxs-lookup"><span data-stu-id="03393-155">Flatten query:</span></span>

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark
    
    
<span data-ttu-id="03393-156">Projection query:</span><span class="sxs-lookup"><span data-stu-id="03393-156">Projection query:</span></span>

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark


<span data-ttu-id="03393-157">Unwind array query:</span><span class="sxs-lookup"><span data-stu-id="03393-157">Unwind array query:</span></span>

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark
    
    
<span data-ttu-id="03393-158">Filter query:</span><span class="sxs-lookup"><span data-stu-id="03393-158">Filter query:</span></span>

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark


### <a id="CreateDataSourceExample"></a><span data-ttu-id="03393-159">Request body example</span><span class="sxs-lookup"><span data-stu-id="03393-159">Request body example</span></span>
<span data-ttu-id="03393-160">The following example creates a data source with a custom query and policy hints:</span><span class="sxs-lookup"><span data-stu-id="03393-160">The following example creates a data source with a custom query and policy hints:</span></span>

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": {
            "name": "myDocDbCollectionId",
            "query": "SELECT s.id, s.Title, s.Abstract, s._ts FROM Sessions s WHERE s._ts > @HighWaterMark"
        },
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

### <a name="response"></a><span data-ttu-id="03393-161">Response</span><span class="sxs-lookup"><span data-stu-id="03393-161">Response</span></span>
<span data-ttu-id="03393-162">You will receive an HTTP 201 Created response if the data source was successfully created.</span><span class="sxs-lookup"><span data-stu-id="03393-162">You will receive an HTTP 201 Created response if the data source was successfully created.</span></span>

## <a id="CreateIndex"></a><span data-ttu-id="03393-163">Step 2: Create an index</span><span class="sxs-lookup"><span data-stu-id="03393-163">Step 2: Create an index</span></span>
<span data-ttu-id="03393-164">Create a target Azure Search index if you don’t have one already.</span><span class="sxs-lookup"><span data-stu-id="03393-164">Create a target Azure Search index if you don’t have one already.</span></span> <span data-ttu-id="03393-165">You can do this from the [Azure Portal UI](../search/search-create-index-portal.md) or by using the [Create Index API](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span><span class="sxs-lookup"><span data-stu-id="03393-165">You can do this from the [Azure Portal UI](../search/search-create-index-portal.md) or by using the [Create Index API](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span></span>

    POST https://[Search service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [Search service admin key]


<span data-ttu-id="03393-166">Ensure that the schema of your target index is compatible with the schema of the source JSON documents or the output of your custom query projection.</span><span class="sxs-lookup"><span data-stu-id="03393-166">Ensure that the schema of your target index is compatible with the schema of the source JSON documents or the output of your custom query projection.</span></span>

> [!NOTE]
> <span data-ttu-id="03393-167">For partitioned collections, the default document key is DocumentDB's `_rid` property, which gets renamed to `rid` in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="03393-167">For partitioned collections, the default document key is DocumentDB's `_rid` property, which gets renamed to `rid` in Azure Search.</span></span> <span data-ttu-id="03393-168">Also, DocumentDB's `_rid` values contain characters that are invalid in Azure Search keys; therefore, the `_rid` values are Base64 encoded.</span><span class="sxs-lookup"><span data-stu-id="03393-168">Also, DocumentDB's `_rid` values contain characters that are invalid in Azure Search keys; therefore, the `_rid` values are Base64 encoded.</span></span>
> 
> 

### <a name="figure-a-mapping-between-json-data-types-and-azure-search-data-types"></a><span data-ttu-id="03393-169">Figure A: Mapping between JSON Data Types and Azure Search Data Types</span><span class="sxs-lookup"><span data-stu-id="03393-169">Figure A: Mapping between JSON Data Types and Azure Search Data Types</span></span>
| <span data-ttu-id="03393-170">JSON DATA TYPE</span><span class="sxs-lookup"><span data-stu-id="03393-170">JSON DATA TYPE</span></span> | <span data-ttu-id="03393-171">COMPATIBLE TARGET INDEX FIELD TYPES</span><span class="sxs-lookup"><span data-stu-id="03393-171">COMPATIBLE TARGET INDEX FIELD TYPES</span></span> |
| --- | --- |
| <span data-ttu-id="03393-172">Bool</span><span class="sxs-lookup"><span data-stu-id="03393-172">Bool</span></span> |<span data-ttu-id="03393-173">Edm.Boolean, Edm.String</span><span class="sxs-lookup"><span data-stu-id="03393-173">Edm.Boolean, Edm.String</span></span> |
| <span data-ttu-id="03393-174">Numbers that look like integers</span><span class="sxs-lookup"><span data-stu-id="03393-174">Numbers that look like integers</span></span> |<span data-ttu-id="03393-175">Edm.Int32, Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="03393-175">Edm.Int32, Edm.Int64, Edm.String</span></span> |
| <span data-ttu-id="03393-176">Numbers that look like floating-points</span><span class="sxs-lookup"><span data-stu-id="03393-176">Numbers that look like floating-points</span></span> |<span data-ttu-id="03393-177">Edm.Double, Edm.String</span><span class="sxs-lookup"><span data-stu-id="03393-177">Edm.Double, Edm.String</span></span> |
| <span data-ttu-id="03393-178">String</span><span class="sxs-lookup"><span data-stu-id="03393-178">String</span></span> |<span data-ttu-id="03393-179">Edm.String</span><span class="sxs-lookup"><span data-stu-id="03393-179">Edm.String</span></span> |
| <span data-ttu-id="03393-180">Arrays of primitive types e.g. "a", "b", "c"</span><span class="sxs-lookup"><span data-stu-id="03393-180">Arrays of primitive types e.g. "a", "b", "c"</span></span> |<span data-ttu-id="03393-181">Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="03393-181">Collection(Edm.String)</span></span> |
| <span data-ttu-id="03393-182">Strings that look like dates</span><span class="sxs-lookup"><span data-stu-id="03393-182">Strings that look like dates</span></span> |<span data-ttu-id="03393-183">Edm.DateTimeOffset, Edm.String</span><span class="sxs-lookup"><span data-stu-id="03393-183">Edm.DateTimeOffset, Edm.String</span></span> |
| <span data-ttu-id="03393-184">GeoJSON objects e.g. { "type": "Point", "coordinates": [ long, lat ] }</span><span class="sxs-lookup"><span data-stu-id="03393-184">GeoJSON objects e.g. { "type": "Point", "coordinates": [ long, lat ] }</span></span> |<span data-ttu-id="03393-185">Edm.GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="03393-185">Edm.GeographyPoint</span></span> |
| <span data-ttu-id="03393-186">Other JSON objects</span><span class="sxs-lookup"><span data-stu-id="03393-186">Other JSON objects</span></span> |<span data-ttu-id="03393-187">N/A</span><span class="sxs-lookup"><span data-stu-id="03393-187">N/A</span></span> |

### <a id="CreateIndexExample"></a><span data-ttu-id="03393-188">Request body example</span><span class="sxs-lookup"><span data-stu-id="03393-188">Request body example</span></span>
<span data-ttu-id="03393-189">The following example creates an index with an id and description field:</span><span class="sxs-lookup"><span data-stu-id="03393-189">The following example creates an index with an id and description field:</span></span>

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

### <a name="response"></a><span data-ttu-id="03393-190">Response</span><span class="sxs-lookup"><span data-stu-id="03393-190">Response</span></span>
<span data-ttu-id="03393-191">You will receive an HTTP 201 Created response if the index was successfully created.</span><span class="sxs-lookup"><span data-stu-id="03393-191">You will receive an HTTP 201 Created response if the index was successfully created.</span></span>

## <a id="CreateIndexer"></a><span data-ttu-id="03393-192">Step 3: Create an indexer</span><span class="sxs-lookup"><span data-stu-id="03393-192">Step 3: Create an indexer</span></span>
<span data-ttu-id="03393-193">You can create a new indexer within an Azure Search service by using an HTTP POST request with the following headers.</span><span class="sxs-lookup"><span data-stu-id="03393-193">You can create a new indexer within an Azure Search service by using an HTTP POST request with the following headers.</span></span>

    POST https://[Search service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [Search service admin key]

<span data-ttu-id="03393-194">The body of the request contains the indexer definition, which should include the following fields:</span><span class="sxs-lookup"><span data-stu-id="03393-194">The body of the request contains the indexer definition, which should include the following fields:</span></span>

* <span data-ttu-id="03393-195">**name**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-195">**name**: Required.</span></span> <span data-ttu-id="03393-196">The name of the indexer.</span><span class="sxs-lookup"><span data-stu-id="03393-196">The name of the indexer.</span></span>
* <span data-ttu-id="03393-197">**dataSourceName**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-197">**dataSourceName**: Required.</span></span> <span data-ttu-id="03393-198">The name of an existing data source.</span><span class="sxs-lookup"><span data-stu-id="03393-198">The name of an existing data source.</span></span>
* <span data-ttu-id="03393-199">**targetIndexName**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-199">**targetIndexName**: Required.</span></span> <span data-ttu-id="03393-200">The name of an existing index.</span><span class="sxs-lookup"><span data-stu-id="03393-200">The name of an existing index.</span></span>
* <span data-ttu-id="03393-201">**schedule**: Optional.</span><span class="sxs-lookup"><span data-stu-id="03393-201">**schedule**: Optional.</span></span> <span data-ttu-id="03393-202">See [Indexing Schedule](#IndexingSchedule) below.</span><span class="sxs-lookup"><span data-stu-id="03393-202">See [Indexing Schedule](#IndexingSchedule) below.</span></span>

### <a id="IndexingSchedule"></a><span data-ttu-id="03393-203">Running indexers on a schedule</span><span class="sxs-lookup"><span data-stu-id="03393-203">Running indexers on a schedule</span></span>
<span data-ttu-id="03393-204">An indexer can optionally specify a schedule.</span><span class="sxs-lookup"><span data-stu-id="03393-204">An indexer can optionally specify a schedule.</span></span> <span data-ttu-id="03393-205">If a schedule is present, the indexer will run periodically as per schedule.</span><span class="sxs-lookup"><span data-stu-id="03393-205">If a schedule is present, the indexer will run periodically as per schedule.</span></span> <span data-ttu-id="03393-206">Schedule has the following attributes:</span><span class="sxs-lookup"><span data-stu-id="03393-206">Schedule has the following attributes:</span></span>

* <span data-ttu-id="03393-207">**interval**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-207">**interval**: Required.</span></span> <span data-ttu-id="03393-208">A duration value that specifies an interval or period for indexer runs.</span><span class="sxs-lookup"><span data-stu-id="03393-208">A duration value that specifies an interval or period for indexer runs.</span></span> <span data-ttu-id="03393-209">The smallest allowed interval is 5 minutes; the longest is one day.</span><span class="sxs-lookup"><span data-stu-id="03393-209">The smallest allowed interval is 5 minutes; the longest is one day.</span></span> <span data-ttu-id="03393-210">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span><span class="sxs-lookup"><span data-stu-id="03393-210">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span></span> <span data-ttu-id="03393-211">The pattern for this is: `P(nD)(T(nH)(nM))`.</span><span class="sxs-lookup"><span data-stu-id="03393-211">The pattern for this is: `P(nD)(T(nH)(nM))`.</span></span> <span data-ttu-id="03393-212">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span><span class="sxs-lookup"><span data-stu-id="03393-212">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span></span>
* <span data-ttu-id="03393-213">**startTime**: Required.</span><span class="sxs-lookup"><span data-stu-id="03393-213">**startTime**: Required.</span></span> <span data-ttu-id="03393-214">An UTC datetime that specifies when the indexer should start running.</span><span class="sxs-lookup"><span data-stu-id="03393-214">An UTC datetime that specifies when the indexer should start running.</span></span>

### <a id="CreateIndexerExample"></a><span data-ttu-id="03393-215">Request body example</span><span class="sxs-lookup"><span data-stu-id="03393-215">Request body example</span></span>
<span data-ttu-id="03393-216">The following example creates an indexer that copies data from the collection referenced by the `myDocDbDataSource` data source to the `mySearchIndex` index on a schedule that starts on Jan 1, 2015 UTC and runs hourly.</span><span class="sxs-lookup"><span data-stu-id="03393-216">The following example creates an indexer that copies data from the collection referenced by the `myDocDbDataSource` data source to the `mySearchIndex` index on a schedule that starts on Jan 1, 2015 UTC and runs hourly.</span></span>

    {
        "name" : "mysearchindexer",
        "dataSourceName" : "mydocdbdatasource",
        "targetIndexName" : "mysearchindex",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" }
    }

### <a name="response"></a><span data-ttu-id="03393-217">Response</span><span class="sxs-lookup"><span data-stu-id="03393-217">Response</span></span>
<span data-ttu-id="03393-218">You will receive an HTTP 201 Created response if the indexer was successfully created.</span><span class="sxs-lookup"><span data-stu-id="03393-218">You will receive an HTTP 201 Created response if the indexer was successfully created.</span></span>

## <a id="RunIndexer"></a><span data-ttu-id="03393-219">Step 4: Run an indexer</span><span class="sxs-lookup"><span data-stu-id="03393-219">Step 4: Run an indexer</span></span>
<span data-ttu-id="03393-220">In addition to running periodically on a schedule, an indexer can also be invoked on demand by issuing the following HTTP POST request:</span><span class="sxs-lookup"><span data-stu-id="03393-220">In addition to running periodically on a schedule, an indexer can also be invoked on demand by issuing the following HTTP POST request:</span></span>

    POST https://[Search service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [Search service admin key]

### <a name="response"></a><span data-ttu-id="03393-221">Response</span><span class="sxs-lookup"><span data-stu-id="03393-221">Response</span></span>
<span data-ttu-id="03393-222">You will receive an HTTP 202 Accepted response if the indexer was successfully invoked.</span><span class="sxs-lookup"><span data-stu-id="03393-222">You will receive an HTTP 202 Accepted response if the indexer was successfully invoked.</span></span>

## <a name="GetIndexerStatus"></a><span data-ttu-id="03393-223">Step 5: Get indexer status</span><span class="sxs-lookup"><span data-stu-id="03393-223">Step 5: Get indexer status</span></span>
<span data-ttu-id="03393-224">You can issue a HTTP GET request to retrieve the current status and execution history of an indexer:</span><span class="sxs-lookup"><span data-stu-id="03393-224">You can issue a HTTP GET request to retrieve the current status and execution history of an indexer:</span></span>

    GET https://[Search service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [Search service admin key]

### <a name="response"></a><span data-ttu-id="03393-225">Response</span><span class="sxs-lookup"><span data-stu-id="03393-225">Response</span></span>
<span data-ttu-id="03393-226">You will see a HTTP 200 OK response returned along with a response body that contains information about overall indexer health status, the last indexer invocation, as well as the history of recent indexer invocations (if present).</span><span class="sxs-lookup"><span data-stu-id="03393-226">You will see a HTTP 200 OK response returned along with a response body that contains information about overall indexer health status, the last indexer invocation, as well as the history of recent indexer invocations (if present).</span></span>

<span data-ttu-id="03393-227">The response should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="03393-227">The response should look similar to the following:</span></span>

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

<span data-ttu-id="03393-228">Execution history contains up to the 50 most recent completed executions, which are sorted in reverse chronological order (so the latest execution comes first in the response).</span><span class="sxs-lookup"><span data-stu-id="03393-228">Execution history contains up to the 50 most recent completed executions, which are sorted in reverse chronological order (so the latest execution comes first in the response).</span></span>

## <a name="NextSteps"></a><span data-ttu-id="03393-229">Next steps</span><span class="sxs-lookup"><span data-stu-id="03393-229">Next steps</span></span>
<span data-ttu-id="03393-230">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="03393-230">Congratulations!</span></span> <span data-ttu-id="03393-231">You have just learned how to integrate Azure DocumentDB with Azure Search using the indexer for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="03393-231">You have just learned how to integrate Azure DocumentDB with Azure Search using the indexer for DocumentDB.</span></span>

* <span data-ttu-id="03393-232">To learn how more about Azure DocumentDB, see the [DocumentDB service page](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="03393-232">To learn how more about Azure DocumentDB, see the [DocumentDB service page](https://azure.microsoft.com/services/documentdb/).</span></span>
* <span data-ttu-id="03393-233">To learn how more about Azure Search, see the [Search service page](https://azure.microsoft.com/services/search/).</span><span class="sxs-lookup"><span data-stu-id="03393-233">To learn how more about Azure Search, see the [Search service page](https://azure.microsoft.com/services/search/).</span></span>

